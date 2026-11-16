## Materi Minggu 1 : Pengenalan Sistem Terdistribusi dan Terdesentralisasi

**AI yang digunakan:** ChatGPT (GPT-6)

**Prompt:** Buatkan rangkuman materi dari modul PDF yang diberikan dengan bahasa Indonesia formal, jelas, ringkas, dan terstruktur. Pertahankan istilah, konsep, contoh, serta urutan pembahasan sesuai modul. Susun dalam format Markdown untuk README.md GitHub.

**Bagian yang disesuaikan dari keluaran prompt ada pada:** Penyusunan struktur pembahasan, pemilihan kalimat, dan format Markdown agar sesuai dengan template tugas. Istilah dan materi utama tetap mengacu pada modul.

## 1. Arti Penting Sistem Terdistribusi dan Terdesentralisasi

Sistem terdistribusi dan terdesentralisasi penting karena pertumbuhan jumlah data dan pengguna semakin besar. Layanan modern membutuhkan sistem yang memiliki skalabilitas, fault tolerance, performa tinggi, dan ketersediaan layanan selama 24 jam sehari dan 7 hari seminggu. Teknologi seperti Google, Netflix, dan Blockchain merupakan contoh penerapan konsep tersebut.

- Skalabilitas adalah kemampuan sistem untuk berkembang dan menangani peningkatan beban kerja, pengguna, atau permintaan tanpa menurunkan kinerja dan kualitas.
- Fault tolerance adalah kemampuan sistem untuk tetap beroperasi meskipun sebagian komponen perangkat keras atau perangkat lunak mengalami kegagalan.

## 2. Pengertian Sistem Terdistribusi

Sistem terdistribusi merupakan kumpulan komputer independen yang saling berkomunikasi melalui jaringan dan terlihat oleh pengguna sebagai satu kesatuan sistem yang utuh. Setiap komponen dapat bekerja secara mandiri, tetapi tetap saling berkoordinasi untuk menjalankan layanan.

Karakteristik utamanya meliputi komponen independen, komunikasi melalui jaringan, serta transparansi lokasi, akses, replikasi, dan kegagalan.

## 3. Arsitektur Sistem Dasar

Terdapat tiga arsitektur dasar sistem terdistribusi:

1. Client-Server: Komunikasi antara client yang mengirimkan permintaan dan server yang menyediakan layanan atau sumber daya.
2. Peer-to-Peer (P2P): Setiap komputer atau node dapat berperan sebagai penyedia sekaligus penerima layanan.
3. Hybrid: Menggabungkan pendekatan Client-Server dan Peer-to-Peer dalam satu sistem.

## 4. Karakteristik Sistem Terdistribusi

Karakteristik sistem terdistribusi meliputi:

- Transparansi lokasi: Pengguna tidak perlu mengetahui lokasi fisik sumber daya yang digunakan.
- Skalabilitas: Sistem mampu menangani pertumbuhan pengguna dan beban kerja.
- Fault tolerance: Sistem tetap berjalan ketika sebagian komponennya mengalami kegagalan.
- Kinerja tinggi: Pembagian pekerjaan dapat membantu meningkatkan performa sistem.
- Heterogenitas: Sistem dapat terdiri dari perangkat keras, perangkat lunak, dan jaringan yang berbeda.

## 5. Pengertian Sistem Terdesentralisasi

Sistem terdesentralisasi merupakan sistem yang mendistribusikan kendali atau pengambilan keputusan ke beberapa pihak atau node, sehingga tidak bergantung pada satu titik kontrol utama. Keputusan dapat dilakukan secara kolektif melalui mekanisme konsensus.

Berbeda dengan sentralisasi yang memiliki satu titik kontrol, desentralisasi membagi kendali sehingga mengurangi ketergantungan pada satu titik yang dapat menjadi sumber kegagalan. Contohnya adalah Blockchain, DNS, dan BitTorrent.

## 6. Perbedaan Sistem Terdistribusi dan Terdesentralisasi

Sistem terdistribusi berfokus pada pembagian beban kerja dan sumber daya ke beberapa komputer atau node. Sementara itu, sistem terdesentralisasi berfokus pada pembagian kendali dan pengambilan keputusan.

Contoh sistem terdistribusi adalah Google File System dan MinIO Object Storage. Contoh sistem terdesentralisasi adalah Blockchain. Kedua konsep ini saling berkaitan, tetapi memiliki fokus yang berbeda.

## 7. Studi Kasus Sistem Terdistribusi

Beberapa penerapan sistem terdistribusi dalam kehidupan sehari-hari dan teknologi antara lain:

