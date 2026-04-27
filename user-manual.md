# ![](media/image1.png){width="6.0in" height="1.9166666666666667in"}![](media/image3.jpeg){width="8.510416666666666in" height="11.0in"} {#section .unnumbered}

# PENDAHULUAN

Aplikasi eFeeder adalah aplikasi yang akan mengintegrasikan data dari eAkademik ke Neo Feeder PDDIKTI, sehingga pelaporan data ke Neo Feeder PDDIKTI dapat dilakukan lebih mudah. Berikut ini adalah arsitektur integrasi eFeeder.

eFeeder akan mengintegrasikan data yang ada di eAkademik ke Neo Feeder PDDIKTI, yang kemudian akan digunakan untuk pelaporan data perguruan tinggi ke PDDIKTI. Di aplikasi Neo Feeder PDDIKTI, proses input data masih harus dilakukan satu per satu. Sementara itu, di aplikasi eAkademik telah ada data -- data yang diperlukan untuk pelaporan.

Terdapat 2 file yang nantinya akan diinstall dalam penggunaan eFeeder yaitu; eFeeder sebagai aplikasi yang nantinya akan diakses, dan eFeeder_services yang akan dipasang pada server aplikasi eAkademik

![](media/image4.png){width="4.069444444444445in" height="4.069444444444445in"}

Di database eAkademik, akan ditambahkan tabel -- tabel dengan prefix feeder\_ atau tabel penampung data akademik yang fungsinya adalah sebagai tabel yang akan menampung data -- data eFeeder yang akan digunakan untuk pelaporan. Setiap ada perubahan data atau copy data dari Neo Feeder PDDIKTI tidak akan mengubah data di aplikasi eAkademik, tetapi hanya akan mengubah data yang ada di tabel **feeder\_**.

Selain integrasi yang sudah dijelaskan diatas, berikut akan dijelaskan terkait dengan prinsip pelaporan menggunakan eFeeder, alurnya sebagai berikut:

> ![](media/image5.png){width="4.405555555555556in" height="1.3125in"}![](media/image6.png){width="4.405555555555556in" height="1.3125in"}![](media/image7.png){width="4.405555555555556in" height="1.3125in"}

Prinsip yang dilakukan oleh aplikasi eFeeder adalah mengirimkan data dari eAkademik lalu akan diolah oleh eFeeder, kemudian dikirim ke Neo Feeder PDDIKTI. eAkademik menjadi sumber data untuk melakukan pelaporan. eFeeder hanya akan berperan aktif untuk mengambil dan mengirimkan data. Bisa disimpulkan, eFeeder adalah sebuah jembatan untuk melakukan pelaporan antara eAkademik dengan Neo Feeder PDDIKTI.

Data -- data yang wajib dilaporkan ke Dikti pada setiap periode pelaporan dibedakan menjadi 2, yaitu data master / data non transaksi dan data transaksi. Data master / data non transaksi yang perlu dilaporkan adalah :

-   Mahasiswa (termasuk status aktif, history pendidikan, dan mahasiswa transfer)

-   Bobot nilai

-   Kurikulum

-   Matakuliah

-   Kurikulum matakuliah

-   RPS

-   Rencana Evaluasi

Sedangkan data transaksi yang wajib dilaporkan adalah :

-   Kelas kuliah

-   Ajar dosen

-   Nilai

-   Nilai transfer

-   Kuliah mahasiswa

-   Aktivitas mahasiswa

-   Prestasi

-   Konversi Nilai

-   Komponen Evaluasi

Selain data -- data tersebut, ada **data dosen dan data program studi (sms)** yang perlu dilaporkan, tetapi hanya bisa dientry dari PDDIKTI. Jadi sebelum pelaporan, pastikan bahwa data dosen dan data prodi sudah terdaftar di PDDIKTI. Jika data tersebut belum ada, maka data pelaporan dengan prodi / dosen tersebut tidak akan ikut disertakan.

Untuk mengecek apakah kode prodi sudah sesuai dengan kode yang terdaftar di PDDIKTI, dapat dilihat di eAkademik. Buka menu **Program Studi Manajemen Program Studi Detail.**

![](media/image11.png){width="6.53125in" height="1.0604166666666666in"}

Selain kode prodi harus sesuai dengan data yang ada di forlap Dikti, status prodi di eAkademik juga harus aktif. Cek status aktif prodi dengan buka menu **Program Studi Manajemen Program Studi Detail.**

![](media/image12.png){width="6.53125in" height="0.74375in"}

## Bisnis Proses Aplikasi & Flowchart

> Berikut ditunjukkan bisnis proses aplikasi eFeeder
>
> Ada langkah utama yang dilakukan ketika menggunakan aplikasi eFeeder untuk upload data ke Neo Feeder PDDIKTI yaitu proses sinkronisasi data non transaksi dan sinkronisasi data transaksi. Berikut flowchart proses sinkronisasi data menggunakan eFeeder. Proses sinkronisasi harus dilakukan sesuai urutan, mulai dari data non transaksi, kemudian data transaksi.

# LOGIN eFeeder

Aplikasi **eFeeder** menerapkan mekanisme **login dua tahap** untuk menjamin keamanan akses serta memastikan integrasi data antara layanan Neo Feeder **PDDIKTI** dan sistem akademik internal kampus **eCampuz**.

Proses login dilakukan secara berurutan, dimulai dari autentikasi akun **NEO Feeder PDDIKTI**, kemudian dilanjutkan dengan autentikasi akun **eAkademik eCampuz** hingga pengguna berhasil masuk ke **halaman beranda aplikasi eFeeder**.

## 2.1 Login Tahap Pertama {#login-tahap-pertama .unnumbered}

Login tahap pertama digunakan untuk melakukan autentikasi awal ke layanan Neo Feeder PDDIKTI, menggunakan akun Neo Feeder PDDIKTI.

### Langkah-langkah Login pada Tahap Pertama : {#langkah-langkah-login-pada-tahap-pertama .unnumbered}

1.  Akses halaman login aplikasi eFeeder melalui browser

2.  Pastikan halaman menampilkan informasi\
    **"Login pertama menggunakan akun NEO Feeder"**

3.  Pastikan indikator akun berada pada **Akun NEO Feeder**

4.  Masukkan **Username akun NEO Feeder PDDIKTI**

5.  Masukkan **Password akun NEO Feeder PDDIKTI**

6.  Klik tombol **LOGIN**

7.  Tunggu hingga proses autentikasi selesai

![](media/image13.png){width="6.53125in" height="3.2819444444444446in"}

### Keberhasilan Login Tahap Pertama ditunjukkan dengan : {#keberhasilan-login-tahap-pertama-ditunjukkan-dengan .unnumbered}

-   Sistem menampilkan **tanda centang hijau** pada indikator **Akun NEO Feeder**

-   Pengguna otomatis diarahkan ke halaman **Login Tahap Kedua**

![](media/image14.png){width="6.53125in" height="3.316666666666667in"}

## 2.2 Login Tahap Kedua {#login-tahap-kedua .unnumbered}

**Menggunakan Akun eAkademik eCampuz**

Login tahap kedua digunakan untuk menghubungkan aplikasi eFeeder dengan sistem akademik internal kampus (eCampuz) dengan **Menggunakan Akun eAkademik eCampuz**

### Langkah-langkah Login pada tahap kedua : {#langkah-langkah-login-pada-tahap-kedua .unnumbered}

1.  Pastikan halaman menampilkan informasi\
    **"Login kedua menggunakan akun eAkademik"**

2.  Pastikan indikator **Akun NEO Feeder** telah bertanda **centang hijau**

3.  Masukkan **Username akun eAkademik eCampuz**

4.  Masukkan **Password akun eAkademik eCampuz**

5.  Klik tombol **LOGIN**

6.  Tunggu proses verifikasi sistem

![](media/image15.png){width="6.53125in" height="3.2194444444444446in"}

### Keberhasilan Login Tahap Pertama ditunjukkan dengan : {#keberhasilan-login-tahap-pertama-ditunjukkan-dengan-1 .unnumbered}

-   Sistem mengarahkan pengguna ke **halaman Beranda aplikasi eFeeder**

-   Aplikasi siap digunakan untuk proses sinkronisasi dan pelaporan data Neo Feeder PDDIKTI

![](media/image16.png){width="6.53125in" height="3.408333333333333in"}

## 2.3 Beranda {#beranda .unnumbered}

Halaman **Beranda** pada aplikasi **eFeeder** berfungsi sebagai **dashboard monitoring** yang menampilkan **informasi perbandingan data** antara **Sistem Informasi Akademik (SIA / eAkademik)** dengan **Neo Feeder PDDIKTI**.

Melalui halaman ini, operator dapat mengetahui **kesesuaian jumlah data**, **potensi selisih data**, serta menentukan **tindak lanjut sinkronisasi atau perbaikan data** sebelum proses pelaporan dilakukan.

Halaman Beranda digunakan untuk:

-   Menampilkan perbandingan jumlah data antara **SIA (eAkademik)** dan **Neo Feeder**

-   Mengetahui adanya **selisih data** antara **SIA (eAkademik)** dan **Neo Feeder**

-   Membantu operator melakukan **kontrol kualitas data pelaporan**

-   Menjadi titik awal sebelum melakukan sinkronisasi atau perbaikan data

Di bagian atas halaman Beranda tersedia **filter pencarian** yang digunakan untuk menentukan data yang akan ditampilkan.

### Komponen Filter: {#komponen-filter .unnumbered}

-   **Semester**\
    Digunakan untuk memilih semester pelaporan yang akan dianalisis.

-   **Program Studi**\
    Digunakan untuk memfilter data berdasarkan program studi tertentu.

-   **Jenis Data**\
    Digunakan untuk memilih jenis data akademik yang ingin ditampilkan.

### Tombol Aksi: {#tombol-aksi .unnumbered}

-   **Tampilkan**\
    Menampilkan data perbandingan sesuai filter yang dipilih.

-   **Reset**\
    Mengosongkan seluruh filter pencarian.

Catatan:\
Seluruh field filter wajib diisi sebelum data dapat ditampilkan.

![](media/image17.png){width="6.53125in" height="3.3520833333333333in"}

Setelah filter dipilih dan tombol **Tampilkan** diklik, sistem akan menampilkan **panel perbandingan data SIA dengan Neo Feeder**.

Jenis data yang ditampilkan meliputi:

-   Kurikulum

-   Mata Kuliah Kurikulum

-   Mahasiswa

-   Kelas

-   KRS

-   KRS Nilai

-   Nilai Transfer

Setiap panel menampilkan informasi ringkas jumlah data dan status perbandingan.

Informasi perbandingan pada setiap panel terdiri dari:

-   **Jumlah Data di SIA (eAkademik)**\
    Menunjukkan total data yang tercatat di sistem akademik kampus.

-   **Jumlah Data di Neo Feeder**\
    Menunjukkan total data yang sudah tercatat di Neo Feeder PDDIKTI.

-   **Selisih Data**\
    Menunjukkan perbedaan jumlah data antara SIA dan Neo Feeder.

Selisih dihitung dari perbandingan jumlah data di SIA dengan jumlah data di Neo Feeder.

![](media/image18.png){width="6.53125in" height="3.370833333333333in"}

## Keterangan Selisih Data {#keterangan-selisih-data .unnumbered}

Di bagian bawah halaman Beranda tersedia **keterangan selisih data** sebagai panduan interpretasi hasil perbandingan.

Keterangan tersebut menjelaskan bahwa:

-   **Tidak ada selisih**\
    Jumlah data di SIA sama dengan jumlah data di Neo Feeder.

-   **Data di SIA lebih banyak**\
    Terdapat data di sistem akademik yang belum tersinkron ke Neo Feeder.

-   **Data di SIA lebih sedikit**\
    Terdapat data di Neo Feeder yang tidak atau belum tercatat di SIA.

![](media/image19.png){width="6.53125in" height="3.3715277777777777in"}

# PROSES INISIASI

Proses inisiasi dilakukan [hanya satu kali]{.underline} pada saat pertamakali menggunakan aplikasi eFeeder setelah berhasil diinstall. Jika sudah melakukan proses inisasi, maka pada periode pelaporan selanjutnya tidak perlu menjalankan proses sinkronisasi awal.

Proses -- proses yang termasuk dalam proses inisiasi adalah :

-   Buat Tabel Feeder di database

-   Pencocokan Kode PT

-   Pemetaan Program Studi

-   Pencocokan Data Referensi

-   Pengaturan Periode

-   Pemetaan ID Pembiayaan

-   Pemetaan Pembiayaan

-   Pemetaan Jalur Masuk

Terdapat juga menu tambahan **Info dari PDDIKTI** untuk menampilkan data dosen yang ada di data eAkademik yang belum terdaftar di PDDIKTI. Tujuannya adalah supaya dari perguruan tinggi mengetahui dosen siapa saja yang perlu didaftarkan ke PDDIKTI agar datanya bisa masuk dan digunakan untuk pelaporan.

## Pembuatan Table Feeder

Pada tahapan ini, table dengan prefiks feeder\_ akan dibuat di database aplikasi eAkademik. Secara aplikasi, tabel-tabel tersebut tidak terlihat namun jika dicek secara teknis di database eAkademik, akan ada tabel-tabel baru dengan prefiks feeder\_. Tabel feeder fungsinya adalah sebagai penampung dari data -- data yang akan dikirimkan ke Neo Feeder PDDIKTI. Untuk create tabel feeder di database, pilih menu **Inisiasi**, lalu klik tombol **Pembuatan Table Feeder.**

![](media/image20.png){width="5.65625in" height="4.584904855643044in"}![](media/image21.png){width="2.2875371828521436in" height="3.861634951881015in"}

Tunggu beberapa saat sampai ada notifikasi bahwa proses telah selesai. Setelah selesai, di database aplikasi eAkademik akan terdapat tabel-tabel dengan prefix **feeder\_**. Setiap ada penambahan data baru atau perubahan data, akan tersimpan pada tabel tersebut sehingga tidak akan mengganggu data-data yang ada di aplikasi eAkademik.

**Note : setelah proses pembuatan table feeder selesai, maka proses dianggap telah selesai dilakukan sehingga proses tidak bisa dijalankan lagi.**

**Tetapi untuk mengganti status proses ketika ada kebutuhan untuk melakukan proses pembuatan table lagi, akan dijelaskan pada langkah 3.5**

## Pencocokan Kode PT (Perguruan Tinggi)

> Pada saat awal menggunakan eFeeder, perlu dicek apakah kode perguruan tinggi pada eFeeder yang sudah terinstall sudah sama dengan kode perguruan tinggi dari PDDIKTI (yang digunakan di Neo Feeder PDDIKTI). Jika kode perguruan tinggi di eFeeder belum sesuai, maka proses -- proses selanjutnya juga tidak dapat dilakukan. Pengecekan kode perguruan tinggi dilakukan di menu **Inisasi** lalu pilih sub-menu **Pencocokan Kode PT.**

![](media/image22.png){width="6.53125in" height="1.9347222222222222in"}

> Pada halaman Pencocokan Kode PT (Perguruan Tinggi), pastikan bahwa nama perguruan tinggi dan kodenya sudah sesuai dengan kode yang digunakan pada Neo Feeder PDDIKTI. Jika sudah muncul nama perguruan tinggi yang dimaksud dan kodenya sudah sesuai, maka proses match kode perguruan tinggi tidak perlu dilakukan. Jika belum sesuai, klik tombol **Edit.**
>
> Setelah muncul nama-nama perguruan tinggi, cari nama perguruan tinggi yang sesuai. Untuk mempermudah pencarian, operator dapat mengetikkan nama perguruan tinggi yang dimaksud dan setelah muncul nama perguruan tinggi yang dimaksud, klik pada nama perguruan tinggi. Kemudian klik **Save.**

![](media/image23.png){width="6.53125in" height="1.7472222222222222in"}

## Pemetaan Program Studi

