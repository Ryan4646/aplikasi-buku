# Panduan Build APK - Aplikasi Buku

## Prasyarat
1. Android Studio versi terbaru (Hedgehog 2023.1.1 atau lebih baru)
2. Java Development Kit (JDK) 11 atau lebih tinggi
3. Android SDK dengan target API level 34
4. Gradle versi 8.1.0 atau lebih baru

## Langkah-Langkah Membuat APK

### 1. Persiapan Awal
```bash
# Clone repository
git clone https://github.com/Ryan4646/aplikasi-buku.git
cd aplikasi-buku

# Buka dengan Android Studio
# File > Open > pilih folder aplikasi-buku
```

### 2. Sinkronisasi Gradle
- Android Studio akan otomatis mendeteksi file `build.gradle.kts`
- Tunggu proses sinkronisasi selesai
- Jika ada error, cek di panel "Sync Now"

### 3. Build APK (Debug)
```bash
# Melalui terminal di Android Studio
./gradlew assembleDebug

# File output: app/build/outputs/apk/debug/app-debug.apk
```

### 4. Build APK (Release) - Untuk Production
```bash
# Buat keystore jika belum ada
keytool -genkey -v -keystore release.keystore -keyalg RSA -keysize 2048 -validity 10000 -alias release-key

# Build signed APK
./gradlew assembleRelease

# File output: app/build/outputs/apk/release/app-release.apk
```

### 5. Alternatif: Build melalui Android Studio GUI
- Menu: Build > Build Bundle(s) / APK(s) > Build APK(s)
- Tunggu proses selesai
- Klik "Locate" untuk membuka folder output

## Konfigurasi Important
- **Compile SDK:** 34
- **Min SDK:** 21 (Android 5.0 Lollipop)
- **Target SDK:** 34 (Android 14)
- **Package Name:** com.buku.aplikasi

## Troubleshooting

### Error: "Could not find com.android.application"
```bash
# Update gradle wrapper
./gradlew wrapper --gradle-version=8.1.0
```

### Error: "Build failed"
- Cek Java version: `java -version` (harus 11+)
- Rebuild project: Build > Clean Project
- Invalidate caches: File > Invalidate Caches

### APK Terlalu Besar
- Aktifkan minification: `isMinifyEnabled = true`
- Gunakan `proguard-rules.pro` untuk optimasi

## Install APK di Device/Emulator
```bash
# Debug APK
adb install app/build/outputs/apk/debug/app-debug.apk

# Release APK
adb install app/build/outputs/apk/release/app-release.apk
```

## Struktur Folder Project
```
aplikasi-buku/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/buku/aplikasi/
│   │   │   ├── res/
│   │   │   └── AndroidManifest.xml
│   │   └── test/
│   └── build.gradle.kts
├── settings.gradle.kts
├── build.gradle.kts
└── proguard-rules.pro
```

## Tips Pengembangan
1. Gunakan emulator dengan API 29+ untuk testing
2. Test di berbagai ukuran layar (portrait & landscape)
3. Aktifkan developer mode di device fisik
4. Gunakan logcat untuk debugging
5. Monitor performance dengan Android Profiler

## Distribusi APK
Setelah APK berhasil dibuat:
1. **Google Play Store:** Upload APK signed release
2. **Direct Distribution:** Share APK langsung ke user
3. **Firebase App Distribution:** Setup untuk beta testing

---
**Build Date:** 2026-05-21
**Version:** 1.0
**Package:** com.buku.aplikasi
