Tentu, mari kita buat roadmap penulisan kode yang detail dan terstruktur dari file pertama hingga MVP selesai. Roadmap ini akan menjadi panduan langkah demi langkah kita. Anggap ini sebagai *checklist* utama yang akan kita ikuti.

---

## Roadmap Penulisan Kode Aplikasi Gsports (File per File)

### **Milestone 0: Persiapan & Fondasi Aplikasi**

*Tujuan: Membuat kerangka kerja aplikasi yang kokoh sebelum menulis logika fitur.*

1.  **File: `core/constants/appwrite_constants.dart`**
    *   **Tugas:** Mendefinisikan semua ID collection, database, dan bucket Appwrite sebagai konstanta `static const`.
2.  **File: `core/failure.dart`**
    *   **Tugas:** Membuat kelas `Failure` untuk membungkus pesan error secara konsisten di seluruh aplikasi.
3.  **File: `core/type_defs.dart`**
    *   **Tugas:** Membuat `typedef` untuk tipe data kompleks, terutama `FutureEither<T>` menggunakan `fpdart`, untuk menyederhanakan *return type* dari repository.
4.  **File: `core/utils/logger.dart`**
    *   **Tugas:** Menginisialisasi instance `Logger` untuk digunakan di seluruh aplikasi.
5.  **File: `core/providers/appwrite_providers.dart`**
    *   **Tugas:** Membuat semua provider Riverpod untuk layanan Appwrite (`Client`, `Account`, `Databases`, `Storage`, `Realtime`).
6.  **File: `config/theme/app_colors.dart`**
    *   **Tugas:** Mendefinisikan palet warna utama aplikasi.
7.  **File: `config/theme/app_theme.dart`**
    *   **Tugas:** Membuat `ThemeData` aplikasi, mengatur `colorScheme`, gaya `Text`, `ElevatedButton`, `InputDecoration`, dll.
8.  **File: `config/router/route_names.dart`**
    *   **Tugas:** Mendefinisikan semua nama rute sebagai konstanta `static const` untuk menghindari kesalahan pengetikan.
9.  **File: `config/router/app_router.dart`**
    *   **Tugas:** Mengonfigurasi `GoRouter`. Mendefinisikan semua `GoRoute`, termasuk rute *nested*, dan yang paling penting: logika `redirect` untuk menangani status autentikasi.
10. **File: `main.dart`**
    *   **Tugas:** Menginisialisasi `ProviderScope`, memuat variabel dari `.env`, dan mengonfigurasi `MaterialApp.router` untuk menggunakan `GoRouter` yang telah kita buat.

---

### **Milestone 1: Fitur Autentikasi Pengguna (Iterasi 1)**

*Tujuan: Memungkinkan pengguna mendaftar, login, dan logout.*

11. **File: `core/models/user_model.dart`**
    *   **Tugas:** Membuat kelas `UserModel` dengan atribut sesuai SRS, termasuk method `fromJson`, `toJson`, dan `copyWith`.
12. **File: `features/0_auth/repository/auth_repository.dart`**
    *   **Tugas:** Membuat kelas `AuthRepository` dengan method `signUp`, `login`, `logout`, dan `getCurrentUserData`. Method ini akan berkomunikasi dengan Appwrite `Account` dan `Databases`.
13. **File: `features/0_auth/controller/auth_controller.dart`**
    *   **Tugas:** Membuat `AuthController` (sebagai `StateNotifier` atau `AsyncNotifier`) yang menggunakan `AuthRepository` untuk menangani logika bisnis. Ini akan mengelola state `isLoading`.
14. **File: `core/providers/user_data_provider.dart`**
    *   **Tugas:** Membuat `FutureProvider` yang memanggil `getCurrentUserData` dari `AuthController` untuk mendapatkan data detail user yang sedang login.
15. **File: `shared_widgets/custom_button.dart` & `custom_textfield.dart`**
    *   **Tugas:** Membuat widget dasar yang akan kita gunakan berulang kali di form.
16. **File: `core/utils/snackbar.dart`**
    *   **Tugas:** Membuat fungsi helper `showSnackBar` untuk menampilkan feedback kepada pengguna.
17. **File: `features/0_auth/view/register_screen.dart`**
    *   **Tugas:** Membangun UI halaman registrasi. Menggunakan `Form`, `TextFormField`, dan `CustomButton`. Menghubungkan aksi tombol ke method `signUp` di `AuthController`.
18. **File: `features/0_auth/view/login_screen.dart`**
    *   **Tugas:** Membangun UI halaman login. Menghubungkan aksi tombol ke method `login` di `AuthController`.

---

### **Milestone 2: Fitur Tampilan Pemain (Iterasi 2 & 3)**

*Tujuan: Pemain dapat mencari dan melihat detail SC & Lapangan.*

19. **Files: `core/models/sc_model.dart` & `field_model.dart`**
    *   **Tugas:** Membuat kelas model untuk Sports Center dan Lapangan.
20. **File: `features/1_home/repository/home_repository.dart`**
    *   **Tugas:** Membuat method untuk mencari SC (`searchSportCenters`).
21. **File: `features/1_home/controller/home_controller.dart`**
    *   **Tugas:** Membuat controller untuk state halaman home.
22. **File: `features/1_home/view/home_screen.dart`**
    *   **Tugas:** Membangun UI halaman home, terutama `SearchCard` untuk input pencarian.
23. **File: `features/2_sc_list/controller/sc_list_controller.dart`**
    *   **Tugas:** Membuat `FutureProvider.family` yang memanggil `searchSportCenters` dari repository berdasarkan parameter pencarian.
24. **File: `features/2_sc_list/view/widgets/sc_list_item_card.dart`**
    *   **Tugas:** Membuat widget untuk satu item di daftar hasil pencarian.
