SwapIn - Marketplace Jual Beli dan Tukar Barang Berbasis Poin

Gambaran Umum
SwapIn adalah sebuah marketplace digital yang memungkinkan pengguna untuk membeli, menjual, dan menukar barang menggunakan sistem poin sebagai pengganti mata uang konvensional. Proyek ini bertujuan untuk menciptakan sebuah platform yang ramah pengguna, dilengkapi dengan fitur gamifikasi, moderasi oleh admin, serta integrasi dengan layanan eksternal seperti API kurir dan data harga pasar.

Nama Proyek: Marketplace Jual Beli Barang dan Bisa Tukar Barang Berbasis Poin
Nama Aplikasi: SwapIn
Tanggal: 10 Juni 2025
Versi: 2.0


Table of Contents

Diagrams
Version 1 Diagrams
Use Case Diagram
Activity Diagram
Class Diagram
Sequence Diagram


Version 2 Diagrams
Use Case Diagram
Activity Diagram
Class Diagram
Sequence Diagram




Installation
Usage
Contributing
License


Diagrams
Version 1 Diagrams
Use Case Diagram V1
@startuml
actor User
actor Admin
actor Kurir
actor Sistem_Pembayaran

User --> (Login/Register)
User --> (Verifikasi Akun)
User --> (Upload Barang)
User --> (Tukar Barang dengan Poin)
User --> (Wishlist)
User --> (Review & Rating)
User --> (Melacak Pengiriman)

Admin --> (Moderasi Konten)
Admin --> (Verifikasi Barang)
Admin --> (Penilaian Poin)
Admin --> (Suspend Akun/Barang)
Admin --> (Kelola Pengguna)
Admin --> (Kelola Katalog Barang)

Kurir --> (Konfirmasi Pengambilan Barang)
Kurir --> (Proses Pengiriman)
Kurir --> (Update Status Pengiriman)

Sistem_Pembayaran --> (Konfirmasi Pembayaran)
Sistem_Pembayaran --> (Pengembalian Dana)
@enduml

Activity Diagram V1
@startuml
start
:Login/Register;
:Verifikasi Akun;
:Upload Barang;
:Menunggu Verifikasi Barang;
if (Barang Terverifikasi?) then (Ya)
  :Barang Tampil di Katalog;
  :Pilih Barang untuk Ditukar;
  if (Poin Cukup?) then (Ya)
    :Proses Pembayaran;
    :Notifikasi Kurir;
    :Proses Pengiriman;
    :Konfirmasi Penerimaan Barang;
    :Ulasan & Rating;
  else (Tidak)
    :Pengguna Harus Mengumpulkan Poin;
  endif
else (Tidak)
  :Diberi Catatan Penolakan;
endif
stop
@enduml

Class Diagram V1
@startuml
class User {
  - id: int
  - nama: string
  - email: string
  - poin: int
  - alamat: string
  + login()
  + uploadBarang()
  + tukarBarang()
}

class Barang {
  - id: int
  - nama: string
  - deskripsi: string
  - poin: int
  - status: string
}

class Transaksi {
  - id: int
  - tanggal: date
  - status: string
  - metodePembayaran: string
}

class Kurir {
  - id: int
  - nama: string
  - statusPengiriman: string
  + updateStatus()
}

class SistemPembayaran {
  + konfirmasiPembayaran()
  + pengembalianDana()
}

User "1" --> "0..*" Barang
User "1" --> "0..*" Transaksi
Barang "1" --> "0..*" Transaksi
User "1" --> "0..*" Kurir
Transaksi "1" --> "1" SistemPembayaran
@enduml

Sequence Diagram V1
@startuml
actor User
participant "Frontend" as FE
participant "Backend" as BE
participant "Database" as DB
participant "Admin" as ADM
participant "Kurir" as KUR
participant "Sistem Pembayaran" as SP

User -> FE : Upload Barang
FE -> BE : Kirim Data Barang
BE -> DB : Simpan Barang (status: pending)
BE -> ADM : Notifikasi Verifikasi Barang

ADM -> BE : Verifikasi & Tetapkan Poin
BE -> DB : Update Barang (status: terverifikasi)
User -> FE : Tukar Barang
FE -> BE : Validasi Poin
BE -> SP : Konfirmasi Pembayaran
SP -> BE : Pembayaran Berhasil
BE -> DB : Simpan Transaksi
BE -> KUR : Notifikasi Pengiriman
KUR -> User : Konfirmasi Pengiriman
User -> KUR : Terima Barang
User -> FE : Berikan Rating
@enduml

Version 2 Diagrams
Use Case Diagram V2
@startuml
actor User
actor Admin
actor "Courier Service" as Courier
actor "AI System" as AI

