## **Spesifikasi Kebutuhan Perangkat Lunak (SKPL)**

**Nama Sistem:** SwapIn - Marketplace Tukar & Jual Barang Berbasis Poin
**Versi:** 2.0
**Tanggal:** 10 Juni 2025
**Disusun oleh:** PIKIRIN AJA (Brian - Norman - Chandra)

---

### **1. Pendahuluan**

#### **1.1 Tujuan Dokumen**

Dokumen ini menjabarkan spesifikasi kebutuhan fungsional dan non-fungsional dari sistem web marketplace bernama SwapIn. SwapIn memungkinkan pengguna untuk menukar atau menjual barang melalui sistem poin tanpa menggunakan uang secara langsung.

#### **1.2 Ruang Lingkup Sistem**

SwapIn adalah platform barter digital yang berfungsi seperti marketplace, namun dengan metode pertukaran barang berbasis poin. Fitur utama:

* Upload barang & penilaian poin otomatis/manual
* Tukar barang satu arah menggunakan poin
* Jual barang dengan poin atau uang (opsional)
* Sistem rating, review, verifikasi, dan pengiriman

#### **1.3 Definisi, Akronim, dan Singkatan**

* **Poin:** Nilai tukar virtual untuk mewakili harga barang.
* **User:** Pengguna sistem SwapIn.
* **Admin:** Pengelola dan moderator sistem.
* **AI:** Sistem kecerdasan buatan yang membantu verifikasi dan penilaian barang.

---

### **2. Deskripsi Umum**

#### **2.1 Perspektif Produk**

SwapIn adalah aplikasi web responsif berbasis PHP (atau Node.js) dan MySQL. Platform ini dapat diperluas menjadi aplikasi mobile.

#### **2.2 Fungsi Produk**

* Autentikasi & verifikasi pengguna
* Unggah barang dan penilaian poin
* Tukar barang dengan poin
* Fitur wishlist & pencarian
* Dashboard admin dan AI verifikasi
* Integrasi kurir dan pelacakan
* Sistem rating dan review
* Gamifikasi untuk meningkatkan partisipasi

#### **2.3 Karakteristik Pengguna**

* Pengguna awam dari berbagai kalangan
* Pengguna gaptek (UI/UX ramah pengguna)
* Admin dan moderator

#### **2.4 Batasan Sistem**

* Sistem barter satu arah (berbasis poin)
* Barang yang ditukar tidak dapat dikembalikan
* Tidak semua barang dapat diterima (tergantung hasil verifikasi)

---

### **3. Kebutuhan Fungsional**

#### **3.1 Autentikasi & Verifikasi**

* **F1.1** Daftar dan login menggunakan email/nomor HP
* **F1.2** Verifikasi email/KTP/selfie
* **F1.3** Admin dapat login dan mengelola sistem

#### **3.2 Manajemen Barang & Poin**

* **F2.1** Upload barang dengan foto & deskripsi
* **F2.2** Sistem memberi nilai poin secara otomatis/manual
* **F2.3** Fitur ajukan negosiasi poin
* **F2.4** Barang dapat ditukar, dijual, atau ditandai promo

#### **3.3 Sistem Tukar & Transaksi**

* **F3.1** Tukar barang dengan poin (satu arah)
* **F3.2** Sistem tracking pengiriman
* **F3.3** Riwayat transaksi tercatat dan dapat dilihat pengguna

#### **3.4 Review & Moderasi**

* **F4.1** Sistem rating dan ulasan antar pengguna
* **F4.2** Admin dapat suspend akun/barang yang mencurigakan

#### **3.5 Gamifikasi**

* **F5.1** Pengguna mendapat badge, level, dan misi mingguan
* **F5.2** Notifikasi & reward untuk aktivitas aktif

#### **3.6 Fitur Tambahan**

* **F6.1** Wishlist dan rekomendasi otomatis
* **F6.2** Fitur bantu (chatbot, FAQ, panduan)

---

### **4. Kebutuhan Non-Fungsional**

#### **4.1 Kinerja**

* Respon sistem maksimal 2 detik per interaksi pengguna
* Skalabel untuk 10.000 pengguna aktif

#### **4.2 Keamanan**

* Enkripsi password (bcrypt)
* Validasi input, proteksi XSS dan SQL Injection
* Audit log aktivitas pengguna

#### **4.3 Ketersediaan & Kompatibilitas**

* Uptime sistem > 99%
* Kompatibel dengan browser modern & perangkat mobile

#### **4.4 Dukungan Eksternal**

* Integrasi kurir & API tracking
* Data harga pasar dari marketplace lain (Tokopedia, OLX)

---

### **5. Antarmuka Pengguna**

#### **5.1 Halaman Utama**

* Barang terbaru, promosi, dan kategori

#### **5.2 Halaman Detail Barang**

* Deskripsi, poin, kondisi, pemilik, wishlist, tombol tukar/beli

#### **5.3 Halaman Profil**

* Barang user, histori tukar, wishlist, saldo poin, rating akun

#### **5.4 Halaman Admin**

* Tabel user, barang, verifikasi, dan kontrol moderasi

---

### **6. Diagram Use Case (Ringkas)**

```
[User] --> (Login/Register)
[User] --> (Verifikasi Akun)
[User] --> (Upload Barang)
[User] --> (Tukar Barang dengan Poin)
[User] --> (Wishlist/Review Barang)
[Admin] --> (Verifikasi & Moderasi)
[Admin] --> (Penilaian Poin)
```

---

### **7. Diagram ERD (Entity Relationship Diagram)**

**Users**

* id (PK), nama, email, password, no\_hp, ktp\_url, selfie\_url, role, poin, rating

**Barang**

* id (PK), nama, deskripsi, gambar, kategori, kondisi, status, id\_user (FK), poin

**Transaksi**

* id (PK), id\_barang, id\_pembeli, status, tanggal, review, rating

**Wishlist**

* id (PK), id\_user, id\_barang

**VerifikasiBarang**

* id (PK), id\_barang, status, catatan, oleh (admin/AI)

**Badge / Misi** (opsional)

---

### **8. Rencana Pengujian**

| Modul         | Skenario                      | Hasil Diharapkan                            |
| ------------- | ----------------------------- | ------------------------------------------- |
| Login         | Login dengan email valid      | Redirect ke halaman utama                   |
| Upload Barang | Isi semua data & gambar valid | Barang muncul di katalog dengan poin awal   |
| Tukar Barang  | Tukar barang senilai poin     | Transaksi tercatat dan barang dikirim       |
| Rating        | User memberi ulasan           | Review tampil di profil barang dan pengguna |
| Verifikasi    | Barang dicek admin/AI         | Status berubah menjadi "Terverifikasi"      |

---

### **9. Lampiran**

* Mockup UI (jika tersedia)
* Referensi database harga barang (OLX, Tokopedia)
* Panduan pengguna untuk pengguna baru
