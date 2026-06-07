# 📱 Cooknote - Smart Pantry & AI Assistant

Aplikasi manajemen bahan makanan dan asisten koki pintar berbasis AI menggunakan Kotlin Multiplatform (KMP). **Ubah sisa bahan di dapurmu menjadi resep lezat dan kurangi limbah makanan (*zero-waste*).**

## 👥 Informasi Kelompok
**Program Studi Teknik Informatika - ITERA**

| Nama | NIM | Rencana Peran |
|------|-----|---------------|
| M. Hafizurrahman Akbar | 123140123 | Domain & Data Layer |
| Jordy Anugrah Akbar | 123140141 | Presentation Layer & UI |

> **📚 Dokumentasi Lengkap**
> 
> | Dokumen | Deskripsi |
> |---------|-----------|
> | [🚀 Cara Menjalankan](./docs/CARA_MENJALANKAN.md) | **BACA INI DULU!** Panduan setup dan running aplikasi |
> | [📋 Panduan Project](./docs/PANDUAN_PROJECT.md) | Informasi lengkap tentang project, timeline, dan penilaian |
> | [🌿 Git Workflow](./docs/GIT_WORKFLOW.md) | Cara menggunakan Git dan branching strategy |
> | [📜 Aturan Modifikasi](./docs/ATURAN_MODIFIKASI.md) | Apa yang boleh dan tidak boleh dimodifikasi |
> | [🏗️ Struktur Kode](./docs/STRUKTUR_KODE.md) | Penjelasan arsitektur dan struktur folder |
> | [🔧 Troubleshooting](./docs/TROUBLESHOOTING.md) | Solusi untuk masalah umum |

## ✨ Fitur Aplikasi

- 📝 **Pantry Inventory** - Tambah, edit, hapus, dan kelola bahan makanan yang tersedia di dapur.
- 🔍 **Smart Search & Filter** - Cari bahan makanan dan filter berdasarkan kategori bahan (Sayur, Daging, Bumbu, dll).
- 🤖 **AI Chef Assistant** - Generate resep masakan selangkah demi selangkah secara cerdas hanya dengan menggunakan bahan yang tersisa di *pantry*.
- 🌙 **Dark Mode** - Tema gelap/terang untuk kenyamanan penggunaan.
- 📱 **Cross-Platform** - Android & iOS dari satu codebase menggunakan KMP.

## 🏗️ Arsitektur & Teknologi

### Clean Architecture + MVVM

```text
┌─────────────────────────────────────────────────────────────┐
│                    PRESENTATION LAYER                        │
│  ┌───────────────┐        ┌───────────────┐                 │
│  │    Screen     │◄──────►│   ViewModel   │                 │
│  │  (Composable) │ State  │  (StateFlow)  │                 │
│  └───────────────┘        └───────┬───────┘                 │
└───────────────────────────────────┼─────────────────────────┘
                                    │
┌───────────────────────────────────┼─────────────────────────┐
│                      DOMAIN LAYER │                          │
│                    ┌──────────────▼──────────────┐          │
│                    │         Use Cases           │          │
│                    │    (Business Logic)         │          │
│                    └──────────────┬──────────────┘          │
│                    ┌──────────────▼──────────────┐          │
│                    │    Repository Interface     │          │
│                    └──────────────┬──────────────┘          │
└───────────────────────────────────┼─────────────────────────┘
                                    │
┌───────────────────────────────────┼─────────────────────────┐
│                       DATA LAYER  │                          │
│                    ┌──────────────▼──────────────┐          │
│                    │   Repository Implementation │          │
│                    └──────────────┬──────────────┘          │
│              ┌────────────────────┼────────────────────┐    │
│              │                    │                    │    │
│        ┌─────▼─────┐        ┌─────▼─────┐       ┌─────▼────┐│
│        │  SQLDelight│        │   Ktor   │       │ DataStore││
│        │  (Local)  │        │ (Remote) │       │  (Prefs) ││
│        └───────────┘        └──────────┘       └──────────┘│
└─────────────────────────────────────────────────────────────┘
```

### Tech Stack

| Layer | Technology |
|-------|------------|
| **UI** | Compose Multiplatform, Material 3 |
| **State** | StateFlow, ViewModel |
| **Navigation** | Compose Navigation (Type-safe) |
| **Networking** | Ktor Client |
| **Local DB** | SQLDelight |
| **Preferences** | DataStore |
| **DI** | Koin |
| **AI** | Google Gemini API |
| **Testing** | Kotlin Test, Turbine |

## 📁 Struktur Project

```text
composeApp/src/
├── commonMain/kotlin/com/example/noteai/      # Root package aplikasi
│   ├── core/                      # Core utilities & DI
│   ├── data/                      # Data layer (SQLDelight, Ktor, Repository Impl)
│   ├── domain/                    # Domain layer (Models, UseCases, Repository Interfaces)
│   └── presentation/              # Presentation layer (UI, Navigation, ViewModels)
├── commonMain/sqldelight/         # SQLDelight schema (.sq files)
├── androidMain/kotlin/            # Android-specific code
└── iosMain/kotlin/                # iOS-specific code
```

