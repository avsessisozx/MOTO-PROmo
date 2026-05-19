# 🏍️ MOTO PRO - GPS Telemetry Tracker

Premium motosiklet GPS telemetri takip uygulaması. DJI Action kameralar için FIT formatında telemetri verisi oluşturur.

## 📱 APK İNDİRME

### GitHub'dan APK almak için:

**Yöntem 1: GitHub Actions ile Otomatik Build**
1. Projeyi fork edin veya klonlayın
2. `ANDROID_BUILD_GUIDE.md` dosyasındaki adımları takip edin
3. GitHub Actions otomatik APK oluşturacak
4. **Actions** sekmesinden indirin

**Yöntem 2: Lokal Build**
1. `npm install` yapın
2. `npm run android:init` ile Android platform ekleyin
3. `npm run android:build` ile APK oluşturun
4. APK konumu: `android/app/build/outputs/apk/debug/app-debug.apk`

Detaylı rehber: **[ANDROID_BUILD_GUIDE.md](./ANDROID_BUILD_GUIDE.md)**

## ✨ Özellikler

### 📡 Gelişmiş Sensör Desteği
- **GPS Tracking**: Konum, hız, yükseklik, yön
- **Accelerometer**: İvmelenme ve G-force ölçümü
- **Gyroscope**: Yatış açısı (lean angle) takibi
- **Magnetometer**: Pusula ve yön bilgisi
- **Weather API**: Hava durumu verisi (opsiyonel)

### 🎯 Motosiklet Vlog Özellikleri
- ⚡ **Gerçek Zamanlı Yatış Açısı**: Sol/sağ yatış ölçümü (-90° ile 90° arası)
- 💪 **G-Force Göstergesi**: İvmelenme kuvveti hesaplama
- 🏁 **Viraj Sayacı**: Sol ve sağ virajları otomatik sayar
- 📊 **Detaylı İstatistikler**: 12+ farklı metrik
- 🌤️ **Hava Durumu**: Sıcaklık, nem, rüzgar hızı
- 📍 **GPS Noktaları**: Saniyede ~1 nokta kayıt

### 💾 Kayıt Defteri
- 📚 Tüm sürüşlerinizi kaydedin ve saklayın
- 📝 Her sürüşe özel isim verin
- 📅 Tarih ve saat bilgisi
- 🔍 Detaylı görüntüleme
- ✏️ Sürüş isimlerini düzenleme
- 🗑️ İstenmeyen kayıtları silme

### 🎨 Premium Tasarım
- 🌙 Modern koyu tema
- 💫 Gradient efektler ve animasyonlar
- 📱 Tam responsive tasarım
- ⚡ Büyük, kolay kullanılır butonlar
- 🎯 Gerçek zamanlı veri göstergeleri
- 🏆 Premium kartlar ve istatistikler

### 📤 FIT Dosya Dışa Aktarımı
- ✅ DJI Mimo uyumlu
- ✅ DJI Studio uyumlu
- ✅ Garmin FIT standardı
- ✅ Tüm telemetri verileri dahil
- ✅ GPS koordinatları
- ✅ Yükseklik profili
- ✅ Hız verileri
- ✅ Zaman damgaları

## 🚀 Kullanım

### 1️⃣ İlk Kurulum
1. Uygulamayı açın
2. GPS ve sensör izinlerini verin
3. (Opsiyonel) Tarayıcınızın "Anasayfaya Ekle" özelliğini kullanarak PWA olarak kurun

### 2️⃣ Kayıt Yapma
1. **"KAYDI BAŞLAT"** butonuna basın
2. Motosikletinize binin ve sürüşe başlayın
3. Gerçek zamanlı verileri takip edin:
   - Anlık hız
   - Yükseklik
   - Yatış açısı (sol/sağ)
   - G-Force
4. Gerekirse **"DURAKLAT"** ile mola verin
5. Sürüş bitince **"DURDUR"** butonuna basın
6. **"SÜRÜŞÜ KAYDET"** ile kalıcı olarak saklayın

### 3️⃣ Geçmiş ve Detaylar
1. **"Geçmiş"** sekmesine geçin
2. Kayıtlı sürüşlerinizi görüntüleyin
3. Bir sürüşe tıklayarak detaylara bakın
4. Sürüş ismini düzenleyin (✏️ ikonu)
5. **"FIT DOSYASI OLARAK İNDİR"** ile dışa aktarın

