## Materi Minggu 5: Fault Tolerance

**Prompt:** Buatkan rangkuman materi berdasarkan modul 5 berjudul Fault Tolerance. Rangkum seluruh materi sesuai urutan pembahasan dalam modul, gunakan bahasa Indonesia yang formal, jelas, dan mudah dipahami. Pertahankan istilah teknis, konsep, contoh, serta penjelasan penting yang terdapat dalam modul. Susun hasilnya menggunakan format Markdown agar dapat dimasukkan ke dalam file README.md di GitHub.

**AI yang digunakan:** ChatGPT (GPT-6)

**Bagian yang disesuaikan dari keluaran prompt ada pada:** Penyusunan struktur materi agar lebih teratur dan mudah dibaca, penyederhanaan beberapa kalimat tanpa mengubah inti pembahasan, dan penggunaan format Markdown berupa judul, subjudul, dan poin-poin.

## 1. Pengertian Fault Tolerance

Fault Tolerance merupakan kemampuan suatu sistem untuk mempertahankan operasionalnya dengan baik meskipun terjadi kegagalan atau kesalahan pada satu atau lebih komponennya.

Kemampuan ini sangat penting bagi sistem yang membutuhkan:
- **High Availability:** sistem harus tetap tersedia dan dapat digunakan.
- **Mission Critical:** sistem yang kegagalannya dapat mengganggu kegiatan penting.
- **Life-Critical System:** sistem yang berkaitan dengan keselamatan manusia.

## 2. Arti Penting Fault Tolerance pada Sistem Terdistribusi dan Terdesentralisasi

Sistem terdistribusi dan terdesentralisasi memiliki banyak komponen yang saling terhubung. Koneksi antar komponen tersebut dapat mengalami gangguan sehingga berpotensi menyebabkan kegagalan sistem.

Semakin penting suatu aplikasi, semakin tinggi tuntutan agar sistem tetap berfungsi dengan baik. Oleh karena itu, diperlukan Fault Tolerance untuk mengantisipasi kegagalan dan menjaga ketersediaan layanan.

## 3. Jenis Fault

Terdapat beberapa jenis fault atau kegagalan dalam sistem, yaitu:

1. **Transient Fault:** kegagalan yang bersifat sementara, misalnya gangguan akibat petir.
2. **Intermittent Fault:** kegagalan yang muncul dan menghilang secara berulang, misalnya akibat hardware yang mengalami overheat.
3. **Permanent Fault:** kegagalan yang bersifat tetap dan tidak hilang dengan sendirinya.
4. **Byzantine Fault:** kondisi ketika suatu komponen memberikan hasil yang acak atau tidak konsisten sehingga komponen lain sulit menentukan informasi yang benar.

## 4. Klasifikasi Fault Berdasarkan Sumber

Berdasarkan sumber penyebabnya, fault dibagi menjadi tiga kategori:

### 4.1 Hardware Faults

Kegagalan yang berasal dari perangkat keras, seperti:
- Disk crash.
- Power failure.

### 4.2 Software Faults

Kegagalan yang disebabkan oleh perangkat lunak, seperti:
- Bugs atau kesalahan pada program.
- Memory leak.
- Race condition.

### 4.3 Communication Faults

Kegagalan yang terjadi pada proses komunikasi antar komponen, seperti:
- Packet loss.
- Network partition atau terputusnya koneksi jaringan antarbagian sistem.

## 5. Teknik untuk Mencapai Fault Tolerance

Terdapat beberapa teknik yang dapat digunakan untuk meningkatkan kemampuan sistem dalam menghadapi kegagalan.

### 5.1 Redundansi dan Replikasi

Redundansi merupakan penyediaan sumber daya atau komponen lebih dari satu. Dalam sistem terdistribusi, sumber daya dapat direplikasi ke beberapa node.

Tujuannya adalah menghindari **Single Point of Failure**, yaitu kondisi ketika kegagalan satu komponen menyebabkan seluruh sistem tidak dapat beroperasi.

Dengan adanya beberapa salinan atau komponen cadangan, sistem masih dapat berjalan ketika salah satu node mengalami kegagalan.

