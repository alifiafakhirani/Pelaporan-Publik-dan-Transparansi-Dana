# Software Requirements Specification (SRS)

## Pelaporan Publik dan Transparansi Dana

Subsistem Aplikasi Pengelolaan Donasi · Mengacu pada ISO/IEC/IEEE 29148 · Versi 1.0 (Draf)

Kelompok: \[Alifiya Fakhirani Hermawan , Rian Fahmi , Ahmad Nurul , Abdurahman\]

Mata kuliah: \[Analisis dan Perancangan Sistem Informasi\] · Tanggal: \[21 Oktober 2026\]

**Konvensi dokumen.** Informasi yang belum dikonfirmasi ditandai sebagai asumsi dengan kode **A-xx** atau pertanyaan untuk stakeholder dengan kode **Q-xx**. Kode kebutuhan: **FR-xxx** (fungsional), **NFR-xxx** (nonfungsional), **BR-xx** (aturan bisnis), **UC-xx** (use case).

## 1. Pendahuluan

### 1.1 Tujuan Dokumen

Dokumen ini menetapkan kebutuhan perangkat lunak untuk subsistem Pelaporan Publik dan Transparansi Dana. Dokumen menjadi acuan bersama bagi anggota kelompok, dosen pembimbing, dan pihak yang berkepentingan dalam perancangan, pengembangan, pengujian, dan penerimaan sistem.

### 1.2 Ruang Lingkup Sistem

Subsistem ini menyajikan informasi dana yang transparan kepada publik, mencakup pemasukan, pengeluaran, saldo berjalan, program yang didanai, penyaluran dana, penerima manfaat, bukti transaksi, dan laporan yang dapat diakses publik.

**Termasuk dalam lingkup:**

- Autentikasi dan pengaturan hak akses pengguna internal.

- Pengelolaan data pemasukan, pengeluaran, program, penyaluran dana, dan penerima manfaat sesuai kebutuhan.

- Verifikasi transaksi, penyusunan laporan, persetujuan, dan publikasi laporan.

- Dashboard transparansi, riwayat transaksi, bukti transaksi, serta pencarian dan filter laporan.

- Pengaduan atau pertanyaan publik (**A-01**: dimasukkan sebagai fitur tentatif, menunggu kesepakatan lingkup, lihat **Q-01**).

**Di luar lingkup:** pembayaran dan pengumpulan donasi oleh donatur (menjadi tanggung jawab modul donasi lain), penghitungan zakat, pembuatan akuntansi lengkap (jurnal, neraca), dan fitur lain yang tidak disebutkan di atas.

### 1.3 Definisi, Akronim, dan Istilah

| **Istilah**      | **Definisi**                                                                                                     |
|------------------|------------------------------------------------------------------------------------------------------------------|
| SRS              | Software Requirements Specification, dokumen spesifikasi kebutuhan perangkat lunak                               |
| FR / NFR / BR    | Functional Requirement / Non-Functional Requirement / Business Rule                                              |
| Pemasukan        | Dana yang diterima organisasi, termasuk donasi                                                                   |
| Pengeluaran      | Dana yang dikeluarkan organisasi, baik untuk program maupun operasional                                          |
| Penyaluran       | Pengeluaran dana yang diberikan kepada program atau penerima manfaat                                             |
| Penerima manfaat | Individu atau kelompok yang menerima bantuan dari program                                                        |
| Verifikasi       | Pemeriksaan kelengkapan dan kebenaran transaksi sebelum dipakai dalam laporan final                              |
| Saldo berjalan   | Total dana masuk terverifikasi dikurangi total dana keluar terverifikasi pada ruang lingkup dan periode tertentu |
| Bukti transaksi  | Berkas pendukung transaksi, misalnya bukti transfer atau kuitansi                                                |
| Pihak berwenang  | Pihak yang berhak menyetujui publikasi laporan (**Q-02**: jabatan konkret perlu dikonfirmasi)                    |
| Audit trail      | Catatan penelusuran perubahan data penting                                                                       |
| RTM              | Requirement Traceability Matrix                                                                                  |

### 1.4 Referensi

1.  ISO/IEC/IEEE 29148:2018, *Systems and Software Engineering: Life Cycle Processes: Requirements Engineering*.

2.  Undang-Undang Nomor 27 Tahun 2022 tentang Pelindungan Data Pribadi.

3.  Dokumen proyek aplikasi pengelolaan donasi (induk) \[isi apabila tersedia\].

4.  Catatan perkuliahan dan arahan dosen pembimbing \[isi apabila tersedia\].

## 2. Gambaran Umum Sistem

### 2.1 Latar Belakang

Organisasi pengelola donasi dituntut akuntabel kepada donatur dan masyarakat. Keterbukaan informasi penggunaan dana meningkatkan kepercayaan publik. Aplikasi pengelolaan donasi memerlukan subsistem khusus yang mengubah data keuangan internal menjadi informasi publik yang terverifikasi, mudah ditelusuri, dan tetap melindungi data pribadi.

### 2.2 Permasalahan yang Ingin Diselesaikan

Bagian ini berdasarkan topik proyek dan **belum dikonfirmasi melalui wawancara** (**A-02**):

1.  Donatur dan publik sulit memantau penggunaan dana secara berkala.

2.  Pencatatan dana berpotensi tidak seragam dan sulit ditelusuri tanpa sistem terpusat.

3.  Laporan berpotensi dipublikasikan tanpa verifikasi dan persetujuan yang jelas.

4.  Data pribadi penerima manfaat berisiko terbuka apabila tidak ada kontrol publikasi.

### 2.3 Tujuan Pengembangan

1.  Menyediakan dashboard dan laporan dana yang dapat diakses publik.

2.  Memastikan hanya data terverifikasi yang tampil pada laporan final.

3.  Menyediakan alur persetujuan sebelum publikasi.

4.  Melindungi data pribadi dan menjaga keterlacakan perubahan data.

### 2.4 Batasan Sistem

- Sistem berbasis web (**A-03**) dan terhubung dengan modul donasi melalui impor atau antarmuka yang akan ditentukan (**Q-03**).

- Sistem tidak memproses pembayaran dan tidak menghitung zakat.

- Kebijakan organisasi (misalnya tingkat persetujuan, batas nominal, kebijakan privasi) mengikuti hasil konfirmasi stakeholder.

- Bahasa antarmuka: Bahasa Indonesia (**A-04**).

### 2.5 Karakteristik Pengguna

| **Kelompok pengguna** | **Karakteristik**                               | **Tingkat keahlian teknis** |
|-----------------------|-------------------------------------------------|-----------------------------|
| Administrator sistem  | Mengelola akun dan hak akses                    | Menengah–tinggi             |
| Staf keuangan         | Mencatat pemasukan dan pengeluaran              | Menengah                    |
| Staf program          | Mengelola program, penyaluran, penerima manfaat | Menengah                    |
| Verifikator           | Memeriksa transaksi dan bukti                   | Menengah                    |
| Pihak berwenang       | Menyetujui laporan                              | Dasar–menengah              |
| Publik/donatur        | Membaca laporan, tanpa login                    | Dasar                       |

## 3. Analisis Stakeholder

### 3.1 Stakeholder Internal dan Eksternal

- **Internal:** pimpinan organisasi, staf keuangan, staf program, verifikator, administrator sistem.

- **Eksternal:** donatur, masyarakat umum, penerima manfaat, auditor atau pengawas eksternal (**Q-04**: apakah ada), pengembang modul donasi (sistem induk).

### 3.2 Stakeholder Register

Nama stakeholder ditulis sebagai peran karena nama individu belum tersedia. Penilaian kepentingan dan pengaruh merupakan **estimasi awal tim** (**A-05**) yang perlu divalidasi.

| **ID** | **Nama (peran)**           | **Peran dalam sistem**                     | **Kepentingan**                       | **Pengaruh** |
|--------|----------------------------|--------------------------------------------|---------------------------------------|--------------|
| SH-01  | Pimpinan/pihak berwenang   | Menyetujui laporan dan kebijakan publikasi | Akuntabilitas dan reputasi organisasi | Tinggi       |
| SH-02  | Staf keuangan              | Mencatat pemasukan dan pengeluaran         | Kemudahan dan akurasi pencatatan      | Sedang       |
| SH-03  | Staf program               | Mengelola program dan penyaluran           | Pelaporan program yang sederhana      | Sedang       |
| SH-04  | Verifikator                | Memverifikasi transaksi                    | Kejelasan kriteria verifikasi         | Sedang       |
| SH-05  | Administrator sistem       | Mengelola akun dan keamanan                | Stabilitas dan keamanan sistem        | Sedang       |
| SH-06  | Donatur                    | Memantau penggunaan dana                   | Transparansi penggunaan donasi        | Sedang       |
| SH-07  | Masyarakat umum            | Mengakses informasi publik                 | Informasi mudah dipahami              | Rendah       |
| SH-08  | Penerima manfaat           | Subjek data program                        | Privasi dan perlindungan data         | Rendah       |
| SH-09  | Auditor/pengawas eksternal | Memeriksa kepatuhan                        | Keterlacakan data                     | Sedang       |
| SH-10  | Pengembang modul donasi    | Penyedia data pemasukan                    | Kompatibilitas integrasi              | Sedang       |

### 3.3 Power/Interest Grid

