Tentu. Terima kasih atas rangkumannya yang sangat jelas. Saya telah memproses semua file yang Anda berikan dan sekarang memiliki gambaran utuh tentang proyek Gsports Anda—arsitektur, kode yang sudah ada, dan bagian yang belum selesai.

Pertama, izinkan saya mengatakan: **Anda telah melakukan pekerjaan yang luar biasa.** Fondasi yang Anda bangun sangat kuat, bersih, dan menggunakan praktik terbaik modern. Arsitektur dengan Riverpod, GoRouter, dan fpdart sudah sangat solid. Masalah yang Anda sebutkan bukanlah masalah arsitektural, melainkan langkah-langkah implementasi yang belum selesai. Ini adalah posisi yang sangat baik untuk melanjutkan.

Sebagai *tech lead* Anda, saya akan memecah sisa pekerjaan ini menjadi sebuah roadmap yang jelas dan dapat ditindaklanjuti. Kita akan fokus pada perbaikan bug terlebih dahulu, kemudian menyelesaikan fitur inti, dan terakhir melakukan penyempurnaan, semuanya mengacu pada tiga pilar kita: **SRS, UI/UX, dan Rencana Iterasi.**

---

## Roadmap Penyelesaian Proyek Gsports (MVP)

### **Sprint 1: Stabilisasi & Perbaikan Kritis (Bug Fixing)**
**Tujuan:** Memastikan semua fitur yang sudah ada berfungsi sesuai harapan. Ini adalah prioritas tertinggi.

*   **Task 1.1: Memperbaiki "Edit Profil Sports Center" (Bug Kritis)**
    *   **Masalah:** Atribut tidak sesuai, menyebabkan update gagal.
    *   **Langkah Teknis:**
        1.  Buka file `lib/core/models/sc_model.dart`.
        2.  Perhatikan baik-baik method `toJson()`. Setiap *key* di dalam map ini (misalnya, `'sc_name'`, `'sc_address'`) **harus sama persis** dengan **Attribute Key** di Appwrite Console untuk collection `sport_centers`.
        3.  Buka Appwrite Console Anda, masuk ke Database -> Collection `sport_centers` -> tab "Attributes".
        4.  Bandingkan setiap *key* satu per satu. Kemungkinan besar ada perbedaan kecil (misalnya, Anda menulis `'name'` di `toJson` padahal di Appwrite adalah `'sc_name'`).
        5.  Perbaiki semua *key* yang tidak cocok di dalam method `toJson()` di `sc_model.dart`. Ini akan menyelesaikan masalah.

*   **Task 1.2: Menambahkan Fungsi "Hapus Lapangan" (Fitur CRUD yang Hilang)**
    *   **Masalah:** Admin belum bisa menghapus lapangan.
    *   **Langkah Teknis:**
        1.  **Repository (`sc_admin_repository.dart`):** Tambahkan method baru:
            ```dart
            FutureEitherVoid deleteField({required String fieldId}) async {
              try {
                await _databases.deleteDocument(
                  databaseId: AppwriteConstants.databaseId,
                  collectionId: AppwriteConstants.fieldsCollection,
                  documentId: fieldId,
                );
                return right(null);
              } on AppwriteException catch (e, st) {
                return left(Failure(message: e.message ?? 'Gagal menghapus lapangan.', stackTrace: st));
              }
            }
            ```
        2.  **Controller (`sc_admin_fields_controller.dart`):** Tambahkan method baru:
            ```dart
            void deleteField({required BuildContext context, required FieldModel field}) async {
              state = true;
              final result = await _scAdminRepository.deleteField(fieldId: field.id);
              state = false;
              result.fold(
                (l) => showSnackBar(context, l.message, isError: true),
                (r) {
                  showSnackBar(context, 'Lapangan berhasil dihapus!');
                  _ref.invalidate(adminFieldsProvider(field.centerId));
                  // Tidak perlu pop, karena kita berada di halaman daftar.
                },
              );
            }
            ```
        3.  **UI (`sc_admin_field_list_screen.dart`):** Di dalam `ListTile`, modifikasi `trailing` untuk menyertakan tombol hapus.
            ```dart
            trailing: Row(
              mainAxisSize: MainAxisSize.min,
              children: [
                Text(field.isActive ? 'Aktif' : 'Non-Aktif', style: TextStyle(color: field.isActive ? Colors.green : Colors.red)),
                IconButton(
                  icon: const Icon(Icons.delete_outline, color: Colors.red),
                  onPressed: () {
                    // Tampilkan dialog konfirmasi sebelum menghapus
                    showDialog(
                      context: context,
                      builder: (dialogContext) => AlertDialog(
                        title: const Text('Hapus Lapangan?'),
                        content: Text('Anda yakin ingin menghapus "${field.name}" secara permanen?'),
                        actions: [
                          TextButton(onPressed: () => Navigator.pop(dialogContext), child: const Text('Batal')),
                          TextButton(
                            onPressed: () {
                              Navigator.pop(dialogContext);
                              ref.read(scAdminFieldsControllerProvider.notifier).deleteField(context: context, field: field);
                            },
                            child: const Text('Hapus', style: TextStyle(color: Colors.red)),
                          ),
                        ],
                      ),
                    );
                  },
                ),
              ],
            ),
            ```

