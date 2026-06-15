# 🏢 Office AI Automation Kit

> **Ofisteki en çok zaman alan 5 işi AI'ye bırak, haftada 10+ saat kazan —**
> Claude Code, n8n ve MCP ile sıfırdan kurulum, tek konfigürasyonla çalışır sistem.

[![MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

---

## 🧩 Bu Repo Ne? (Nasıl Çalışır)

Bu bir **orkestrasyon / birleştirme katmanı** — kendisi araç yazmaz, ofis otomasyonunda
en güçlü açık kaynak ve hosted **MCP server'larını** + **n8n workflow'larını** bir araya getirir.

**Repo'nun kattığı değer:**

- ✅ **Hazır n8n workflow'ları** — import et → çalıştır (5 temel ofis otomasyonu)
- ✅ **Claude Code skill & prompt'ları** — doğal dille ofis araçlarını yönet
- ✅ **MCP config'leri** — Gmail, Google Calendar, Notion, HubSpot bağlantısı
- ✅ **Türkçe, sıfırdan dokümantasyon** — kurulum, yol haritası, troubleshooting

> 💡 **İpucu:** Bu kitteki her otomasyon bağımsız çalışır. Tek seferde 5'ini de kurabileceğin
> gibi, en acil olanla başlayıp diğerlerini sonra ekleyebilirsin.

---

## 🗺️ Nereden Başlamalıyım? (Yol Haritası)

Durumuna göre doğru rehbere git — sırayla takip et:

| Durumun | Başla buradan |
|---------|---------------|
| 🆕 **"Sıfırdanım, hiç kurmadım"** | [`docs/KURULUM.md`](docs/KURULUM.md) — 8 adımlık sıfırdan kurulum |
| 🔌 **"n8n kurulu, sadece workflow import edeceğim"** | [`docs/N8N-KURULUM.md`](docs/N8N-KURULUM.md) — workflow import + credential |
| 🤖 **"Claude Code + MCP bağlayacağım"** | [`docs/MCP-KURULUM.md`](docs/MCP-KURULUM.md) — MCP ekleme |
| 🔍 **"Önce inceliyorum"** | Aşağıdaki [5 Otomasyon](#-5-otomasyon) + [Araç Karşılaştırması](#-araç-karşılaştırması) |
| 🛠️ **"Geliştirmek / yeni otomasyon eklemek istiyorum"** | [`CONTRIBUTING.md`](CONTRIBUTING.md) |

**Önerilen akış:** Sıfırdansan → `KURULUM.md` (n8n kur) → `N8N-KURULUM.md` (workflow import et) → `MCP-KURULUM.md` (Claude Code bağla)

---

## ⚡ 5 Otomasyon — Hızlı Özet

Her otomasyon **workflow + skill + prompt + MCP config** olarak gelir.

| # | Otomasyon | Ana Araçlar | Zaman Tasarrufu | Zorluk |
|---|----------|-------------|-----------------|--------|
| 1 | **Email Otomasyonu** — önceliklendirme + AI yanıt + takip hatırlatıcı | Gmail + n8n + Claude | Haftada 5+ saat | ⭐ Kolay |
| 2 | **Toplantı & Takvim** — otomatik planlama + transkript + özet | Google Calendar + Fireflies + n8n | Haftada 3+ saat | ⭐ Kolay |
| 3 | **Doküman İşleme** — fatura/sözleşme okuma + veri çıkarma | Rossum / Claude PDF + Notion | %95 (15 dk → 30 sn) | ⭐⭐ Orta |
| 4 | **Veri Girişi & CRM** — webform → CRM otomatik kayıt | HubSpot + n8n + Gmail | %100 (5 dk → 0) | ⭐ Kolay |
| 5 | **Raporlama** — haftalık/aylık otomatik rapor PDF + email | Google Sheets + n8n + Claude | %90 (3 saat → 15 dk) | ⭐⭐ Orta |

---

## 🎯 Desteklenen Araçlar

| Araç | Tür | Durum | Kaynak |
|------|-----|-------|--------|
| **Gmail / Google Calendar** | Email + Takvim | ✅ Hazır | Gmail MCP veya n8n Google nodes |
| **Notion** | Doküman yönetimi | ✅ Hazır | Notion MCP |
| **HubSpot** | CRM | ✅ Hazır | HubSpot MCP + n8n node |
| **Google Sheets** | Veri + Raporlama | ✅ Hazır | n8n Google Sheets node |
| **Fireflies / Otter.ai** | Toplantı transkript | ✅ Hazır | API + n8n HTTP Request |
| **Rossum** | Fatura OCR | ✅ Hazır | API + n8n HTTP Request |
| **Slack / Teams** | Bildirim | ✅ Hazır | n8n notification node |
| **Claude API** | AI analiz + yanıt | ✅ Hazır | Direct API |

---

## ⚡ Hızlı Başlangıç

### 1. Kurulum (5 dakika)

```bash
# n8n kur (Docker)
docker run -d \
  --name n8n \
  -p 5678:5678 \
  -v n8n_data:/home/node/.n8n \
  n8nio/n8n

# Gmail MCP ekle (opsiyonel, n8n yet)
claude mcp add gmail https://gmail.mcp.so/

# HubSpot MCP ekle (opsiyonel)
claude mcp add hubspot https://hubspot.mcp.so/
```

### 2. Workflow Import

```bash
# n8n'ye git → Settings → Import from File
# workflows/ klasöründen ilgili JSON'u seç
# Credential ayarla → Activate
```

### 3. Kullanım

```bash
# Email otomasyonu başlat
claude "Gelen kutuma bak, acil olanları önceliklendir"

# Toplantı özeti al
claude "Son toplantımın transkriptini al, action items çıkar"

# Rapor oluştur
claude "Bu haftanın satış raporunu hazırla, PDF olarak gönder"
```

---

## 📁 Repoda Ne Var?

```
office-ai-automation-kit/
├── workflows/              # n8n JSON workflow'ları (import et → çalıştır)
│   ├── 1-email-otomasyon.json
│   ├── 2-toplanti-takvim.json
│   ├── 3-dokuman-isleme.json
│   ├── 4-veri-girisi-crm.json
│   └── 5-raporlama.json
├── skills/                 # Claude Code skill dosyaları
│   ├── email-otomasyon-skill.md
│   ├── toplanti-skill.md
│   ├── dokuman-isleme-skill.md
│   ├── veri-girisi-skill.md
│   └── raporlama-skill.md
├── prompts/                # Claude system prompt'ları
│   ├── email-otomasyon-prompt.md
│   ├── toplanti-prompt.md
│   ├── dokuman-prompt.md
│   ├── veri-girisi-prompt.md
│   └── raporlama-prompt.md
├── mcp/                    # MCP server config'leri
│   ├── gmail-mcp.json
│   ├── notion-mcp.json
│   └── hubspot-mcp.json
├── docs/                   # Detaylı dokümantasyon
│   ├── KURULUM.md          # Sıfırdan kurulum (8 adım)
│   ├── MCP-KURULUM.md      # Claude Code'a MCP ekleme
│   ├── N8N-KURULUM.md      # n8n workflow import
│   ├── YOL-HARITASI.md     # Haftalık ilerleme planı
│   └── TROUBLESHOOTING.md  # Sık karşılaşılan hatalar
├── .env.example
├── requirements.txt
├── CLAUDE.md               # AI ajanlar için kurulum rehberi
├── CONTRIBUTING.md         # Katkı & geliştirme rehberi
└── LICENSE
```

---

## 📊 Araç Karşılaştırması

### No-Code Otomasyon Platformları

| Platform | Güçlü Yön | Fiyat |
|----------|-----------|-------|
| [n8n](https://n8n.io/) | Açık kaynak, esnek, AI entegrasyonu | Ücretsiz (self-hosted) |
| [Zapier](https://zapier.com/) | 5000+ uygulama | Ücretsiz başlangıç, $20+/ay |
| [Make.com](https://make.com/) | Görsel akış | Ücretsiz, $9+/ay |
| [Power Automate](https://flow.microsoft.com/) | Office 365 entegrasyonu | Office ile ücretsiz |

### AI API Servisleri

| Servis | Kullanım | Fiyat |
|--------|----------|-------|
| [Claude API](https://console.anthropic.com/) | Doküman analizi, yazı | $0.001-0.01/istek |
| [OpenAI API](https://platform.openai.com/) | Yazı, analiz | $0.001-0.06/istek |

### Email & Takvim

| Araç | Kullanım | Fiyat |
|------|----------|-------|
| [Gmail](https://gmail.com/) | Email | Ücretsiz |
| [Google Calendar](https://calendar.google.com/) | Takvim | Ücretsiz |
| [Calendly](https://calendly.com/) | Toplantı planlama | Ücretsiz / $12/ay |
| [Fireflies.ai](https://fireflies.ai/) | Toplantı transkript + AI özet | Ücretsiz / $10/ay |

### Doküman & Veri

| Araç | Kullanım | Fiyat |
|------|----------|-------|
| [Notion](https://notion.so/) | Doküman yönetimi | Ücretsiz / $10/kullanıcı |
| [Rossum](https://rossum.ai/) | Fatura OCR | €3/fatura |
| [HubSpot](https://hubspot.com/) | CRM | Ücretsiz / $50+/ay |
| [Google Sheets](https://sheets.google.com/) | Veri + Raporlama | Ücretsiz |

---

## 📈 Beklenen Sonuçlar

Bu 5 otomasyonu kurduktan sonra:

| Metrik | Önce | Sonra |
|--------|------|-------|
| Email okuma/yazma süresi | Günde 1-2 saat | 20-30 dakika |
| Toplantı notu yazma | 15 dk/kişi | 0 dk |
| Fatura kaydetme | 15 dakika | 30 saniye |
| Veri girişi | 5 dakika/form | 0 dakika (otomatik) |
| Rapor hazırlama | 3 saat | 15 dakika |
| **Toplam haftalık tasarruf** | — | **10-15 saat** |

---

## 🙏 Kaynak Repolar

Bu kit, aşağıdaki açık kaynak projelerden ilham alır ve bunları bir araya getirir:

| Proje | Yıldız | Ne Sağlar? |
|-------|--------|------------|
| [n8n-io/n8n](https://github.com/n8n-io/n8n) | ⭐ 92k | Workflow otomasyon platformu |
| [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) | ⭐ 64k | Claude AI yetenekleri |
| [FlowiseAI/Flowise](https://github.com/FlowiseAI/Flowise) | ⭐ 53k | Görsel AI ajanı oluşturma |
| [emretasss/AI-Workflow-Hub-2000-](https://github.com/emretasss/AI-Workflow-Hub-2000-) | ⭐ 262 | 2000+ N8N şablonu |

---

## 🤝 Katkıda Bulunma

Yeni otomasyon eklemek veya mevcutları geliştirmek için:
[`CONTRIBUTING.md`](CONTRIBUTING.md) dosyasına bak.

---

## 📝 Lisans

MIT License — Ticari ve kişisel kullanım için ücretsiz.
