# Detail Halaman UI/UX Aplikasi Pemesanan Lapangan Olahraga (Mobile)

## I. Alur Pengguna Pemain (Player Flow)

### UI-P01: Halaman Splash Screen
*   **Tujuan:** Tampilan awal saat aplikasi dibuka.
*   **Elemen Utama:**
    *   Logo Aplikasi
    *   (Opsional) Animasi singkat loading/branding
*   **Aksi Utama:** Otomatis mengarah ke Halaman Onboarding (UI-P02) atau Halaman Login (UI-P04).

### UI-P02: Halaman Onboarding (Opsional)
*   **Tujuan:** Memperkenalkan fitur utama aplikasi kepada pengguna baru.
*   **Elemen Utama:**
    *   Beberapa slide (2-3) dengan ilustrasi/gambar dan teks singkat per fitur.
    *   Indikator slide (dots).
    *   Tombol "Lewati".
    *   Tombol "Selanjutnya" / "Mulai".
*   **Aksi Utama:** Mengarah ke Halaman Registrasi (UI-P03) atau Halaman Login (UI-P04).

### UI-P03: Halaman Registrasi
*   **Tujuan:** Memungkinkan pengguna baru membuat akun.
*   **Elemen Utama:**
    *   Judul Halaman (cth: "Daftar Akun Baru").
    *   Input Field: Nama Lengkap (Wajib).
    *   Input Field: Alamat Email (Wajib, validasi format email).
    *   Input Field: Kata Sandi (Wajib, dengan opsi lihat/sembunyikan).
    *   Input Field: Konfirmasi Kata Sandi (Wajib, validasi kesamaan dengan kata sandi).
    *   Checkbox/Link: Persetujuan Syarat & Ketentuan dan Kebijakan Privasi (Wajib dicentang/dikunjungi).
    *   Tombol Utama: "Daftar".
    *   Link Navigasi: "Sudah punya akun? Login di sini".
*   **Aksi Utama:** Validasi input, kirim data registrasi ke backend, navigasi ke Halaman Login (UI-P04) atau Home (UI-P05) setelah sukses, tampilkan pesan error jika gagal.

### UI-P04: Halaman Login
*   **Tujuan:** Memungkinkan pengguna terdaftar masuk ke akun mereka.
*   **Elemen Utama:**
    *   Judul Halaman (cth: "Login ke Akun Anda").
    *   Logo Aplikasi (Opsional).
    *   Input Field: Alamat Email (Wajib).
    *   Input Field: Kata Sandi (Wajib, dengan opsi lihat/sembunyikan).
    *   Link: "Lupa Kata Sandi?" (Fitur tunda setelah MVP).
    *   Tombol Utama: "Login".
    *   Link Navigasi: "Belum punya akun? Daftar di sini".
    *   (Opsional) Tombol Login dengan Google/Facebook (Fitur tunda setelah MVP).
*   **Aksi Utama:** Validasi input, kirim data login ke backend, navigasi ke Halaman Home Pemain (UI-P05) atau Dasbor Admin SC (UI-A01) sesuai peran setelah sukses, tampilkan pesan error jika gagal.

### UI-P05: Halaman Home/Beranda Pemain
*   **Tujuan:** Titik awal setelah login pemain, menampilkan pencarian.
*   **Elemen Utama:**
    *   Header: Salam (cth: "Hai, [Nama Pengguna]!"), (Opsional) Ikon Notifikasi, (Opsional) Ikon Profil.
    *   Form Pencarian Utama:
        *   Input Field / Dropdown: Pilih Jenis Olahraga.
        *   Input Field: Masukkan Kota atau Lokasi.
        *   Tombol: "Cari Lapangan".
    *   (Opsional untuk MVP Awal):
        *   Banner Promosi (carousel).
        *   Daftar Sports Center Terdekat/Populer (berdasarkan data dummy/logika sederhana).
    *   Bottom Navigation Bar (Navigasi Utama Aplikasi):
        *   Icon & Label: Beranda (Aktif).
        *   Icon & Label: Riwayat.
        *   Icon & Label: Akun.
