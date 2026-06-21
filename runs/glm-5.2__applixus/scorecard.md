# Scorecard — glm-5.2 · applixus

| Alan | Değer |
|---|---|
| Model | **glm-5.2** |
| Site | applixus (https://www.applixus.com) |
| Deploy | https://glm-5-2.applixus.com/ |
| Run | `glm-5.2__applixus` |
| Tarih | 2026-06-21 (3-run yeniden skorlama) |
| Puanlayan | Codex (nötr, codex-cli 0.136.0, **3 bağımsız run**) + PageSpeed (kullanıcı ölçümü) |
| Maliyet | **$11.09** (glm-5.2 rebuild — OpenRouter / z-ai/glm-5.2) |

## Skorlar (3-run medyan)

| Kategori | Puan | Puanlayan |
|---|---:|---|
| Teknik kalite (SEO + mobil-uyum + a11y) | **80** | Codex |
| PageSpeed çıktıları | **98** | Sen (Lighthouse, Performans) |
| UI kalitesi (estetik + görsel sadakat) | **56** | Codex |
| Kod okunabilirliği | **82** | Codex |

> **Composite:** `(80 + 98 + 56 + 82) / 4` = **79.0 / 100** (medyan run = run3; eşit ağırlık %25).
> ⚖️ **opus vs glm composite ≈ istatistiksel beraberlik** (opus 78.5–81.0 · glm 77.0–79.75, aralıklar örtüşüyor). UI ekseninde opus önde.

## 3-run dağılımı (Codex, nötr)

| Run | Teknik | UI | Okunabilirlik | Composite* |
|---|---:|---:|---:|---:|
| 1 | 78 | 50 | 82 | 77.0 |
| 2 | 82 | 55 | 84 | 79.75 |
| 3 *(medyan, kanonik)* | 80 | 56 | 82 | **79.0** |
| **Medyan** | **80** | **55** | **82** | **79.0** |
| **Aralık** | 78–82 | **50–56** | 82–84 | 77.0–79.75 |

\* Composite = `(teknik + 98 + ui + okunabilirlik) / 4`. Kanonik scorecard.json = **run3** (medyan run, içsel tutarlı).

> **UI gözlemi:** glm UI 3 run'ın hepsinde **50–56** bandında; opus UI **58–64** bandında → aralıklar **örtüşmüyor**, opus görsel sadakatte her üç run'da daha yüksek. glm'in dark/indigo SVG estetiği kendi içinde cilalı, fakat referansın siyah/kırmızı + X motifi + fotoğraflı kart diline glm de opus da uzak. (n=3; eğilim, kesin hüküm değil.)

## PageSpeed çıktıları — 98

Kaynak: Google PageSpeed Insights / Lighthouse, 21 Haz 2026 19:00. Benchmark PageSpeed kategorisi
= **Performans** skoru (SEO/a11y/best-practices zaten Teknik kategoride sayıldığı için çift sayım yapılmaz).
Tek skor = mobil Performans (opus-4.8 ile aynı mobil-birincil yöntem).

| Lighthouse kategorisi | Mobil | Masaüstü |
|---|---:|---:|
| **Performans** (PageSpeed skoru) | **98** | **99** |
| Erişilebilirlik | 94 | 93 |
| En İyi Uygulamalar | 100 | 100 |
| SEO | 100 | 100 |

**Core Web Vitals:** FCP 0,8 sn · LCP 0,9 sn · TBT 0 ms · CLS 0 · Speed Index 3,8 sn (mobil) / FCP 0,2 sn · LCP 0,3 sn · TBT 0 ms · CLS 0,072 · Speed Index 1,1 sn (masaüstü).

## Teknik kalite — 80 (medyan run)

**Gerekçe:** SEO ve semantik HTML güçlü; iki sayfada viewport, title, description, OG/Twitter, canonical, tek H1, alt metinler, header/nav/main/footer ve responsive breakpoint'ler var. Ana zayıflık gerçek bağlantı doğruluğu: apps sayfasındaki store/web CTA'larının çoğu placeholder `href="#"`, bazı footer ürün linkleri de sayfa içi anlamsız hedeflere gidiyor.

- İçerik `specs/applixus/reference/content.md` ile büyük ölçüde uyumlu: anasayfa bölümleri, iletişim bilgileri, web ürünleri ve öne çıkan mobil uygulamalar korunmuş.
- SEO temeli iyi: title/description, canonical, OpenGraph, Twitter card ve görsel alt metinleri mevcut.
- Mobil uyum iyi planlanmış: 1024/760/375px breakpoint'leri, tek kolon mobil kart düzeni, görünür focus ve `prefers-reduced-motion` desteği var.
- Apps sayfasında çok sayıda `href="#"` placeholder link var; bu kırık/yanıltıcı ürün ve store linki etkisi yaratıyor.
- Graphify talimatındaki `graphify-out/GRAPH_REPORT.md` bu checkout'ta yoktu; `graphify-out` boş olduğu için mimari grafikten doğrulama yapılamadı.

## UI kalitesi — 56 (medyan run)

**Gerekçe:** Rebuild kendi içinde temiz, okunaklı ve mobilde düzenli; fakat referans tasarıma görsel sadakat zayıf. Referans ekranlar siyah/kırmızı, güçlü X motifli, fotoğraf ve büyük medya kartlı bir dil kullanırken rebuild mor/mavi gradient, SVG placeholder ve kompakt ikon-kart estetiğine kaymış.

- Anasayfa içerik sırası referansa benziyor, ancak hero görseli, kırmızı X marka sinyali, siyah/kırmızı palet ve fotoğraflı about bölümü belirgin şekilde farklı.
- Uygulamalar sayfasında referanstaki büyük görsel kapaklı kartlar yerine küçük ikonlu mor kartlar kullanılmış; bu sayfa görsel sadakati en çok düşüren bölüm.
- Mobil render düzeni genel olarak okunaklı ve taşma göstermiyor; kartlar tek kolona düzgün iniyor.
- Tipografi, spacing ve kart hiyerarşisi modern ve tutarlı, fakat marka karakteri referansa göre fazla jenerik SaaS/purple-dashboard hissi veriyor.
- Logo, CTA vurguları, footer ve referans markalar bölümü referanstaki kırmızı aksanlı görsel dili yakalamıyor.

## Kod okunabilirliği — 82 (medyan run)

**Gerekçe:** Kod sade statik HTML/CSS/JS olarak ayrılmış, class isimleri anlamlı, CSS değişkenleri ve bölümlenmiş yorumlar okunabilirliği artırıyor. Bakım maliyetini artıran taraflar tekrar eden header/footer ve elle çoğaltılmış app kartları.

- Dosya organizasyonu net: `index.html`, `apps.html`, ortak `assets/styles.css`, `assets/app.js` ve SVG varlıkları ayrılmış.
- CSS değişkenleri, bölüm başlıkları ve responsive bloklar düzenli; başka geliştiricinin takip etmesi kolay.
- JavaScript kısa ve sınırlı sorumlulukta: sticky header, mobil nav ve FAQ davranışı okunur biçimde yazılmış.
- Header/footer iki HTML dosyasında tekrar edilmiş; statik projede kabul edilebilir ama değişiklikte çift bakım riski yaratıyor.
- Apps kartları veri kaynağı olmadan elle tekrarlanmış; içerik ekleme/güncelleme sürdürülebilirliği orta seviyede.

## Durum

✅ **Tamamlandı (3-run yeniden skorlama).** Dört kategori puanlandı; PageSpeed `done`, composite **79.0/100**.
Ham 3-run örnekleri: [`rescore/`](rescore/) · önceki tek-run: [`scorecard.prev.md`](scorecard.prev.md) · karşılaştırma: [`runs/rescore-analysis.json`](../rescore-analysis.json).
