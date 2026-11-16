Materi Minggu 2: Proses dan Komunikasi Antar Proses pada Sistem Terdistribusi

Prompt: Buatkan rangkuman materi dari modul PDF yang diberikan menggunakan bahasa Indonesia formal, jelas, ringkas, dan terstruktur. Pertahankan istilah, konsep, contoh, serta urutan pembahasan sesuai modul. Susun dalam format Markdown untuk README.md GitHub.

AI yang digunakan: ChatGPT (GPT-6).

Bagian yang disesuaikan dari keluaran prompt ada pada: Penyusunan struktur pembahasan, pemilihan kalimat, dan format Markdown agar sesuai dengan template tugas. Materi utama dan istilah tetap mengacu pada modul.

# Materi Minggu 2: Proses dan Komunikasi Antar Proses pada Sistem Terdistribusi

## 1. Pengertian Proses

Proses merupakan program yang sedang dijalankan oleh sistem operasi. Dalam sistem terdistribusi, setiap komputer atau node dapat menjalankan proses secara independen. Agar seluruh proses dapat bekerja sebagai satu kesatuan sistem, diperlukan komunikasi dan koordinasi antarproses.

## 2. Manajemen Proses

Manajemen proses merupakan kegiatan untuk mengatur proses yang berjalan dalam sistem. Berdasarkan modul, terdapat tiga kegiatan utama:

- Process Creation: Proses pembuatan atau pembentukan proses baru.
- Process Migration: Proses pemindahan proses dari satu komputer atau node ke node lainnya.
- Process Monitoring: Proses pemantauan aktivitas dan kondisi proses yang sedang berjalan.

## 3. Sistem Terdistribusi dan Komunikasi

Sistem terdistribusi merupakan sekumpulan komputer atau node independen yang bekerja bersama melalui koordinasi sebagai satu kesatuan logis. Setiap node menjalankan proses masing-masing. Karena proses dapat berada pada komputer yang berbeda, komunikasi antar-node diperlukan agar seluruh bagian sistem dapat bekerja sama.

Contoh penerapannya adalah:

- Multiplayer Games: Komunikasi antarperangkat pemain untuk menjalankan permainan bersama.
- Gojek dan Grab: Komunikasi antara antarmuka pengguna dengan layanan driver, pelacakan lokasi, dan perhitungan biaya.
- WhatsApp: Komunikasi point-to-point untuk layanan chat dan video call melalui infrastruktur terdistribusi.

## 4. Model Komunikasi Pesan

Model komunikasi pesan dibagi menjadi beberapa jenis:

1. Komunikasi langsung: Proses saling berkomunikasi secara langsung menggunakan socket.
2. Komunikasi tidak langsung: Pesan dikirim melalui perantara seperti mailbox atau message queue.
3. Publish/Subscribe (Pub/Sub): Pengirim menerbitkan pesan ke suatu saluran, kemudian penerima yang berlangganan saluran tersebut akan menerima pesan.

## 5. Proses pada Sistem Terdistribusi

Dalam sistem terdistribusi, proses dapat berjalan pada node yang berbeda. Karena setiap node memiliki memori masing-masing, proses pada satu node tidak dapat langsung mengakses shared memory pada node lainnya. Oleh sebab itu, dibutuhkan mekanisme Inter-Process Communication (IPC) untuk memungkinkan proses saling bertukar informasi.

## 6. Inter-Process Communication (IPC)

IPC merupakan mekanisme komunikasi yang memungkinkan proses bertukar informasi dan berkoordinasi. Berdasarkan modul, terdapat empat jenis IPC:

- Shared Memory: Proses bertukar informasi melalui area memori yang digunakan bersama. Mekanisme ini tidak cocok untuk komunikasi antar-node dalam sistem terdistribusi karena tidak terdapat akses memori bersama secara langsung antar-node.
- Message Passing: Proses bertukar informasi dengan cara mengirim dan menerima pesan.
- Remote Procedure Call (RPC): Mekanisme yang memungkinkan suatu proses memanggil prosedur atau fungsi pada komputer lain melalui jaringan.
- Middleware: Perangkat lunak perantara yang membantu proses komunikasi dan pertukaran informasi antar-aplikasi.

## 7. Message Passing