quadrantChart  
title Power/Interest Grid  
x-axis Kepentingan Rendah --\> Kepentingan Tinggi  
y-axis Pengaruh Rendah --\> Pengaruh Tinggi  
quadrant-1 Manage Closely  
quadrant-2 Keep Satisfied  
quadrant-3 Monitor  
quadrant-4 Keep Informed  
Pimpinan: \[0.9, 0.9\]  
Staf Keuangan: \[0.8, 0.6\]  
Staf Program: \[0.7, 0.55\]  
Verifikator: \[0.75, 0.6\]  
Admin Sistem: \[0.6, 0.55\]  
Auditor: \[0.5, 0.65\]  
Pengembang Modul Donasi: \[0.45, 0.6\]  
Donatur: \[0.8, 0.4\]  
Penerima Manfaat: \[0.7, 0.2\]  
Masyarakat: \[0.4, 0.2\]

| **Kuadran**                                      | **Stakeholder**            | **Pendekatan**                             |
|--------------------------------------------------|----------------------------|--------------------------------------------|
| Manage Closely (pengaruh dan kepentingan tinggi) | SH-01, SH-02, SH-03, SH-04 | Libatkan aktif dalam pengambilan keputusan |
| Keep Satisfied                                   | SH-09, SH-10, SH-05        | Konsultasi dan jaga kepuasan               |
| Keep Informed                                    | SH-06, SH-08               | Informasikan secara berkala                |
| Monitor                                          | SH-07                      | Pantau umpan balik                         |

### 3.4 RACI Matrix

R = Responsible, A = Accountable, C = Consulted, I = Informed. Pembagian ini merupakan **usulan awal** (**A-06**).

| **Aktivitas**                    | **Pimpinan** | **Keuangan** | **Program** | **Verifikator** | **Admin Sistem** | **Publik** |
|----------------------------------|--------------|--------------|-------------|-----------------|------------------|------------|
| Mencatat pemasukan               | I            | R/A          | I           | C               | –                | –          |
| Mencatat pengeluaran             | I            | R/A          | C           | C               | –                | –          |
| Mengelola program                | A            | C            | R           | I               | –                | –          |
| Mencatat penyaluran dana         | I            | C            | R/A         | C               | –                | –          |
| Verifikasi transaksi             | I            | C            | C           | R/A             | –                | –          |
| Menyusun laporan                 | I            | R            | C           | C               | –                | –          |
| Menyetujui dan publikasi laporan | A/R          | C            | I           | C               | R (teknis)       | I          |
| Mengelola akun dan hak akses     | A            | I            | I           | I               | R                | –          |
| Menanggapi pengaduan publik      | A            | C            | R           | C               | –                | I          |

### 3.5 Strategi Komunikasi dan Engagement

| **Stakeholder**                     | **Strategi**                                    | **Media**             | **Frekuensi**            |
|-------------------------------------|-------------------------------------------------|-----------------------|--------------------------|
| Pimpinan                            | Pelibatan aktif, validasi kebijakan dan lingkup | Rapat, demo           | Setiap tahap/iterasi     |
| Staf keuangan, program, verifikator | Wawancara kebutuhan, uji coba prototipe         | Wawancara, workshop   | Awal dan tiap iterasi    |
| Admin sistem                        | Konsultasi teknis dan keamanan                  | Diskusi teknis        | Sesuai kebutuhan         |
| Pengembang modul donasi             | Koordinasi format dan antarmuka data            | Dokumen antarmuka     | Awal proyek              |
| Donatur dan masyarakat              | Pemberitahuan publikasi, kanal umpan balik      | Dashboard, pengumuman | Setiap publikasi laporan |
| Penerima manfaat                    | Penjelasan kebijakan privasi                    | Informasi tertulis    | Saat pendataan           |

## 4. Deskripsi Proses Bisnis

Proses berikut merupakan **rancangan usulan** berdasarkan lingkup proyek dan perlu divalidasi stakeholder (**Q-05**).

### 4.1 Pencatatan Dana Masuk

1.  Staf keuangan menerima data dana masuk (impor dari modul donasi atau input manual).

2.  Staf keuangan melengkapi tanggal, sumber, nominal, kategori, dan bukti.

3.  Sistem memvalidasi data dan menyimpan dengan status **Menunggu Verifikasi**.

### 4.2 Pencatatan Pengeluaran

1.  Staf keuangan mencatat tanggal, nominal, kategori, penerima pembayaran, program terkait, dan bukti.

2.  Sistem memvalidasi dan menyimpan dengan status **Menunggu Verifikasi**.

### 4.3 Pengelolaan Program

1.  Staf program membuat program (nama, deskripsi, periode, target dana, status).

2.  Program dapat diubah, dinonaktifkan, atau diselesaikan. Perubahan penting tercatat pada audit trail.

### 4.4 Penyaluran Dana

1.  Staf program memilih program dan penerima manfaat (apabila relevan).

2.  Staf program mencatat nominal, tanggal, dan bukti penyaluran.

3.  Sistem mencatat penyaluran sebagai pengeluaran program berstatus **Menunggu Verifikasi**.

### 4.5 Verifikasi Transaksi

1.  Verifikator memeriksa data dan bukti transaksi.

2.  Verifikator memilih **Terverifikasi** atau **Ditolak** (disertai alasan).

3.  Transaksi ditolak dikembalikan kepada pencatat untuk diperbaiki.

### 4.6 Penyusunan dan Publikasi Laporan

1.  Staf keuangan menentukan periode dan ruang lingkup (keseluruhan atau per program).

2.  Sistem menyusun draf laporan hanya dari transaksi terverifikasi dan menghitung saldo.

3.  Verifikator meninjau draf, lalu pihak berwenang menyetujui atau menolak.

4.  Setelah disetujui, administrator atau sistem memublikasikan laporan ke dashboard publik.

### 4.7 Alur Proses Bisnis End-to-End

flowchart TD  
A\[Dana masuk diterima\] --\> B\[Staf keuangan mencatat pemasukan\]  
P\[Staf program mengelola program\] --\> D\[Staf program mencatat penyaluran dana\]  
B --\> C\[Status: Menunggu Verifikasi\]  
E\[Staf keuangan mencatat pengeluaran\] --\> C  
D --\> C  
C --\> F{Verifikator memeriksa data dan bukti}  
F -- Ditolak --\> G\[Dikembalikan untuk perbaikan\]  
G --\> C  
F -- Terverifikasi --\> H\[Transaksi masuk basis data terverifikasi\]  
H --\> I\[Staf keuangan menyusun draf laporan periode\]  
I --\> J\[Sistem menghitung saldo dan membentuk draf\]  
J --\> K{Pihak berwenang menyetujui?}  
K -- Ditolak --\> L\[Revisi draf laporan\]  
L --\> I  
K -- Disetujui --\> M\[Laporan dipublikasikan\]  
M --\> N\[Dashboard publik menampilkan laporan\]  
N --\> O\[Publik mengakses, mencari, dan mengunduh laporan\]

## 5. Kebutuhan Fungsional (Functional Requirements)

Setiap kebutuhan memuat nama fitur, deskripsi, aktor, input, proses, output, aturan validasi, dan kriteria penerimaan. Peran pengguna mengikuti Bagian 2.5 dan 8.1.

### FR-001 Login dan Hak Akses

| **Atribut**         | **Uraian**                                                                                                                                                  |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Nama fitur          | Login dan pengelolaan hak akses                                                                                                                             |
| Deskripsi           | Sistem mengautentikasi pengguna internal dan membatasi fitur berdasarkan peran.                                                                             |
| Aktor               | Administrator sistem, staf keuangan, staf program, verifikator, pihak berwenang                                                                             |
| Input               | Nama pengguna, kata sandi; data akun dan peran (oleh administrator)                                                                                         |
| Proses              | Memeriksa kredensial, membuat sesi, menerapkan hak akses per peran, mengunci akun setelah percobaan gagal berulang                                          |
| Output              | Akses ke menu sesuai peran atau pesan kesalahan                                                                                                             |
| Aturan validasi     | Nama pengguna unik; kata sandi memenuhi kebijakan kompleksitas; akun dikunci sementara setelah 5 kali gagal berturut-turut (**A-07**)                       |
| Kriteria penerimaan | Pengguna dengan kredensial valid berhasil masuk dan hanya melihat menu perannya; akses ke halaman di luar peran ditolak; akun terkunci setelah 5 kali gagal |

### FR-002 Pengelolaan Data Pemasukan

| **Atribut**         | **Uraian**                                                                                                                                                                                    |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Nama fitur          | Pengelolaan data pemasukan                                                                                                                                                                    |
| Deskripsi           | Mencatat, melihat, mengubah, dan membatalkan data dana masuk.                                                                                                                                 |
| Aktor               | Staf keuangan                                                                                                                                                                                 |
| Input               | Tanggal, sumber dana, nominal, kategori, keterangan, berkas bukti, program tujuan (opsional)                                                                                                  |
| Proses              | Validasi data, simpan dengan status Menunggu Verifikasi, catat pada audit trail                                                                                                               |
| Output              | Data pemasukan tersimpan dan tampil pada daftar pemasukan                                                                                                                                     |
| Aturan validasi     | Nominal lebih dari nol; tanggal tidak melebihi tanggal hari ini; bukti berformat PDF/JPG/PNG dengan ukuran maksimum 5 MB (**A-07**); data berstatus Terverifikasi tidak dapat diubah langsung |
| Kriteria penerimaan | Data valid tersimpan berstatus Menunggu Verifikasi; data tidak valid ditolak dengan pesan yang jelas; ubah data terverifikasi diarahkan ke mekanisme koreksi dan tercatat                     |

### FR-003 Pengelolaan Data Pengeluaran