### 4️⃣ DJI'a Aktarma
1. İndirilen `.fit` dosyasını telefonunuza kaydedin
2. DJI Mimo veya DJI Studio uygulamasını açın
3. Videonuzu import edin
4. FIT dosyasını telemetri olarak ekleyin
5. Otomatik overlay'ler oluşun:
   - Hız göstergesi
   - Yükseklik grafiği
   - GPS haritası
   - G-Force göstergesi
   - Lean angle animasyonu

## 📊 Ölçülen Veriler

| Veri | Kaynak | Açıklama |
|------|--------|----------|
| **Konum** | GPS | Enlem/Boylam koordinatları |
| **Hız** | GPS | km/s cinsinden anlık hız |
| **Yükseklik** | GPS | Deniz seviyesinden metre |
| **Yön** | GPS + Magnetometer | Pusula yönü (0-360°) |
| **Yatış Açısı** | Gyroscope | Sol/Sağ eğim (-90° ile 90°) |
| **G-Force** | Accelerometer | İvme kuvveti (G cinsinden) |
| **Mesafe** | Hesaplanan | Haversine formülü ile |
| **Tırmanış** | Hesaplanan | Pozitif yükseklik değişimi |
| **Virajlar** | Hesaplanan | >15° yatış açısı tespiti |
| **Hava Durumu** | Weather API | Sıcaklık, nem, rüzgar |

## 🔧 Teknik Detaylar

### Teknoloji Yığını
- **React 19** - UI framework
- **TypeScript** - Type safety
- **Tailwind CSS 4** - Premium styling
- **Vite 7** - Build tool
- **@markw65/fit-file-writer** - FIT dosya oluşturma

### Tarayıcı API'leri
- **Geolocation API** - GPS tracking
- **DeviceMotion API** - Accelerometer
- **DeviceOrientation API** - Gyroscope & Magnetometer
- **LocalStorage API** - Veri saklama
- **Blob API** - Dosya indirme

### Sensör Desteği
- ✅ **iOS 13+**: DeviceMotion permission gerekli
- ✅ **Android**: Otomatik izin
- ✅ **Desktop**: GPS varsa çalışır (sensörler yok)

### Tarayıcı Uyumluluğu
- ✅ Chrome/Edge 90+
- ✅ Safari 13+
- ✅ Firefox 88+
- ✅ Samsung Internet 14+

## 💡 İpuçları

### En İyi Performans İçin
1. **Telefonu Sabit Tutun**: Motosiklete ram mount ile sabitleyin
2. **Tam Şarjlı Başlayın**: GPS tracking batarya tüketir
3. **Mobil Veri**: Hava durumu için internet gerekli
4. **Ekran Açık**: Uygulama ön planda çalışmalı
5. **Uçak Modunu Kapatın**: GPS çalışması için gerekli

### Veri Kalitesi
- GPS sinyali açık alanda daha iyidir
- Yüksek binalar sinyal kalitesini düşürür
- İlk GPS fix 30-60 saniye alabilir
- Sensor kalibrasyonu için telefonun düz durması önerilir

### Kayıt Yönetimi
- LocalStorage kapasitesi ~5-10MB
- Ortalama sürüş ~100-500KB
- ~20-50 sürüş kaydedilebilir
- Düzenli olarak FIT export yapıp silin

## 🆘 Sorun Giderme

### GPS Çalışmıyor
- Tarayıcı izinlerini kontrol edin
- Konum servislerinin açık olduğundan emin olun
- Açık alanda test edin
- Sayfayı yenileyin

### Sensörler Çalışmıyor
- iOS'ta izin verdiğinizden emin olun
- HTTPS bağlantısı gerekli (localhost hariç)
- Telefonu hafifçe hareket ettirin (kalibre için)

### FIT Dosyası Oluşturulamıyor
- En az 2 GPS noktası gerekli
- Tarayıcı depolama alanını kontrol edin
- Popup blocker'ı devre dışı bırakın

### Hava Durumu Gelmiyor
- Internet bağlantınızı kontrol edin
- Demo modda çalışıyor (gerçek API key eklenebilir)

## 🔐 Gizlilik

- Tüm veriler cihazınızda saklanır (LocalStorage)
- Sunucuya veri gönderilmez
- Hava durumu için sadece konum paylaşılır (opsiyonel)
- Verilerinizi istediğiniz zaman silebilirsiniz

## 📝 Lisans

Bu proje kişisel kullanım içindir. Ticari kullanım için izin gereklidir.

## 🤝 Katkıda Bulunma

Önerileriniz ve geri bildirimleriniz için issue açabilirsiniz.

---

**Made with ❤️ for motorcycle enthusiasts and vloggers**

🏍️💨 Safe rides!
