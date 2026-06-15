# Raporlama Skill — Claude Code

## Konsept

Bu skill, Claude Code'a otomatik raporlama yetenekleri kazandırır.
Veri kaynaklarından (Sheets, CRM, Email) çeker, AI ile analiz eder ve profesyonel rapor üretir.

## Kullanım

```bash
claude "Bu haftanın satış raporunu oluştur"
claude "Aylık performans raporu hazırla"
claude "Raporu PDF olarak kaydet"
claude "CEO'ya email ile gönder"
```

## Araçlar

### Veri Çekme
- `sheets_read` — Google Sheets'ten veri çek
- `sheets_get_metrics` — Belirli metrikleri al
- `hubspot_get_report` — HubSpot rapor verisi al
- `email_fetch_data` — Email'den veri çek

### Rapor Üretimi
- `report_generate` — AI ile rapor oluştur
- `report_compare` — Dönem karşılaştırması yap
- `report_forecast` — Tahmin raporu oluştur

### Çıktı
- `report_save_pdf` — PDF olarak kaydet
- `report_send_email` — Email ile gönder
- `notion_save` — Notion'a arşivle

## Prompt Template

```
"Rapor görevim:
1. Google Sheets / HubSpot'tan veri çek
2. AI ile analiz et
3. Haftalık/aylık karşılaştırma yap
4. Action items belirle
5. Markdown/PDF formatında rapor üret

Rapor bölümleri:
1. Özet (2-3 cümle)
2. Metrikler (Tablo)
3. Karşılaştırma (Bu dönem vs Önceki dönem)
4. En iyi performans gösterenler
5. Dikkat noktaları
6. Öneriler (3 madde)"
```

## Rapor Formatı

```markdown
# 📊 [Rapor Adı]

**Dönem:** [Tarih aralığı]
**Hazırlayan:** AI Otomasyon
**Tarih:** [GG.AA.YYYY]

---

## 1. Özet
[2-3 cümle]

## 2. Metrikler

| Metrik | Bu Dönem | Önceki Dönem | Değişim |
|--------|----------|--------------|---------|
| ... | ... | ... | ...% |

## 3. Karşılaştırma
[Değişim analizi]

## 4. En İyi Performans
- ...
- ...

## 5. Dikkat Noktaları
- ...

## 6. Önümüzdeki Dönem Önerileri
1. ...
2. ...
3. ...
```

## Entegrasyonlar

- **Google Sheets API**: Veri kaynağı
- **HubSpot API**: CRM verileri
- **Notion API**: Rapor arşivi
- **Gmail API**: Rapor gönderimi
- **Claude API**: Rapor üretimi
- **n8n**: Workflow (workflows/5-raporlama.json)