> Pemetaan program studi dilakukan untuk menentukan data dari prodi mana saja yang akan dikirim ke Neo Feeder PDDIKTI ketika pelaporan. Jika kode program studi belum dipetakan, maka semua data yang berkaitan dengan program studi tersebut tidak akan terbawa saat pelaporan. Langkah untuk melakukan pemetaan program studi adalah :

1.  Masuk ke menu **Inisiasi Pemetaan Program Studi**

2.  Jika ada program studi yang masih belum match antara prodi yang ada di eAkademik dengan prodi di Neo Feeder PDDIKTI, klik tombol **Edit**

![](media/image24.png){width="6.53125in" height="2.01875in"}

> Prodi yang belum match dengan Neo Feeder PDDIKTI dapat diketahui dari kolom **prodiKodeDikti** dan **dikti_label** yang masih kosong atau tanda strip ( - ). Jika pada kolom tersebut pada suatu prodi masih kosong atau bertanda strip seperti pada contoh di atas, maka perlu dipetakan dahulu untuk program studinya. Tetapi jika memang data -- data pada suatu prodi tidak disertakan pada pelaporan, maka pada kolom **prodiKodeDikti** dan **dikti_label** dibiarkan kosong atau bertanda strip ( - ).
>
> Atau jika akan menghapus pemetaan program studi, karena data prodi tidak disertakan dalam pelaporan, maka klik tombol **Reset**.

![](media/image25.png){width="6.53125in" height="1.601388888888889in"}

3.  Setelah muncul pilihan nama -- nama prodi, pilih salah satu prodi yang sesuai dengan prodi yang akan di-match. Untuk mempermudah pencarian, nama prodi dapat diketik di field pencarian yang telah tersedia.

![](media/image26.png){width="6.53125in" height="1.9166666666666667in"}

4.  Jika program studi yang sudah sesuai dengan prodi yang telah ditentukan, klik **Save**

![](media/image29.png){width="6.53125in" height="1.6152777777777778in"}

## Pencocokan Data Referensi

Proses ini dilakukan untuk mencocokan antara data referensi dari Neo Feeder PDDIKTI dengan data referensi yang ada di aplikasi eAkademik. Misalnya pada data agama, Agama Kristen yang terdaftar di PDDIKTI adalah Kristen tetapi di eAkademik terdaftar dengan nama Protestan. Data ini perlu dicocokkan antara data agama Kristen yang terdaftar di Dikti dengan data Protestan yang ada di eAkademik, karena sebenarnya data tersebut sama maksudnya. Jika tidak di-*match*-kan, maka akan terjadi kegagalan untuk sinkronisasi ke Neo Feeder PDDIKTI pada data yang menggunakan data agama Protestan di eAkademik. Jadi jika tidak di-*match*-kan dulu, agama Protestan pada mahasiswa tidak akan terbawa pada saat pelaporan, karena di Neo Feeder PDDIKTI nama agama yang dikenali adalah agama Kristen. Kemudian untuk data referensi lainnya juga sama seperti ilustrasi contoh kasus tersebut.

Langkah-langkah untuk match data referensi adalah sebagai berikut :

1.  Pilih menu **Inisiasi**, lalu klik **Pencocokan Data Referensi.**

2.  Klik nama tabel yang akan dicocokkan, misalnya untuk mencocokkan data agama maka klik **Ref Agama**. Akan ditampilkan data referensi agama dari Neo Feeder PDDIKTI dan data referensi agama dari eAkademik.

![](media/image30.png){width="6.53125in" height="2.3625in"}

3.  Jika ada data referensi dari eAkademik yang tidak terisi artinya data referensi di eAkademik tidak cocok dengan data yang ada di Neo Feeder PDDIKTI. Untuk menyesuaikan dengan data yang ada di Neo Feeder PDDIKTI, klik tombol **Edit** pada kolom data yang akan dicocokan

![](media/image31.png){width="6.53125in" height="2.548611111111111in"}

> Misalnya pada data referensi agama Khonghucu, di data Neo Feeder PDDIKTI tertulis Khonghucu. Sedangkan yang ada di database eAkademik adalah masih kosong, sehingga data ini perlu dicocokan. Caranya adalah cari data *Khonghucu* di kolom **gt_id** lalu klik tombol **Save**.

4.  Lakukan langkah yang sama pada semua tabel data referensi lainnya sampai semua tabel telah dicocokan.

**Note : Apabila ada data referensi di Neo Feeder PDDIKTI tetapi tidak ada di eAkademik, maka abaikan untuk pencocokan data referensi tersebut karena di eAkademik tidak ada data yang menggunakan data referensi tersebut dan tidak mempengaruhi pelaporan.**

> Misalnya pada saat match data referensi Ikatan Kerja Dosen, pada data referensi dari Neo Feeder PDDIKTI ada data DOSEN TIDAK TETAP. Ketika di klik tombol **Edit** untuk di-*match*-kan dengan data referensi dari eAkademik, maka akan muncul data -- data referensi ikatan kerja dosen yang ada di eAkademik.

![](media/image32.png){width="5.593751093613299in" height="1.9916557305336833in"}![](media/image33.png){width="4.229166666666667in" height="1.5070680227471567in"}

Kemudian setelah dicari data referensi di eAkademik tidak ada yang cocok dengan data referensi DOSEN TIDAK TETAP. Maka untuk data yang seperti ini bisa dikosongkan saja ketika match data referensi.

Data -- data referensi yang perlu di-*match*-kan adalah data agama, ikatan kerja dosen, pangkat golongan, jenjang pendidikan, status mahasiswa, negara, wilayah, pekerjaan, penghasilan, status aktif pegawai, dan status kepegawaian. Langkahnya hampir sama dengan langkah match data seperti pada contoh yang telah ditunjukkan di atas.

## Pengaturan Periode

Menu **Pengaturan Periode** pada aplikasi **eFeeder** digunakan untuk menentukan **periode atau semester aktif** yang akan digunakan dalam proses **pelaporan data ke Neo Feeder PDDIKTI**.\
Periode yang dipilih pada menu ini akan menjadi **acuan utama** bagi seluruh proses sinkronisasi dan pelaporan data akademik.

Pengaturan Periode berfungsi untuk:

-   Menetapkan **semester pelaporan aktif**

-   Menyesuaikan data yang ditampilkan dan diproses pada menu lain

-   Memastikan data yang dilaporkan sesuai dengan semester yang berjalan

-   Menghindari kesalahan pelaporan lintas semester

## Langkah-Langkah Pengaturan Periode :  {#langkah-langkah-pengaturan-periode .unnumbered}

### **1. Mengakses Menu Pengaturan Periode :** {#mengakses-menu-pengaturan-periode .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pada menu utama, pilih **Inisiasi**

3.  Klik submenu **Pengaturan Periode**

### **2. Memilih Periode Pelaporan** {#memilih-periode-pelaporan .unnumbered}

1.  Pada halaman **Pengaturan Pelaporan**, klik dropdown **Periode/Semester**

2.  Pilih semester yang akan dijadikan **periode pelaporan aktif**\
    Contoh: *2024/2025 Ganjil*

### **3. Menetapkan Periode Aktif** {#menetapkan-periode-aktif .unnumbered}

1.  Setelah periode dipilih, klik tombol **Set Periode**

2.  Sistem akan memproses dan menyimpan pengaturan periode

![](media/image34.png){width="6.53125in" height="1.7951388888888888in"}

## Reset Table

> Menu reset table difungsikan untuk mengembalikan data -- data di table feeder di database, supaya keadaan data di eFeeder sama dengan data yang ada di Neo Feeder PDDIKTI saat melakukan proses reset table tersebut. Ini hampir mirip dengan proses Pembuatan Table Feeder. Bedanya yaitu di proses reset table, operator dapat memilih tabel mana yang akan direset. Sedangkan pada proses pembuatan table feeder, yang diproses adalah semua tabel feeder. Jadi proses reset table ini jauh lebih cepat daripada proses pembuatan table feeder, karena yang diproses hanya tabel -- tabel tertentu yang sesuai pilihan operator.
>
> Contoh kejadian; misalnya operator menambahkan data mahasiswa 'A' langsung dari Neo Feeder PDDIKTI, maka data mahasiswa yang ditambahkan tersebut tidak ada dalam tabel feeder di database. Jadi ketika melaporkan data -- data lain yang berkaitan dengan mahasiswa tersebut di eFeeder akan bermasalah. Solusinya adalah, data mahasiswa 'A' tersebut harus ada di tabel feeder supaya dapat diproses dengan eFeeder. Maka untuk menambahkan data mahasiswa 'A' tersebut supaya ada di tabel feeder, dapat menggunakan Reset Table. Setelah melakukan reset table untuk data mahasiswa dan data mahasiswa 'A' tersebut sudah ada di tabel feeder, untuk pelaporan data lainnya yang berkaitan dengan mahasiswa tersebut sudah bisa dilakukan kembali.

Langkah untuk melakukan proses reset table adalah :

1.  Masuk ke menu **Inisiai**

2.  Pilih **Reset Table**

![](media/image35.png){width="6.53125in" height="1.9493055555555556in"}

3.  Cari nama tabel yang akan di-*reset*.

Misalnya pada kasus seperti yang telah dicontohkan di atas, maka yang perlu di-*reset* adalah tabel mahasiswa. Cari nama tabel mahasiswa pada filter pencarian yang tersedia.

![](media/image36.png){width="6.53125in" height="2.567361111111111in"}

4.  Klik tombol **Reset** pada tabel yang akan di-reset datanya, dan tunggu hingga ada pemberitahuan bahwa proses telah selesai

![](media/image37.png){width="6.53125in" height="2.8784722222222223in"}

## Pengaturan Module

> Menu pengaturan modul ini digunakan ketika akan mengubah status dari proses -- proses yang dilakukan pada saat sinkronisasi awal. Seperti misalnya pada langkah Pembuatan Table Feeder, jika sudah selesai maka proses tidak dapat dijalankan lagi seperti pada gambar berikut
>
> ![](media/image38.png){width="5.229166666666667in" height="1.8265715223097112in"}
>
> Jika ada keperluan untuk mengulangi proses lagi, user tetap dapat mengubah status prosesnya di menu **Pengaturan Modul**. Langkahnya adalah :

1.  Masuk ke menu **Inisiasi**

2.  Pilih **Pengaturan Modul,** kemudian akan ditampilkan status proses dari setiap proses yang dilakukan pada saat sinkronisasi awal.

![](media/image40.png){width="6.53125in" height="2.1180555555555554in"}

> **Note : Status proses "1" menunjukkan bahwa proses telah selesai (user sudah melakukan klik pada tanda cek saat melakukan proses di sinkronisasi awal). Sedangkan status proses "0" menunjukkan bahwa proses belum dianggap selesai meskipun data -- data eFeeder telah berubah sesuai proses sinkronisasi awal yg telah dilakukan (setelah selesai melakukan proses, user tidak klik tanda cek).**

3.  Untuk mengubah status proses, klik tanda panah pada proses yang ingin diubah statusnya. Misalnya akan mengubah status proses Pembuatan Table Feeder untuk mengulangi proses create table lagi, maka status proses di Create Table diganti menjadi 0. Kemudian klik **Simpan**.

![](media/image41.png){width="6.53125in" height="1.7131944444444445in"}

> Setelah muncul pemberitahuan bahwa proses setting modul berhasil, artinya status untuk proses Pembuatan Table Feeder sudah bisa dilakukan lagi dengan langkah seperti biasa.

## Pemetaan ID Pembiayaan

Pada **Neo Feeder PDDIKTI**, referensi **ID Pembiayaan** terdiri dari tiga kategori utama, yaitu:

1.  **Beasiswa Penuh**

2.  **Beasiswa Tidak Penuh**

3.  **Mandiri**

Sementara itu, pada **Sistem Akademik (eAkademik)**, referensi pembiayaan dapat memiliki struktur dan penamaan yang berbeda dengan Neo Feeder.\
Agar proses pelaporan data ke Neo Feeder PDDIKTI berjalan dengan benar, diperlukan **pemetaan ID Pembiayaan** supaya data pembiayaan di sistem akademik **sesuai (match)** dengan referensi Neo Feeder.

Aplikasi eFeeder menyediakan **dua metode pemetaan ID Pembiayaan**, dan **perguruan tinggi dapat memilih salah satu metode** sesuai kebijakan internal.

Terdapat dua metode pemetaan yang tersedia di eFeeder:

1.  **Pemetaan ID Pembiayaan Based UKT**

2.  **Pemetaan ID Pembiayaan Based Sumber Dana**

### **3.7.1 Pemetaan ID Pembiayaan Based UKT** {#pemetaan-id-pembiayaan-based-ukt .unnumbered}

Metode ini digunakan apabila penentuan jenis pembiayaan mahasiswa **mengacu pada kelompok UKT**. Langkah-Langkah Pemetaan:

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Inisiasi**

3.  Klik submenu **Pemetaan ID Pembiayaan Based UKT**

4.  Halaman daftar pemetaan akan ditampilkan

5.  Klik tombol **Tambah**

![](media/image42.png){width="6.53125in" height="2.175in"}

### Form Tambah Pemetaan (Based UKT) : {#form-tambah-pemetaan-based-ukt .unnumbered}

1.  Pilih **ID Pembiayaan**\
    Contoh: *Beasiswa Penuh / Beasiswa Tidak Penuh / Mandiri*

2.  Pilih **UKT** yang sesuai\
    Contoh: *UKT 1, UKT 2, dst.*

3.  Pastikan seluruh kolom bertanda **(\*)** telah diisi

4.  Klik tombol **Simpan** untuk menyimpan pemetaan

5.  Klik **Batal** jika ingin membatalkan proses

![](media/image43.png){width="6.53125in" height="2.1631944444444446in"}

### Hasil: {#hasil .unnumbered}

-   Data pemetaan akan tampil pada tabel

-   ID Pembiayaan di Neo Feeder akan mengikuti pemetaan berdasarkan UKT

### **3.7.2 Pemetaan ID Pembiayaan Based Sumber Dana** {#pemetaan-id-pembiayaan-based-sumber-dana .unnumbered}

Metode ini digunakan apabila penentuan jenis pembiayaan mahasiswa **mengacu pada sumber dana**. Langkah-Langkah Pemetaan:

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Inisiasi**

3.  Klik submenu **Pemetaan ID Pembiayaan Based Sumber Dana**

4.  Halaman daftar pemetaan akan ditampilkan

5.  Klik tombol **Tambah**

![](media/image44.png){width="6.53125in" height="2.3180555555555555in"}

### Form Tambah Pemetaan (Based Sumber Dana) : {#form-tambah-pemetaan-based-sumber-dana .unnumbered}

1.  Pilih **ID Pembiayaan**\
    Contoh: *Beasiswa Penuh / Beasiswa Tidak Penuh / Mandiri*

2.  Pilih **Sumber Dana**\
    Contoh: *Beasiswa, Lain-lain, Orang Tua Asuh, Orang Tua/Wali, Sendiri*

3.  Pastikan seluruh kolom bertanda **(\*)** telah diisi

4.  Klik tombol **Simpan** untuk menyimpan pemetaan

5.  Klik **Batal** jika ingin membatalkan proses

![](media/image45.png){width="6.53125in" height="2.214583333333333in"}

### Hasil: {#hasil-1 .unnumbered}

-   Data pemetaan akan tersimpan dan tampil di tabel

-   ID Pembiayaan Neo Feeder akan ditentukan berdasarkan sumber dana

## Pemetaan Pembiayaan

Menu **Pemetaan Pembiayaan** pada aplikasi **eFeeder** digunakan untuk menentukan **sumber perhitungan total nominal pembiayaan** yang akan dilaporkan ke **Neo Feeder PDDIKTI**.

Pemetaan ini berperan penting dalam:

-   Pelaporan **Biaya Masuk** pada data **mahasiswa baru** (history pendidikan -- master mahasiswa)

-   Pelaporan **Biaya per Semester** pada data **aktivitas kuliah mahasiswa**

