# Katkıda Bulunma

## Nasıl Katkıda Bulunulur?

1. Bu repoyu fork'la
2. Yeni bir branch oluştur: `git checkout -b yeni-otomasyon`
3. Değişikliklerini yap
4. Commit at: `git commit -m 'Yeni özellik: ...'`
5. Push at: `git push origin yeni-otomasyon`
6. Pull Request aç

## Yeni Otomasyon Eklerken

Her otomasyon **4 parçayla** gelir (tıpkı mevcut yapıdaki gibi):

1. **Workflow** → `workflows/N-otomasyon-adi.json` (geçerli n8n JSON formatı)
2. **Skill** → `skills/otomasyon-adi-skill.md` (bu repo formatını izle)
3. **Prompt** → `prompts/otomasyon-adi-prompt.md`
4. **MCP Config** → `mcp/arac-adi-mcp.json` (varsa, yoksa klasör boş kalabilir)

## Dosya Format Kuralları

### n8n Workflow JSON
- `workflows/` klasöründeki her dosya geçerli n8n v1 JSON olmalı
- Node tipleri `n8n-nodes-base.*` veya bilinen MCP/noditure package'ları olmalı
- Credential'lar `credentials/` bölümünde tanımlı olmalı (değerler BOŞ, sadece isimler)
- Workflow varsayılan olarak **PAUSED** durumda olmalı (otomatik çalışmasın)

### Skill Dosyası
```markdown
# [Araç] Skill — Claude Code

## Konsept
## Araçlar
## Prompt Template
## API Uç Noktaları (varsa)
```

### MCP Config
```json
{
  "mcpServers": {
    "arac-adi": {
      "transport": "http",
      "url": "https://arac.mcp.so/"
    }
  }
}
```

## README Güncelleme

Yeni otomasyon eklerken:
1. README.md'deki "5 Otomasyon" tablosuna satır ekle
2. "Desteklenen Araçlar" tablosuna varsa yeni aracı ekle
3. "Repoda Ne Var" klasör listesini güncelle

## Test Etme

```bash
# Workflow JSON geçerli mi kontrol et
python -c "import json; json.load(open('workflows/1-email-otomasyon.json'))"

# Skill geçerli mi kontrol et (syntax)
python -c "import json; json.load(open('skills/email-otomasyon-skill.md'))"  # skill .md değil .json olsaydı
```

## İlke

- Araçları biz yazmıyoruz — **gerçek MCP server'ları ve API'leri birleştiriyoruz**
- Geri alınamaz işlemler (email gönderme, CRM kaydı silme) prompt'larda **PAUSED/varsayılan** olmalı
- Kullanıcı onayı olmadan veri değişikliği YAPMA
