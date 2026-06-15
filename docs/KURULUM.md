# Kurulum Rehberi — Sıfırdan Office AI Automation Kit

Bu rehber, hiçbir şey kurulu olmadan başlayıp 5 otomasyonu tam çalışır hale getirmeniz içindir.

---

## 🗺️ Genel Bakış — Neler Kurulacak?

```
Adım 1: Docker kurulumu
Adım 2: n8n kurulumu
Adım 3: Google hesabı + OAuth2 (Gmail + Calendar)
Adım 4: Notion entegrasyonu
Adım 5: HubSpot entegrasyonu
Adım 6: Claude API key
Adım 7: Workflow import
Adım 8: İlk otomasyonu çalıştır
```

---

## Adım 1: Docker Kurulumu

### Windows
1. [docker.com](https://www.docker.com/) → "Download Desktop for Windows"
2. İndirilen `.exe` dosyasını çalıştır
3. Kurulum sırasında "WSL 2 backend" seçeneğini işaretle
4. Bilgisayarı yeniden başlat
5. Docker Desktop'u aç

### Mac
```bash
brew install --cask docker
```

### Linux
```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

### Kurulum doğrulama
```bash
docker --version
# → Docker version 20.x.x veya üzeri görüyorsan tamam
docker run hello-world
```

---

## Adım 2: n8n Kurulumu

```bash
# n8n çalıştır (arka planda)
docker run -d \
  --name n8n \
  -p 5678:5678 \
  -v n8n_data:/home/node/.n8n \
  -e N8N_SECURE_COOKIE=false \
  n8nio/n8n

# Çalışıyor mu kontrol et
# → http://localhost:5678 aç (tarayıcıda)
```

**İlk ayar:**
1. Açılan sayfada hesap oluştur (email + şifre)
2. Settings → Workers Mode → Single instance (varsayılan kalabilir)

---

## Adım 3: Google OAuth2 Kurulumu (Gmail + Calendar)

### 3.1: Google Cloud Console'da proje oluştur
1. [console.cloud.google.com](https://console.cloud.google.com/) → "Select a project" → "New Project"
2. Proje adı: `office-ai-kit`
3. Create → Projeyi seç

### 3.2: API'leri etkinleştir
1. "APIs & Services" → "Library"
2. Ara ve etkinleştir:
   - **Gmail API**
   - **Google Calendar API**
   - **Google Sheets API**

### 3.3: OAuth2 Client oluştur
1. "APIs & Services" → "Credentials" → "Create Credentials" → "OAuth client ID"
2. Application type: **Web application**
3. Name: `Office AI Kit`
4. Authorized redirect URIs:
   ```
   http://localhost:5678/oauth2/callback
   ```
5. Create → **Client ID** ve **Client Secret** alın

### 3.4: .env dosyasına kaydet
```bash
# .env dosyasını düzenle
GMAIL_CLIENT_ID=senin-client-id
GMAIL_CLIENT_SECRET=senin-client-secret
GOOGLE_REDIRECT_URI=http://localhost:5678/oauth2/callback
```

---

## Adım 4: Notion Entegrasyonu

### 4.1: Notion Integration oluştur
1. [notion.so/my-integrations](https://www.notion.so/my-integrations) → "New integration"
2. Name: `Office AI Kit`
3. Associated workspace: Senin workspace'ın
4. Type: **Internal**
5. Submit → **Integration Token** alın

### 4.2: Token'ı kaydet
```bash
NOTION_TOKEN=secret_xxxxxx
```

### 4.3: Notion sayfasına yetki ver
1. Notion'da kullanmak istediğin sayfayı aç
2. "..." menüsü → "Connections" → "Add a connection"
3. "Office AI Kit" seç → Confirm

---

## Adım 5: HubSpot Entegrasyonu

### 5.1: Private App oluştur
1. [developers.hubspot.com](https://developers.hubspot.com/) → Account → Dashboards
2. "Apps" → "Private Apps" → "Create a private app"
3. Name: `Office AI Kit`
4. Scopes (gerekli minimum):
   - `crm.objects.contacts.read`
   - `crm.objects.contacts.write`
   - `crm.objects.companies.read`
5. Save → **Access Token** alın

### 5.2: Token'ı kaydet
```bash
HUBSPOT_API_KEY=pat-na1-xxxxxx
```

---

## Adım 6: Claude API Key

1. [console.anthropic.com](https://console.anthropic.com/) → Settings → API Keys
2. "Create Key" → İsim: `Office AI Kit`
3. Copy → **API Key** alın

```bash
ANTHROPIC_API_KEY=sk-ant-xxxxxx
```

---

## Adım 7: Workflow Import

n8n'ye workflow'ları import et:

1. [http://localhost:5678](http://localhost:5678) → aç
2. Sol menü → "Workflows" → "Import from File" (üst sağdaki "..." menüsü)
3. `workflows/1-email-otomasyon.json` dosyasını seç
4. Credentials ayarla (Google OAuth2, HubSpot, Claude API)
5. "Activate" butonuna bas → **PAUSED** durumundan **ACTIVE** geçer

**Her workflow için aynı adımları tekrarla:**
- `workflows/2-toplanti-takvim.json`
- `workflows/3-dokuman-isleme.json`
- `workflows/4-veri-girisi-crm.json`
- `workflows/5-raporlama.json`

---

## Adım 8: İlk Otomasyonu Çalıştır

### Email Otomasyonu (En Kolay Başlangıç)
1. Workflow 1 → "Active" durumunda olmalı
2. Gmail'e test email'i gönder
3. 1-2 dakika içinde n8n email'i işler
4. n8n logs → "Executions" → Sonucu gör

### Doğrulama
```bash
# n8n container log'larını izle
docker logs -f n8n
```

---

## 🚨 Sorun Olursa

| Sorun | Çözüm |
|-------|-------|
| n8n açılmıyor | `docker logs n8n` → hata mesajını oku |
| Google OAuth hatası | Redirect URI doğru mu? `http://localhost:5678/oauth2/callback` |
| Workflow çalışmıyor | n8n "Execution History" → hata detayını gör |
| Credential kırmızı | OAuth2 tekrar yetkilendir, token süresi dolmuş olabilir |

Detaylı sorunlar → [`TROUBLESHOOTING.md`](TROUBLESHOOTING.md)

---

## ✅ Kurulum Tamamlandığında

Artık 5 otomasyon aktif:
- 📧 Email önceliklendirme + AI yanıt
- 📅 Toplantı planlama + transkript özet
- 📄 Fatura/sözleşme okuma
- 📊 Webform → CRM otomatik kayıt
- 📈 Haftalık/aylık rapor

Hepsini `docs/N8N-KURULUM.md` ve `docs/MCP-KURULUM.md` dosyalarında detaylıca bulacaksın.