*   **Aksi Utama:** Input kriteria pencarian, navigasi ke Halaman Hasil Pencarian (UI-P06).

### UI-P06: Halaman Hasil Pencarian Sports Center
*   **Tujuan:** Menampilkan daftar Sports Center (SC) yang sesuai kriteria.
*   **Elemen Utama:**
    *   Header: Judul (cth: "Hasil Pencarian: [Kriteria]") atau "Sports Center Ditemukan". Tombol "Kembali". (Opsional) Tombol Filter Lanjutan.
    *   Daftar SC (Scrollable List):
        *   Setiap item (Card): Foto Utama SC, Nama SC, Alamat Singkat, (Opsional) Jenis Olahraga Utama, (Opsional) Rating Bintang.
    *   Pesan jika tidak ada hasil: "Oops! Tidak ada Sports Center yang cocok dengan pencarianmu."
    *   (Opsional) Tombol untuk beralih ke Tampilan Peta (Fitur tunda).
*   **Aksi Utama:** Scroll daftar, tap pada item SC untuk navigasi ke Halaman Detail Sports Center (UI-P07).

### UI-P07: Halaman Detail Sports Center
*   **Tujuan:** Menampilkan informasi lengkap tentang SC dan daftar lapangannya.
*   **Elemen Utama:**
    *   Header: Nama Sports Center. Tombol "Kembali". (Opsional) Tombol Favorit/Bookmark.
    *   Galeri Foto SC (Image Carousel/Slider).
    *   Nama SC.
    *   Alamat Lengkap.
    *   (Opsional) Tombol "Lihat di Peta" (Membuka aplikasi peta eksternal).
    *   Nomor Telepon (dengan opsi tap-to-call).
    *   Jam Operasional.
    *   Deskripsi SC.
    *   Daftar Fasilitas (dengan ikon, cth: Parkir, Toilet, Wifi).
    *   (Opsional) Ulasan & Rating Pengguna (Fitur tunda).
    *   Judul Bagian: "Pilihan Lapangan".
    *   Daftar Lapangan Milik SC (Scrollable List Horizontal/Vertikal):
        *   Setiap item (Card): Foto Lapangan, Nama Lapangan, Jenis Olahraga, Harga per Jam.
*   **Aksi Utama:** Tap pada item lapangan untuk navigasi ke Halaman Detail Lapangan (UI-P08).

### UI-P08: Halaman Detail Lapangan
*   **Tujuan:** Menampilkan info lapangan dan jadwal ketersediaan.
*   **Elemen Utama:**
    *   Header: Nama Lapangan. Tombol "Kembali".
    *   Galeri Foto Lapangan (Image Carousel/Slider).
    *   Nama Lapangan.
    *   Jenis Olahraga.
    *   (Opsional) Tipe Lapangan (Indoor/Outdoor).
    *   (Opsional) Jenis Lantai.
    *   Harga per Jam/Sesi.
    *   Deskripsi Lapangan.
    *   Pemilihan Tanggal: Kalender interaktif atau Date Picker input.
    *   Jadwal Ketersediaan Slot Waktu (untuk tanggal terpilih):
        *   Grid/List slot waktu (cth: 08:00-09:00, 09:00-10:00).
        *   Indikator visual status per slot: Tersedia (clickable), Sudah Dipesan (disabled), Diblokir Admin (disabled).
*   **Aksi Utama:** Pilih tanggal, tap pada slot waktu yang "Tersedia" untuk memulai proses booking (navigasi ke UI-P09).

### UI-P09: Halaman Konfirmasi Pemesanan
*   **Tujuan:** Ringkasan pemesanan sebelum finalisasi.
*   **Elemen Utama:**
    *   Header: "Konfirmasi Pemesanan". Tombol "Kembali".
    *   Detail Pemesanan:
        *   Nama Sports Center.
        *   Nama Lapangan.
        *   Tanggal Terpilih.
        *   Jam Mulai & Jam Selesai Terpilih.
        *   Durasi Sewa.
    *   Rincian Biaya:
        *   Harga per Jam x Durasi.
        *   (Opsional) Biaya Layanan.
        *   Total Pembayaran.
    *   (Untuk MVP dengan opsi pembayaran di tempat/transfer manual):
        *   Pilihan Metode Pembayaran (jika ada >1, misal: "Bayar di Tempat", "Transfer Bank").
        *   (Jika "Transfer Bank" dipilih) Informasi: No. Rekening SC, Nama Bank, Nama Pemilik Rekening, Batas Waktu Transfer.
    *   Tombol Utama: "Pesan Sekarang" / "Lanjutkan ke Pembayaran".