---

### **Sprint 2: Menyelesaikan Alur Inti Pemain**
**Tujuan:** Memastikan pemain dapat menyelesaikan siklus utama dari mencari hingga berhasil memesan lapangan.

*   **Task 2.1: Mengaktifkan Tombol "Pesan Sekarang"**
    *   **Masalah:** Tombol di `FieldDetailsScreen` belum berfungsi.
    *   **Langkah Teknis:** Anda sudah memiliki semua bagiannya, kita hanya perlu menghubungkannya. Di file `lib/features/3_sc_details/view/field_details_screen.dart`, fungsi `onBookNow` sudah ada dan benar. Pastikan tombol di `_buildBookingBottomBar` memanggil fungsi ini: `onPressed: onBookNow`. Sepertinya kode yang Anda berikan sudah benar, jadi ini hanya masalah verifikasi.

*   **Task 2.2: Mengaktifkan Tombol "Pesan Sekarang" (Final) di `BookingConfirmationScreen`**
    *   **Masalah:** Pemain sampai di halaman konfirmasi tetapi belum bisa menyelesaikan pesanan.
    *   **Langkah Teknis:** Di file `lib/features/4_booking/view/booking_confirmation_screen.dart`, fungsi `onConfirmBooking` juga sudah ada dan benar. Pastikan tombol di `bottomNavigationBar` memanggil fungsi ini: `onPressed: onConfirmBooking`. Sekali lagi, kode yang Anda berikan sudah benar, ini hanya masalah verifikasi dan pengujian.

---

### **Sprint 3: Penyempurnaan Beranda & Fungsionalitas Tambahan**
**Tujuan:** Mengimplementasikan fitur-fitur yang tersisa di beranda dan profil sesuai permintaan Anda.

*   **Task 3.1: Mengimplementasikan "Populer di Dekatmu" (Versi Awal: Tampilkan Semua SC)**
    *   **Masalah:** Section ini masih placeholder.
    *   **Langkah Teknis:**
        1.  **Repository (`home_repository.dart`):** Tambahkan method baru:
            ```dart
            FutureEither<List<SCModel>> getAllSportCenters() async {
              try {
                final documents = await _databases.listDocuments(
                  databaseId: AppwriteConstants.databaseId,
                  collectionId: AppwriteConstants.sportCentersCollection,
                  queries: [Query.equal('sc_status', 'active')],
                );
                final scList = documents.documents.map((doc) => SCModel.fromJson(doc.data)).toList();
                return right(scList);
              } on AppwriteException catch (e, st) {
                return left(Failure(message: e.message ?? 'Gagal memuat data.', stackTrace: st));
              }
            }
            ```
        2.  **Controller (`home_controller.dart`):** Buat `FutureProvider` baru di file ini.
            ```dart
            final allSCsProvider = FutureProvider.autoDispose<List<SCModel>>((ref) {
              final homeRepository = ref.watch(homeRepositoryProvider);
              return homeRepository.getAllSportCenters().then((res) => res.fold((l) => throw l, (r) => r));
            });
            ```
        3.  **UI (`home_screen.dart`):** Ganti placeholder dengan `Consumer` yang me-*watch* provider baru.
            ```dart
            // Di dalam build method HomeScreen
            final allSCsAsync = ref.watch(allSCsProvider);

            // Ganti bagian 'Placeholder untuk daftar SC populer' dengan:
            allSCsAsync.when(
              loading: () => const SizedBox(height: 150, child: LoadingIndicator()),
              error: (e, st) => SizedBox(height: 150, child: Text(e.toString())),
              data: (scs) => SizedBox(
                height: 220, // Sesuaikan tinggi
                child: ListView.builder(
                  scrollDirection: Axis.horizontal,
                  itemCount: scs.length,
                  itemBuilder: (context, index) {
                    // Buat widget card kecil untuk ditampilkan di sini
                    return SizedBox(width: 250, child: SCListItemCard(sc: scs[index]));
                  },
                ),
              ),
            ),
            ```