Dengan pemetaan yang benar, sistem eFeeder dapat menarik dan menjumlahkan nominal pembiayaan dari sistem akademik sesuai aturan pelaporan PDDIKTI. Pemetaan Pembiayaan berfungsi untuk:

-   Menentukan **jenis transaksi keuangan** yang dihitung sebagai pembiayaan

-   Mengatur apakah suatu pembayaran dihitung sebagai:

    -   **Biaya Masuk**

    -   **Biaya Semester**

-   Menghasilkan **total nominal pembiayaan** yang akurat saat proses sinkronisasi ke Neo Feeder

Aplikasi eFeeder menyediakan **dua metode pemetaan**, dan **perguruan tinggi dapat memilih salah satu metode** sesuai kebijakan internal:

1.  **Pemetaan Pembiayaan Based Jenis Pembayaran**

2.  **Pemetaan Pembiayaan Based Jenis Biaya**

### **3.8.1 Pemetaan Pembiayaan Based Jenis Pembayaran** {#pemetaan-pembiayaan-based-jenis-pembayaran .unnumbered}

Metode ini digunakan apabila perhitungan pembiayaan mengacu pada **jenis pembayaran** (misalnya: registrasi, uang pangkal, daftar ulang, dll).

### Langkah-Langkah: {#langkah-langkah .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Inisiasi**

3.  Klik submenu **Pemetaan Pembiayaan Based Jenis Pembayaran**

4.  Halaman daftar pemetaan akan ditampilkan

5.  Klik tombol **Tambah**

![](media/image46.png){width="6.53125in" height="2.2256944444444446in"}

### Form Tambah Pemetaan (Based Jenis Pembayaran) : {#form-tambah-pemetaan-based-jenis-pembayaran .unnumbered}

1.  Pilih **Jenis Pembayaran**\
    Contoh: *01 Registrasi*

2.  Pada field **Atur sebagai**, pilih kategori pembiayaan:

    -   **Biaya Masuk**

    -   **Biaya per Semester**

3.  Pastikan seluruh kolom bertanda **(\*)** telah diisi

4.  Klik tombol **Simpan** untuk menyimpan pemetaan

5.  Klik **Batal** untuk membatalkan proses

![](media/image47.png){width="6.53125in" height="2.5659722222222223in"}

### Hasil: {#hasil-2 .unnumbered}

-   Jenis pembayaran tersebut akan dihitung dalam total pembiayaan

-   Nominalnya akan ditarik saat proses pelaporan mahasiswa baru atau aktivitas kuliah

### **3.8.2 Pemetaan Pembiayaan Based Jenis Biaya** {#pemetaan-pembiayaan-based-jenis-biaya .unnumbered}

Metode ini digunakan apabila perhitungan pembiayaan mengacu pada **jenis biaya akademik** (misalnya: SKS teori, SKS praktik, biaya laboratorium, dll).

### Langkah-Langkah: {#langkah-langkah-1 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Inisiasi**

3.  Klik submenu **Pemetaan Pembiayaan Based Jenis Biaya**

4.  Halaman daftar pemetaan akan ditampilkan

5.  Klik tombol **Tambah**

![](media/image48.png){width="6.53125in" height="2.082638888888889in"}

### Form Tambah Pemetaan (Based Jenis Biaya) {#form-tambah-pemetaan-based-jenis-biaya .unnumbered}

1.  Pilih **Jenis Biaya**\
    Contoh: *SKS Teori*

2.  Pada field **Atur sebagai**, pilih kategori pembiayaan:

    -   **Biaya Masuk**

    -   **Biaya per Semester**

3.  Pastikan seluruh kolom bertanda **(\*)** telah diisi

4.  Klik tombol **Simpan** untuk menyimpan pemetaan

5.  Klik **Batal** untuk membatalkan proses

![](media/image49.png){width="6.53125in" height="2.454861111111111in"}

### Hasil: {#hasil-3 .unnumbered}

-   Jenis biaya tersebut akan masuk dalam perhitungan total pembiayaan

-   Digunakan saat penarikan data aktivitas kuliah mahasiswa

## Info Data dari PDDIKTI

> Proses ini dilakukan untuk [menampilkan informasi]{.underline} data dosen yang ada di eAkademik tetapi tidak terdata di Neo Feeder PDDIKTI, sehingga pihak perguruan tinggi bisa segera mendaftarkan dosen yang bersangkutan agar datanya tercatat di Neo Feeder PDDIKTI. Langkah untuk menampilkan data tersebut adalah :

1.  Masuk ke menu **Info dari PDDIKTI**.

2.  Pilih **Data Dosen**

![](media/image50.png){width="6.53125in" height="3.1618055555555555in"}

> Setelah itu akan muncul nama -- nama dosen di eAkademik yang belum terdaftar di Neo Feeder PDDIKTI.

# PROSES PELAPORAN

Proses pelaporan dilakukan pada saat pelaporan rutin setiap semester berikutnya. Proses ini merupakan proses utama dari aplikasi eFeeder ini. Inti dari proses pelaporan dengan eFeeder ini adalah pada proses Sinkronisasi Data Transaksi dan Sinkronisasi Data Non Transaksi. Pada proses Sinkronisasi data, baik data transaksi maupun data non transaksi, eFeeder akan mengambil data dari eAkademik kemudian akan disimpan pada tabel penampung data (tabel *feeder* yang di create saat proses Create Table). Setelah data - data dari eAkademik tersebut di-*Sinkronisasi* ke Neo Feeder PDDIKTI, maka data dari tabel *feeder* akan dikirim ke Neo Feeder PDDIKTI. Jika sudah sesuai dengan kelengkapan data yang perlu diisikan di Neo Feeder PDDIKTI, maka data tersebut akan masuk ke Neo Feeder PDDIKTI, dan jika belum lengkap maka data tidak akan masuk ke Neo Feeder PDDIKTI dan akan menampilkan deskripsi error penyebab data tidak dapat masuk ke Neo Feeder PDDIKTI pada aplikasi eFeeder. Jika hat tersebut terjadi, maka cek deskripsi error penyebab data tidak bisa di-*Sinkronisasi* ke Neo Feeder PDDIKTI, lalu lengkapi kekurangan data itu dari eAkademik.

Inti dari proses pelaporan rutin di eFeeder yang akan diulang - ulang adalah pada proses Sinkronisasi Data (transaksi dan non transaksi). Secara keseluruhan, proses yang termasuk dalam proses pelaporan di eFeeder adalah :

1.  Sinkronisasi data referensi

2.  Sinkronisasi data non transaksi

3.  Sinkronisasi data transaksi

Untuk masuk ke tahapan pada proses utama, di halaman utama setelah berhasil login klik tombol **Pelaporan.**

![](media/image51.png){width="6.53125in" height="2.515972222222222in"}

## Sinkronisasi Data Referensi

> Sinkronisasi data referensi **hanya dilakukan** ketika ada perubahan data referensi (misalnya data referensi agama, jurusan, jenjang pendidikan, dll.) di Neo Feeder PDDIKTI. Data perubahan dari Neo Feeder PDDIKTI akan disesuaikan dengan data di eFeeder, sehingga keadaan data referensi akan menjadi sama antara di Neo Feeder PDDIKTI dan eFeeder. Langkah untuk melakukan proses Sinkronisasi Data Referensi adalah :

1.  Masuk ke menu **Pelaporan Sinkronisasi Data Referensi**

2.  Setelah masuk ke **Sinkronisasi Data Referensi,** lalu tunggu sampai proses selesai.

![](media/image52.png){width="6.53125in" height="2.1534722222222222in"}

**Note : Proses Sinkronisasi Data Referensi bisa dilewati. Proses ini hanya dilakukan ketika ada perubahan data referensi dari Neo Feeder PDDIKTI. Jika tidak ada perubahan, proses ini bisa diabaikan.**

## Pencocokan Data Referensi

> Proses Pencocokan Data Referensi pada Proses Utama ini sama dengan proses Pencocokan Data yang ada di Sinkronisasi Awal. Jika pada saat Sinkronisasi Awal sudah yakin bahwa semua data referensi sudah dicocokkan, maka proses Pencocokan Data pada Proses Utama ini dapat dilewati.

## Sinkronisasi Data

> Proses sinkronisasi data ini merupakan proses inti dari proses pelaporan yang akan dilakukan. Sinkronisasi data, baik data transaksi maupun data non transaksi akan sering dilakukan berulang-ulang sampai semua data yang akan dilaporkan berhasil masuk ke Neo Feeder PDDIKTI, untuk kemudian disinkronisasi ke PDDIKTI. Pada proses Sinkronisasi data (memasukkan data dari eFeeder ke Neo Feeder PDDIKTI), akan ada 2 istilah yang sering digunakan yaitu ***crawl*** dan ***Sinkronisasi***.
>
> ***Crawl*** adalah proses dimana eFeeder akan menyalin data dari eAkademik yang akan dilaporkan ke Neo Feeder PDDIKTI, dan kemudian data -- data tersebut diletakkan pada tabel penampung data akademik atau yang disebut dengan table feeder (yang dicreate pada saat proses Buat Tabel Feeder).
>
> ***Sinkronisasi*** adalah proses ketika mengirim data dari tabel penampung data akademik ke Neo Feeder PDDIKTI. Pada proses ini juga akan dicek kelengkapan data yang perlu dilaporkan ke Neo Feeder PDDIKTI. Jika bagian data dari eAkademik yang belum diisi tetapi data tersebut merupakan data yang wajib diisi di Neo Feeder PDDIKTI, maka ketika proses ***Sinkronisasi*** data tersebut akan ditolak (tidak dapat masuk ke Neo Feeder PDDIKTI). Ketika data ditolak karena kurang lengkap, operator dapat melengkapi data di eAkademik lalu lakukan ***crawl*** dan ***Sinkronisasi*** lagi hingga data berhasil masuk ke Neo Feeder PDDIKTI.

Proses ketika Sinkronisasi data dapat digambarkan sebagai berikut :

> Ketika ***crawl***, eFeeder akan mengambil data yang akan dilaporkan dari eAkademik. Kemudian data dari eAkademik yang diambil akan dicopy ke tabel penampung atau di tabel feeder.
>
> Pada proses ***Sinkronisasi*** data, data dari eAkademik yang telah ada di tabel penampung akan dicek dan dikirim ke Neo Feeder PDDIKTI.
>
> Yang terjadi pada saat proses Sinkronisasi data, akan ada juga pengecekan apakah data-data yang wajib diisi di Neo Feeder PDDIKTI juga sudah diisi di eAkademik. Jika data di eAkademik ada yang belum lengkap, maka akan terjadi gagal ketika proses ***Sinkronisasi*** dan data yang belum lengkap tersebut tidak akan masuk ke Neo Feeder PDDIKTI.

### Sinkronisasi Data Non Transaksi

> Proses ini akan melakukan sinkronisasi data non transaksi (data mahasiswa, bobot nilai, kurikulum, dan lain-lain) dari eAkademik ke Neo Feeder PDDIKTI. Pada proses ini, user dapat menambahkan data yang ada di eAkademik ke Neo Feeder PDDIKTI jika data non transaksi belum ada di Neo Feeder PDDIKTI, dan user dapat mengupdate data di Neo Feeder PDDIKTI jika pernah melakukan edit data dari eAkademik.
>
> Ketika akan melakukan insert data ke Neo Feeder PDDIKTI, gunakan menu-menu dengan pilihan **(Insert)** saja. Apabila akan melakukan pengubahan data yang sudah ada di Neo Feeder PDDIKTI, gunakan menu dengan pilihan **(Update).** Menu-menu dengan **(Update)** hanya dilakukan apabila akan mengubah data yang sudah masuk ke PDDIKTI saja, apabila tidak ada keperluan untuk mengubah data yang sudah masuk ke PDDIKTI, maka menu-menu dengan **(Update)** tidak perlu dilakukan.

### Sinkronisasi Data Non Transaksi - Mahasiswa (Insert)

> Menu **Mahasiswa (Insert)** pada aplikasi **eFeeder** digunakan untuk melakukan **pelaporan data mahasiswa baru** ke **Neo Feeder PDDIKTI**. Menu ini termasuk dalam **Sinkronisasi Data Non Transaksi**, yang berarti data yang dikirim bersifat **data master mahasiswa**, bukan data aktivitas perkuliahan. Menu ini digunakan **khusus untuk menambahkan data mahasiswa yang belum pernah tercatat di PDDIKTI**.
>
> Menu Mahasiswa (Insert) berfungsi untuk:

-   Mengambil data mahasiswa baru dari sistem akademik (eAkademik)

-   Menampilkan hasil data mahasiswa yang akan dikirim

-   Mengirim (insert) data mahasiswa ke Neo Feeder PDDIKTI

> Langkah-Langkah Penggunaan :

### **Mengakses Menu Mahasiswa (Insert) :**

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Non Transaksi**

4.  Pilih menu **Mahasiswa (Insert)**

![](media/image53.png){width="3.0104166666666665in" height="4.489583333333333in"}

### **Mengatur Filter Data Mahasiswa :**

### Pada halaman **Tabel "mahasiswa"**, lakukan pengaturan filter: {#pada-halaman-tabel-mahasiswa-lakukan-pengaturan-filter .unnumbered}

1.  Pilih **Program Studi (Prodi)**

2.  Pilih **Tahun Angkatan**

> Filter ini menentukan data mahasiswa yang akan diproses :

![](media/image56.png){width="6.53125in" height="2.8194444444444446in"}

### **Melakukan Crawl Data**

1.  Setelah Prodi dan Tahun Angkatan dipilih, klik tombol **Crawl Data**

2.  Sistem akan mengambil data mahasiswa dari sistem akademik

3.  Tunggu hingga proses crawl selesai

Catatan:\
Proses ini **belum mengirim data ke PDDIKTI**, hanya mengambil data ke sistem eFeeder.

![](media/image57.png){width="6.53125in" height="2.189583333333333in"}

### **Menampilkan Data Hasil Crawl**

1.  Klik tombol **Display Crawl Data**

2.  Sistem akan menampilkan daftar mahasiswa hasil crawl

![](media/image58.png){width="6.53125in" height="3.5555555555555554in"}

3.  Lakukan pengecekan data jika pada kolom error muncul keterangan error nya dengan cara Klik "Info".

![](media/image59.png){width="6.53125in" height="3.3430555555555554in"}

4.  Lakukan penanganan sesuai dengan Petunjuk pada Informasi yang dimunculkan

![](media/image60.png){width="4.190715223097113in" height="3.400249343832021in"}

### **Sinkronisasi Data Mahasiswa**

1.  Jika data sudah sesuai, klik tombol **Sync Data Mahasiswa**

2.  Sistem akan mengirim data mahasiswa ke **Neo Feeder PDDIKTI**

3.  Tunggu hingga proses sinkronisasi selesai

![](media/image61.png){width="6.53125in" height="2.9243055555555557in"}

## Catatan Penting {#catatan-penting .unnumbered}

## Keberhasilan proses Sinkronisasi ditunjukkan dengan data mahasiswa tercatat di Neo Feeder PDDIKTI

-   Jika terjadi kegagalan bisa dilakukan pengecekan dengan klik Tombol "Display Crawl Data" untuk mengetahui penyebab kegagalan

-   Menu **Mahasiswa (Insert)** hanya digunakan untuk **data mahasiswa baru**

-   Untuk perubahan data mahasiswa yang sudah terlapor, gunakan menu **Mahasiswa (Update)**

### Sinkronisasi Data Non Transaksi -- Mahasiswa PT (Insert)

Menu **Mahasiswa PT (Insert)** digunakan untuk melakukan pelaporan **History Pendidikan Mahasiswa (Riwayat Pendidikan Tinggi Mahasiswa)** ke **Neo Feeder PDDIKTI**.

Menu ini berbeda dengan, perbedaannya adalah :

-   **Mahasiswa (Insert)** → untuk data master mahasiswa

-   **Mahasiswa PT (Insert)** → untuk data riwayat pendidikan mahasiswa pada perguruan tinggi

Data yang ditarik pada menu ini akan menjadi bagian dari:

