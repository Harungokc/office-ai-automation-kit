# Toplantı & Takvim Skill — Claude Code

## Konsept

Bu skill, Claude Code'a takvim ve toplantı yönetimi yetenekleri kazandırır.
[AI-Powered-Meeting-Summarizer](https://github.com/AI-Powered-Meeting-Summarizer) (⭐150) ve
[Meeting-Summary-Generator](https://github.com/Meeting-Summary-Generator) (⭐53) projelerinden ilham alır.

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
- `meeting_transcript` — Toplantı transkriptini al (Whisper + Fireflies/Otter)
- `meeting_summarize` — Transkripti analiz et, özet çıkar (GPT/Claude)
- `meeting_action_items` — Action items'ları belirle (AI extraction)

### Notion Entegrasyonu
- `notion_create_page` — Notion'da yeni sayfa oluştur
- `notion_append_block` — Notion sayfasına içerik ekle
- `notion_search` — Notion'da ara

## Prompt Template

```
"Toplantı görevim:
1. Bugünkü/yaklaşan toplantıları listele
2. Transkript varsa al (Whisper)
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

## AI Pipeline

```
[Schedule / Google Calendar Trigger]
  ↓
[Google Calendar - Yaklaşan toplantıları çek]
  ↓
[Whisper / Fireflies API - Transkript çek]
  ↓
[Claude/GPT - Özet + Action Items çıkar]
  ↓
[Notion - Toplantı notu kaydet]
  ↓
[Email - Katılımcılara özet gönder]
```

## Referans Projeler

| Proje | ⭐ | Katkı |
|-------|----|-------|
| [AI-Powered-Meeting-Summarizer](https://github.com/AI-Powered-Meeting-Summarizer) | 150 | Whisper + GPT tabanlı toplantı özeti |
| [Meeting-Summary-Generator](https://github.com/Meeting-Summary-Generator) | 53 | Kararlar, action items, tartışma noktaları |
| [fathom-mcp](https://github.com/search?q=fathom+mcp) | 15 | Cursor'dan Fathom transkriptlerine MCP erişimi |
| [MeetSummAIzer-AzureOpenAI](https://github.com/MeetSummAIzer-AzureOpenAI) | 16 | Teams/Skype .docx → AI özet |