Message Passing merupakan metode komunikasi antarproses dengan mengirimkan pesan dari satu proses ke proses lainnya. Mekanisme ini memungkinkan pertukaran data tanpa harus menggunakan memori bersama.

Salah satu standar yang digunakan adalah Message Passing Interface (MPI). MPI menyediakan standar komunikasi untuk aplikasi yang menjalankan proses secara paralel dan terdistribusi. Modul juga mencantumkan implementasi MPI menggunakan Python melalui pustaka mpi4py.

## 8. Remote Procedure Call (RPC)

Remote Procedure Call merupakan mekanisme komunikasi yang memungkinkan suatu program menjalankan prosedur pada komputer lain seolah-olah prosedur tersebut dipanggil secara lokal. RPC menyederhanakan komunikasi antarproses karena pengembang tidak harus mengatur seluruh proses pertukaran pesan secara manual.

Contoh teknologi yang dibahas dalam modul adalah gRPC.

## 9. Message-Oriented Middleware (MOM)

Message-Oriented Middleware merupakan infrastruktur yang memfasilitasi komunikasi dan pertukaran data antar-aplikasi melalui pesan. Dalam MOM, pesan dikirim dan diterima secara asinkron sehingga pengirim dan penerima tidak harus aktif pada waktu yang sama.

Beberapa standar dan protokol MOM yang disebutkan dalam modul adalah:

- XATMI: Spesifikasi untuk Distributed Transaction Processing.
- AMQP (Advanced Message Queuing Protocol): Umumnya digunakan untuk aplikasi enterprise.
- HLA (High Level Architecture): Standar untuk kebutuhan simulasi.
- MQTT (MQ Telemetry Transport): Umumnya digunakan pada perangkat dengan sumber daya terbatas.
- DDS (Data Distribution Service): Standar distribusi data dari OMG.
- XMPP (eXtensible Messaging and Presence Protocol): Protokol komunikasi berbasis pesan dan presence.

## 10. Studi Kasus: Microservices

Microservices merupakan pendekatan pengembangan aplikasi dengan membagi aplikasi menjadi layanan-layanan kecil yang dapat berjalan secara independen. Setiap layanan memiliki fungsi tertentu dan berkomunikasi dengan layanan lainnya melalui mekanisme komunikasi antarproses. Pendekatan ini berkaitan dengan konsep sistem terdistribusi karena layanan dapat berjalan pada node yang berbeda.

## 11. Komunikasi Sinkron dan Asinkron

Komunikasi antarproses dapat dibedakan menjadi dua jenis:

- Sinkron: Proses pengirim menunggu respons dari proses penerima sebelum melanjutkan pekerjaan berikutnya.
- Asinkron: Proses pengirim tidak harus menunggu respons langsung sehingga dapat melanjutkan pekerjaan lainnya setelah mengirim pesan.

Komunikasi sinkron cocok untuk proses yang membutuhkan respons langsung, sedangkan komunikasi asinkron memungkinkan proses berjalan lebih independen.

## 12. Masalah pada Komunikasi Antarproses

Beberapa masalah yang dapat terjadi dalam komunikasi antarproses meliputi:

- Reliability: Memastikan pesan terkirim secara lengkap dan benar meskipun terjadi kehilangan paket atau kegagalan sistem. Solusinya meliputi acknowledgement, transmisi ulang, dan penggunaan TCP.
- Ordering: Memastikan pesan diproses berdasarkan urutan yang logis. Mekanisme yang dapat digunakan antara lain FIFO pipes, message queues, shared memory, sockets, message passing, dan RPC.
- Security: Menjaga keamanan komunikasi melalui enkripsi dan autentikasi.
- Performance: Berkaitan dengan latency dan bandwidth dalam proses komunikasi.

## 13. Protokol Komunikasi

Protokol komunikasi merupakan aturan yang mengatur pertukaran data antarproses melalui jaringan. Modul membahas beberapa protokol berikut:

- TCP: Protokol komunikasi yang menyediakan pengiriman data secara andal dan berurutan.
- UDP: Protokol komunikasi yang tidak menyediakan jaminan pengiriman seperti TCP.
- HTTP: Protokol yang digunakan untuk komunikasi dalam layanan web.

Beberapa teknologi komunikasi yang berjalan di atas HTTP adalah gRPC, GraphQL, dan REST.

## 14. Konsep Sinkronisasi