| **Atribut**         | **Uraian**                                                                                                              |
|---------------------|-------------------------------------------------------------------------------------------------------------------------|
| Nama fitur          | Pengelolaan data pengeluaran                                                                                            |
| Deskripsi           | Mencatat, melihat, mengubah, dan membatalkan data dana keluar (program maupun operasional).                             |
| Aktor               | Staf keuangan                                                                                                           |
| Input               | Tanggal, nominal, kategori, pihak penerima pembayaran, program terkait (opsional), keterangan, berkas bukti             |
| Proses              | Validasi data, simpan dengan status Menunggu Verifikasi, catat pada audit trail                                         |
| Output              | Data pengeluaran tersimpan dan tampil pada daftar pengeluaran                                                           |
| Aturan validasi     | Nominal lebih dari nol; bukti wajib dilampirkan; program terkait harus berstatus aktif; aturan ubah data seperti FR-002 |
| Kriteria penerimaan | Pengeluaran tanpa bukti ditolak; data valid tersimpan berstatus Menunggu Verifikasi; perubahan tercatat                 |

### FR-004 Pengelolaan Data Program

| **Atribut**         | **Uraian**                                                                                                                                             |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| Nama fitur          | Pengelolaan data program                                                                                                                               |
| Deskripsi           | Mengelola program yang didanai beserta statusnya.                                                                                                      |
| Aktor               | Staf program; pihak berwenang (persetujuan, apabila disyaratkan, **Q-06**)                                                                             |
| Input               | Nama program, deskripsi, periode, target dana, status                                                                                                  |
| Proses              | Validasi, simpan, ubah status (Aktif, Selesai, Nonaktif), catat pada audit trail                                                                       |
| Output              | Daftar dan detail program                                                                                                                              |
| Aturan validasi     | Nama program unik; tanggal selesai tidak lebih awal dari tanggal mulai; program yang sudah memiliki transaksi tidak dapat dihapus, hanya dinonaktifkan |
| Kriteria penerimaan | Program valid tersimpan; penghapusan program bertransaksi ditolak; perubahan status tercatat                                                           |

### FR-005 Pengelolaan Data Penyaluran Dana

| **Atribut**         | **Uraian**                                                                                                                                                          |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Nama fitur          | Pengelolaan data penyaluran dana                                                                                                                                    |
| Deskripsi           | Mencatat penyaluran dana kepada program dan/atau penerima manfaat.                                                                                                  |
| Aktor               | Staf program                                                                                                                                                        |
| Input               | Program, penerima manfaat (opsional), tanggal, nominal, bentuk penyaluran, berkas bukti                                                                             |
| Proses              | Validasi, simpan sebagai transaksi pengeluaran berstatus Menunggu Verifikasi, tautkan ke program                                                                    |
| Output              | Data penyaluran tersimpan                                                                                                                                           |
| Aturan validasi     | Program wajib dipilih; nominal lebih dari nol; bukti wajib; nominal tidak melebihi saldo terverifikasi program/dana yang tersedia (**Q-07**: kebijakan saldo minus) |
| Kriteria penerimaan | Penyaluran valid tersimpan dan terhubung ke program; penyaluran melebihi saldo yang tersedia ditolak sesuai kebijakan                                               |

### FR-006 Pengelolaan Data Penerima Manfaat (Sesuai Kebutuhan)

| **Atribut**         | **Uraian**                                                                                                                                                                                            |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Nama fitur          | Pengelolaan data penerima manfaat                                                                                                                                                                     |
| Deskripsi           | Mengelola data penerima manfaat seminimal mungkin untuk keperluan pertanggungjawaban penyaluran.                                                                                                      |
| Aktor               | Staf program                                                                                                                                                                                          |
| Input               | Kode penerima, nama atau inisial, kategori, wilayah (tingkat umum), status persetujuan publikasi                                                                                                      |
| Proses              | Validasi, simpan, tetapkan atribut yang boleh dipublikasikan                                                                                                                                          |
| Output              | Daftar penerima manfaat (internal) dan versi teranonimkan (publik)                                                                                                                                    |
| Aturan validasi     | Hanya data yang diperlukan yang dikumpulkan (prinsip minimisasi); data pribadi tampil publik hanya bila ada dasar dan otorisasi (BR-04); kebutuhan data konkret mengikuti hasil konfirmasi (**Q-08**) |
| Kriteria penerimaan | Tampilan publik tidak memuat data pribadi tanpa otorisasi; data internal hanya dapat dilihat peran berwenang                                                                                          |

### FR-007 Verifikasi Transaksi

| **Atribut**         | **Uraian**                                                                                                                                                                                     |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Nama fitur          | Verifikasi transaksi                                                                                                                                                                           |
| Deskripsi           | Memeriksa kebenaran dan kelengkapan transaksi sebelum masuk laporan final.                                                                                                                     |
| Aktor               | Verifikator                                                                                                                                                                                    |
| Input               | Pilihan transaksi, keputusan (Terverifikasi atau Ditolak), catatan/alasan                                                                                                                      |
| Proses              | Menampilkan data dan bukti, menyimpan keputusan, memperbarui status, mencatat pelaku dan waktu                                                                                                 |
| Output              | Status transaksi diperbarui; notifikasi kepada pencatat apabila ditolak                                                                                                                        |
| Aturan validasi     | Alasan wajib diisi saat menolak; verifikator tidak dapat memverifikasi transaksi yang ia catat sendiri (pemisahan tugas); status Terverifikasi hanya dapat dibatalkan melalui koreksi tercatat |
| Kriteria penerimaan | Hanya transaksi Terverifikasi yang tersedia untuk laporan final; penolakan tanpa alasan gagal; seluruh keputusan tercatat                                                                      |

### FR-008 Penyusunan Laporan

| **Atribut**         | **Uraian**                                                                                                                                                                                |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Nama fitur          | Penyusunan laporan                                                                                                                                                                        |
| Deskripsi           | Menyusun draf laporan per periode dan/atau per program.                                                                                                                                   |
| Aktor               | Staf keuangan                                                                                                                                                                             |
| Input               | Jenis laporan, periode, program (opsional), catatan                                                                                                                                       |
| Proses              | Mengambil transaksi Terverifikasi pada periode, menghitung total masuk, total keluar, dan saldo (BR-03), membentuk draf                                                                   |
| Output              | Draf laporan berstatus Draf                                                                                                                                                               |
| Aturan validasi     | Tanggal akhir tidak lebih awal dari tanggal awal; periode tidak boleh tumpang tindih dengan laporan final jenis sama untuk lingkup yang sama (**A-08**); draf kosong tidak dapat diajukan |
| Kriteria penerimaan | Total pada draf sama dengan hasil hitung manual dari transaksi terverifikasi periode tersebut; transaksi belum terverifikasi tidak ikut terhitung                                         |

### FR-009 Verifikasi dan Publikasi Laporan

| **Atribut**         | **Uraian**                                                                                                                                                                          |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Nama fitur          | Verifikasi dan publikasi laporan                                                                                                                                                    |
| Deskripsi           | Meninjau, menyetujui, dan memublikasikan laporan, serta menarik laporan bila diperlukan.                                                                                            |
| Aktor               | Verifikator, pihak berwenang, administrator sistem                                                                                                                                  |
| Input               | Draf laporan, keputusan (Setuju atau Tolak), catatan                                                                                                                                |
| Proses              | Peninjauan oleh verifikator; persetujuan pihak berwenang; publikasi; penarikan (unpublish) dengan alasan                                                                            |
| Output              | Laporan berstatus Disetujui atau Dipublikasikan; versi laporan tersimpan                                                                                                            |
| Aturan validasi     | Laporan hanya dapat dipublikasikan setelah disetujui pihak berwenang (BR-02); penolakan wajib beralasan; laporan terpublikasi tidak dapat diubah, hanya direvisi sebagai versi baru |
| Kriteria penerimaan | Laporan belum disetujui tidak tampil di publik; setelah dipublikasikan, laporan tampil di dashboard dalam waktu maksimal 1 menit (**A-07**); penarikan dan revisi tercatat          |

### FR-010 Dashboard Transparansi Dana

| **Atribut**         | **Uraian**                                                                                       |
|---------------------|--------------------------------------------------------------------------------------------------|
| Nama fitur          | Dashboard transparansi dana                                                                      |
| Deskripsi           | Halaman publik berisi ringkasan dana berdasarkan data laporan yang telah dipublikasikan.         |
| Aktor               | Publik, donatur                                                                                  |
| Input               | Pilihan periode atau program (opsional)                                                          |
| Proses              | Mengambil ringkasan dari laporan terpublikasi dan menampilkan total, saldo, dan grafik           |
| Output              | Total pemasukan, total pengeluaran, saldo, daftar program, grafik tren, waktu pembaruan terakhir |
| Aturan validasi     | Hanya data terverifikasi dan terpublikasi yang tampil; tanpa data pribadi                        |
| Kriteria penerimaan | Angka dashboard konsisten dengan laporan terpublikasi; dashboard dapat diakses tanpa login       |

### FR-011 Riwayat Transaksi dan Bukti Transaksi

| **Atribut**         | **Uraian**                                                                                                                      |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Nama fitur          | Riwayat dan bukti transaksi                                                                                                     |
| Deskripsi           | Menampilkan daftar transaksi terverifikasi beserta bukti yang boleh dilihat publik.                                             |
| Aktor               | Publik; staf internal (tampilan lengkap sesuai peran)                                                                           |
| Input               | Pilihan transaksi, filter periode/program                                                                                       |
| Proses              | Mengambil transaksi terverifikasi, menerapkan penyamaran data sensitif pada bukti publik                                        |
| Output              | Daftar riwayat; bukti (setelah penyamaran) dapat dilihat atau diunduh                                                           |
| Aturan validasi     | Bukti publik tidak memuat data pribadi (nomor rekening, identitas) tanpa otorisasi; kebijakan tampilan bukti mengikuti **Q-09** |
| Kriteria penerimaan | Publik hanya melihat transaksi terverifikasi; bukti publik bebas dari data sensitif; staf internal melihat riwayat perubahan    |

