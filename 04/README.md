## Materi Minggu 4: Konsistensi dan Replikasi pada Sistem Terdistribusi

**Prompt:** Buatkan rangkuman materi berdasarkan modul 4 berjudul Konsistensi dan Replikasi pada Sistem Terdistribusi. Rangkum seluruh materi sesuai urutan pembahasan dalam modul, gunakan bahasa Indonesia yang formal, jelas, dan mudah dipahami. Pertahankan istilah teknis, konsep, contoh, serta penjelasan penting yang terdapat dalam modul. Susun hasilnya menggunakan format Markdown agar dapat dimasukkan ke dalam file README.md di GitHub.

**AI yang digunakan:** ChatGPT (GPT-6)

**Bagian yang disesuaikan dari keluaran prompt ada pada:** Penyusunan struktur materi agar lebih teratur dan mudah dibaca, penyederhanaan beberapa kalimat tanpa mengubah inti pembahasan dan penggunaan format Markdown berupa judul, subjudul, dan poin-poin.

## 1. Pengertian Konsistensi pada Sistem Terdistribusi

Konsistensi merupakan kondisi ketika seluruh node atau server dalam sistem terdistribusi memiliki data yang sama atau menampilkan data yang sama pada waktu tertentu. Hal ini penting karena data disimpan di beberapa lokasi dan dapat mengalami perubahan secara bersamaan oleh pengguna atau proses yang berbeda.

Contohnya, ketika data diperbarui pada satu server, sistem perlu memastikan bahwa server lain juga menerima perubahan tersebut agar seluruh salinan data tetap sesuai.

## 2. Pentingnya Konsistensi pada Sistem Terdistribusi

Konsistensi diperlukan agar pengguna mendapatkan informasi yang benar dan terbaru. Tanpa konsistensi, pengguna dapat melihat versi data yang berbeda tergantung server yang digunakan.

Contohnya adalah transaksi perbankan. Ketika nasabah mentransfer uang dari rekening A ke rekening B, saldo rekening A mungkin sudah berkurang, tetapi saldo rekening B belum bertambah karena pembaruan belum diterima server lain. Kondisi tersebut dapat menyebabkan ketidaksesuaian data dan mengganggu transaksi.

Oleh karena itu, konsistensi bertujuan menjaga kesamaan data antarnode, meskipun terdapat banyak server dan kemungkinan perubahan data secara bersamaan.

## 3. Teorema CAP

Teorema CAP menjelaskan tiga karakteristik penting dalam sistem terdistribusi, yaitu:

1. **Consistency:** seluruh node memiliki data yang konsisten atau sama.
2. **Availability:** sistem tetap menyediakan data ketika pengguna membutuhkannya.
3. **Partition Tolerance:** sistem tetap dapat berjalan meskipun terdapat gangguan atau pemutusan koneksi jaringan antarbagian sistem.

Dalam kondisi jaringan mengalami partition, sistem harus menentukan prioritas antara konsistensi dan ketersediaan.

Contoh pada aplikasi e-commerce:
- **AP (Availability dan Partition Tolerance):** pengguna tetap dapat berbelanja meskipun jaringan antarwilayah terputus, tetapi informasi stok mungkin belum sinkron.
- **CP (Consistency dan Partition Tolerance):** sistem menolak transaksi sementara sampai jaringan kembali normal agar data stok tetap konsisten.

## 4. Model Konsistensi

Model konsistensi merupakan aturan atau jaminan mengenai bagaimana dan kapan perubahan data dapat dilihat oleh node atau klien lain. Setiap model memiliki tingkat jaminan yang berbeda terhadap keseragaman data.

### 4.1 Strong Consistency

Setelah data diperbarui, seluruh node langsung melihat versi terbaru. Setiap proses pembacaan setelah penulisan akan memperoleh nilai yang sama.

Model ini biasanya menggunakan protokol seperti Two-Phase Commit atau Paxos.

**Contoh:** sistem perbankan yang harus memastikan seluruh server mengetahui perubahan saldo rekening.

### 4.2 Eventual Consistency

Model ini tidak mengharuskan seluruh node memiliki data yang sama secara langsung. Namun, seluruh salinan data akan menjadi konsisten apabila tidak ada pembaruan baru dalam jangka waktu tertentu.

Model ini cocok untuk sistem yang mengutamakan ketersediaan dan kecepatan.

**Contoh:** Amazon DynamoDB dan Apache Cassandra.

Eventual Consistency berkaitan dengan konsep **BASE**, yaitu:
- **Basically Available:** data tetap dapat dibaca atau ditulis meskipun sebagian sistem mengalami gangguan.
- **Soft State:** keadaan replika dapat berubah seiring waktu dan belum tentu selalu konsisten.
- **Eventual Consistency:** seluruh node pada akhirnya memiliki data yang konsisten jika tidak ada pembaruan baru.

