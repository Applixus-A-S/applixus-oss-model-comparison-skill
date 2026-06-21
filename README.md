# llm-ux-benchmark

Applixus'un açık **LLM UX benchmark**'ı. Bir LLM'e gerçek bir görev verir — *verilen siteyi sıfırdan
yeniden kodla* — ve sonucu standart bir rubriğe göre puanlar. Amaç: "hangi model daha iyi?" değil,
**"hangi model hangi iş için daha uygun?"** sorusuna şeffaf cevap.

İlk test konuğu: **GLM 5.2**.

## Nasıl çalışır

1. **`/llm-ux-benchmark:rebuild <model> <url> [site-slug]`** — Aktif backend model siteyi sıfırdan
   **vanilla static** (HTML/CSS/JS, build yok) olarak yeniden kodlar. İlk çalıştırmada bir **spec**
   oluşturur: sabit brief (SEO-uyumlu + estetik + mobil-uyumlu), senden orijinal sitenin tasarım
   ekran görüntülerini ister, URL içeriğini indeksler. Spec tüm modeller arasında **paylaşılır**.
2. **`/llm-ux-benchmark:score <model>__<site> [--pagespeed N]`** — Puanlamayı **tamamıyla Codex**
   (nötr yargıç) yapar. Codex senden rebuild'in **anasayfa + uygulamalar** render ekran görüntülerini
   ister, sonra 0-100 puanlar. PageSpeed'i sen deploy sonrası ölçer, `--pagespeed N` ile girersin.
3. **`/llm-ux-benchmark:compare [site-slug]`** — Tüm scorecard'ları model karşılaştırma tablosuna
   (leaderboard) çevirir.

## Değerlendirme başlıkları (her biri 0–100)

| Kategori | Puanlayan |
|---|---|
| Teknik kalite (SEO + mobil-uyum + a11y dahil) | Codex |
| PageSpeed çıktıları | **Sen** (deploy sonrası ölç, `--pagespeed N`) |
| UI kalitesi (estetik + görsel sadakat) | Codex (render ekran görüntülerinden) |
| Kod okunabilirliği | Codex |

Rubrik ve ağırlıklar tek kaynakta: [`lib/RUBRIC.md`](lib/RUBRIC.md). Bileşik skor = 4 kategorinin
eşit ağırlıklı ortalaması (değiştirilebilir).

## 🏆 Sonuçlar (Leaderboard)

Site: **applixus** — referans: <https://www.applixus.com>