### FR-012 Pencarian dan Filter Laporan

| **Atribut**         | **Uraian**                                                                                                      |
|---------------------|-----------------------------------------------------------------------------------------------------------------|
| Nama fitur          | Pencarian dan filter laporan                                                                                    |
| Deskripsi           | Mencari dan menyaring laporan berdasarkan periode, program, dan jenis.                                          |
| Aktor               | Publik, staf internal                                                                                           |
| Input               | Kata kunci, rentang periode, program, jenis laporan                                                             |
| Proses              | Menyaring laporan terpublikasi (publik) atau semua status (internal)                                            |
| Output              | Daftar laporan sesuai kriteria dan tombol unduh                                                                 |
| Aturan validasi     | Rentang tanggal valid; hasil kosong menampilkan pesan informatif                                                |
| Kriteria penerimaan | Hasil hanya memuat laporan yang sesuai seluruh filter; publik tidak menemukan laporan yang belum dipublikasikan |

### FR-013 Pengaduan atau Pertanyaan Publik (Tentatif, A-01)

| **Atribut**         | **Uraian**                                                                                                                                     |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| Nama fitur          | Pengaduan atau pertanyaan publik                                                                                                               |
| Deskripsi           | Publik mengirim pertanyaan atau pengaduan terkait laporan; staf menanggapi.                                                                    |
| Aktor               | Publik, staf program (penanggap), pihak berwenang (eskalasi)                                                                                   |
| Input               | Nama (opsional), surel/kontak (opsional), isi pesan, tautan laporan terkait (opsional)                                                         |
| Proses              | Validasi, simpan dengan nomor tiket, penugasan, tanggapan, perubahan status                                                                    |
| Output              | Nomor tiket dan status tanggapan                                                                                                               |
| Aturan validasi     | Isi pesan wajib dan maksimum 1.000 karakter (**A-07**); perlindungan dari pengiriman otomatis (CAPTCHA atau pembatasan frekuensi)              |
| Kriteria penerimaan | Pengaduan valid menghasilkan nomor tiket; penanggap dapat memperbarui status; fitur diimplementasikan hanya bila lingkup disepakati (**Q-01**) |

### FR-014 Jejak Audit Perubahan Data

| **Atribut**         | **Uraian**                                                                                                                          |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Nama fitur          | Jejak audit (audit trail)                                                                                                           |
| Deskripsi           | Mencatat setiap perubahan data penting agar dapat ditelusuri (BR-05).                                                               |
| Aktor               | Sistem (otomatis); administrator sistem dan auditor (melihat)                                                                       |
| Input               | Peristiwa perubahan (tambah, ubah, hapus, verifikasi, persetujuan, publikasi)                                                       |
| Proses              | Menyimpan pelaku, waktu, objek, nilai lama, nilai baru, alasan                                                                      |
| Output              | Daftar log yang dapat dicari dan disaring                                                                                           |
| Aturan validasi     | Log tidak dapat diubah atau dihapus oleh pengguna aplikasi                                                                          |
| Kriteria penerimaan | Setiap perubahan pada pemasukan, pengeluaran, program, penyaluran, dan laporan menghasilkan log lengkap; upaya mengubah log ditolak |

## 6. Kebutuhan Nonfungsional

Angka target pada bagian ini merupakan **asumsi awal tim (A-07)** yang perlu disepakati dengan stakeholder dan dosen pembimbing.

| **Kode** | **Kategori**         | **Kebutuhan**                                                                                                                                               | **Cara pengukuran**                          |
|----------|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------|
| NFR-001  | Keamanan             | Seluruh komunikasi menggunakan HTTPS/TLS.                                                                                                                   | Pemeriksaan konfigurasi dan pemindaian situs |
| NFR-002  | Keamanan             | Kata sandi disimpan dalam bentuk hash dengan algoritma yang kuat dan salt.                                                                                  | Tinjauan kode dan basis data                 |
| NFR-003  | Keamanan             | Akses fitur internal wajib melalui autentikasi dan otorisasi berbasis peran.                                                                                | Uji akses lintas peran                       |
| NFR-004  | Keamanan             | Sesi pengguna kedaluwarsa setelah 30 menit tanpa aktivitas; sistem terlindung dari serangan umum (injeksi SQL, XSS, CSRF).                                  | Uji sesi dan uji keamanan dasar              |
| NFR-005  | Privasi              | Data pribadi penerima manfaat tidak tampil di antarmuka publik tanpa dasar dan otorisasi (BR-04), serta dikumpulkan seminimal mungkin.                      | Uji tampilan publik dan tinjauan data        |
| NFR-006  | Privasi              | Sistem menyediakan pemberitahuan kebijakan privasi bagi pengguna publik dan pengunggah data; kepatuhan pada UU PDP ditinjau bersama stakeholder (**Q-10**). | Tinjauan dokumen kebijakan                   |
| NFR-007  | Kinerja              | Halaman dashboard publik dimuat dalam maksimal 3 detik pada koneksi normal untuk 100 pengguna bersamaan.                                                    | Uji beban                                    |
| NFR-008  | Kinerja              | Pencarian dan filter laporan menghasilkan hasil dalam maksimal 3 detik; pembuatan draf laporan satu periode maksimal 10 detik.                              | Uji kinerja                                  |
| NFR-009  | Kemudahan penggunaan | Pengguna baru dapat melihat saldo dan laporan tanpa pelatihan; antarmuka berbahasa Indonesia dengan istilah yang konsisten.                                 | Uji kegunaan dengan minimal 5 responden      |
| NFR-010  | Kemudahan penggunaan | Pesan kesalahan menjelaskan penyebab dan cara perbaikan; tampilan mengikuti pedoman aksesibilitas dasar (kontras, label formulir).                          | Tinjauan antarmuka                           |
| NFR-011  | Kompatibilitas       | Sistem berjalan pada peramban modern versi terbaru (Chrome, Firefox, Edge, Safari) dan responsif pada layar ponsel hingga desktop.                          | Uji lintas peramban dan perangkat            |
| NFR-012  | Ketersediaan         | Dashboard publik tersedia minimal 99% per bulan di luar pemeliharaan terjadwal; cadangan basis data dibuat setiap hari.                                     | Pemantauan dan uji pemulihan                 |
| NFR-013  | Integritas data      | Basis data menerapkan batasan integritas (kunci unik, kunci asing, tipe data) dan transaksi atomik.                                                         | Tinjauan skema dan uji basis data            |
| NFR-014  | Integritas data      | Angka pada dashboard, laporan, dan riwayat transaksi harus konsisten dan berasal dari satu sumber data terverifikasi.                                       | Uji rekonsiliasi                             |

## 7. Aturan Bisnis

Aturan bisnis berikut berasal dari ketentuan proyek. Rincian kebijakan lainnya menunggu konfirmasi stakeholder.

| **Kode** | **Aturan Bisnis**                                                                                                                 | **Keterkaitan**         |
|----------|-----------------------------------------------------------------------------------------------------------------------------------|-------------------------|
| BR-01    | Hanya transaksi yang sudah diverifikasi yang dapat dimasukkan ke laporan final.                                                   | FR-007, FR-008          |
| BR-02    | Laporan harus melalui persetujuan pihak berwenang sebelum dipublikasikan.                                                         | FR-009                  |
| BR-03    | Saldo dihitung dari total dana masuk dikurangi total dana keluar sesuai ruang lingkup dan periode yang ditentukan.                | FR-008, FR-010          |
| BR-04    | Data pribadi penerima manfaat tidak boleh ditampilkan kepada publik tanpa dasar dan otorisasi yang sesuai.                        | FR-006, FR-011, NFR-005 |
| BR-05    | Setiap perubahan data penting harus dapat ditelusuri.                                                                             | FR-014                  |
| BR-06    | Verifikator tidak boleh memverifikasi transaksi yang ia catat sendiri (pemisahan tugas). Usulan tim, perlu konfirmasi (**Q-11**). | FR-007                  |
| BR-07    | Laporan yang telah dipublikasikan tidak diubah; koreksi dilakukan melalui revisi dengan nomor versi baru. Usulan tim (**Q-12**).  | FR-009                  |

## 8. Aktor dan Use Case

### 8.1 Identifikasi Aktor

| **Aktor**                       | **Deskripsi**                                                            |
|---------------------------------|--------------------------------------------------------------------------|
| Administrator sistem            | Mengelola akun, peran, konfigurasi, dan melihat audit trail              |
| Staf keuangan                   | Mencatat pemasukan dan pengeluaran, menyusun laporan                     |
| Staf program                    | Mengelola program, penyaluran, penerima manfaat, dan tanggapan pengaduan |
| Verifikator                     | Memverifikasi transaksi dan meninjau draf laporan                        |
| Pihak berwenang                 | Menyetujui laporan untuk dipublikasikan                                  |
| Publik/donatur                  | Mengakses dashboard, laporan, dan mengirim pertanyaan (tanpa login)      |
| Modul donasi (sistem eksternal) | Sumber data pemasukan, apabila terintegrasi (**Q-03**)                   |

### 8.2 Daftar Use Case

