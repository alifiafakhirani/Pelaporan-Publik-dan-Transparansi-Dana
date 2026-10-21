# Dokumen Functional Requirements (FR)

## Pelaporan Publik dan Transparansi Dana

Sistem Informasi Pelaporan Publik dan Transparansi Dana · Versi 1.0 (Draf)

Kelompok 10 : \[Alifiya Fakhirani Hermawan. Rian Fahmi , Ahmad Nurul, Abdurahman\]

· Mata kuliah: \[Analisis dan Perancangan Sistem Informasi\] · Tanggal: \[21 Oktober 2026\]

## 1. Pendahuluan

### 1.1 Tujuan

Dokumen ini memuat kebutuhan fungsional (Functional Requirements) sistem Pelaporan Publik dan Transparansi Dana. Ruang lingkupnya: pencatatan pemasukan dan pengeluaran, pengelolaan program yang didanai, pencatatan penyaluran dana, verifikasi transaksi, penyusunan laporan, dan publikasi informasi keuangan kepada publik.

### 1.2 Konvensi Penyajian

- Setiap kebutuhan diberi ID unik **FR-001** dan seterusnya, serta memuat 12 atribut: ID FR, nama fitur, deskripsi kebutuhan, aktor/role, data input, proses sistem, output, aturan validasi, kondisi awal, kondisi akhir, prioritas, dan acceptance criteria.

- Karena 12 kolom terlalu lebar untuk satu tabel pada halaman Word, setiap FR disajikan sebagai tabel vertikal (atribut → uraian). Bagian 3 memuat tabel ringkasan seluruh FR.

- Prioritas memakai skala MoSCoW: **Must Have**, **Should Have**, **Could Have**.

- Hal yang belum dikonfirmasi ditandai sebagai asumsi **AS-xx** (lihat Lampiran) dan dikonfirmasi kepada stakeholder pada tahap elicitation (wawancara).

### 1.3 Prinsip yang Berlaku pada Seluruh FR

1.  Publik hanya dapat membaca informasi; publik tidak dapat menambah, mengubah, atau menghapus data keuangan.

2.  Data internal dan data publik dipisahkan secara tegas (Bagian 2).

3.  Data pribadi dan dokumen sensitif penerima manfaat tidak ditampilkan kepada publik.

4.  Laporan tidak otomatis dipublikasikan; laporan baru tampil di publik setelah diverifikasi dan disetujui.

5.  Hanya transaksi berstatus Terverifikasi yang dapat masuk laporan final.

## 2. Klasifikasi Data Internal dan Data Publik

| **Data**                                                                                                  | **Internal**    | **Publik** | **Keterangan**                                           |
|-----------------------------------------------------------------------------------------------------------|-----------------|------------|----------------------------------------------------------|
| Transaksi berstatus Menunggu Verifikasi atau Ditolak                                                      | Ya              | Tidak      | Tidak masuk laporan final dan dashboard                  |
| Transaksi Terverifikasi dalam laporan terpublikasi (tanggal, kategori, program, nominal, keterangan umum) | Ya              | Ya         | Melalui rincian transaksi aman publik (FR-023)           |
| Bukti transaksi asli                                                                                      | Ya              | Tidak      | Versi publik hanya bila disamarkan dan disetujui (AS-11) |
| Data pribadi dan dokumen penerima manfaat                                                                 | Ya, sesuai role | Tidak      | Publik hanya melihat ringkasan teranonimkan              |
| Nama donatur                                                                                              | Ya              | Tidak      | Publik hanya bila donatur menyetujui (AS-12)             |
| Draf laporan, laporan Diajukan atau Ditolak                                                               | Ya              | Tidak      | Hanya laporan Dipublikasikan yang tampil                 |
| Laporan Dipublikasikan                                                                                    | Ya              | Ya         | Versi terbaru ditandai                                   |
| Riwayat perubahan data, akun pengguna, hak akses                                                          | Ya, sesuai role | Tidak      | Hanya baca bagi yang berhak                              |

## 3. Ringkasan Daftar Functional Requirements

| **ID FR** | **Nama fitur**                                   | **Aktor utama**                | **Prioritas** |
|-----------|--------------------------------------------------|--------------------------------|---------------|
| FR-001    | Login admin                                      | Pengguna internal              | Must Have     |
| FR-002    | Logout                                           | Pengguna internal              | Must Have     |
| FR-003    | Pengaturan hak akses berdasarkan role            | Administrator sistem           | Must Have     |
| FR-004    | Input dana masuk                                 | Staf keuangan                  | Must Have     |
| FR-005    | Edit data transaksi sesuai hak akses             | Staf keuangan, administrator   | Must Have     |
| FR-006    | Input dana keluar                                | Staf keuangan                  | Must Have     |
| FR-007    | Unggah bukti transaksi                           | Staf keuangan, staf program    | Must Have     |
| FR-008    | Verifikasi transaksi                             | Verifikator                    | Must Have     |
| FR-009    | Riwayat perubahan data                           | Sistem, administrator          | Must Have     |
| FR-010    | Tambah dan edit program                          | Staf program                   | Must Have     |
| FR-011    | Menghubungkan transaksi dengan program           | Staf keuangan, staf program    | Must Have     |
| FR-012    | Mencatat penyaluran dana                         | Staf program                   | Must Have     |
| FR-013    | Mengelola status program                         | Staf program                   | Should Have   |
| FR-014    | Membuat laporan pemasukan dan pengeluaran        | Staf keuangan                  | Must Have     |
| FR-015    | Menghitung saldo sesuai periode                  | Sistem                         | Must Have     |
| FR-016    | Menampilkan laporan per program                  | Staf keuangan, staf program    | Must Have     |
| FR-017    | Memfilter laporan berdasarkan periode (internal) | Pengguna internal              | Could Have    |
| FR-018    | Memverifikasi laporan                            | Verifikator, pihak berwenang   | Must Have     |
| FR-019    | Mempublikasikan dan memperbarui laporan          | Pihak berwenang, administrator | Must Have     |
| FR-020    | Ringkasan dana pada dashboard publik             | Publik                         | Must Have     |
| FR-021    | Daftar program pada dashboard publik             | Publik                         | Should Have   |
| FR-022    | Laporan yang sudah dipublikasikan                | Publik                         | Must Have     |
| FR-023    | Rincian transaksi yang aman untuk publik         | Publik                         | Must Have     |
| FR-024    | Pencarian dan filter laporan publik              | Publik                         | Should Have   |