*   **Aksi Utama:** Tap tombol utama untuk memproses booking, navigasi ke Halaman Status Pemesanan (UI-P10).

### UI-P10: Halaman Status Pemesanan/Pembayaran
*   **Tujuan:** Konfirmasi booking atau instruksi pembayaran.
*   **Elemen Utama (Contoh jika booking berhasil dengan "Bayar di Tempat"):**
    *   Ikon Sukses (centang hijau).
    *   Judul: "Pemesanan Berhasil!"
    *   Informasi: Booking ID.
    *   Ringkasan singkat: Lapangan, Tanggal, Jam.
    *   Pesan: "Pembayaran dilakukan di lokasi. Mohon datang tepat waktu."
    *   Tombol: "Lihat Riwayat Pemesanan", Tombol "Kembali ke Beranda".
*   **Elemen Utama (Contoh jika "Transfer Bank" dan menunggu pembayaran):**
    *   Judul: "Selesaikan Pembayaran Anda".
    *   Informasi: Booking ID.
    *   Jumlah yang harus dibayar.
    *   Detail Rekening Tujuan SC.
    *   Instruksi transfer (misal: sertakan Booking ID di berita transfer).
    *   Batas waktu pembayaran.
    *   (Opsional untuk MVP Awal) Tombol/Input: Upload Bukti Pembayaran.
    *   Tombol: "Saya Sudah Transfer" (jika tanpa upload) atau "Konfirmasi Pembayaran".
    *   Tombol: "Kembali ke Beranda".
*   **Aksi Utama:** Navigasi sesuai tombol yang tersedia.

### UI-P11: Halaman Riwayat Pemesanan
*   **Tujuan:** Menampilkan daftar semua pemesanan pemain.
*   **Elemen Utama:**
    *   Header: "Riwayat Pemesanan".
    *   (Opsional) Tabs/Filter: Semua, Menunggu Pembayaran, Terkonfirmasi, Selesai, Dibatalkan.
    *   Daftar Pemesanan (Scrollable List):
        *   Setiap item (Card): Nama Lapangan & SC, Tanggal & Jam, Status Pemesanan (dengan warna/ikon berbeda), Total Harga.
*   **Aksi Utama:** Tap pada item riwayat untuk navigasi ke Halaman Detail Riwayat Pemesanan (UI-P12).

### UI-P12: Halaman Detail Riwayat Pemesanan
*   **Tujuan:** Menampilkan detail lengkap satu pemesanan dari riwayat.
*   **Elemen Utama:**
    *   Header: "Detail Pemesanan". Tombol "Kembali".
    *   Booking ID.
    *   Status Pemesanan yang jelas.
    *   Semua detail pemesanan seperti di UI-P09 (Lapangan, SC, Tanggal, Jam, Durasi, Rincian Biaya).
    *   (Jika ada) Informasi Pembayaran (Metode, status, bukti transfer jika ada).
    *   (Opsional, tergantung status & kebijakan): Tombol "Batalkan Pemesanan".
    *   (Opsional) Tombol "Hubungi Sports Center".
    *   (Opsional, jika sudah selesai) Tombol "Beri Ulasan" (Fitur tunda).
*   **Aksi Utama:** Sesuai tombol yang tersedia.

### UI-P13: Halaman Profil/Akun Pemain
*   **Tujuan:** Melihat dan mengelola informasi akun pemain.
*   **Elemen Utama:**
    *   (Opsional) Foto Profil Pengguna.
    *   Nama Pengguna.
    *   Alamat Email Pengguna.
    *   Daftar Menu (List Tiles):
        *   Edit Profil.
        *   Ubah Kata Sandi (Fitur tunda).
        *   Notifikasi (Pengaturan - Fitur tunda).
        *   Bantuan / FAQ.
        *   Tentang Aplikasi.
        *   Logout.
