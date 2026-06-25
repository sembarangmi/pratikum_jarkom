# Laporan Praktikum Modul 14

## WiFi

**Wireless Fidelity (WiFi)** merupakan teknologi komunikasi nirkabel yang mengacu pada standar **IEEE 802.11**. Teknologi ini memungkinkan berbagai perangkat, seperti laptop, smartphone, maupun tablet, saling bertukar data tanpa memerlukan media kabel. Dalam proses komunikasinya, jaringan WiFi memanfaatkan beberapa jenis frame yang memiliki fungsi berbeda, di antaranya **Beacon Frame**, **Data Frame**, **Association Frame**, dan **Disassociation Frame**. Setiap frame memiliki peran tersendiri, mulai dari memperkenalkan jaringan, membangun koneksi, hingga mengirimkan data antar perangkat.

---

## Starting

Sebelum melakukan analisis, file **Wireshark_802_11.pcap** yang terdapat pada arsip **wireshark-traces.zip** diunduh dari situs praktikum kemudian diekstrak. File hasil ekstraksi tersebut selanjutnya dibuka menggunakan aplikasi **Wireshark** sehingga seluruh aktivitas komunikasi pada jaringan WiFi dapat diamati secara detail.

Setelah file berhasil dibuka, Wireshark menampilkan berbagai paket IEEE 802.11 yang terekam selama proses komunikasi berlangsung. Paket-paket tersebut terdiri atas management frame, control frame, serta data frame. Dari kumpulan paket inilah proses analisis dilakukan untuk mengetahui bagaimana perangkat melakukan pencarian jaringan, membangun koneksi dengan Access Point, hingga melakukan pertukaran data.

---

## Beacon Frames

**Beacon Frame** merupakan salah satu management frame yang secara rutin dikirim oleh **Access Point (AP)** untuk mengumumkan keberadaan jaringan WiFi kepada perangkat di sekitarnya. Informasi yang terdapat pada Beacon Frame sangat penting karena digunakan oleh perangkat sebelum melakukan proses koneksi. Beberapa informasi tersebut meliputi **SSID**, channel yang digunakan, kemampuan jaringan, kecepatan transfer yang didukung, hingga parameter lain yang berkaitan dengan konfigurasi jaringan nirkabel.

Untuk mempermudah proses analisis, digunakan filter:

`wlan.fc.type_subtype == 8`

Filter tersebut hanya akan menampilkan paket **Beacon Frame** sehingga informasi mengenai Access Point dapat diamati dengan lebih mudah.

Hasil pengamatan menunjukkan bahwa Beacon Frame yang dikirim oleh Access Point memiliki **Type/Subtype 0x0008**. Dari informasi yang terdapat pada paket tersebut diketahui bahwa Access Point menggunakan **SSID "30 Munroe St"** dan beroperasi pada **Channel 6**. Selain itu juga terlihat berbagai parameter tambahan seperti **Supported Rates** hingga **54 Mbit/s**, informasi negara (**Country Code US**), serta berbagai kemampuan lain yang dimiliki Access Point. Seluruh informasi tersebut dikirim secara berkala agar perangkat di sekitar dapat mengenali keberadaan jaringan dan menentukan apakah jaringan tersebut sesuai untuk digunakan.

---

## Data Transfer

**Data Transfer** merupakan proses pertukaran informasi antara client dan server setelah perangkat berhasil terhubung dengan Access Point. Pada tahap ini berbagai jenis data, seperti halaman web, gambar, file, maupun informasi dari aplikasi, akan dikirim menggunakan **Data Frame** sesuai standar IEEE 802.11.

Untuk mengamati proses pengiriman data HTTP digunakan filter:

`tcp.port == 80`

Melalui hasil pengamatan diketahui bahwa perangkat dengan alamat IP **192.168.1.109** mengirimkan permintaan **HTTP GET** menuju server **128.119.245.12 (gaia.cs.umass.edu)** untuk mengambil file **alice.txt**. Informasi tersebut terlihat pada bagian protokol HTTP yang menunjukkan adanya permintaan terhadap file tersebut.