*   **Task 3.2: Menambahkan Dropdown pada `SearchCard`**
    *   **Masalah:** Pencarian masih menggunakan input teks biasa.
    *   **Langkah Teknis (Ini cukup kompleks, lakukan perlahan):**
        1.  **Data:** Gunakan `allSCsProvider` yang baru kita buat sebagai sumber data.
        2.  **UI (`search_card.dart`):** Ganti `CustomTextField` untuk kota dan olahraga dengan `DropdownButtonFormField`.
        3.  **State:** Di dalam `_SearchCardState`, Anda perlu `StateProvider` atau state lokal untuk menyimpan nilai dropdown yang dipilih.
        4.  **Logika:** `items` dari `DropdownButtonFormField` akan di-generate dari data `allSCsProvider` (gunakan `map` dan `toSet` untuk mendapatkan daftar kota/olahraga yang unik). `onChanged` akan meng-update state pilihan Anda. Tombol "Cari" akan membaca state pilihan tersebut.

*   **Task 3.3: Mengimplementasikan "Ubah Nomor Telepon"**
    *   **Masalah:** Fitur ini belum berfungsi karena memerlukan password.
    *   **Langkah Teknis:**
        1.  **Repository (`auth_repository.dart`):** Modifikasi `updateUserProfile`.
            ```dart
            // Tambahkan parameter password
            FutureEither<UserModel> updateUserProfile({required String name, String? phone, String? password}) async {
              try {
                await _account.updateName(name: name);
                if (phone != null && password != null) {
                  await _account.updatePhone(phone: phone, password: password);
                }
                final user = await _account.get();
                return right(UserModel.fromAppwriteUser(user));
              } ...
            }
            ```
        2.  **UI (`edit_profile_screen.dart`):** Di dalam method `_onSave`, jika `_phoneController.text` berbeda dari `widget.user.phone`, tampilkan `showDialog` yang meminta pengguna memasukkan password mereka.
        3.  **Controller (`profile_controller.dart`):** Modifikasi `updateUserProfile` untuk menerima dan meneruskan password opsional ke *repository*.

---

### **Sprint 4: Polish & Finalisasi**
**Tujuan:** Mengisi data dummy, membersihkan UI, dan mempersiapkan rilis.

*   **Task 4.1: Mengimplementasikan Dasbor Admin (Data Nyata)**
    *   **Masalah:** Dasbor admin masih menggunakan data dummy.
    *   **Langkah Teknis:**
        1.  Buat `SCAdminDashboardRepository` dan `SCAdminDashboardController`.
        2.  Di *repository*, buat method seperti `getTodaysBookingsCount(scId)` yang akan melakukan `listDocuments` pada collection `bookings` dengan `Query.equal('booking_date', ...)` dan `Query.equal('center_id', scId)`.
        3.  Di *controller*, buat `FutureProvider` untuk setiap data yang ingin ditampilkan.
        4.  Di `SCAdminDashboardScreen`, ganti nilai dummy dengan `ref.watch(...)` pada provider yang relevan.

*   **Task 4.2: Melanjutkan dari Rencana Iterasi 6 Anda**
    *   Lakukan pengujian menyeluruh untuk setiap alur.
    *   Perbaiki bug-bug kecil yang ditemukan.
    *   Pastikan semua UI terlihat baik di berbagai ukuran layar.
    *   Mulai proses build untuk Android/iOS.

---

Roadmap ini memberikan Anda serangkaian tugas yang jelas dan dapat dicapai, dimulai dari yang paling kritis. Fokuslah pada satu sprint pada satu waktu. Arsitektur Anda sudah sangat baik, jadi sebagian besar pekerjaan ini adalah tentang "menghubungkan kabel" yang sudah ada.

Saya siap membantu Anda di setiap langkah. Beri tahu saya tugas mana yang ingin Anda mulai, dan kita bisa membahasnya lebih detail. Mari kita selesaikan proyek ini