### 5.2 Load Balancing

Load Balancing merupakan proses membagi beban kerja aplikasi ke beberapa instance. Satu instance dalam konteks ini merupakan satu proses aplikasi penuh yang sedang aktif.

Pembagian beban dilakukan menggunakan load balancer yang mengarahkan permintaan pengguna ke beberapa instance aplikasi.

Contoh perangkat lunak yang digunakan:
- HAProxy.
- Nginx.

Teknik ini membantu proses scaling aplikasi dan menghindari penumpukan beban pada satu instance.

### 5.3 Checkpointing dan Rollback Recovery

Kedua teknik ini digunakan untuk membantu sistem pulih setelah terjadi kegagalan.

- **Checkpointing:** proses menyimpan status sistem secara berkala ke media penyimpanan.
- **Rollback Recovery:** proses mengembalikan sistem ke checkpoint yang telah tersimpan sebelumnya setelah terjadi kegagalan.

Dengan teknik tersebut, sistem dapat melanjutkan proses dari status terakhir yang tersimpan, bukan harus memulai seluruh proses dari awal. Hal ini membantu mengurangi kehilangan data dan waktu pemrosesan.

### 5.4 Heartbeat dan Failure Detection

**Heartbeat** merupakan sinyal periodik yang dikirim antar komponen untuk menunjukkan bahwa suatu komponen masih aktif.

Sementara itu, **Failure Detection** merupakan proses mendeteksi kemungkinan kegagalan berdasarkan sinyal heartbeat.

Jika komponen pemantau tidak menerima heartbeat dari komponen lain dalam jangka waktu tertentu, komponen tersebut dapat diasumsikan mengalami kegagalan atau tidak memberikan respons.

Pola ini penting karena memungkinkan sistem mendeteksi dan menangani kegagalan secara tepat waktu.

Modul menyertakan contoh script `check-server.py` untuk melakukan pengecekan komponen sederhana. Untuk kebutuhan diagnostik yang lebih lanjut, diperlukan program yang lebih kompleks.

### 5.5 Retry dengan Library Tenacity

Library **Tenacity** dapat digunakan untuk mengelola proses yang bergantung pada komponen di luar aplikasi.

Hal ini diperlukan karena komunikasi atau koneksi dengan komponen eksternal selalu memiliki kemungkinan mengalami kegagalan.

Dengan mekanisme retry, aplikasi dapat mencoba kembali operasi yang gagal sesuai aturan yang ditentukan.

Modul menyertakan contoh implementasi melalui file `check-retry.py`.

### 5.6 Circuit Breaker

Circuit Breaker merupakan pola desain yang digunakan dalam microservices untuk mencegah kegagalan berantai (*cascading failure*).

Pola ini bekerja dengan memblokir sementara permintaan menuju layanan yang sedang mengalami kegagalan. Circuit Breaker memiliki tiga status:

1. **Closed:** permintaan diizinkan dan kegagalan dipantau. Jika jumlah kegagalan mencapai batas tertentu, status berubah menjadi Open.
2. **Open:** permintaan berikutnya ditolak sementara agar layanan memiliki waktu untuk pulih.
3. **Half-Open:** setelah waktu tertentu, sejumlah permintaan terbatas diizinkan untuk menguji apakah layanan telah pulih.

Jika permintaan pengujian berhasil, status kembali menjadi Closed. Jika gagal, status kembali menjadi Open.

## 6. Consensus dan Coordination

### 6.1 Consensus

Consensus merupakan proses ketika beberapa node menyepakati satu nilai, status, atau urutan operasi, meskipun terdapat kegagalan atau keterlambatan jaringan.

Consensus membantu memastikan bahwa node dalam sistem memiliki kesepakatan terhadap keputusan tertentu.

### 6.2 Coordination

Coordination merupakan praktik yang lebih luas dalam mengelola interaksi antar node agar seluruh komponen dapat bekerja sama secara efektif dan konsisten.

Coordination sering melibatkan Consensus sebagai salah satu komponen penting untuk mencapai kesepakatan antar node.

