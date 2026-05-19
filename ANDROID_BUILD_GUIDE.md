# 📱 Android APK Oluşturma Rehberi

## ⚠️ ÖNEMLİ NOTLAR

**GitHub'a yüklediğinizde:**
- ❌ Otomatik APK oluşturmaz (ekstra yapılandırma gerekir)
- ✅ GitHub Actions workflow'u eklendi (bu dosyada açıklanıyor)
- ✅ Manuel build yapabilirsiniz
- ✅ GitHub Actions ile otomatik build yapabilirsiniz

---

## 🎯 İki Yöntem Var

### **Yöntem 1: Lokal Bilgisayarınızda APK Oluşturma** (Önerilen)
### **Yöntem 2: GitHub Actions ile Otomatik APK** (Gelişmiş)

---

# 📦 YÖNTEM 1: Lokal Build (Bilgisayarınızda)

## Ön Gereksinimler

✅ Node.js 18+
✅ Android Studio (veya Android SDK)
✅ Java JDK 17+

## Adım Adım Kurulum

### 1️⃣ Projeyi Klonlayın

```bash
git clone <your-repo-url>
cd moto-pro-gps-tracker
npm install
```

### 2️⃣ Capacitor Kurulumu

```bash
# Zaten package.json'da var, tekrar yüklemeye gerek yok
# Ama kontrol için:
npm install @capacitor/core @capacitor/cli @capacitor/android
```

### 3️⃣ Android Platform Ekleme

```bash
# Web build
npm run build

# Android platform ekle (ilk kez)
npm run android:init

# veya shortcut:
npx cap add android
```

### 4️⃣ Android Studio Kurulumu

**Android Studio yoksa:**

1. İndirin: https://developer.android.com/studio
2. Kurun
3. SDK Manager'dan Android SDK Platform-Tools kurun
4. Android SDK (API 33+) kurun

**ANDROID_HOME environment variable ayarlayın:**

```bash
# Linux/Mac
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/platform-tools

# Windows (PowerShell)
$env:ANDROID_HOME = "C:\Users\YourName\AppData\Local\Android\Sdk"
```

### 5️⃣ APK Build

**Yöntem A: Komut Satırı (Hızlı)**

```bash
# Debug APK
npm run android:build

# veya manuel:
cd android
./gradlew assembleDebug

# APK konumu:
# android/app/build/outputs/apk/debug/app-debug.apk
```

**Yöntem B: Android Studio (GUI)**

```bash
# Android Studio'yu aç
npm run android:open

# Android Studio içinde:
# Build → Build Bundle(s) / APK(s) → Build APK(s)
```

### 6️⃣ APK'yı Telefonunuza Kurun

**USB ile:**

```bash
# USB debugging aktif olmalı
adb install android/app/build/outputs/apk/debug/app-debug.apk
```

**Manuel:**

1. APK dosyasını telefonunuza kopyalayın
2. Dosya yöneticisinden açın
3. "Bilinmeyen kaynaklardan yükleme" iznini verin
4. Kurun

---

# 🤖 YÖNTEM 2: GitHub Actions ile Otomatik APK

## Nasıl Çalışır?

Projeye `.github/workflows/android-build.yml` dosyası eklendi. Bu dosya:

- ✅ Her push'ta otomatik build yapar
- ✅ APK'yı GitHub Actions Artifacts'e yükler
- ✅ Release oluşturur (main/master branch)

## Kurulum Adımları

### 1️⃣ Projeyi GitHub'a Yükleyin

```bash
git init
git add .
git commit -m "Initial commit with Android build support"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/moto-pro-gps-tracker.git
git push -u origin main
```

### 2️⃣ Android Platform'u İlk Kez Oluşturun

**Lokal bilgisayarınızda:**

```bash
npm run build
npx cap add android
git add android/
git commit -m "Add Android platform"
git push
```

### 3️⃣ GitHub Actions İzinlerini Ayarlayın

1. GitHub repo → **Settings**
2. **Actions** → **General**
3. **Workflow permissions** → **Read and write permissions** seçin
4. **Allow GitHub Actions to create and approve pull requests** işaretleyin
5. **Save**

### 4️⃣ İlk Build'i Tetikleyin

```bash
# Herhangi bir değişiklik yapın ve push edin
git add .
git commit -m "Trigger Android build"
git push
```

### 5️⃣ Build Sonucunu İndirin

1. GitHub repo → **Actions** sekmesi
2. En son workflow'a tıklayın
3. **Artifacts** bölümünden `moto-pro-debug.apk` indirin
4. Zip'i açın ve APK'yı telefonunuza kurun

### 6️⃣ Release'den İndirin (Main branch)

1. GitHub repo → **Releases**
2. En son release'i bulun
3. Assets bölümünden APK'yı indirin

---

## 🔧 Android Manifest İzinleri

`android/app/src/main/AndroidManifest.xml` dosyasına şu izinleri ekleyin:

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android">

    <!-- GPS İzinleri -->
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION" />
    
    <!-- Sensör İzinleri -->
    <uses-permission android:name="android.permission.BODY_SENSORS" />
    <uses-permission android:name="android.permission.HIGH_SAMPLING_RATE_SENSORS" />
    
    <!-- Internet -->
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    
    <!-- Dosya İndirme -->
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    
    <!-- Ekran Açık Kalma -->
    <uses-permission android:name="android.permission.WAKE_LOCK" />

    <application>
        <!-- App config -->
    </application>