## 4. Spesifikasi Functional Requirements

Peran pada dokumen ini: Administrator Sistem, Staf Keuangan, Staf Program, Verifikator, Pihak Berwenang, dan Publik (AS-01).

### A. Autentikasi dan Hak Akses

#### FR-001 Login Admin

| **Atribut**         | **Uraian**                                                                                                                                                                                                                                                    |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-001                                                                                                                                                                                                                                                        |
| Nama fitur          | Login admin                                                                                                                                                                                                                                                   |
| Deskripsi kebutuhan | Sistem mengautentikasi pengguna internal, termasuk admin, sebelum mengakses fitur pengelolaan.                                                                                                                                                                |
| Aktor/role          | Administrator Sistem, Staf Keuangan, Staf Program, Verifikator, Pihak Berwenang                                                                                                                                                                               |
| Data input          | Nama pengguna, kata sandi                                                                                                                                                                                                                                     |
| Proses sistem       | Memeriksa akun aktif, membandingkan hash kata sandi, membuat sesi, mencatat percobaan gagal, mengunci akun sementara bila batas terlampaui                                                                                                                    |
| Output              | Beranda sesuai role, atau pesan kesalahan umum                                                                                                                                                                                                                |
| Aturan validasi     | Nama pengguna dan kata sandi wajib diisi; akun berstatus aktif; akun terkunci 15 menit setelah 5 kali gagal berturut-turut (AS-03); pesan kesalahan tidak menyebut bagian mana yang salah                                                                     |
| Kondisi awal        | Akun sudah dibuat dan aktif; pengguna belum login                                                                                                                                                                                                             |
| Kondisi akhir       | Sesi aktif terbentuk dan login tercatat; atau akun terkunci                                                                                                                                                                                                   |
| Prioritas           | Must Have                                                                                                                                                                                                                                                     |
| Acceptance criteria | \(1\) Kredensial valid menampilkan beranda dalam maksimal 3 detik. (2) Kredensial salah menampilkan pesan umum dan tidak membuat sesi. (3) Percobaan gagal ke-5 mengunci akun selama 15 menit. (4) Pengguna tanpa login tidak dapat membuka halaman internal. |

#### FR-002 Logout

| **Atribut**         | **Uraian**                                                                                                                                                              |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-002                                                                                                                                                                  |
| Nama fitur          | Logout                                                                                                                                                                  |
| Deskripsi kebutuhan | Sistem mengakhiri sesi pengguna secara manual maupun otomatis ketika tidak ada aktivitas.                                                                               |
| Aktor/role          | Seluruh pengguna internal                                                                                                                                               |
| Data input          | Perintah keluar; atau inaktivitas 30 menit (AS-04)                                                                                                                      |
| Proses sistem       | Menghapus sesi, membatalkan token, mengarahkan ke halaman login, mencatat peristiwa logout                                                                              |
| Output              | Halaman login dan pesan konfirmasi                                                                                                                                      |
| Aturan validasi     | Hanya sesi aktif yang dapat diakhiri; formulir yang belum disimpan memunculkan peringatan sebelum keluar                                                                |
| Kondisi awal        | Pengguna sedang login                                                                                                                                                   |
| Kondisi akhir       | Sesi tidak berlaku; halaman internal tidak dapat dibuka kembali tanpa login                                                                                             |
| Prioritas           | Must Have                                                                                                                                                               |
| Acceptance criteria | \(1\) Setelah logout, membuka alamat halaman internal mengarahkan ke login. (2) Sesi berakhir otomatis setelah 30 menit tanpa aktivitas. (3) Peristiwa logout tercatat. |

#### FR-003 Pengaturan Hak Akses Berdasarkan Role

| **Atribut**         | **Uraian**                                                                                                                                                                                                         |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-003                                                                                                                                                                                                             |
| Nama fitur          | Pengaturan hak akses berdasarkan role                                                                                                                                                                              |
| Deskripsi kebutuhan | Administrator menetapkan role pada akun; sistem membatasi menu dan operasi sesuai role.                                                                                                                            |
| Aktor/role          | Administrator Sistem                                                                                                                                                                                               |
| Data input          | Data akun, role, status aktif/nonaktif                                                                                                                                                                             |
| Proses sistem       | Menyimpan penetapan role, memberlakukan matriks hak akses pada setiap permintaan, mencatat perubahan role                                                                                                          |
| Output              | Akun dengan role; penolakan akses untuk operasi di luar hak                                                                                                                                                        |
| Aturan validasi     | Setiap akun memiliki tepat satu role (AS-01); role admin terakhir tidak dapat dihapus atau dinonaktifkan; hanya admin yang dapat mengubah role; role Publik tidak memiliki akun dan hanya mengakses area publik    |
| Kondisi awal        | Pengguna login sebagai Administrator Sistem                                                                                                                                                                        |
| Kondisi akhir       | Hak akses berlaku pada akses berikutnya; perubahan tercatat                                                                                                                                                        |
| Prioritas           | Must Have                                                                                                                                                                                                          |
| Acceptance criteria | \(1\) Staf Program yang membuka menu verifikasi ditolak (100% pada skenario uji). (2) Perubahan role tercatat dengan pelaku dan waktu. (3) Publik tidak dapat menjalankan fungsi tambah, ubah, atau hapus apa pun. |

### B. Pengelolaan Data Keuangan

#### FR-004 Input Dana Masuk