## 🚀 Getting Started

### Prerequisites

- Android Studio Ladybug (2024.2.1) atau lebih baru
- Xcode 15+ (untuk iOS)
- JDK 17+

### Setup

1. **Clone repository**
   ```bash
   git clone git@github.com:informatika-itera/Proyek-Pengembangan-Aplikasi-Mobile.git
   cd Proyek-Pengembangan-Aplikasi-Mobile
   ```

2. **Gunakan Branch Kelompok**
   ```bash
   git checkout project/123140123-123140141-Cooknote
   ```

3. **Setup `local.properties`**
   Salin template, lalu isi API key masing-masing anggota (jangan di-commit):
   ```bash
   cp local.properties.example local.properties
   # edit local.properties dan isi GEMINI_API_KEY=...
   ```
   *Dapatkan API key gratis di: https://aistudio.google.com/*

4. **Sync & Build**
   ```bash
   ./gradlew build                       # build semua target
   ./gradlew :composeApp:assembleDebug   # build APK debug saja
   ```

## 🧪 Testing Guide

Aplikasi ini dilengkapi dengan pengujian otomatis untuk menjamin stabilitas fitur.

### 1. Unit Testing (Tepat 15 Tests)
Menguji logika bisnis pada layer Repository dan ViewModel (Common Code).
- **Lokasi File:** `composeApp/src/commonTest/kotlin/com/example/noteai/`
- **Cara Menjalankan via Android Studio:** Klik kanan folder `commonTest/kotlin` -> Pilih **Run 'Tests in noteai'**.
- **Cara Menjalankan via Terminal:** `./gradlew :composeApp:testDebugUnitTest`

**Daftar Unit Tests:**
1. `insertNote` - Menambah catatan ke database lokal.
2. `searchNotes` - Pencarian catatan berdasarkan judul.
3. `deleteNote` - Penghapusan catatan.
4. `registerUser` - Alur pendaftaran akun pengguna.
5. `loginUser` - Verifikasi login dengan kredensial benar.
6. `logoutUser` - Penghapusan sesi pengguna.
7. `initialRecipesState` - Memastikan list resep awal kosong.
8. `saveRecipe` - Menyimpan resep baru ke database.
9. `filterFavoriteRecipes` - Filter resep favorit.
10. `initialPantryItems` - Memastikan pantry awal kosong.
11. `searchPantry` - Mencari bahan makanan di inventory.
12. `categoryFilterPantry` - Filter kategori bahan dapur.
13. `initialChatState` - Verifikasi pesan pembuka AI Chef.
14. `chatInputUpdate` - Perubahan state teks saat mengetik.
15. `chatSendMessage` - Alur kirim pesan dan pembersihan input.

### 2. UI Testing (5 Tests)
Menguji alur aplikasi secara visual pada Emulator/Device Android.
- **Lokasi File:** `composeApp/src/androidInstrumentedTest/kotlin/com/example/noteai/AppUiTest.kt`
- **Cara Menjalankan via Terminal:** `./gradlew :composeApp:connectedDebugAndroidTest`

**Daftar UI Tests:**
1. `testLoginFlow` - Uji input login dan tombol masuk.
2. `testNavigationBetweenTabs` - Uji navigasi antar menu utama.
3. `testAddPantryItemFlow` - Uji alur tambah bahan makanan baru.
4. `testRecipeClickNavigation` - Uji klik resep menuju detail.
5. `testProfileDisplay` - Uji tampilan nama & email user di profil.

## 📝 Tugas Mahasiswa (Sprint Plan)

### Sprint 1: Foundation
- [x] Clone dan setup project
- [x] Pahami struktur folder Clean Architecture
- [x] Modifikasi tema/warna Cooknote (Hijau/Oranye)
- [x] Update README identitas dan rancangan proyek

### Sprint 2: Core Features
- [x] Tambahkan domain model baru (`PantryItem` & `Recipe`)
- [x] Implementasi fitur CRUD bahan makanan
- [x] Implementasi local storage SQLite (SQLDelight) untuk bahan

### Sprint 3: Advanced Features
- [x] Implementasi search bahan makanan dengan debounce
- [x] Tambahkan filter kategori bahan (Sayur, Protein, Bumbu, dll)
- [x] Implementasi offline-first (menyimpan resep favorit lokal)
- [x] Sistem Login & Halaman Profil Terintegrasi

### Sprint 4: AI & Polish
- [x] Integrasikan fitur "Generate Resep dari Bahan" menggunakan Gemini API
- [x] UI polish (consistent design, dropdown category, detail resep)
- [x] Pengujian Otomatis (15 Unit Tests & 5 UI Tests)

### Sprint 5: Final
- [ ] Bug fixes
- [ ] Dokumentasi lengkap
- [ ] Prepare presentasi & demo

## 📄 License
MIT License - silakan gunakan untuk pembelajaran.

## 👨‍🏫 Dosen Pengampu
### Pak Habib
[GitHub: mh4Scripts](https://github.com/mh4Scripts)

**Program Studi Teknik Informatika** Institut Teknologi Sumatera (ITERA)
