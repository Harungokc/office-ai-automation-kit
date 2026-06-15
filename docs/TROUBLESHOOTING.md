# Troubleshooting — Sık Karşılaşılan Hatalar

---

## n8n Kurulumu

### ❌ "Port 5678 already in use"
```bash
# Başka bir uygulama port kullanıyor
netstat -ano | findstr :5678
# PID'i bul → görev yöneticisinden kapat
# VEYA farklı port kullan:
docker run -d --name n8n -p 5679:5678 n8nio/n8n
# → http://localhost:5679 olarak eriş
```

### ❌ "Docker daemon is not running"
```bash
# Windows/Mac: Docker Desktop'u aç
# Linux:
sudo systemctl start docker
```

### ❌ n8n açılışta beyaz ekran
```bash
# Cookie ayarı eksik
docker stop n8n
docker rm n8n
docker run -d \
  --name n8n \
  -p 5678:5678 \
  -v n8n_data:/home/node/.n8n \
  -e N8N_SECURE_COOKIE=false \
  n8nio/n8n
```

---

## Google OAuth2

### ❌ "invalid_client: The OAuth client was not found"
1. [console.cloud.google.com](https://console.cloud.google.com/) → Credentials
2. OAuth 2.0 Client ID'nin bilgilerini kontrol et
3. Client ID + Secret `.env`'de doğru kaydedilmiş mi?

### ❌ "redirect_uri_mismatch"
1. Google Cloud Console → Credentials → OAuth 2.0 Client
2. "Authorized redirect URIs" → `http://localhost:5678/oauth2/callback` ekle
3. Save → tekrar dene

### ❌ "This app isn't verified" uyarısı
1. Google hesabıyla giriş yap
2. "Advanced" → "Go to [site] (unsafe)" tıkla
3. Yetkilendirmeyi ver

---

## n8n Workflow

### ❌ Workflow "Paused" durumunda kalıyor
- Trigger node'a bak — tetikleyici doğru mu?
- Gmail trigger: Email geldi mi?
- Schedule trigger: Doğru saat mi ayarlı?

### ❌ "Credentials not found" hatası
1. Workflow → kırmızı credential node'u tıkla
2. Açılan pencerede credential'ı yeniden ayarla
3. Veya yeni credential oluştur

### ❌ Email gönderilmiyor
```bash
# Gmail: "Less secure apps" yerine App Password kullan
# 1. Google Account → Security → 2-Step Verification aç
# 2. App Passwords → yeni password oluştur
# 3. n8n credential'da şifre yerine App Password kullan
```

### ❌ HubSpot kaydı oluşturulmuyor
- API key yetkilerini kontrol et (scopes)
- `crm.objects.contacts.write` aktif mi?
- Rate limit aşıldı mı? (15 dakikada 100 istek)

---

## Claude API

### ❌ "Invalid API key" hatası
1. [console.anthropic.com](https://console.anthropic.com/) → API Keys
2. Key'in aktif olduğunu kontrol et
3. `.env`'de `ANTHROPIC_API_KEY=sk-ant-...` doğru mu?

### ❌ "Rate limit exceeded"
- Yapılan istek sayısını azalt
- Workflow'da delay node kullan
- Daha ucuz model kullan (haiku-sonnet mi opus mu)

### ❌ "Context length exceeded"
- Gönderilen email/veri çok uzun
- Workflow'da metin kısaltma adımı ekle
- Claude API max token sınırını kontrol et

---

## Notion

### ❌ "Bearer token missing" hatası
1. [notion.so/my-integrations](https://www.notion.so/my-integrations)
2. Integration'ı seç → Secret tekrar al
3. n8n credential'da token doğru mu?

### ❌ "Could not find page" hatası
1. Notion'da sayfayı aç
2. "..." menüsü → Connections → "Office AI Kit" ekle
3. Sayfaya erişim yetkisi ver

---

## Genel

### ❌ "Connection refused" (localhost:5678)
```bash
# n8n container çalışıyor mu?
docker ps | grep n8n

# Çalışmıyorsa başlat
docker start n8n

# Log kontrol
docker logs n8n
```

### ❌ Workflow timeout (30 saniye aşıldı)
- n8n ayarlarında timeout süresini artır
- Veya workflow'u parçalara böl (önce veri çek, sonra işle)
- Asenkron execution kullan

### ❌ JSON import hatası
- JSON formatı bozuk olabilir
- [jsonlint.com](https://jsonlint.com) ile doğrula
- Workflow JSON geçerli n8n v1 formatında olmalı

---

## Hata Kaydı

Bir hata aldığında, sorunu çözmek için şu bilgileri topla:

1. **Hata mesajı:** Tam olarak ne diyor?
2. **Hangi workflow:** Workflow 1, 2, 3, 4, 5?
3. **Hangi adımda:** Workflow Execution Tree'de hangi node'da hata verdi?
4. **n8n log:** `docker logs n8n` çıktısı

---

## Yardım Almak

1. [n8n.io/docs](https://docs.n8n.io/) → Resmi dokümantasyon
2. [community.n8n.io](https://community.n8n.io/) → Forum
3. [GitHub Issues](https://github.com/n8n-io/n8n/issues) → Hata raporu

---

## Sorunuz Çözülmedi Mi?

Bir GitHub Issue açın:
- Hata mesajı
- Workflow adı
- Adımlar (ne yapmaya çalışıyordunuz)
- Log çıktısı