- Google File System dan HDFS untuk penyimpanan data berukuran besar.
- Apache Kafka dan Apache Pulsar untuk messaging dan streaming data.
- Netflix dan Twitch untuk layanan distribusi konten.
- YouTube untuk penyediaan layanan video.
- Instagram, Threads, Facebook, dan TikTok untuk layanan media sosial.

## 8. Studi Kasus Sistem Terdesentralisasi

Contoh penerapan sistem terdesentralisasi meliputi:

- Blockchain, seperti Bitcoin, Ethereum, Algorand, Sui, Near, dan Aptos.
- DNS (Domain Name System), yaitu sistem yang membantu proses penerjemahan nama domain.
- BitTorrent, yaitu teknologi berbagi file dengan pendekatan peer-to-peer.

## 9. CAP Theorem

CAP Theorem atau Brewer's Theorem diperkenalkan oleh Eric Brewer pada tahun 2000. Teorema ini menjelaskan tiga aspek penting dalam sistem penyimpanan data terdistribusi:

1. Consistency: Setiap operasi pembacaan menghasilkan data terbaru atau memberikan pesan kesalahan.
2. Availability: Setiap permintaan pada node yang tidak mengalami kegagalan akan memperoleh respons, meskipun data yang diberikan belum tentu terbaru.
3. Partition Tolerance: Sistem tetap dapat beroperasi meskipun komunikasi antar-node terputus atau mengalami gangguan jaringan.

Ketika terjadi network partition, sistem harus menentukan prioritas antara Availability dan Consistency dengan tetap mempertahankan Partition Tolerance.

- AP (Availability + Partition Tolerance): Sistem tetap melayani permintaan, tetapi terdapat risiko data belum sinkron atau konsisten. Contoh dalam modul: MongoDB.
- CP (Consistency + Partition Tolerance): Sistem mempertahankan konsistensi data dengan menolak sebagian permintaan baca maupun tulis ketika diperlukan, sehingga availability dikorbankan. Contoh dalam modul: Apache Cassandra.

## 10. Konsistensi Data

Konsistensi data menjelaskan kesesuaian data yang tersedia ketika diakses oleh pengguna atau komponen sistem. Terdapat dua jenis konsistensi yang dibahas:

- Strong Consistency: Hasil pembacaan selalu menunjukkan data yang sama dan terbaru sesuai operasi penulisan.
- Eventual Consistency: Data tidak harus langsung sama pada seluruh node, tetapi akan menjadi konsisten setelah beberapa waktu.

Contohnya, sistem perbankan membutuhkan strong consistency untuk menjaga ketepatan transaksi, sedangkan media sosial dapat menggunakan eventual consistency.

## 11. Tantangan Sistem Terdistribusi dan Terdesentralisasi

Beberapa tantangan dalam penerapan kedua sistem tersebut adalah:

- Latency: Waktu yang diperlukan untuk memproses suatu permintaan.
- Throughput: Jumlah permintaan atau pekerjaan yang dapat diproses dalam periode tertentu.
- Keamanan: Ancaman seperti DDoS dan Sybil Attack.
- Kompleksitas manajemen node: Pengelolaan banyak node yang saling terhubung membutuhkan koordinasi.
- Governance: Pengaturan tata kelola dan pengambilan keputusan dalam sistem terdesentralisasi.

Sybil Attack merupakan serangan siber dengan membuat banyak identitas palsu untuk memengaruhi atau mendominasi suatu jaringan. Serangan ini dapat mengganggu integritas sistem, khususnya pada jaringan peer-to-peer dan blockchain.

## 12. Tren Masa Depan

Beberapa tren perkembangan sistem terdistribusi dan terdesentralisasi meliputi:

- Cloud-native: Pengembangan dan pengelolaan aplikasi menggunakan teknologi seperti Kubernetes dan Docker.
- Edge dan Fog Computing: Pemrosesan data yang dilakukan lebih dekat dengan sumber data.
- Web3 dan DeFi: Pengembangan teknologi internet dan layanan keuangan berbasis desentralisasi.
- Federated Data-Learning: Pendekatan pembelajaran AI terdistribusi.

## 13. Kesimpulan

Sistem terdistribusi merupakan sistem yang membagi beban kerja dan sumber daya ke beberapa komputer atau node agar dapat bekerja sebagai satu kesatuan. Sementara itu, sistem terdesentralisasi membagi kendali dan pengambilan keputusan agar tidak bergantung pada satu titik kontrol. Keduanya memiliki karakteristik dan fokus yang berbeda, tetapi saling berkaitan serta menjadi fondasi berbagai teknologi modern. Dalam penerapannya, kedua sistem menghadapi tantangan seperti konsistensi data, keamanan, latency, throughput, dan pengelolaan node. Perkembangan cloud-native, edge computing, Web3, dan AI terdistribusi menjadi bagian dari tren masa depannya.





