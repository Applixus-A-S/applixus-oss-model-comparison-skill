---
description: "Verilen URL'deki siteyi sıfırdan vanilla static (HTML/CSS/JS) olarak yeniden kodlar; benchmark spec'ini oluşturur/yeniden kullanır."
argument-hint: "<model> <url> [site-slug]"
---

# /llm-ux-benchmark:rebuild

Bu benchmark'ta **test edilen model sensin**. Görevin: ikinci argümandaki adreste bulunan siteyi
**sıfırdan** yeniden kodlamak. Stack ve gereksinimler sabittir (her model birebir aynı görevi alır).

## Argümanlar
- `$1` = model adı (örn. `opus-4.8`, `glm-5.2`, `sonnet-4.6`) — run'a damgalanır.
- `$2` = referans site URL'i (örn. `https://www.applixus.com`).
- `$3` = site-slug (opsiyonel). Verilmezse URL'in domain'inden türet (örn. `https://www.applixus.com` → `applixus`).

## Kök (ROOT) tespiti — ÖNCE bunu yap
Benchmark kökü = içinde **`lib/RUBRIC.md`** bulunan dizin. Sırayla dene ve **doğrula**:
1. `${CLAUDE_PLUGIN_ROOT}` set **ve** `${CLAUDE_PLUGIN_ROOT}/lib/RUBRIC.md` varsa → `ROOT=${CLAUDE_PLUGIN_ROOT}`.
2. Değilse `$(pwd)/lib/RUBRIC.md` varsa → `ROOT=$(pwd)`.
3. İkisi de yoksa → **DUR**: "Benchmark kökü bulunamadı (`lib/RUBRIC.md` yok). llm-ux-benchmark repo kökünden çalıştır." de, devam etme.

Devam etmeden önce `$ROOT/lib/RUBRIC.md`'nin gerçekten var olduğunu teyit et (yanlış dizine sessizce
yazma riskine karşı). Tüm veri `$ROOT` altında: `$ROOT/specs`, `$ROOT/runs`, `$ROOT/lib`.
Slug'ı `$3`'ten ya da domain'den hesapla → `SLUG`.

## Adım 1 — Spec bootstrap (paylaşımlı, sabit girdi)

`$ROOT/specs/$SLUG/` **yoksa** oluştur:

1. `$ROOT/specs/$SLUG/spec.md` yaz — **zorunlu brief**:
   - **Stack:** Saf HTML + CSS + minimal vanilla JS. **Build adımı YOK** (framework yok, npm yok, paket yok). `index.html` + `assets/`.
   - **SEO-uyumlu:** `<title>`, `<meta name="description">`, OpenGraph + Twitter card, tek `<h1>` ile tutarlı heading hiyerarşisi, tüm görsellerde `alt`, `<link rel="canonical">`.
   - **Göze hoş / estetik:** tutarlı renk paleti, tipografi ölçeği, hizalama, boşluk, görsel hiyerarşi, cila.
   - **Mobil-uyumlu (responsive):** `<meta name="viewport">`, breakpoint'ler, mobilde yatay-scroll/taşma yok.
   - **Viewport hedefleri:** mobil 375px, masaüstü 1440px.
2. `$ROOT/specs/$SLUG/screenshots/` klasörünü oluştur ve **kullanıcıdan orijinal sitenin tasarım (reference) ekran görüntülerini** bu klasöre koymasını iste (anasayfa + uygulamalar/öne çıkan bölümler). **DUR ve bekle** — ekran görüntüleri gelene kadar rebuild'e başlama.
3. Referans içerik: `$2` URL'ini `ctx_fetch_and_index` ile indeksle, `ctx_search` ile başlık/menü/bölüm/metin/CTA yapısını çıkar, özetini `$ROOT/specs/$SLUG/reference/content.md` olarak yaz.

`$ROOT/specs/$SLUG/` **varsa** → mevcut `screenshots/` + `reference/`'ı **yeniden kullan**, tekrar isteme.

## Adım 2 — Rebuild

Spec'i (brief + reference ekran görüntüleri + `reference/content.md`) oku ve siteyi **sıfırdan** üret:
- Çıktı dizini: `$ROOT/runs/$1__$SLUG/site/` (örn. `index.html`, `assets/styles.css`, `assets/app.js`, varsa `assets/img/`).
- Brief'teki **SEO + estetik + mobil-uyum** gereksinimlerinin **hepsini** karşıla.
- Referans tasarıma görsel olarak sadık kal; içerik/metinleri `reference/content.md`'den al.
- Görseller için harici asset indirme; placeholder/CSS ile çöz veya referans yapıyı sadakatle taklit et.

## Adım 3 — meta.json

`$ROOT/runs/$1__$SLUG/meta.json` yaz:
```
{ "model": "<$1>", "site": "<SLUG>", "url": "<$2>", "created": "<ISO tarih>", "spec": "specs/<SLUG>", "pagespeed": "pending" }
```

## Adım 4 — Kullanıcıya bilgi

Şunu söyle: "Site hazır → `runs/$1__$SLUG/site/`. Sıradaki adımlar: (1) siteyi deploy et + PageSpeed/Lighthouse ölç, (2) `/llm-ux-benchmark:score $1__$SLUG` ile Codex puanlamasını başlat (Codex senden render ekran görüntüsü isteyecek)."

> Not: Üretilen site, modelin doğal çıktısıdır; tüm modeller aynı Applixus-harness koşullarında test edilir (global no-comments backstop yalnız reminder'dır, üretimi bloklamaz).
