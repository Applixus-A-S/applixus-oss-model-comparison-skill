# Scorecard — moonshotai/kimi-k2.7-code · applixus

| Alan | Değer |
|---|---|
| Model | **moonshotai/kimi-k2.7-code** |
| Site | applixus (https://www.applixus.com) |
| Deploy | https://kimi-2-7-code.applixus.com/ |
| Run | `moonshotai-kimi-k2.7-code__applixus` |
| Tarih | 2026-06-24 |
| Maliyet | **$1.45** |
| Puanlayan | Codex (nötr, codex-cli) + PageSpeed (kullanıcı ölçümü) |

## Skorlar

| Kategori | Puan | Puanlayan |
|---|---:|---|
| Teknik kalite (SEO + mobil-uyum + a11y) | **72** | Codex |
| PageSpeed çıktıları | **88** | Sen (Lighthouse, Performans, mobil) |
| UI kalitesi (estetik + görsel sadakat) | **43** | Codex |
| Kod okunabilirliği | **80** | Codex |

> **Composite:** `(72 + 88 + 43 + 80) / 4` = **70.75 / 100** (eşit ağırlık %25).
> Not: Bu skorlar **tek Codex run'ından** gelmektedir; benchmark standartı N ≥ 3 bağımsız run ve medyan değerlendirmedir.

## PageSpeed çıktıları — 88

Kaynak: Google PageSpeed Insights / Lighthouse. Benchmark PageSpeed kategorisi = **Performans** skoru (mobil).

| Lighthouse kategorisi | Mobil | Masaüstü |
|---|---:|---:|
| **Performans** (PageSpeed skoru) | **88** | **97** |
| Erişilebilirlik | — | — |
| En İyi Uygulamalar | — | — |
| SEO | — | — |

## Teknik kalite — 72

**Gerekçe:** Semantik yapı, viewport, temel SEO meta etiketleri ve responsive grid mevcut; ancak bazı asset/link doğruluğu ve erişilebilirlik ayrıntıları zayıf.

- `header`/`nav`/`main`/`footer` landmark yapısı, tek h1, canonical, description, OpenGraph/Twitter ve mobil breakpoint'ler var.
- `og:image` olarak verilen `assets/img/og-home.jpg` ve `assets/img/og-apps.jpg` dosyaları site içinde yok; sosyal paylaşım görselleri kırık olur.
- Birçok ürün linki `href="#"` ve `onclick alert` ile sahte davranış veriyor; anlamlı URL/disabled durum yok.
- Görünür focus stilleri tanımlanmamış; klavye erişilebilirliği temel seviyede kalıyor.
- Mobil CSS tek kolona düşüyor ve hamburger menü var; ekran görüntülerinde yatay taşma görünmüyor.

## UI kalitesi — 43

**Gerekçe:** Rebuild kendi içinde temiz ve okunabilir bir koyu mavi SaaS görünümü kuruyor, fakat referans tasarımın kırmızı/siyah görsel dili, X motifleri, gerçek kart görselleri, logo/referans sunumu ve yoğun uygulama vitriniyle sadaketi düşük.

- Referans anasayfadaki kırmızı-siyah marka atmosferi, büyük X görsel dili, fotoğraflı about alanı ve kırmızı CTA dili rebuild'de mavi gradient placeholder/SVG estetiğine dönmüş.
- Referans uygulamalar sayfası görselli kartlar, kırmızı teknoloji/özellik etiketleri ve çok daha geniş uygulama listesiyle daha zengin; rebuild basit ikonlu kartlara ve daha kısa listeye indirgenmiş.
- Masaüstü ve mobil rebuild düzeni teknik olarak dengeli, spacing tutarlı ve okunabilir; ancak görsel sadakat açısından referansın kompozisyon karakterini yakalamıyor.
- Mobil rebuild temiz tek kolon akıyor, fakat referanstaki marka yoğunluğu ve uygulama kartlarının medya ağırlığı kaybolmuş.
- Footer ve header düzeni referansa yapısal olarak benziyor, ama renk, logo vurgusu, CTA ve detay seviyesi farklı.

## Kod okunabilirliği — 80

**Gerekçe:** Kod basit, ayrıştırılmış ve takip edilebilir; HTML/CSS/JS sorumlulukları ayrı. Tekrar ve uzun inline SVG/tekrarlanan kart markup'ı sürdürülebilirliği bir miktar düşürüyor.

- `index.html`, `apps.html`, `assets/styles.css` ve `assets/app.js` net ayrılmış; sınıf adları BEM'e yakın ve anlamlı.
- CSS değişkenleri renk, radius, container ve shadow değerlerini merkezi tutuyor; breakpoint'ler anlaşılır.
- `apps.html` içinde store ikon SVG'leri ve kart yapıları çok tekrarlı; veri tabanlı üretim veya küçük bileşen yaklaşımı olsaydı bakım kolaylaşırdı.
- Inline `onclick alert` kullanımı HTML'i davranışla karıştırıyor ve link durumunu temiz modellemiyor.
- JS küçük ve anlaşılır; hamburger menü için yeterli.

## Durum

✅ **Tamamlandı.** Dört kategori puanlandı; PageSpeed `done`, composite **70.75/100**.