</manifest>
```

---

## 📝 Capacitor Config Dosyası

`capacitor.config.ts` dosyası zaten oluşturuldu:

```typescript
import { CapacitorConfig } from '@capacitor/cli';

const config: CapacitorConfig = {
  appId: 'com.motopro.tracker',
  appName: 'Moto Pro GPS Tracker',
  webDir: 'dist',
  bundledWebRuntime: false,
  server: {
    androidScheme: 'https',
    cleartext: true
  },
  android: {
    allowMixedContent: true
  }
};

export default config;
```

**App ID değiştirme:**

`com.motopro.tracker` yerine kendi domain'inizi kullanın:
- `com.yourname.motopro`
- `com.yourcompany.tracker`
- vb.

---

## 🎨 App İkonu ve Splash Screen

### İkon Oluşturma

1. 1024x1024 PNG ikon hazırlayın
2. https://icon.kitchen kullanın (ücretsiz)
3. Android resources indirin
4. `android/app/src/main/res/` klasörüne kopyalayın

### Splash Screen

`android/app/src/main/res/drawable/splash.png` oluşturun (2732x2732 px)

---

## 🔐 Production APK (İmzalı)

### 1. Keystore Oluşturun

```bash
keytool -genkey -v -keystore moto-pro-release.keystore \
  -alias moto-pro -keyalg RSA -keysize 2048 -validity 10000
```

### 2. Keystore Bilgilerini Ekleyin

`android/gradle.properties` dosyasına:

```properties
MOTO_PRO_RELEASE_STORE_FILE=../moto-pro-release.keystore
MOTO_PRO_RELEASE_KEY_ALIAS=moto-pro
MOTO_PRO_RELEASE_STORE_PASSWORD=your-store-password
MOTO_PRO_RELEASE_KEY_PASSWORD=your-key-password
```

### 3. Build Config

`android/app/build.gradle` dosyasında:

```gradle
android {
    signingConfigs {
        release {
            storeFile file(MOTO_PRO_RELEASE_STORE_FILE)
            storePassword MOTO_PRO_RELEASE_STORE_PASSWORD
            keyAlias MOTO_PRO_RELEASE_KEY_ALIAS
            keyPassword MOTO_PRO_RELEASE_KEY_PASSWORD
        }
    }
    
    buildTypes {
        release {
            signingConfig signingConfigs.release
            minifyEnabled true
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
}
```

### 4. Release Build

```bash
cd android
./gradlew assembleRelease

# APK konumu:
# android/app/build/outputs/apk/release/app-release.apk
```

---

## 🚀 Google Play Store Yayınlama

### 1. AAB (Bundle) Oluşturun

```bash
cd android
./gradlew bundleRelease

# AAB konumu:
# android/app/build/outputs/bundle/release/app-release.aab
```

### 2. Play Console'a Yükleyin

1. https://play.google.com/console
2. Uygulama oluştur
3. AAB dosyasını yükle
4. Store listing bilgilerini doldur
5. Yayınla

---

## 🐛 Sorun Giderme

### Hata: "SDK location not found"

```bash
# android/local.properties oluştur:
sdk.dir=/path/to/Android/Sdk

# veya:
echo "sdk.dir=$ANDROID_HOME" > android/local.properties
```

### Hata: "Gradle build failed"

```bash
cd android
./gradlew clean
./gradlew assembleDebug --stacktrace
```

### Hata: "Java version mismatch"

```bash
# Java 17 kullanın
java -version

# Eğer farklı ise:
export JAVA_HOME=/path/to/jdk-17
```

### GitHub Actions Başarısız

1. **Actions** sekmesinde log'lara bakın
2. Android platform'un commit edildiğinden emin olun
3. Workflow permissions kontrolü yapın

---

## 📊 Build Boyutları

- **Debug APK**: ~15-20 MB
- **Release APK**: ~10-15 MB (minified)
- **AAB (Bundle)**: ~8-12 MB

---

## ✅ Checklist

Build öncesi kontrol:

- [ ] `npm run build` başarılı
- [ ] `capacitor.config.ts` var
- [ ] Android platform eklendi (`android/` klasörü var)
- [ ] Android SDK kurulu
- [ ] Java JDK 17 kurulu
- [ ] `ANDROID_HOME` ayarlandı
- [ ] Manifest izinleri eklendi

---

## 🎯 Hızlı Komutlar

```bash
# Web build
npm run build

# Android sync (web değişiklikleri Android'e kopyala)
npm run android:sync

# Android Studio aç
npm run android:open

# Debug APK build
npm run android:build

# Release APK (imzalı)
cd android && ./gradlew assembleRelease

# AAB bundle (Play Store)
cd android && ./gradlew bundleRelease

# Emulator'da test
npx cap run android
```

---

## 📱 APK Test

Telefonunuzda test ederken:

1. **Ayarlar** → **Güvenlik**
2. **Bilinmeyen kaynaklardan yükleme** iznini verin
3. APK'yı kopyalayın ve açın
4. GPS ve sensör izinlerini verin

---

## 🔗 Faydalı Linkler

- Capacitor Docs: https://capacitorjs.com/docs
- Android Studio: https://developer.android.com/studio
- Gradle Docs: https://docs.gradle.org
- GitHub Actions: https://docs.github.com/actions

---

**Başarılar! 🏍️📱**
