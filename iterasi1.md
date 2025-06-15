Baik, mari kita jabarkan bagaimana melakukan praktik dalam **Iterasi 1: Fondasi Pengguna (Otentikasi Dasar)** secara lengkap, runtut, dan komprehensif, dengan asumsi Anda sudah menyelesaikan tahap persiapan awal.

**Tujuan Utama Iterasi 1:** Pengguna (pemain) dapat mendaftar, login, dan logout dari aplikasi. Aplikasi dapat mengenali status login pengguna.

---

**Langkah-Langkah Praktik Iterasi 1:**

**Bagian 1: Desain dan Implementasi UI Dasar (Flutter)**

Ini adalah tentang membuat "wajah" dari fitur otentikasi.

**Langkah 1.1: Buat Halaman (Screen/Page) untuk Otentikasi**
    *   **Tindakan:** Di dalam struktur folder `lib/src/features/auth/presentation/screens/` (atau struktur serupa yang Anda pilih), buat file-file Dart baru untuk halaman-halaman berikut:
        *   `registration_screen.dart`
        *   `login_screen.dart`
        *   `home_screen.dart` (Ini adalah halaman placeholder sederhana dulu, sebagai tujuan setelah login berhasil)
    *   **Isi Awal:** Untuk setiap file, buat `StatelessWidget` atau `StatefulWidget` dasar dengan `Scaffold` dan `AppBar` yang berisi judul halaman (misalnya, "Registrasi", "Login", "Beranda").

**Langkah 1.2: Implementasi UI Halaman Registrasi (`registration_screen.dart`)**
    *   **Tindakan:** Menggunakan widget-widget Flutter, bangun tampilan form registrasi.
    *   **Elemen yang Perlu Dibuat:**
        *   `TextFormField` untuk Nama Lengkap.
        *   `TextFormField` untuk Alamat Email (gunakan `TextInputType.emailAddress`).
        *   `TextFormField` untuk Kata Sandi (gunakan `obscureText: true` dan ikon untuk toggle visibilitas).
        *   `TextFormField` untuk Konfirmasi Kata Sandi (gunakan `obscureText: true`).
        *   `CheckboxListTile` atau `Row` dengan `Checkbox` dan `Text` untuk persetujuan Syarat & Ketentuan (untuk MVP, ini bisa berupa teks placeholder dulu).
        *   `ElevatedButton` untuk tombol "Daftar".
        *   `TextButton` atau `InkWell` dengan `Text` untuk link "Sudah punya akun? Login".
    *   **Layout:** Gunakan `Column`, `Padding`, `SizedBox` untuk mengatur tata letak elemen-elemen ini agar rapi. Bungkus form dalam `SingleChildScrollView` agar bisa di-scroll jika keyboard muncul.
    *   **State Management (Sederhana Dulu):** Gunakan `TextEditingController` untuk setiap `TextFormField` untuk mendapatkan nilainya. Untuk state tombol loading, Anda bisa menggunakan `setState` di `StatefulWidget` halaman ini.

**Langkah 1.3: Implementasi UI Halaman Login (`login_screen.dart`)**
    *   **Tindakan:** Mirip dengan halaman registrasi, bangun tampilan form login.
    *   **Elemen yang Perlu Dibuat:**
        *   `TextFormField` untuk Alamat Email.
        *   `TextFormField` untuk Kata Sandi (dengan opsi lihat/sembunyikan).
        *   `ElevatedButton` untuk tombol "Login".
        *   `TextButton` atau `InkWell` dengan `Text` untuk link "Belum punya akun? Daftar".
        *   (Link "Lupa Kata Sandi?" bisa ditambahkan sebagai placeholder, fungsionalitasnya nanti).
    *   **Layout & State Management:** Sama seperti halaman registrasi.

