# n8n Workflow Kurulum Rehberi

Bu rehber, `workflows/` klasöründeki JSON dosyalarını n8n'ye import etmenizi ve çalıştırmanızı sağlar.

---

## workflow Dosyaları

| Dosya | Otomasyon | Açıklama |
|-------|----------|----------|
| `1-email-otomasyon.json` | Email | Gelen email önceliklendirme + AI yanıt + takip hatırlatıcı |
| `2-toplanti-takvim.json` | Toplantı | Otomatik planlama + Fireflies transkript + özet |
| `3-dokuman-isleme.json` | Doküman | Fatura/sözleşme okuma + veri çıkarma + Notion kaydetme |
| `4-veri-girisi-crm.json` | Veri Girişi | Webform → HubSpot CRM otomatik kayıt |
| `5-raporlama.json` | Raporlama | Haftalık/aylık rapor → PDF → email gönderim |

---

## Import Adımları

### 1. n8n'yi aç
```
http://localhost:5678
```

### 2. Workflow import et
```
Sol menü → Workflows
Sağ üst → "..." menü → Import from File
```

### 3. JSON dosyasını seç
```
workflows/1-email-otomasyon.json
```

### 4. Credentials ayarla

Her workflow'da `credentials/` bölümünde tanımlı hesaplar var.
Import ettikten sonra **kırmızı uyarı** görürsen:

1. Workflow'u aç
2. Kırmızı credential'ı tıkla
3. Açılan pencerede gerekli bilgileri doldur:
   - **Google OAuth2 API**: Client ID + Secret (KURULUM.md Adım 3)
   - **HubSpot API**: Private App Token (KURULUM.md Adım 5)
   - **Claude API**: API Key (KURULUM.md Adım 6)

### 5. Activate et
```
Aktif değilse → "Activate" butonuna tıkla
```

---

## Workflow Detayları

### Workflow 1: Email Otomasyonu

**Trigger:** Gmail - Email received (polling her 5 dakika)

**Akış:**
```
[Gmail Trigger]
  ↓
[AI - Intent Analizi] (Claude API)
  ├── Toplantı isteği → Takvim kontrolü → Yanıt hazırla
  ├── Fiyat sorusu → Ürün bilgisi → Otomatik yanıt
  ├── Şikayet → Öncelikli etiket → İnsan devreye girsin
  └── Basit soru → AI otomatik yanıt
  ↓
[Gmail - Send Reply]
  ↓
[Slack/Email - Bildirim]
```

**Credential:** Google OAuth2 API (Gmail)

---

### Workflow 2: Toplantı & Takvim

**Trigger:** Schedule (her saat veya günlük)

**Akış:**
```
[Schedule Trigger]
  ↓
[Google Calendar - Yaklaşan toplantıları çek]
  ↓
[Fireflies API - Transkript çek] (varsa)
  ↓
[AI - Özet + Action Items çıkar] (Claude API)
  ↓
[Notion - Toplantı notu kaydet]
  ↓
[Email - Katılımcılara özet gönder]
```

**Credential:** Google OAuth2 API, Claude API

---

### Workflow 3: Doküman İşleme

**Trigger:** Email - Yeni fatura/sözleşme (belirli label)

**Akış:**
```
[Email Trigger - Fatura label]
  ↓
[Email - Attachment çek]
  ↓
[Rossum API - Fatura verisi çıkar] VEYA [Claude PDF - İçerik okuma]
  ↓
[AI - Veri yapılandır] (Claude API)
  ↓
[Notion - Fatura kaydet]
  ↓
[Google Sheets - Rapor tablosuna ekle]
```

**Credential:** Gmail, Claude API, Rossum API (opsiyonel)

---

### Workflow 4: Veri Girişi & CRM

**Trigger:** Webhook (harici form'dan) VEYA Schedule (CRM'den periyodik çekme)

**Akış:**
```
[Webhook Trigger] VEYA [Schedule + HubSpot API]
  ↓
[AI - Veri temizleme + doğrulama] (Claude API)
  ↓
[HubSpot - Create/Update Contact]
  ↓
[Email - Otomatik teşekkür yanıtı]
  ↓
[Slack - Yeni lead bildirimi]
```

**Credential:** HubSpot API, Gmail, Claude API

---

### Workflow 5: Raporlama

**Trigger:** Schedule (her Cuma 17:00)

**Akış:**
```
[Schedule - Haftalık]
  ↓
[Google Sheets - Veri çek]
  ↓
[AI - Rapor oluştur] (Claude API)
  ├── Bu hafta kaç satış?
  ├── Geçen hafta ile karşılaştırma
  ├── En iyi performans gösterenler
  └── Önümüzdeki hafta önerileri
  ↓
[PDF - Rapor formatla]
  ↓
[Email - İlgili kişilere gönder]
```

**Credential:** Google OAuth2 API, Claude API, Gmail

---

## Aktif/Pasif Geçiş

n8n'de workflow'u aç → sağ üstteki **Active/Pause** toggle'ı:

- **Active:** Otomatik çalışır (schedule veya tetikleyiciye göre)
- **Paused:** Durdurulur, elle tetiklenebilir

---

## Elle Tetikleme

Workflow'u test etmek için:
1. Workflow'u **Paused** durumuna al
2. "Run Workflow" → "Test Workflow" tıkla
3. Sonucu "Execution Tree" gör

---

## Log İzleme

```
Sol menü → Executions
→ Son çalışma tarihi, süresi, hata varsa detay
```

---

## Sorunlar

| Sorun | Çözüm |
|-------|-------|
| Credential kırmızı | Credential ayarlarını kontrol et |
| Workflow çalışmıyor | Executions → Hata detayını oku |
| Email gönderilmiyor | Gmail OAuth2 yeniden yetkilendir |
| AI yanıt vermiyor | Claude API key doğru mu? |
| HubSpot kaydı atlanıyor | API key yetkilerini kontrol et |

Detaylı → [`TROUBLESHOOTING.md`](TROUBLESHOOTING.md)