### 6.3 Contoh Penerapan Consensus dan Coordination

Beberapa contoh penerapannya adalah:

- **Database Leader Election:** dalam cluster database yang menggunakan replikasi, diperlukan pemilihan leader untuk menangani operasi write. Algoritma consensus seperti Raft dapat digunakan.
- **Cloud Storage File Updates:** ketika file diperbarui pada layanan seperti Google Drive, sistem menggunakan consensus untuk memastikan perubahan disetujui dan dikomit oleh mayoritas server. Setelah mayoritas menyetujui, pembaruan dianggap final dan kemudian direplikasi ke seluruh server.
- **Cryptocurrency dan Blockchain:** teknologi blockchain menggunakan mekanisme consensus untuk memvalidasi dan menyepakati transaksi.

## 7. Actor Model untuk Supervisi Proses

Actor Model merupakan model pemrograman yang menggunakan actor sebagai unit dasar untuk menjalankan proses dan berkomunikasi dalam sistem.

Dalam konteks Fault Tolerance, Actor Model dapat digunakan untuk mendukung supervisi proses. Mekanisme supervisi memungkinkan suatu komponen mengawasi komponen lain dan menangani kegagalan yang terjadi.

Salah satu pola yang berkaitan dengan pendekatan ini adalah **Supervisor-Worker**, yaitu supervisor bertugas mengawasi worker yang menjalankan pekerjaan. Jika worker mengalami kegagalan, supervisor dapat mengelola tindakan pemulihan sesuai mekanisme yang diterapkan.

## 8. Implementasi Fault Tolerance pada Berbagai Bahasa Pemrograman dan Peranti Pengembangan

Fault Tolerance dapat diterapkan menggunakan berbagai bahasa pemrograman dan library.

### 8.1 Erlang dan Elixir

Erlang dan Elixir memiliki mekanisme bawaan untuk mendukung Actor Model serta pola Supervisor-Worker.

### 8.2 Pony

Pony merupakan bahasa pemrograman yang secara khusus berfokus pada Actor Model.

Situs resmi: https://www.ponylang.io

### 8.3 Python

Python dapat menggunakan beberapa library pihak ketiga untuk mendukung Fault Tolerance, seperti:
- **Xoscar:** https://xoscar.dev
- **Tenacity:** untuk mengelola mekanisme percobaan ulang operasi.
- **Circuit Breaker:** untuk membantu mencegah kegagalan berantai.

### 8.4 Java

Java memiliki beberapa perangkat pengembangan yang dapat digunakan, seperti:
- **Apache Pekko:** mendukung Actor Model dan pola Supervisor-Worker.
- **Resilience4j:** library untuk mendukung penerapan Fault Tolerance.

Repositori Resilience4j: https://github.com/resilience4j/resilience4j

### 8.5 Bahasa Pemrograman Lain

Pengembang juga dapat mencari library Fault Tolerance sesuai bahasa pemrograman yang digunakan, misalnya:
- **npm:** untuk ekosistem JavaScript.
- **crates.io:** untuk ekosistem Rust.

## 9. Kesimpulan

Fault Tolerance merupakan kemampuan sistem untuk tetap beroperasi meskipun terdapat kegagalan pada sebagian komponennya. Konsep ini sangat penting dalam sistem terdistribusi dan terdesentralisasi karena sistem terdiri dari banyak komponen yang saling terhubung dan memiliki kemungkinan mengalami gangguan.

Fault dapat berasal dari perangkat keras, perangkat lunak, maupun komunikasi jaringan. Untuk mengatasinya, terdapat beberapa teknik seperti redundansi dan replikasi, load balancing, checkpointing, rollback recovery, heartbeat, failure detection, retry, serta circuit breaker.

Selain itu, Consensus dan Coordination membantu node mencapai kesepakatan dan bekerja sama secara konsisten. Actor Model juga dapat digunakan untuk mendukung supervisi proses. Berbagai bahasa pemrograman seperti Erlang, Elixir, Pony, Python, dan Java menyediakan mekanisme atau library yang dapat membantu penerapan Fault Tolerance.