-   Riwayat pendidikan mahasiswa di PDDIKTI

-   Status awal mahasiswa (baru, pindahan, dll.)

-   Informasi jalur masuk dan pembiayaan

Menu ini berfungsi untuk:

-   Menarik data history pendidikan mahasiswa dari sistem akademik

-   Menampilkan data riwayat pendidikan yang akan dilaporkan

-   Mengirim data history pendidikan ke Neo Feeder PDDIKTI

## Langkah-Langkah Proses Mahasiswa PT (Insert) :  {#langkah-langkah-proses-mahasiswa-pt-insert .unnumbered}

## ● Mengakses Menu : {#mengakses-menu .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Non Transaksi**

4.  Pilih **Mahasiswa PT (Insert)**

![](media/image62.png){width="6.53125in" height="2.248611111111111in"}

## ● Mengatur Filter Data : {#mengatur-filter-data .unnumbered}

1.  Pada halaman **Tabel "mahasiswa PT"**, pilih **Prodi** sesuai kebutuhan

2.  Pilih **Tahun Angkatan** sesuai periode masuk mahasiswa

Filter ini menentukan data history pendidikan yang akan diproses.

![](media/image63.png){width="6.53125in" height="1.957638888888889in"}

## ● Melakukan Crawl Data : {#melakukan-crawl-data-1 .unnumbered}

1.  Klik tombol **Crawl Data**

2.  Sistem akan menarik data history pendidikan mahasiswa dari sistem akademik

3.  Tunggu hingga proses selesai

![](media/image64.png){width="6.53125in" height="2.3493055555555555in"}

Catatan:\
Proses ini hanya mengambil data ke eFeeder dan belum mengirim ke PDDIKTI.

## ● Menampilkan Data Hasil Crawl : {#menampilkan-data-hasil-crawl-1 .unnumbered}

1.  Klik tombol **Display Crawl Data**

2.  Sistem akan menampilkan daftar history pendidikan mahasiswa

3.  Pastikan seluruh data sudah sesuai sebelum dilakukan sinkronisasi.

![](media/image65.png){width="6.53125in" height="3.8520833333333333in"}

4.  Lakukan pengecekan data jika pada kolom error muncul keterangan error nya dengan cara Klik "Info".

![](media/image66.png){width="6.53125in" height="2.652083333333333in"}

5.  Lakukan penanganan sesuai dengan Petunjuk pada Informasi yang dimunculkan

![](media/image67.png){width="3.7118755468066493in" height="3.5066469816272967in"}

## ● Sinkronisasi Data ke Neo Feeder PDDIKTI : {#sinkronisasi-data-ke-neo-feeder-pddikti .unnumbered}

1.  Klik tombol **Sync Data**

2.  Sistem akan mengirim data history pendidikan ke Neo Feeder

3.  Tunggu hingga proses selesai

4.  Pastikan status berhasil tanpa error

![](media/image68.png){width="6.53125in" height="2.0166666666666666in"}

## ● Penanganan Jika Gagal :  {#penanganan-jika-gagal .unnumbered}

1.  Klik kembali **Display Crawl Data**

2.  Periksa kolom error yang muncul

3.  Lakukan perbaikan data pada sistem akademik sesuai informasi error

4.  Lakukan proses **Crawl Data** dan **Sync Data** ulang

## ● Ketentuan Penting {#ketentuan-penting .unnumbered}

-   Proses ini wajib dilakukan agar mahasiswa memiliki riwayat pendidikan aktif di Neo Feeder PDDIKTI

-   Data Mahasiswa PT tidak dapat dikirim jika data **Mahasiswa (Insert)** belum berhasil

-   Pastikan pemetaan berikut sudah dilakukan:

    -   Jalur Masuk

    -   Pembiayaan

### Sinkronisasi Data Non Transaksi - Mahasiswa (Update) :

Menu **Mahasiswa (Update)** digunakan untuk melakukan pembaruan data mahasiswa yang sudah terdaftar di **Neo Feeder PDDIKTI**. Menu ini digunakan apabila terdapat perubahan data akademik yang perlu disesuaikan di Neo Feeder PDDIKTI.

## ● Ketentuan Umum Update : {#ketentuan-umum-update .unnumbered}

-   Proses update hanya berlaku untuk mahasiswa yang **sudah berhasil diinsert sebelumnya**.

-   Data yang dapat diperbarui **mengikuti aturan dan validasi yang berlaku pada Neo Feeder PDDIKTI**.

-   Jika terdapat pembatasan update, maka sistem akan menyesuaikan dengan ketentuan dari layanan Neo Feeder.

-   Apabila data tidak berubah setelah proses update, lakukan pengecekan periode dan reset tabel sesuai kebutuhan.

## ● Mengakses Menu : {#mengakses-menu-1 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Non Transaksi**

4.  Pilih **Mahasiswa (Update)**

![](media/image69.png){width="6.53125in" height="2.5381944444444446in"}

## ● Mengatur Filter Data : {#mengatur-filter-data-1 .unnumbered}

1.  Pilih **Prodi** sesuai kebutuhan

2.  Pilih **Tahun Angkatan** sesuai data yang akan diperbarui

![](media/image70.png){width="6.53125in" height="2.5104166666666665in"}

## ● Melakukan Crawl Data Update : {#melakukan-crawl-data-update .unnumbered}

1.  Klik tombol **Crawl Data Update**

2.  Sistem akan menarik data mahasiswa yang telah terdaftar di PDDIKTI

3.  Tunggu hingga proses selesai

![](media/image71.png){width="6.53125in" height="2.4493055555555556in"}

## ● Sinkronisasi Data Update {#sinkronisasi-data-update .unnumbered}

1.  Klik tombol **Sync Data**

2.  Sistem akan mengirim perubahan data ke Neo Feeder PDDIKTI

3.  Tunggu hingga proses selesai

4.  Pastikan tidak terdapat error pada hasil sinkronisasi

![](media/image72.png){width="6.53125in" height="2.5416666666666665in"}

## ● Jika Update Tidak Berubah {#jika-update-tidak-berubah .unnumbered}

1.  Pastikan data yang diubah termasuk kategori yang diperbolehkan oleh Neo Feeder

2.  Periksa periode pelaporan aktif

3.  Lakukan **Reset Table Mahasiswa PT** jika diperlukan

4.  Ulangi proses:

    -   Crawl Data Update

    -   Sync Data

## ● Catatan Penting {#catatan-penting-1 .unnumbered}

-   Proses update sepenuhnya mengikuti **validasi dan kebijakan Neo Feeder PDDIKTI**.

-   Jika sistem Neo Feeder menolak perubahan data, maka perubahan tidak akan tersimpan.

-   Disarankan melakukan pengecekan hasil update langsung melalui Neo Feeder untuk memastikan data telah berubah.

### Sinkronisasi Data Non Transaksi -- Status Mahasiswa (Update)

Menu **Status Mahasiswa (Update)** digunakan untuk melakukan pembaruan **status keluar mahasiswa** di Neo Feeder PDDIKTI, seperti:

-   Lulus

-   Drop Out (DO)

-   Mengundurkan Diri / Keluar

## ● Mengakses Menu {#mengakses-menu-2 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Non Transaksi**

4.  Pilih **Status Mahasiswa (Update)**

![](media/image73.png){width="1.7982327209098863in" height="3.3757425634295712in"}

## ● Mengatur Filter Data {#mengatur-filter-data-2 .unnumbered}

Filter digunakan untuk menentukan data mahasiswa yang akan diperbarui statusnya.

### ▪ Filter Massal (Berdasarkan Prodi / Angkatan) {#filter-massal-berdasarkan-prodi-angkatan .unnumbered}

1.  Pilih **Prodi** sesuai kebutuhan

2.  Pilih **Tahun Angkatan** sesuai kebutuhan

3.  Kosongkan kolom NIM dan Nama jika ingin memproses banyak data sekaligus

![](media/image74.png){width="6.53125in" height="2.2354166666666666in"}

### ▪ Filter Satuan (Per Mahasiswa) {#filter-satuan-per-mahasiswa .unnumbered}

Jika ingin memproses **satu mahasiswa tertentu**, lakukan:

1.  Pilih **Prodi = Semua**

2.  Pilih **Tahun Angkatan = Semua**

3.  Masukkan **NIM** atau **Nama Mahasiswa** pada kolom yang tersedia

Metode ini digunakan apabila:

-   Ingin melakukan update hanya untuk satu mahasiswa

-   Ingin melakukan pengecekan atau Force Sync pada kasus tertentu

![](media/image75.png){width="6.53125in" height="2.282638888888889in"}

## ● Melakukan Crawl Status {#melakukan-crawl-status .unnumbered}

1.  Klik tombol **Crawl Status**

2.  Sistem akan menarik data status mahasiswa dari sistem akademik

3.  Tunggu hingga proses selesai

![](media/image76.png){width="6.53125in" height="2.720138888888889in"}

## ● Menampilkan Data Hasil Crawl {#menampilkan-data-hasil-crawl-2 .unnumbered}

1.  Klik tombol **Display Crawl Data**

2.  Periksa dan pastikan data sudah sesuai sebelum dilakukan sinkronisasi.

![](media/image77.png){width="6.53125in" height="4.028472222222222in"}

## ● Sinkronisasi Status Mahasiswa (Normal Sync) {#sinkronisasi-status-mahasiswa-normal-sync .unnumbered}

1.  Klik tombol **Sync Status mahasiswa_pt**

2.  Tunggu hingga proses selesai

3.  Pastikan tidak terdapat error

![](media/image78.png){width="6.53125in" height="2.240972222222222in"}

## ● Force Sync Status Mahasiswa {#force-sync-status-mahasiswa .unnumbered}

Fitur ini digunakan untuk **memaksa status di Neo Feeder mengikuti data sistem akademik**.

### Contoh Kasus: {#contoh-kasus .unnumbered}

-   Status di Neo Feeder: **Lulus**

-   Status di Akademik: **Aktif**

-   Sync normal tidak mengubah data

-   Dengan **Force Sync**, status akan kembali menjadi **A (Aktif)** di Neo Feeder

### Cara Menggunakan: {#cara-menggunakan .unnumbered}

1.  Pastikan data di sistem akademik sudah benar

2.  Klik **Force Sync Status mahasiswa_pt**

3.  Tunggu hingga proses selesai

4.  Lakukan pengecekan di Neo Feeder

![](media/image79.png){width="6.53125in" height="2.2958333333333334in"}

## ● Catatan Penting {#catatan-penting-2 .unnumbered}

-   Gunakan Force Sync hanya jika diperlukan

-   Pastikan perubahan telah diverifikasi oleh bagian akademik

-   Perubahan status berdampak langsung pada pelaporan PDDIKTI

### Sinkronisasi Data Non Transaksi -- Bobot Nilai (Insert)

Menu **Bobot Nilai (Insert)** berfungsi untuk mengirimkan **data referensi rentang penilaian** ke Neo Feeder PDDIKTI. Data ini menjadi dasar validasi saat pelaporan nilai mahasiswa ke Neo Feeder.

## ● Mengakses Menu {#mengakses-menu-3 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Non Transaksi**

4.  Pilih **Bobot Nilai (Insert)**

![](media/image80.png){width="1.905067804024497in" height="4.350481189851268in"}

## ● Mengatur Filter Data {#mengatur-filter-data-3 .unnumbered}

Filter digunakan untuk menentukan program studi yang akan diproses.

1.  Pilih **Prodi** tertentu jika ingin memproses satu program studi saja

2.  Atau Pilih **Prodi = Semua** untuk memproses seluruh program studi sekaligus

![](media/image81.png){width="6.53125in" height="1.6368055555555556in"}

## ● Melakukan Crawl Data {#melakukan-crawl-data-2 .unnumbered}

1.  Klik tombol **Crawl Data**

2.  Sistem akan menarik data **rentang penilaian** dari sistem akademik

3.  Tunggu hingga proses selesai

![](media/image82.png){width="6.53125in" height="1.8409722222222222in"}

## ● Menampilkan Data Hasil Crawl {#menampilkan-data-hasil-crawl-3 .unnumbered}

1.  Klik tombol **Display Crawl Data**

2.  Sistem akan menampilkan data referensi yang akan dikirim ke Neo Feeder, meliputi:

    -   Nilai Huruf (A, B, C, D, E)

    -   Nilai Angka

    -   Nilai Minimum

    -   Nilai Maksimum

    -   Bobot Nilai

![](media/image83.png){width="6.53125in" height="4.490277777777778in"}

Pastikan:

-   Tidak ada rentang nilai yang tumpang tindih

-   Tidak ada rentang nilai yang kosong

-   Susunan rentang sudah sesuai standar akademik kampus

## ● Sinkronisasi Data ke Neo Feeder {#sinkronisasi-data-ke-neo-feeder .unnumbered}

1.  Klik tombol **Sync Data**

2.  Tunggu hingga proses sinkronisasi selesai

3.  Pastikan tidak muncul pesan error

![](media/image84.png){width="6.53125in" height="1.7104166666666667in"}

Jika berhasil, data referensi bobot nilai akan tersimpan di Neo Feeder dan dapat digunakan untuk pelaporan nilai mahasiswa.

## ● Catatan Penting {#catatan-penting-3 .unnumbered}

-   Bobot nilai harus dikirim terlebih dahulu sebelum melakukan pelaporan nilai mahasiswa

-   Pastikan struktur rentang penilaian di sistem akademik sudah final

-   Perubahan rentang di tengah semester dapat memengaruhi validasi nilai

-   Format dan struktur harus mengikuti ketentuan Neo Feeder PDDIKTI

-   Bobot nilai ini diproses ketika memang belum ada data referensi bobot nilai di Neo Feeder

### Sinkronisasi Data Non Transaksi -- Bobot Nilai (Update)

Menu **Bobot Nilai (Update)** berfungsi untuk memperbarui data referensi **rentang penilaian** yang sudah terdaftar di Neo Feeder PDDIKTI apabila terjadi perubahan pada sistem akademik.

Menu ini digunakan jika:

-   Terjadi perubahan rentang nilai (misalnya 80--100 menjadi 85--100)

-   Terjadi perubahan bobot nilai

-   Terjadi penyesuaian standar penilaian kampus

-   Data referensi di Neo Feeder perlu disesuaikan dengan data terbaru di sistem akademik

## ● Mengakses Menu {#mengakses-menu-4 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Non Transaksi**

4.  Pilih **Bobot Nilai (Update)**

![](media/image85.png){width="2.0658300524934385in" height="4.817729658792651in"}

## ● Mengatur Filter Data {#mengatur-filter-data-4 .unnumbered}

Filter digunakan untuk menentukan program studi yang akan diproses.

▪ Untuk update per prodi tertentu, Pilih **Prodi** sesuai kebutuhan

▪ Untuk update seluruh prodi, Pilih **Prodi = Semua**

![](media/image86.png){width="6.53125in" height="1.820138888888889in"}

## ● Melakukan Crawl Data Update {#melakukan-crawl-data-update-1 .unnumbered}

1.  Klik tombol **Crawl Data Update**

2.  Sistem akan menarik data rentang penilaian terbaru dari sistem akademik

3.  Data ini akan dibandingkan dengan data yang sudah ada di Neo Feeder

![](media/image87.png){width="6.53125in" height="1.6347222222222222in"}

Pastikan:

-   Tidak ada rentang yang tumpang tindih

-   Nilai minimum dan maksimum sudah sesuai

-   Struktur penilaian sudah final

## ● Sinkronisasi Data Update {#sinkronisasi-data-update-1 .unnumbered}

1.  Klik tombol **Sync Data**

2.  Tunggu hingga proses selesai

3.  Pastikan tidak muncul pesan error

![](media/image88.png){width="6.53125in" height="1.6277777777777778in"}

Jika berhasil, data rentang penilaian di Neo Feeder akan diperbarui mengikuti data terbaru dari sistem akademik.

## ● Perbedaan Bobot Nilai (Insert) dan (Update) {#perbedaan-bobot-nilai-insert-dan-update .unnumbered}

