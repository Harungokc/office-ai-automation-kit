# Yol Haritası — 4 Haftada Tam Otomasyon

Hafta hafta ilerleme planı. Her hafta 1 otomasyon kurup çalışır hale getireceksin.

---

## 📅 Hafta 1: Email Otomasyonu

**Hedef:** Gelen email'leri AI önceliklendirsin, otomatik yanıtlasın

**Kurulacak:**
- [ ] Docker + n8n kurulumu (Adım 1-2)
- [ ] Google OAuth2 (Adım 3)
- [ ] Claude API key (Adım 6)
- [ ] Workflow 1 import + credential
- [ ] Test: Gerçek email'le test et

**Sonuç:**
- Email'ler otomatik önceliklendirilir
- Acil olmayanlara AI yanıt verir
- Takip hatırlatıcıları çalışır

**Zaman tasarrufu:** Haftada 5+ saat

---

## 📅 Hafta 2: Toplantı & Takvim Otomasyonu

**Hedef:** Toplantıları AI özetlesin, Notion'a kaydetsin

**Kurulacak:**
- [ ] Google Calendar entegrasyonu (OAuth2 zaten kuruluydu)
- [ ] Fireflies.ai hesabı (ücretsiz plan yeterli)
- [ ] Workflow 2 import + credential
- [ ] Notion sayfası oluştur ("Toplantılar")
- [ ] Test: Gerçek toplantıyla test et

**Sonuç:**
- Toplantı sonrası otomatik transkript
- AI özet + action items
- Notion'a otomatik kayıt

**Zaman tasarrufu:** Haftada 3+ saat

---

## 📅 Hafta 3: Doküman İşleme

**Hedef:** Faturaları/sözleşmeleri AI okusun, veri çıkarsın

**Kurulacak:**
- [ ] Rossum hesabı (veya Claude PDF) (opsiyonel)
- [ ] Workflow 3 import + credential
- [ ] Notion "Faturalar" sayfası oluştur
- [ ] Gmail'de "Fatura" label oluştur
- [ ] Test: Fatura email'i gönder

**Sonuç:**
- Faturalar otomatik okunur
- Veriler Notion'a kaydedilir
- Toplam tutar hesaplanır

**Zaman tasarrufu:** %95 (15 dk → 30 sn/form)

---

## 📅 Hafta 4: Veri Girişi & Raporlama

**Hedef:** Webform verileri CRM'e otomatik kayıtsın + haftalık rapor çalışsın

**Kurulacak:**
- [ ] HubSpot hesabı (ücretsiz CRM yeterli)
- [ ] Workflow 4 + 5 import + credential
- [ ] Google Sheets "Satış Verileri" oluştur
- [ ] Haftalık rapor schedule ayarla
- [ ] Test: Form gönder + cuma günü rapor

**Sonuç:**
- Yeni lead'ler otomatik HubSpot'a kaydedilir
- Haftalık rapor otomatik oluşur
- Email ile PDF rapor gönderilir

**Zaman tasarrufu:** %100 veri girişi + 3 saat raporlama → 15 dakika

---

## 📊 Haftalık İlerleme Takibi

| Hafta | Otomasyon | Kuruldu? | Test Edildi? | Tasarruf |
|-------|----------|----------|--------------|----------|
| 1 | Email | ⬜ | ⬜ | — |
| 2 | Toplantı | ⬜ | ⬜ | — |
| 3 | Doküman | ⬜ | ⬜ | — |
| 4 | Veri + Rapor | ⬜ | ⬜ | — |

---

## 🎯 4 Hafta Sonunda

Toplam **10-15 saat/hafta** tasarruf:

- 📧 Email: 1-2 saat → 20-30 dakika
- 📅 Toplantı notu: 15 dk/kişi → 0 dk
- 📄 Fatura: 15 dakika → 30 saniye
- 📊 Veri girişi: 5 dakika → 0 dakika
- 📈 Rapor: 3 saat → 15 dakika

---

## 💡 İpuçları

1. **Hızlı başla, yavaş ilerle** — Her hafta sadece 1 otomasyona odaklan
2. **Test etmeden aktif etme** — Her workflow'u elle test et, sonra activate et
3. **Log'ları izle** — İlk günlerde n8n Execution History'yi sık kontrol et
4. **Claude token'ını koru** — Haftada ~5000 token yeterli başlangıç için
5. **Notion'ı düzenli tut** — Her otomasyon için ayrı sayfa/grupy kullan

---

## 🚨 Takıldığında

1. [`TROUBLESHOOTING.md`](TROUBLESHOOTING.md) → Sık hatalar ve çözümleri
2. [`KURULUM.md`](KURULUM.md) → Adım adım kurulum
3. [`N8N-KURULUM.md`](N8N-KURULUM.md) → Workflow detayları
4. GitHub Issue aç → Hata mesajı + adımları paylaş