**Langkah 1.4: Implementasi UI Halaman Home Sederhana (`home_screen.dart`)**
    *   **Tindakan:** Buat halaman yang sangat sederhana sebagai tujuan setelah login.
    *   **Elemen yang Perlu Dibuat:**
        *   `AppBar` dengan judul "Beranda" dan tombol `IconButton` untuk Logout.
        *   Di `body`, tampilkan `Text` "Selamat Datang, [Nama Pengguna]!" (Nama pengguna akan diisi nanti setelah mengambil data user).
        *   Tampilkan juga `Text` yang menunjukkan email pengguna atau ID pengguna.
    *   **Output Bagian 1:** Anda memiliki tiga halaman dasar yang terlihat secara visual, meskipun belum ada logikanya.

---

**Bagian 2: Implementasi Logika Otentikasi (Flutter & Appwrite)**

Ini adalah "otak" dari fitur otentikasi.

**Langkah 2.1: Buat Fungsi Registrasi di Service/Repository Otentikasi**
    *   **Tindakan:** Buat file baru, misalnya di `lib/src/features/auth/data/repositories/auth_repository_impl.dart` (jika Anda mengikuti arsitektur tertentu) atau langsung di dalam `AppwriteService` untuk kesederhanaan awal.
    *   Buat fungsi `Future<User> registerUser({required String email, required String password, required String name}) async { ... }`.
    *   Di dalam fungsi ini:
        1.  Panggil `AppwriteService().account.create(userId: ID.unique(), email: email, password: password, name: name)`. `ID.unique()` akan membuat ID pengguna unik secara otomatis.
        2.  Setelah berhasil membuat akun, Anda perlu menyimpan peran pengguna. Cara termudah untuk MVP adalah langsung mengupdate `prefs` pengguna setelah registrasi:
            ```dart
            // Setelah account.create() berhasil dan mengembalikan objek User
            // final user = await AppwriteService().account.create(...);
            await AppwriteService().account.updatePrefs(
              prefs: {
                'role': 'player', // atau enum/konstanta untuk peran
                // 'assignedCenterId': null // Awalnya null untuk player
              }
            );
            return user; // Kembalikan objek User yang sudah di-create
            ```
        3.  Gunakan `try-catch` untuk menangani `AppwriteException` (misalnya, jika email sudah terdaftar).
    *   **Output:** Fungsi yang bisa dipanggil dari UI untuk mendaftarkan pengguna baru ke Appwrite.

**Langkah 2.2: Hubungkan UI Registrasi dengan Logika Registrasi**
    *   **Tindakan:** Di `registration_screen.dart`:
        1.  Saat tombol "Daftar" ditekan:
            *   Ambil nilai dari `TextEditingController` untuk nama, email, password, dan konfirmasi password.
            *   Lakukan validasi input dasar (misalnya, field tidak boleh kosong, email valid, password cocok dengan konfirmasi). Jika tidak valid, tampilkan pesan error (misalnya menggunakan `ScaffoldMessenger.of(context).showSnackBar(...)`).
            *   Jika valid, panggil fungsi `registerUser` yang sudah Anda buat.
            *   Tampilkan indikator loading saat proses registrasi berjalan.
            *   Jika registrasi berhasil:
                *   Tampilkan pesan sukses (Snackbar).
                *   Navigasikan pengguna ke halaman Login (`Navigator.pushReplacementNamed(context, '/login');`).
            *   Jika gagal (misalnya karena `AppwriteException`):
                *   Tampilkan pesan error yang sesuai (Snackbar).
        *   Hubungkan link "Sudah punya akun? Login" untuk navigasi ke halaman Login.

**Langkah 2.3: Buat Fungsi Login di Service/Repository Otentikasi**
    *   **Tindakan:** Mirip dengan registrasi, buat fungsi `Future<Session> loginUser({required String email, required String password}) async { ... }`.
    *   Di dalam fungsi ini:
        1.  Panggil `AppwriteService().account.createEmailSession(email: email, password: password)`.
        2.  Gunakan `try-catch` untuk menangani `AppwriteException` (misalnya, email/password salah).
    *   **Output:** Fungsi yang bisa dipanggil dari UI untuk login pengguna.