### 4.3 Causal Consistency

Causal Consistency memastikan urutan operasi yang memiliki hubungan sebab-akibat tetap dipertahankan. Sementara itu, operasi yang tidak saling berhubungan dapat terlihat dalam urutan berbeda pada node lain.

**Contoh:** pada media sosial, komentar atau reaksi terhadap suatu postingan tidak boleh muncul sebelum postingan tersebut.

### 4.4 Read-Your-Writes Consistency

Model ini memastikan bahwa setelah pengguna menulis atau memperbarui data, pembacaan berikutnya oleh pengguna tersebut akan menampilkan hasil tulisannya.

Namun, model ini tidak menjamin pengguna lain langsung melihat perubahan yang sama.

**Contoh:** pesan yang dikirim melalui aplikasi messaging langsung muncul di layar pengirim meskipun penerima belum melihatnya.

### 4.5 Monotonic Read Consistency

Model ini memastikan pengguna tidak melihat versi data yang lebih lama daripada versi yang sebelumnya sudah pernah dibaca.

**Contoh:** timeline media sosial tidak kembali menampilkan versi lama setelah halaman diperbarui.

### 4.6 Sequential Consistency

Sequential Consistency memastikan seluruh operasi pada sistem terlihat dijalankan dalam urutan yang sama oleh semua node, meskipun urutan tersebut tidak harus sesuai dengan waktu nyata.

**Contoh:** seluruh pengguna media sosial melihat urutan postingan yang sama meskipun terdapat sedikit keterlambatan.

### 4.7 Linearizability

Linearizability merupakan varian paling kuat dari Strong Consistency. Operasi terlihat seolah-olah dilakukan secara atomik dan langsung, dengan urutan yang sama bagi seluruh node.

Setelah suatu penulisan selesai, pembacaan berikutnya oleh klien mana pun harus mencerminkan hasil penulisan tersebut atau penulisan yang lebih baru.

Contoh penerapannya terdapat pada etcd, ZooKeeper, dan Spanner. Salah satu penggunaannya adalah memastikan dua pengguna tidak dapat mendaftarkan username atau ID yang sama secara bersamaan.

## 5. Trade-off Latensi dengan Konsistensi

Dalam sistem terdistribusi terdapat kompromi antara tingkat konsistensi dan latensi atau waktu respons.

- **Konsistensi tinggi:** sistem menunggu proses sinkronisasi ant server selesai sebelum memberikan respons. Data lebih terjamin konsisten, tetapi latensi cenderung lebih tinggi.
- **Konsistensi lebih lemah:** sistem dapat memberikan respons tanpa menunggu seluruh replika selesai melakukan sinkronisasi. Latensi lebih rendah, tetapi data mungkin belum sama di semua server.

Contohnya adalah dua pusat data di Jakarta dan Yogyakarta. Pada Strong Consistency, sistem menunggu kedua pusat data memiliki data yang sama sebelum memberikan respons. Pada Eventual Consistency, sistem dapat langsung memberikan respons sementara pembaruan dikirim ke pusat data lainnya.

## 6. Pengertian Replikasi Data

Replikasi data merupakan proses membuat dan memelihara salinan data yang sama pada beberapa node atau server dalam sistem terdistribusi.

Tujuan replikasi adalah menjaga sistem tetap tersedia, andal, dan cepat meskipun salah satu node mengalami kegagalan.

Contohnya, sebuah database utama berada di Jakarta, kemudian dibuat salinan database di Yogyakarta dan Denpasar untuk meningkatkan ketersediaan data.

Tujuan replikasi data meliputi:
1. **Availability:** server lain tetap memiliki salinan data apabila salah satu server gagal.
2. **Performance:** pengguna dapat membaca data dari server yang lebih dekat.
3. **Reliability:** mengurangi risiko kehilangan data karena terdapat salinan di beberapa lokasi.
4. **Scalability:** membagi beban pembacaan data ke beberapa server.

## 7. Jenis Replikasi

### 7.1 Master–Slave (Primary–Secondary)

Satu server bertindak sebagai master yang menangani penulisan data, sedangkan server slave digunakan untuk membaca data.

Kelebihannya adalah pengelolaan konsistensi lebih sederhana, tetapi server master dapat menjadi bottleneck.

**Contoh:** PostgreSQL Streaming Replication.

### 7.2 Multi-Master (Peer-to-Peer)

Seluruh node dapat melakukan operasi baca dan tulis. Model ini lebih fleksibel, tetapi memiliki risiko konflik ketika beberapa node memperbarui data yang sama.