-   **Insert** → Digunakan saat pertama kali mengirim referensi rentang nilai ke Neo Feeder

-   **Update** → Digunakan untuk memperbarui referensi yang sudah pernah dikirim sebelumnya

## ● Catatan Penting {#catatan-penting-4 .unnumbered}

-   Update hanya dapat dilakukan sesuai ketentuan Neo Feeder PDDIKTI

-   Perubahan rentang nilai harus mengikuti aturan validasi Neo Feeder

-   Disarankan melakukan update sebelum pelaporan nilai semester berjalan

-   Hindari perubahan struktur penilaian di tengah periode pelaporan jika sudah ada data nilai terkirim

### Sinkronisasi Data Non Transaksi -- Kurikulum (Insert)

Menu **Kurikulum (Insert)** berfungsi untuk mengirimkan data referensi kurikulum dari sistem akademik ke Neo Feeder PDDIKTI.

## ● Mengakses Menu {#mengakses-menu-5 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Non Transaksi**

4.  Pilih **Kurikulum (Insert)**

![](media/image89.png){width="6.53125in" height="2.763888888888889in"}

## ● Mengatur Filter Data {#mengatur-filter-data-5 .unnumbered}

▪ Untuk insert kurikulum per prodi tertentu, pilih **Prodi** sesuai kebutuhan

▪ Untuk insert seluruh prodi, Pilih **Prodi = Semua**

![](media/image90.png){width="6.53125in" height="1.8729166666666666in"}

## ● Melakukan Crawl Data {#melakukan-crawl-data-3 .unnumbered}

1.  Klik tombol **Crawl Data**

2.  Sistem akan menarik data kurikulum dari sistem akademik

3.  Pastikan data yang ditarik sudah sesuai

![](media/image91.png){width="6.53125in" height="1.5895833333333333in"}

## ● Display Crawl Data (Melihat Detail & Validasi Data) {#display-crawl-data-melihat-detail-validasi-data .unnumbered}

Tombol **Display Crawl Data** berfungsi untuk:

-   Melihat detail data kurikulum yang akan dikirim ke Neo Feeder

-   Melihat status validasi data

-   Mengetahui apakah terdapat error

-   Melihat informasi panduan penanganan jika terdapat error data

Langkah penggunaan:

1.  Klik **Display Crawl Data**

2.  Periksa kolom status/error (jika ada)

3.  Jika terdapat error, klik tombol **Info** (jika tersedia) untuk melihat guideline perbaikan

4.  Lakukan perbaikan data di sistem akademik

5.  Ulangi proses **Crawl Data** hingga tidak ada error

![](media/image92.png){width="6.53125in" height="3.8305555555555557in"}

## ● Sinkronisasi Data ke Neo Feeder {#sinkronisasi-data-ke-neo-feeder-1 .unnumbered}

1.  Setelah data valid dan tidak terdapat error, klik **Sync Data**

2.  Tunggu hingga proses selesai

3.  Pastikan tidak muncul pesan gagal

Jika berhasil, data kurikulum akan tersimpan di Neo Feeder PDDIKTI.

![](media/image93.png){width="6.53125in" height="1.6083333333333334in"}

## ● Catatan Penting {#catatan-penting-5 .unnumbered}

-   Pastikan kurikulum sudah final dan aktif sebelum dilakukan insert

-   Periksa error melalui Display Crawl Data sebelum sync

-   Jika kurikulum sudah pernah dikirim, gunakan menu **Kurikulum (Update)** untuk perubahan

-   Struktur kurikulum harus sesuai dengan aturan Neo Feeder PDDIKTI

### Sinkronisasi Data Non Transaksi -- Kurikulum (Update)

Menu **Kurikulum (Update)** berfungsi untuk memperbarui data kurikulum yang sudah pernah dikirim ke Neo Feeder PDDIKTI apabila terdapat perubahan pada sistem akademik.

Menu ini digunakan jika:

-   Terdapat perubahan nama kurikulum

-   Penyesuaian tahun mulai berlaku

-   Perbaikan data kurikulum yang sudah tersimpan di Neo Feeder

## ● Mengakses Menu {#mengakses-menu-6 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Non Transaksi**

4.  Pilih **Kurikulum (Update)**

![](media/image94.png){width="6.53125in" height="2.2534722222222223in"}

## ● Mengatur Filter Data {#mengatur-filter-data-6 .unnumbered}

▪ Untuk update kurikulum per prodi tertentu, Pilih **Prodi** sesuai kebutuhan

▪ Untuk update seluruh prodi, Pilih **Prodi = Semua**

![](media/image95.png){width="6.53125in" height="1.8423611111111111in"}

## ● Melakukan Crawl Data Update {#melakukan-crawl-data-update-2 .unnumbered}

1.  Klik tombol **Crawl Data Update**

2.  Sistem akan menarik data kurikulum terbaru dari sistem akademik

3.  Data tersebut akan dibandingkan dengan data yang sudah ada di Neo Feeder

Pastikan perubahan data sudah benar sebelum dilakukan sinkronisasi.

![](media/image96.png){width="6.53125in" height="1.9416666666666667in"}

## ● Sinkronisasi Data ke Neo Feeder {#sinkronisasi-data-ke-neo-feeder-2 .unnumbered}

1.  Setelah proses crawl selesai dan data sudah valid, klik **Sync Data**

2.  Tunggu hingga proses selesai

3.  Pastikan tidak terdapat pesan error

Jika berhasil, maka data kurikulum di Neo Feeder akan diperbarui mengikuti data terbaru dari sistem akademik.

![](media/image97.png){width="6.53125in" height="2.082638888888889in"}

## ● Catatan Penting {#catatan-penting-6 .unnumbered}

-   Update hanya dapat dilakukan untuk kurikulum yang sudah pernah diinsert sebelumnya

-   Perubahan data harus mengikuti aturan validasi Neo Feeder PDDIKTI

-   Hindari perubahan struktur kurikulum yang sudah digunakan dalam pelaporan aktif

-   Disarankan melakukan pengecekan data sebelum periode pelaporan berjalan

### Sinkronisasi Data Non Transaksi -- Mata Kuliah (Insert)

Menu **Mata Kuliah (Insert)** berfungsi untuk mengirimkan data referensi mata kuliah dari sistem akademik ke Neo Feeder PDDIKTI.

Data mata kuliah ini menjadi dasar pelaporan:

-   KRS dan nilai

-   Relasi dengan kurikulum

Menu ini digunakan saat:

-   Pertama kali mengirim data mata kuliah ke Neo Feeder

-   Menambahkan mata kuliah baru yang belum pernah dilaporkan

## ● Mengakses Menu {#mengakses-menu-7 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Non Transaksi**

4.  Pilih **Matakuliah (Insert)**

![](media/image98.png){width="6.53125in" height="2.229861111111111in"}

## ● Mengatur Filter Data {#mengatur-filter-data-7 .unnumbered}

▪ Untuk insert mata kuliah per prodi tertentu, Pilih **Prodi** sesuai kebutuhan

▪ Untuk insert seluruh prodi, Pilih **Prodi = Semua**

![](media/image99.png){width="6.53125in" height="1.7152777777777777in"}

## ● Melakukan Crawl Data {#melakukan-crawl-data-4 .unnumbered}

1.  Klik tombol **Crawl Data**

2.  Sistem akan menarik data mata kuliah dari sistem akademik

3.  Pastikan data yang ditarik sudah sesuai

![](media/image100.png){width="6.53125in" height="1.6875in"}

## ● Display Crawl Data (Validasi Data) {#display-crawl-data-validasi-data .unnumbered}

Tombol **Display Crawl Data** berfungsi untuk:

-   Melihat detail mata kuliah yang akan dikirim

-   Mengecek validasi data

-   Melihat error jika ada

-   Melihat informasi panduan penanganan error

Langkah:

1.  Klik **Display Crawl Data**

2.  Periksa kolom error (jika ada)

3.  Jika terdapat error, klik **Info** untuk melihat guideline perbaikan

4.  Lakukan perbaikan di sistem akademik

5.  Ulangi proses Crawl Data hingga tidak ada error

![](media/image101.png){width="6.53125in" height="3.8229166666666665in"}

## ● Sinkronisasi Data ke Neo Feeder {#sinkronisasi-data-ke-neo-feeder-3 .unnumbered}

1.  Setelah data valid dan tidak terdapat error, klik **Sync Data**

2.  Tunggu hingga proses selesai

3.  Pastikan tidak ada pesan gagal

Jika berhasil, data mata kuliah akan tersimpan di Neo Feeder PDDIKTI.

![](media/image102.png){width="6.53125in" height="1.5590277777777777in"}

## ● Catatan Penting {#catatan-penting-7 .unnumbered}

-   Pastikan kurikulum sudah diinsert terlebih dahulu sebelum insert mata kuliah

-   Kode mata kuliah tidak boleh duplikat

-   SKS dan struktur mata kuliah harus sesuai dengan aturan Neo Feeder PDDIKTI

-   Jika mata kuliah sudah pernah dikirim sebelumnya dan ingin diperbarui, gunakan menu **Mata Kuliah (Update)** sesuai kebutuhan

### Sinkronisasi Data Non Transaksi -- Mata Kuliah (Match Data)

Menu **Matakuliah (Match Data)** berfungsi untuk melakukan pencocokan (mapping) antara data mata kuliah di sistem akademik dengan data mata kuliah yang sudah ada di Neo Feeder PDDIKTI.

Menu ini digunakan jika:

-   Mata kuliah sudah pernah ada di Neo Feeder

-   Terjadi perbedaan kode antara sistem akademik dan Neo Feeder

-   Insert gagal karena data sudah tersedia di Neo Feeder

-   Perlu menghubungkan data lama Neo Feeder dengan data akademik

## ● Mengakses Menu {#mengakses-menu-8 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Non Transaksi**

4.  Pilih **Matakuliah (Match Data)**

![](media/image103.png){width="6.53125in" height="3.0034722222222223in"}

## ● Mengatur Filter Data {#mengatur-filter-data-8 .unnumbered}

Filter digunakan untuk mempermudah pencarian mata kuliah yang akan di-match.

▪ Pilih **Program Studi**\
▪ Jika diperlukan, isi:

-   **Kode Matakuliah**

-   **Nama Matakuliah**

Klik **Search** untuk menampilkan data.

![](media/image104.png){width="6.53125in" height="2.4944444444444445in"}

## ● Memahami Tampilan Data {#memahami-tampilan-data .unnumbered}

Pada tabel yang ditampilkan terdapat informasi:

-   Prodi

-   Kode MK

-   Nama MK

-   SKS

-   gt_id_label (data yang sudah terhubung ke Neo Feeder)

-   gt_id (ID match dengan Neo Feeder)

Jika kolom **gt_id_label** kosong (-), berarti mata kuliah belum terhubung ke Neo Feeder dan perlu dilakukan match.

![](media/image105.png){width="6.53125in" height="3.80625in"}

## ● Melakukan Match Data {#melakukan-match-data .unnumbered}

1.  Klik tombol **Edit (ikon pensil)** pada baris mata kuliah yang akan di-match

2.  Sistem akan menampilkan daftar mata kuliah yang tersedia di Neo Feeder

3.  Pilih mata kuliah yang sesuai

4.  Klik Save proses match

![](media/image106.png){width="6.53125in" height="3.473611111111111in"}

Setelah berhasil, kolom **gt_id_label** dan **gt_id** akan terisi menandakan data sudah terhubung.

![](media/image107.png){width="6.53125in" height="3.0527777777777776in"}

## ● Fungsi Tombol Reset {#fungsi-tombol-reset .unnumbered}

Tombol **Reset** berfungsi untuk:

-   Membatalkan pemetaan (match) antara mata kuliah akademik dan Neo Feeder

-   Digunakan jika terjadi salah match

Gunakan reset dengan hati-hati, terutama jika data sudah digunakan dalam pelaporan nilai atau KRS.

![](media/image108.png){width="6.53125in" height="3.477777777777778in"}

## ● Catatan Penting {#catatan-penting-8 .unnumbered}

-   Pastikan kode dan nama mata kuliah yang dipilih benar-benar sesuai

-   Hindari melakukan match pada mata kuliah yang berbeda hanya karena nama mirip

-   Disarankan melakukan match sebelum melakukan sinkronisasi aktivitas perkuliahan

-   Perubahan match dapat mempengaruhi pelaporan nilai dan KRS

### Sinkronisasi Data Non Transaksi -- Mata Kuliah (Update)

Menu **Matakuliah (Update)** berfungsi untuk memperbarui data referensi mata kuliah yang sudah pernah dikirim ke Neo Feeder PDDIKTI apabila terdapat perubahan pada sistem akademik.

Menu ini digunakan jika terjadi perubahan seperti:

-   Nama mata kuliah

-   Jumlah SKS

-   Jenis mata kuliah

## ● Mengakses Menu {#mengakses-menu-9 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Non Transaksi**

4.  Pilih **Matakuliah (Update)**

![](media/image109.png){width="6.53125in" height="2.795138888888889in"}

## ● Mengatur Filter Data {#mengatur-filter-data-9 .unnumbered}

▪ Untuk update mata kuliah per prodi tertentu, Pilih **Prodi** sesuai kebutuhan

▪ Untuk update seluruh prodi, Pilih **Prodi = Semua**

![](media/image110.png){width="6.53125in" height="1.95in"}

## ● Melakukan Crawl Data Update {#melakukan-crawl-data-update-3 .unnumbered}

1.  Klik tombol **Crawl Data Update**

2.  Sistem akan menarik data mata kuliah terbaru dari sistem akademik

3.  Sistem akan membandingkan data akademik dengan data yang sudah tersimpan di Neo Feeder

4.  Pastikan perubahan yang dilakukan sudah final sebelum dilakukan sinkronisasi.

![](media/image111.png){width="6.53125in" height="1.9520833333333334in"}

## ● Sinkronisasi Data {#sinkronisasi-data-1 .unnumbered}

1.  Setelah proses crawl selesai dan data sudah sesuai, klik **Sync Data**

2.  Tunggu hingga proses selesai

3.  Pastikan tidak muncul pesan error

4.  Jika berhasil, data mata kuliah di Neo Feeder akan diperbarui mengikuti data terbaru dari sistem akademik.

![](media/image112.png){width="6.53125in" height="2.167361111111111in"}

## ● Catatan Penting {#catatan-penting-9 .unnumbered}

-   Update hanya berlaku untuk mata kuliah yang sudah pernah diinsert atau sudah di-match sebelumnya

-   Perubahan harus mengikuti validasi dan aturan Neo Feeder PDDIKTI

-   Hindari perubahan kode mata kuliah jika sudah digunakan dalam pelaporan KRS dan nilai

-   Disarankan melakukan update sebelum periode pelaporan berjalan

### Sinkronisasi Data Non Transaksi -- MK Kurikulum (Insert)

Menu **MK Kurikulum (Insert)** berfungsi untuk mengirimkan relasi antara Mata Kuliah dan Kurikulum ke Neo Feeder PDDIKTI.

Menu ini digunakan untuk melaporkan:

-   Mata kuliah apa saja yang masuk ke dalam suatu kurikulum

-   Semester penempatan mata kuliah dalam kurikulum

-   Status wajib/pilihan

Menu ini dijalankan setelah:\
✔ Kurikulum sudah diinsert\
✔ Mata kuliah sudah diinsert dan sudah di-match

## ● Mengakses Menu {#mengakses-menu-10 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Non Transaksi**

4.  Pilih **MK Kurikulum (Insert)**

![](media/image113.png){width="6.53125in" height="2.3375in"}

## ● Mengatur Filter Data {#mengatur-filter-data-10 .unnumbered}

▪ Untuk insert relasi per prodi tertentu, Pilih **Prodi** sesuai kebutuhan

▪ Untuk insert seluruh prodi, Pilih **Prodi = Semua**

![](media/image114.png){width="6.53125in" height="1.7479166666666666in"}

## ● Melakukan Crawl Data {#melakukan-crawl-data-5 .unnumbered}

