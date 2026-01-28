# 🌐 Automated Domain Monitoring & Alert System

**[Turkish / Türkçe](#türkçe-versiyon)** | **[English](#english-version)**

---

## English Version

### ⚡ Overview

A **production-ready, open-source automation system** that monitors domain registrations, WHOIS/DNS data, and sends real-time alerts via Telegram. Built with **n8n**, it performs daily checks using RDAP protocol to track expiration dates, nameserver changes, and security status.

**Zero coding required.** Deploy on your own infrastructure.

---

### 🎯 Key Features

✅ **Automated Daily Monitoring**
- Scheduled daily domain checks at 12:00 UTC
- Queries live WHOIS/DNS data via RDAP protocol
- Supports 30+ TLD registries (COM, ORG, NET, DE, FR, IO, etc.)

✅ **Intelligent Change Detection**
- Detects status shifts (active → prohibited)
- Tracks expiration date changes
- Monitors nameserver modifications
- Identifies "expiring soon" domains (30-day countdown)

✅ **Real-Time Notifications**
- Sends Telegram alerts only when changes detected
- Professional formatted messages with actionable data
- Tracks registration dates and RDAP update timestamps

✅ **Multi-Channel Reporting**
- Updates master Google Sheets spreadsheet
- Maintains complete audit trail
- Manual override capabilities

✅ **Security & Compliance**
- Monitors "Client/Server Prohibited" locks
- Prevents unauthorized transfers
- Infrastructure verification with nameserver tracking

---

### 📊 What It Monitors

| Metric | Details |
|--------|---------|
| **Expiration Date** | Exact expiration timestamp with countdown |
| **Status** | Current WHOIS status (active, prohibited, etc.) |
| **Days Remaining** | Automated "days until expiration" |
| **Nameservers** | DNS infrastructure integrity tracking |
| **Registration Date** | Domain registration timestamp |
| **Security Locks** | Client/Server Prohibited status |
| **Change History** | Before/after status comparisons |

---

### 🚀 Quick Start

#### Prerequisites
- **n8n** instance (self-hosted on your server)
- **Google Sheets** account
- **Telegram Bot** (free)
- Domains to monitor

#### 1. Create Telegram Bot (2 minutes)

```bash
# Talk to @BotFather on Telegram
/newbot
# Name: "Domain Monitor"
# Username: "your_domain_monitor_bot"
# Get: Bot Token & Chat ID
```

#### 2. Set Up Google Sheets

1. Create new Google Sheets document
2. Add column headers:
   ```
   Domain | Days Remaining | Latest Status | Expiration Date | 
   Registration Date | Nameservers | Expiring Soon | 
   RDAP Last Update | Last Check
   ```
3. Add your domains to monitor:
   ```
   microsoft.com
   facebook.com
   chatgpt.com
   ```
4. Share sheet with n8n Google Sheets credential

#### 3. Import n8n Workflow

1. Open n8n instance → Workflows
2. Click "Import from file" 
3. Upload `n8n-workflow.json`
4. **Connect credentials:**
   - Google Sheets (your sheet ID)
   - Telegram Bot (Bot token + Chat ID)

#### 4. Activate & Test

```
Workflow Settings → Active: ON
Test → Manual Trigger
```

---

### 📝 Configuration

**Modify these parameters in the workflow:**

- **Schedule:** Edit "Daily Check" node → `triggerAtHour: 12` (change to your timezone)
- **Notification Threshold:** "Data Analysis" node → `is_expiring_soon = days_to_expiry <= 30` (change 30 to your preference)
- **Telegram Format:** "Send Telegram Message" node → Customize message template

---

### 🔧 How It Works

```
Daily Trigger (12:00 UTC)
    ↓
Get Domains from Sheet
    ↓
Loop Through Each Domain
    ↓
Prepare Data (validate format, extract TLD)
    ↓
Is Domain Supported? (check RDAP registry)
    ├─ YES → Query RDAP Server
    └─ NO → Log & Continue
    ↓
Successful Response?
    ├─ YES → Data Analysis
    │         ├─ Detect Changes
    │         ├─ Update Sheet
    │         └─ Send Alert (if change detected)
    └─ NO → Log Error & Continue
    ↓
Cool Down Engine (rate limiting)
    ↓
Repeat for next domain
```

---

### 🎮 Supported TLDs

**ICANN TLDs:** COM, NET, NAME, ORG, INFO, BIZ, IO, ME, TV, CC, MOBI, ASIA, DEV, APP, PAGE, ZIP, etc.

**Country-Code TLDs:** DE, FR, NL, EU, UK, IT, ES, CH, AT, SE, NO, DK, FI, US, CA, AU, JP, CN, RU, BR

**New gTLDs:** GURU, EMAIL, LIVE, NEWS, MEDIA, TODAY, WORLD, DIGITAL, EXPERT, AGENCY, TECHNOLOGY, SOFTWARE, SOLUTIONS, SERVICES, COMPANY

---

### 📱 Alert Example

```
🌐 Domain Check Automation
🔗 Domain: facebook.com
📌 Current Status: active
📅 Expiration Date: 30.03.2034
⏳ Days Remaining: 2984

🔄 Status changed: active → prohibited

🌍 Nameservers:
A.NS.FACEBOOK.COM
B.NS.FACEBOOK.COM

🕒 Last Check: 28.01.2026, 12:42:17
```

---

### 🔐 Security Notes

- **Self-hosted:** Run on your own infrastructure - no cloud vendor lock-in
- **Credentials:** Store securely in n8n credential manager
- **Rate Limiting:** Built-in 1-second delays between queries
- **Error Handling:** Continues on failed lookups, logs errors
- **Data Privacy:** Your spreadsheet remains private

---



### 🛠️ Troubleshooting

**Domain not updating?**
- Check if domain TLD is in supported list
- Verify RDAP server is responding (try manual HTTP request)
- Check n8n execution logs

**Telegram alerts not sending?**
- Verify Bot Token is correct
- Confirm Chat ID is numeric and matches your chat
- Test: `/start` message in Telegram to activate bot

**Sheet not updating?**
- Confirm Google Sheets credential has write permissions
- Verify column headers match exactly
- Check if sheet is shared with n8n service account

See `docs/TROUBLESHOOTING.md` for detailed solutions.

---


### 💡 Use Cases

- **Agency Networks:** Monitor 50+ client domains automatically
- **E-Commerce:** Alerts for mission-critical domain expirations
- **DevOps:** Integrate with infrastructure automation
- **Security Teams:** Monitor unauthorized nameserver changes
- **Registrar Monitoring:** Track multiple registrar accounts

---

### 🤝 Contributing

Contributions welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Commit changes (`git commit -am 'Add feature'`)
4. Push to branch (`git push origin feature/improvement`)
5. Open a Pull Request

---

### 📄 License

MIT License - Free for personal & commercial use. See [LICENSE](LICENSE) file.

---

### 🙋 Support

- **Issues:** Open a GitHub issue with error logs
- **Discussions:** Start a discussion for feature requests
- **Docs:** Check `docs/` folder for detailed guides

---

### ✨ Version History

**v1.0** (Jan 2026)
- Initial release with RDAP support
- Support for 30+ TLD registries
- Intelligent change detection
- Telegram notifications
- Google Sheets integration

---

<br>

---

## Türkçe Versiyon

### ⚡ Genel Bakış

Domain kayıtlarını, WHOIS/DNS verilerini izleyen ve Telegram üzerinden gerçek zamanlı uyarılar gönderen **üretim hazırı, açık kaynak otomasyonu**. **n8n** ile oluşturuldu, RDAP protokolünü kullanarak günlük kontroller yaparak son kullanma tarihleri, nameserver değişiklikleri ve güvenlik durumunu takip eder.

**Hiç kod yazmanıza gerek yok.** Kendi altyapınızda dağıtın.

---

### 🎯 Ana Özellikler

✅ **Otomatik Günlük İzleme**
- Saat 12:00 UTC'de zamanlanmış günlük domain kontrolleri
- RDAP protokolü üzerinden canlı WHOIS/DNS verilerini sorgular
- 30+ TLD kayıt defterini destekler (COM, ORG, NET, DE, FR, IO, vb.)

✅ **Akıllı Değişim Algılama**
- Durum değişikliklerini tespit eder (active → prohibited)
- Son kullanma tarihi değişikliklerini izler
- Nameserver değişikliklerini izler
- "Yakında bitecek" domain'leri tanımlar (30 günlük geri sayım)

✅ **Gerçek Zamanlı Bildirimler**
- Yalnızca değişim tespit edildiğinde Telegram uyarıları gönderir
- Profesyonel formatlanmış işlem yapılabilir mesajlar
- Kayıt tarihleri ve RDAP güncelleme zaman damgalarını izler

✅ **Çok Kanallı Raporlama**
- Ana Google Sheets tablosunu günceller
- Tam denetim izini tutar
- Manuel geçersiz kılma olanakları

✅ **Güvenlik & Uyum**
- "Client/Server Prohibited" kilitlerini izler
- Yetkisiz transferleri önler
- Nameserver izlemesi ile altyapı doğrulaması

---

### 📊 Ne İzlenir?

| Metrik | Detaylar |
|--------|----------|
| **Son Kullanma Tarihi** | Tam son kullanma zaman damgası geri sayım ile |
| **Durum** | Mevcut WHOIS durumu (aktif, yasaklı, vb.) |
| **Kalan Gün** | Otomatik "son kullanmaya kadar gün sayısı" |
| **Nameserver'lar** | DNS altyapısı bütünlüğü izlemesi |
| **Kayıt Tarihi** | Domain kayıt zaman damgası |
| **Güvenlik Kilitleri** | Client/Server Prohibited durumu |
| **Değişim Geçmişi** | Öncesi/sonrası durum karşılaştırmaları |

---

### 🚀 Hızlı Başlangıç

#### Ön Koşullar
- **n8n** örneği (sunucunuzda barındırılan)
- **Google Sheets** hesabı
- **Telegram Bot** (ücretsiz)
- İzlenecek domain'ler

#### 1. Telegram Bot'u Oluşturun (2 dakika)

```bash
# Telegram'da @BotFather ile konuşun
/newbot
# İsim: "Domain Monitor"
# Kullanıcı adı: "your_domain_monitor_bot"
# Alın: Bot Token & Chat ID
```

#### 2. Google Sheets'i Ayarlayın

1. Yeni Google Sheets belgesi oluşturun
2. Sütun başlıklarını ekleyin:
   ```
   Alan Adı | Kalan Gün | Son Durum | Son Geçerlilik Tarihi | 
   Kayıt Tarihi | Nameserverlar | Yakında Bitecek | 
   RDAP Güncelleme Zamanı | Son Kontrol
   ```
3. İzlenecek domain'lerinizi ekleyin:
   ```
   microsoft.com
   facebook.com
   chatgpt.com
   ```
4. Tabloyu n8n Google Sheets kimliği bilgisi ile paylaşın

#### 3. n8n Workflow'unu İçeri Aktarın

1. n8n örneğinizi açın → Workflow'lar
2. "Dosyadan içeri aktar" seçeneğine tıklayın
3. `n8n-workflow.json` dosyasını yükleyin
4. **Kimlik bilgilerini bağlayın:**
   - Google Sheets (sheet ID'niz)
   - Telegram Bot (Bot token + Chat ID)

#### 4. Etkinleştirin & Test Edin

```
Workflow Ayarları → Etkin: AÇIK
Test → Manuel Tetikleyici
```

---

### 📝 Yapılandırma

**Workflow'ta bu parametreleri değiştirin:**

- **Zamanlama:** "Daily Check" düğümünü düzenleyin → `triggerAtHour: 12` (saat diliminizi değiştirmek için)
- **Bildirim Eşiği:** "Data Analysis" düğümü → `is_expiring_soon = days_to_expiry <= 30` (30'u tercihine göre değiştirin)
- **Telegram Formatı:** "Send Telegram Message" düğümü → İleti şablonunu özelleştirin

---

### 🔧 Nasıl Çalışır?

```
Günlük Tetikleyici (12:00 UTC)
    ↓
Sheet'ten Domain'leri Al
    ↓
Her Domain'i Döngüde İşle
    ↓
Veri Hazırla (formatı doğrula, TLD'yi çıkar)
    ↓
Domain Destekleniyor mu? (RDAP kayıt defterini kontrol et)
    ├─ EVET → RDAP Sunucusunu Sorgula
    └─ HAYIR → Günlüğe Kaydet & Devam Et
    ↓
Başarılı Yanıt mı?
    ├─ EVET → Veri Analizi
    │         ├─ Değişiklikleri Algıla
    │         ├─ Sheet'i Güncelle
    │         └─ Uyarı Gönder (değişim tespit edilirse)
    └─ HAYIR → Hatayı Günlüğe Kaydet & Devam Et
    ↓
Motor Soğutma (hız sınırlaması)
    ↓
Sonraki domain'i tekrarla
```

---

### 🎮 Desteklenen TLD'ler

**ICANN TLD'leri:** COM, NET, NAME, ORG, INFO, BIZ, IO, ME, TV, CC, MOBI, ASIA, DEV, APP, PAGE, ZIP, vb.

**Ülke Kod TLD'leri:** DE, FR, NL, EU, UK, IT, ES, CH, AT, SE, NO, DK, FI, US, CA, AU, JP, CN, RU, BR

**Yeni gTLD'ler:** GURU, EMAIL, LIVE, NEWS, MEDIA, TODAY, WORLD, DIGITAL, EXPERT, AGENCY, TECHNOLOGY, SOFTWARE, SOLUTIONS, SERVICES, COMPANY

---

### 📱 Uyarı Örneği

```
🌐 Alan Adı Takibi Otomasyonu
🔗 Alan Adı: facebook.com
📌 Mevcut Durum: aktif
📅 Son Kullanma Tarihi: 30.03.2034
⏳ Kalan Gün: 2984

🔄 Durum değişti: aktif → yasaklı

🌍 Nameserver'lar:
A.NS.FACEBOOK.COM
B.NS.FACEBOOK.COM

🕒 Son Kontrol: 28.01.2026, 12:42:17
```

---

### 🔐 Güvenlik Notları

- **Kendi barındırılan:** Kendi altyapınızda çalıştırın - bulut satıcısı bağımlılığı yok
- **Kimlik Bilgileri:** n8n kimlik bilgileri yöneticisinde güvenli şekilde saklayın
- **Hız Sınırlaması:** Sorgular arasında yerleşik 1 saniye gecikmesi
- **Hata İşleme:** Başarısız aramalarda devam eder, hataları günlüğe kaydeder
- **Veri Gizliliği:** Tablosu özel kalır



---

### 🛠️ Sorun Giderme

**Domain güncellemiyor mu?**
- Domain TLD'sinin desteklenen listede olup olmadığını kontrol edin
- RDAP sunucusunun yanıt verip vermediğini doğrulayın (manuel HTTP isteği deneyin)
- n8n yürütme günlüklerini kontrol edin

**Telegram uyarıları gönderilmiyor mu?**
- Bot Token'ın doğru olduğunu doğrulayın
- Chat ID'nin sayısal olduğunu ve sohbetinizle eşleştiğini onaylayın
- Test: Telegram'da bot'u etkinleştirmek için `/start` mesajı gönderin

**Sheet güncellemiyor mu?**
- Google Sheets kimlik bilgisinin yazma izni olduğunu onaylayın
- Sütun başlıklarının tam olarak eşleştiğini doğrulayın
- Sheet'in n8n hizmet hesabı ile paylaşılıp paylaşılmadığını kontrol edin

Ayrıntılı çözümler için `docs/TROUBLESHOOTING.md`'ye bakın.

---


### 💡 Kullanım Alanları

- **Acenteler:** 50+ müşteri domain'ini otomatik olarak izleyin
- **E-Ticaret:** Görev kritik domain son kullanma tarihleri için uyarılar
- **DevOps:** Altyapı otomasyonu ile entegre edin
- **Güvenlik Ekipleri:** Yetkisiz nameserver değişikliklerini izleyin
- **Kayıt Defteri İzlemesi:** Birden fazla kayıt defteri hesabını takip edin

---

### 🤝 Katkıda Bulunma

Katkılar memnuniyetle karşılanır! Lütfen:

1. Depoyu çatallayın
2. Özellik dalı oluşturun (`git checkout -b feature/improvement`)
3. Değişiklikleri işleyin (`git commit -am 'Özellik ekle'`)
4. Dala itin (`git push origin feature/improvement`)
5. Pull Request açın

---


### 🙋 Destek

- **Sorunlar:** Hata günlükleri ile GitHub sorunu açın
- **Tartışmalar:** Özellik istekleri için tartışma başlatın
- **Belgeler:** Ayrıntılı rehberler için `docs/` klasörüne bakın

---

### ✨ Sürüm Geçmişi

**v1.0** (Oca 2026)
- İlk yayın RDAP desteği ile
- 30+ TLD kayıt defteri desteği
- Akıllı değişim algılama
- Telegram bildirimleri
- Google Sheets entegrasyonu

---

**Made with ❤️ for domain enthusiasts and DevOps teams worldwide**