User --> (Login/Register)
User --> (Verifikasi Akun)
User --> (Upload Barang)
User --> (Tukar Barang dengan Poin)
User --> (Jual Barang dengan Poin)
User --> (Wishlist)
User --> (Review & Rating)
User --> (Pencarian Barang)
User --> (Ajukan Negosiasi Poin)
User --> (Lihat Riwayat Transaksi)
User --> (Lihat Profil & Poin)
User --> (Ikut Misi Mingguan)
User --> (Lihat Badge & Level)
User --> (Gunakan Chatbot Bantuan)

Admin --> (Moderasi Konten)
Admin --> (Verifikasi Barang)
Admin --> (Penilaian Poin)
Admin --> (Suspend Akun/Barang)
Admin --> (Kelola Kategori)
Admin --> (Monitor Transaksi)
Admin --> (Kelola Promo)
Admin --> (Analisis Laporan)

Courier --> (Lacak Pengiriman)

AI --> (Analisis Barang)
AI --> (Rekomendasi Barang)
AI --> (Deteksi Konten Tidak Pantas)

(Upload Barang) .> (Analisis Barang) : <<include>>
(Tukar Barang dengan Poin) .> (Lacak Pengiriman) : <<include>>
(Pencarian Barang) .> (Rekomendasi Barang) : <<include>>
(Moderasi Konten) .> (Deteksi Konten Tidak Pantas) : <<include>>

note right of (Login/Register)
  F1.1: Mendukung email/no HP, OAuth
end note

note right of (Verifikasi Akun)
  F1.2: Verifikasi KTP/selfie wajib
end note

note right of (Upload Barang)
  F2.1: Foto, deskripsi, kategori wajib
end note

note right of (Tukar Barang dengan Poin)
  F3.1: Transaksi satu arah, poin dikurangi
end note

note right of (Ikut Misi Mingguan)
  F5.1: Gamifikasi untuk engagement
end note

note right of (Analisis Barang)
  F2.2: AI menilai poin berdasarkan pasar
end note

note left of Courier
  F3.2: Integrasi API kurir (JNE, SiCepat)
end note
@enduml

Activity Diagram V2
@startuml
start

:Login/Register;
note right: F1.1 - Email/no HP, validasi OAuth

if (Pengguna Baru?) then (Ya)
  :Verifikasi Akun;
  note right: F1.2 - Upload KTP/selfie
else (Tidak)
endif

:Dashboard Pengguna;
note right: Menampilkan poin, badge, rekomendasi

fork
  :Upload Barang;
  note right: F2.1 - Foto, deskripsi, kategori
  :Analisis AI;
  note right: F2.2 - Nilai poin awal
  :Menunggu Verifikasi Admin;
  if (Barang Terverifikasi?) then (Ya)
    :Barang Tampil di Katalog;
    note right: Status: tersedia
  else (Tidak)
    :Diberi Catatan Penolakan;
    :Revisi Barang;
    note right: Pengguna revisi atau batal
    if (Revisi?) then (Ya)
      :Kembali ke Upload;
    else (Tidak)
      stop
    endif
  endif
fork again
  :Pencarian Barang;
  note right: F6.1 - Filter kategori, harga
  :Lihat Rekomendasi AI;
  :Ajukan Negosiasi Poin;
  note right: F2.3 - Usulan poin baru
  if (Negosiasi Diterima?) then (Ya)
    :Tukar Barang;
    note right: F3.1 - Poin dikurangi
    :Integrasi Kurir;
    note right: F3.2 - API pelacakan
    :Proses Pengiriman;
    if (Barang Diterima?) then (Ya)
      :Ulasan & Rating;
      note right: F4.1 - Review pengguna
      :Dapatkan Poin Bonus;
      note right: F5.1 - Gamifikasi
    else (Tidak)
      :Ajukan Komplain;
    endif
  else (Tidak)
    :Kembali ke Katalog;
  endif
fork again
  :Ikut Misi Mingguan;
  note right: F5.1 - Tugas untuk badge
  :Dapatkan Badge;
end fork

stop
@enduml

Class Diagram V2
@startuml
class User {
  - id: int
  - nama: string
  - email: string
  - no_hp: string
  - password: string
  - ktp_url: string
  - selfie_url: string
  - poin: int
  - rating: float
  - role: enum {user, admin}
  - level: int
  + login()
  + register()
  + uploadBarang()
  + tukarBarang()
  + tambahWishlist()
  + beriReview()
  + ajukanNegosiasi()
  + ikutMisi()
}

class Barang {
  - id: int
  - nama: string
  - deskripsi: string
  - gambar: string[]
  - kategori: string
  - kondisi: enum {baru, bekas}
  - status: enum {pending, terverifikasi, ditolak}
  - poin: int
  - id_user: int
  + tambahPromo()
}

class Transaksi {
  - id: int
  - id_barang: int
  - id_pembeli: int
  - id_penjual: int
  - tanggal: date
  - status: enum {pending, dikirim, selesai}
  - review: string
  - rating: float
  - tracking_number: string
}

class Wishlist {
  - id: int
  - id_user: int
  - id_barang: int
  - tanggal_ditambahkan: date
}

