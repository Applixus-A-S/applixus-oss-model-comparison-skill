# LLM UX Benchmark — Puanlama Rubriği (Tek Kaynak)

> Bu dosya benchmark'ın **standartlarını** tanımlar. Codex puanlamayı bu dosyayı okuyarak yapar.
> Ağırlıklar burada tek noktada tutulur — değiştirmek için **yalnız bu dosyayı** düzenle.

## Genel kurallar

- Her kategori **0–100** tam sayı puanlanır.
- Puanlama **kanıta dayalı** olmalı: her kategori için kısa gerekçe (`rationale`) + somut bulgu listesi (`findings`).
- Tutarlılık için şu bantları kullan:
  - **90–100** mükemmel, kusursuza yakın
  - **75–89** iyi, küçük eksikler
  - **60–74** orta, belirgin eksikler
  - **40–59** zayıf, çok sayıda sorun
  - **0–39** yetersiz / kırık

## Kategoriler

### 1) Teknik kalite (0–100)
- Semantik HTML (doğru etiketler, landmark'lar: `header`/`nav`/`main`/`footer`).
- **SEO uyumu:** `<title>`, `<meta name="description">`, OpenGraph + Twitter card, tek `<h1>` ve tutarlı heading hiyerarşisi, tüm görsellerde `alt`, `<link rel="canonical">`, anlamlı anchor metinleri.
- **Mobil-uyum / responsive:** `<meta name="viewport">`, breakpoint'ler, mobilde yatay-scroll/taşma yok, dokunma hedefleri yeterli büyüklükte.
- Erişilebilirlik (a11y): renk kontrastı, görünür focus, form etiketleri, gerektiğinde ARIA.
- Doğruluk: kırık link/asset yok, konsol hatası yok, geçerli markup.

### 2) PageSpeed çıktıları (0–100) — MANUEL
- **Codex bu kategoriyi puanlamaz.** Kullanıcı siteyi deploy edip Google PageSpeed / Lighthouse ile ölçer ve puanı `/llm-ux-benchmark:score <run> --pagespeed N` ile girer.
- Codex çıktısında `pagespeed.status = "pending"` ve `pagespeed.score = null` bırakılır.

### 3) UI kalitesi (0–100)
- **Estetik / göze hoşluk:** kompozisyon, görsel hiyerarşi, denge, cila.
- **Görsel sadakat:** rebuild'in render ekran görüntüleri (anasayfa + uygulamalar) referans tasarım ekran görüntülerine ne kadar yakın.
- Layout & boşluk: spacing, hizalama, grid tutarlılığı.
- Tipografi (ölçek, satır yüksekliği, okunabilirlik) + renk paleti tutarlılığı.
- **Mobil görünüm:** render ekran görüntülerinde mobil düzen düzgün mü.
- Codex bunu eklenen ekran görüntüleri (`-i`) üzerinden **görsel** değerlendirir.

### 4) Kod okunabilirliği (0–100)
- Dosya/klasör organizasyonu ve sorumluluk ayrımı (HTML / CSS / JS).
- İsimlendirme (class, id, değişken) anlamlı ve tutarlı.
- Modülerlik, tekrar yok (DRY), tutarlı biçimlendirme.
- Sürdürülebilirlik: başka bir geliştirici kolayca değiştirebilir mi.

## Bileşik (composite) skor

```
composite = (teknik + pagespeed + ui + okunabilirlik) / 4      (eşit ağırlık, her biri %25)
```

- Ağırlıklar eşit. Farklı ağırlık istersen bu formülü güncelle (örn. PageSpeed ağırlıklı: `0.2·teknik + 0.4·pagespeed + 0.2·ui + 0.2·okunabilirlik`).
- PageSpeed henüz girilmemişse (`pending`) composite **kısmi**'dir: mevcut 3 kategorinin ortalaması alınır ve `composite_partial` işaretlenir. PageSpeed girilince tam composite hesaplanır.

## Çoklu-run ve yeniden skorlama protokolü (BAĞLAYICI)

> Codex bir LLM-yargıçtır; tek run **gürültülüdür**. (Gerçek örnek: opus-4.8 tek-run UI=53 bir düşük
> outlier'dı; 3 run'da UI 58–64 çıktı ve opus↔glm sıralaması ters döndü.) Bu yüzden:

- **N ≥ 3 bağımsız Codex run.** Her kategori için **medyan** kanonik değerdir; **aralık** (min–max) raporlanır.
  Kanonik `scorecard.json` = composite'i medyana en yakın olan **temsilci run** (birebir; rationale/findings
  o run'dan, Frankenstein içerik yok). `scorecard.md` tam N-run tablosunu + medyan + aralık gösterir.
  N=3 **alt sınırdır**; varyans büyükse (ör. tek kategori aralığı ≥10 puan) run sayısını artır.
- **Hiçbir model sabit baseline DEĞİLDİR.** Yeni bir model eklendiğinde **mevcut tüm modeller aynı batch'te,
  aynı Codex sürümüyle yeniden skorlanır** — eski modellerin tek-run skorları dondurulup taşınmaz. Bu, hem
  tek-run gürültüsünü hem de judge-sürüm kaymasını eler (elma-elmaya kıyas). Ham run'lar `runs/<run>/rescore/`
  + özet `runs/rescore-analysis.json` olarak commit edilir (tekrarlanabilirlik kanıtı).
- **İstatistiksel beraberlik:** İki modelin composite **aralıkları örtüşüyorsa** leaderboard'da "≈ beraberlik"
  notu düşülür; medyan farkı "net kazanan" gibi sunulmaz. Kategori bazında örtüşmeyen aralık (ör. UI) ayrı belirtilir.