*   **Aksi Utama:** Navigasi ke halaman terkait (Edit Profil, dll.), proses Logout.

### UI-P14: Halaman Edit Profil Pemain
*   **Tujuan:** Mengubah data profil pemain.
*   **Elemen Utama:**
    *   Header: "Edit Profil". Tombol "Kembali".
    *   (Opsional) Tampilan Foto Profil dengan opsi ganti foto.
    *   Input Field: Nama Lengkap (terisi data saat ini).
    *   Input Field: Nomor Telepon (opsional, terisi data saat ini).
    *   Tombol Utama: "Simpan Perubahan".
*   **Aksi Utama:** Validasi input, simpan perubahan ke backend.

---

## II. Alur Pengguna Admin Sports Center (SC Admin Flow)

*(Admin SC login menggunakan Halaman Login UI-P04, kemudian diarahkan ke dasbor berbeda)*

### UI-A01: Halaman Dasbor Admin SC
*   **Tujuan:** Tampilan utama Admin SC, ringkasan dan navigasi manajemen.
*   **Elemen Utama:**
    *   Header: Nama Sports Center yang dikelola. (Opsional) Ikon Notifikasi, Ikon Profil Admin.
    *   (Opsional) Kartu Ringkasan: Jumlah Booking Hari Ini, Pendapatan Hari Ini, Okupansi Lapangan.
    *   Grid/List Menu Navigasi Utama:
        *   Manajemen Lapangan.
        *   Jadwal & Ketersediaan (Kalender).
        *   Daftar Pemesanan.
        *   Profil Sports Center (Edit Info SC).
    *   (Opsional) Bottom Navigation Bar: Dasbor (Aktif), Pemesanan, Lapangan, Profil SC/Akun.
*   **Aksi Utama:** Navigasi ke halaman manajemen terkait.

### UI-A02: Halaman Manajemen Lapangan
*   **Tujuan:** Daftar lapangan SC dan CRUD.
*   **Elemen Utama:**
    *   Header: "Manajemen Lapangan".
    *   Tombol Aksi Utama (FAB atau di header): "Tambah Lapangan Baru" (+ ikon).
    *   Daftar Lapangan (Scrollable List):
        *   Setiap item (Card): Nama Lapangan, Jenis Olahraga, Harga per Jam, Status (Aktif/Tidak Aktif).
        *   Menu Aksi per item (ikon titik tiga atau swipe): Edit, Hapus/Nonaktifkan.
*   **Aksi Utama:** Navigasi ke Halaman Tambah/Edit Lapangan (UI-A03), memicu aksi edit/hapus.

### UI-A03: Halaman Tambah/Edit Lapangan
*   **Tujuan:** Form untuk menambah atau mengedit detail lapangan.
*   **Elemen Utama (Form):**
    *   Header: "Tambah Lapangan Baru" atau "Edit Lapangan: [Nama Lapangan]". Tombol "Kembali".
    *   Input Field: Nama Lapangan (Wajib).
    *   Dropdown/Pilihan: Jenis Olahraga (Wajib).
    *   Input Field (Numeric): Harga per Jam (Wajib).
    *   (Opsional) Dropdown/Pilihan: Tipe Lapangan (Indoor/Outdoor).
    *   (Opsional) Input Field: Jenis Lantai.
    *   (Opsional) Text Area: Deskripsi Lapangan.
    *   (Opsional) Fitur Upload Foto Lapangan (bisa multiple).
    *   Toggle/Switch: Status Aktif/Tidak Aktif.
    *   Tombol Utama: "Simpan Lapangan".
*   **Aksi Utama:** Validasi input, simpan data ke backend.

