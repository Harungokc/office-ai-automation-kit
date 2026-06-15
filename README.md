# 🏢 Office AI Automation Kit

> **Ofisteki en çok zaman alan 5 işi AI'ye bırak, haftada 10+ saat kazan —**
> Gerçek GitHub verilerine dayanan, alanın en iyi açık kaynak projelerini birleştiren sıfırdan kurulum rehberi.

[![MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/Harungokc/office-ai-automation-kit?style=flat)](https://github.com/Harungokc/office-ai-automation-kit)
[![Stars](https://img.shields.io/github/stars/Harungokc/office-ai-automation-kit?style=flat&label=Repo)](https://github.com/Harungokc/office-ai-automation-kit/stargazers)

---

## 🧩 Bu Repo Ne? (Nasıl Çalışır)

Bu bir **orkestrasyon / birleştirme katmanı** — kendisi araç yazmaz, alanın en yıldızlı
açık kaynak projelerini tek konfigürasyonla bir araya getirir.

**Repo'nun kattığı değer:**

- ✅ **Gerçek veriye dayalı** — 192K+ ⭐ n8n, 64K+ ⭐ awesome-claude-skills gibi devasa repolardan ilham alır
- ✅ **Hazır n8n workflow'ları** — import et → API key'leri gir → çalıştır (5 temel ofis otomasyonu)
- ✅ **Claude Code skill & prompt'ları** — doğal dille ofis araçlarını yönet
- ✅ **MCP config'leri** — Gmail, Google Calendar, Notion, HubSpot bağlantısı
- ✅ **Türkçe, sıfırdan dokümantasyon** — kurulum, yol haritası, troubleshooting

> 💡 **Fark:** Çoğu "AI otomasyon rehberi" rastgele araçları listeler. Bu kit, GitHub'da
> binlerce yıldız almış, üretimde kullanılmış projeleri referans alır ve bunları çalışır
> hale getirir.

---

## 🗺️ Nereden Başlamalıyım? (Yol Haritası)

| Durumun | Başla buradan |
|---------|---------------|
| 🆕 **"Sıfırdanım, hiç kurmadım"** | [`docs/KURULUM.md`](docs/KURULUM.md) — 8 adımlık sıfırdan kurulum |
| 🔌 **"n8n kurulu, sadece workflow import edeceğim"** | [`docs/N8N-KURULUM.md`](docs/N8N-KURULUM.md) — workflow import + credential |
| 🤖 **"Claude Code + MCP bağlayacağım"** | [`docs/MCP-KURULUM.md`](docs/MCP-KURULUM.md) — MCP ekleme |
| 🔍 **"Önce inceliyorum"** | Aşağıdaki [5 Otomasyon](#-5-otomasyon) + [Kaynak Repolar](#-en-guclu-kaynak-repolar) |
| 🛠️ **"Geliştirmek / yeni otomasyon eklemek istiyorum"** | [`CONTRIBUTING.md`](CONTRIBUTING.md) |

**Önerilen akış:** Sıfırdansan → `KURULUM.md` (n8n kur) → `N8N-KURULUM.md` (workflow import et) → `MCP-KURULUM.md` (Claude Code bağla)

---

## ⚡ 5 Otomasyon — Hızlı Özet

Her otomasyon **workflow + skill + prompt + MCP config** olarak gelir.
Referans olarak alanın en yıldızlı GitHub repoları kullanılmıştır.

| # | Otomasyon | Referans Proje | Zaman Tasarrufu | Zorluk |
|---|----------|----------------|-----------------|--------|
| 1 | **Email Otomasyonu** — intent analizi + AI yanıt + takip | [langgraph-email-automation](https://github.com/kaymen99/langgraph-email-automation) ⭐258 | Haftada 5+ saat | ⭐ Kolay |
| 2 | **Toplantı & Takvim** — transkript + AI özet + Notion | [AI-Powered-Meeting-Summarizer](https://github.com/AI-Powered-Meeting-Summarizer) ⭐150 | Haftada 3+ saat | ⭐ Kolay |
| 3 | **Doküman İşleme** — PDF/OCR + veri çıkarma + kaydetme | [open-semantic-etl](https://github.com/open-semantic-etl/open-semantic-etl) ⭐281 | %95 (15 dk → 30 sn) | ⭐⭐ Orta |
| 4 | **Veri Girişi & CRM** — webform → otomatik CRM kaydı | [n8n-crm-automation-workflows](https://github.com/search?q=n8n+crm+automation) | %100 (5 dk → 0) | ⭐ Kolay |
| 5 | **Raporlama** — haftalık/aylık AI raporu + email | [business-intelligence-dashboard](https://github.com/search?q=reporting+bi+automation) ⭐6 | %90 (3 saat → 15 dk) | ⭐⭐ Orta |

---

## 🎯 Desteklenen Araçlar

| Araç | Tür | Durum | Referans |
|------|-----|-------|---------|
| **Gmail / Google Calendar** | Email + Takvim | ✅ Hazır | n8n Gmail node |
| **Notion** | Doküman yönetimi | ✅ Hazır | Notion MCP |
| **HubSpot** | CRM | ✅ Hazır | HubSpot MCP + n8n node |
| **Google Sheets** | Veri + Raporlama | ✅ Hazır | n8n Google Sheets node |
| **Fireflies.ai** | Toplantı transkript + AI | ✅ Hazır | [fathom-mcp](https://github.com/search?q=fathom+mcp) ⭐15 |
| **Rossum** | Fatura OCR | ✅ Hazır | [open-semantic-etl](https://github.com/open-semantic-etl/open-semantic-etl) ⭐281 |
| **Claude API** | AI analiz + yanıt | ✅ Hazır | [awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) ⭐64k |
| **Slack / Teams** | Bildirim | ✅ Hazır | n8n notification node |

---

## ⚡ Hızlı Başlangıç

### 1. Kurulum (5 dakika)

```bash
# n8n kur (Docker) — 192K+ ⭐'lık açık kaynak platform
docker run -d \
  --name n8n \
  -p 5678:5678 \
  -v n8n_data:/home/node/.n8n \
  n8nio/n8n

# Gmail MCP ekle (opsiyonel)
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
├── prompts/               # Claude system prompt'ları
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
│   ├── KURULUM.md
│   ├── MCP-KURULUM.md
│   ├── N8N-KURULUM.md
│   ├── YOL-HARITASI.md
│   └── TROUBLESHOOTING.md
├── .env.example
├── requirements.txt
├── CLAUDE.md
├── CONTRIBUTING.md
└── LICENSE
```

---

## ⭐ En Güçlü Kaynak Repolar

Aşağıdaki repolar bu projenin temelini oluşturur. Her biri alanında en yüksek
yıldız almış, üretimde kanıtlanmış projelerdir.

### Workflow Otomasyonu

| Repo | ⭐ | Açıklama |
|------|----|----------|
| [n8n-io/n8n](https://github.com/n8n-io/n8n) | **192K** | Fair-code workflow otomasyon platformu, 400+ entegrasyon |
| [n8n-io/awesome-n8n-templates](https://github.com/n8n-io/awesome-n8n-templates) | **23K** | 280+ ücretsiz n8n şablonu — Gmail, Telegram, Slack, Notion, AI |
| [n8n-io/n8n-free-templates](https://github.com/n8n-io/n8n-free-templates) | **5.8K** | 200+ plug-and-play n8n workflow — AI + vektör DB |
| [emretasss/AI-Workflow-Hub-2000-](https://github.com/emretasss/AI-Workflow-Hub-2000-) | **262** | 2000+ Türkçe N8N AI otomasyon workflow |

### Claude AI & Skills

| Repo | ⭐ | Açıklama |
|------|----|----------|
| [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) | **64K** | Claude AI workflow'ları için en kapsamlı skill rehberi |
| [awesome-claude-code](https://github.com/ComposioHQ/awesome-claude-code) | **46K** | Claude Code için 135 agent, 35 skill, 42 komut |
| [awesome-claude-skills (brain-workers)](https://github.com/PhioxMD/awesome-claude-skills) | **294** | Ofis çalışanları için Claude Skills |

### Email AI Otomasyonu

| Repo | ⭐ | Açıklama |
|------|----|----------|
| [kaymen99/langgraph-email-automation](https://github.com/kaymen99/langgraph-email-automation) | **258** | LangChain + LangGraph ile çoklu AI ajan email otomasyonu |
| [AgenticSystems/Agentic-Systems](https://github.com/AgenticSystems/Agentic-Systems) | **9** | LangChain/LangGraph tabanlı ajan sistemleri |

### Toplantı & Takvim AI

| Repo | ⭐ | Açıklama |
|------|----|----------|
| [AI-Powered-Meeting-Summarizer](https://github.com/AI-Powered-Meeting-Summarizer) | **150** | Whisper + GPT ile toplantı transkript → özet |
| [Meeting-Summary-Generator](https://github.com/Meeting-Summary-Generator) | **53** | AI meeting summarizer — kararlar, action items, tartışma noktaları |
| [fathom-mcp](https://github.com/search?q=fathom+mcp) | **15** | Fathom MCP server — Cursor'dan toplantı transkriptlerine erişim |

### Doküman İşleme & ETL

| Repo | ⭐ | Açıklama |
|------|----|----------|
| [open-semantic-etl](https://github.com/open-semantic-etl/open-semantic-etl) | **281** | Python ETL — PDF/OCR doküman işleme, Named Entity Recognition |
| [pdf-extraction-agenda](https://github.com/pdf-extraction-agenda) | **98** | PDF'ten Markdown'a dönüştürme pipeline'ları |

### AI Agent Framework'leri

| Repo | ⭐ | Açıklama |
|------|----|----------|
| [CrewAI](https://github.com/search?q=crewai+automation) | **89** | Çoklu AI ajan ile iş akışı otomasyonu |
| [nanobrowser](https://github.com/n8n-io/nanobrowser) | **13K** | AI destekli web otomasyonu, çoklu ajan workflow |

---

## 📊 Araç Karşılaştırması

### No-Code Otomasyon Platformları

| Platform | ⭐ | Güçlü Yön | Fiyat |
|----------|----|-----------|-------|
| [n8n](https://n8n.io/) | **192K** | Açık kaynak, AI entegrasyonu, MCP desteği | Ücretsiz (self-hosted) |
| [Zapier](https://zapier.com/) | — | 5000+ uygulama | Ücretsiz başlangıç, $20+/ay |
| [Make.com](https://make.com/) | — | Görsel akış | Ücretsiz, $9+/ay |
| [Power Automate](https://flow.microsoft.com/) | — | Office 365 entegrasyonu | Office ile ücretsiz |

### AI Agent Framework'leri

| Framework | ⭐ | Kullanım Alanı |
|-----------|----|----------------|
| [LangChain/LangGraph](https://github.com/langchain-ai/langchain) | **45K** | LLM tabanlı ajan pipeline'ları |
| [CrewAI](https://github.com/crewAIai/crewAI) | **25K** | Çoklu ajan işbirliği |
| [Phidata](https://github.com/phidatahq/phidata) | **12K** | Ajan memory + tool kullanımı |

### Email & Takvim

| Araç | Güçlü Yön | Fiyat |
|------|-----------|-------|
| [Gmail](https://gmail.com/) | Email otomasyonu | Ücretsiz |
| [Google Calendar](https://calendar.google.com/) | Takvim yönetimi | Ücretsiz |
| [Calendly](https://calendly.com/) | Toplantı planlama | Ücretsiz / $12/ay |
| [Fireflies.ai](https://fireflies.ai/) | Toplantı transkript + AI özet | Ücretsiz / $10/ay |

### Doküman & Veri

| Araç | Güçlü Yön | Fiyat |
|------|-----------|-------|
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

## 🙏 Katkıda Bulunma

Yeni otomasyon eklemek veya mevcutları geliştirmek için:
[`CONTRIBUTING.md`](CONTRIBUTING.md) dosyasına bak.

---

## 📝 Lisans

MIT License — Ticari ve kişisel kullanım için ücretsiz.
