# Warcraft 3 Android — Indonesia + LAN

![Warsmash Reforged](docs/images/banner.png)

**Versi 0.3.6.4 · versionCode 5 · Android 8.0+ · AsfatreHilmi**

Engine dan launcher Warcraft III untuk Android, berdasarkan
[Warsmash](https://github.com/Retera/WarsmashModEngine). Versi ini memuat
antarmuka Bahasa Indonesia, perbaikan kontrol sentuh, pengaturan performa,
menu sumber daya untuk pemain tunggal, dan multiplayer LAN.

APK memerlukan data Warcraft III milik sendiri. Repositori memuat engine,
launcher, dan kamus lokalisasi; instalasi game lengkap tidak disertakan.

- [Cara mengunggah ke GitHub](docs/CARA-UPLOAD-GITHUB.md)
- [Panduan kontrol](docs/PANDUAN-KONTROL-INDONESIA.txt)
- [Panduan LAN](docs/PANDUAN-LAN-INDONESIA.txt)
- [Catatan versi](CHANGELOG.md)
- [Hasil pemeriksaan paket](docs/VERIFIKASI-v0.3.6.4.md)
- [Dokumentasi upstream dan Windows](docs/README-UPSTREAM.md)

## Fitur versi ini

- Bahasa Indonesia untuk launcher, menu permainan, dan teks yang tersedia
  dalam kamus. Nama hero, peta, dan judul misi dipertahankan.
- Seleksi unit dengan tap, double tap unit sejenis, kotak seleksi, serta
  perintah pekerja untuk menambang, menyetor hasil, membangun, dan memperbaiki.
- Pengaturan target 30/60 FPS dan resolusi render 540p, 720p, atau asli.
  FPS nyata bergantung pada perangkat dan peta.
- Panel sumber daya yang dapat digeser untuk permainan pemain tunggal.
- Host/join LAN melalui Wi-Fi atau hotspot, menggunakan IP host dan peta
  melee/JASS yang sama, untuk 2–12 pemain sesuai slot peta.
- Source engine, Android, desktop, parser, server, dan tes JVM disertakan.

LAN masih memerlukan uji pertandingan lengkap pada dua HP fisik. Peta
kampanye, Lua, dan custom forces seperti Dota belum didukung oleh alur LAN
ini. Rincian implementasi tersedia di [FITUR-LAN.md](FITUR-LAN.md).

## Memasang APK

1. Unduh APK debug versi 0.3.6.4 dari [Releases](../../releases) setelah
   pemilik repositori menerbitkannya. APK juga tersedia dalam folder
   `GitHub-Release-v0.3.6.4` pada paket unggah.
2. Pasang pada Android 8.0 / API 26 atau lebih baru. ABI yang tersedia:
   `arm64-v8a`, `armeabi-v7a`, dan `x86_64`.
3. Sediakan data game dari salinan Warcraft III milik sendiri, versi 1.31
   atau lebih baru, dalam bentuk instalasi CASC atau hasil ekstraksi.
4. Pilih folder data melalui launcher, kemudian buka kampanye, permainan
   kustom, atau **Jaringan lokal (LAN)**.

Paket APK yang disiapkan merupakan build **debug**. Untuk pembaruan aplikasi,
Android memerlukan tanda tangan yang sama dengan APK yang telah terpasang.
APK hasil GitHub Actions menggunakan kunci debug milik runner, sehingga
sertifikatnya dapat berbeda dari APK yang disertakan dalam paket ini.

## Build dari source

Siapkan **JDK 21**, Android SDK Platform **36.1**, dan Build Tools **36.1.0**.
Kode Java ditargetkan ke Java 17; JDK 21 digunakan untuk proses build.
Gradle **9.9.0** tersedia melalui wrapper dan Android Gradle Plugin memakai
versi **9.5.1** yang ditetapkan proyek.

Setel `JAVA_HOME` ke JDK dan `ANDROID_HOME` ke Android SDK, atau isi
`sdk.dir` pada `local.properties` di komputer sendiri. Unduhan dependensi
memerlukan Internet pada build pertama.

Dengan command-line tools Android yang tersedia di PATH:

```bash
sdkmanager "platform-tools" "platforms;android-36.1" "build-tools;36.1.0"
```

Dari folder repositori pada Linux/macOS atau Git Bash:

```bash
chmod +x gradlew
./gradlew :core:test :android:lintDebug :android:assembleDebug --no-daemon --max-workers=2 --console=plain
```

Pada PowerShell:

```powershell
.\gradlew.bat :core:test :android:lintDebug :android:assembleDebug --no-daemon --max-workers=2 --console=plain
```

APK berada di `android/build/outputs/apk/debug/android-debug.apk`.
Laporan tes berada di `core/build/reports/tests/test/index.html` dan laporan
Lint di `android/build/reports/lint-results-debug.html`.

Source paket ini sudah dibangun dari salinan bersih di Linux menggunakan
JDK 21. Hasilnya: **324 tes lulus, 0 gagal; Android Lint 0 error dan 65
warning**. Pemeriksaan ini tidak mencakup gameplay pada perangkat fisik.

## Build melalui GitHub Actions

Workflow [Android](.github/workflows/android.yml) berjalan saat push ke
`main`/`master`, pull request, atau melalui **Actions → Android → Run workflow**.
Workflow menyiapkan JDK/SDK, menjalankan tes dan Lint, lalu membuat APK debug.
Unduh APK dari **Artifacts** pada run yang berhasil. Laporan pemeriksaan
juga disimpan sebagai artifact.

Workflow memakai versi action stabil terbaru yang diperiksa pada
13 November 2026 dan dikunci ke commit masing-masing. Workflow telah
diperiksa secara statis; eksekusi di runner GitHub dilakukan setelah
repositori diunggah. Penerbitan GitHub Release dilakukan melalui panduan
unggah, dengan APK yang dipilih pemilik repositori.

## Struktur proyek

```text
android/       aplikasi, launcher, dan kontrol native Android
core/          engine, lokalisasi, input, LAN, serta tes
shared/        protokol dan kode jaringan bersama
server/        server warisan Warsmash
desktop/       launcher dan engine desktop
jassparser/    parser JASS
fdfparser/     parser FDF
gradle/        Gradle wrapper
jars/          dependensi JAR yang diperlukan build
resources/     skrip dan antarmuka engine
docs/          panduan, gambar, dan hasil pemeriksaan
.github/       workflow GitHub Actions
```

## Catatan perubahan terperinci

- [Lokalisasi Indonesia](LOKALISASI-INDONESIA.md)
- [Kontrol, menu sumber daya, dan FPS](PERBAIKAN-KONTROL-MOD-FPS.md)
- [Penyesuaian Redmi Note 9 Pro](PERBAIKAN-REDMI-NOTE9-PRO.md)
- [Seleksi dan perintah pekerja](PERBAIKAN-SELEKSI-PERINTAH.md)
- [Multiplayer LAN](FITUR-LAN.md)

## Kredit dan lisensi

- [Retera/WarsmashModEngine](https://github.com/Retera/WarsmashModEngine)
  dan para kontributor Warsmash.
- Penyesuaian versi Indonesia/Android: **AsfatreHilmi**.
- libGDX, LWJGL, ANTLR, Gson, Guava, Apache Commons, FFmpeg/JavaCPP,
  serta komponen lain mengikuti lisensi masing-masing.

Engine dan launcher menggunakan **GNU AGPL-3.0**; lihat [LICENSE](LICENSE).
Nama, aset, dan teks Warcraft III merupakan milik pemegang haknya; lisensi
engine tidak mengalihkan hak tersebut. Asal kamus dan metode penerjemahan
tersedia dalam [catatan lokalisasi](LOKALISASI-INDONESIA.md).
Proyek ini independen dan tidak berafiliasi dengan Blizzard Entertainment.