### UI-A04: Halaman Jadwal & Ketersediaan (Kalender Admin SC)
*   **Tujuan:** Tampilan kalender semua lapangan SC, status booking, blokir slot/tambah manual.
*   **Elemen Utama:**
    *   Header: "Jadwal Lapangan".
    *   (Jika SC punya >1 lapangan) Dropdown/Filter: Pilih Lapangan untuk ditampilkan.
    *   Pemilihan Tanggal: Kalender interaktif atau navigasi tanggal (Sebelumnya/Berikutnya).
    *   Tampilan Jadwal (untuk tanggal & lapangan terpilih):
        *   Grid/List slot waktu (per jam).
        *   Indikator visual status: Dipesan (dengan info pemesan singkat), Diblokir Admin, Tersedia.
*   **Aksi Utama:**
    *   Tap pada slot "Tersedia": Muncul opsi/dialog "Tambah Booking Manual" atau "Blokir Slot Ini".
    *   Tap pada slot "Dipesan": Navigasi ke Detail Pemesanan (Admin SC) (UI-A08) untuk booking tersebut.
    *   Tap pada slot "Diblokir Admin": Muncul opsi/dialog "Edit Blokir" atau "Hapus Blokir".
    *   Navigasi ke Halaman Tambah Booking Manual (UI-A05) atau Form Blokir Slot (UI-A06).

### UI-A05: Halaman/Modal Tambah Booking Manual
*   **Tujuan:** Input data booking yang diterima di luar aplikasi.
*   **Elemen Utama (Form, bisa sebagai Modal/Dialog):**
    *   Judul: "Tambah Booking Manual".
    *   Informasi (Read-only): Lapangan Terpilih, Tanggal, Jam Mulai.
    *   Input Field: Nama Pemesan (Wajib).
    *   (Opsional) Input Field: Kontak Pemesan (Telepon/Email).
    *   Dropdown/Input: Durasi Sewa (dalam jam).
    *   (Otomatis) Jam Selesai, Total Harga.
    *   (Opsional) Text Area: Catatan Tambahan.
    *   Tombol Utama: "Simpan Booking". Tombol "Batal".
*   **Aksi Utama:** Simpan booking manual ke backend.

### UI-A06: Halaman/Modal Blokir Slot
*   **Tujuan:** Memblokir slot waktu untuk maintenance atau acara internal.
*   **Elemen Utama (Form, bisa sebagai Modal/Dialog):**
    *   Judul: "Blokir Slot Waktu".
    *   Informasi (Read-only): Lapangan Terpilih, Tanggal, Jam Mulai.
    *   Dropdown/Input: Durasi Blokir (atau input Jam Selesai).
    *   (Opsional) Input Field: Alasan Blokir.
    *   Tombol Utama: "Blokir Slot Ini". Tombol "Batal".
*   **Aksi Utama:** Simpan data blokir ke backend.

### UI-A07: Halaman Daftar Pemesanan (Admin SC)
*   **Tujuan:** Menampilkan semua booking yang masuk ke SC tersebut.
*   **Elemen Utama:**
    *   Header: "Daftar Pemesanan".
    *   (Opsional) Filter: Tanggal (Rentang), Status (Menunggu Konfirmasi, Terkonfirmasi, dll.), Lapangan. Tombol "Terapkan Filter".
    *   Daftar Pemesanan (Scrollable List):
        *   Setiap item (Card): Nama Pemesan, Nama Lapangan, Tanggal & Jam, Status Pemesanan (dengan warna/ikon), Total Harga.
*   **Aksi Utama:** Tap pada item untuk navigasi ke Halaman Detail Pemesanan (Admin SC) (UI-A08).

### UI-A08: Halaman Detail Pemesanan (Admin SC)
*   **Tujuan:** Detail lengkap satu booking dan aksi manajemen status.
*   **Elemen Utama:**
    *   Header: "Detail Pemesanan: [Booking ID]". Tombol "Kembali".
    *   Informasi Pemesan: Nama, Kontak (jika ada).
    *   Detail Lapangan & Jadwal: Nama Lapangan, Tanggal, Jam, Durasi.
    *   Rincian Biaya & Total Harga.
    *   Status Pemesanan saat ini (jelas terlihat).
    *   Metode Pembayaran.
    *   (Jika transfer manual & bukti ada) Tampilan/Link ke Bukti Pembayaran.
    *   Catatan dari Pemain (jika ada).
    *   Input Field/Text Area: Catatan Admin SC untuk booking ini.
    *   Tombol Aksi (sesuai status booking):
        *   "Konfirmasi Pembayaran/Booking".
        *   "Tolak Pembayaran/Booking" (dengan input alasan jika perlu).
        *   "Tandai Sebagai Selesai".
        *   "Batalkan Pemesanan (oleh SC)".
    *   Tombol: "Simpan Catatan SC".