**Contoh:** PostgreSQL Logical Replication, Apache Cassandra, MongoDB, dan Apache Ignite.

### 7.3 Synchronous Replication

Pembaruan data dikirim dan dikonfirmasi oleh node replika sebelum operasi dianggap selesai. Model ini memberikan konsistensi lebih tinggi, tetapi dapat memperlambat proses.

**Contoh:** Google Spanner.

### 7.4 Asynchronous Replication

Pembaruan data dikirim ke node lain setelah transaksi selesai pada server utama. Model ini lebih cepat, tetapi dapat menyebabkan keterlambatan pembaruan data pada replika.

**Contoh:** MySQL Async Mode dan DynamoDB.

## 8. Strategi Sinkronisasi Replika

Strategi sinkronisasi replika dapat dikelompokkan berdasarkan beberapa aspek berikut.

### 8.1 Berdasarkan Waktu Sinkronisasi

- **Asynchronous:** server sumber melakukan commit tanpa menunggu replika. Performanya cepat, tetapi risiko kehilangan data lebih tinggi.
- **Semi-synchronous:** server sumber menunggu setidaknya satu replika menerima data. Strategi ini memberikan keseimbangan antara konsistensi dan performa. Modul menyebut MySQL sebagai salah satu pengguna strategi ini.
- **Synchronous:** server sumber menunggu seluruh replika melakukan commit. Konsistensinya tinggi, tetapi performanya lebih rendah.

### 8.2 Berdasarkan Arah Replikasi

- **Master-Slave:** satu node melakukan baca dan tulis, sedangkan node lain hanya membaca.
- **Master-Master:** seluruh node memiliki peran dan kemampuan yang setara untuk membaca serta menulis.
- **Master-Master Asymmetric:** seluruh node dapat melakukan baca dan tulis, tetapi memiliki peran atau sumber daya yang berbeda.

### 8.3 Berdasarkan Cara Sinkronisasi

- **Pull-based:** replika memeriksa pembaruan secara berkala pada server sumber. Jika terdapat perubahan, replika mengambil pembaruan tersebut.
- **Push-based:** server sumber secara aktif mengirimkan pembaruan ketika terjadi perubahan. Pengiriman dapat menggunakan Change Data Capture (CDC), WebSockets, atau Server-Sent Events (SSE).
- **Hybrid:** menggabungkan pendekatan pull-based dan push-based.

### 8.4 Berdasarkan Penanganan Konflik

Beberapa pendekatan untuk menangani konflik pembaruan data adalah:

- **LWW (Last Write Wins):** pembaruan dengan timestamp terbaru yang dipertahankan, sedangkan pembaruan lainnya diabaikan.
- **Vector Clock:** menggunakan vector clock untuk membantu menentukan urutan dan hubungan antarperubahan.
- **CRDT (Conflict-free Replicated Data Types):** menggunakan struktur data yang dirancang agar perubahan pada beberapa node dapat digabungkan tanpa menimbulkan konflik.
- **OT (Operational Transformation):** melakukan transformasi operasi berdasarkan informasi perubahan lokal agar hasil akhir tetap sama.

## 9. Contoh CRDT dan OT

### 9.1 CRDT

CRDT digunakan untuk menggabungkan perubahan data dari beberapa node tanpa membutuhkan satu server pusat sebagai pengendali seluruh perubahan.

Contoh dalam modul adalah dua pengguna yang menghitung jumlah akses website secara terpisah. Pengguna pertama mencatat 5 pengunjung, sedangkan pengguna kedua mencatat 3 pengunjung.

Ketika kedua data disinkronkan menggunakan aturan Max, nilai masing-masing pengguna dipertahankan sehingga hasil akhirnya adalah 5 dan 3. Total pengunjung menjadi 8.

Salah satu contoh teknologi yang disebutkan dalam modul adalah Yjs, yang digunakan antara lain untuk editor kolaboratif seperti Google Docs.

### 9.2 Operational Transformation (OT)

OT digunakan untuk menyelesaikan konflik ketika beberapa pengguna mengedit dokumen secara bersamaan.

Contohnya, dua pengguna mengedit teks `abc`:
- Pengguna pertama menyisipkan huruf `x` di awal sehingga menjadi `xabc`.
- Pengguna kedua menghapus karakter `c` sehingga menjadi `ab`.

Jika kedua perubahan diterapkan tanpa penyesuaian posisi, hasil dokumen dapat berbeda. OT mengubah posisi operasi berdasarkan perubahan yang sudah terjadi agar kedua pengguna memperoleh hasil yang sama, yaitu `xab`.

## 10. Protokol Replikasi

Beberapa protokol yang digunakan dalam replikasi data pada sistem terdistribusi adalah:

