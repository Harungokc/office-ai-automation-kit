# Email Otomasyon Skill — Claude Code

## Konsept

Bu skill, Claude Code'a email yönetimi ve otomasyon yetenekleri kazandırır.
Gelen email'leri analiz eder, önceliklendirir, AI ile yanıtlar ve takip hatırlatıcıları yönetir.

## Kullanım

```bash
claude "Gelen kutuma bak, acil olanları önceliklendir"
claude "Son 5 email'i özetle"
claude "Bu email'e profesyonel bir yanıt hazırla"
claude "Cevaplanmayan email'lerimi kontrol et"
```

## Araçlar

### Email Okuma
- `gmail_read` — Gelen kutusunu oku, filtrele
- `gmail_search` — Email'leri ara (konu, gönderen, tarih)

### Email Gönderme
- `gmail_send` — Email gönder
- `gmail_reply` — Email'e yanıt ver
- `gmail_forward` — Email'i ilet

### Yönetim
- `gmail_label` — Email'e etiket ekle
- `gmail_archive` — Email'i arşivle
- `gmail_draft` — Taslak oluştur

### AI Analiz
- `email_intent_classify` — Email intent'ini analiz et
- `email_prioritize` — Email'leri önceliklendir
- `email_draft_response` — AI ile yanıt taslağı oluştur

## Prompt Template

```
"Email görevim:
1. Gelen kutusunu kontrol et
2. Email'leri öncelik sırasına koy
3. Acil olanları işaretle
4. Otomatik yanıt verilebilecekleri yanıtla
5. Kullanıcının müdahalesi gerekenleri bildir

Hedef: Email yönetim süresini %60 azalt"
```

## Intent Sınıflandırması

| Intent | Açıklama | Otomatik Yanıt? |
|--------|----------|-----------------|
| `toplanti_sor` | Toplantı talebi | Evet (takvim kontrolü ile) |
| `fiyat_sor` | Fiyat/sipariş sorusu | Evet |
| `sikayet` | Şikayet/mağduriyet | Hayır (insan onayı) |
| `basit_soru` | Bilgi talebi | Evet |
| `geri_bildirim` | Geri bildirim | Koşullu |
| `diger` | Diğer | Hayır |

## Entegrasyonlar

- **Gmail API**: OAuth2 ile bağlantı
- **Claude API**: Intent analizi + yanıt üretimi
- **n8n**: Workflow tetikleyici olarak (workflows/1-email-otomasyon.json)
