# MCP Kurulum Rehberi — Claude Code + Office AI Kit

Bu rehber, Claude Code'a MCP server'ları ekleyerek ofis araçlarını doğal dille yönetmenizi sağlar.

---

## MCP Nedir?

MCP (Model Context Protocol), AI asistanlarının dış araçlara erişmesini sağlayan bir protokoldür.
Bir kez kurduktan sonra şöyle komutlar verebilirsin:

```bash
# Email kontrol et
claude "Gelen kutuma bak, acil olanları önceliklendir"

# Toplantı planla
claude "Yarın 14:00'te Mümtaz ile toplantı ayarla"

# Notion'a not ekle
claude "Bu toplantı notlarını Notion'a 'Toplantılar' sayfasına kaydet"

# HubSpot'tan lead bilgisi al
claude "son haftanın yeni lead'lerini HubSpot'tan çek"
```

---

## Desteklenen MCP Server'lar

| Araç | MCP Server | Kurulum |
|------|-----------|---------|
| Gmail | `gmail-mcp` | hosted |
| Notion | `notion-mcp` | hosted |
| HubSpot | `hubspot-mcp` | hosted |
| Google Calendar | `gmail-mcp` (aynı) | hosted |
| Google Sheets | `gmail-mcp` (aynı) | hosted |

---

## Kurulum

### Ön Koşul
- Claude Code kurulu olmalı → [claude.ai/code](https://claude.ai/code)
- `claude --version` çalışıyor olmalı

### Adım 1: Gmail MCP Ekle

```bash
claude mcp add gmail https://gmail.mcp.so/
```

### Adım 2: Notion MCP Ekle

```bash
claude mcp add notion https://notion.mcp.so/
```

### Adım 3: HubSpot MCP Ekle

```bash
claude mcp add hubspot https://hubspot.mcp.so/
```

### Adım 4: Bağlantıyı Doğrula

```bash
claude mcp list
# → gmail, notion, hubspot görünmeli
```

### Adım 5: Test Et

```bash
claude "Gmail'imde son 5 email ne?"
claude "Notion'da 'AI Otomasyonları' sayfası var mı?"
```

---

## Manuel Config Ekleme (.mcp.json)

Eğer hosted MCP çalışmazsa, proje köküne `.mcp.json` dosyası oluştur:

```json
{
  "mcpServers": {
    "gmail": {
      "transport": "http",
      "url": "https://gmail.mcp.so/"
    },
    "notion": {
      "transport": "http",
      "url": "https://notion.mcp.so/"
    },
    "hubspot": {
      "transport": "http",
      "url": "https://hubspot.mcp.so/"
    }
  }
}
```

---

## MCP Config Dosyaları

Bu repo'daki `mcp/` klasöründe hazır config'ler var:

```
mcp/
├── gmail-mcp.json
├── notion-mcp.json
└── hubspot-mcp.json
```

Manuel eklemek yerine bunları kullan:
```bash
# Her config için
claude mcp add --file mcp/gmail-mcp.json
```

---

## OAuth2 Token'ları (Gmail/Google Calendar)

MCP server'lar Google hesabına erişim için OAuth2 gerektirir:

1. [console.cloud.google.com](https://console.cloud.google.com/) → OAuth2 Client oluştur
2. Client ID + Secret al
3. `~/.claude/` dizininde credentials dosyası oluştur (n8n credential ile aynı mantık)
4. İlk komutta tarayıcı açılacak → Google hesabınla yetkilendir

---

## MCP Kaldırma

```bash
claude mcp remove gmail
claude mcp remove notion
claude mcp remove hubspot
```

---

## Sorunlar

| Sorun | Çözüm |
|-------|-------|
| `MCP server not found` | URL doğru mu kontrol et |
| `Authentication failed` | OAuth2 token yenile / yeniden yetkilendir |
| `Permission denied` | Google hesabında API erişimi açık mı? |

Detaylı → [`TROUBLESHOOTING.md`](TROUBLESHOOTING.md)
