# Coffee Bliss - Membership Card App

Aplikasi Android modern untuk sistem kartu member digital Coffee Bliss.

---

## Fitur Aplikasi

| Fitur | Deskripsi |
|-------|-----------|
| 🔐 Registrasi Member | Daftar dengan Nama, Email, No. HP |
| 🔑 Login | Masuk menggunakan email |
| 💳 Kartu Member Digital | QR Code, Nomor Member, Status |
| 📊 Riwayat Transaksi | Daftar pembelian & poin didapat |
| ➕ Tambah Transaksi | Input nominal, kalkulasi poin otomatis |
| 🎁 Tukar Reward | Redeem poin dengan hadiah coffee |
| 👤 Profil Member | Info akun & tingkatan member |

---

## Arsitektur & Teknologi

```
Tech Stack:
├── Language       : Kotlin
├── UI             : Jetpack Compose + Material 3
├── Database       : Room Database
├── Architecture   : MVVM (ViewModel + Repository Pattern)
├── Navigation     : Navigation Compose
├── QR Code        : ZXing (Google)
└── Min SDK        : API 26 (Android 8.0)
```

### Struktur Package

```
com.coffeebliss/
├── data/
│   ├── dao/           ← MemberDao, TransactionDao, RedemptionDao
│   ├── database/      ← CoffeeBlissDatabase (Room)
│   ├── entity/        ← Member, Transaction, Redemption
│   └── repository/    ← CoffeeBlissRepository
├── navigation/
│   ├── Screen.kt      ← Route definitions
│   └── NavGraph.kt    ← Navigation graph
├── ui/
│   ├── screens/       ← Semua Composable Screen
│   └── theme/         ← Color, Type, Theme
└── MainActivity.kt
```

---

## Database Design 

### Tabel `members`
| Kolom | Tipe | Keterangan |
|-------|------|------------|
| id | TEXT (PK) | UUID unik |
| name | TEXT | Nama member |
| email | TEXT | Email (unique) |
| phone | TEXT | No. Handphone |
| memberNumber | TEXT | Nomor member (CB + timestamp) |
| totalPoints | INTEGER | Total poin terkumpul |
| memberStatus | TEXT | Regular / Silver / Gold |
| registrationDate | INTEGER | Timestamp pendaftaran |

### Tabel `transactions`
| Kolom | Tipe | Keterangan |
|-------|------|------------|
| id | TEXT (PK) | UUID unik |
| memberId | TEXT (FK) | Referensi ke members.id |
| amount | INTEGER | Nominal pembelian (Rp) |
| pointsEarned | INTEGER | Poin yang didapat |
| date | INTEGER | Timestamp transaksi |
| description | TEXT | Keterangan transaksi |

### Tabel `redemptions`
| Kolom | Tipe | Keterangan |
|-------|------|------------|
| id | TEXT (PK) | UUID unik |
| memberId | TEXT (FK) | Referensi ke members.id |
| rewardName | TEXT | Nama reward ditukar |
| pointsUsed | INTEGER | Poin yang digunakan |
| date | INTEGER | Timestamp penukaran |

---

## 📐 Aturan Bisnis

### Kalkulasi Poin
```
Poin = Nominal Pembelian ÷ 10.000
Contoh: Rp150.000 ÷ Rp10.000 = 15 poin
```

### Reward Catalog
| Poin | Reward |
|------|--------|
| 50   | ☕ Espresso |
| 100  | 🥤 Cappuccino |
| 150  | 🧋 Latte Gratis |

### Tingkatan Member
| Status | Syarat |
|--------|--------|
| Regular | 0 – 199 poin |
| Silver | 200 – 499 poin |
| Gold | 500+ poin |

---

## User Flow

```
[Splash] → [Login / Register] → [Home Dashboard]
                                       │
                    ┌──────────────────┼──────────────────┐
                    ▼                  ▼                   ▼
            [Kartu Member]      [Transaksi]          [Reward]
            - QR Code           - Riwayat            - Daftar reward
            - Info member       - Tambah baru        - Tukar poin
                                - Poin otomatis      - Riwayat tukar
```

---

## Cara Menjalankan
- Android Studio Ladybug (2024.2.1) atau lebih baru
- JDK 11+
- Android SDK API 35
- Emulator / Device API 26+



