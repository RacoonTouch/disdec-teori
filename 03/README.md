## Materi Minggu 3: Sinkronisasi dan Koordinasi pada Sistem Terdistribusi

**Prompt:** Buatkan rangkuman materi dari modul PDF yang diberikan menggunakan bahasa Indonesia formal, jelas, ringkas, dan terstruktur. Pertahankan istilah, konsep, contoh, serta urutan pembahasan sesuai modul. Susun hasilnya dalam format Markdown untuk README.md GitHub.

**AI yang digunakan:** ChatGPT (GPT-6).

**Bagian yang disesuaikan dari keluaran prompt ada pada:** Penyusunan struktur pembahasan, pemilihan kalimat, dan format Markdown agar sesuai dengan template tugas. Materi utama tetap mengacu pada modul.

## 1. Pengertian Sinkronisasi

Sinkronisasi merupakan proses koordinasi antara proses, data, dan sumber daya pada berbagai node dalam sistem terdistribusi untuk memastikan operasi berjalan secara konsisten dan andal. Sinkronisasi diperlukan karena setiap node dapat menjalankan proses secara bersamaan sehingga berpotensi menimbulkan konflik data atau race condition.

Contohnya adalah sistem e-commerce yang memiliki stok produk sebanyak 10 unit. Ketika dua pengguna membeli produk secara bersamaan, keduanya dapat membaca stok awal sebanyak 10 unit. Setelah masing-masing transaksi mengurangi stok menjadi 9, sistem justru mencatat dua pembelian dengan sisa stok 9, padahal seharusnya tersisa 8 unit. Kondisi ini terjadi karena tidak adanya sinkronisasi terhadap proses perubahan stok.

## 2. Pentingnya Sinkronisasi

Sinkronisasi memiliki beberapa tujuan penting dalam sistem terdistribusi, yaitu:

- Integritas data: Mencegah data race dan race condition agar data tetap benar.
- Sinkronisasi state: Menjaga agar kondisi aplikasi pada seluruh node tetap sesuai.
- Koordinasi tasks: Mengatur pelaksanaan tugas antarproses agar berjalan dengan baik.
- Pengelolaan resources: Mengatur penggunaan sumber daya bersama.
- Recovery: Mempertahankan state agar sistem dapat melakukan pemulihan ketika terjadi kegagalan.
- Utilisasi efisien: Mencegah operasi yang berulang atau tidak diperlukan.
- Load balancing: Membantu pembagian beban kerja.
- Mencegah deadlock: Menghindari kondisi ketika proses saling menunggu sumber daya.
- Scalable operations: Mendukung peningkatan kapasitas dan jumlah proses sistem.

## 3. Tantangan Sinkronisasi

Dalam penerapannya, sinkronisasi pada sistem terdistribusi menghadapi beberapa tantangan, yaitu:

- Network latency dan partitioning: Keterlambatan komunikasi dan terputusnya koneksi antar-node dapat menghambat sinkronisasi.
- Skalabilitas: Semakin banyak node, semakin kompleks proses koordinasinya.
- Fault-tolerant system: Sinkronisasi harus tetap berjalan ketika sebagian node mengalami kegagalan.
- Concurrency control: Mengatur proses yang berjalan secara bersamaan agar tidak menimbulkan konflik.
- Data consistency: Menjaga kesesuaian data antar-node.
- Sinkronisasi waktu: Menyamakan atau mengatur urutan waktu dan kejadian pada sistem.

## 4. Sinkronisasi Waktu Fisik

Sinkronisasi waktu fisik merupakan proses menyelaraskan real-time clock atau jam nyata pada berbagai komputer dalam sistem terdistribusi menggunakan standar waktu yang sama. Hal ini penting untuk korelasi log, penjadwalan event, dan menjaga konsistensi sistem.

Sinkronisasi waktu dapat dilakukan menggunakan protokol jaringan atau sumber waktu berbasis perangkat keras seperti atomic clock dan GPS.

### 4.1 Standar Waktu

Beberapa standar waktu yang dijelaskan dalam modul adalah:

- GMT (Greenwich Mean Time): Standar waktu yang dahulu digunakan dan saat ini sudah tidak digunakan sebagai standar utama.
- UTC (Coordinated Universal Time): Standar waktu internasional yang didefinisikan oleh ITU dan digunakan sejak tahun 1963.
- TAI (International Atomic Time): Standar waktu yang didasarkan pada pengukuran atomic clock dan menjadi dasar bagi UTC.
- LTC (Coordinated Lunar Time): Standar waktu untuk kebutuhan aktivitas di Bulan yang masih dalam proses pengembangan.