| **Atribut**         | **Uraian**                                                                                                                                                                                   |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-004                                                                                                                                                                                       |
| Nama fitur          | Input dana masuk                                                                                                                                                                             |
| Deskripsi kebutuhan | Staf keuangan mencatat transaksi pemasukan dana. Pemasukan diinput manual (AS-15).                                                                                                           |
| Aktor/role          | Staf Keuangan                                                                                                                                                                                |
| Data input          | Tanggal, sumber dana, nominal (Rp), kategori, program tujuan (opsional), keterangan                                                                                                          |
| Proses sistem       | Memvalidasi data, membuat nomor transaksi unik, menyimpan berstatus Menunggu Verifikasi, mencatat riwayat                                                                                    |
| Output              | Transaksi tersimpan dengan nomor dan status                                                                                                                                                  |
| Aturan validasi     | Nominal angka lebih dari 0 dengan maksimal 2 desimal; tanggal tidak melebihi hari ini; sumber dan kategori wajib; program, bila diisi, berstatus aktif                                       |
| Kondisi awal        | Login sebagai Staf Keuangan; kategori pemasukan tersedia                                                                                                                                     |
| Kondisi akhir       | Pemasukan tersimpan berstatus Menunggu Verifikasi dan belum tampil di laporan final maupun publik                                                                                            |
| Prioritas           | Must Have                                                                                                                                                                                    |
| Acceptance criteria | \(1\) Nominal 0 atau negatif ditolak. (2) Tanggal esok hari ditolak. (3) Data valid menghasilkan nomor transaksi unik. (4) Pemasukan Menunggu Verifikasi tidak tampil pada dashboard publik. |

#### FR-005 Edit Data Transaksi Sesuai Hak Akses

| **Atribut**         | **Uraian**                                                                                                                                                                                                                          |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-005                                                                                                                                                                                                                              |
| Nama fitur          | Edit data transaksi sesuai hak akses                                                                                                                                                                                                |
| Deskripsi kebutuhan | Transaksi hanya dapat diubah oleh role yang berhak dan sesuai statusnya.                                                                                                                                                            |
| Aktor/role          | Staf Keuangan; Administrator Sistem (koreksi, AS-08)                                                                                                                                                                                |
| Data input          | Nomor transaksi, nilai baru, alasan perubahan                                                                                                                                                                                       |
| Proses sistem       | Memeriksa role dan status; menyimpan perubahan; transaksi Ditolak kembali menjadi Menunggu Verifikasi; transaksi Terverifikasi yang dikoreksi kembali menjadi Menunggu Verifikasi; menyimpan nilai lama dan baru pada riwayat       |
| Output              | Transaksi diperbarui                                                                                                                                                                                                                |
| Aturan validasi     | Alasan wajib (minimal 10 karakter); aturan validasi FR-004 atau FR-006 berlaku kembali; transaksi yang sudah masuk laporan terpublikasi tidak dapat diubah langsung dan hanya dikoreksi melalui revisi laporan (FR-019)             |
| Kondisi awal        | Transaksi ada; pengguna berhak atas transaksi tersebut                                                                                                                                                                              |
| Kondisi akhir       | Transaksi diperbarui, status Menunggu Verifikasi, riwayat tercatat                                                                                                                                                                  |
| Prioritas           | Must Have                                                                                                                                                                                                                           |
| Acceptance criteria | \(1\) Edit tanpa alasan ditolak. (2) Staf Program tidak dapat membuka formulir edit transaksi keuangan. (3) Setelah transaksi terverifikasi dikoreksi, status menjadi Menunggu Verifikasi dan riwayat memuat nilai lama serta baru. |

#### FR-006 Input Dana Keluar

| **Atribut**         | **Uraian**                                                                                                                                                                             |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-006                                                                                                                                                                                 |
| Nama fitur          | Input dana keluar                                                                                                                                                                      |
| Deskripsi kebutuhan | Staf keuangan mencatat pengeluaran dana, baik operasional maupun untuk program.                                                                                                        |
| Aktor/role          | Staf Keuangan                                                                                                                                                                          |
| Data input          | Tanggal, pihak penerima pembayaran, nominal (Rp), kategori, program terkait (opsional), keterangan                                                                                     |
| Proses sistem       | Memvalidasi data, membuat nomor transaksi unik, menyimpan berstatus Menunggu Verifikasi, mencatat riwayat                                                                              |
| Output              | Transaksi pengeluaran tersimpan dengan nomor dan status                                                                                                                                |
| Aturan validasi     | Nominal lebih dari 0; tanggal tidak melebihi hari ini; kategori wajib; program, bila diisi, berstatus aktif; bukti wajib sebelum transaksi dapat diajukan untuk verifikasi (FR-007)    |
| Kondisi awal        | Login sebagai Staf Keuangan                                                                                                                                                            |
| Kondisi akhir       | Pengeluaran tersimpan berstatus Menunggu Verifikasi                                                                                                                                    |
| Prioritas           | Must Have                                                                                                                                                                              |
| Acceptance criteria | \(1\) Pengeluaran tanpa bukti tidak dapat diajukan verifikasi. (2) Nominal tidak valid ditolak dengan pesan yang jelas. (3) Pengeluaran Menunggu Verifikasi tidak masuk laporan final. |

#### FR-007 Unggah Bukti Transaksi

| **Atribut**         | **Uraian**                                                                                                                                                |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-007                                                                                                                                                    |
| Nama fitur          | Unggah bukti transaksi                                                                                                                                    |
| Deskripsi kebutuhan | Pengguna berhak mengunggah berkas bukti dan menautkannya ke transaksi.                                                                                    |
| Aktor/role          | Staf Keuangan, Staf Program (bukti penyaluran)                                                                                                            |
| Data input          | Berkas, jenis bukti, nomor transaksi, penanda versi publik (opsional, AS-11)                                                                              |
| Proses sistem       | Memeriksa tipe dan ukuran, menyimpan pada penyimpanan terproteksi, menghitung checksum, menautkan ke transaksi                                            |
| Output              | Berkas tertaut dan dapat dipratinjau oleh pengguna internal                                                                                               |
| Aturan validasi     | Format PDF, JPG, atau PNG; maksimal 5 MB per berkas dan 5 berkas per transaksi (AS-02); nama berkas dinormalisasi; berkas tidak dapat diakses tanpa login |
| Kondisi awal        | Transaksi ada dan belum berstatus Terverifikasi                                                                                                           |
| Kondisi akhir       | Bukti tersimpan, hanya dapat dibuka pengguna internal berhak                                                                                              |
| Prioritas           | Must Have                                                                                                                                                 |
| Acceptance criteria | \(1\) Berkas .exe ditolak. (2) Berkas lebih dari 5 MB ditolak. (3) Alamat bukti tidak dapat dibuka tanpa login.                                           |