class VerifikasiBarang {
  - id: int
  - id_barang: int
  - status: enum {pending, approved, rejected}
  - catatan: string
  - oleh: enum {admin, AI}
  - tanggal: date
}

class Badge {
  - id: int
  - id_user: int
  - nama: string
  - deskripsi: string
  - tanggal_diberikan: date
}

class Misi {
  - id: int
  - nama: string
  - deskripsi: string
  - poin_reward: int
  - status: enum {aktif, selesai}
}

class Kategori {
  - id: int
  - nama: string
  - deskripsi: string
}

class Promo {
  - id: int
  - id_barang: int
  - diskon_poin: float
  - start_date: date
  - end_date: date
}

User "1" --> "0..*" Barang : uploads
User "1" --> "0..*" Transaksi : initiates
User "1" --> "0..*" Transaksi : sells
User "1" --> "0..*" Wishlist : creates
User "1" --> "0..*" Badge : earns
User "1" --> "0..*" Misi : participates
Barang "1" --> "0..*" Transaksi : involved in
Barang "1" --> "0..*" VerifikasiBarang : verified by
Barang "1" --> "1" Kategori : belongs to
Barang "0..*" --> "0..1" Promo : has
Wishlist --> "1" Barang : references
Misi "0..*" --> "1" : awards Badge

note right of User
  Mendukung role-based access
  Gamifikasi dengan level
end note

note right of Barang
  Mendukung gambar multiple
  Status enum untuk workflow
end note

note right of Transaksi
  Mendukung tracking number
  untuk integrasi kurir
end note

note right of Misi
  F5.1: Gamifikasi dengan
  misi mingguan
end note
@enduml

Sequence Diagram V2
@startuml
actor User
participant "Frontend" as FE
participant "Backend" as BE
participant "Database" as DB
participant "Admin" as Admin
participant "AI System" as AI
participant "Courier API" as Courier
participant "Market API" as MarketApi

== Autentifikasi ==
User -> FE: Login/Register (email, password)
FE -> BE: Kirim Kredensial
BE -> DB: Validasi User
DB --> BE: Data Pengguna
BE --> FE: JWT Token
FE --> User: Dashboard

== Upload Barang ==
User -> FE: Upload Barang (foto, deskripsi, kategori)
FE -> BE: Kirim Data Barang
BE -> DB: Simpan Barang (status: pending)
DB --> BE: ID Barang
BE -> AI: Analisis Barang (foto, kategori)
AI -> MarketApi: Ambil Harga Pasar
MarketApi --> AI: Data Harga (Tokopedia, OLX)
AI --> BE: Poin Awal
BE -> Admin: Notifikasi Verifikasi
Admin -> BE: Setujui/Tolak, Tetapkan Poin
BE -> DB: Update Barang (status: terverifikasi, poin)
DB --> BE: Berhasil
BE --> FE: Barang di Katalog
FE --> User: Notifikasi

== Negosiasi Poin ==
User -> FE: Ajukan Negosiasi (id_barang, poin_usulan)
FE -> BE: Kirim Usulan
BE -> Admin: Notifikasi Negosiasi
Admin -> BE: Setuju/Tolak
BE -> DB: Update Poin Barang
DB --> BE: Berhasil
BE --> FE: Hasil Negosiasi
FE --> User: Notifikasi

== Tukar Barang ==
User -> FE: Tukar Barang (id_barang, id_pembeli)
FE -> BE: Proses Transaksi
BE -> DB: Validasi Poin Pengguna
DB --> BE: Poin Cukup
BE -> DB: Simpan Transaksi (status: pending)
DB --> BE: ID Transaksi
BE -> Courier: Buat Pengiriman
Courier --> BE: Nomor Tracking
BE -> DB: Update Transaksi (tracking_number)
DB --> BE: Berhasil
BE --> FE: Konfirmasi Transaksi
FE --> User: Notifikasi

== Pelacakan Pengiriman ==
User -> FE: Lacak Pengiriman
FE -> BE: Minta Status (id_transaksi)
BE -> Courier: Cek Status (tracking_number)
Courier --> BE: Status Pengiriman
BE -> DB: Update Status Transaksi
DB --> BE: Berhasil
BE --> FE: Informasi Pengiriman
FE --> User: Status

== Review & Gamifikasi ==
User -> FE: Beri Review & Rating (id_transaksi, review, rating)
FE -> BE: Kirim Review
BE -> DB: Simpan Review & Rating
DB --> BE: Berhasil
BE -> DB: Cek Kriteria Misi
DB --> BE: Misi Selesai
BE -> DB: Tambah Poin/Badge
DB --> BE: Berhasil
BE --> FE: Notifikasi Reward
FE --> User: Badge/Poin Baru

note right
  Integrasi: API Kurir, Harga Pasar
  Gamifikasi: Poin bonus, badge
end note
@enduml
