# Materi Minggu 6: Distributed File System

**Prompt:**

Buatkan rangkuman materi berdasarkan modul 6 berjudul *Distributed File System*. Rangkum seluruh materi sesuai urutan pembahasan dalam modul, gunakan bahasa Indonesia yang formal, jelas, dan mudah dipahami. Pertahankan istilah teknis, konsep, contoh, serta penjelasan penting yang terdapat dalam modul. Susun hasilnya menggunakan format Markdown agar dapat dimasukkan ke dalam file README.md di GitHub.

**AI yang digunakan:** ChatGPT (GPT-6)

**Bagian yang disesuaikan dari keluaran prompt ada pada:**
- Penyusunan struktur materi agar lebih teratur dan mudah dibaca.
- Penyederhanaan beberapa kalimat tanpa mengubah inti pembahasan.
- Penggunaan format Markdown berupa judul, subjudul, dan poin-poin.

---

## 1. Pengertian File System

File System (FS) merupakan metode yang digunakan oleh sistem operasi untuk mengelola dan mengatur file pada media penyimpanan, seperti hard disk, USB flashdisk, dan SSD.

File System memiliki berbagai jenis sesuai sistem operasi yang digunakan, antara lain:

- **Linux:** ext4, XFS, btrfs, dan ReiserFS.
- **DOS/Windows:** FAT16, FAT32, dan NTFS.
- **Mac:** APFS (Apple File System).

File System diakses melalui *file system driver* yang dikelola oleh kernel. Kernel menyediakan Virtual File System (VFS) agar aplikasi pada user space dapat mengakses file tanpa harus mengetahui detail implementasi setiap jenis File System.

File System juga berbeda dengan hierarki File System. Hierarki File System merupakan susunan file dan direktori dalam sistem operasi, sedangkan File System mengatur bagaimana data disimpan dan dikelola pada media penyimpanan.

## 2. Cara Kerja File System

Secara umum, proses akses file melalui beberapa lapisan, yaitu:

1. **Aplikasi:** aplikasi meminta akses terhadap file.
2. **System Call Interface:** meneruskan permintaan aplikasi kepada kernel.
3. **Virtual File System (VFS):** menyediakan antarmuka umum agar aplikasi dapat menggunakan berbagai jenis File System.
4. **Driver Kernel:** menangani operasi sesuai jenis File System yang digunakan.
5. **Hardware:** media penyimpanan yang digunakan untuk menyimpan atau mengambil data.

Dengan mekanisme tersebut, aplikasi dapat mengakses file tanpa perlu berkomunikasi langsung dengan perangkat penyimpanan.

## 3. Pengertian Distributed File System (DFS)

Distributed File System (DFS) merupakan sistem abstraksi terkoordinasi dari sekumpulan media penyimpanan yang tersebar pada beberapa node. DFS menyatukan penyimpanan tersebut sehingga terlihat oleh pengguna seperti satu media penyimpanan.

DFS tidak hanya sekadar menyimpan file pada beberapa mesin, tetapi juga mengelola perbedaan perangkat, kegagalan, dan akses secara bersamaan (*concurrency*). Tujuannya adalah menghasilkan jaringan penyimpanan yang terintegrasi, andal, dan memiliki kinerja tinggi.

### 3.1 Perbedaan DAS, DFS, NAS, dan SAN

Beberapa konsep penyimpanan yang berkaitan dengan DFS adalah:

- **DAS (Direct-Attached Storage):** media penyimpanan yang terhubung langsung ke suatu komputer atau server.
- **DFS (Distributed File System):** sistem berbasis perangkat lunak yang mengelola file dan direktori pada beberapa node penyimpanan.
- **NAS (Network-Attached Storage):** penyimpanan yang menyediakan akses file melalui jaringan.
- **SAN (Storage Area Network):** jaringan penyimpanan yang menyediakan perangkat penyimpanan dalam bentuk block-level devices agar dapat dihubungkan dan diformat oleh server menggunakan File System sendiri.

DFS bekerja pada tingkat abstraksi perangkat lunak dan mengelola data sebagai file serta direktori. Sementara itu, SAN menyediakan penyimpanan dalam bentuk blok.

SAN secara konseptual dapat digunakan sebagai media penyimpanan untuk DFS, meskipun modul menyebutkan bahwa penggunaan tersebut tidak disarankan. Contoh penggunaan SAN meliputi backend database skala besar, pengolahan video dan audio, serta virtualisasi skala besar.

## 4. Berbagai Distributed File System yang Umum

Beberapa contoh Distributed File System yang digunakan adalah:

1. **Google File System (GFS):** sistem penyimpanan terdistribusi yang dikembangkan Google.
2. **Colossus:** sistem yang menggantikan Google File System dan digunakan pada layanan seperti YouTube, Gmail, dan Google Docs.
3. **CephFS:** Distributed File System yang merupakan bagian dari ekosistem Ceph.
4. **Gluster:** sistem penyimpanan terdistribusi yang menggabungkan kapasitas penyimpanan dari beberapa server.
5. **HDFS (Hadoop Distributed File System):** sistem penyimpanan terdistribusi yang digunakan dalam ekosistem Apache Hadoop.
6. **Lustre:** Distributed File System yang digunakan untuk kebutuhan penyimpanan berkinerja tinggi.

## 5. Cara Kerja Distributed File System

DFS menggabungkan beberapa media penyimpanan yang berada pada node berbeda menjadi satu sistem penyimpanan yang dapat diakses pengguna.