#### FR-008 Verifikasi Transaksi

| **Atribut**         | **Uraian**                                                                                                                                                                    |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-008                                                                                                                                                                        |
| Nama fitur          | Verifikasi transaksi                                                                                                                                                          |
| Deskripsi kebutuhan | Verifikator memeriksa kebenaran dan kelengkapan transaksi beserta bukti sebelum masuk laporan.                                                                                |
| Aktor/role          | Verifikator                                                                                                                                                                   |
| Data input          | Transaksi, keputusan (Terverifikasi atau Ditolak), catatan                                                                                                                    |
| Proses sistem       | Menampilkan data dan bukti, menyimpan keputusan, memperbarui status, mencatat pelaku dan waktu, memberi tahu pencatat bila ditolak                                            |
| Output              | Status transaksi diperbarui                                                                                                                                                   |
| Aturan validasi     | Alasan wajib saat Ditolak; transaksi tanpa bukti tidak dapat diverifikasi; verifikator tidak boleh sama dengan pencatat transaksi (AS-07)                                     |
| Kondisi awal        | Transaksi berstatus Menunggu Verifikasi dan bukti lengkap                                                                                                                     |
| Kondisi akhir       | Transaksi berstatus Terverifikasi atau Ditolak; keputusan tercatat                                                                                                            |
| Prioritas           | Must Have                                                                                                                                                                     |
| Acceptance criteria | \(1\) Penolakan tanpa alasan gagal. (2) Verifikator tidak dapat memverifikasi transaksi yang ia catat sendiri. (3) Hanya transaksi Terverifikasi yang tersedia untuk laporan. |

#### FR-009 Riwayat Perubahan Data

| **Atribut**         | **Uraian**                                                                                                                                                                                                  |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-009                                                                                                                                                                                                      |
| Nama fitur          | Riwayat perubahan data                                                                                                                                                                                      |
| Deskripsi kebutuhan | Sistem mencatat setiap perubahan data penting agar dapat ditelusuri.                                                                                                                                        |
| Aktor/role          | Sistem (otomatis); Administrator Sistem dan Pihak Berwenang (melihat)                                                                                                                                       |
| Data input          | Peristiwa tambah, ubah, hapus, verifikasi, persetujuan, publikasi; filter pencarian log                                                                                                                     |
| Proses sistem       | Menyimpan pelaku, waktu, objek, nilai lama, nilai baru, dan alasan pada log yang tidak dapat diubah                                                                                                         |
| Output              | Daftar riwayat yang dapat dicari menurut tanggal, pengguna, dan objek                                                                                                                                       |
| Aturan validasi     | Log bersifat hanya baca; tidak ada fungsi ubah atau hapus log; waktu memakai zona waktu server (AS-05)                                                                                                      |
| Kondisi awal        | Terjadi perubahan data penting; pengguna melihat riwayat berstatus berhak                                                                                                                                   |
| Kondisi akhir       | Satu entri log tersimpan per perubahan                                                                                                                                                                      |
| Prioritas           | Must Have                                                                                                                                                                                                   |
| Acceptance criteria | \(1\) Setiap edit transaksi menghasilkan satu entri berisi nilai lama dan baru. (2) Upaya mengubah atau menghapus log ditolak. (3) Pencarian log berdasarkan rentang tanggal menampilkan hasil yang sesuai. |

### C. Pengelolaan Program dan Penyaluran

#### FR-010 Tambah dan Edit Program

| **Atribut**         | **Uraian**                                                                                                                                                                               |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-010                                                                                                                                                                                   |
| Nama fitur          | Tambah dan edit program                                                                                                                                                                  |
| Deskripsi kebutuhan | Staf program membuat dan mengubah data program yang didanai.                                                                                                                             |
| Aktor/role          | Staf Program                                                                                                                                                                             |
| Data input          | Nama program, deskripsi, tanggal mulai, tanggal selesai, target dana, penanda tampil publik (AS-16)                                                                                      |
| Proses sistem       | Memvalidasi, menyimpan program berstatus Aktif, menyimpan perubahan, mencatat riwayat                                                                                                    |
| Output              | Program tersimpan dan tampil pada daftar program internal                                                                                                                                |
| Aturan validasi     | Nama unik, wajib, maksimal 150 karakter; tanggal selesai tidak lebih awal dari tanggal mulai; target lebih dari 0; perubahan periode atau target setelah ada transaksi memerlukan alasan |
| Kondisi awal        | Login sebagai Staf Program                                                                                                                                                               |
| Kondisi akhir       | Program tersimpan atau diperbarui dan tercatat pada riwayat                                                                                                                              |
| Prioritas           | Must Have                                                                                                                                                                                |
| Acceptance criteria | \(1\) Nama program kembar ditolak. (2) Tanggal selesai lebih awal dari tanggal mulai ditolak. (3) Program baru berstatus Aktif dan muncul pada pilihan program transaksi.                |

#### FR-011 Menghubungkan Transaksi dengan Program

| **Atribut**         | **Uraian**                                                                                                                                                                                      |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-011                                                                                                                                                                                          |
| Nama fitur          | Menghubungkan transaksi dengan program                                                                                                                                                          |
| Deskripsi kebutuhan | Transaksi pemasukan dan pengeluaran dapat ditautkan ke program agar dapat dilaporkan per program.                                                                                               |
| Aktor/role          | Staf Keuangan, Staf Program                                                                                                                                                                     |
| Data input          | Nomor transaksi, program                                                                                                                                                                        |
| Proses sistem       | Memeriksa status program dan transaksi, menyimpan tautan, menghitung ulang total dana program                                                                                                   |
| Output              | Transaksi tertaut ke program; total program diperbarui                                                                                                                                          |
| Aturan validasi     | Satu transaksi terhubung ke maksimal satu program (AS-10); program berstatus Selesai atau Nonaktif tidak menerima tautan baru; mengubah tautan transaksi terverifikasi melalui koreksi (FR-005) |
| Kondisi awal        | Transaksi dan program aktif tersedia                                                                                                                                                            |
| Kondisi akhir       | Tautan tersimpan dan total program konsisten dengan transaksi                                                                                                                                   |
| Prioritas           | Must Have                                                                                                                                                                                       |
| Acceptance criteria | \(1\) Menautkan ke program Nonaktif ditolak. (2) Total dana program sama dengan jumlah transaksi terhubung. (3) Perubahan tautan tercatat.                                                      |

