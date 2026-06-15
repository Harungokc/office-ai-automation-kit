# Email Otomasyon Skill — Claude Code

## Konsept

Bu skill, Claude Code'a email yönetimi ve otomasyon yetenekleri kazandırır.
[langgraph-email-automation](https://github.com/kaymen99/langgraph-email-automation) (⭐258) projesinden ilham alır.

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
- `email_intent_classify` — Email intent'ini analiz et (LangGraph state machine pattern)
- `email_prioritize` — Email'leri önceliklendir
- `email_draft_response` — AI ile yanıt taslağı oluştur

## Prompt Template

```
"Email görevim:
1. Gelen kutusunu kontrol et
2. Email'leri öncelik sırasına koy (LangGraph intent classification)
3. Acil olanları işaretle
4. Otomatik yanıt verilebilecekleri yanıtla
5. Kullanıcının müdahalesi gerekenleri bildir

Hedef: Email yönetim süresini %60 azalt"
```

## Intent Sınıflandırması

| Intent | Açıklama | Otomatik Yanıt? | Referans |
|--------|----------|-----------------|---------|
| `toplanti_sor` | Toplantı talebi | Evet (takvim kontrolü ile) | langgraph-email-automation |
| `fiyat_sor` | Fiyat/sipariş sorusu | Evet | LangGraph RAG |
| `sikayet` | Şikayet/mağduriyet | Hayır (insan onayı) | — |
| `basit_soru` | Bilgi talebi | Evet | langgraph-email-automation |
| `geri_bildirim` | Geri bildirim | Koşullu | — |
| `diger` | Diğer | Hayır | — |

## AI Pipeline (LangGraph Pattern)

```
[Gmail Trigger]
  ↓
[AI - Intent Analizi] (Claude + LangGraph state machine)
  ├── Toplantı → Takvim kontrolü → Yanıt hazırla
  ├── Fiyat → Ürün bilgisi → Otomatik yanıt
  ├── Şikayet → Öncelikli etiket → İnsan devreye girsin
  └── Basit soru → AI otomatik yanıt
  ↓
[Gmail - Send Reply]
  ↓
[Slack/Email - Bildirim]
```

## Entegrasyonlar

- **Gmail API**: OAuth2 ile bağlantı
- **Claude API**: Intent analizi + yanıt üretimi
- **LangGraph** (opsiyonel): Çoklu ajan pipeline'ı için — [kaymen99/langgraph-email-automation](https://github.com/kaymen99/langgraph-email-automation)
- **n8n**: Workflow tetikleyici olarak (workflows/1-email-otomasyon.json)
