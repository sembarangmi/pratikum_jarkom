# Laporan Praktikum Modul 7

## Program Socket dengan UDP

UDP merupakan protokol komunikasi yang bekerja tanpa membangun koneksi terlebih dahulu (**connectionless**). Agar data dapat dikirim ke tujuan yang benar, pengirim harus menyertakan alamat IP dan nomor port tujuan pada setiap paket. Setelah paket diterima, sistem akan meneruskannya ke aplikasi yang sesuai berdasarkan nomor port yang digunakan. Selain alamat tujuan, paket juga memiliki informasi alamat sumber yang biasanya diatur secara otomatis oleh sistem operasi sehingga aplikasi tidak perlu menentukannya secara manual.

## Program Socket dengan TCP

TCP adalah protokol yang bersifat **connection-oriented**, sehingga client dan server harus membangun koneksi terlebih dahulu sebelum melakukan pertukaran data. Proses tersebut dilakukan melalui mekanisme **three-way handshake** yang berjalan secara otomatis pada layer transport.

Setelah koneksi berhasil dibuat, client dapat mengirim data tanpa perlu menyertakan alamat tujuan pada setiap proses pengiriman karena koneksi sudah terbentuk. Di sisi server, tersedia sebuah socket yang berfungsi menerima permintaan koneksi dari client. Ketika koneksi diterima, server akan membuat socket baru yang khusus digunakan untuk melayani client tersebut. Dengan mekanisme ini, TCP mampu menjamin pengiriman data secara berurutan, lengkap, dan lebih andal dibandingkan UDP.

## Kesimpulan

Berdasarkan praktikum yang telah dilakukan, dapat dipahami bahwa komunikasi jaringan menggunakan socket dapat diimplementasikan melalui dua protokol, yaitu **UDP** dan **TCP**. UDP bekerja tanpa membangun koneksi sehingga proses pengiriman data lebih sederhana dan cepat, namun tidak menjamin paket diterima oleh tujuan.

Sebaliknya, TCP mengharuskan adanya pembentukan koneksi sebelum data dikirim. Meskipun prosesnya sedikit lebih kompleks, TCP mampu memberikan jaminan bahwa data diterima secara utuh, berurutan, dan lebih stabil selama komunikasi berlangsung.

Dengan demikian, pemilihan penggunaan UDP atau TCP disesuaikan dengan kebutuhan aplikasi. UDP lebih cocok digunakan ketika kecepatan menjadi prioritas, sedangkan TCP lebih sesuai untuk aplikasi yang membutuhkan keandalan dan integritas data.