*   **Aksi Utama:** Update status booking dan/atau catatan admin SC ke backend.

### UI-A09: Halaman Profil Sports Center (Edit Info SC)
*   **Tujuan:** Admin SC mengedit informasi detail SC mereka.
*   **Elemen Utama (Form dengan data SC saat ini):**
    *   Header: "Edit Profil Sports Center". Tombol "Kembali".
    *   Input Field: Nama Sports Center.
    *   Input Field: Alamat Lengkap.
    *   Input Field: Kota.
    *   Input Field: Nomor Telepon Kontak.
    *   Input Field: Email Kontak.
    *   Text Area: Deskripsi SC.
    *   Input Field (Time Picker): Jam Buka.
    *   Input Field (Time Picker): Jam Tutup.
    *   Fitur Upload/Ganti Foto Utama SC.
    *   Fitur Upload/Manajemen Foto Tambahan SC (bisa multiple).
    *   Manajemen Fasilitas (Checklist atau input tag dinamis).
    *   Tombol Utama: "Simpan Perubahan Profil SC".
*   **Aksi Utama:** Validasi input, simpan perubahan ke backend.

### UI-A10: Halaman Profil/Akun Admin SC
*   **Tujuan:** Mengelola akun admin SC itu sendiri.
*   **Elemen Utama:**
    *   Header: "Akun Saya".
    *   Nama Admin.
    *   Email Admin.
    *   Informasi: "Mengelola: [Nama Sports Center]".
    *   Daftar Menu (List Tiles):
        *   Edit Profil Admin (nama pribadi, telepon pribadi).
        *   Ubah Kata Sandi (Fitur tunda).
        *   Logout.
*   **Aksi Utama:** Navigasi ke halaman edit profil admin (jika ada), proses Logout.

---

## III. Halaman Umum/Utility

### UI-G01: Halaman Tidak Ada Koneksi Internet
*   **Elemen Utama:** Ikon (cth: Wifi disilang), Pesan "Tidak ada koneksi internet.", Tombol "Coba Lagi".

### UI-G02: Halaman Error Umum
*   **Elemen Utama:** Ikon (cth: Tanda seru), Pesan "Oops! Terjadi kesalahan.", (Opsional) Kode Error, Tombol "Kembali" atau "Coba Lagi".

### UI-G03: Dialog/Modal Konfirmasi
*   **Elemen Utama:** Judul Konfirmasi (cth: "Anda yakin ingin logout?"), Pesan Detail, Tombol "Ya", Tombol "Tidak/Batal". (Digunakan untuk berbagai aksi destruktif atau penting).

### UI-G04: Loading Indicator/Spinner
*   **Elemen Utama:** Animasi loading (progress circle, shimmer effect pada placeholder konten). Digunakan saat memuat data atau proses backend.

### UI-G05: Halaman Syarat & Ketentuan / Kebijakan Privasi
*   **Elemen Utama:** Header (Judul Halaman). Tombol "Kembali". Konten teks statis yang bisa di-scroll.

### UI-G06: Halaman Bantuan/FAQ
*   **Elemen Utama:** Header ("Bantuan"). Tombol "Kembali". Daftar pertanyaan yang bisa di-expand untuk melihat jawaban, atau konten teks statis.

### UI-G07: Halaman Tentang Aplikasi
*   **Elemen Utama:** Header ("Tentang Aplikasi"). Tombol "Kembali". Logo Aplikasi, Nama Aplikasi, Versi Aplikasi, (Opsional) Kredit/Lisensi.