1.  Klik tombol **Crawl Data**

2.  Sistem akan menarik data relasi Mata Kuliah dengan Kurikulum dari sistem akademik

3.  Pastikan struktur kurikulum sudah benar

![](media/image115.png){width="6.53125in" height="1.492361111111111in"}

## ● Display Crawl Data (Validasi Data) {#display-crawl-data-validasi-data-1 .unnumbered}

Tombol **Display Crawl Data** berfungsi untuk:

-   Melihat detail relasi mata kuliah dalam kurikulum

-   Mengecek apakah terdapat error

-   Melihat informasi panduan jika ada error

Langkah:

1.  Klik **Display Crawl Data**

2.  Periksa kolom error (jika ada)

3.  Jika terdapat error, klik **Info** untuk melihat guideline penanganan

4.  Perbaiki data di sistem akademik

5.  Ulangi proses Crawl hingga data valid

![](media/image116.png){width="6.53125in" height="3.8472222222222223in"}

## ● Sinkronisasi Data {#sinkronisasi-data-2 .unnumbered}

1.  Setelah data valid dan tidak terdapat error, klik **Sync Data**

2.  Tunggu hingga proses selesai

3.  Pastikan tidak ada pesan gagal

4.  Jika berhasil, maka relasi Mata Kuliah dan Kurikulum akan tersimpan di Neo Feeder.

![](media/image117.png){width="6.53125in" height="1.7729166666666667in"}

## ● Catatan Penting {#catatan-penting-10 .unnumbered}

-   Pastikan kurikulum dan mata kuliah sudah tersinkronisasi terlebih dahulu

-   Hindari perubahan struktur kurikulum jika sudah digunakan dalam pelaporan KRS dan nilai

-   Relasi yang sudah digunakan dalam aktivitas kuliah sebaiknya tidak dihapus tanpa analisis dampak

-   Ikuti aturan validasi Neo Feeder PDDIKTI

### Sinkronisasi Data Non Transaksi -- MK Kurikulum (Match Data)

Menu **MK Kurikulum (Match Data)** berfungsi untuk melakukan pencocokan (mapping) antara relasi Mata Kuliah--Kurikulum di sistem akademik dengan data yang sudah ada di Neo Feeder PDDIKTI.

Menu ini digunakan apabila:

-   Data relasi sudah ada di Neo Feeder

-   Namun belum memiliki **gt_id**

-   Atau terjadi ketidaksesuaian antara data akademik dan Neo Feeder

## ● Mengakses Menu {#mengakses-menu-11 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Non Transaksi**

4.  Pilih **MK Kurikulum (Match Data)**

![](media/image118.png){width="6.53125in" height="2.7805555555555554in"}

## ● Generate GT ID (Matching Data) {#generate-gt-id-matching-data .unnumbered}

Tombol **Generate gt id** berfungsi untuk:

-   Mengambil dan menghasilkan ID referensi dari Neo Feeder

-   Menyelaraskan data relasi Mata Kuliah--Kurikulum dengan ID yang ada di Neo Feeder

Langkah:

1.  Klik tombol **Generate gt id**

2.  Tunggu hingga proses selesai

3.  Pastikan kolom **gt_id** terisi untuk data yang sudah berhasil dicocokkan

![](media/image119.png){width="6.53125in" height="1.96875in"}

## ● Mengatur Filter Data {#mengatur-filter-data-11 .unnumbered}

▪ Untuk pencarian berdasarkan Prodi, Pilih **Program Studi**

▪ Untuk pencarian spesifik:

-   Isi **Kode Matakuliah** atau

-   Isi **Nama Matakuliah**

▪ Klik **Search** untuk menampilkan data

▪ Tombol **Download Data.xls** dapat digunakan untuk mengunduh data dalam format Excel

![](media/image120.png){width="6.53125in" height="2.3694444444444445in"}

## ● Catatan Penting {#catatan-penting-11 .unnumbered}

-   Pastikan **Kurikulum (Insert)** dan **Matakuliah (Insert)** sudah dilakukan sebelumnya

-   Pastikan tidak ada perbedaan kode atau penamaan antara sistem akademik dan Neo Feeder

-   Matching diperlukan agar relasi tidak dianggap sebagai data baru saat sinkronisasi

-   Data yang sudah memiliki **gt_id** berarti sudah terhubung dengan Neo Feeder

### Sinkronisasi Data Non Transaksi -- MK Kurikulum (Update)

Menu **MK Kurikulum (Update)** berfungsi untuk memperbarui (update) relasi Mata Kuliah--Kurikulum yang sudah terdaftar di Neo Feeder PDDIKTI.

## ● Mengakses Menu {#mengakses-menu-12 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Non Transaksi**

4.  Pilih **MK Kurikulum (Update)**

![](media/image121.png){width="6.53125in" height="2.6326388888888888in"}

## ● Mengatur Filter Data {#mengatur-filter-data-12 .unnumbered}

▪ Pilih **Prodi** sesuai kebutuhan

![](media/image122.png){width="6.53125in" height="1.5631944444444446in"}

## ● Crawl Data Update {#crawl-data-update .unnumbered}

Tombol **Crawl Data Update** berfungsi untuk:

-   Menarik data relasi Mata Kuliah--Kurikulum terbaru dari sistem akademik

-   Membandingkan dengan data yang sudah ada di Neo Feeder

-   Menyiapkan data yang mengalami perubahan untuk proses update

Langkah:

1.  Klik **Crawl Data Update**

2.  Tunggu hingga proses selesai

3.  Pastikan tidak ada error sebelum melakukan sync

![](media/image123.png){width="6.53125in" height="1.8722222222222222in"}

## ● Proses Update ke Neo Feeder {#proses-update-ke-neo-feeder .unnumbered}

Setelah crawl berhasil:

1.  Klik tombol **Sync Data**

2.  Sistem akan mengirimkan data perubahan ke Neo Feeder

3.  Tunggu hingga proses selesai

4.  Pastikan tidak muncul notifikasi error

![](media/image124.png){width="6.53125in" height="2.1041666666666665in"}

## ● Catatan Penting {#catatan-penting-12 .unnumbered}

-   Update hanya dapat dilakukan jika data sudah pernah diinsert dan memiliki **gt_id**

-   Jika data belum memiliki gt_id, lakukan proses pada menu:

    -   **MK Kurikulum (Match Data)** terlebih dahulu

-   Perubahan yang tidak diperbolehkan oleh Neo Feeder akan ditolak saat proses sync

### Sinkronisasi Data Non Transaksi -- RPS (Insert)

Menu **RPS (Insert)** berfungsi untuk mengirimkan data **Rencana Pembelajaran Semester (RPS)** ke Neo Feeder PDDIKTI. Data ini merupakan referensi rencana pembelajaran untuk setiap Mata Kuliah pada Kurikulum tertentu.

## ● Mengakses Menu {#mengakses-menu-13 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Non Transaksi**

4.  Pilih **RPS (Insert)**

![](media/image125.png){width="6.53125in" height="3.170138888888889in"}

## ● Mengatur Filter Data {#mengatur-filter-data-13 .unnumbered}

▪ Pilih **Prodi** sesuai kebutuhan![](media/image126.png){width="6.53125in" height="1.825in"}

## ● Crawl Data {#crawl-data .unnumbered}

Langkah -- Langkah :

1.  Klik **Crawl Data**

2.  Tunggu hingga proses selesai

3.  Pastikan tidak ada notifikasi error

![](media/image127.png){width="6.53125in" height="1.6701388888888888in"}

## ● Display Crawl Data {#display-crawl-data .unnumbered}

Tombol **Display Crawl Data** berfungsi untuk:

-   Melihat detail data RPS yang akan dikirim

-   Melihat struktur data yang ditarik

-   Melihat informasi error jika terdapat data yang tidak valid

-   Mengakses panduan penanganan apabila muncul error

Jika terdapat error:

-   Perbaiki data di sistem akademik

-   Lakukan ulang proses **Crawl Data**

![](media/image128.png){width="6.53125in" height="3.9298611111111112in"}

## ● Proses Insert ke Neo Feeder {#proses-insert-ke-neo-feeder .unnumbered}

Setelah data valid:

1.  Klik tombol **Sync Data**

2.  Sistem akan mengirim data RPS ke Neo Feeder

3.  Tunggu hingga proses selesai

4.  Pastikan tidak muncul notifikasi error

![](media/image129.png){width="6.53125in" height="1.7916666666666667in"}

## ● Jika Gagal Sinkronisasi {#jika-gagal-sinkronisasi .unnumbered}

Periksa hal berikut:

-   Pastikan Mata Kuliah sudah memiliki **gt_id**

-   Pastikan relasi MK Kurikulum sudah tersedia

-   Pastikan format dan kelengkapan data RPS sesuai ketentuan Neo Feeder

-   Perbaiki data, lalu ulangi proses Crawl dan Sync

## ● Catatan Penting {#catatan-penting-13 .unnumbered}

-   RPS hanya dapat dikirim jika:

    -   Mata Kuliah sudah terdaftar di Neo Feeder

    -   MK Kurikulum sudah terinsert

-   Data yang dikirim mengikuti struktur dan validasi dari Neo Feeder PDDIKTI

-   Jika terjadi perubahan pada RPS yang sudah pernah dikirim, gunakan menu **RPS (Update)**

### Sinkronisasi Data Non Transaksi -- RPS (Update)

Menu **RPS (Update)** berfungsi untuk memperbarui data **Rencana Pembelajaran Semester (RPS)** yang sebelumnya sudah berhasil diinsert ke Neo Feeder PDDIKTI.

## ● Mengakses Menu {#mengakses-menu-14 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Non Transaksi**

4.  Pilih **RPS (Update)**

![](media/image130.png){width="6.53125in" height="2.7090277777777776in"}

## ● Mengatur Filter Data {#mengatur-filter-data-14 .unnumbered}

▪ Pilih **Prodi** sesuai kebutuhan\
![](media/image131.png){width="6.53125in" height="1.7770833333333333in"}

## ● Crawl Data Update {#crawl-data-update-1 .unnumbered}

Tombol **Crawl Data** berfungsi untuk:

-   Menarik data RPS terbaru dari sistem akademik

-   Membandingkan dengan data yang sudah ada di Neo Feeder

-   Menyiapkan data yang akan diupdate

Langkah -- Langkah :

1.  Klik **Crawl Data**

2.  Tunggu hingga proses selesai

3.  Pastikan tidak ada notifikasi error

![](media/image132.png){width="6.53125in" height="1.8472222222222223in"}

## ● Proses Update ke Neo Feeder {#proses-update-ke-neo-feeder-1 .unnumbered}

Setelah data berhasil dicrawl dan tidak ada error:

1.  Klik tombol **Sync Data**

2.  Sistem akan mengirim perubahan data ke Neo Feeder

3.  Tunggu hingga proses selesai

4.  Pastikan tidak muncul notifikasi error

![](media/image133.png){width="6.53125in" height="1.675in"}

## ● Catatan Penting {#catatan-penting-14 .unnumbered}

-   Update hanya berlaku untuk data yang sudah memiliki referensi di Neo Feeder

-   Perubahan mengikuti aturan dan validasi dari Neo Feeder PDDIKTI

-   Jika data belum pernah dikirim sebelumnya, gunakan menu **RPS (Insert)**

### Sinkronisasi Data Non Transaksi -- Rencana Evaluasi (Insert)

Menu **Rencana Evaluasi (Insert)** berfungsi untuk mengirimkan data komponen evaluasi pembelajaran ke Neo Feeder PDDIKTI.

## ● Mengakses Menu {#mengakses-menu-15 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Non Transaksi**

4.  Pilih **Rencana Evaluasi (Insert)**

![](media/image134.png){width="6.53125in" height="3.157638888888889in"}

## ● Mengatur Filter Data {#mengatur-filter-data-15 .unnumbered}

▪ Pilih **Prodi** sesuai kebutuhan\
▪ Pastikan data berikut sudah berhasil dikirim sebelumnya:

-   Kurikulum

-   Mata Kuliah

-   MK Kurikulum

Jika salah satu belum dikirim, maka proses insert akan gagal.

![](media/image135.png){width="6.53125in" height="2.183333333333333in"}

## ● Crawl Data {#crawl-data-1 .unnumbered}

Tombol **Crawl Data** berfungsi untuk:

-   Menarik data rencana evaluasi dari sistem akademik

-   Menyiapkan data yang akan dikirim ke Neo Feeder

-   Melakukan validasi awal terhadap kelengkapan data

Langkah:

1.  Klik **Crawl Data**

2.  Tunggu hingga proses selesai

3.  Pastikan tidak muncul notifikasi error

![](media/image136.png){width="6.53125in" height="2.45625in"}

## ● Display Crawl Data {#display-crawl-data-1 .unnumbered}

Tombol **Display Crawl Data** berfungsi untuk:

-   Melihat detail data evaluasi yang akan dikirim

-   Melihat informasi error jika ada data yang tidak valid

Jika terdapat error:

-   Perbaiki data di sistem akademik

-   Lakukan crawl ulang sebelum melakukan sync

![](media/image137.png){width="6.53125in" height="2.313888888888889in"}

## ● Proses Insert ke Neo Feeder {#proses-insert-ke-neo-feeder-1 .unnumbered}

Setelah data berhasil dicrawl dan tidak ada error:

1.  Klik tombol **Sync Data**

2.  Sistem akan mengirim data rencana evaluasi ke Neo Feeder

3.  Tunggu hingga proses selesai

4.  Pastikan tidak muncul notifikasi error

![](media/image138.png){width="6.53125in" height="2.2180555555555554in"}

## ● Catatan Penting {#catatan-penting-15 .unnumbered}

-   Struktur dan komponen evaluasi mengikuti aturan dan validasi Neo Feeder PDDIKTI

-   Jika terjadi error, gunakan fitur **Display Crawl Data** untuk melihat detail

-   Pastikan Status Service dalam kondisi **Terhubung**

-   Pastikan Semester Pelaporan sesuai

### Sinkronisasi Data Non Transaksi -- Rencana Evaluasi (Update)

Menu **Rencana Evaluasi (Update)** berfungsi untuk memperbarui data komponen evaluasi pembelajaran yang sudah pernah dikirim ke Neo Feeder PDDIKTI.

## ● Mengakses Menu {#mengakses-menu-16 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Non Transaksi**

4.  Pilih **Rencana Evaluasi (Update)**

![](media/image139.png){width="6.53125in" height="3.1104166666666666in"}

## ● Mengatur Filter Data {#mengatur-filter-data-16 .unnumbered}

▪ Pilih **Prodi** sesuai kebutuhan![](media/image140.png){width="6.53125in" height="2.4569444444444444in"}

Jika belum pernah dilakukan insert, gunakan menu **Rencana Evaluasi (Insert)** terlebih dahulu.

## ● Crawl Data {#crawl-data-2 .unnumbered}

Tombol **Crawl Data** berfungsi untuk:

-   Menarik ulang data rencana evaluasi dari sistem akademik

-   Membandingkan data akademik dengan data di Neo Feeder

-   Mempersiapkan data yang akan diperbarui

Langkah:

1.  Klik **Crawl Data**

2.  Tunggu hingga proses selesai

3.  Pastikan tidak muncul notifikasi error

![](media/image141.png){width="6.53125in" height="2.311111111111111in"}

## ● Proses Update ke Neo Feeder {#proses-update-ke-neo-feeder-2 .unnumbered}

Setelah proses crawl selesai dan tidak ada error:

1.  Klik tombol **Sync Data**

2.  Sistem akan mengirim perubahan data ke Neo Feeder

3.  Tunggu hingga proses selesai

4.  Pastikan tidak muncul notifikasi error

![](media/image142.png){width="6.53125in" height="2.198611111111111in"}

## ● Catatan Penting {#catatan-penting-16 .unnumbered}

-   Validasi data tetap mengikuti aturan Neo Feeder PDDIKTI

-   Pastikan **Status Service: Terhubung**

### Sinkronisasi Data Transaksi

