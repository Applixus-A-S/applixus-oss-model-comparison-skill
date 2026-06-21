# Scorecard — opus-4.8 · applixus

| Alan | Değer |
|---|---|
| Model | **opus-4.8** |
| Site | applixus (https://www.applixus.com) |
| Deploy | https://opus4-8.applixus.com/ |
| Run | `opus-4.8__applixus` |
| Tarih | 2026-06-21 (3-run yeniden skorlama) |
| Puanlayan | Codex (nötr, codex-cli 0.136.0, **3 bağımsız run**) + PageSpeed (kullanıcı ölçümü) |

## Skorlar (3-run medyan)

| Kategori | Puan | Puanlayan |
|---|---:|---|
| Teknik kalite (SEO + mobil-uyum + a11y) | **78** | Codex |
| PageSpeed çıktıları | **98** | Sen (Lighthouse, Performans) |
| UI kalitesi (estetik + görsel sadakat) | **58** | Codex |
| Kod okunabilirliği | **84** | Codex |

> **Composite:** `(78 + 98 + 58 + 84) / 4` = **79.5 / 100** (medyan run = run1; eşit ağırlık %25).
> ⚖️ **opus vs glm composite ≈ istatistiksel beraberlik** (opus 78.5–81.0 · glm 77.0–79.75, aralıklar örtüşüyor). opus composite'te hafif önde.

## 3-run dağılımı (Codex, nötr)

| Run | Teknik | UI | Okunabilirlik | Composite* |
|---|---:|---:|---:|---:|
| 1 *(medyan, kanonik)* | 78 | 58 | 84 | **79.5** |
| 2 | 82 | 64 | 80 | 81.0 |
| 3 | 72 | 61 | 83 | 78.5 |
| **Medyan** | **78** | **61** | **83** | **79.5** |
| **Aralık** | 72–82 | **58–64** | 80–84 | 78.5–81.0 |

\* Composite = `(teknik + 98 + ui + okunabilirlik) / 4`. Kanonik scorecard.json = **run1** (medyan run, içsel tutarlı).

> **UI gözlemi:** opus UI 3 run'ın hepsinde **58–64** bandında; glm UI **50–56** bandında → bu iki aralık **örtüşmüyor**. opus, görsel kalite/sadakat ekseninde her üç bağımsız run'da glm'den **tutarlı şekilde yüksek** puanlandı (medyan 61 vs 55). (n=3; "tutarlı", "kesin üstün" değil.)

## PageSpeed çıktıları — 98

Kaynak: Google PageSpeed Insights / Lighthouse. Benchmark PageSpeed kategorisi = **Performans** skoru
(SEO/a11y/best-practices zaten Teknik kategoride sayıldığı için çift sayım yapılmaz).

| Lighthouse kategorisi | Mobil | Masaüstü |
|---|---:|---:|
| **Performans** (PageSpeed skoru) | **98** | **98** |
| Erişilebilirlik | 96 | 95 |
| En İyi Uygulamalar | 100 | 100 |
| SEO | 100 | 100 |

**Core Web Vitals:** FCP 0,8 sn · LCP 0,8 sn · TBT 0 ms · CLS 0 · Speed Index 4,1 sn (mobil) / 1,2 sn (masaüstü).

## Teknik kalite — 78 (medyan run)

**Gerekçe:** Semantik yapı, temel SEO meta etiketleri, canonical, viewport, responsive grid ve erişilebilirlik için skip/focus desteği iyi. Ancak içerik tamamlığı ve doğrulukta eksikler, dummy linkler ve eksik sosyal görsel asset'i teknik kaliteyi düşürüyor.

- `header`/`nav`/`main`/`footer`, tek H1, title/description, OG/Twitter ve canonical genel olarak mevcut.
- Mobil görünüm kırılmadan çalışıyor; grid ve menü breakpoint'leri uygulanmış.
- `og:image` ve `twitter:image` `assets/img/og-cover.png` adresine bakıyor ama site içinde bu asset yok.
- Footer'daki çerez/gizlilik linkleri `#`; sosyal linkler gerçek Applixus profilleri yerine genel domainlere gidiyor.
- Content spec'teki SSS bölümü yok; uygulamalar sayfası 20+ iddiasına rağmen referans görseldeki birçok uygulama kartını üretmiyor.

## UI kalitesi — 58 (medyan run)

**Gerekçe:** Rebuild kendi içinde temiz ve okunabilir bir dark/red arayüz kurmuş, fakat referans tasarıma görsel sadakat belirgin biçimde düşük. Özellikle uygulama kartları, görseller, referans/FAQ bölümleri ve sayfa uzunluğu referanstan ciddi sapıyor.

- Anasayfa hero renk/ton olarak yakın, ancak referanstaki büyük X kompozisyonu, diagonal arka plan etkisi ve görsel yoğunluk daha zayıf yeniden kurulmuş.
- Biz Kimiz bölümünde referanstaki gerçek ekip fotoğrafı yerine soyut halka görseli kullanılmış.
- Referans tasarımındaki marka kartları ve SSS bölümü rebuild'de yok; referanslar sadece küçük pill etiketlere indirgenmiş.
- Uygulamalar sayfasında zengin thumbnail görseller yerine emoji/gradient placeholder'lar var; görsel sadakat en büyük kaybı burada.
- Mobil layout kullanılabilir, fakat referansın yoğun kart görsel dili ve kapsamı korunmamış.

## Kod okunabilirliği — 84 (medyan run)

**Gerekçe:** Kod sade statik HTML/CSS/JS ayrımıyla okunabilir; sınıf adları anlamlı ve JS küçük, odaklı. Bakım açısından tekrar eden header/footer ve hardcoded kart listeleri ana zayıflıklar.

- Dosyalar net ayrılmış: iki HTML sayfası, ortak CSS ve küçük bir JS dosyası.
- Class isimleri tutarlı ve bileşen mantığı anlaşılır: `hero`, `app-card`, `filter-btn`, `contact-list` gibi.
- CSS uzun ama bölümler halinde düzenli; responsive kurallar dosyanın sonunda anlaşılır konumda.
- Header/footer iki HTML dosyasında kopyalanmış; ortak template yok.
- Uygulama kartları tamamen hardcoded, veri tabanlı bir yapı olmadığı için 20+ uygulama kapsamını sürdürmek zahmetli.

## Durum

✅ **Tamamlandı (3-run yeniden skorlama).** Dört kategori puanlandı; PageSpeed `done`, composite **79.5/100**.
Ham 3-run örnekleri: [`rescore/`](rescore/) · önceki tek-run: [`scorecard.prev.md`](scorecard.prev.md) · karşılaştırma: [`runs/rescore-analysis.json`](../rescore-analysis.json).
