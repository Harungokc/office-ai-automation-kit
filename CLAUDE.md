# Office AI Automation Kit — AI Ajanlar İçin Kurulum Rehberi

Bu proje Claude Code, Cursor, Windsurf ve diğer AI ajanları ile çalışır.

## Hızlı Kurulum

```bash
# 1. Bu repoyu klonla
git clone https://github.com/Harungokc/office-ai-automation-kit.git
cd office-ai-automation-kit

# 2. Bağımlılıkları yükle (Python gerekliyse)
pip install -r requirements.txt

# 3. .env dosyasını oluştur
cp .env.example .env
# .env dosyasını kendi API anahtarlarınla doldur

# 4. n8n kur (Docker)
docker run -d \
  --name n8n \
  -p 5678:5678 \
  -v n8n_data:/home/node/.n8n \
  n8nio/n8n

# 5. Workflow import et → docs/N8N-KURULUM.md
# 6. MCP ekle (opsiyonel) → docs/MCP-KURULUM.md
```

## MCP Server Config'leri

> MCP server'lar hosted servislerdir. URL formunda eklenir.
> Ayrıntı: [`docs/MCP-KURULUM.md`](docs/MCP-KURULUM.md).

### Gmail MCP (hosted)
```bash
claude mcp add gmail https://gmail.mcp.so/
```

### Notion MCP (hosted)
```bash
claude mcp add notion https://notion.mcp.so/
```

### HubSpot MCP (hosted)
```bash
claude mcp add hubspot https://hubspot.mcp.so/
```

## Platform API Anahtarları

### Gmail / Google Calendar
1. [Google Cloud Console](https://console.cloud.google.com/) → OAuth2 Client oluştur
2. `GMAIL_CLIENT_ID`, `GMAIL_CLIENT_SECRET` → `.env`'e kaydet
3. n8n'de Google OAuth2 credential ayarla

### Notion
1. [notion.so/my-integrations](https://www.notion.so/my-integrations) → Yeni entegrasyon oluştur
2. Internal Integration Token al → `NOTION_TOKEN` → `.env`'e kaydet
3. İlgili Notion sayfalarına bağlantı yetkisi ver

### HubSpot
1. [developers.hubspot.com](https://developers.hubspot.com/) → Private App oluştur
2. `HUBSPOT_API_KEY` → `.env`'e kaydet
3. Scopes: `crm.objects.contacts.read`, `crm.objects.contacts.write`

### Claude API
1. [console.anthropic.com](https://console.anthropic.com/) → API Key al
2. `ANTHROPIC_API_KEY` → `.env`'e kaydet

## AI Ajan Komut Örnekleri

```bash
# Email otomasyonu
> "Gelen kutuma bak, acil olanları önceliklendir ve yanıtla"

# Toplantı özeti
> "Son toplantımın transkriptini al, action items çıkar"

# Doküman işleme
> "Bu faturaları oku, toplam tutarı hesapla"

# CRM veri girişi
> "Yeni lead'leri HubSpot'a otomatik kaydet"

# Raporlama
> "Bu haftanın satış raporunu hazırla, PDF olarak gönder"
```

## Klasör Yapısı

```
workflows/   → 5 n8n JSON workflow
skills/       → 5 Claude Code skill
prompts/      → 5 system prompt
mcp/          → MCP server config'leri
docs/         → Türkçe kurulum rehberleri
```
