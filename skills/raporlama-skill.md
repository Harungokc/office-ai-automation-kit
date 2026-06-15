# Raporlama Skill — Claude Code

## Konsept

Bu skill, Claude Code'a haftalık/aylık otomatik raporlama kazandırır.
[business-intelligence-dashboard](https://github.com/search?q=business+intelligence+dashboard+automation) (⭐6) ve
[data-engineering-portfolio](https://github.com/search?q=data+engineering+portfolio+bi) projelerinden ilham alır.

## Kullanım

```bash
claude "Bu haftanın satış raporunu hazırla"
claude "Aylık CRM raporunu PDF olarak gönder"
claude "Performans dashboardunu güncelle"
claude "Raporu stakeholder'lara email ile gönder"
```

## Araçlar

### Veri Çekme
- `sheets_read` — Google Sheets'ten veri çek
- `hubspot_get_deals` — CRM'den fırsat verisi çek
- `email_fetch` — Email'lerden metrik çek

### Rapor Oluşturma
- `report_generate_text` — Metin tabanlı rapor oluştur
- `report_generate_markdown` — Markdown formatında rapor
- `report_generate_pdf` — PDF rapor oluştur
- `report_generate_chart` — Grafik/chart oluştur

### Dağıtım
- `email_send_report` — Raporu email ile gönder
- `notion_create_page` — Notion'da rapor sayfası oluştur
- `slack_post` — Slack'e gönder

## Prompt Template

```
"Raporlama görevim:
1. Veri kaynaklarından (Sheets, CRM, Email) veri çek
2. AI ile analiz et — trendler, anomaliler, içgörüler
3. Yapılandırılmış rapor oluştur
4. PDF/HTML formatında kaydet
5. Stakeholder'lara email gönder

Hedef: Haftalık rapor hazırlama süresini 3 saat → 15 dakika"
```

## Rapor Şablonu

```markdown
# 📊 [Rapor Adı] — [Dönem]

**Tarih:** [GG.AA.YYYY]
**Hazırlayan:** Claude AI

---

## 📌 Yönetici Özeti
[Bir paragrafta en önemli 3 bulgu]

## 📈 Temel Metrikler
| Metrik | Bu Dönem | Geçen Dönem | Değişim |
|--------|----------|-------------|---------|
| ... | ... | ... | ↑/↓ %X |

## 🔍 Detaylı Analiz
[Metrik bazlı detaylı açıklama]

## ⚠️ Dikkat Gerektiren Noktalar
[Olası sorunlar, riskler]

## ✅ Öneriler
[AI tarafından üretilen öneriler]

## 📅 Sonraki Dönem Beklentileri
[Projeksiyonlar]
```

## ETL + Raporlama Pipeline

```
[Schedule (Haftalık/Aylık) - Cron trigger]
  ↓
[n8n - Veri kaynaklarından çek]
  ├── Google Sheets (satış verileri)
  ├── HubSpot (CRM pipeline)
  └── Email (müşteri geri bildirimleri)
  ↓
[Python/Pandas - Veri temizleme + birleştirme]
  ↓
[Claude API - AI analizi + içgörüler]
  ↓
[Markdown → PDF dönüştürme]
  ↓
[Email - Stakeholder'lara gönderim]
  ↓
[Notion - Arşivleme]
```

## Referans Projeler

| Proje | ⭐ | Katkı |
|-------|----|-------|
| [business-intelligence-dashboard](https://github.com/search?q=business+intelligence+dashboard) | **6** | End-to-end BI platformu — KPI, dashboard, otomatik raporlama |
| [data-engineering-portfolio](https://github.com/search?q=data+engineering+portfolio) | **5** | Data pipeline + Power BI raporlama |
| [Azure-Data-Engineering-Project](https://github.com/Azure-Data-Engineering-Project) | **4** | ADF → Databricks → Synapse → Power BI pipeline |
| [Scalable-Data-Pipeline-Real-Time](https://github.com/Scalable-Data-Pipeline-Real-Time-Analytics-on-Azure) | **4** | Real-time analytics + Power BI |
| [End-to-End-Data-Engineering-Project](https://github.com/End-to-End-Data-Engineering-Project) | **3** | Bronze → Silver → Gold medallion architecture |

## Entegrasyonlar

- **Google Sheets API**: Veri çekme
- **HubSpot API**: CRM metrikleri
- **Claude API**: AI analizi
- **Notion API**: Arşivleme
- **n8n**: Workflow (workflows/5-raporlama.json)