#### FR-012 Mencatat Penyaluran Dana

| **Atribut**         | **Uraian**                                                                                                                                                                                                              |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-012                                                                                                                                                                                                                  |
| Nama fitur          | Mencatat penyaluran dana                                                                                                                                                                                                |
| Deskripsi kebutuhan | Staf program mencatat penyaluran dana dari program kepada penerima manfaat atau kegiatan program.                                                                                                                       |
| Aktor/role          | Staf Program                                                                                                                                                                                                            |
| Data input          | Program, kode penerima manfaat (opsional), tanggal, nominal (Rp), bentuk penyaluran, bukti                                                                                                                              |
| Proses sistem       | Memvalidasi, membuat catatan penyaluran dan transaksi pengeluaran jenis Penyaluran berstatus Menunggu Verifikasi, menautkan ke program                                                                                  |
| Output              | Catatan penyaluran tersimpan                                                                                                                                                                                            |
| Aturan validasi     | Program berstatus Aktif; nominal lebih dari 0 dan tidak melebihi dana terverifikasi yang tersedia pada program (kebijakan saldo minus perlu konfirmasi); bukti wajib; identitas penerima disimpan sebagai kode internal |
| Kondisi awal        | Login sebagai Staf Program; program aktif memiliki dana tersedia                                                                                                                                                        |
| Kondisi akhir       | Penyaluran tersimpan Menunggu Verifikasi dan tertaut ke program                                                                                                                                                         |
| Prioritas           | Must Have                                                                                                                                                                                                               |
| Acceptance criteria | \(1\) Penyaluran melebihi dana tersedia ditolak. (2) Penyaluran tanpa bukti tidak dapat diajukan verifikasi. (3) Nama dan identitas penerima tidak muncul pada tampilan publik.                                         |

#### FR-013 Mengelola Status Program

| **Atribut**         | **Uraian**                                                                                                                                                                                  |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-013                                                                                                                                                                                      |
| Nama fitur          | Mengelola status program                                                                                                                                                                    |
| Deskripsi kebutuhan | Staf program mengubah status program (Aktif, Selesai, Nonaktif).                                                                                                                            |
| Aktor/role          | Staf Program; Pihak Berwenang (membuka kembali program Selesai, AS-17)                                                                                                                      |
| Data input          | Program, status baru, alasan                                                                                                                                                                |
| Proses sistem       | Memeriksa aturan transisi, menyimpan status, mencatat riwayat                                                                                                                               |
| Output              | Status program diperbarui                                                                                                                                                                   |
| Aturan validasi     | Alasan wajib; program yang masih memiliki transaksi Menunggu Verifikasi tidak dapat ditandai Selesai; program Selesai tidak kembali Aktif tanpa persetujuan Pihak Berwenang (AS-17)         |
| Kondisi awal        | Program ada; pengguna berhak                                                                                                                                                                |
| Kondisi akhir       | Status baru berlaku dan tercatat                                                                                                                                                            |
| Prioritas           | Should Have                                                                                                                                                                                 |
| Acceptance criteria | \(1\) Perubahan tanpa alasan ditolak. (2) Program dengan transaksi menunggu verifikasi tidak dapat ditandai Selesai. (3) Program Nonaktif tidak muncul pada pilihan program transaksi baru. |

### D. Pelaporan

#### FR-014 Membuat Laporan Pemasukan dan Pengeluaran

| **Atribut**         | **Uraian**                                                                                                                                                                                                                                  |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-014                                                                                                                                                                                                                                      |
| Nama fitur          | Membuat laporan pemasukan dan pengeluaran                                                                                                                                                                                                   |
| Deskripsi kebutuhan | Staf keuangan menyusun draf laporan pemasukan, pengeluaran, atau gabungan untuk satu periode.                                                                                                                                               |
| Aktor/role          | Staf Keuangan                                                                                                                                                                                                                               |
| Data input          | Jenis laporan, periode awal, periode akhir, cakupan (keseluruhan atau program)                                                                                                                                                              |
| Proses sistem       | Mengambil hanya transaksi Terverifikasi pada periode, merekap per kategori, membentuk draf versi 1 berstatus Draf                                                                                                                           |
| Output              | Draf laporan berisi rekap per kategori dan total                                                                                                                                                                                            |
| Aturan validasi     | Periode wajib; tanggal akhir tidak lebih awal dari tanggal awal; rentang maksimal 12 bulan (AS-14); draf tanpa transaksi terverifikasi tidak dapat diajukan; periode tidak tumpang tindih dengan laporan final jenis sama pada cakupan sama |
| Kondisi awal        | Login sebagai Staf Keuangan; terdapat transaksi Terverifikasi pada periode                                                                                                                                                                  |
| Kondisi akhir       | Draf laporan tersimpan berstatus Draf; belum tampil di publik                                                                                                                                                                               |
| Prioritas           | Must Have                                                                                                                                                                                                                                   |
| Acceptance criteria | \(1\) Total pada draf sama dengan penjumlahan manual transaksi terverifikasi periode tersebut. (2) Transaksi Menunggu Verifikasi dan Ditolak tidak ikut terhitung. (3) Draf tanpa transaksi terverifikasi ditolak saat diajukan.            |

#### FR-015 Menghitung Saldo Sesuai Periode

