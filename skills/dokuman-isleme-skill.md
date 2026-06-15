# Doküman İşleme Skill — Claude Code

## Konsept

Bu skill, Claude Code'a doküman okuma ve veri çıkarma yetenekleri kazandırır.
[open-semantic-etl](https://github.com/open-semantic-etl/open-semantic-etl) (⭐281) projesinden ilham alır.

## Kullanım

```bash
claude "Bu faturadaki toplam tutarı bul"
claude "Sözleşmedeki riskli maddeleri işaretle"
claude "PDF'ten tüm verileri çıkar"
claude "Fatura verilerini Notion'a kaydet"
```

## Araçlar

### Doküman Okuma
- `document_read_pdf` — PDF dosyasını oku
- `document_extract_text` — Metin çıkar
- `document_scan_image` — Görsel/taranmış doküman oku (OCR)

### Fatura İşleme
- `invoice_parse` — Fatura verilerini çıkar
- `invoice_validate` — Fatura bilgilerini doğrula
- `invoice_total` — Toplam tutarı hesapla

### Sözleşme Analizi
- `contract_parse` — Sözleşme maddelerini çıkar
- `contract_risk_flag` — Riskli maddeleri işaretle
- `contract_summary` — Sözleşme özetini çıkar

### Kayıt
- `notion_append` — Notion'a kaydet
- `sheets_append_row` — Google Sheets'e satır ekle

## Prompt Template

```
"Doküman analiz görevim:
1. PDF/görsel dosyayı oku (OCR + LLM pipeline)
2. Yapılandırılmış veri çıkar
3. Eksik/şaşırtıcı bilgileri işaretle
4. Notion'a kaydet

Fatura için: fatura no, tarih, tedarikçi, kalemler, toplam tutar
Sözleşme için: taraflar, maddeler, riskli noktalar, son tarihler"
```

## AI Pipeline (ETL Pattern)

```
[Email / Webhook - Doküman geldi]
  ↓
[OCR - Görsel/taranmış dosya oku]
  ↓
[LLM - İçerik çıkarma + yapılandırma]
  ↓
[N8N / Claude - Veri doğrulama]
  ↓
[Notion - Kayıt]
  ↓
[Google Sheets - Rapor tablosuna ekle]
```

## Fatura Veri Formatı

```json
{
  "fatura_no": "...",
  "tarih": "GG.AA.YYYY",
  "tedarikci": "...",
  "toplam_tutar": 0.00,
  "kur": "TL",
  "kalemler": [
    {"aciklama": "...", "adet": N, "birim_fiyat": 0.00, "toplam": 0.00}
  ],
  "durum": "bekliyor|onaylandi|odendi"
}
```

## Referans Projeler

| Proje | ⭐ | Katkı |
|-------|----|-------|
| [open-semantic-etl](https://github.com/open-semantic-etl/open-semantic-etl) | **281** | Python ETL — PDF/OCR, Named Entity Recognition, veri zenginleştirme |
| [pdf-extraction-agenda](https://github.com/pdf-extraction-agenda) | **98** | PDF → Markdown pipeline |
| [bookllm](https://github.com/bookllm) | **26** | LLM tabanlı kitap/doküman çeviri + glossar extraction |
| [ocr-pdf-extraction-regex-vs-llm](https://github.com/ocr-pdf-extraction-regex-vs-llm) | **7** | Geleneksel regex vs LLM karşılaştırması |
| [docflow.ai](https://github.com/docflow.ai) | **3** | LLM ile doküman Q&A pipeline |

## Entegrasyonlar

- **Rossum API**: Fatura OCR (opsiyonel, €3/fatura)
- **Claude API**: PDF okuma, veri çıkarma
- **Notion API**: Kayıt
- **Google Sheets**: Fatura tablosu
- **n8n**: Workflow (workflows/3-dokuman-isleme.json)