1. **Primary-based (Master-Slave):** satu node bertugas menangani penulisan dan pembacaan data, sedangkan node lainnya digunakan untuk membaca.
2. **Quorum-based:** operasi baca dan tulis dinyatakan berhasil setelah memperoleh konfirmasi dari sejumlah node tertentu.
3. **State Machine Replication:** beberapa replika menjalankan perintah yang sama dengan urutan yang sama agar menghasilkan keadaan data yang konsisten.
4. **Gossip Protocol:** node menyebarkan informasi atau pembaruan kepada node lain secara bertahap melalui pemilihan peer.
5. **Chain Replication:** merupakan salah satu protokol replikasi yang dibahas dalam modul.

### 10.1 Quorum-based

Quorum-based merupakan mekanisme replikasi yang menentukan keberhasilan operasi baca dan tulis berdasarkan jumlah konfirmasi dari node.

Ketentuannya adalah:

**W + R > N**

Keterangan:
- **W:** jumlah minimal node yang harus mengonfirmasi operasi write.
- **R:** jumlah minimal node yang harus memberikan respons operasi read.
- **N:** jumlah keseluruhan node.

Contohnya, sistem memiliki 3 node dengan konfigurasi N = 3, W = 2, dan R = 2. Karena 2 + 2 lebih besar dari 3, persyaratan quorum terpenuhi.

Pada operasi write, jika dua node sudah berhasil menyimpan data dan memberikan konfirmasi, operasi dapat dinyatakan berhasil meskipun node ketiga belum selesai.

Pada operasi read, sistem meminta data dari minimal dua node. Dengan konfigurasi tersebut, terdapat irisan antara node yang mengonfirmasi penulisan dan node yang memberikan hasil pembacaan sehingga data terbaru dapat diperoleh.

### 10.2 State Machine Replication

State Machine Replication bertujuan menjaga ketersediaan sistem dengan menjalankan perintah yang sama dalam urutan yang sama pada beberapa server replika.

Server utama atau leader menerima permintaan klien, mencatat perintah ke dalam log, menentukan urutannya, kemudian mengirimkannya ke replika lain.

Contohnya, replika A, B, dan C awalnya memiliki nilai `x = 10`. Klien mengirim perintah `SET x = 20` kepada leader A. Perintah tersebut dicatat dan dikirim ke B serta C. Setelah memperoleh konfirmasi bahwa perintah telah masuk ke log replika, perintah dikomit dan dijalankan oleh seluruh replika. Akhirnya, ketiganya memiliki nilai `x = 20`.

### 10.3 Gossip Protocol

Gossip Protocol digunakan untuk menyebarkan informasi mengenai keadaan node dan pembaruan data dalam sistem terdistribusi.

Contohnya pada Apache Cassandra:
1. Node A mendeteksi perubahan data atau mengetahui bahwa node lain mengalami gangguan.
2. Node A memilih satu hingga tiga peer secara acak dan membagikan status terbarunya.
3. Node penerima memperbarui statusnya, kemudian menyebarkan informasi tersebut kepada node lain.
4. Proses berlangsung berulang sehingga informasi dapat diketahui oleh seluruh node dalam cluster.

## 11. Studi Kasus

Modul membahas dua studi kasus penerapan replikasi data:

1. **PostgreSQL 18 Streaming Replication:** membahas penerapan replikasi streaming pada PostgreSQL.
2. **Apache Ignite 3 Master-Master:** membahas penerapan strategi replikasi master-master pada Apache Ignite.

Pembahasan lebih lanjut mengenai kedua studi kasus tersebut merujuk pada dokumen *lecture notes* dan source code yang menyertai materi modul.

## 12. Kesimpulan

Konsistensi dan replikasi merupakan konsep penting dalam sistem terdistribusi. Konsistensi memastikan data pada berbagai node tetap sesuai, sedangkan replikasi menyediakan salinan data pada beberapa server untuk meningkatkan ketersediaan, kinerja, keandalan, dan skalabilitas.

Terdapat berbagai model konsistensi, seperti Strong Consistency, Eventual Consistency, Causal Consistency, Read-Your-Writes, Monotonic Read, Sequential Consistency, dan Linearizability. Setiap model memiliki tingkat jaminan yang berbeda dan dapat memengaruhi latensi sistem.

Replikasi data dapat diterapkan melalui berbagai jenis, strategi sinkronisasi, dan protokol, seperti Master-Slave, Multi-Master, Quorum-based, State Machine Replication, dan Gossip Protocol. Pemilihan pendekatan perlu disesuaikan dengan kebutuhan sistem, terutama dalam menjaga keseimbangan antara konsistensi, ketersediaan, dan performa.
