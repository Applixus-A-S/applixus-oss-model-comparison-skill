# Benchmark Spec — applixus

> Bu, llm-ux-benchmark'ın **paylaşılan, sabit girdisidir**. Tüm modeller (opus-4.8, glm-5.2, …)
> birebir aynı brief + aynı reference içerik + aynı tasarım ekran görüntülerini alır.
> Görev: aşağıdaki adresteki siteyi **sıfırdan** yeniden kodlamak.

- **Referans site:** https://www.applixus.com
- **Slug:** applixus

## Zorunlu brief

### Stack
- Saf **HTML + CSS + minimal vanilla JS**. **Build adımı YOK** (framework yok, npm yok, paket yok).
- Çıktı yapısı: `index.html` + `assets/` (`assets/styles.css`, `assets/app.js`, gerekiyorsa `assets/img/`).

### SEO-uyumlu
- `<title>`, `<meta name="description">`.
- OpenGraph + Twitter card meta etiketleri.
- Tek `<h1>` ve tutarlı heading hiyerarşisi.
- Tüm görsellerde `alt`.
- `<link rel="canonical">`.

### Göze hoş / estetik
- Tutarlı renk paleti, tipografi ölçeği, hizalama, boşluk, görsel hiyerarşi ve cila.

### Mobil-uyumlu (responsive)
- `<meta name="viewport">`.
- Breakpoint'ler; mobilde yatay-scroll / taşma yok.
- Yeterli büyüklükte dokunma hedefleri.

### Viewport hedefleri
- Mobil: **375px**
- Masaüstü: **1440px**

## Girdi dosyaları
- `reference/content.md` — referans sitenin başlık/menü/bölüm/metin/CTA yapısı (ctx ile indekslenip çıkarıldı).
- `screenshots/` — orijinal sitenin tasarım (reference) ekran görüntüleri (anasayfa + öne çıkan bölümler).