Secara umum, DFS mengatur penyimpanan dan akses file melalui jaringan. Data dapat ditempatkan pada beberapa node, sementara sistem mengelola distribusi dan koordinasi penyimpanan tersebut.

Dengan pendekatan ini, pengguna tidak harus mengetahui lokasi fisik setiap file. DFS juga dirancang untuk menghadapi perbedaan perangkat, kegagalan komponen, dan akses secara bersamaan.

## 6. Studi Kasus: Hadoop Distributed File System (HDFS)

HDFS merupakan File System yang bersifat open source, scalable, terdistribusi, dan fault-tolerant. HDFS dirancang untuk mengelola serta menyimpan dataset berukuran besar pada cluster yang terdiri dari commodity hardware.

**Commodity hardware** merupakan perangkat keras komputer yang diproduksi secara massal, memiliki harga relatif terjangkau, mudah dipertukarkan, dan tersedia dari berbagai vendor.

HDFS merupakan salah satu komponen utama Apache Hadoop. Sistem ini digunakan untuk pemrosesan data skala besar dengan cara:
- Membagi file menjadi beberapa blok.
- Mendistribusikan blok ke beberapa server.
- Mereplikasi blok untuk meningkatkan ketersediaan data (*high availability*).

Melalui mekanisme tersebut, HDFS dapat menyimpan dataset berukuran besar dengan memanfaatkan beberapa komputer dalam satu cluster.

Modul juga mencantumkan Apache Hadoop 3.5.0 yang dikompilasi menggunakan JDK 17 dan dapat dijalankan menggunakan Java 17 untuk server serta Java 17 atau Java 21 untuk client.

Untuk memahami cara kerja HDFS secara langsung, modul mengarahkan mahasiswa untuk mempraktikkan penggunaannya berdasarkan dokumen yang disertakan pada EL-UTDI.

## 7. Pengertian Cloud Storage

Cloud Storage merupakan layanan penyimpanan data secara online yang memungkinkan pengguna menyimpan dan mengakses data melalui jaringan internet, tanpa harus menyimpan seluruh data pada hard drive lokal atau perangkat fisik milik pengguna.

Data disimpan dalam kumpulan penyimpanan logis (*logical pool*) yang dikelola secara jarak jauh oleh penyedia layanan cloud.

Secara fisik, penyimpanan dapat terdiri dari beberapa server yang berada di satu atau beberapa lokasi. Infrastruktur tersebut biasanya dimiliki dan dikelola oleh penyedia cloud computing.

Contoh layanan Cloud Storage:
- **Amazon S3:** https://aws.amazon.com/s3/
- **Azure Blob Storage.**
- **Google Cloud Storage (GCS).**

## 8. Relasi Cloud Storage dengan Distributed File System

Cloud Storage berfungsi sebagai tempat penyimpanan data, sedangkan Distributed File System dapat mengatur pengorganisasian dan operasi file pada penyimpanan tersebut.

Salah satu contoh yang dijelaskan dalam modul adalah penggunaan Amazon S3 sebagai media penyimpanan untuk HDFS. Dalam penerapan ini, S3 menyediakan penyimpanan berbasis cloud, sementara operasi File System dilakukan oleh HDFS.

Penggunaan tersebut dapat dilakukan melalui konfigurasi pada file `core-site.xml`.

## 9. Tipe Cloud Storage

Cloud Storage memiliki tiga tipe utama berdasarkan cara data disimpan dan diakses.

### 9.1 Object Storage

Object Storage menyimpan data sebagai objek yang terdiri dari data itu sendiri, metadata, dan identifier unik. Tipe ini umum digunakan untuk menyimpan data dalam jumlah besar, seperti gambar, video, dan file cadangan.

### 9.2 File Storage

File Storage menyimpan data dalam bentuk file dan direktori dengan struktur hierarki. Pengguna dapat mengakses data melalui susunan folder dan nama file.

### 9.3 Block Storage

Block Storage membagi data menjadi blok-blok berukuran tertentu. Setiap blok dapat dikelola dan diakses sebagai unit penyimpanan oleh sistem atau aplikasi.

## 10. Studi Kasus Cloud Storage

Pada bagian studi kasus, modul menyertakan referensi mengenai arsitektur CubeFS.

CubeFS merupakan sistem penyimpanan terdistribusi yang dokumentasi arsitekturnya digunakan sebagai bahan pembahasan Cloud Storage.

Referensi dokumentasi: https://cubefs.io/docs/master/overview/architecture.html#architecture

## 11. Kesimpulan

File System merupakan bagian dari sistem operasi yang bertugas mengelola file pada media penyimpanan. Dalam perkembangannya, Distributed File System memungkinkan beberapa media penyimpanan pada node berbeda dikelola sebagai satu sistem terpadu.

DFS membantu menyediakan penyimpanan yang terintegrasi, andal, dan berkinerja tinggi. Salah satu penerapannya adalah HDFS pada Apache Hadoop, yang membagi file menjadi blok, mendistribusikannya ke beberapa server, dan melakukan replikasi untuk meningkatkan ketersediaan data.

Sementara itu, Cloud Storage menyediakan layanan penyimpanan data melalui jaringan internet dengan infrastruktur yang dikelola oleh penyedia cloud. Cloud Storage dapat digunakan bersama DFS, dan memiliki tiga tipe utama, yaitu Object Storage, File Storage, dan Block Storage.