| **Kode** | **Use case**                            | **Aktor utama**                        | **FR terkait** |
|----------|-----------------------------------------|----------------------------------------|----------------|
| UC-01    | Login dan kelola hak akses              | Semua pengguna internal, administrator | FR-001         |
| UC-02    | Kelola data pemasukan                   | Staf keuangan                          | FR-002         |
| UC-03    | Kelola data pengeluaran                 | Staf keuangan                          | FR-003         |
| UC-04    | Kelola data program                     | Staf program                           | FR-004         |
| UC-05    | Kelola penyaluran dana                  | Staf program                           | FR-005         |
| UC-06    | Kelola data penerima manfaat            | Staf program                           | FR-006         |
| UC-07    | Verifikasi transaksi                    | Verifikator                            | FR-007         |
| UC-08    | Susun laporan                           | Staf keuangan                          | FR-008         |
| UC-09    | Setujui dan publikasikan laporan        | Verifikator, pihak berwenang           | FR-009         |
| UC-10    | Lihat dashboard transparansi            | Publik/donatur                         | FR-010         |
| UC-11    | Lihat riwayat dan bukti transaksi       | Publik/donatur, staf                   | FR-011         |
| UC-12    | Cari dan filter laporan                 | Publik/donatur, staf                   | FR-012         |
| UC-13    | Kirim dan tanggapi pengaduan (tentatif) | Publik, staf program                   | FR-013         |
| UC-14    | Lihat jejak audit                       | Administrator, auditor                 | FR-014         |

### 8.3 Use Case Diagram

Mermaid tidak memiliki notasi use case baku, sehingga diagram digambar dengan diagram alir: aktor berbentuk kapsul dan use case berada di dalam batas sistem.

flowchart LR  
ADM(\[Administrator Sistem\])  
KEU(\[Staf Keuangan\])  
PRG(\[Staf Program\])  
VER(\[Verifikator\])  
PIM(\[Pihak Berwenang\])  
PUB(\[Publik / Donatur\])  
subgraph SIS\[Subsistem Pelaporan Publik dan Transparansi Dana\]  
UC01(\[UC-01 Login dan Hak Akses\])  
UC02(\[UC-02 Kelola Pemasukan\])  
UC03(\[UC-03 Kelola Pengeluaran\])  
UC04(\[UC-04 Kelola Program\])  
UC05(\[UC-05 Kelola Penyaluran\])  
UC06(\[UC-06 Kelola Penerima Manfaat\])  
UC07(\[UC-07 Verifikasi Transaksi\])  
UC08(\[UC-08 Susun Laporan\])  
UC09(\[UC-09 Setujui dan Publikasikan Laporan\])  
UC10(\[UC-10 Dashboard Transparansi\])  
UC11(\[UC-11 Riwayat dan Bukti Transaksi\])  
UC12(\[UC-12 Cari dan Filter Laporan\])  
UC13(\[UC-13 Pengaduan Publik\])  
UC14(\[UC-14 Jejak Audit\])  
end  
ADM --- UC01  
ADM --- UC14  
ADM --- UC09  
KEU --- UC01  
KEU --- UC02  
KEU --- UC03  
KEU --- UC08  
PRG --- UC01  
PRG --- UC04  
PRG --- UC05  
PRG --- UC06  
PRG --- UC13  
VER --- UC01  
VER --- UC07  
VER --- UC09  
PIM --- UC01  
PIM --- UC09  
PUB --- UC10  
PUB --- UC11  
PUB --- UC12  
PUB --- UC13

### 8.4 Use Case Description

Deskripsi berikut merupakan rancangan alur yang perlu divalidasi (**Q-05**).

| **Kode**                       | **Prakondisi**                           | **Alur utama**                                                                                                                   | **Alur alternatif**                                                                                 | **Pascakondisi**                                |
|--------------------------------|------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------|-------------------------------------------------|
| UC-01 Login                    | Akun aktif                               | 1\) Pengguna membuka halaman login. 2) Mengisi kredensial. 3) Sistem memeriksa dan membuat sesi. 4) Menu sesuai peran tampil.    | Kredensial salah: pesan kesalahan. Gagal 5 kali: akun terkunci sementara.                           | Pengguna masuk dengan hak akses sesuai peran    |
| UC-02 Kelola pemasukan         | Pengguna login sebagai staf keuangan     | 1\) Pilih tambah pemasukan. 2) Isi data dan unggah bukti. 3) Sistem validasi. 4) Sistem menyimpan berstatus Menunggu Verifikasi. | Validasi gagal: pesan kesalahan. Ubah data terverifikasi: diarahkan ke koreksi.                     | Pemasukan tersimpan dan tercatat di audit trail |
| UC-03 Kelola pengeluaran       | Staf keuangan login                      | 1\) Pilih tambah pengeluaran. 2) Isi data dan bukti. 3) Sistem validasi. 4) Simpan Menunggu Verifikasi.                          | Bukti tidak ada: simpan ditolak.                                                                    | Pengeluaran tersimpan                           |
| UC-04 Kelola program           | Staf program login                       | 1\) Isi data program. 2) Sistem validasi nama unik dan periode. 3) Simpan. 4) Ubah status bila diperlukan.                       | Program bertransaksi tidak dapat dihapus; hanya dinonaktifkan.                                      | Program tersimpan dan tampil                    |
| UC-05 Kelola penyaluran        | Program aktif tersedia                   | 1\) Pilih program dan penerima (opsional). 2) Isi nominal, tanggal, bukti. 3) Sistem validasi. 4) Simpan Menunggu Verifikasi.    | Nominal melebihi saldo tersedia: ditolak sesuai kebijakan (**Q-07**).                               | Penyaluran tercatat dan tertaut ke program      |
| UC-06 Kelola penerima manfaat  | Staf program login                       | 1\) Isi data minimum. 2) Tetapkan atribut publik. 3) Simpan.                                                                     | Data tidak diizinkan publik tetap disamarkan.                                                       | Data tersimpan; tampilan publik teranonimkan    |
| UC-07 Verifikasi transaksi     | Ada transaksi Menunggu Verifikasi        | 1\) Verifikator membuka transaksi dan bukti. 2) Memilih Terverifikasi. 3) Sistem memperbarui status dan mencatat log.            | Pilih Ditolak: wajib isi alasan, transaksi dikembalikan. Pencatat sama dengan verifikator: ditolak. | Status transaksi diperbarui                     |
| UC-08 Susun laporan            | Ada transaksi Terverifikasi              | 1\) Pilih jenis, periode, program. 2) Sistem menghitung total dan saldo. 3) Draf dibuat. 4) Diajukan ke tinjauan.                | Tidak ada transaksi terverifikasi: draf tidak dapat diajukan. Periode tumpang tindih: ditolak.      | Draf laporan berstatus Diajukan                 |
| UC-09 Setujui dan publikasikan | Draf diajukan                            | 1\) Verifikator meninjau. 2) Pihak berwenang menyetujui. 3) Laporan dipublikasikan. 4) Dashboard diperbarui.                     | Ditolak: kembali ke Draf dengan catatan. Penarikan laporan: wajib alasan.                           | Laporan tampil di publik                        |
| UC-10 Dashboard                | Ada laporan terpublikasi                 | 1\) Publik membuka dashboard. 2) Sistem menampilkan ringkasan dan grafik. 3) Publik memilih periode/program.                     | Belum ada laporan: pesan informatif.                                                                | Ringkasan sesuai filter tampil                  |
| UC-11 Riwayat dan bukti        | Transaksi terverifikasi tersedia         | 1\) Buka riwayat. 2) Pilih transaksi. 3) Lihat bukti publik yang sudah disamarkan.                                               | Bukti tidak boleh publik: hanya keterangan tampil.                                                  | Riwayat dan bukti tampil                        |
| UC-12 Cari dan filter          | Laporan tersedia                         | 1\) Isi kata kunci dan filter. 2) Sistem menampilkan hasil. 3) Pengguna mengunduh laporan.                                       | Hasil kosong: pesan informatif.                                                                     | Daftar laporan sesuai kriteria                  |
| UC-13 Pengaduan (tentatif)     | Lingkup disepakati (**Q-01**)            | 1\) Publik mengisi formulir. 2) Sistem memberi nomor tiket. 3) Staf menanggapi dan mengubah status.                              | Isi kosong atau melebihi batas: ditolak.                                                            | Tiket tercatat dan tertanggapi                  |
| UC-14 Jejak audit              | Login sebagai administrator atau auditor | 1\) Buka log. 2) Saring berdasarkan pengguna, objek, waktu. 3) Lihat nilai lama dan baru.                                        | Tidak ada data: pesan informatif.                                                                   | Log dapat ditelusuri tanpa dapat diubah         |

## 9. Data dan Laporan

### 9.1 Entitas Data

Pengguna, Peran, Pemasukan, Pengeluaran, Program, Penyaluran, Penerima Manfaat, Bukti Transaksi, Laporan, Pengaduan, dan Log Audit.