Menu **Sinkronisasi Data Transaksi** berfungsi untuk mengirim dan memperbarui data akademik yang bersifat *transaksional* (berjalan setiap semester) dari Sistem Akademik ke Neo Feeder PDDIKTI. Berbeda dengan **Data Non Transaksi** (referensi seperti kurikulum, mata kuliah, RPS, dll), menu ini digunakan untuk data operasional per semester seperti kelas, KRS, nilai, dan aktivitas mahasiswa.

Ketika akan melakukan insert data ke Neo Feeder PDDIKTI, gunakan menu-menu dengan pilihan **(Insert)** saja. Apabila akan melakukan pengubahan data yang sudah ada di Neo Feeder PDDIKTI, gunakan menu dengan pilihan **(Update).** Menu-menu dengan **(Update)** hanya dilakukan apabila akan mengubah data yang sudah masuk ke PDDIKTI saja, apabila tidak ada keperluan untuk mengubah data yang sudah masuk ke PDDIKTI, maka menu-menu dengan **(Update)** tidak perlu dilakukan.

### Sinkronisasi Data Transaksi -- Kelas Kuliah (Insert)

Menu **Kelas Kuliah (Insert)** berfungsi untuk mengirimkan data kelas perkuliahan per semester ke Neo Feeder PDDIKTI. Data ini merupakan pembukaan kelas dari suatu Mata Kuliah pada semester tertentu.

## ● Mengakses Menu {#mengakses-menu-17 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Transaksi**

4.  Pilih **Kelas Kuliah (Insert)**

![](media/image143.png){width="6.53125in" height="2.8354166666666667in"}

## ● Mengatur Filter Data {#mengatur-filter-data-17 .unnumbered}

▪ Pilih **Prodi** sesuai kebutuhan\
▪ Pilih **Semester Proses** sesuai semester pelaporan

![](media/image144.png){width="6.53125in" height="2.8256944444444443in"}

## ● Crawl Data {#crawl-data-3 .unnumbered}

Tombol **Crawl Data** berfungsi untuk:

-   Menarik data kelas dari sistem akademik

-   Menyiapkan data kelas yang akan dikirim ke Neo Feeder

Langkah -- Langkah :

1.  Klik **Crawl Data**

2.  Tunggu hingga proses selesai

3.  Pastikan tidak ada notifikasi error

![](media/image145.png){width="6.53125in" height="2.897222222222222in"}

## ● Display Crawl Kls Reguler {#display-crawl-kls-reguler .unnumbered}

Tombol **Display Crawl Kls Reguler** berfungsi untuk:

-   Melihat daftar kelas yang akan dikirim

-   Melihat detail data kelas (kode MK, nama kelas, kapasitas, dll)

-   Melihat error jika ada data yang tidak valid

-   Mengakses informasi panduan perbaikan melalui tombol **info** (jika tersedia)

Jika terdapat error:

-   Perbaiki data di sistem akademik

-   Lakukan ulang proses **Crawl Data**

![](media/image146.png){width="6.53125in" height="2.832638888888889in"}

![](media/image147.png){width="6.53125in" height="3.904166666666667in"}

## ● Proses Insert ke Neo Feeder {#proses-insert-ke-neo-feeder-2 .unnumbered}

Setelah data berhasil dicrawl dan tidak ada error:

1.  Klik tombol **Sync Data Kls Reguler**

2.  Sistem akan mengirim data kelas ke Neo Feeder

3.  Tunggu hingga proses selesai

4.  Pastikan tidak muncul notifikasi error

![](media/image148.png){width="6.53125in" height="2.623611111111111in"}

## ● Catatan Penting {#catatan-penting-17 .unnumbered}

-   Kelas Kuliah harus diinsert sebelum:

    -   Ajar Dosen

    -   Kuliah Mahasiswa (KRS)

    -   Nilai

-   Jika kelas sudah pernah dikirim sebelumnya, gunakan menu **Kelas Kuliah (Update)** untuk update data kelas

-   Validasi data mengikuti aturan Neo Feeder PDDIKTI

### Sinkronisasi Data Transaksi -- Kelas Kuliah (Update)

Menu **Kelas Kuliah (Update)** berfungsi untuk memperbarui data kelas perkuliahan yang sudah pernah dikirim ke Neo Feeder PDDIKTI.

## ● Mengakses Menu {#mengakses-menu-18 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Transaksi**

4.  Pilih **Kelas Kuliah (Update)**

![](media/image149.png){width="6.53125in" height="2.9055555555555554in"}

## ● Mengatur Filter Data {#mengatur-filter-data-18 .unnumbered}

▪ Pilih **Prodi** sesuai kebutuhan\
▪ Pilih **Semester Proses** sesuai semester yang akan diperbarui\
![](media/image150.png){width="6.53125in" height="2.7020833333333334in"}

## ● Crawl Data {#crawl-data-4 .unnumbered}

Tombol **Crawl Data** berfungsi untuk:

-   Menarik data kelas terbaru dari sistem akademik

-   Membandingkan dengan data yang sudah ada di Neo Feeder

-   Menyiapkan data yang mengalami perubahan

Langkah -- Langkah :

1.  Klik **Crawl Data**

2.  Tunggu hingga proses selesai

3.  Pastikan tidak ada notifikasi error

![](media/image151.png){width="6.53125in" height="3.140972222222222in"}

## ● Proses Update ke Neo Feeder {#proses-update-ke-neo-feeder-3 .unnumbered}

Setelah data berhasil dicrawl dan tidak ada error:

1.  Klik tombol **Sync Data**

2.  Sistem akan mengirim perubahan data ke Neo Feeder

3.  Tunggu hingga proses selesai

4.  Pastikan tidak muncul notifikasi error

![](media/image152.png){width="6.53125in" height="3.423611111111111in"}

## ● Catatan Penting {#catatan-penting-18 .unnumbered}

-   Update hanya dapat dilakukan untuk kelas yang sudah terdaftar di Neo Feeder

-   Jika kelas belum pernah dikirim, gunakan menu **Kelas Kuliah (Insert)**

-   Validasi tetap mengikuti aturan Neo Feeder PDDIKTI

### Sinkronisasi Data Transaksi -- Ajar Dosen (Insert)

Menu **Ajar Dosen (Insert)** berfungsi untuk mengirimkan data aktivitas mengajar dosen pada kelas perkuliahan ke Neo Feeder PDDIKTI.

Data yang dikirim meliputi:

-   Relasi dosen dengan kelas kuliah

-   SKS ajar

-   Rencana pertemuan

-   Realisasi jumlah pertemuan

## ● Mengakses Menu {#mengakses-menu-19 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Transaksi**

4.  Pilih **Ajar Dosen (Insert)**

![](media/image153.png){width="6.53125in" height="2.7256944444444446in"}

## ● Mengatur Filter Data {#mengatur-filter-data-19 .unnumbered}

▪ Pilih **Prodi** sesuai kebutuhan\
▪ Pilih **Semester Proses** sesuai semester berjalan\
![](media/image154.png){width="6.53125in" height="2.078472222222222in"}

## ⚠ Catatan Penting Sebelum Insert {#catatan-penting-sebelum-insert .unnumbered}

Pastikan hal berikut sudah terpenuhi:

✔ Master Dosen sudah terdaftar di Neo Feeder PDDIKTI\
✔ Penugasan Dosen (homebase / afiliasi) sudah terdaftar di Neo Feeder\
✔ Kelas Kuliah sudah berhasil diinsert

## ● Crawl Data {#crawl-data-5 .unnumbered}

Tombol **Crawl Data** berfungsi untuk:

-   Menarik data dosen yang mengajar dari sistem akademik

-   Menarik rencana jumlah pertemuan

-   Menarik realisasi pertemuan (jika tersedia)

-   Menyiapkan data untuk dikirim ke Neo Feeder

Langkah -- Langkah :

1.  Klik **Crawl Data**

2.  Tunggu hingga proses selesai

3.  Pastikan tidak ada notifikasi error

![](media/image155.png){width="6.53125in" height="2.1819444444444445in"}

## ● Display Crawl Data {#display-crawl-data-2 .unnumbered}

Tombol **Display Crawl Data** berfungsi untuk:

-   Melihat daftar dosen yang akan dikirim

-   Melihat detail jumlah rencana dan jumlah realisasi pertemuan

Jika terdapat error:

-   Pastikan penugasan dosen sesuai dengan prodi dan semester

-   Perbaiki data di sistem akademik lalu lakukan crawl ulang

![](media/image156.png){width="6.53125in" height="2.6319444444444446in"}

## ● Proses Insert ke Neo Feeder {#proses-insert-ke-neo-feeder-3 .unnumbered}

Setelah data berhasil dicrawl dan valid:

1.  Klik tombol **Sync Data**

2.  Sistem akan mengirim data ajar dosen ke Neo Feeder

3.  Tunggu hingga proses selesai

4.  Pastikan tidak muncul notifikasi error

![](media/image157.png){width="6.53125in" height="2.6180555555555554in"}

## ● Catatan Penting {#catatan-penting-19 .unnumbered}

-   Ajar Dosen (Insert) dilakukan setelah Kelas Kuliah (Insert)

-   Data rencana dan realisasi pertemuan mengikuti aturan validasi Neo Feeder

-   Jika terdapat perubahan data mengajar, gunakan menu **Ajar Dosen (Update)**

### Sinkronisasi Data Transaksi -- Ajar Dosen (Update)

Menu **Ajar Dosen (Update)** digunakan untuk memperbarui data aktivitas mengajar dosen yang **sudah pernah diinsert ke Neo Feeder PDDIKTI**.

Update dilakukan apabila terdapat perubahan, seperti:

-   Perubahan jumlah rencana pertemuan

-   Perubahan realisasi pertemuan

## ● Mengakses Menu {#mengakses-menu-20 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Transaksi**

4.  Pilih **Ajar Dosen (Update)**

![](media/image158.png){width="6.53125in" height="2.470833333333333in"}

## ● Mengatur Filter Data {#mengatur-filter-data-20 .unnumbered}

▪ Pilih **Prodi** sesuai kebutuhan\
▪ Pilih **Semester Proses** sesuai semester yang akan diperbarui\
![](media/image159.png){width="6.53125in" height="2.154166666666667in"}

## ⚠ Syarat Sebelum Update {#syarat-sebelum-update .unnumbered}

Pastikan:

✔ Data Ajar Dosen sudah pernah berhasil diinsert\
✔ Perubahan data sudah diperbaiki di sistem akademik

Jika belum pernah insert, gunakan menu **Ajar Dosen (Insert)** terlebih dahulu.

## ● Crawl Data {#crawl-data-6 .unnumbered}

Tombol **Crawl Data** berfungsi untuk:

-   Menarik ulang data mengajar dosen dari sistem akademik

-   Membandingkan data lokal dengan data di Neo Feeder

-   Menyiapkan data perubahan yang akan dikirim

> Langkah -- Langkah :

1.  Klik **Crawl Data**

2.  Tunggu proses selesai

3.  Pastikan tidak ada notifikasi error

![](media/image160.png){width="6.53125in" height="2.077777777777778in"}

## ● Proses Update ke Neo Feeder {#proses-update-ke-neo-feeder-4 .unnumbered}

Setelah data berhasil dicrawl:

1.  Klik tombol **Sync Data**

2.  Sistem akan mengirim perubahan data ajar dosen ke Neo Feeder

3.  Tunggu hingga proses selesai

4.  Pastikan tidak muncul notifikasi error

![](media/image161.png){width="6.53125in" height="2.1041666666666665in"}

## ● Hal yang Perlu Diperhatikan {#hal-yang-perlu-diperhatikan .unnumbered}

▪ Update hanya berlaku untuk data yang sudah memiliki referensi di Neo Feeder\
▪ Jika dosen diganti total, pastikan dosen baru sudah terdaftar dan gunakan Ajar Dosen (Insert)\
▪ Perubahan rencana dan realisasi pertemuan mengikuti validasi Neo Feeder\
▪ Jika struktur kelas berubah besar (misalnya kelas dihapus dan dibuat ulang), sebaiknya evaluasi kembali alur insert

### Sinkronisasi Data Transaksi -- Nilai (Insert)

Menu **Nilai (Insert)** digunakan untuk mengirimkan data KRS dan nilai mahasiswa pada kelas perkuliahan ke Neo Feeder PDDIKTI.

Data yang dikirim meliputi:

-   Peserta kelas (KRS mahasiswa)

-   Nilai angka

-   Nilai huruf

## ● Mengakses Menu {#mengakses-menu-21 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Pelaporan**

3.  Klik submenu **Sinkronisasi Data Transaksi**

4.  Pilih **Nilai (Insert)**

![](media/image162.png){width="6.53125in" height="1.773611111111111in"}

## ● Mengatur Filter Data {#mengatur-filter-data-21 .unnumbered}

▪ Pilih **Prodi** sesuai kebutuhan\
▪ Pilih **Semester Proses** sesuai semester yang akan dikirim nilainya

![](media/image163.png){width="6.53125in" height="2.2270833333333333in"}

## ⚠ Syarat Sebelum Insert Nilai {#syarat-sebelum-insert-nilai .unnumbered}

Pastikan tahapan berikut sudah dilakukan:

✔ Kelas Kuliah (Insert) sudah berhasil\
✔ Bobot Nilai sudah sinkron

## ● Crawl Data {#crawl-data-7 .unnumbered}

Tombol **Crawl Data** berfungsi untuk:

-   Menarik data peserta kelas dan nilai mahasiswa dari sistem akademik

-   Mengambil nilai angka dan konversi huruf

-   Menyiapkan data untuk dikirim ke Neo Feeder

Langkah -- Langkah :

1.  Klik **Crawl Data**

2.  Tunggu hingga proses selesai

3.  Pastikan tidak ada notifikasi error

![](media/image164.png){width="6.53125in" height="2.0069444444444446in"}

## ● Display Crawl Data {#display-crawl-data-3 .unnumbered}

Tombol **Display Crawl Data** berfungsi untuk:

-   Melihat daftar mahasiswa dan nilai yang akan dikirim

-   Melihat detail nilai angka dan huruf

-   Melihat error data

-   Melihat informasi panduan jika terdapat error

![](media/image165.png){width="6.53125in" height="2.015277777777778in"}

![](media/image166.png){width="6.53125in" height="3.5125in"}

## ● Proses Insert ke Neo Feeder {#proses-insert-ke-neo-feeder-4 .unnumbered}

Setelah data valid:

1.  Klik tombol **Sync Data**

2.  Sistem akan mengirim nilai mahasiswa ke Neo Feeder

3.  Tunggu hingga proses selesai

4.  Pastikan tidak muncul notifikasi error

![](media/image167.png){width="6.53125in" height="2.04375in"}

## ● Ketentuan Penting {#ketentuan-penting-1 .unnumbered}

▪ Nilai yang dikirim harus sesuai rentang bobot nilai yang telah diinsert\
▪ Nilai huruf harus sesuai dengan aturan Neo Feeder PDDIKTI\
▪ Mahasiswa harus berstatus aktif pada semester tersebut\
▪ Nilai hanya dapat diinsert satu kali (selanjutnya gunakan menu Update jika ada perubahan)\
▪ Jika saat proses **Nilai (Insert)** dilakukan data peserta kelas belum memiliki nilai (masih kosong), maka nilai dapat dikirim kemudian menggunakan menu **Nilai (Update)** setelah nilai tersedia di sistem akademik

### Sinkronisasi Data Transaksi -- Nilai (Update)

Menu **Nilai (Update)** digunakan untuk memperbarui data nilai mahasiswa yang **sudah pernah diinsert ke Neo Feeder PDDIKTI**.

Update dilakukan apabila:

-   Nilai baru dimasukkan setelah sebelumnya kosong

-   Terjadi perubahan nilai (angka / huruf)

-   Ada revisi hasil perbaikan nilai

## ● Mengakses Menu {#mengakses-menu-22 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Sinkronisasi Data Transaksi**

3.  Klik **Nilai (Update)**

