# Toplantı & Takvim Skill — Claude Code

## Konsept

Bu skill, Claude Code'a takvim ve toplantı yönetimi yetenekleri kazandırır.
Toplantıları planlar, transkriptleri analiz eder, özet çıkarır ve Notion'a kaydeder.

## Kullanım

```bash
claude "Yarın 14:00'te Mümtaz ile toplantı ayarla"
claude "Bu haftaki toplantılarımı listele"
claude "Son toplantımın action items'larını çıkar"
claude "Toplantı özetini Notion'a kaydet"
```

## Araçlar

### Takvim Yönetimi
- `calendar_list_events` — Takvimdeki toplantıları listele
- `calendar_create_event` — Yeni toplantı oluştur
- `calendar_update_event` — Toplantıyı güncelle
- `calendar_delete_event` — Toplantıyı sil

### Toplantı Analizi
- `meeting_transcript` — Toplantı transkriptini al (Fireflies/Otter)
- `meeting_summarize` — Transkripti analiz et, özet çıkar
- `meeting_action_items` — Action items'ları belirle

### Notion Entegrasyonu
- `notion_create_page` — Notion'da yeni sayfa oluştur
- `notion_append_block` — Notion sayfasına içerik ekle
- `notion_search` — Notion'da ara

## Prompt Template

```
"Toplantı görevim:
1. Bugünkü/yaklaşan toplantıları listele
2. Transkript varsa al
3. AI ile özet + action items çıkar
4. Notion'a kaydet
5. Katılımcılara email gönder

Hedef: Toplantı notu yazma süresini 0'a indir"
```

## Toplantı Özet Formatı

```
## 📋 Toplantı Özeti

**Konu:** [Toplantı adı]
**Tarih:** [GG.AA.YYYY]
**Katılımcılar:** [İsimler]
**Süre:** [Dakika]

### 🎯 Alınan Kararlar
- [Karar 1]
- [Karar 2]

### ✅ Action Items
- [Kişi] → [Görev] (son tarih)
- [Kişi] → [Görev] (son tarih)

### 📌 Takip
- [Takip edilecek konu]
```

## Entegrasyonlar

- **Google Calendar API**: Toplantı verisi
- **Fireflies.ai / Otter.ai**: Transkript
- **Notion API**: Özet kayıt
- **Claude API**: Özet + action items üretimi
- **n8n**: Workflow (workflows/2-toplanti-takvim.json)
