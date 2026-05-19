# 📦 MOTO PRO - Tüm Proje Dosyaları

Bu dosya, projenin tüm dosyalarını ve konumlarını içerir.

## 📁 Klasör Yapısı

```
moto-pro-gps-tracker/
│
├── index.html                    # Ana HTML dosyası
├── package.json                  # NPM bağımlılıkları
├── tsconfig.json                 # TypeScript konfigürasyonu
├── vite.config.ts                # Vite build konfigürasyonu
├── .gitignore                    # Git ignore dosyası
├── README.md                     # Proje dokümantasyonu
├── SETUP.md                      # Kurulum talimatları
│
└── src/
    ├── main.tsx                  # React entry point
    ├── App.tsx                   # Ana uygulama component'i
    ├── index.css                 # Global CSS
    ├── types.ts                  # TypeScript tip tanımlamaları
    │
    └── utils/
        ├── cn.ts                 # Tailwind utility
        ├── fitExporter.ts        # FIT dosya export fonksiyonu
        ├── sensors.ts            # Sensor yönetimi
        ├── storage.ts            # LocalStorage yönetimi
        └── weatherApi.ts         # Hava durumu API'si
```

## 🔧 Dosya Sayısı

- **Toplam:** 15 dosya
- **TypeScript/TSX:** 9 dosya
- **Config:** 3 dosya
- **Dokümantasyon:** 3 dosya

## ✅ Dosya Kontrol Listesi

- [x] index.html - ✓
- [x] package.json - ✓
- [x] tsconfig.json - ✓
- [x] vite.config.ts - ✓
- [x] .gitignore - ✓
- [x] README.md - ✓
- [x] SETUP.md - ✓
- [x] src/main.tsx - ✓
- [x] src/App.tsx - ✓
- [x] src/index.css - ✓
- [x] src/types.ts - ✓
- [x] src/utils/cn.ts - ✓
- [x] src/utils/fitExporter.ts - ✓
- [x] src/utils/sensors.ts - ✓
- [x] src/utils/storage.ts - ✓
- [x] src/utils/weatherApi.ts - ✓

## 🎯 Her Dosyanın Amacı

### Root Dosyalar

| Dosya | Amaç |
|-------|------|
| index.html | HTML template ve entry point |
| package.json | NPM bağımlılıkları ve scriptler |
| tsconfig.json | TypeScript derleyici ayarları |
| vite.config.ts | Vite build tool konfigürasyonu |
| .gitignore | Git'te ignore edilecek dosyalar |
| README.md | Proje dokümantasyonu |
| SETUP.md | Kurulum ve build talimatları |

### src/ Dosyaları

| Dosya | Amaç |
|-------|------|
| main.tsx | React uygulamasının başlangıç noktası |
| App.tsx | Ana uygulama component'i (2500+ satır) |
| index.css | Global Tailwind CSS import |
| types.ts | TypeScript interface ve type tanımları |

### src/utils/ Dosyaları

| Dosya | Amaç |
|-------|------|
| cn.ts | Tailwind class merge utility |
| fitExporter.ts | FIT dosya oluşturma ve export |
| sensors.ts | Device sensors yönetimi (GPS, Gyro, Accel) |
| storage.ts | LocalStorage CRUD işlemleri |
| weatherApi.ts | Hava durumu API entegrasyonu |

## 📊 Satır Sayıları (Yaklaşık)

```
src/App.tsx           : ~700 satır
src/utils/sensors.ts  : ~120 satır
src/utils/fitExporter.ts : ~100 satır
src/utils/storage.ts  : ~60 satır
src/utils/weatherApi.ts : ~80 satır
src/types.ts          : ~45 satır
src/main.tsx          : ~10 satır
src/index.css         : ~3 satır
-----------------------------------
Toplam                : ~1,118 satır kod
```

## 🚀 Manuel Kurulum Adımları

1. Yeni bir klasör oluşturun: `moto-pro-gps-tracker`
2. Aşağıdaki dosyaları tam olarak belirtilen yerlere kopyalayın
3. Terminal'de `npm install` çalıştırın
4. `npm run build` ile derleyin

## ⚠️ Önemli Notlar

- Tüm dosya yolları **CASE-SENSITIVE**'dir
- `src/main.tsx` dosyası mutlaka **tsx** uzantılı olmalı
- `index.html` içindeki import yolu `/src/main.tsx` olmalı
- Node.js 18+ gereklidir
- UTF-8 encoding kullanın

## 🔍 Dosya İçerikleri

Her dosyanın tam içeriği aşağıdaki bölümlerde verilmiştir.