| **Atribut**         | **Uraian**                                                                                                                                                                                                                                         |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-015                                                                                                                                                                                                                                             |
| Nama fitur          | Menghitung saldo sesuai periode                                                                                                                                                                                                                    |
| Deskripsi kebutuhan | Sistem menghitung saldo berdasarkan transaksi terverifikasi pada periode dan cakupan yang dipilih.                                                                                                                                                 |
| Aktor/role          | Sistem (dipicu oleh Staf Keuangan saat menyusun laporan)                                                                                                                                                                                           |
| Data input          | Periode, cakupan (keseluruhan atau program)                                                                                                                                                                                                        |
| Proses sistem       | Saldo akhir = saldo awal + total dana masuk terverifikasi − total dana keluar terverifikasi. Saldo awal adalah saldo akhir periode sebelumnya (AS-09)                                                                                              |
| Output              | Saldo awal, total masuk, total keluar, saldo akhir                                                                                                                                                                                                 |
| Aturan validasi     | Transaksi dihitung berdasarkan tanggal transaksi, bukan tanggal input; presisi 2 desimal; saldo negatif diberi tanda peringatan pada draf                                                                                                          |
| Kondisi awal        | Terdapat data transaksi terverifikasi; periode valid                                                                                                                                                                                               |
| Kondisi akhir       | Hasil perhitungan tersimpan pada draf laporan                                                                                                                                                                                                      |
| Prioritas           | Must Have                                                                                                                                                                                                                                          |
| Acceptance criteria | \(1\) Contoh: saldo awal Rp10.000.000, masuk Rp5.000.000, keluar Rp3.000.000 menghasilkan saldo akhir Rp12.000.000. (2) Perubahan periode menghasilkan saldo yang berbeda sesuai transaksi periode tersebut. (3) Saldo negatif ditandai pada draf. |

#### FR-016 Menampilkan Laporan per Program

| **Atribut**         | **Uraian**                                                                                                                                                                                             |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-016                                                                                                                                                                                                 |
| Nama fitur          | Menampilkan laporan per program                                                                                                                                                                        |
| Deskripsi kebutuhan | Sistem menyajikan rekap dana per program untuk periode terpilih.                                                                                                                                       |
| Aktor/role          | Staf Keuangan, Staf Program (melihat)                                                                                                                                                                  |
| Data input          | Program (satu atau semua), periode                                                                                                                                                                     |
| Proses sistem       | Merekap dana masuk tertaut, dana tersalurkan, sisa dana, dan persentase capaian target dari transaksi terverifikasi                                                                                    |
| Output              | Laporan per program; transaksi tanpa program ditampilkan sebagai Tidak Terkait Program                                                                                                                 |
| Aturan validasi     | Program harus ada; periode valid; hanya transaksi Terverifikasi                                                                                                                                        |
| Kondisi awal        | Terdapat program dan transaksi terverifikasi                                                                                                                                                           |
| Kondisi akhir       | Laporan per program tampil atau tersimpan sebagai draf                                                                                                                                                 |
| Prioritas           | Must Have                                                                                                                                                                                              |
| Acceptance criteria | \(1\) Jumlah seluruh laporan per program ditambah Tidak Terkait Program sama dengan total keseluruhan. (2) Sisa dana = dana masuk − dana tersalurkan. (3) Program tanpa transaksi menampilkan nilai 0. |

#### FR-017 Memfilter Laporan Berdasarkan Periode (Internal)

| **Atribut**         | **Uraian**                                                                                                                                                      |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-017                                                                                                                                                          |
| Nama fitur          | Memfilter laporan berdasarkan periode                                                                                                                           |
| Deskripsi kebutuhan | Pengguna internal menyaring daftar laporan menurut periode, program, dan status laporan.                                                                        |
| Aktor/role          | Seluruh pengguna internal                                                                                                                                       |
| Data input          | Tanggal awal, tanggal akhir, program, status laporan                                                                                                            |
| Proses sistem       | Menyaring daftar laporan semua status sesuai hak akses                                                                                                          |
| Output              | Daftar laporan sesuai kriteria dengan jumlah hasil                                                                                                              |
| Aturan validasi     | Tanggal valid; tanggal akhir tidak lebih awal dari tanggal awal                                                                                                 |
| Kondisi awal        | Pengguna login; terdapat laporan                                                                                                                                |
| Kondisi akhir       | Daftar hasil filter tampil; data tidak berubah                                                                                                                  |
| Prioritas           | Could Have                                                                                                                                                      |
| Acceptance criteria | \(1\) Hasil hanya memuat laporan yang periodenya berada dalam rentang filter. (2) Hasil kosong menampilkan pesan informatif. (3) Hasil tampil maksimal 3 detik. |

#### FR-018 Memverifikasi Laporan

| **Atribut**         | **Uraian**                                                                                                                                                    |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-018                                                                                                                                                        |
| Nama fitur          | Memverifikasi laporan                                                                                                                                         |
| Deskripsi kebutuhan | Draf laporan ditinjau Verifikator, lalu disetujui atau ditolak Pihak Berwenang sebelum dapat dipublikasikan (AS-06).                                          |
| Aktor/role          | Verifikator (tinjauan), Pihak Berwenang (persetujuan)                                                                                                         |
| Data input          | Laporan berstatus Diajukan, keputusan (Setuju atau Tolak), catatan                                                                                            |
| Proses sistem       | Menampilkan laporan dan data sumber, memeriksa kesesuaian total, menyimpan keputusan, memperbarui status, mencatat riwayat                                    |
| Output              | Laporan berstatus Disetujui atau Ditolak beserta catatan                                                                                                      |
| Aturan validasi     | Hanya laporan berstatus Diajukan yang dapat ditinjau; alasan wajib saat Ditolak; laporan ditolak kembali menjadi Draf; persetujuan hanya oleh Pihak Berwenang |
| Kondisi awal        | Draf laporan diajukan oleh Staf Keuangan                                                                                                                      |
| Kondisi akhir       | Laporan Disetujui (siap dipublikasikan) atau kembali ke Draf                                                                                                  |
| Prioritas           | Must Have                                                                                                                                                     |
| Acceptance criteria | \(1\) Laporan yang belum disetujui tidak dapat dipublikasikan. (2) Penolakan tanpa alasan gagal. (3) Setiap keputusan tercatat dengan pelaku dan waktu.       |

#### FR-019 Mempublikasikan dan Memperbarui Laporan

