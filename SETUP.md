# 🚀 MOTO PRO - Kurulum Talimatları

## 📋 Gereksinimler

- Node.js 18+ 
- npm 9+ veya yarn 1.22+

## 🔧 Kurulum Adımları

### 1. Bağımlılıkları Yükleyin

```bash
npm install
```

veya

```bash
yarn install
```

### 2. Geliştirme Sunucusunu Başlatın

```bash
npm run dev
```

veya

```bash
yarn dev
```

Tarayıcınızda `http://localhost:5173` adresini açın.

### 3. Production Build

```bash
npm run build
```

veya

```bash
yarn build
```

Build edilen dosyalar `dist/` klasöründe oluşacaktır.

### 4. Build'i Önizleyin

```bash
npm run preview
```

veya

```bash
yarn preview
```

## 📱 Android Studio ile Derleme

### Yöntem 1: Capacitor ile (Önerilen)

```bash
# Capacitor ekle
npm install @capacitor/core @capacitor/cli
npm install @capacitor/android

# Initialize
npx cap init

# Build
npm run build

# Android platform ekle
npx cap add android

# Android Studio'da aç
npx cap open android
```

### Yöntem 2: Cordova ile

```bash
# Cordova ekle
npm install -g cordova

# Platform ekle
cordova platform add android

# Build
cordova build android
```

## 🐳 Docker ile Build

```bash
# Docker image oluştur
docker build -t moto-pro .

# Container çalıştır
docker run -p 5173:5173 moto-pro
```

## 🔍 Sorun Giderme

### Hata: "Failed to resolve /src/main.tsx"

**Çözüm 1:** node_modules'ü temizleyin
```bash
rm -rf node_modules package-lock.json
npm install
```

**Çözüm 2:** Vite cache'i temizleyin
```bash
rm -rf node_modules/.vite
npm run build
```

**Çözüm 3:** Dosya yollarını kontrol edin
- `src/main.tsx` dosyasının var olduğundan emin olun
- `index.html` dosyasında doğru path olduğundan emin olun

### Hata: "Module not found"

```bash
npm install --legacy-peer-deps
```

### TypeScript Hataları

```bash
# tsconfig.json'u yeniden oluştur
npx tsc --init

# Veya strict modunu kapat
# tsconfig.json içinde "strict": false
```

### Build boyutu çok büyük

`vite.config.ts` dosyasında `viteSingleFile` plugin'ini kaldırın:

```typescript
export default defineConfig({
  plugins: [react(), tailwindcss()],
  // viteSingleFile() kaldırıldı
});
```

## 🌐 Deployment

### Vercel

```bash
npm install -g vercel
vercel
```

### Netlify

```bash
npm install -g netlify-cli
netlify deploy
```

### GitHub Pages

```bash
npm run build
# dist/ klasörünü gh-pages branch'ine push edin
```

## 📦 Dosya Yapısı

```
moto-pro/
├── dist/                 # Build çıktısı
├── src/
│   ├── utils/           # Utility fonksiyonları
│   │   ├── fitExporter.ts
│   │   ├── sensors.ts
│   │   ├── storage.ts
│   │   └── weatherApi.ts
│   ├── App.tsx          # Ana component
│   ├── main.tsx         # Entry point
│   ├── types.ts         # TypeScript tipleri
│   └── index.css        # Global CSS
├── index.html           # HTML template
├── package.json         # Dependencies
├── tsconfig.json        # TypeScript config
├── vite.config.ts       # Vite config
└── README.md            # Dokümantasyon
```

## ✅ Build Başarı Kontrol

Build başarılı olduysa şu çıktıyı görmelisiniz:

```
✓ 35 modules transformed.
dist/index.html  818.10 kB │ gzip: 160.20 kB
✓ built in 2.12s
```

## 🆘 Yardım

Sorun yaşıyorsanız:
1. Node.js versiyonunu kontrol edin: `node -v` (18+ olmalı)
2. npm cache'i temizleyin: `npm cache clean --force`
3. Tüm node_modules'ü silin ve yeniden yükleyin
4. GitHub'da issue açın

## 📞 İletişim

- GitHub Issues: Sorun bildirimi için
- Email: Destek için

---

**Happy Coding! 🏍️💨**