Selain itu, paket HTTP tersebut berada di dalam **IEEE 802.11 QoS Data Frame**. Hal ini menunjukkan bahwa setelah proses koneksi berhasil dilakukan, komunikasi data berlangsung melalui Data Frame yang membawa informasi dari layer aplikasi. Dengan demikian dapat dipahami bahwa jaringan WiFi tidak hanya bertugas membangun koneksi, tetapi juga menjadi media utama dalam proses pengiriman data antara client dan server.

---

## Association / Disassociation

**Association** merupakan proses ketika perangkat pengguna mengajukan permintaan untuk bergabung dengan sebuah Access Point agar dapat menggunakan layanan jaringan yang tersedia. Sebaliknya, **Disassociation** merupakan proses berakhirnya hubungan komunikasi antara perangkat dengan Access Point. Kedua proses tersebut termasuk ke dalam kategori **Management Frame** pada standar IEEE 802.11.

Untuk melihat proses Association Request digunakan filter:

`wlan.fc.type==0 && wlan.fc.subtype==0`

Hasil analisis menunjukkan adanya beberapa paket **Association Request** yang dikirim oleh host menuju Access Point **linksys_SES_24086**. Munculnya beberapa request secara berulang menunjukkan bahwa perangkat melakukan beberapa kali percobaan untuk bergabung ke jaringan tersebut karena belum memperoleh respons yang sesuai.

Selanjutnya dilakukan pengamatan terhadap **Association Response** menggunakan filter:

`wlan.fc.type==0 && wlan.fc.subtype==1`

Pada hasil pengamatan terlihat bahwa Access Point **30 Munroe St** mengirimkan **Association Response** kepada host sebagai balasan atas permintaan koneksi yang diterima sebelumnya. Paket ini menandakan bahwa proses asosiasi berhasil dilakukan sehingga perangkat telah memperoleh izin untuk bergabung ke jaringan WiFi dan dapat mulai melakukan komunikasi data.

Terakhir dilakukan pencarian terhadap **Disassociation Frame** menggunakan filter:

`wlan.fc.type==0 && wlan.fc.subtype==10`

Dari hasil analisis tidak ditemukan paket **Disassociation** pada file capture. Hal tersebut menunjukkan bahwa selama proses perekaman berlangsung tidak terjadi pemutusan koneksi antara host dan Access Point. Dengan kata lain, perangkat tetap berada dalam kondisi terhubung hingga proses komunikasi selesai.

---

## Kesimpulan

Berdasarkan hasil praktikum, dapat disimpulkan bahwa **Wireshark** dapat digunakan untuk menganalisis mekanisme komunikasi pada jaringan **WiFi IEEE 802.11** secara rinci. Melalui proses pengamatan dapat diketahui bagaimana Access Point secara berkala mengirimkan **Beacon Frame** untuk menginformasikan keberadaan jaringan beserta konfigurasi yang dimilikinya. Setelah perangkat menemukan jaringan yang sesuai, proses koneksi dilakukan melalui pertukaran **Association Request** dan **Association Response** sebelum akhirnya perangkat dapat melakukan komunikasi data.

Selain itu, proses pertukaran informasi antar perangkat berlangsung menggunakan **Data Frame**, yang pada praktikum ini ditunjukkan melalui permintaan **HTTP GET** terhadap file **alice.txt**. Hasil analisis juga menunjukkan bahwa perangkat sempat melakukan beberapa kali percobaan asosiasi sebelum berhasil terhubung dengan Access Point **30 Munroe St**, sementara tidak ditemukan proses **Disassociation** selama proses perekaman berlangsung. Dari keseluruhan pengamatan tersebut dapat dipahami bahwa komunikasi pada jaringan WiFi melibatkan beberapa jenis frame yang saling mendukung sehingga proses koneksi dan pertukaran data dapat berlangsung dengan baik.