| **Atribut**         | **Uraian**                                                                                                                                                                                                                                                     |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-019                                                                                                                                                                                                                                                         |
| Nama fitur          | Mempublikasikan dan memperbarui laporan                                                                                                                                                                                                                        |
| Deskripsi kebutuhan | Laporan yang telah disetujui dipublikasikan ke dashboard publik; pembaruan dilakukan sebagai versi baru, dan laporan dapat ditarik bila diperlukan.                                                                                                            |
| Aktor/role          | Pihak Berwenang, Administrator Sistem (pelaksana teknis)                                                                                                                                                                                                       |
| Data input          | Laporan Disetujui, perintah publikasi; untuk pembaruan: versi baru dan catatan revisi; untuk penarikan: alasan                                                                                                                                                 |
| Proses sistem       | Mengubah status menjadi Dipublikasikan, menampilkan di area publik, menyimpan versi lama pada arsip internal, mencatat riwayat                                                                                                                                 |
| Output              | Laporan tampil di publik; versi dan tanggal publikasi tercatat                                                                                                                                                                                                 |
| Aturan validasi     | Hanya laporan berstatus Disetujui yang dapat dipublikasikan; laporan terpublikasi tidak diubah langsung; revisi wajib melalui FR-018 kembali; penarikan wajib beralasan                                                                                        |
| Kondisi awal        | Laporan berstatus Disetujui                                                                                                                                                                                                                                    |
| Kondisi akhir       | Laporan Dipublikasikan, atau versi baru menggantikan versi lama, atau laporan Ditarik                                                                                                                                                                          |
| Prioritas           | Must Have                                                                                                                                                                                                                                                      |
| Acceptance criteria | \(1\) Laporan tampil di dashboard publik dalam maksimal 1 menit setelah publikasi (AS-13). (2) Laporan Draf, Diajukan, dan Ditolak tidak tampil di publik. (3) Versi lama tersimpan pada arsip internal. (4) Laporan yang ditarik tidak lagi tampil di publik. |

### E. Dashboard Publik

Seluruh fitur pada kelompok ini bersifat hanya baca dan tidak memerlukan login.

#### FR-020 Menampilkan Ringkasan Dana Masuk, Dana Keluar, dan Saldo

| **Atribut**         | **Uraian**                                                                                                                                                                                                            |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-020                                                                                                                                                                                                                |
| Nama fitur          | Ringkasan dana masuk, dana keluar, dan saldo                                                                                                                                                                          |
| Deskripsi kebutuhan | Dashboard publik menampilkan ringkasan dana dari laporan yang sudah dipublikasikan.                                                                                                                                   |
| Aktor/role          | Publik                                                                                                                                                                                                                |
| Data input          | Pilihan periode (opsional); bawaan: periode laporan terpublikasi terbaru                                                                                                                                              |
| Proses sistem       | Mengambil angka dari laporan terpublikasi, bukan dari transaksi mentah, lalu menyusun ringkasan dan grafik                                                                                                            |
| Output              | Total dana masuk, total dana keluar, saldo, grafik tren, dan tanggal pembaruan terakhir                                                                                                                               |
| Aturan validasi     | Akses hanya baca; periode tanpa laporan terpublikasi menampilkan pesan informatif; tidak ada kontrol ubah data                                                                                                        |
| Kondisi awal        | Terdapat minimal satu laporan terpublikasi                                                                                                                                                                            |
| Kondisi akhir       | Ringkasan tampil; data tidak berubah                                                                                                                                                                                  |
| Prioritas           | Must Have                                                                                                                                                                                                             |
| Acceptance criteria | \(1\) Angka dashboard sama 100% dengan laporan terpublikasi periode yang sama. (2) Dashboard dimuat maksimal 3 detik untuk 100 pengguna bersamaan (AS-13). (3) Tidak ada tombol atau alamat yang dapat mengubah data. |

#### FR-021 Menampilkan Daftar Program

| **Atribut**         | **Uraian**                                                                                                                                                                                   |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-021                                                                                                                                                                                       |
| Nama fitur          | Daftar program                                                                                                                                                                               |
| Deskripsi kebutuhan | Publik melihat daftar program yang didanai beserta ringkasan dana dan statusnya.                                                                                                             |
| Aktor/role          | Publik                                                                                                                                                                                       |
| Data input          | Filter status program (opsional)                                                                                                                                                             |
| Proses sistem       | Menampilkan program yang ditandai tampil publik (AS-16) dengan angka dari laporan terpublikasi                                                                                               |
| Output              | Nama, deskripsi singkat, periode, status, target, dana masuk, dan dana tersalurkan per program                                                                                               |
| Aturan validasi     | Hanya program yang ditandai tampil publik; tidak memuat data penerima manfaat; angka hanya dari laporan terpublikasi                                                                         |
| Kondisi awal        | Terdapat program yang ditandai tampil publik                                                                                                                                                 |
| Kondisi akhir       | Daftar program tampil                                                                                                                                                                        |
| Prioritas           | Should Have                                                                                                                                                                                  |
| Acceptance criteria | \(1\) Program yang tidak ditandai tampil publik tidak muncul. (2) Dana per program sama dengan laporan per program yang terpublikasi. (3) Tidak ada nama atau data pribadi penerima manfaat. |

#### FR-022 Menampilkan Laporan yang Sudah Dipublikasikan

| **Atribut**         | **Uraian**                                                                                                                                               |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-022                                                                                                                                                   |
| Nama fitur          | Laporan yang sudah dipublikasikan                                                                                                                        |
| Deskripsi kebutuhan | Publik melihat dan mengunduh laporan yang telah dipublikasikan.                                                                                          |
| Aktor/role          | Publik                                                                                                                                                   |
| Data input          | Pilihan laporan                                                                                                                                          |
| Proses sistem       | Menampilkan daftar dan detail laporan berstatus Dipublikasikan, menandai versi terbaru, menyediakan unduhan                                              |
| Output              | Daftar laporan (judul, jenis, periode, versi, tanggal publikasi), tampilan detail, dan berkas unduhan (format PDF, perlu konfirmasi)                     |
| Aturan validasi     | Hanya laporan Dipublikasikan; laporan Ditarik tidak tampil; versi lama tidak diunduh dari area publik                                                    |
| Kondisi awal        | Terdapat laporan Dipublikasikan                                                                                                                          |
| Kondisi akhir       | Laporan tampil atau terunduh; data tidak berubah                                                                                                         |
| Prioritas           | Must Have                                                                                                                                                |
| Acceptance criteria | \(1\) Hanya laporan Dipublikasikan yang muncul. (2) Isi berkas unduhan sama dengan tampilan laporan. (3) Laporan terbaru ditandai sebagai versi terkini. |

#### FR-023 Menampilkan Rincian Transaksi yang Aman untuk Publik