Sinkronisasi merupakan proses menyelaraskan waktu atau aktivitas beberapa node agar dapat bekerja secara terkoordinasi. Dalam sistem terdistribusi, setiap node memiliki clock atau jam lokal sendiri. Perbedaan waktu dapat terjadi karena latency jaringan dan pergeseran jam perangkat keras.

Sinkronisasi diperlukan untuk memastikan urutan kejadian, konsistensi data, dan koordinasi sistem. Metode yang disebutkan dalam modul meliputi penggunaan atomic clock, GPS, TAI, UTC, Network Time Protocol (NTP), dan Precision Time Protocol (PTP). PTP memiliki tingkat presisi lebih tinggi dibandingkan NTP.

## 15. Logical Clock

Logical Clock merupakan mekanisme pencatatan urutan kejadian dalam sistem terdistribusi tanpa bergantung langsung pada waktu sebenarnya. Salah satu metode yang dibahas adalah Lamport Logical Clock.

Aturan Lamport Logical Clock:

1. Setiap terjadi suatu kejadian, nilai logical clock bertambah satu.
2. Ketika mengirim pesan, proses menyertakan nilai logical clock ke dalam pesan.
3. Ketika menerima pesan, proses membandingkan nilai clock lokal dengan nilai clock pada pesan, mengambil nilai terbesar, kemudian menambahkan satu.

Contoh pada modul menggunakan tiga layanan:

- Sales Service mencatat transaksi dan mengirim pesan dengan logical clock 1.
- Product Service menerima pesan, memperbarui clock menjadi 2, kemudian meneruskan permintaan.
- Invoice Service menerima pesan, memperbarui clock menjadi 3, kemudian menghasilkan faktur.

Dengan demikian, urutan kejadian dapat diketahui melalui nilai logical clock, yaitu Sales Service, Product Service, kemudian Invoice Service.

Modul juga menyebutkan pengembangan logical clock lainnya, yaitu Vector Clocks, Plausible Clocks, Chain Clocks, Interval Tree Clocks, dan Blum Clocks.

## 16. Koordinasi Proses

Koordinasi proses merupakan mekanisme yang memungkinkan beberapa proses independen pada komputer berbeda bekerja sama untuk mencapai tujuan bersama. Koordinasi mencakup komunikasi, sinkronisasi, dan pengaturan akses sumber daya agar tidak terjadi konflik seperti deadlock dan race condition.

Contoh teknologi yang disebutkan dalam modul adalah Apache ZooKeeper, etcd, Consul, ClickHouse Keeper, Oxia, dan KRaft.

## 17. Tantangan dan Solusi pada Proses Sistem Terdistribusi

Beberapa tantangan beserta solusi yang dibahas dalam modul adalah:

- Message Loss: Kehilangan pesan dapat ditangani menggunakan retransmission dan acknowledgement.
- Deadlock: Dapat ditangani menggunakan timeout dan algoritma deteksi.
- Data Inconsistency: Dapat diatasi menggunakan protokol konsensus seperti Raft dan Paxos.
- Security: Keamanan komunikasi dapat ditingkatkan menggunakan SSL/TLS dan OAuth2.

## 18. Current Issues

Beberapa perkembangan dan isu terkini dalam pengelolaan proses pada sistem terdistribusi meliputi:

- Edge dan Fog Computing: Pemrosesan data dilakukan lebih dekat dengan sumber data.
- Observability dan Tracing: Penggunaan telemetry untuk memantau aktivitas dan kinerja sistem.
- Container Orchestration: Pengelolaan dan pengaturan container menggunakan teknologi seperti Kubernetes dan Docker Swarm.

## 19. Kesimpulan

Proses dan komunikasi antarproses merupakan bagian penting dalam sistem terdistribusi. Setiap node menjalankan proses secara independen sehingga dibutuhkan IPC untuk memungkinkan pertukaran pesan dan koordinasi. Mekanisme seperti Message Passing, RPC, dan MOM membantu komunikasi antarproses, sedangkan sinkronisasi dan logical clock digunakan untuk menjaga urutan kejadian. Dalam penerapannya, sistem terdistribusi menghadapi tantangan seperti kehilangan pesan, deadlock, inkonsistensi data, keamanan, dan performa. Oleh karena itu, diperlukan protokol komunikasi, mekanisme koordinasi, serta teknologi pendukung agar sistem dapat berjalan secara andal.