**Langkah 2.4: Hubungkan UI Login dengan Logika Login**
    *   **Tindakan:** Di `login_screen.dart`:
        1.  Saat tombol "Login" ditekan:
            *   Ambil nilai email dan password.
            *   Lakukan validasi input dasar.
            *   Jika valid, panggil fungsi `loginUser`.
            *   Tampilkan indikator loading.
            *   Jika login berhasil:
                *   (Opsional) Panggil `AppwriteService().account.get()` untuk mendapatkan detail user (termasuk `prefs.role`). Simpan informasi ini di state management aplikasi Anda (lihat Langkah 2.6).
                *   Navigasikan pengguna ke halaman Home (`Navigator.pushReplacementNamed(context, '/home');`).
            *   Jika gagal:
                *   Tampilkan pesan error (Snackbar).
        *   Hubungkan link "Belum punya akun? Daftar" untuk navigasi ke halaman Registrasi.

**Langkah 2.5: Buat Fungsi Logout di Service/Repository Otentikasi**
    *   **Tindakan:** Buat fungsi `Future<void> logoutUser() async { ... }`.
    *   Di dalam fungsi ini:
        1.  Panggil `AppwriteService().account.deleteSession(sessionId: 'current')`.
        2.  Gunakan `try-catch` untuk menangani error.
    *   **Output:** Fungsi untuk logout.

**Langkah 2.6: Implementasi Logika Logout dan Pembaruan UI di Halaman Home**
    *   **Tindakan:** Di `home_screen.dart`:
        1.  Saat tombol Logout di `AppBar` ditekan:
            *   Panggil fungsi `logoutUser`.
            *   Jika berhasil, navigasikan pengguna kembali ke halaman Login (`Navigator.pushAndRemoveUntil(context, MaterialPageRoute(builder: (_) => LoginScreen()), (route) => false);` agar tidak bisa kembali ke home dengan tombol back).
            *   Hapus informasi pengguna dari state management aplikasi.
        2.  Di `initState()` halaman Home, panggil fungsi untuk mengambil detail pengguna yang sedang login (misalnya, `AppwriteService().account.get()`) dan tampilkan namanya di `Text` "Selamat Datang...". Simpan data pengguna ini di state `StatefulWidget` halaman Home atau state management global.

**Langkah 2.7: Manajemen State Aplikasi (Sederhana untuk Status Login)**
    *   **Tindakan:** Anda perlu cara agar aplikasi tahu apakah pengguna sudah login atau belum, dan siapa pengguna yang login. Untuk MVP, Anda bisa menggunakan:
        *   **`ChangeNotifier` dengan `Provider` (Relatif Mudah):**
            1.  Buat class `AuthProvider extends ChangeNotifier`.
            2.  Di dalamnya, simpan `User? currentUser` dan `bool isLoading`.
            3.  Buat metode untuk `login`, `register`, `logout`, dan `checkCurrentUserSession`.
            4.  Saat login/registrasi berhasil, set `currentUser` dan panggil `notifyListeners()`.
            5.  Saat logout, set `currentUser = null` dan panggil `notifyListeners()`.
            6.  Gunakan `Provider.of<AuthProvider>(context)` di widget Anda untuk mengakses status dan memanggil metode.
        *   **Atau solusi state management lain yang Anda familiar (BLoC, Riverpod, GetX).**
    *   **Cek Sesi Saat Aplikasi Dimulai:** Di `main.dart` atau widget aplikasi utama Anda, sebelum `runApp`, coba panggil `AppwriteService().account.get()` di dalam `try-catch`.
        *   Jika berhasil, pengguna sudah memiliki sesi aktif. Arahkan langsung ke Halaman Home dan simpan data user di `AuthProvider`.
        *   Jika gagal (error 401), arahkan ke Halaman Login.