| **Atribut**         | **Uraian**                                                                                                                                                                                      |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-023                                                                                                                                                                                          |
| Nama fitur          | Rincian transaksi yang aman untuk publik                                                                                                                                                        |
| Deskripsi kebutuhan | Publik melihat rincian transaksi terverifikasi yang termasuk laporan terpublikasi, tanpa data pribadi dan dokumen sensitif.                                                                     |
| Aktor/role          | Publik                                                                                                                                                                                          |
| Data input          | Pilihan laporan atau program; filter periode (opsional)                                                                                                                                         |
| Proses sistem       | Menampilkan transaksi Terverifikasi dalam laporan terpublikasi; menyaring kolom sensitif di sisi server sebelum dikirim ke peramban                                                             |
| Output              | Tanggal, kategori, program, nominal, dan keterangan umum; bukti hanya versi disamarkan yang disetujui (AS-11)                                                                                   |
| Aturan validasi     | Tidak menampilkan nama donatur (AS-12), nama atau identitas penerima manfaat, nomor rekening, alamat, maupun dokumen asli; transaksi dalam laporan belum terpublikasi tidak tampil              |
| Kondisi awal        | Terdapat laporan terpublikasi berisi transaksi terverifikasi                                                                                                                                    |
| Kondisi akhir       | Rincian aman tampil; data tidak berubah                                                                                                                                                         |
| Prioritas           | Must Have                                                                                                                                                                                       |
| Acceptance criteria | \(1\) Pada uji seluruh data, 0 kolom data pribadi muncul pada respons publik. (2) Transaksi Menunggu Verifikasi atau Ditolak tidak muncul. (3) Mengakses alamat bukti asli tanpa login ditolak. |

#### FR-024 Menyediakan Pencarian dan Filter Laporan

| **Atribut**         | **Uraian**                                                                                                                                                                                                    |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID FR               | FR-024                                                                                                                                                                                                        |
| Nama fitur          | Pencarian dan filter laporan publik                                                                                                                                                                           |
| Deskripsi kebutuhan | Publik mencari dan menyaring laporan terpublikasi menurut kata kunci, periode, program, dan jenis laporan.                                                                                                    |
| Aktor/role          | Publik                                                                                                                                                                                                        |
| Data input          | Kata kunci, periode, program, jenis laporan                                                                                                                                                                   |
| Proses sistem       | Menyanitasi masukan, menyaring laporan Dipublikasikan, membagi hasil per halaman (10 per halaman)                                                                                                             |
| Output              | Daftar hasil beserta jumlah hasil                                                                                                                                                                             |
| Aturan validasi     | Kata kunci maksimal 100 karakter dan disanitasi; tanggal valid; tanggal akhir tidak lebih awal dari tanggal awal                                                                                              |
| Kondisi awal        | Terdapat laporan terpublikasi                                                                                                                                                                                 |
| Kondisi akhir       | Hasil tampil; data tidak berubah                                                                                                                                                                              |
| Prioritas           | Should Have                                                                                                                                                                                                   |
| Acceptance criteria | \(1\) Hasil hanya memuat laporan yang memenuhi semua filter. (2) Laporan belum terpublikasi tidak pernah muncul pada hasil. (3) Hasil tampil maksimal 3 detik. (4) Hasil kosong menampilkan pesan informatif. |

## Lampiran. Daftar Asumsi yang Perlu Dikonfirmasi

Asumsi berikut disusun berdasarkan ruang lingkup proyek, bukan hasil wawancara, dan perlu dikonfirmasi kepada stakeholder.

| **Kode** | **Asumsi**                                                                                                                             | **Terkait**    |
|----------|----------------------------------------------------------------------------------------------------------------------------------------|----------------|
| AS-01    | Role terdiri atas Administrator Sistem, Staf Keuangan, Staf Program, Verifikator, dan Pihak Berwenang; setiap akun memiliki satu role. | FR-001, FR-003 |
| AS-02    | Bukti berformat PDF, JPG, atau PNG, maksimal 5 MB per berkas dan 5 berkas per transaksi.                                               | FR-007         |
| AS-03    | Akun terkunci 15 menit setelah 5 kali gagal login berturut-turut.                                                                      | FR-001         |
| AS-04    | Sesi berakhir setelah 30 menit tanpa aktivitas.                                                                                        | FR-002         |
| AS-05    | Mata uang Rupiah dan zona waktu WIB.                                                                                                   | FR-004, FR-009 |
| AS-06    | Laporan memerlukan satu tingkat persetujuan Pihak Berwenang setelah ditinjau Verifikator.                                              | FR-018         |
| AS-07    | Pencatat dan verifikator suatu transaksi tidak boleh orang yang sama.                                                                  | FR-008         |
| AS-08    | Transaksi Terverifikasi tidak diubah langsung; koreksi mengembalikannya ke Menunggu Verifikasi.                                        | FR-005         |
| AS-09    | Saldo awal periode adalah saldo akhir terverifikasi periode sebelumnya; nilai saldo awal pertama perlu dikonfirmasi.                   | FR-015         |
| AS-10    | Satu transaksi terhubung ke maksimal satu program.                                                                                     | FR-011         |
| AS-11    | Bukti asli tidak ditampilkan di publik; hanya versi disamarkan yang disetujui.                                                         | FR-007, FR-023 |
| AS-12    | Nama donatur tidak ditampilkan di publik kecuali donatur menyetujui.                                                                   | FR-023         |
| AS-13    | Target waktu: dashboard dimuat 3 detik untuk 100 pengguna bersamaan; laporan tampil di publik dalam 1 menit setelah publikasi.         | FR-019, FR-020 |
| AS-14    | Rentang maksimal satu laporan adalah 12 bulan.                                                                                         | FR-014         |
| AS-15    | Data pemasukan diinput manual; integrasi dengan modul donasi belum ditetapkan.                                                         | FR-004         |
| AS-16    | Program tampil di publik apabila ditandai oleh Staf Program; kebutuhan persetujuan program belum ditentukan.                           | FR-010, FR-021 |
| AS-17    | Program berstatus Selesai tidak dapat kembali Aktif tanpa persetujuan Pihak Berwenang.                                                 | FR-013         |
