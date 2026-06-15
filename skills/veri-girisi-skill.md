# Veri Girişi & CRM Skill — Claude Code

## Konsept

Bu skill, Claude Code'a CRM ve veri girişi otomasyonu yetenekleri kazandırır.
Webform verilerini alır, doğrular, CRM'e kaydeder ve takip bildirimleri gönderir.

## Kullanım

```bash
claude "Yeni lead'leri HubSpot'a kontrol et"
claude "Bu form verisini temizle ve CRM'e kaydet"
claude "Bu haftaki yeni müşterileri listele"
claude "Müşteri bilgilerini güncelle"
```

## Araçlar

### CRM Yönetimi
- `hubspot_create_contact` — Yeni contact oluştur
- `hubspot_update_contact` — Contact güncelle
- `hubspot_search_contact` — Contact ara
- `hubspot_get_deals` — Deal'ları getir

### Veri Doğrulama
- `data_validate_email` — Email format doğrulama
- `data_validate_phone` — Telefon doğrulama
- `data_clean` — Veri temizleme (boşluk, format)

### Bildirim
- `slack_send` — Slack'e mesaj gönder
- `email_send` — Email gönder
- `email_thank_you` — Otomatik teşekkür emaili

## Prompt Template

```
"CRM görevim:
1. Webform/email'den veri al
2. AI ile doğrula ve temizle
3. CRM'e kaydet ( HubSpot / Notion)
4. Düşük güvenilirlik → insan onayına gönder
5. Yüksek güvenilirlik → otomatik teşekkür + Slack bildirimi

Hedef: Veri girişi süresini %100 azalt"
```

## Lead Güvenilirlik Skoru

| Skor | Açıklama | Aksiyon |
|------|----------|---------|
| `yuksek` | Tüm bilgiler mevcut, email doğru, şirket geçerli | Otomatik CRM kaydı |
| `orta` | Eksik bilgi var ama email doğru | CRM kaydı + işaretle |
| `düşük` | Email yanlış veya bilgiler eksik | İnsan onayı bekle |

## Veri Çıkış Formatı

```json
{
  "contact": {
    "email": "...",
    "firstname": "...",
    "lastname": "...",
    "phone": "...",
    "company": "...",
    "lead_source": "Web Form",
    "guvenilirlik": "yuksek|orta|dusuk"
  },
  "action": "auto|manual",
  "bildirim": "email|slack|both|none"
}
```

## Entegrasyonlar

- **HubSpot API**: CRM kayıtları
- **Notion API**: Alternatif CRM
- **Gmail API**: Email bildirimleri
- **Slack API**: Ekip bildirimleri
- **Claude API**: Veri doğrulama
- **n8n**: Workflow (workflows/4-veri-girisi-crm.json)
