# Laporan Praktikum Jaringan Komputer

## Modul 2 - Pengenalan Tools

## Tujuan Praktikum

1. Memahami proses instalasi aplikasi **Wireshark** yang akan digunakan selama praktikum jaringan komputer.
2. Mempelajari cara menggunakan Wireshark untuk menangkap (**capture**) serta menganalisis paket data yang melewati jaringan.

---

## Dasar Teori

**Wireshark** merupakan perangkat lunak **network protocol analyzer** yang berfungsi untuk menangkap sekaligus menganalisis paket data yang melintas pada suatu jaringan komputer. Dengan aplikasi ini, pengguna dapat mengamati proses komunikasi antar perangkat secara langsung, mulai dari alamat sumber dan tujuan, jenis protokol yang digunakan, hingga informasi yang terdapat di dalam setiap paket.

Sebagai sebuah **packet sniffer**, Wireshark bekerja secara pasif. Artinya, aplikasi ini hanya merekam lalu lintas jaringan tanpa mengubah isi ataupun jalannya komunikasi yang sedang berlangsung. Oleh karena itu, Wireshark sering dimanfaatkan untuk kebutuhan analisis jaringan, troubleshooting, maupun pembelajaran mengenai cara kerja berbagai protokol komunikasi.

Informasi yang ditampilkan oleh Wireshark tersusun berdasarkan lapisan protokol jaringan, seperti **Ethernet**, **Internet Protocol (IP)**, **TCP/UDP**, hingga protokol aplikasi seperti **HTTP**, **DNS**, dan lain sebagainya. Dengan tampilan tersebut, pengguna dapat memahami bagaimana sebuah data dikirim dari pengirim hingga diterima oleh tujuan.

Beberapa bagian utama pada antarmuka Wireshark meliputi:

- **Command Menu** → Berisi berbagai menu dan fungsi utama untuk mengatur proses capture maupun analisis paket.
- **Packet List Window** → Menampilkan daftar seluruh paket yang berhasil direkam selama proses capture.
- **Packet Details Window** → Menampilkan rincian setiap lapisan protokol dari paket yang dipilih.
- **Packet Contents Window** → Menampilkan isi paket dalam format heksadesimal maupun ASCII.
- **Display Filter** → Digunakan untuk menyaring paket berdasarkan protokol atau kriteria tertentu sehingga proses analisis menjadi lebih mudah.

Melalui Wireshark, proses komunikasi jaringan yang biasanya tidak terlihat dapat diamati secara langsung, sehingga memudahkan pengguna dalam memahami mekanisme pertukaran data pada jaringan komputer.

---

## Percobaan

1. Instal aplikasi **Wireshark** pada komputer atau laptop.
2. Jalankan aplikasi Wireshark.
3. Pilih interface jaringan yang sedang digunakan, misalnya **WiFi** atau **Ethernet**.
4. Mulai proses **capture** dengan menekan tombol **Start Capture**.
5. Buka browser kemudian akses halaman berikut:

   `http://gaia.cs.umass.edu/wireshark-labs/INTRO-wireshark-file1.html`

6. Setelah halaman berhasil dimuat, hentikan proses capture pada Wireshark.
7. Gunakan **Display Filter** dengan mengetik:

   `http`

   agar hanya paket HTTP yang ditampilkan.
8. Amati paket **HTTP GET** yang dikirim dari komputer menuju server.
9. Periksa detail paket pada bagian **Packet Details** untuk melihat informasi setiap lapisan protokol.
10. Tutup aplikasi Wireshark setelah seluruh proses pengamatan selesai.

---

## Hasil

Dari hasil capture menggunakan Wireshark, terlihat bahwa aplikasi berhasil merekam berbagai aktivitas komunikasi jaringan yang terjadi ketika browser mengakses halaman web. Paket yang berhasil ditangkap tidak hanya berasal dari satu protokol, tetapi terdiri atas beberapa jenis protokol seperti **TCP**, **DNS**, dan **HTTP** yang saling bekerja sama selama proses komunikasi berlangsung.

Setelah filter **http** diterapkan, hanya paket yang berkaitan dengan protokol HTTP yang ditampilkan. Dari hasil tersebut terlihat adanya paket **HTTP GET** yang dikirim oleh browser sebagai permintaan terhadap halaman web, kemudian server memberikan balasan berupa **HTTP Response** yang berisi data halaman yang diminta.

Selain itu, pada bagian **Packet Details** terlihat bahwa satu paket jaringan tersusun atas beberapa lapisan protokol. Urutan lapisan tersebut dimulai dari **Ethernet Frame**, kemudian **Internet Protocol (IP)**, dilanjutkan dengan **Transmission Control Protocol (TCP)**, dan diakhiri oleh **Hypertext Transfer Protocol (HTTP)** sebagai protokol pada layer aplikasi. Susunan tersebut menunjukkan bahwa setiap protokol memiliki tugas masing-masing dalam proses pengiriman data melalui jaringan.

---

## Analisa

Berdasarkan hasil praktikum, Wireshark mampu menampilkan seluruh aktivitas komunikasi jaringan secara rinci sehingga pengguna dapat mengetahui bagaimana proses pertukaran data berlangsung. Ketika browser mengakses sebuah website, browser terlebih dahulu mengirimkan **HTTP GET Request** kepada server. Setelah permintaan diterima, server kemudian memberikan balasan berupa **HTTP Response** yang berisi halaman web sehingga dapat ditampilkan pada browser.

Selama proses tersebut, tidak hanya paket HTTP yang muncul, tetapi juga paket dari protokol lain seperti **DNS** yang berfungsi menerjemahkan nama domain menjadi alamat IP, serta **TCP** yang bertanggung jawab menjaga keandalan proses pengiriman data. Dengan memanfaatkan fitur **Display Filter**, proses analisis menjadi lebih mudah karena pengguna dapat memfokuskan pengamatan pada protokol tertentu tanpa terganggu oleh paket-paket lainnya.

---

## Kesimpulan

1. Wireshark merupakan aplikasi yang digunakan untuk melakukan proses capture dan analisis terhadap paket data pada jaringan komputer.
2. Komunikasi jaringan melibatkan beberapa lapisan protokol, seperti **Ethernet**, **IP**, **TCP**, dan **HTTP**, yang bekerja secara berurutan dalam proses pengiriman data.
3. Fitur **Display Filter** mempermudah pengguna dalam melakukan analisis karena hanya paket yang sesuai dengan filter yang akan ditampilkan.
4. Praktikum ini memberikan pemahaman mengenai mekanisme komunikasi jaringan secara nyata melalui proses pertukaran paket antara client dan server yang dapat diamati langsung menggunakan Wireshark.