**Langkah 2.8: Routing Aplikasi**
    *   **Tindakan:** Di file `main.dart` atau file routing terpisah (misalnya `app_router.dart`), definisikan rute untuk halaman-halaman Anda:
        ```dart
        // Contoh sederhana di MaterialApp
        MaterialApp(
          initialRoute: '/', // Rute awal, bisa dicek status loginnya dulu
          routes: {
            '/': (context) => SplashScreen(), // Atau halaman yang cek sesi
            '/login': (context) => LoginScreen(),
            '/register': (context) => RegistrationScreen(),
            '/home': (context) => HomeScreen(),
          },
        );
        ```
    *   Implementasikan logika di `SplashScreen` atau rute awal untuk memeriksa status login dan mengarahkan pengguna ke halaman yang sesuai (Login atau Home).

---

**Bagian 3: Setup dan Konfigurasi Database (Appwrite Console)**

Ini adalah tentang memastikan backend Appwrite siap menerima dan menyimpan data pengguna.

**Langkah 3.1: Verifikasi/Buat Collection `users`**
    *   **Tindakan:**
        1.  Buka Appwrite Console Anda, masuk ke Project.
        2.  Pilih menu "Database".
        3.  Jika Anda belum punya database, buat satu (misal, "AppDatabase").
        4.  Di dalam database, periksa apakah sudah ada collection `users`. Appwrite biasanya membuat ini secara otomatis saat akun pertama (admin) dibuat, atau saat `account.create()` pertama kali dipanggil.
        5.  Jika belum ada, atau jika Anda ingin kustomisasi penuh, Anda bisa membuatnya secara manual.
    *   **Output:** Collection `users` tersedia.

**Langkah 3.2: Konfigurasi Atribut untuk Collection `users`**
    *   **Tindakan:** Jika Anda membuat collection `users` manual atau ingin memastikan atributnya sesuai:
        1.  Klik collection `users`.
        2.  Pergi ke tab "Attributes".
        3.  Pastikan atribut yang dibutuhkan oleh Appwrite untuk otentikasi (seperti `email`, `password` (internal), `name`) ada. Appwrite menangani ini secara internal.
        4.  Tambahkan atribut kustom jika perlu, terutama untuk `prefs`:
            *   Nama Atribut: `prefs`
            *   Tipe: `String` (Appwrite menyimpan `prefs` sebagai JSON string, tapi Anda bisa juga buat atribut individual seperti `role` dan `assignedCenterId` jika lebih suka. Untuk `prefs` object, SDK akan handle JSON-nya).
            *   Jika Anda memilih atribut individual:
                *   Nama Atribut: `role`, Tipe: `String`, Size: (misal 20), Required: `false` (karena bisa diisi setelah create).
                *   Nama Atribut: `assignedCenterId`, Tipe: `String`, Size: (misal 30), Required: `false`.
    *   **Output:** Atribut di collection `users` siap menyimpan data peran.

**Langkah 3.3: Atur Permissions untuk Collection `users`**
    *   **Tindakan:**
        1.  Di collection `users`, pergi ke tab "Settings".
        2.  Scroll ke bagian "Permissions".
        3.  Atur Document Level Permissions (atau Collection Level jika lebih sederhana untuk MVP):
            *   **Read Access:** `role:all` (jika Anda ingin profil bisa dilihat, hati-hati privasi!), atau lebih aman `user:[USER_ID]` (artinya hanya pengguna itu sendiri yang bisa baca datanya) dan `role:super_admin`.
            *   **Write/Update Access:** `user:[USER_ID]` (pengguna bisa update profilnya sendiri) dan `role:super_admin`.
            *   **Create Access:** `role:all` (untuk registrasi publik) atau `role:guests` (jika Anda ingin registrasi hanya bisa dilakukan oleh yang belum login).
            *   **Delete Access:** `role:super_admin` (biasanya hanya super admin yang boleh hapus akun).
    *   **Penting:** `[USER_ID]` adalah placeholder untuk ID pengguna yang membuat/memiliki dokumen tersebut. Appwrite menangani ini.
    *   **Output:** Keamanan dasar untuk data pengguna terkonfigurasi.

