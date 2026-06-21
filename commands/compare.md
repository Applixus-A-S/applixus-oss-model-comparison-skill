---
description: "Tüm scorecard'ları okuyup model karşılaştırma leaderboard'u (markdown tablo) üretir."
argument-hint: "[site-slug]"
---

# /llm-ux-benchmark:compare

Deterministik birleştirme — **yargı yok**, sadece okuma + tablo + ortalama.

## Kök (ROOT) tespiti — ÖNCE bunu yap
Benchmark kökü = içinde **`lib/RUBRIC.md`** bulunan dizin. `${CLAUDE_PLUGIN_ROOT}/lib/RUBRIC.md`
varsa `ROOT=${CLAUDE_PLUGIN_ROOT}`; değilse `$(pwd)/lib/RUBRIC.md` varsa `ROOT=$(pwd)`; ikisi de
yoksa **DUR** ("Benchmark kökü bulunamadı. llm-ux-benchmark repo kökünden çalıştır."). Devam etmeden
`$ROOT/lib/RUBRIC.md`'yi teyit et. Hedef: `$1` (site-slug, opsiyonel).

## Adımlar
1. `$ROOT/runs/*/scorecard.json` dosyalarını bul. `$1` verildiyse yalnız `*__$1` run'larını al.
2. Her scorecard'dan oku: `model`, `scores.technical.score`, `scores.ui.score`, `scores.readability.score`, `pagespeed`.
3. Composite = `lib/RUBRIC.md` eşit ağırlık:
   - PageSpeed `done` ise: `(teknik + pagespeed + ui + okunabilirlik) / 4`.
   - PageSpeed `pending`/null ise: mevcut 3 kategorinin ortalaması, PageSpeed hücresine `pending`, composite'e `*` (kısmi) işareti.
4. Composite'e göre **azalan** sırala.
5. `$ROOT/results/<$1 ya da "all">-leaderboard.md` yaz: tarih başlığı + tablo:
   ```
   | Model | Teknik | PageSpeed | UI | Okunabilirlik | Composite |
   |-------|:------:|:---------:|:--:|:-------------:|:---------:|
   ```
6. Tabloyu kullanıcıya da göster. `*` = PageSpeed bekleniyor (kısmi composite) açıklamasını ekle.
