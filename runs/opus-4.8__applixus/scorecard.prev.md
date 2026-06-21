# Scorecard — opus-4.8 · applixus

| Alan | Değer |
|---|---|
| Model | **opus-4.8** |
| Site | applixus (https://www.applixus.com) |
| Deploy | https://opus4-8.applixus.com/ |
| Run | `opus-4.8__applixus` |
| Tarih | 2026-06-21 |
| Puanlayan | Codex (gpt-5.5, nötr) + PageSpeed (kullanıcı ölçümü) |

## Skorlar

| Kategori | Puan | Puanlayan |
|---|---:|---|
| Teknik kalite (SEO + mobil-uyum + a11y) | **78** | Codex |
| PageSpeed çıktıları | **98** | Sen (Lighthouse, Performans) |
| UI kalitesi (estetik + görsel sadakat) | **53** | Codex |
| Kod okunabilirliği | **82** | Codex |

> **Composite (TAM):** `(teknik + pagespeed + ui + okunabilirlik) / 4`
> = `(78 + 98 + 53 + 82) / 4` = **77.75 / 100**. (eşit ağırlık, her biri %25)

## PageSpeed çıktıları — 98

Kaynak: Google PageSpeed Insights / Lighthouse, 21 Haz 2026 17:18. Benchmark PageSpeed kategorisi
= **Performans** skoru (SEO/a11y/best-practices zaten Teknik kategoride sayıldığı için çift sayım yapılmaz).

| Lighthouse kategorisi | Mobil | Masaüstü |
|---|---:|---:|
| **Performans** (PageSpeed skoru) | **98** | **98** |
| Erişilebilirlik | 96 | 95 |
| En İyi Uygulamalar | 100 | 100 |
| SEO | 100 | 100 |

**Core Web Vitals:** FCP 0,8 sn · LCP 0,8 sn · TBT 0 ms · CLS 0 · Speed Index 4,1 sn (mobil) / 1,2 sn (masaüstü). Tümü yeşil bant; CLS = 0 (layout shift yok), TBT = 0 ms.

## Teknik kalite — 78

**Gerekçe:** Semantik HTML, temel SEO meta yapısı, responsive kırılımlar ve erişilebilirlik temelleri iyi; ancak içerik eksikleri, boş/belirsiz bağlantılar ve küçük a11y/SEO asset sorunları puanı düşürüyor.

- index.html ve apps.html'de viewport, title, description, canonical, OG/Twitter meta, tek `h1` ve header/nav/main/footer landmark yapısı mevcut.
- Skip link, `:focus-visible` stili, `aria-label`'lı navigasyon ve mobil menü `aria-expanded` yönetimi olumlu.
- content.md'deki SSS/FAQ bölümü index.html'de yok; apps.html yalnız 13 kart üretiyor ve orijinal apps ekranındaki uzun katalog kapsamını karşılamıyor.
- Çerez Politikası ve Gizlilik Politikası bağlantıları `href="#"` placeholder; gerçek hedef yok.
- OG/Twitter image `assets/img/og-cover.png` gösteriyor ama site klasöründe bu asset yok.
- Filtreler `role="tablist"/"tab"` kullanıyor ama ilişkili `tabpanel`/`aria-controls` ve klavye tab davranışı tamamlanmamış.

## UI kalitesi — 53

**Gerekçe:** Kendi içinde temiz ve tutarlı bir koyu tema var, fakat referans tasarıma görsel sadakat düşük-orta seviyede; özellikle uygulama kartları, gerçek görseller, katalog uzunluğu, referans/FAQ sunumu ve mobil detaylar belirgin biçimde ayrışıyor.

- Anasayfa rebuild'i referanstaki büyük X hero fikrini ve kırmızı/siyah paleti koruyor; ancak orijinaldeki açılı arka plan, daha güçlü hero kompozisyonu, gerçek about görseli, referans kartları ve FAQ akışı eksik.
- Uygulamalar sayfası orijinalde gerçek görsel thumbnail'lı, daha yoğun ve uzun bir katalogken rebuild emoji/gradient placeholder kartlara dönmüş; görsel sadakat ciddi düşüyor.
- Rebuild ekran görüntüsü yüksekliği referanslardan çok kısa: apps desktop ~7.780px vs ~13.380px, apps mobile ~17.498px vs ~35.276px — eksik içerik ve daha seyrek katalog etkisi.
- Kart grid'i, spacing ve renk uyumu genel olarak düzenli; masaüstünde okunabilir ve dengeli bir statik site hissi veriyor.
- Mobil görünüm çalışıyor ve tek kolon okunabilir, ancak referanstaki daha yoğun bölüm hiyerarşisi ve kart görselliği yerine sadeleştirilmiş bir akış var.

## Kod okunabilirliği — 82

**Gerekçe:** Dosyalar basit ve anlaşılır şekilde ayrılmış; CSS değişkenleri, sınıf isimleri ve küçük JS modülü sürdürülebilir. Yine de header/footer ve uygulama kartları manuel tekrarlandığı için ölçeklenebilirlik sınırlı.

- index.html, apps.html, assets/styles.css ve assets/app.js sorumlulukları net ayrılmış.
- CSS custom property kullanımı, tutarlı class isimleri ve breakpoint yapısı okunabilirliği artırıyor.
- app.js küçük, amaç odaklı; menü, reveal, filtreleme, yıl güncelleme davranışlarını anlaşılır biçimde ayırıyor.
- Header/footer iki HTML dosyasında kopyalanmış; değişiklikte çift bakım riski var.
- Uygulama kartları veri kaynağı/template yerine elle tekrarlanmış; 20+ uygulamaya büyüdükçe bakım maliyeti artar.
- Emoji/thumbnail varyasyonları ayrı `thumb-*` class'larıyla yönetiliyor; küçük ölçekte anlaşılır ama gerçek katalogda daha veri odaklı yapı daha sürdürülebilir olur.

## Genel notlar (Codex)

Rebuild teknik olarak büyük ölçüde sağlam ve okunabilir, ancak orijinal Applixus tasarımına görsel sadakat zayıf kalıyor. En büyük kayıp uygulamalar sayfasındaki gerçek görsel kartların ve uzun katalog yapısının emoji placeholder'lı kısa bir listeye indirgenmesi; anasayfada da FAQ, gerçek about görseli ve referans kartı sunumu eksik.

## Durum

✅ **Tamamlandı.** Dört kategori de puanlandı; PageSpeed `done`, composite **tam** (77.75/100).
Model karşılaştırması için: `/llm-ux-benchmark:compare applixus`.
