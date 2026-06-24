# Leaderboard — applixus

> Üretim tarihi: 2026-06-24 · Referans site: https://www.applixus.com
> Composite = `(teknik + pagespeed + ui + okunabilirlik) / 4` (eşit ağırlık, her biri %25).
> PageSpeed = kullanıcı ölçümü (Lighthouse Performans, mobil-birincil); diğer 3 kategori = **Codex (nötr)**.

| Model | Teknik | PageSpeed | UI | Okunabilirlik | Composite | Composite aralığı |
|-------|:------:|:---------:|:--:|:-------------:|:---------:|:-----------------:|
| **opus-4.8** | 78 | 98 | 58 | 84 | **79.5** | 78.5–81.0 (3-run medyan) |
| **glm-5.2** | 80 | 98 | 56 | 82 | **79.0** | 77.0–79.75 (3-run medyan) |
| **moonshotai/kimi-k2.7-code** | 72 | 88 | 43 | 80 | **70.75** | — (tek-run) |

⚖️ **opus-4.8 ≈ glm-5.2:** composite aralıkları örtüşüyor; opus medyanda 0,5 puan önde.
🆕 **moonshotai/kimi-k2.7-code** tek-run sonucu mevcut iki modelin arkasında kalıyor; özellikle **UI sadakati** (43) ve **PageSpeed** (88) eksenlerinde fark belirgin.

> **Metodoloji notu:** opus-4.8 ve glm-5.2 skorları **3-run medyan**dır; moonshotai/kimi-k2.7-code şu an **tek Codex run** değerlendirmesidir. Yeni model eklendiğinde tüm modellerin aynı batch'te, aynı Codex sürümüyle yeniden skorlanması önerilir.

Detaylar:
- **opus-4.8** → [`runs/opus-4.8__applixus/scorecard.md`](../runs/opus-4.8__applixus/scorecard.md) · canlı demo: https://opus4-8.applixus.com/
- **glm-5.2** → [`runs/glm-5.2__applixus/scorecard.md`](../runs/glm-5.2__applixus/scorecard.md) · canlı demo: https://glm-5-2.applixus.com/
- **moonshotai/kimi-k2.7-code** → [`runs/moonshotai-kimi-k2.7-code__applixus/scorecard.md`](../runs/moonshotai-kimi-k2.7-code__applixus/scorecard.md) · canlı demo: https://kimi-2-7-code.applixus.com/ · maliyet: $1.45
- Ham 3-run örnekleri (opus/glm): `runs/*/rescore/` · özet: [`runs/rescore-analysis.json`](../runs/rescore-analysis.json)
