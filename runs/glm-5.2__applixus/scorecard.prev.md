# Scorecard — glm-5.2 · applixus

| Alan | Değer |
|---|---|
| Model | **glm-5.2** |
| Site | applixus (https://www.applixus.com) |
| Deploy | https://glm-5-2.applixus.com/ |
| Run | `glm-5.2__applixus` |
| Tarih | 2026-06-21 |
| Puanlayan | Codex (nötr) + PageSpeed (kullanıcı ölçümü) |
| Maliyet | **$11.09** (glm-5.2 rebuild — OpenRouter / z-ai/glm-5.2) |

## Skorlar

| Kategori | Puan | Puanlayan |
|---|---:|---|
| Teknik kalite (SEO + mobil-uyum + a11y) | **82** | Codex |
| PageSpeed çıktıları | **98** | Sen (Lighthouse, Performans) |
| UI kalitesi (estetik + görsel sadakat) | **55** | Codex |
| Kod okunabilirliği | **84** | Codex |

> **Composite (TAM):** `(teknik + pagespeed + ui + okunabilirlik) / 4`
> = `(82 + 98 + 55 + 84) / 4` = **79.75 / 100**. (eşit ağırlık, her biri %25)

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

## Teknik kalite — 82

**Gerekçe:** Semantik yapı, SEO temelleri ve responsive davranış güçlü; içerik referans dosyayla büyük ölçüde eşleşiyor. Puanı düşüren ana sorun, uygulama/store/web CTA'larının çoğunun gerçek hedef yerine placeholder link olması.

- index.html ve apps.html içinde viewport, title, description, OpenGraph, Twitter card, canonical, header/nav/main/footer ve tek H1 mevcut.
- Görsellerin alt metinleri var; mobil menü `aria-expanded` ile yönetiliyor, `:focus-visible` tanımlı ve 1024/760/375 breakpoint'leri mobil görünümü destekliyor.
- specs/applixus/reference/content.md'deki ana metinler, ürün adları, iletişim bilgileri, referanslar ve uygulama listesi büyük ölçüde korunmuş.
- apps.html içinde çok sayıda `href="#"` store/web linki var; ayrıca footer ürün linkleri `#top`'a gidiyor ama apps.html'de `top` id'si yok.
- OG görselleri relatif SVG olarak verilmiş; deploy/SEO açısından mutlak sosyal paylaşım görseli kadar sağlam değil.

## UI kalitesi — 55

**Gerekçe:** Rebuild kendi içinde temiz, okunaklı ve mobilde düzenli; ancak ekli referans tasarıma görsel sadakat zayıf. Referanstaki siyah/kırmızı marka dili, büyük X motifi, image-heavy uygulama kartları ve kırmızı CTA sistemi yerine mor/indigo, ikon kartlı farklı bir tasarım kurulmuş.

- Anasayfa render'ı içerik sırasını yakalıyor fakat referans görseldeki kırmızı-siyah dramatik hero, büyük X arka planı ve gerçek görsel ağırlığı yerine mor gradient/SVG telefon yaklaşımı kullanılmış.
- Uygulamalar sayfası referanstaki büyük kapak görselli, kırmızı rozetli kart yapısından uzak; render küçük ikonlu, daha kurumsal SaaS kartları gibi duruyor.
- Mobil render'lar hizalama ve okunabilirlik açısından iyi; kartlar tek kolona düzgün düşüyor, belirgin taşma görünmüyor.
- Görsel hiyerarşi ve spacing genel olarak cilalı olsa da referansın nav/footer, referans kartları, CTA renkleri ve uygulama görselleriyle uyum düşük.
- İçerik doğruluğu UI içinde iyi korunmuş, fakat birebir tasarım benchmark'ı açısından marka paleti ve komponent dili ciddi sapıyor.

## Kod okunabilirliği — 84

**Gerekçe:** Kod sade statik HTML/CSS/JS olarak iyi ayrılmış, isimlendirme anlaşılır ve CSS bölümlenmiş. Sürdürülebilirliği düşüren nokta, header/footer ve uygulama kartlarının elle tekrar edilmesi.

- Dosya yapısı anlaşılır: iki HTML sayfası, ortak styles.css, ortak app.js ve asset klasörü var.
- CSS değişkenleri, section yorumları, breakpoint blokları ve component class isimleri okunabilirliği artırıyor.
- JavaScript küçük ve sorumluluğu net: sticky header, mobil menü, FAQ accordion ve anchor scroll.
- HTML içinde header/footer ve çok sayıda app-card markup'ı tekrar ediyor; veri tabanlı bir yapı olmadığı için içerik güncellemek zahmetli.
- Tek dosyada 683 satır CSS var; düzenli olsa da büyüme halinde component bazlı ayrım daha sürdürülebilir olur.

## Genel notlar (Codex)

PageSpeed puanlanmadı (kullanıcı ölçümüyle sonradan merge edildi). Graphify zorunluluğu için sorgu denendi ancak `graphify-out/graph.json` bulunmadı; read-only ve KOD YAZMA kısıtı nedeniyle graph oluşturulmadı (skorları etkilemez).

## Durum

✅ **Tamamlandı.** Dört kategori de puanlandı; PageSpeed `done`, composite **tam** (79.75/100).
Model karşılaştırması için: `/llm-ux-benchmark:compare applixus`.