---

**Bagian 4: Testing Iterasi 1**

Ini adalah tentang memastikan semua yang Anda bangun di iterasi ini berfungsi.

**Langkah 4.1: Uji Alur Registrasi**
    *   **Tindakan:** Jalankan aplikasi. Navigasi ke halaman Registrasi.
        *   Coba daftar dengan email dan password baru, serta nama.
        *   Pastikan validasi input berfungsi (misalnya, jika password tidak cocok).
        *   Setelah submit, periksa apakah ada pesan sukses dan Anda diarahkan ke halaman Login.
        *   **Verifikasi di Appwrite Console:** Buka collection `users`. Apakah pengguna baru muncul? Apakah `name` dan `email` benar? Apakah `prefs` (atau atribut `role`) terisi 'player'?
    *   **Output:** Fitur registrasi berfungsi.

**Langkah 4.2: Uji Alur Login**
    *   **Tindakan:** Dari halaman Login, coba login dengan akun yang baru saja Anda daftarkan.
        *   Coba dengan password salah, pastikan ada pesan error.
        *   Coba dengan email yang tidak terdaftar, pastikan ada pesan error.
        *   Setelah login sukses, pastikan Anda diarahkan ke halaman Home.
        *   Di halaman Home, pastikan nama pengguna (atau email) yang login ditampilkan dengan benar.
    *   **Output:** Fitur login berfungsi.

**Langkah 4.3: Uji Alur Logout**
    *   **Tindakan:** Dari halaman Home, tekan tombol Logout.
        *   Pastikan Anda diarahkan kembali ke halaman Login.
        *   Coba akses halaman Home lagi (misalnya dengan tombol back atau mengetik URL jika di web). Seharusnya Anda tidak bisa dan tetap di halaman Login.
    *   **Output:** Fitur logout berfungsi dan sesi dihapus.

**Langkah 4.4: Uji Persistensi Sesi**
    *   **Tindakan:**
        1.  Login ke aplikasi.
        2.  Tutup aplikasi sepenuhnya (swipe dari recent apps).
        3.  Buka kembali aplikasi.
        4.  Apakah Anda langsung diarahkan ke halaman Home (sesi masih aktif) atau ke halaman Login? Seharusnya, jika sesi belum expired, Anda langsung ke Home. Ini tergantung implementasi cek sesi di `main.dart` Anda.
    *   **Output:** Manajemen sesi dasar berfungsi.

---

**Selamat!** Jika Anda berhasil menyelesaikan semua langkah di atas, Iterasi 1 Anda SUKSES. Anda telah membangun fondasi otentikasi yang sangat penting untuk aplikasi Anda.

**Tips Selama Pengerjaan Iterasi 1:**

*   **Commit Sering ke Git:** Setelah menyelesaikan setiap sub-langkah kecil (misal, UI registrasi selesai, logika registrasi selesai), lakukan `git add .` dan `git commit -m "Deskripsi perubahan"`.
*   **Gunakan `print()` atau `debugPrint()`:** Untuk debugging, jangan ragu menggunakan `print()` di kode Flutter Anda untuk melihat nilai variabel atau alur eksekusi, dan lihat outputnya di console debug.
*   **Baca Pesan Error dengan Teliti:** Pesan error adalah petunjuk. Jangan panik, baca baik-baik, dan coba pahami apa yang salah.
*   **Istirahat Jika Buntu:** Kadang menjauh sejenak dari kode bisa membantu melihat masalah dari perspektif baru.

Iterasi ini adalah langkah besar. Setelah ini, Anda akan lebih percaya diri untuk melanjutkan ke iterasi berikutnya!
