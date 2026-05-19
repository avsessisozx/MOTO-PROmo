# 🏍️ MOTO PRO - Komple Proje Kurulum Rehberi

## 📦 Proje Dosyalarını Manuel Oluşturma

Aşağıdaki adımları takip ederek projeyi sıfırdan oluşturabilirsiniz.

---

## 1️⃣ Klasör Yapısını Oluşturun

```bash
mkdir moto-pro-gps-tracker
cd moto-pro-gps-tracker
mkdir src
mkdir src/utils
```

---

## 2️⃣ Root Seviye Dosyalar

### 📄 `package.json`

```json
{
  "name": "moto-pro-gps-tracker",
  "private": true,
  "version": "1.0.0",
  "type": "module",
  "description": "Premium motosiklet GPS telemetri tracker - DJI Action için FIT dosya oluşturucu",
  "author": "Your Name",
  "license": "MIT",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "clean": "rm -rf node_modules dist",
    "reinstall": "npm run clean && npm install",
    "type-check": "tsc --noEmit"
  },
  "dependencies": {
    "@markw65/fit-file-writer": "^0.1.9",
    "clsx": "2.1.1",
    "react": "19.2.6",
    "react-dom": "19.2.6",
    "tailwind-merge": "3.4.0"
  },
  "devDependencies": {
    "@tailwindcss/vite": "4.1.17",
    "@types/node": "22.19.17",
    "@types/react": "19.2.7",
    "@types/react-dom": "19.2.3",
    "@vitejs/plugin-react": "5.1.1",
    "tailwindcss": "4.1.17",
    "typescript": "5.9.3",
    "vite": "7.3.2",
    "vite-plugin-singlefile": "2.3.0"
  }
}
```

### 📄 `tsconfig.json`

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "useDefineForClassFields": true,
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "module": "ESNext",
    "skipLibCheck": true,
    "types": ["node"],

    /* Bundler mode */
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx",

    /* Path mapping */
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
    },

    /* Linting */
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true
  },
  "include": ["src", "vite.config.ts"]
}
```

### 📄 `vite.config.ts`

```typescript
import path from "path";
import { fileURLToPath } from "url";
import tailwindcss from "@tailwindcss/vite";
import react from "@vitejs/plugin-react";
import { defineConfig } from "vite";
import { viteSingleFile } from "vite-plugin-singlefile";

const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);

// https://vite.dev/config/
export default defineConfig({
  plugins: [react(), tailwindcss(), viteSingleFile()],
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "src"),
    },
  },
});
```

### 📄 `index.html`

```html
<!DOCTYPE html>
<html lang="tr">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" content="Motosiklet GPS Telemetri Tracker - DJI Action için FIT dosya oluşturucu" />
    <meta name="theme-color" content="#DC2626" />
    <link rel="icon" type="image/svg+xml" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>🏍️</text></svg>" />
    <title>MOTO PRO - GPS Telemetry Tracker</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.tsx"></script>
  </body>
</html>
```

### 📄 `.gitignore`

```
# Logs
logs
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*
pnpm-debug.log*
lerna-debug.log*

# Dependencies
node_modules
dist
dist-ssr
*.local

