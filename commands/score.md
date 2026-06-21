---
description: "Rebuild edilen siteyi Codex ile 0-100 puanlar (Teknik/UI/Okunabilirlik). PageSpeed manuel: --pagespeed N."
argument-hint: "<model>__<site> [--pagespeed N]"
---

# /llm-ux-benchmark:score

**Saf Codex handoff.** Sen bir forwarder'sın: girdileri topla, Codex'i çağır, çıktısını **birebir**
kaydet. Puanı **kendin yargılama / değiştirme** (tek istisna: `--pagespeed` aritmetik merge'i).

## Argümanlar
- `$1` = `<model>__<site>` run kimliği (örn. `opus-4.8__applixus`).
- `--pagespeed N` (opsiyonel) = kullanıcının ölçtüğü PageSpeed skoru (0-100 tam sayı).

## Kök (ROOT) tespiti — ÖNCE bunu yap
Benchmark kökü = içinde **`lib/RUBRIC.md`** bulunan dizin. Sırayla dene ve **doğrula**:
1. `${CLAUDE_PLUGIN_ROOT}` set **ve** `${CLAUDE_PLUGIN_ROOT}/lib/RUBRIC.md` varsa → `ROOT=${CLAUDE_PLUGIN_ROOT}`.
2. Değilse `$(pwd)/lib/RUBRIC.md` varsa → `ROOT=$(pwd)`.
3. İkisi de yoksa → **DUR**: "Benchmark kökü bulunamadı (`lib/RUBRIC.md` yok). llm-ux-benchmark repo kökünden çalıştır." de, devam etme.

Devam etmeden önce `$ROOT/lib/RUBRIC.md`'nin var olduğunu teyit et. Sonra:
- `RUN="$1"` ; `SITE="${RUN##*__}"` (run kimliğinin `__`'dan sonraki kısmı).
- Run dizini: `$ROOT/runs/$RUN` · Spec dizini: `$ROOT/specs/$SITE`.

---

## Mod A — `--pagespeed N` verildiyse (Codex çağrılmaz)
1. `$ROOT/runs/$RUN/scorecard.json` oku.
2. `pagespeed = { "score": N, "status": "done" }` yap.
3. Composite'i `lib/RUBRIC.md` ağırlıklarıyla yeniden hesapla (eşit ağırlık → 4 kategorinin ortalaması).
4. `scorecard.json` + `scorecard.md`'yi güncelle, kullanıcıya tam skoru göster. **Bitir.**

---

## Mod B — Codex puanlaması (varsayılan)

> **Çoklu-run protokolü (BAĞLAYICI — bkz. `lib/RUBRIC.md`):** Tek run gürültülüdür. B2'yi **N ≥ 3 kez**
> bağımsız çalıştır (`runs/$RUN/rescore/run{1..N}.json`); kanonik `scorecard.json` = composite'i medyana
> en yakın **temsilci run** (birebir), `scorecard.md` tam N-run tablosu + medyan + aralık. **Yeni model
> eklenirken hiçbir mevcut model sabit baseline değildir** — tüm modelleri aynı batch'te, aynı Codex
> sürümüyle yeniden skorla; ham run'ları + `runs/rescore-analysis.json`'u commit et. Composite aralıkları
> örtüşürse leaderboard'da "≈ beraberlik" yaz.

### B1 — Render ekran görüntüsü talebi (Codex adına)
`$ROOT/runs/$RUN/screenshots/` boş/yoksa: kullanıcıdan **rebuild edilen sitenin render ekran
görüntülerini** bu klasöre koymasını iste — en az **anasayfa** ve **uygulamalar** görünümü (mobil +
masaüstü tercih edilir). Codex read-only sandbox'ta siteyi render edemez; UI'yi **bu ekran
görüntülerinden** yargılar. **DUR ve bekle** — gelene kadar Codex'i çağırma (sahte UI skoru yok).

### B2 — Codex'i çağır
`codex exec`'i **BACKGROUND Bash** ile çalıştır (uzun sürebilir). `-i` argümanlarını **yalnız var
olan dosyalar için** ekle (boş glob hatası olmasın). Çıktıyı dosyaya stream et (head/tail YASAK):

```
codex exec \
  --sandbox read-only \
  --skip-git-repo-check \
  -C "$ROOT" \
  -i "runs/$RUN/screenshots/"*.png \
  -i "specs/$SITE/screenshots/"*.png \
  --output-schema "lib/scorecard.schema.json" \
  -o "runs/$RUN/scorecard.json" \
  "lib/RUBRIC.md'yi oku ve uygula. runs/$RUN/site içindeki yeniden kodlanmış siteyi puanla. Ekteki render ekran görüntülerini (rebuild'in anasayfa + uygulamalar görünümü) referans tasarım ekran görüntüleriyle karşılaştırarak UI'yi yargıla; specs/$SITE/reference/content.md ile içerik doğruluğunu kontrol et. Teknik kalite (SEO + mobil-uyum dahil), UI kalitesi (estetik + görsel sadakat), kod okunabilirliğini 0-100 puanla. PageSpeed'e DOKUNMA: status 'pending', score null bırak. KOD YAZMA, sadece puanla. model alanına '$RUN'in __ öncesi, site alanına '$SITE' yaz. Çıktıyı verilen JSON şemasına birebir uydur." \
  > "runs/$RUN/codex-score.log" 2>&1
```
- `.jpg/.jpeg/.webp` ekran görüntüleri varsa onlar için de `-i` ekle.
- Codex yoksa / çağrı başarısızsa → **DUR ve kullanıcıya bildir** (`/codex:setup` öner). Sahte PASS/skor üretme.

### B3 — Sonuç
1. Codex bitince `$ROOT/runs/$RUN/scorecard.json`'u oku (Codex `-o` ile yazdı). **Değiştirme.**
2. `scorecard.json`'dan **birebir** `$ROOT/runs/$RUN/scorecard.md` türet (insan-okur tablo + gerekçeler). PageSpeed `pending` olduğu için composite'i **kısmi** işaretle.
3. Kullanıcıya skorları göster + şunu söyle: "Deploy edip PageSpeed ölç, sonra `/llm-ux-benchmark:score $RUN --pagespeed N` ile gir."
