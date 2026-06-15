# Veri Girişi & CRM Skill — Claude Code

## Konsept

Bu skill, Claude Code'a CRM ve veri girişi otomasyonu kazandırır.
[HubSpot MCP](https://github.com/search?q=hubspot+mcp+automation) projelerinden ilham alır.

## Kullanım

```bash
claude "Yeni müşteri ekle: Ahmet Yılmaz, firma XYZ, email ahmet@xyz.com"
claude "Bugünkü lead'leri HubSpot'a sync et"
claude "Firma XXX'in iletişim bilgilerini güncelle"
claude "Bu email'deki lead'i CRM'e kaydet"
```

## Araçlar

### CRM Yönetimi
- `hubspot_create_contact` — Yeni kişi oluştur
- `hubspot_update_contact` — Kişi güncelle
- `hubspot_search_contact` — Kişi ara
- `hubspot_create_deal` — Fırsat oluştur
- `hubspot_update_deal_stage` — Fırsat aşamasını güncelle

### Form Processing
- `form_parse` — Webform verilerini çıkar
- `form_to_crm` — Form verilerini CRM'e kaydet
- `email_parse_lead` — Email'den lead bilgisi çıkar

### Entegrasyon
- `notion_append` — Notion'a kaydet
- `sheets_append_row` — Google Sheets'e ekle
- `email_send` — Email gönder (onay/takip)

## Prompt Template

```
"CRM görevim:
1. Gelen veriyi al (form, email, webhook)
2. Lead bilgisini çıkar
3. HubSpot'da kişi/firma kontrolü yap
4. Varsa güncelle, yoksa oluştur
5. Fırsat varsa ilgili deal'a bağla
6. Onay emaili gönder

Hedef: Manuel veri girişini %100 otomatik yap"
```

## Lead Processing Pipeline

```
[Webform / Email / LinkedIn mesajı]
  ↓
[Claude - Lead bilgi çıkarma]
  ↓
[HubSpot - Mevcut kişi kontrolü (email ile)]
  ├── Varsa → Güncelle
  └── Yoksa → Yeni kişi oluştur
  ↓
[Deal oluştur (opsiyonel)]
  ↓
[Notion'a kaydet]
  ↓
[Email - Onay bildirimi]
```

## CRM Alan Mapping

| Form Alanı | HubSpot Alanı |
|------------|---------------|
| Ad Soyad | firstname + lastname |
| Email | email |
| Telefon | phone |
| Firma | company |
| Mesaj | message |
| Kaynak | hs_analytics_source |

## Referans Projeler

| Proje | ⭐ | Katkı |
|-------|----|-------|
| [mcp-servers](https://github.com/search?q=mcp+servers+hubspot) | **3** | 24 Enterprise MCP Server — HubSpot, Salesforce, Power BI |
| [CRM-Updater-via-call-transcript](https://github.com/CRM-Updater-via-call-transcript-Claude-Skill) | **2** | Görüşme transkriptinden CRM güncelleme |
| [crmsync](https://github.com/crmsync) | **0** | HubSpot/Pipedrive/Salesforce bidirectional sync |
| [n8n-crm-automation-workflows](https://github.com/search?q=n8n+crm+automation) | **0** | n8n CRM otomasyon workflow'ları |

## Entegrasyonlar

- **HubSpot API**: CRM işlemleri
- **Notion API**: Kayıt
- **Google Sheets**: Veri tablosu
- **n8n**: Workflow (workflows/4-veri-girisi-crm.json)
