z**ANALISIS PROSES AS-IS**

**Sistem Pelaporan Publik dan Transparansi Dana Donasi**

_Disusun sebagai bagian dari dokumen Software Requirements Specification (SRS)_

Catatan ruang lingkup: Dokumen ini merupakan model awal proses As-Is berdasarkan asumsi umum pengelolaan donasi. Alur, peran, dan potensi masalah perlu dikonfirmasi melalui wawancara stakeholder serta pemeriksaan dokumen pada lembaga yang menjadi objek penelitian.

# 1. Pengertian Proses As-Is

Proses As-Is adalah analisis terhadap proses bisnis yang sedang berjalan sebelum sistem baru diterapkan. Analisis ini bertujuan mengetahui bagaimana data dikelola, siapa yang terlibat, bagaimana laporan dibuat, serta masalah yang mungkin terjadi dalam proses tersebut.

Dalam proyek ini, analisis berfokus pada proses pencatatan, pemeriksaan, dan publikasi laporan penerimaan serta penyaluran dana donasi kepada masyarakat.

# 2. Tujuan Analisis

1. Mengetahui alur pengelolaan laporan dana donasi yang sedang berjalan.
2. Mengidentifikasi pihak-pihak yang terlibat dalam penyusunan laporan.
3. Mengetahui sumber data penerimaan dan penyaluran donasi.
4. Mengidentifikasi kendala dalam penyusunan dan publikasi laporan.
5. Menjadi dasar dalam merancang sistem pelaporan publik yang lebih transparan dan mudah diakses.

# 3. Identifikasi Stakeholder

| **Stakeholder** | **Peran dalam Proses** |
| --- | --- |
| Donatur / masyarakat | Memberikan donasi dan membutuhkan informasi penggunaan dana. |
| Petugas penerimaan donasi | Mencatat dana yang masuk dan mengumpulkan bukti transaksi. |
| Bagian keuangan | Merekap penerimaan dan penyaluran dana serta menyiapkan laporan. |
| Admin sistem / publikasi | Mengunggah atau menyampaikan laporan kepada masyarakat. |
| Pimpinan pengelola donasi | Memeriksa dan menyetujui laporan sebelum dipublikasikan. |
| Dewan pengawas | Melakukan pemeriksaan sesuai kewenangan dan ketentuan lembaga. |

# 4. Alur Proses Bisnis As-Is

Model alur proses awal:

1. **1\. Penerimaan donasi:** Donatur memberikan dana melalui kanal yang tersedia.
2. **2\. Pencatatan transaksi:** Petugas mencatat transaksi dan menyimpan bukti penerimaan.
3. **3\. Rekapitulasi dana:** Bagian keuangan mengumpulkan data penerimaan dan penyaluran dana.
4. **4\. Pemeriksaan laporan:** Pihak berwenang memeriksa kesesuaian data dan bukti transaksi.
5. **5\. Persetujuan laporan:** Laporan diperbaiki jika ada kesalahan, lalu diajukan kembali untuk disetujui.
6. **6\. Publikasi laporan:** Admin memublikasikan laporan melalui media yang digunakan lembaga.
7. **7\. Akses informasi publik:** Masyarakat melihat laporan yang telah dipublikasikan.

Catatan: Diagram/alur ini merupakan model awal. Urutan dan aktivitas sebenarnya perlu dikonfirmasi melalui wawancara dan pemeriksaan dokumen pada lembaga yang menjadi objek penelitian.

# 5. Deskripsi Aktivitas Proses

| **Tahap** | **Aktivitas** | **Output** |
| --- | --- | --- |
| Penerimaan | Donatur menyerahkan donasi melalui kanal yang tersedia. | Dana diterima. |
| Pencatatan | Petugas mencatat nominal, tanggal, dan informasi transaksi sesuai prosedur. | Data transaksi dan bukti penerimaan. |
| Rekapitulasi | Bagian keuangan menggabungkan data penerimaan dan penyaluran. | Rekapitulasi dana. |
| Pemeriksaan | Pihak berwenang memeriksa data, bukti transaksi, dan kesesuaian nominal. | Laporan diperiksa atau daftar koreksi. |
| Persetujuan | Pihak berwenang menyetujui laporan atau meminta perbaikan. | Laporan yang disetujui. |
| Publikasi | Admin menampilkan laporan melalui media publikasi lembaga. | Laporan yang dapat diakses masyarakat. |
| Pemantauan | Masyarakat membaca informasi penerimaan dan penggunaan dana. | Informasi transparansi dana. |