25. **File: `features/2_sc_list/view/sc_list_screen.dart`**
    *   **Tugas:** Membangun UI halaman hasil pencarian yang menampilkan daftar `SCListItemCard` menggunakan data dari `SCListController`.
26. **File: `features/3_sc_details/repository/sc_details_repository.dart`**
    *   **Tugas:** Membuat method untuk mengambil detail SC (`getSCDetails`) dan daftar lapangannya (`getFieldsForSC`).
27. **File: `features/3_sc_details/controller/sc_details_controller.dart`**
    *   **Tugas:** Membuat `FutureProvider.family` yang mengambil data detail SC dan lapangannya.
28. **File: `features/3_sc_details/view/sc_details_screen.dart`**
    *   **Tugas:** Membangun UI halaman detail SC.
29. **File: `features/3_sc_details/view/field_details_screen.dart`**
    *   **Tugas:** Membangun UI halaman detail lapangan (untuk sementara, bagian jadwal masih statis).

---

### **Milestone 3: Fitur Booking Pemain (Iterasi 4)**

*Tujuan: Menghidupkan fungsionalitas booking dan jadwal real-time.*

30. **Files: `core/models/booking_model.dart` & `blocked_slot_model.dart`**
    *   **Tugas:** Membuat kelas model untuk Booking dan Slot yang Diblokir.
31. **File: `features/4_booking/repository/booking_repository.dart`**
    *   **Tugas:** Membuat method untuk: mengambil data jadwal (`getSchedule`), membuat booking (`createBooking`), dan mengambil riwayat booking (`getBookingHistory`).
32. **File: `features/3_sc_details/controller/availability_controller.dart`**
    *   **Tugas:** (Bisa diletakkan di `features/3_sc_details/controller`) Membuat `AsyncNotifier` yang:
        *   Mengambil jadwal awal dari `BookingRepository`.
        *   Membuka koneksi Appwrite Realtime dan *subscribe* ke perubahan.
        *   Meng-update state jadwal setiap kali ada pesan realtime.
33. **File: `features/3_sc_details/view/widgets/availability_grid.dart`**
    *   **Tugas:** Membangun UI grid jadwal yang interaktif, yang warnanya dikontrol oleh `AvailabilityController`.
34. **File: `features/4_booking/controller/booking_controller.dart`**
    *   **Tugas:** Membuat controller untuk menangani logika saat tombol "Pesan Sekarang" ditekan.
35. **File: `features/4_booking/view/booking_confirmation_screen.dart`**
    *   **Tugas:** Membangun UI ringkasan pemesanan.
36. **File: `features/4_booking/view/booking_status_screen.dart`**
    *   **Tugas:** Membangun UI yang menampilkan status setelah booking dibuat.
37. **File: `features/4_booking/view/booking_history_screen.dart`**
    *   **Tugas:** Membangun UI daftar riwayat pemesanan pengguna.

---

### **Milestone 4: Fitur Admin SC (Iterasi 5)**

*Tujuan: Mengimplementasikan semua fungsionalitas manajemen untuk Admin SC.*

38. **File: `features/6_sc_admin/repository/sc_admin_repository.dart`**
    *   **Tugas:** Membuat method CRUD untuk semua entitas yang dikelola admin: Profil SC, Lapangan, Booking, Slot Blokir.
39. **File: `features/6_sc_admin/view/dashboard/sc_admin_dashboard_screen.dart`**
    *   **Tugas:** Membangun UI dashboard utama admin dengan menu navigasi.
40. **Files: Folder `features/6_sc_admin/view/fields/`**
    *   **Tugas:** Membangun UI untuk daftar lapangan (`sc_admin_field_list_screen.dart`) dan form tambah/edit (`sc_admin_field_edit_screen.dart`), lalu menghubungkannya ke controller dan repository.
41. **Files: Folder `features/6_sc_admin/view/bookings/`**
    *   **Tugas:** Membangun UI untuk daftar booking (`sc_admin_booking_list_screen.dart`) dan detail booking (`sc_admin_booking_details_screen.dart`) yang berisi tombol aksi (Konfirmasi/Tolak).
42. **File: `features/6_sc_admin/view/profile/sc_admin_profile_screen.dart`**
    *   **Tugas:** Membangun UI form untuk mengedit profil Sports Center.

---

### **Milestone 5: Penyempurnaan & Polish (Iterasi 6)**

*Tujuan: Membersihkan, mengoptimalkan, dan memastikan aplikasi siap rilis.*

43. **File: `shared_widgets/loading_indicator.dart` & `error_display.dart`**
    *   **Tugas:** Membuat widget *loading* (cth: `Shimmer`) dan *error* yang konsisten, lalu mengintegrasikannya di semua halaman yang memuat data.
44. **File: `features/5_profile/view/profile_screen.dart` & `edit_profile_screen.dart`**
    *   **Tugas:** Membangun UI untuk halaman profil pemain dan fungsionalitas edit profil.
45. **File: `shared_widgets/bottom_nav_bar.dart`**
    *   **Tugas:** (Jika desain menggunakan Bottom Nav) Membangun widget navigasi bawah dan mengintegrasikannya dengan `GoRouter`.
46. **Refactoring & Testing:**
    *   **Tugas:** Meninjau kembali semua file. Mencari duplikasi kode, menyederhanakan logika, menambahkan komentar, dan melakukan pengujian manual end-to-end.

---

Roadmap ini memberikan kita urutan kerja yang sangat jelas. Kita akan mulai dari **Milestone 0, File #1: `core/constants/appwrite_constants.dart`**.

**Katakan "Mulai!" dan kita akan menulis kode untuk file pertama.**