erDiagram  
PERAN \|\|--o{ PENGGUNA : memiliki  
PROGRAM \|\|--o{ PEMASUKAN : menerima  
PROGRAM \|\|--o{ PENGELUARAN : memakai  
PROGRAM \|\|--o{ PENYALURAN : memiliki  
PENERIMA_MANFAAT \|\|--o{ PENYALURAN : menerima  
PENGELUARAN \|\|--o\| PENYALURAN : mencatat  
PEMASUKAN \|\|--o{ BUKTI_TRANSAKSI : dilengkapi  
PENGELUARAN \|\|--o{ BUKTI_TRANSAKSI : dilengkapi  
LAPORAN }o--o{ PROGRAM : mencakup  
PENGGUNA \|\|--o{ LOG_AUDIT : melakukan  
LAPORAN \|\|--o{ PENGADUAN : dirujuk

### 9.2 Data Dictionary Awal

Tipe data bersifat awal dan dapat disesuaikan pada tahap perancangan basis data.

| **Entitas**      | **Atribut**                                                                                                                                                             | **Tipe**                                                                                          | **Keterangan**                                             |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|------------------------------------------------------------|
| Pengguna         | id_pengguna (PK), nama, nama_pengguna, kata_sandi_hash, id_peran (FK), status_aktif                                                                                     | Integer, String, String, String, Integer, Boolean                                                 | Nama pengguna unik                                         |
| Peran            | id_peran (PK), nama_peran                                                                                                                                               | Integer, String                                                                                   | Contoh: admin, keuangan, program, verifikator, berwenang   |
| Pemasukan        | id_pemasukan (PK), tanggal, sumber, nominal, kategori, id_program (FK, opsional), keterangan, status, dicatat_oleh (FK), diverifikasi_oleh (FK)                         | Integer, Date, String, Decimal, String, Integer, Text, Enum, Integer, Integer                     | Status: Menunggu Verifikasi, Terverifikasi, Ditolak        |
| Pengeluaran      | id_pengeluaran (PK), tanggal, penerima_pembayaran, nominal, kategori, id_program (FK, opsional), keterangan, status, dicatat_oleh (FK), diverifikasi_oleh (FK)          | Integer, Date, String, Decimal, String, Integer, Text, Enum, Integer, Integer                     | Nominal lebih dari nol                                     |
| Program          | id_program (PK), nama, deskripsi, tanggal_mulai, tanggal_selesai, target_dana, status                                                                                   | Integer, String, Text, Date, Date, Decimal, Enum                                                  | Status: Aktif, Selesai, Nonaktif                           |
| Penyaluran       | id_penyaluran (PK), id_program (FK), id_penerima (FK, opsional), id_pengeluaran (FK), tanggal, nominal, bentuk                                                          | Integer, Integer, Integer, Integer, Date, Decimal, String                                         | Tertaut ke pengeluaran                                     |
| Penerima Manfaat | id_penerima (PK), kode_penerima, nama, kategori, wilayah, boleh_dipublikasikan                                                                                          | Integer, String, String, String, String, Boolean                                                  | Data pribadi dilindungi (BR-04)                            |
| Bukti Transaksi  | id_bukti (PK), jenis_transaksi, id_transaksi, nama_berkas, tipe_berkas, ukuran, tampil_publik                                                                           | Integer, Enum, Integer, String, String, Integer, Boolean                                          | Berkas di penyimpanan aman                                 |
| Laporan          | id_laporan (PK), jenis, periode_awal, periode_akhir, id_program (FK, opsional), total_masuk, total_keluar, saldo, status, versi, disetujui_oleh (FK), tanggal_publikasi | Integer, String, Date, Date, Integer, Decimal, Decimal, Decimal, Enum, Integer, Integer, DateTime | Status: Draf, Diajukan, Disetujui, Dipublikasikan, Ditarik |
| Pengaduan        | id_pengaduan (PK), nomor_tiket, isi, kontak_opsional, id_laporan (FK, opsional), status, tanggapan                                                                      | Integer, String, Text, String, Integer, Enum, Text                                                | Tentatif (A-01)                                            |
| Log Audit        | id_log (PK), id_pengguna (FK), waktu, jenis_aksi, objek, id_objek, nilai_lama, nilai_baru, alasan                                                                       | Integer, Integer, DateTime, String, String, Integer, Text, Text, Text                             | Tidak dapat diubah (FR-014)                                |

### 9.3 Daftar Laporan yang Dihasilkan

| **Kode** | **Laporan**                                                           | **Pengguna**           | **Visibilitas**          |
|----------|-----------------------------------------------------------------------|------------------------|--------------------------|
| LAP-01   | Laporan pemasukan per periode                                         | Staf, publik           | Publik setelah publikasi |
| LAP-02   | Laporan pengeluaran per periode                                       | Staf, publik           | Publik setelah publikasi |
| LAP-03   | Laporan saldo berjalan dan ringkasan dana                             | Staf, publik           | Publik setelah publikasi |
| LAP-04   | Laporan per program (dana masuk, dana tersalurkan, sisa)              | Staf, publik           | Publik setelah publikasi |
| LAP-05   | Laporan penyaluran dana dan ringkasan penerima manfaat (teranonimkan) | Staf, publik           | Publik setelah publikasi |
| LAP-06   | Daftar transaksi menunggu dan hasil verifikasi                        | Verifikator            | Internal                 |
| LAP-07   | Log audit perubahan data                                              | Administrator, auditor | Internal                 |

Format keluaran (misalnya PDF dan CSV) mengikuti kesepakatan (**Q-13**).

### 9.4 Informasi pada Dashboard Publik

1.  Total pemasukan, total pengeluaran, dan saldo berjalan pada periode terpilih.

2.  Daftar program beserta status, target, dana masuk, dan dana tersalurkan.

3.  Grafik tren pemasukan dan pengeluaran per periode.

4.  Ringkasan penyaluran per program dan kategori (tanpa data pribadi).

5.  Daftar laporan terpublikasi beserta tombol unduh.

6.  Riwayat transaksi terverifikasi dan bukti publik.

7.  Waktu pembaruan terakhir dan keterangan bahwa data bersumber dari transaksi terverifikasi.

## 10. Kriteria Penerimaan dan Traceability

### 10.1 Kriteria Penerimaan Sistem

1.  Seluruh FR berprioritas wajib (FR-001 sampai FR-012 dan FR-014) lulus pengujian penerimaan; FR-013 diuji bila lingkup disepakati.

2.  Tidak ada cacat berkategori kritis atau tinggi yang belum diselesaikan.

3.  Seluruh aturan bisnis BR-01 sampai BR-07 terbukti terpenuhi melalui skenario uji.

4.  Angka dashboard, laporan, dan data transaksi terverifikasi konsisten pada uji rekonsiliasi.

5.  Uji tampilan publik membuktikan tidak ada data pribadi penerima manfaat yang terbuka tanpa otorisasi.

6.  Target kinerja dan keamanan pada NFR-001 sampai NFR-014 terpenuhi atau disetujui secara tertulis bila disesuaikan.

7.  Pemangku kepentingan utama (pihak berwenang dan dosen pembimbing) menyetujui hasil demonstrasi.

### 10.2 Requirement Traceability Matrix

| **Kebutuhan**          | **Fitur/modul**             | **Use case**               | **Pengujian**                                                                                          |
|------------------------|-----------------------------|----------------------------|--------------------------------------------------------------------------------------------------------|
| FR-001                 | Autentikasi dan hak akses   | UC-01                      | TC-001 login valid/tidak valid, TC-002 kunci akun, TC-003 akses lintas peran                           |
| FR-002                 | Pemasukan                   | UC-02                      | TC-004 tambah pemasukan, TC-005 validasi nominal dan bukti                                             |
| FR-003                 | Pengeluaran                 | UC-03                      | TC-006 tambah pengeluaran, TC-007 tanpa bukti ditolak                                                  |
| FR-004                 | Program                     | UC-04                      | TC-008 tambah/ubah program, TC-009 hapus program bertransaksi                                          |
| FR-005                 | Penyaluran dana             | UC-05                      | TC-010 catat penyaluran, TC-011 melebihi saldo                                                         |
| FR-006                 | Penerima manfaat            | UC-06                      | TC-012 simpan data, TC-013 anonimisasi tampilan publik                                                 |
| FR-007                 | Verifikasi transaksi        | UC-07                      | TC-014 verifikasi, TC-015 tolak tanpa alasan, TC-016 pemisahan tugas                                   |
| FR-008                 | Penyusunan laporan          | UC-08                      | TC-017 hitung saldo, TC-018 hanya transaksi terverifikasi                                              |
| FR-009                 | Persetujuan dan publikasi   | UC-09                      | TC-019 setujui dan publikasi, TC-020 laporan belum disetujui tidak tampil, TC-021 revisi dan penarikan |
| FR-010                 | Dashboard                   | UC-10                      | TC-022 konsistensi angka, TC-023 akses tanpa login                                                     |
| FR-011                 | Riwayat dan bukti           | UC-11                      | TC-024 riwayat publik, TC-025 bukti tanpa data sensitif                                                |
| FR-012                 | Pencarian dan filter        | UC-12                      | TC-026 filter periode/program, TC-027 hasil kosong                                                     |
| FR-013                 | Pengaduan publik (tentatif) | UC-13                      | TC-028 kirim pengaduan, TC-029 tanggapan dan status                                                    |
| FR-014                 | Audit trail                 | UC-14                      | TC-030 log perubahan, TC-031 log tidak dapat diubah                                                    |
| NFR-001 sampai NFR-004 | Keamanan                    | UC-01                      | TC-032 uji HTTPS, TC-033 hash kata sandi, TC-034 sesi, TC-035 uji kerentanan dasar                     |
| NFR-005, NFR-006       | Privasi                     | UC-06, UC-11               | TC-013, TC-025, TC-036 tinjauan kebijakan privasi                                                      |
| NFR-007, NFR-008       | Kinerja                     | UC-10, UC-12               | TC-037 uji beban dashboard, TC-038 uji waktu pencarian dan laporan                                     |
| NFR-009, NFR-010       | Kemudahan penggunaan        | Semua                      | TC-039 uji kegunaan, TC-040 tinjauan pesan kesalahan                                                   |
| NFR-011                | Kompatibilitas              | Semua                      | TC-041 uji lintas peramban dan perangkat                                                               |
| NFR-012                | Ketersediaan                | Semua                      | TC-042 pemantauan dan pemulihan cadangan                                                               |
| NFR-013, NFR-014       | Integritas data             | UC-02, UC-03, UC-08, UC-10 | TC-043 uji batasan basis data, TC-044 rekonsiliasi                                                     |
| BR-01                  | Verifikasi dan laporan      | UC-07, UC-08               | TC-014, TC-018                                                                                         |
| BR-02                  | Persetujuan                 | UC-09                      | TC-019, TC-020                                                                                         |
| BR-03                  | Perhitungan saldo           | UC-08, UC-10               | TC-017, TC-022                                                                                         |
| BR-04                  | Privasi penerima            | UC-06, UC-11               | TC-013, TC-025                                                                                         |
| BR-05                  | Keterlacakan                | UC-14                      | TC-030, TC-031                                                                                         |
| BR-06                  | Pemisahan tugas             | UC-07                      | TC-016                                                                                                 |
| BR-07                  | Versi laporan               | UC-09                      | TC-021                                                                                                 |

## Lampiran A. Daftar Asumsi

| Kode | Asumsi                                                                                                             |
|------|--------------------------------------------------------------------------------------------------------------------|
| A-01 | Fitur pengaduan/pertanyaan publik dimasukkan sebagai fitur tentatif.                                               |
| A-02 | Latar belakang masalah disusun dari topik proyek, bukan dari hasil wawancara.                                      |
| A-03 | Sistem berbasis web.                                                                                               |
| A-04 | Antarmuka berbahasa Indonesia.                                                                                     |
| A-05 | Penilaian kepentingan dan pengaruh stakeholder adalah estimasi awal tim.                                           |
| A-06 | Pembagian RACI adalah usulan awal.                                                                                 |
| A-07 | Angka target (batas percobaan login, ukuran berkas, waktu respons, ketersediaan, panjang teks) adalah usulan awal. |
| A-08 | Laporan final jenis sama tidak boleh memiliki periode yang tumpang tindih untuk lingkup yang sama.                 |

## Lampiran B. Daftar Pertanyaan untuk Stakeholder

| **Kode** | **Pertanyaan**                                                                                         | **Ditujukan kepada**                |
|----------|--------------------------------------------------------------------------------------------------------|-------------------------------------|
| Q-01     | Apakah fitur pengaduan/pertanyaan publik termasuk ruang lingkup yang disepakati?                       | Pimpinan, dosen pembimbing          |
| Q-02     | Siapa jabatan yang berwenang menyetujui laporan, dan apakah perlu lebih dari satu tingkat persetujuan? | Pimpinan                            |
| Q-03     | Bagaimana data pemasukan diperoleh dari modul donasi (impor, antarmuka, atau input manual)?            | Tim modul donasi                    |
| Q-04     | Apakah ada auditor atau pengawas eksternal yang memerlukan akses khusus?                               | Pimpinan                            |
| Q-05     | Apakah alur proses bisnis pada Bagian 4 sesuai praktik organisasi?                                     | Staf keuangan, program, verifikator |
| Q-06     | Apakah pembuatan atau perubahan program memerlukan persetujuan pihak berwenang?                        | Pimpinan                            |
| Q-07     | Bagaimana kebijakan bila penyaluran melebihi saldo tersedia?                                           | Pimpinan, keuangan                  |
| Q-08     | Data penerima manfaat apa saja yang dikumpulkan, dan data apa yang boleh dipublikasikan?               | Staf program, pimpinan              |
| Q-09     | Jenis bukti apa yang boleh ditampilkan kepada publik dan bagaimana penyamarannya?                      | Pimpinan                            |
| Q-10     | Apakah organisasi sudah memiliki kebijakan privasi dan prosedur pelindungan data pribadi?              | Pimpinan                            |
| Q-11     | Apakah prinsip pemisahan tugas pencatat dan verifikator dapat diterapkan dengan jumlah staf yang ada?  | Pimpinan, keuangan                  |
| Q-12     | Bagaimana kebijakan koreksi atau penarikan laporan yang sudah dipublikasikan?                          | Pimpinan                            |
| Q-13     | Format keluaran laporan apa yang dibutuhkan (PDF, CSV, lainnya)?                                       | Pimpinan, publik pengguna           |

## Lampiran C. Antarmuka Eksternal

Lampiran C sampai F melengkapi dokumen dengan klausa antarmuka dan verifikasi yang lazim pada ISO/IEC/IEEE 29148, serta daftar modul dan daftar fungsi sebagai turunan kebutuhan. Daftar modul dan daftar fungsi bukan klausa wajib ISO 29148; keduanya ditambahkan untuk menjembatani SRS ke perancangan sistem. Kebutuhan antarmuka yang belum dikonfirmasi ditandai asumsi **A-09** dan pertanyaan **Q-14**, **Q-15**.

| **Kode** | **Jenis**          | **Kebutuhan antarmuka**                                                                                                                                                                             | **Keterkaitan**         |
|----------|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------|
| IF-01    | Antarmuka pengguna | Sistem menyediakan dua area berbahasa Indonesia: area publik tanpa login (dashboard, laporan, riwayat transaksi, pencarian) dan area internal dengan login (pengelolaan data, verifikasi, laporan). | FR-001, FR-010, NFR-009 |
| IF-02    | Antarmuka pengguna | Tampilan responsif dan dapat dipakai pada layar ponsel hingga desktop.                                                                                                                              | NFR-011                 |
| IF-03    | Antarmuka pengguna | Area publik hanya memuat kontrol baca (lihat, cari, filter, unduh) dan tidak memuat kontrol tambah, ubah, atau hapus data.                                                                          | FR-010, FR-011, BR-04   |
| IF-04    | Perangkat keras    | Tidak ada perangkat keras khusus pada sisi pengguna; sistem berjalan pada server atau layanan hosting yang spesifikasinya ditetapkan pada tahap perancangan (**A-09**).                             | NFR-012                 |
| IF-05    | Perangkat lunak    | Sistem diakses melalui peramban modern versi terbaru (Chrome, Firefox, Edge, Safari).                                                                                                               | NFR-011                 |
| IF-06    | Perangkat lunak    | Sistem menyimpan data pada basis data relasional; produk dan versinya belum ditetapkan (**Q-14**).                                                                                                  | NFR-013                 |
| IF-07    | Perangkat lunak    | Sistem menerima data pemasukan dari modul donasi melalui impor berkas atau antarmuka layanan; mekanisme belum ditetapkan (**Q-03**).                                                                | FR-002, UC-02           |
| IF-08    | Komunikasi         | Seluruh pertukaran data antara peramban dan server menggunakan HTTPS/TLS.                                                                                                                           | NFR-001                 |
| IF-09    | Komunikasi         | Laporan dapat diunduh dalam format yang disepakati, minimal PDF (**Q-13**).                                                                                                                         | FR-009, FR-012          |
| IF-10    | Komunikasi         | Notifikasi kepada pengguna internal (misalnya transaksi ditolak) disampaikan pada aplikasi; notifikasi surel bersifat opsional (**Q-15**).                                                          | FR-007                  |

## Lampiran D. Daftar Modul

| **Kode** | **Modul**                   | **Deskripsi**                                                                                  | **Aktor utama**                             | **FR terkait**                 | **Use case**               |
|----------|-----------------------------|------------------------------------------------------------------------------------------------|---------------------------------------------|--------------------------------|----------------------------|
| M-01     | Autentikasi dan Hak Akses   | Login, logout, pengelolaan akun, peran, dan hak akses                                          | Semua pengguna internal, administrator      | FR-001                         | UC-01                      |
| M-02     | Pengelolaan Pemasukan       | Pencatatan dan pengelolaan data dana masuk                                                     | Staf keuangan                               | FR-002                         | UC-02                      |
| M-03     | Pengelolaan Pengeluaran     | Pencatatan dan pengelolaan data dana keluar                                                    | Staf keuangan                               | FR-003                         | UC-03                      |
| M-04     | Pengelolaan Program         | Data program, periode, target, dan status                                                      | Staf program                                | FR-004                         | UC-04                      |
| M-05     | Penyaluran Dana             | Pencatatan penyaluran dana ke program dan penerima manfaat                                     | Staf program                                | FR-005                         | UC-05                      |
| M-06     | Penerima Manfaat            | Data penerima manfaat seminimal mungkin dan pengaturan tampilan publik                         | Staf program                                | FR-006                         | UC-06                      |
| M-07     | Verifikasi Transaksi        | Antrean dan keputusan verifikasi transaksi                                                     | Verifikator                                 | FR-007                         | UC-07                      |
| M-08     | Pelaporan                   | Penyusunan, perhitungan saldo, tinjauan, persetujuan, publikasi, revisi, dan penarikan laporan | Staf keuangan, verifikator, pihak berwenang | FR-008, FR-009                 | UC-08, UC-09               |
| M-09     | Portal dan Dashboard Publik | Dashboard, riwayat transaksi, bukti publik, serta pencarian dan filter laporan                 | Publik/donatur                              | FR-010, FR-011, FR-012         | UC-10, UC-11, UC-12        |
| M-10     | Pengaduan Publik (tentatif) | Pengiriman dan tanggapan pengaduan atau pertanyaan                                             | Publik, staf program                        | FR-013                         | UC-13                      |
| M-11     | Audit Trail                 | Pencatatan dan penelusuran perubahan data                                                      | Sistem, administrator                       | FR-014                         | UC-14                      |
| M-12     | Pengelolaan Bukti Transaksi | Unggah, validasi, penyimpanan terproteksi, dan penyamaran bukti                                | Staf keuangan, staf program                 | FR-002, FR-003, FR-005, FR-011 | UC-02, UC-03, UC-05, UC-11 |

## Lampiran E. Daftar Fungsi

| **Kode** | **Fungsi**                                                | **Modul** | **FR**         | **Aktor**                      |
|----------|-----------------------------------------------------------|-----------|----------------|--------------------------------|
| F-01.1   | Login pengguna                                            | M-01      | FR-001         | Pengguna internal              |
| F-01.2   | Logout dan pengakhiran sesi otomatis                      | M-01      | FR-001         | Pengguna internal              |
| F-01.3   | Penguncian akun setelah percobaan gagal berulang          | M-01      | FR-001         | Sistem                         |
| F-01.4   | Kelola akun pengguna                                      | M-01      | FR-001         | Administrator                  |
| F-01.5   | Tetapkan peran dan hak akses                              | M-01      | FR-001         | Administrator                  |
| F-02.1   | Tambah data pemasukan                                     | M-02      | FR-002         | Staf keuangan                  |
| F-02.2   | Lihat daftar dan detail pemasukan                         | M-02      | FR-002         | Staf keuangan, verifikator     |
| F-02.3   | Ubah data pemasukan (sesuai status)                       | M-02      | FR-002         | Staf keuangan                  |
| F-02.4   | Batalkan data pemasukan                                   | M-02      | FR-002         | Staf keuangan                  |
| F-02.5   | Impor pemasukan dari modul donasi (tentatif, **Q-03**)    | M-02      | FR-002         | Staf keuangan                  |
| F-03.1   | Tambah data pengeluaran                                   | M-03      | FR-003         | Staf keuangan                  |
| F-03.2   | Lihat daftar dan detail pengeluaran                       | M-03      | FR-003         | Staf keuangan, verifikator     |
| F-03.3   | Ubah data pengeluaran (sesuai status)                     | M-03      | FR-003         | Staf keuangan                  |
| F-03.4   | Batalkan data pengeluaran                                 | M-03      | FR-003         | Staf keuangan                  |
| F-04.1   | Tambah program                                            | M-04      | FR-004         | Staf program                   |
| F-04.2   | Ubah data program                                         | M-04      | FR-004         | Staf program                   |
| F-04.3   | Ubah status program (Aktif, Selesai, Nonaktif)            | M-04      | FR-004         | Staf program                   |
| F-04.4   | Lihat daftar dan detail program                           | M-04      | FR-004         | Pengguna internal              |
| F-05.1   | Catat penyaluran dana                                     | M-05      | FR-005         | Staf program                   |
| F-05.2   | Periksa batas dana tersedia pada program                  | M-05      | FR-005         | Sistem                         |
| F-05.3   | Lihat riwayat penyaluran                                  | M-05      | FR-005         | Staf program, verifikator      |
| F-06.1   | Tambah dan ubah data penerima manfaat                     | M-06      | FR-006         | Staf program                   |
| F-06.2   | Tetapkan atribut yang boleh tampil di publik              | M-06      | FR-006         | Staf program                   |
| F-06.3   | Anonimisasi data penerima untuk tampilan publik           | M-06      | FR-006         | Sistem                         |
| F-07.1   | Tampilkan antrean transaksi Menunggu Verifikasi           | M-07      | FR-007         | Verifikator                    |
| F-07.2   | Periksa data dan bukti transaksi                          | M-07      | FR-007         | Verifikator                    |
| F-07.3   | Setujui atau tolak transaksi (dengan alasan)              | M-07      | FR-007         | Verifikator                    |
| F-07.4   | Cegah verifikasi oleh pencatat yang sama                  | M-07      | FR-007         | Sistem                         |
| F-08.1   | Buat draf laporan per periode atau program                | M-08      | FR-008         | Staf keuangan                  |
| F-08.2   | Hitung total masuk, total keluar, dan saldo               | M-08      | FR-008         | Sistem                         |
| F-08.3   | Ajukan draf untuk tinjauan                                | M-08      | FR-008         | Staf keuangan                  |
| F-08.4   | Tinjau laporan                                            | M-08      | FR-009         | Verifikator                    |
| F-08.5   | Setujui atau tolak laporan                                | M-08      | FR-009         | Pihak berwenang                |
| F-08.6   | Publikasikan laporan                                      | M-08      | FR-009         | Pihak berwenang, administrator |
| F-08.7   | Buat revisi (versi baru) dan arsipkan versi lama          | M-08      | FR-009         | Staf keuangan, sistem          |
| F-08.8   | Tarik laporan dari publik                                 | M-08      | FR-009         | Pihak berwenang                |
| F-09.1   | Tampilkan ringkasan dana dan grafik tren                  | M-09      | FR-010         | Publik                         |
| F-09.2   | Tampilkan daftar program dan ringkasannya                 | M-09      | FR-010         | Publik                         |
| F-09.3   | Tampilkan dan unduh laporan terpublikasi                  | M-09      | FR-010         | Publik                         |
| F-09.4   | Tampilkan riwayat transaksi terverifikasi                 | M-09      | FR-011         | Publik, staf                   |
| F-09.5   | Tampilkan bukti publik (disamarkan)                       | M-09      | FR-011         | Publik                         |
| F-09.6   | Cari dan filter laporan menurut periode, program, jenis   | M-09      | FR-012         | Publik, staf                   |
| F-10.1   | Kirim pengaduan atau pertanyaan dan terbitkan nomor tiket | M-10      | FR-013         | Publik                         |
| F-10.2   | Tanggapi dan ubah status tiket                            | M-10      | FR-013         | Staf program                   |
| F-11.1   | Catat log perubahan data secara otomatis                  | M-11      | FR-014         | Sistem                         |
| F-11.2   | Cari dan saring log audit                                 | M-11      | FR-014         | Administrator, auditor         |
| F-12.1   | Unggah bukti dan validasi tipe serta ukuran               | M-12      | FR-002, FR-003 | Staf keuangan, staf program    |
| F-12.2   | Simpan bukti pada penyimpanan terproteksi                 | M-12      | FR-002, FR-003 | Sistem                         |
| F-12.3   | Samarkan data sensitif pada bukti untuk publik            | M-12      | FR-011         | Sistem                         |

## Lampiran F. Prioritas dan Metode Verifikasi Kebutuhan

Metode verifikasi mengikuti empat kategori ISO 29148: **Uji** (test), **Inspeksi**, **Demonstrasi**, dan **Analisis**. Prioritas memakai skala Must, Should, Could dan merupakan usulan awal tim yang perlu disepakati.

| Kebutuhan | Prioritas        | Metode verifikasi | Keterangan                                       |
|-----------|------------------|-------------------|--------------------------------------------------|
| FR-001    | Must             | Uji, demonstrasi  | TC-001 sampai TC-003                             |
| FR-002    | Must             | Uji               | TC-004, TC-005                                   |
| FR-003    | Must             | Uji               | TC-006, TC-007                                   |
| FR-004    | Must             | Uji               | TC-008, TC-009                                   |
| FR-005    | Must             | Uji               | TC-010, TC-011                                   |
| FR-006    | Must             | Uji, inspeksi     | TC-012, TC-013; inspeksi tampilan publik         |
| FR-007    | Must             | Uji               | TC-014 sampai TC-016                             |
| FR-008    | Must             | Uji, analisis     | TC-017, TC-018; analisis rumus saldo             |
| FR-009    | Must             | Uji, demonstrasi  | TC-019 sampai TC-021                             |
| FR-010    | Must             | Uji, demonstrasi  | TC-022, TC-023                                   |
| FR-011    | Must             | Uji, inspeksi     | TC-024, TC-025                                   |
| FR-012    | Should           | Uji               | TC-026, TC-027                                   |
| FR-013    | Could (tentatif) | Uji               | TC-028, TC-029; bergantung **Q-01**              |
| FR-014    | Must             | Uji, inspeksi     | TC-030, TC-031                                   |
| NFR-001   | Must             | Inspeksi, uji     | Konfigurasi dan pemindaian situs                 |
| NFR-002   | Must             | Inspeksi          | Tinjauan kode dan basis data                     |
| NFR-003   | Must             | Uji               | Uji akses lintas peran                           |
| NFR-004   | Must             | Uji               | Uji sesi dan kerentanan dasar                    |
| NFR-005   | Must             | Uji, inspeksi     | Tampilan publik tanpa data pribadi               |
| NFR-006   | Must             | Inspeksi          | Tinjauan kebijakan privasi                       |
| NFR-007   | Should           | Uji               | Uji beban dashboard                              |
| NFR-008   | Should           | Uji               | Uji waktu pencarian dan laporan                  |
| NFR-009   | Should           | Uji, demonstrasi  | Uji kegunaan dengan minimal 5 responden          |
| NFR-010   | Should           | Inspeksi          | Tinjauan pesan kesalahan dan aksesibilitas       |
| NFR-011   | Must             | Uji               | Lintas peramban dan perangkat                    |
| NFR-012   | Should           | Analisis, uji     | Pemantauan ketersediaan dan pemulihan cadangan   |
| NFR-013   | Must             | Inspeksi, uji     | Tinjauan skema dan uji basis data                |
| NFR-014   | Must             | Uji, analisis     | Rekonsiliasi angka dashboard, laporan, transaksi |
| BR-01     | Must             | Uji               | TC-014, TC-018                                   |
| BR-02     | Must             | Uji               | TC-019, TC-020                                   |
| BR-03     | Must             | Uji, analisis     | TC-017, TC-022                                   |
| BR-04     | Must             | Uji, inspeksi     | TC-013, TC-025                                   |
| BR-05     | Must             | Uji               | TC-030, TC-031                                   |
| BR-06     | Should           | Uji               | TC-016; bergantung **Q-11**                      |
| BR-07     | Should           | Uji               | TC-021; bergantung **Q-12**                      |

## Tambahan Asumsi dan Pertanyaan

| **Kode** | **Uraian**                                                                                                                                     |
|----------|------------------------------------------------------------------------------------------------------------------------------------------------|
| A-09     | Sistem dihosting pada server atau layanan hosting yang ditentukan pada tahap perancangan; tidak ada perangkat keras khusus pada sisi pengguna. |
| Q-14     | Basis data dan lingkungan hosting apa yang akan dipakai atau tersedia di organisasi?                                                           |
| Q-15     | Apakah notifikasi surel diperlukan selain notifikasi pada aplikasi?                                                                            |
