# Laporan Praktikum Modul 12

## ICMP

**ICMP (Internet Control Message Protocol)** merupakan salah satu protokol pada layer jaringan yang berfungsi sebagai media komunikasi untuk menyampaikan informasi, laporan kesalahan, serta pesan diagnostik antar perangkat di dalam jaringan. Berbeda dengan TCP maupun UDP yang digunakan untuk mengirim data aplikasi, ICMP lebih berperan dalam membantu proses pengecekan kondisi jaringan, seperti mengetahui apakah suatu host dapat dijangkau, mendeteksi kesalahan pengiriman paket, hingga memberikan informasi mengenai jalur yang dilewati paket selama proses komunikasi.

### Struktur ICMP

- **Type** → Menunjukkan jenis pesan ICMP.
- **Code** → Memberikan informasi yang lebih spesifik mengenai jenis pesan tersebut.
- **Checksum** → Digunakan untuk memeriksa apakah data mengalami kerusakan selama proses transmisi.
- **Data** → Berisi informasi tambahan sesuai dengan tipe pesan ICMP.

### Beberapa Tipe ICMP

- **Echo Request** → Digunakan saat mengirim permintaan ping.
- **Echo Reply** → Balasan dari Echo Request.
- **Destination Unreachable** → Menunjukkan bahwa tujuan tidak dapat dicapai.
- **Time Exceeded** → Menunjukkan nilai TTL paket telah habis.
- **Redirect** → Memberikan informasi adanya jalur routing yang lebih baik.

---

## Ping

**Ping** merupakan utilitas jaringan yang digunakan untuk menguji apakah suatu host atau server dapat dijangkau melalui jaringan. Perintah ini bekerja dengan mengirimkan paket **ICMP Echo Request** ke alamat tujuan, kemudian menunggu balasan berupa **ICMP Echo Reply**. Selain mengetahui apakah koneksi berhasil, ping juga dapat digunakan untuk mengukur waktu respons (latency), mengetahui kestabilan koneksi, serta mendeteksi kemungkinan terjadinya packet loss.

---

## Tahap Implementasi ICMP dan Ping

Pengujian dilakukan menggunakan perintah:

`ping -n 10 www.ust.hk`

Perintah tersebut digunakan untuk mengirimkan **10 kali** permintaan ping ke server **www.ust.hk**. Selama proses berlangsung, seluruh aktivitas komunikasi direkam menggunakan Wireshark agar setiap paket ICMP dapat diamati secara lebih rinci.

Berdasarkan hasil pengamatan, terdapat **20 paket ICMP** yang tercatat pada Wireshark. Jumlah tersebut terdiri atas **10 paket Echo Request** yang dikirim oleh komputer dan **10 paket Echo Reply** yang dikirim kembali oleh server sebagai balasan. Hal ini menunjukkan bahwa setiap permintaan yang dikirim memperoleh respons dari server sehingga komunikasi berlangsung dengan baik.

Pada proses pengiriman terlihat bahwa komputer mengirimkan paket **ICMP Echo Request** dengan **Type 8 Code 0** menuju alamat IP server tujuan. Paket tersebut membawa payload berukuran **32 byte** yang nantinya akan dikembalikan oleh server sebagai bagian dari proses verifikasi koneksi. Selain itu, nilai **TTL** yang terdapat pada paket menunjukkan batas jumlah hop yang dapat dilewati selama proses pengiriman menuju tujuan.

Setelah server menerima permintaan tersebut, server mengirimkan **ICMP Echo Reply** dengan **Type 0 Code 0** sebagai balasan. Data yang diterima kembali memiliki ukuran yang sama dengan data yang dikirim sebelumnya, sehingga menunjukkan bahwa proses transmisi berlangsung tanpa perubahan isi paket. Dari hasil pengamatan juga diperoleh waktu respons sekitar **65 ms**, yang menunjukkan lamanya perjalanan paket dari komputer menuju server kemudian kembali lagi ke komputer.