### 4.2 Sumber Waktu dan Sinkronisasi

Atomic clock merupakan sumber waktu dengan tingkat ketelitian tinggi. GPS juga menggunakan atomic clock pada satelitnya untuk menghasilkan sinyal waktu.

Alur sinkronisasi waktu yang dijelaskan dalam modul adalah penggunaan master atomic clock, atomic clock pada satelit GPS, GPS dongle, server Linux, kemudian client seperti Linux, Windows, Mac, dan perangkat mobile. Proses sinkronisasi antara server dan client dapat menggunakan protokol NTP atau PTP.

Modul juga membahas sumber atomic clock, antara lain satelit GPS, Deep Space Atomic Clock (DSAC), International Space Station (ISS) melalui misi ACES, serta pengelolaan master clock di stasiun kontrol darat.

### 4.3 Network Time Protocol (NTP)

Network Time Protocol merupakan protokol yang digunakan untuk menyinkronkan waktu komputer melalui jaringan. NTP memungkinkan perangkat memperoleh referensi waktu dari server sehingga jam lokal dapat disesuaikan dengan standar waktu yang digunakan.

### 4.4 Precision Time Protocol (PTP)

Precision Time Protocol merupakan protokol sinkronisasi waktu yang distandardisasi oleh IEEE 1588. PTP digunakan untuk memperoleh sinkronisasi waktu dengan tingkat presisi tinggi.

Modul menjelaskan beberapa perkembangan standar PTP, yaitu IEEE 1588-2002, IEEE 1588-2008, dan IEEE 1588-2019. Selain itu, terdapat IEEE 802.1AS yang merupakan adaptasi PTP untuk Audio Video Bridging (AVB) dan Time-Sensitive Networking (TSN).

Salah satu persyaratan penggunaan PTP dengan presisi tinggi adalah Network Interface Card (NIC) harus mendukung hardware timestamping.

## 5. Sinkronisasi Waktu Logis

Sinkronisasi waktu logis merupakan metode untuk menentukan urutan sebab-akibat dari berbagai kejadian dalam sistem terdistribusi. Berbeda dengan waktu fisik, waktu logis tidak bergantung pada jam nyata, melainkan digunakan untuk mengetahui hubungan urutan kejadian.

Prinsip dasarnya adalah jika kejadian A terjadi sebelum B dan B terjadi sebelum C, maka A juga terjadi sebelum C. Konsep ini berkaitan dengan algoritma Lamport Logical Clock yang telah dibahas pada materi sebelumnya.

## 6. Vector Clocks

Vector Clocks merupakan mekanisme pencatatan urutan kejadian dengan menggunakan kumpulan nilai clock untuk setiap proses dalam sistem terdistribusi. Berbeda dengan Lamport Logical Clock yang menggunakan satu nilai, Vector Clocks menggunakan vektor yang memiliki satu komponen untuk setiap proses.

Contohnya, jika terdapat tiga proses A, B, dan C, setiap proses memiliki vector clock awal [0, 0, 0]. Setiap kali terjadi event, komponen yang mewakili proses tersebut akan bertambah satu.

Aturan Vector Clocks meliputi:

1. Setiap terjadi event internal atau pengiriman pesan, proses menambahkan satu pada komponen clock miliknya.
2. Saat mengirim pesan, proses menyertakan nilai vector clock ke dalam pesan.
3. Saat menerima pesan, proses membandingkan vector clock yang diterima dengan clock lokal menggunakan elemen-wise maximum.
4. Setelah menggabungkan nilai clock, proses menambahkan satu pada komponen miliknya ketika mencatat event penerimaan.

Hubungan urutan kejadian ditentukan dengan aturan berikut:

- Event A terjadi sebelum B jika seluruh komponen vector clock A lebih kecil atau sama dengan B dan setidaknya satu komponen lebih kecil.
- Dua event dikatakan concurrent atau independen jika tidak memenuhi hubungan urutan tersebut.

Vector Clocks membantu mengetahui hubungan sebab-akibat dan mendeteksi kejadian yang berlangsung secara independen dalam sistem terdistribusi.

## 7. Tantangan Mutual Exclusion

Mutual Exclusion merupakan prinsip yang memastikan hanya satu proses atau thread yang dapat mengakses sumber daya bersama pada waktu tertentu. Tujuannya adalah mencegah konflik dan menjaga integritas data.