| Model | Teknik | PageSpeed | UI | Okunabilirlik | **Composite** | Detay |
|---|---:|---:|---:|---:|---:|---|
| [**opus-4.8**](runs/opus-4.8__applixus/scorecard.md) | 78 | 98 | 58 | 84 | **79.5** | [scorecard](runs/opus-4.8__applixus/scorecard.md) · [canlı demo](https://opus4-8.applixus.com/) |
| [**glm-5.2**](runs/glm-5.2__applixus/scorecard.md) | 80 | 98 | 56 | 82 | **79.0** | [scorecard](runs/glm-5.2__applixus/scorecard.md) · [canlı demo](https://glm-5-2.applixus.com/) |

> ⚖️ **opus-4.8 ≈ glm-5.2 — istatistiksel beraberlik.** Skorlar **3 bağımsız Codex run'ının medyanı** (LLM-yargıç gürültüsünü
> azaltmak için). Composite aralıkları örtüşüyor: opus **78.5–81.0** · glm **77.0–79.75** → opus medyanda 0,5 puan önde.
> **UI ekseninde** opus 3 run'da **58–64**, glm **50–56** (örtüşmeyen) → opus görsel sadakatte her run'da tutarlı şekilde daha yüksek.
> İlk yayındaki tek-run tablo (glm 79.75 / opus 77.75) gürültüydü: şanslı-yüksek glm örneği vs şanssız-düşük opus UI (53,
> yeni 3 run'ın hepsinin altında); medyan bu şansı eler. Ham örnekler: [`runs/rescore-analysis.json`](runs/rescore-analysis.json).

> **opus-4.8** · composite **79.5/100** = `(78 + 98 + 58 + 84) / 4` (medyan run). PageSpeed = Lighthouse Performans
> (mobil **98** / masaüstü **98**; SEO 100, En İyi Uygulamalar 100, Erişilebilirlik 96/95).
> Teknik/UI/Okunabilirlik = Codex (nötr, 3-run medyan). Gerekçe + 3-run dağılımı: [scorecard.md](runs/opus-4.8__applixus/scorecard.md).
> Canlı demo: <https://opus4-8.applixus.com/> · rebuild kaynağı: [`runs/opus-4.8__applixus/site/`](runs/opus-4.8__applixus/site/).

> **glm-5.2** · composite **79.0/100** = `(80 + 98 + 56 + 82) / 4` (medyan run). PageSpeed = Lighthouse Performans
> (mobil **98** / masaüstü **99**; SEO 100, En İyi Uygulamalar 100, Erişilebilirlik 94/93).
> Teknik/UI/Okunabilirlik = Codex (nötr, 3-run medyan). Maliyet: **$11.09**. Gerekçe + 3-run dağılımı: [scorecard.md](runs/glm-5.2__applixus/scorecard.md).
> Canlı demo: <https://glm-5-2.applixus.com/> · rebuild kaynağı: [`runs/glm-5.2__applixus/site/`](runs/glm-5.2__applixus/site/).

## Örnek kullanım

```
# 1) İlk model — spec oluşur (tasarım ekran görüntüsü ister) + rebuild
/llm-ux-benchmark:rebuild opus-4.8 https://www.applixus.com applixus

# 2) Codex puanlama (render ekran görüntüsü ister)
/llm-ux-benchmark:score opus-4.8__applixus

# 3) Deploy + PageSpeed ölç → puanı gir
/llm-ux-benchmark:score opus-4.8__applixus --pagespeed 94

# 4) İkinci model (GLM 5.2'yi claude-code-router ile backend yap) — aynı spec
/llm-ux-benchmark:rebuild glm-5.2 https://www.applixus.com applixus
/llm-ux-benchmark:score   glm-5.2__applixus
/llm-ux-benchmark:score   glm-5.2__applixus --pagespeed 90

# 5) Karşılaştır
/llm-ux-benchmark:compare applixus
```

## Benchmark mekanizması

Rebuild'i, o an Claude Code'u besleyen **backend model** yapar. Farklı bir modeli test etmek için
modeli `claude-code-router` ile bağlayıp **aynı** `/rebuild` komutunu çalıştırırsın; model adını
komuta argüman olarak verirsin. Codex her zaman nötr puanlayıcıdır.

### Çoklu-run & yeniden skorlama (gürültü kontrolü)

Codex bir LLM-yargıçtır; **tek run gürültülüdür**. Standart (bkz. [`lib/RUBRIC.md`](lib/RUBRIC.md)):

- Her model **N ≥ 3 bağımsız Codex run** ile puanlanır → kategori **medyanı** kanonik, **aralık** raporlanır.
- **Hiçbir model sabit baseline değildir:** yeni bir model eklendiğinde **mevcut tüm modeller aynı batch'te,
  aynı Codex sürümüyle yeniden skorlanır** (eski tek-run skoru dondurulmaz). Ham run'lar `runs/*/rescore/` +
  `runs/rescore-analysis.json` olarak commit edilir.
- Composite **aralıkları örtüşüyorsa** "≈ istatistiksel beraberlik" yazılır; kategori bazında ayrışma ayrıca belirtilir.

> Neden: ilk yayında opus-4.8 vs glm-5.2 **tek-run** kıyaslandı ve glm öne geçti; 3-run medyana geçilince
> opus-4.8'in tek-run UI=53 skorunun bir **outlier** olduğu görüldü (3 run'da 58–64) ve sıralama düzeldi
> (opus 79.5 ≈ glm 79.0, UI'da opus tutarlı önde). Tek-run sonuçlarına bu yüzden güvenilmez.

## Klasör yapısı

```
specs/<site>/        # paylaşılan, sabit girdi: spec.md + screenshots/ (tasarım) + reference/
runs/<model>__<site>/# çıktı: site/ + screenshots/ (render) + scorecard.json/md + meta.json
results/             # leaderboard çıktıları (commit edilir)
lib/                 # RUBRIC.md + scorecard.schema.json
```

`specs/`, `runs/` ve `results/` bilerek commit edilir — benchmark'ın **şeffaflığı ve
tekrarlanabilirliği** için (her model birebir aynı spec girdisini aldı, kanıtıyla görülebilir).
Vanilla static olduğu için build/`node_modules` yok, repo şişmez.

## Gereksinimler

- Codex CLI (`codex`) kurulu ve giriş yapılmış olmalı — `/codex:setup` ile doğrula.
- `ctx_fetch_and_index` (context-mode) reference içerik çekimi için.

## Notlar

- Üretilen site modelin **doğal** çıktısıdır; tüm modeller aynı Applixus-harness koşullarında test
  edilir (global no-comments backstop yalnız reminder'dır, üretimi bloklamaz → *göreli* sıralama
  elma-elmaya kalır).
- Codex skoru **birebir** kaydedilir; PageSpeed dışında hiçbir kategori elle değiştirilmez.
