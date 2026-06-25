# Laporan praktikum jarkom modul 3

## Basic HTTP GET/response interaction

Saat mengakses sebuah halaman web menggunakan protokol HTTP, browser akan mengirimkan **HTTP GET request** ke server. Selanjutnya server memberikan **HTTP response** yang berisi halaman web (HTML). Seluruh proses tersebut dapat diamati melalui Wireshark.

Langkah-langkah percobaan:

1. Jalankan aplikasi Wireshark.
2. Salin dan buka link berikut pada browser dengan memastikan menggunakan protokol **http**.

   `http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file1.html`

3. Setelah halaman berhasil dimuat, kembali ke Wireshark lalu hentikan proses capture dengan menekan tombol **Stop Capture** (ikon kotak merah). Setelah itu masukkan filter **http**.
4. Cari paket HTTP yang sesuai, kemudian klik paket tersebut untuk melihat detailnya.

Pada bagian paling bawah detail paket akan terlihat isi HTTP Response. Jika isi teks yang ditampilkan sama dengan halaman web yang dibuka sebelumnya, maka proses request dan response berhasil diamati.

---

## HTTP Conditional GET/response interaction

Pada **HTTP Conditional GET**, browser hanya akan meminta data baru apabila file pada server mengalami perubahan. Jika file belum berubah, browser akan menggunakan data yang tersimpan di cache. Proses ini juga dapat diamati melalui Wireshark.

> Sebelum memulai percobaan, pastikan cache browser sudah dikosongkan.

Langkah-langkah:

1. Jalankan Wireshark.
2. Buka link berikut menggunakan browser dengan protokol **http**.

   `http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file2.html`

3. Setelah halaman terbuka, hentikan proses capture pada Wireshark lalu gunakan filter **http**.
4. Pilih paket HTTP yang sesuai dan periksa isi paket tersebut.
5. Cocokkan isi teks pada bagian bawah paket dengan isi halaman web. Jika sama, maka proses berhasil.

### Penjelasan

Pada hasil capture akan terlihat proses **TCP Reassembly**. Halaman web dikirim dalam beberapa segmen TCP karena ukuran data cukup besar. Setelah seluruh segmen diterima, Wireshark akan menyusun kembali data tersebut sehingga file dapat diterima secara utuh.

---

## Retrieving Long Documents

Saat mengunduh dokumen HTML berukuran besar, server akan membaginya menjadi beberapa segmen TCP sebelum dikirim ke klien. Setelah semua segmen diterima, data akan digabungkan kembali melalui proses **TCP Reassembly**.

Langkah-langkah:

1. Jalankan Wireshark.
2. Buka halaman berikut menggunakan browser.

   `http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file3.html`

3. Setelah halaman berhasil dimuat, hentikan proses capture lalu gunakan filter **http**.
4. Pilih paket HTTP yang sesuai dan pastikan isi halaman sama dengan yang tampil pada browser.
5. Selanjutnya ubah filter menjadi **tcp** untuk melihat proses pengiriman data.

### Penjelasan

1. Paket pertama menunjukkan **HTTP GET Request** dari klien menuju server.
2. Server kemudian memberikan respons sebagai tanda bahwa permintaan telah diterima.
3. File HTML dikirim dalam beberapa segmen TCP karena ukurannya cukup besar.
4. Setelah semua segmen diterima, Wireshark melakukan **TCP Reassembly** sehingga data dapat dibaca secara lengkap.

---

## HTML Documents dengan Embedded Objects

Halaman HTML yang memiliki **embedded objects** seperti gambar akan membuat browser mengirim beberapa HTTP GET request untuk mengambil setiap objek tersebut. Request tersebut dapat berasal dari server yang sama maupun server yang berbeda.

Langkah-langkah:

1. Jalankan Wireshark.
2. Buka halaman berikut menggunakan browser.

   `http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file4.html`

3. Lakukan **Inspect Element** pada browser untuk melihat sumber gambar yang digunakan.
4. Hentikan proses capture di Wireshark kemudian gunakan filter **http**.
5. Amati paket-paket HTTP yang muncul.

### Penjelasan

Terlihat beberapa request tambahan selain file HTML utama. Browser mengirim request untuk mengambil file gambar dengan format seperti **PNG** dan **JPG**. Hal tersebut menunjukkan bahwa setiap objek pada halaman web diambil secara terpisah sebelum seluruh halaman ditampilkan.

---

## HTTP Authentication

Pada **HTTP Authentication**, informasi login dikirim dalam bentuk **plaintext**, sehingga username dan password dapat terlihat melalui Wireshark. Hal ini menunjukkan bahwa HTTP tidak memberikan perlindungan berupa enkripsi.

Langkah-langkah:

1. Jalankan Wireshark.
2. Buka halaman berikut menggunakan browser.

   `http://gaia.cs.umass.edu/wireshark-labs/protected_pages/HTTP-wireshark-file5.html`

3. Masukkan username **wireshark-students** dan password **network**.
4. Setelah berhasil login, hentikan proses capture lalu gunakan filter **http**.
5. Pilih paket HTTP yang berkaitan dengan proses autentikasi.

### Penjelasan

Pada detail paket terlihat bahwa username dan password masih dapat dibaca dalam bentuk teks biasa (plaintext). Hal ini membuktikan bahwa HTTP tidak menggunakan enkripsi sehingga kurang aman untuk mengirimkan data yang bersifat sensitif.

---

## Kesimpulan

Berdasarkan praktikum yang telah dilakukan, dapat dipahami bahwa browser selalu mengirimkan **HTTP GET Request** ketika mengakses halaman web dan server akan membalas dengan **HTTP Response**. Pada **Conditional GET**, browser memanfaatkan cache sehingga data tidak selalu diunduh kembali apabila belum mengalami perubahan.

Untuk dokumen berukuran besar, data dikirim dalam beberapa segmen TCP kemudian digabungkan kembali melalui proses **TCP Reassembly**. Selain itu, halaman web yang memiliki embedded objects akan menghasilkan beberapa request tambahan untuk mengambil setiap objek yang terdapat pada halaman tersebut.

Pada percobaan **HTTP Authentication**, terlihat bahwa username dan password masih dikirim dalam bentuk plaintext sehingga menunjukkan bahwa HTTP tidak aman untuk pertukaran data sensitif tanpa menggunakan enkripsi seperti HTTPS.