# 6. Identifikasi Potensi Masalah

| **No.** | **Potensi Masalah** | **Dampak** |
| --- | --- | --- |
| 1 | Data transaksi tersimpan di beberapa file atau media berbeda. | Rekapitulasi lebih lama dan berisiko terjadi ketidaksesuaian data. |
| 2 | Rekapitulasi laporan masih dilakukan secara manual. | Penyusunan laporan berpotensi lambat. |
| 3 | Pemeriksaan dan persetujuan belum terdokumentasi dengan baik. | Status laporan dan pihak yang menyetujui sulit ditelusuri. |
| 4 | Laporan tidak diperbarui secara konsisten. | Masyarakat mungkin memperoleh informasi yang tidak mutakhir. |
| 5 | Informasi penerimaan dan penyaluran kurang terperinci. | Masyarakat kesulitan memahami penggunaan dana. |
| 6 | Riwayat perubahan laporan tidak tercatat secara memadai. | Kesalahan atau perubahan data lebih sulit ditelusuri. |

Penting: Daftar di atas adalah potensi masalah yang harus divalidasi melalui wawancara atau bukti proses aktual. Jangan menyatakan masalah sebagai fakta sebelum memperoleh data pendukung.

# 7. Analisis Kesenjangan dan Kebutuhan Perbaikan

| **Kondisi As-Is yang Perlu Diverifikasi** | **Kebutuhan Perbaikan yang Diusulkan** |
| --- | --- |
| Data transaksi dikumpulkan dari beberapa sumber (perlu diverifikasi). | Data laporan terorganisasi dalam sumber data yang terkelola. |
| Rekapitulasi membutuhkan pekerjaan berulang (perlu diverifikasi). | Sistem membantu menyusun rekapitulasi berdasarkan data transaksi. |
| Persetujuan dilakukan melalui komunikasi terpisah (perlu diverifikasi). | Sistem menyediakan status pemeriksaan dan persetujuan. |
| Publikasi laporan terpisah dari proses rekapitulasi (perlu diverifikasi). | Laporan yang telah disetujui dapat dipublikasikan melalui sistem. |
| Masyarakat mencari laporan dari berbagai media (perlu diverifikasi). | Tersedia halaman publik untuk melihat laporan berdasarkan periode. |
| Riwayat perubahan sulit ditelusuri (perlu diverifikasi). | Sistem mencatat riwayat perubahan dan pengguna yang melakukan perubahan. |

# 8. Kesimpulan

Model awal proses As-Is menunjukkan bahwa pelaporan dana donasi mencakup penerimaan data, pencatatan transaksi, rekapitulasi, pemeriksaan, persetujuan, dan publikasi laporan kepada masyarakat. Analisis lanjutan diperlukan untuk memastikan bagaimana proses tersebut benar-benar dilaksanakan pada lembaga yang menjadi objek penelitian. Potensi permasalahan yang telah divalidasi dapat menjadi dasar untuk merancang sistem yang meningkatkan keteraturan data, ketertelusuran transaksi, efisiensi penyusunan laporan, dan transparansi informasi kepada publik.

# 9. Acuan Standar

ISO/IEC/IEEE 29148:2018 — Systems and software engineering — Life cycle processes — Requirements engineering. Standar ini digunakan sebagai acuan umum dalam proses rekayasa kebutuhan dan pendokumentasian kebutuhan sistem. Dokumen ini merupakan penerapan praktis, bukan pernyataan bahwa setiap tabel atau alur di dalamnya diwajibkan secara persis oleh standar.

Sumber resmi: https://www.iso.org/standard/72089.html

# Lampiran: Pertanyaan Wawancara untuk Validasi As-Is

1. Bagaimana proses pencatatan dana donasi yang masuk saat ini?
2. Bagaimana data penyaluran dana dicatat dan diverifikasi?
3. Siapa yang menyusun, memeriksa, dan menyetujui laporan?
4. Media apa yang digunakan untuk memublikasikan laporan kepada masyarakat?
5. Seberapa sering laporan diperbarui?
6. Apa kendala yang paling sering terjadi dalam proses pelaporan?
7. Informasi apa saja yang boleh dilihat masyarakat dan informasi apa yang harus dibatasi?