Berdasarkan keseluruhan proses tersebut dapat disimpulkan bahwa komunikasi antara komputer dan server berjalan dengan baik. Seluruh paket permintaan berhasil memperoleh balasan tanpa adanya indikasi kehilangan paket (**packet loss**), sehingga koneksi jaringan dapat dikatakan stabil dan server tujuan dapat diakses dengan normal.

---

## Traceroute

**Traceroute** merupakan utilitas jaringan yang digunakan untuk mengetahui jalur yang dilalui paket data dari komputer pengirim menuju server tujuan. Informasi yang ditampilkan berupa daftar router atau **hop** yang dilewati paket selama proses komunikasi berlangsung.

Cara kerja traceroute berbeda pada setiap sistem operasi. Pada Windows digunakan paket **ICMP**, sedangkan pada Linux dan Unix umumnya menggunakan paket **UDP**. Prinsip kerjanya adalah mengirim paket dengan nilai **TTL (Time To Live)** yang terus bertambah secara bertahap. Ketika nilai TTL habis di sebuah router, router tersebut akan mengirimkan pesan **ICMP Time Exceeded** sehingga alamat router tersebut dapat diketahui.

---

## Tahap Implementasi ICMP dan Traceroute

Pengujian dilakukan menggunakan perintah:

`tracert www.inria.fr`

Perintah tersebut digunakan untuk mengetahui jalur yang ditempuh paket dari komputer menuju server **www.inria.fr**. Seluruh proses komunikasi kemudian diamati menggunakan Wireshark.

Hasil pengamatan menunjukkan bahwa komputer mengirimkan paket dengan nilai **TTL** yang meningkat secara bertahap, dimulai dari **TTL = 1**, kemudian **TTL = 2**, dan seterusnya hingga paket berhasil mencapai server tujuan. Setiap router yang dilewati akan mengurangi nilai TTL sebanyak satu. Ketika nilai tersebut mencapai nol, router akan menghentikan pengiriman paket dan mengirimkan pesan **ICMP Time Exceeded (Type 11)** kepada komputer pengirim.

Melalui mekanisme tersebut, setiap router yang berada pada jalur komunikasi dapat diketahui secara berurutan. Dengan kata lain, traceroute mampu menampilkan seluruh hop yang dilewati paket mulai dari jaringan lokal hingga mencapai server tujuan. Informasi ini sangat berguna untuk melakukan analisis jaringan maupun mendeteksi lokasi terjadinya gangguan komunikasi.

Selain pesan **Time Exceeded**, pada beberapa kondisi juga dapat ditemukan pesan **Destination Unreachable (Type 3)** apabila tujuan tidak dapat dicapai atau terdapat pembatasan tertentu pada jaringan. Pesan-pesan ICMP tersebut menjadi dasar bagi traceroute untuk menyusun daftar jalur yang dilalui paket selama proses pengiriman.

---

## Kesimpulan

Berdasarkan hasil praktikum, dapat dipahami bahwa **ICMP** merupakan protokol yang memiliki peran penting dalam proses monitoring dan diagnosis jaringan. Melalui utilitas **ping**, pengguna dapat mengetahui apakah suatu host dapat diakses sekaligus mengukur waktu respons koneksi menggunakan mekanisme **Echo Request** dan **Echo Reply**.

Selain itu, penggunaan **traceroute** memperlihatkan bagaimana nilai **TTL** dimanfaatkan untuk mengidentifikasi setiap router yang dilewati paket menuju tujuan. Ketika nilai TTL habis, router akan mengirimkan pesan **ICMP Time Exceeded**, sehingga jalur komunikasi dapat dipetakan secara bertahap. Dari seluruh hasil pengamatan menggunakan Wireshark, proses komunikasi jaringan dapat dianalisis dengan lebih detail, mulai dari pengiriman paket, penerimaan balasan, hingga proses identifikasi rute yang dilalui paket menuju server tujuan.