# Editor directories and files
.vscode/*
!.vscode/extensions.json
.idea
.DS_Store
*.suo
*.ntvs*
*.njsproj
*.sln
*.sw?

# Environment variables
.env
.env.local
.env.production.local
.env.development.local
.env.test.local

# Build output
dist/
build/

# Cache
.cache/
.vite/
.turbo/

# Testing
coverage/
.nyc_output/

# Misc
*.tsbuildinfo
```

---

## 3️⃣ src/ Klasörü Dosyaları

### 📄 `src/index.css`

```css
@import "tailwindcss";
```

### 📄 `src/main.tsx`

```typescript
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import "./index.css";
import App from "./App";

createRoot(document.getElementById("root")!).render(
  <StrictMode>
    <App />
  </StrictMode>
);
```

---

## 4️⃣ Kurulum Komutları

Tüm dosyaları oluşturduktan sonra:

```bash
# 1. Bağımlılıkları yükle
npm install

# 2. Geliştirme sunucusunu başlat
npm run dev

# 3. Production build
npm run build

# 4. Build'i test et
npm run preview
```

---

## 5️⃣ Build Sorunları için Çözümler

### Sorun: "Failed to resolve /src/main.tsx"

**Çözüm:**
```bash
# Cache temizle
rm -rf node_modules/.vite
rm -rf dist
npm run build
```

### Sorun: "Module not found"

**Çözüm:**
```bash
# Tüm node_modules'ü sil ve yeniden yükle
rm -rf node_modules package-lock.json
npm install
```

### Sorun: TypeScript hataları

**Çözüm:**
```bash
# Type check
npm run type-check

# Hataları görmezden gel (geçici)
# tsconfig.json içinde "strict": false yap
```

---

## 6️⃣ Android Studio ile Derleme

### Capacitor ile (Önerilen):

```bash
# 1. Capacitor kur
npm install @capacitor/core @capacitor/cli
npm install @capacitor/android

# 2. Initialize
npx cap init "Moto Pro" "com.motopro.tracker"

# 3. Web build
npm run build

# 4. Android ekle
npx cap add android

# 5. Copy web assets
npx cap copy android

# 6. Android Studio'da aç
npx cap open android
```

### capacitor.config.ts oluşturun:

```typescript
import { CapacitorConfig } from '@capacitor/cli';

const config: CapacitorConfig = {
  appId: 'com.motopro.tracker',
  appName: 'Moto Pro',
  webDir: 'dist',
  bundledWebRuntime: false,
  server: {
    androidScheme: 'https'
  }
};

export default config;
```

---

## 7️⃣ GitHub Actions Build

`.github/workflows/build.yml` oluşturun:

```yaml
name: Build

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    
    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'
        
    - name: Install dependencies
      run: npm ci
      
    - name: Build
      run: npm run build
      
    - name: Upload artifacts
      uses: actions/upload-artifact@v3
      with:
        name: dist
        path: dist/
```

---

## 8️⃣ Dosya Boyutları Kontrolü

Build sonrası beklenen çıktı:

```
dist/index.html  ~818 kB │ gzip: ~160 kB
✓ built in ~2s
```

---

## 9️⃣ Test Checklist

- [ ] `npm install` çalışıyor
- [ ] `npm run dev` sunucuyu başlatıyor
- [ ] `npm run build` hatasız tamamlanıyor
- [ ] `dist/index.html` oluşuyor
- [ ] Tarayıcıda açılınca GPS izni istiyor
- [ ] Sensör verileri gösteriliyor
- [ ] FIT dosyası indirilebiliyor
- [ ] LocalStorage'a kayıt yapılıyor

---

## 🆘 Destek

Sorun yaşıyorsanız:

1. ✅ Node.js versiyonunu kontrol edin: `node -v` (18+ olmalı)
2. ✅ Dosya yapısını kontrol edin
3. ✅ Tüm dosyaların UTF-8 encoding'de olduğundan emin olun
4. ✅ Dosya isimlerinin tam eşleştiğinden emin olun (case-sensitive!)

---

## ✅ Başarı Kriterleri

Build başarılı olduğunda:
- ✓ `dist/` klasörü oluşmalı
- ✓ `dist/index.html` ~800KB olmalı
- ✓ Console'da hata olmamalı
- ✓ Tarayıcıda açıldığında uygulama çalışmalı

---

**Not:** Diğer dosyaların (App.tsx, types.ts, utils/*) tam içeriği için projedeki mevcut dosyalara bakın. Bunlar zaten doğru konumlarda oluşturulmuş durumda.

## 📥 Projeyi İndirme

Eğer GitHub'dan indiriyorsanız:

```bash
git clone <repository-url>
cd moto-pro-gps-tracker
npm install
npm run build
```

Başarılar! 🏍️💨