Sumber daya bersama dapat berupa printer, file, dan database. Bagian kode yang mengakses sumber daya bersama disebut Critical Section (CS). Jika beberapa proses mengakses bagian tersebut secara bersamaan tanpa pengaturan, dapat terjadi inkonsistensi atau kerusakan data.

Prinsip utama Mutual Exclusion adalah:

- Mutual Exclusion: Hanya satu proses yang boleh mengakses sumber daya bersama pada satu waktu.
- Progress: Jika tidak ada proses yang sedang menggunakan critical section, proses lain harus memiliki kesempatan untuk mengaksesnya.
- Bounded Waiting: Tidak boleh ada proses yang menunggu tanpa batas waktu.
- Fairness: Permintaan akses harus dilayani secara adil berdasarkan urutan yang wajar.

### 7.1 Centralized Algorithm

Centralized Algorithm menggunakan satu node sebagai koordinator untuk mengatur akses ke critical section.

Tahapannya adalah:
1. Proses mengirim permintaan izin kepada koordinator.
2. Koordinator memberikan izin jika critical section sedang tidak digunakan.
3. Setelah proses selesai, koordinator memberikan izin kepada proses berikutnya.

Kelebihannya adalah sederhana dan memiliki biaya komunikasi yang relatif rendah. Kekurangannya adalah adanya single point of failure dan kemungkinan bottleneck pada koordinator.

### 7.2 Ricart-Agrawala Algorithm

Ricart-Agrawala merupakan algoritma mutual exclusion yang bekerja secara terdistribusi tanpa menggunakan koordinator pusat. Setiap proses mengirimkan pesan permintaan akses yang dilengkapi timestamp kepada proses lainnya.

Proses dapat memasuki critical section setelah menerima balasan OK dari seluruh proses lainnya.

Jumlah pesan yang diperlukan untuk setiap akses critical section adalah 2 x (N - 1), yaitu N - 1 pesan permintaan dan minimal N - 1 pesan balasan.

Kelebihannya adalah tidak bergantung pada koordinator pusat, sedangkan kekurangannya adalah overhead komunikasi yang tinggi.

### 7.3 Token-Based Algorithm

Token-Based Algorithm menggunakan satu token unik yang beredar di antara proses. Proses hanya dapat memasuki critical section jika memiliki token tersebut.

Kelebihannya adalah hanya membutuhkan satu pesan untuk setiap entri critical section ketika token tersedia. Kekurangannya adalah kesulitan mendeteksi kehilangan token sehingga diperlukan mekanisme pemulihan.

## 8. Pemilihan Koordinator

Pemilihan koordinator merupakan proses menentukan satu node sebagai pemimpin untuk mengatur berbagai aktivitas dalam sistem terdistribusi. Koordinator dibutuhkan untuk mengelola sumber daya bersama, menyinkronkan operasi, dan membuat keputusan global.

Jika koordinator mengalami kegagalan atau terdapat node baru yang bergabung, sistem perlu melakukan pemilihan pemimpin baru secara otomatis agar koordinasi tetap berjalan.

Beberapa algoritma pemilihan koordinator yang dibahas dalam modul adalah:

- Bully Algorithm: Algoritma pemilihan koordinator berdasarkan prioritas atau identitas node.
- Ring Algorithm: Algoritma pemilihan koordinator dengan meneruskan pesan melalui node-node dalam suatu ring.
- Raft dan Paxos: Algoritma berbasis konsensus yang digunakan untuk mencapai kesepakatan antar-node.

Contoh penerapannya adalah Apache ZooKeeper yang menggunakan Zab (ZooKeeper Atomic Broadcast), serta Kubernetes yang menggunakan Raft melalui etcd.

## 9. Kesimpulan

Sinkronisasi dan koordinasi merupakan bagian penting dalam sistem terdistribusi untuk menjaga konsistensi data, mengatur proses yang berjalan secara bersamaan, serta mengelola penggunaan sumber daya. Sinkronisasi waktu fisik menggunakan standar dan protokol seperti UTC, NTP, dan PTP, sedangkan sinkronisasi waktu logis menggunakan algoritma seperti Lamport Logical Clock dan Vector Clocks untuk menentukan urutan kejadian. Selain itu, Mutual Exclusion diperlukan untuk mencegah konflik akses terhadap sumber daya bersama, sedangkan pemilihan koordinator membantu mengatur kerja antar-node. Penerapan mekanisme tersebut memungkinkan sistem terdistribusi berjalan lebih konsisten, terkoordinasi, dan andal.
