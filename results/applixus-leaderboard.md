# Leaderboard — applixus

> Üretim tarihi: 2026-06-21 · Referans site: https://www.applixus.com
> Composite = `(teknik + pagespeed + ui + okunabilirlik) / 4` (eşit ağırlık, her biri %25).
> PageSpeed = kullanıcı ölçümü (Lighthouse Performans, mobil-birincil); diğer 3 kategori = **Codex (nötr, 3 bağımsız run medyanı)**.

| Model | Teknik | PageSpeed | UI | Okunabilirlik | Composite | Composite aralığı |
|-------|:------:|:---------:|:--:|:-------------:|:---------:|:-----------------:|
| **opus-4.8** | 78 | 98 | 58 | 84 | **79.5** | 78.5–81.0 |
| **glm-5.2** | 80 | 98 | 56 | 82 | **79.0** | 77.0–79.75 |

⚖️ **Composite ≈ istatistiksel beraberlik:** opus (78.5–81.0) ve glm (77.0–79.75) aralıkları örtüşüyor; opus medyan composite'te 0,5 puan önde.
🎨 **UI ekseni:** opus UI 3 run'da **58–64**, glm UI **50–56** → örtüşmeyen aralıklar; opus görsel sadakatte her run'da tutarlı şekilde daha yüksek (medyan 61 vs 55). Her iki model de referansın siyah/kırmızı + X motifli tasarımından uzak (ikisi de koyu temaya kaçtı).

> **Metodoloji notu:** Sayılar tek-run → **3-run medyana** geçti (LLM-yargıç gürültüsünü azaltmak için). İlk tek-run, şanslı-yüksek bir glm örneğini (tech 82=max, read 84=max) şanssız-düşük bir opus UI örneğiyle (53; 3 yeni run'ın hepsinin altında) kıyaslamıştı; ortalama bu şansı eler.

Detaylar:
- **opus-4.8** → [`runs/opus-4.8__applixus/scorecard.md`](../runs/opus-4.8__applixus/scorecard.md) · canlı demo: https://opus4-8.applixus.com/
- **glm-5.2** → [`runs/glm-5.2__applixus/scorecard.md`](../runs/glm-5.2__applixus/scorecard.md) · canlı demo: https://glm-5-2.applixus.com/ · maliyet: $11.09
- Ham 3-run örnekleri: `runs/*/rescore/` · özet: [`runs/rescore-analysis.json`](../runs/rescore-analysis.json)