![](media/image168.png){width="6.53125in" height="1.7416666666666667in"}

## ● Mengatur Filter Data {#mengatur-filter-data-22 .unnumbered}

▪ Pilih **Prodi**\
▪ Pilih **Semester Proses** sesuai semester yang akan diperbarui\
![](media/image169.png){width="6.53125in" height="1.9715277777777778in"}

## ⚠ Syarat Sebelum Update {#syarat-sebelum-update-1 .unnumbered}

Pastikan:

✔ Nilai sudah pernah berhasil diinsert sebelumnya\
✔ Mahasiswa Pesert akelas sudah berhasil diinsert sebelumnya\
✔ Bobot nilai sudah sesuai dan tersinkron\
✔ Perubahan nilai sudah diperbaiki di sistem akademik

✔ Jika Mahasiswa Peserta kelas belum pernah diinsert sama sekali, gunakan menu **Nilai (Insert)** terlebih dahulu.

## ● Crawl Data {#crawl-data-8 .unnumbered}

Tombol **Crawl Data** berfungsi untuk:

-   Menarik ulang data nilai mahasiswa dari sistem akademik

-   Membandingkan nilai lokal dengan data di Neo Feeder

-   Menyiapkan data perubahan untuk dikirim

Langkah -- Langkah :

1.  Klik **Crawl Data**

2.  Tunggu proses selesai

3.  Pastikan tidak ada notifikasi error

![](media/image170.png){width="6.53125in" height="2.341666666666667in"}

## ● Proses Update ke Neo Feeder {#proses-update-ke-neo-feeder-5 .unnumbered}

Setelah data valid:

1.  Klik tombol **Sync Data**

2.  Sistem akan mengirim perubahan nilai ke Neo Feeder

3.  Tunggu hingga proses selesai

4.  Pastikan tidak muncul notifikasi error

![](media/image171.png){width="6.53125in" height="2.4916666666666667in"}

## ● Ketentuan Penting {#ketentuan-penting-2 .unnumbered}

▪ Menu ini digunakan untuk mengirim nilai yang sebelumnya kosong saat proses Insert\
▪ Digunakan juga untuk koreksi atau perubahan nilai\
▪ Nilai harus sesuai dengan rentang bobot nilai yang berlaku\
▪ Tidak dapat digunakan untuk mahasiswa yang belum pernah terdaftar di kelas

### Sinkronisasi Data Transaksi -- Nilai Transfer (Insert)

Menu **Nilai Transfer (Insert)** digunakan untuk mengirimkan data nilai konversi/transfer mahasiswa (Pindahan, RPL Transfer SKS, RPL Perolehan SKS, Pertukaran Pelajar MBKM) ke Neo Feeder PDDIKTI.

Data yang dikirim meliputi:

-   Mata kuliah asal

-   Mata kuliah yang diakui (konversi)

-   SKS diakui

-   Nilai angka / huruf hasil konversi

## ● Mengakses Menu {#mengakses-menu-23 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Sinkronisasi Data Transaksi**

3.  Klik **Nilai Transfer (Insert)**

![](media/image172.png){width="6.53125in" height="2.3381944444444445in"}

## ● Mengatur Filter Data {#mengatur-filter-data-23 .unnumbered}

▪ Pilih **Prodi**\
▪ Pilih **Angkatan Tahun**\
▪ Isi **NIM** atau **Nama** jika ingin spesifik\
▪ Pastikan Semester Pelaporan sesuai

![](media/image173.png){width="6.53125in" height="2.3833333333333333in"}

## ⚠ Syarat Sebelum Insert Nilai Transfer {#syarat-sebelum-insert-nilai-transfer .unnumbered}

Pastikan:

✔ Mahasiswa sudah terdaftar di Neo Feeder\
✔ Status mahasiswa aktif atau sesuai ketentuan\
✔ Mata kuliah tujuan (yang diakui) sudah terdaftar\
✔ Data konversi sudah lengkap di sistem akademik

Jika master mahasiswa atau mata kuliah belum ada, proses insert akan gagal.

## ● Crawl Data {#crawl-data-9 .unnumbered}

Tombol **Crawl Data** berfungsi untuk:

-   Menarik data nilai transfer dari sistem akademik

-   Menampilkan daftar mata kuliah yang dikonversi

-   Menyiapkan data untuk dikirim ke Neo Feeder

Langkah -- Langkah :

1.  Klik **Crawl Data**

2.  Tunggu proses selesai

3.  Pastikan tidak ada notifikasi error

![](media/image174.png){width="6.53125in" height="2.9125in"}

## ● Display Crawl Data {#display-crawl-data-4 .unnumbered}

Tombol **Display Crawl Data** berfungsi untuk:

-   Melihat detail mata kuliah asal dan konversi

-   Melihat SKS yang diakui

-   Melihat nilai hasil konversi

-   Melihat error dan panduan perbaikan jika ada

![](media/image175.png){width="6.53125in" height="2.2944444444444443in"}

![](media/image176.png){width="6.53125in" height="2.236111111111111in"}

## ● Proses Insert ke Neo Feeder {#proses-insert-ke-neo-feeder-5 .unnumbered}

Setelah data valid:

1.  Klik **Sync Data**

2.  Sistem akan mengirim data nilai transfer ke Neo Feeder

3.  Tunggu hingga proses selesai

4.  Pastikan tidak muncul notifikasi error

![](media/image177.png){width="6.53125in" height="2.4291666666666667in"}

## ● Ketentuan Penting {#ketentuan-penting-3 .unnumbered}

▪ Nilai transfer hanya dikirim satu kali (selanjutnya gunakan menu Update jika ada perubahan)\
▪ SKS diakui tidak boleh melebihi ketentuan kurikulum\
▪ Nilai harus sesuai dengan bobot nilai yang berlaku\
▪ Data transfer harus sesuai dengan dokumen resmi konversi

### Sinkronisasi Data Transaksi -- Nilai Transfer (Update)

Menu **Nilai Transfer (Update)** digunakan untuk memperbarui data nilai transfer mahasiswa yang **sudah pernah diinsert ke Neo Feeder PDDIKTI**.

Update dilakukan apabila terdapat:

-   Perubahan nilai hasil konversi

## ● Mengakses Menu {#mengakses-menu-24 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Sinkronisasi Data Transaksi**

3.  Klik **Nilai Transfer (Update)**

![](media/image178.png){width="6.53125in" height="2.25in"}

## ● Mengatur Filter Data {#mengatur-filter-data-24 .unnumbered}

▪ Pilih **Prodi**\
▪ Pilih **Angkatan Tahun** (opsional)\
▪ Isi **NIM** atau **Nama** jika ingin spesifik\
▪ Pastikan Semester Pelaporan sesuai

Filter digunakan untuk memudahkan pencarian data mahasiswa yang akan diperbarui.

![](media/image179.png){width="6.53125in" height="2.5284722222222222in"}

## ⚠ Syarat Sebelum Update {#syarat-sebelum-update-2 .unnumbered}

Pastikan:

✔ Data nilai transfer sudah pernah berhasil diinsert\
✔ Perubahan sudah diperbaiki di sistem akademik

Jika belum pernah dilakukan Insert, gunakan menu **Nilai Transfer (Insert)** terlebih dahulu.

## ● Crawl Data {#crawl-data-10 .unnumbered}

Tombol **Crawl Data** berfungsi untuk:

-   Menarik ulang data nilai transfer dari sistem akademik

-   Membandingkan data lokal dengan data di Neo Feeder

-   Menyiapkan perubahan yang akan dikirim

Langkah:

1.  Klik **Crawl Data**

2.  Tunggu proses selesai

3.  Pastikan tidak ada notifikasi error

![](media/image180.png){width="6.53125in" height="2.402083333333333in"}

## ● Proses Update ke Neo Feeder {#proses-update-ke-neo-feeder-6 .unnumbered}

Setelah data valid:

1.  Klik tombol **Sync Data**

2.  Sistem akan mengirim perubahan nilai transfer ke Neo Feeder

3.  Tunggu hingga proses selesai

4.  Pastikan tidak muncul notifikasi error

![](media/image181.png){width="6.53125in" height="2.4319444444444445in"}

## ● Ketentuan Penting {#ketentuan-penting-4 .unnumbered}

▪ Digunakan hanya untuk data yang sudah memiliki referensi di Neo Feeder\
▪ Perubahan SKS tidak boleh melanggar ketentuan kurikulum\
▪ Nilai harus sesuai dengan rentang bobot nilai yang berlaku\
▪ Tidak dapat digunakan untuk mahasiswa yang belum pernah memiliki data transfer

### Sinkronisasi Data Transaksi -- Kuliah Mahasiswa (Insert)

Menu **Kuliah Mahasiswa (Insert)** digunakan untuk mengirimkan data **Aktivitas Kuliah Mahasiswa per semester** ke Neo Feeder PDDIKTI.

Data yang dikirim merupakan ringkasan aktivitas akademik mahasiswa pada semester berjalan.

Menu ini akan menarik data **Aktivitas Kuliah Mahasiswa**, yang terdiri dari:

-   Status Mahasiswa (Aktif, Non Aktif, Cuti, kampus merdeka, menunggu ujian)

-   IP Semester

-   IP Kumulatif

-   Jumlah SKS Semester

-   Jumlah SKS Total

-   Jenis Pembiayaan (Mandiri, Beasiswa Tidak Penuh, Beasiswa Penuh)

-   Biaya Kuliah Semester

## ● Mengakses Menu {#mengakses-menu-25 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Sinkronisasi Data Transaksi**

3.  Klik **Kuliah Mahasiswa (Insert)**

![](media/image182.png){width="6.53125in" height="1.6152777777777778in"}

## ● Mengatur Filter Data {#mengatur-filter-data-25 .unnumbered}

▪ Pilih **Prodi**\
▪ Pilih **Semester Proses** sesuai semester pelaporan\
![](media/image183.png){width="6.53125in" height="2.134027777777778in"}

## ⚠ Syarat Sebelum Insert {#syarat-sebelum-insert .unnumbered}

Pastikan:

✔ Mahasiswa sudah terdaftar di Neo Feeder\
✔ Status mahasiswa sudah benar di sistem akademik\
✔ Nilai semester sudah lengkap\
✔ Data SKS semester dan total sudah sesuai\
✔ Jenis pembiayaan dan biaya kuliah sudah diinput

Jika mahasiswa belum terdaftar, proses insert akan gagal.

## ● Crawl Data {#crawl-data-11 .unnumbered}

Tombol **Crawl Data** berfungsi untuk:

-   Menarik data aktivitas kuliah mahasiswa dari sistem akademik

-   Mengambil status semester mahasiswa

-   Mengambil IP Semester dan IP Kumulatif

-   Mengambil total SKS semester dan kumulatif

-   Mengambil data pembiayaan dan biaya kuliah

Langkah -- Langkah :

1.  Klik **Crawl Data**

2.  Tunggu hingga proses selesai

3.  Pastikan tidak ada notifikasi error

![](media/image184.png){width="6.53125in" height="1.9791666666666667in"}

## ● Display Crawl Data {#display-crawl-data-5 .unnumbered}

Tombol **Display Crawl Data** berfungsi untuk:

-   Melihat daftar mahasiswa yang akan dikirim

-   Melihat detail status dan IP

-   Melihat detail SKS semester dan total

-   Melihat jenis pembiayaan

-   Melihat error dan panduan jika ada kesalahan

![](media/image185.png){width="6.53125in" height="1.9076388888888889in"}

![](media/image186.png){width="6.53125in" height="2.540277777777778in"}

## ● Proses Insert ke Neo Feeder {#proses-insert-ke-neo-feeder-6 .unnumbered}

Setelah data valid:

1.  Klik **Sync Data**

2.  Sistem akan mengirim data aktivitas kuliah ke Neo Feeder

3.  Tunggu hingga proses selesai

4.  Pastikan tidak muncul notifikasi error

![](media/image187.png){width="6.53125in" height="1.85in"}

## ● Ketentuan Penting {#ketentuan-penting-5 .unnumbered}

▪ Aktivitas kuliah dikirim setiap semester\
▪ Status mahasiswa harus sesuai kondisi semester tersebut\
▪ IP Semester dan IP Kumulatif harus konsisten dengan data nilai

▪ Sebelum proses, dapat dipastikan sudah dilakukan proses Rekap Nilai atau Buat Transkrip di Akademik\
▪ Jika sebelumnya sudah pernah dikirim, gunakan menu **Kuliah Mahasiswa (Update)** untuk perubahan data

### Sinkronisasi Data Transaksi -- Kuliah Mahasiswa (Update)

Menu **Kuliah Mahasiswa (Update)** digunakan untuk memperbarui data **Aktivitas Kuliah Mahasiswa per semester** yang **sudah pernah diinsert ke Neo Feeder PDDIKTI**.

Menu ini memperbarui data Aktivitas Kuliah Mahasiswa, meliputi:

-   Status Mahasiswa (Aktif, Non Aktif, Cuti, kampus merdeka, menunggu ujian)

-   IP Semester

-   IP Kumulatif

-   Jumlah SKS Semester

-   Jumlah SKS Total

-   Jenis Pembiayaan (Mandiri, Beasiswa Tidak Penuh, Beasiswa Penuh)

-   Biaya Kuliah Semester

## ● Mengakses Menu {#mengakses-menu-26 .unnumbered}

1.  Login ke aplikasi **eFeeder**

2.  Pilih menu **Sinkronisasi Data Transaksi**

3.  Klik **Kuliah Mahasiswa (Update)**

![](media/image188.png){width="6.53125in" height="1.7631944444444445in"}

## ● Mengatur Filter Data {#mengatur-filter-data-26 .unnumbered}

▪ Pilih **Prodi**\
▪ Pilih **Semester Proses** sesuai semester yang akan diperbarui\
![](media/image189.png){width="6.53125in" height="2.120833333333333in"}

## ⚠ Syarat Sebelum Update {#syarat-sebelum-update-3 .unnumbered}

Pastikan:

✔ Data aktivitas semester sudah pernah berhasil diinsert\
✔ Mahasiswa sudah ada di Neo Feeder\
✔ Perubahan data sudah diperbaiki di sistem akademik\
✔ IP dan SKS sudah final dan konsisten dengan data nilai

Jika belum pernah dilakukan Insert, gunakan menu **Kuliah Mahasiswa (Insert)** terlebih dahulu.

## ● Crawl Data {#crawl-data-12 .unnumbered}

Tombol **Crawl Data** berfungsi untuk:

-   Menarik ulang data aktivitas semester mahasiswa

-   Membandingkan data lokal dengan data di Neo Feeder

-   Menyiapkan perubahan yang akan dikirim

Langkah -- Langkah :

1.  Klik **Crawl Data**

2.  Tunggu proses selesai

3.  Pastikan tidak ada notifikasi error

![](media/image190.png){width="6.53125in" height="2.020138888888889in"}

## ● Proses Update ke Neo Feeder {#proses-update-ke-neo-feeder-7 .unnumbered}

Setelah data valid:

1.  Klik tombol **Sync Data**

2.  Sistem akan mengirim perubahan aktivitas semester ke Neo Feeder

3.  Tunggu hingga proses selesai

4.  Pastikan tidak muncul notifikasi error

![](media/image191.png){width="6.53125in" height="1.8402777777777777in"}

## ● Ketentuan Penting {#ketentuan-penting-6 .unnumbered}

▪ Digunakan hanya untuk semester yang sudah memiliki data di Neo Feeder\
▪ Status mahasiswa harus sesuai kondisi aktual semester tersebut\
▪ IP Semester dan IP Kumulatif harus sesuai dengan nilai yang telah dilaporkan\
▪ Perubahan SKS harus konsisten dengan total mata kuliah yang diambil\
▪ Jenis pembiayaan dan biaya kuliah harus sesuai data resmi institusi

### Sinkronisasi Data Transaksi

### Sinkronisasi Data Transaksi

### Sinkronisasi Data Transaksi

### Sinkronisasi Data Transaksi

### Sinkronisasi Data Transaksi
