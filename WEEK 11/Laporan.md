# Laporan Praktikum Modul 11

## DHCP

DHCP (**Dynamic Host Configuration Protocol**) merupakan protokol jaringan yang digunakan untuk memberikan konfigurasi jaringan secara otomatis kepada perangkat yang terhubung ke suatu jaringan. Dengan adanya DHCP, pengguna tidak perlu lagi mengatur alamat IP, subnet mask, gateway, maupun DNS secara manual karena seluruh informasi tersebut diberikan langsung oleh DHCP Server. Cara ini membuat pengelolaan jaringan menjadi lebih mudah, terutama pada jaringan yang memiliki banyak perangkat.

### Proses DHCP (DORA)

- **Discover** → Client mencari DHCP Server yang tersedia.
- **Offer** → Server menawarkan alamat IP kepada client.
- **Request** → Client memilih dan meminta alamat IP yang ditawarkan.
- **Acknowledgement (ACK)** → Server mengonfirmasi bahwa alamat IP telah diberikan kepada client.

### Jenis Pesan DHCP

- **DHCP Discover**
- **DHCP Offer**
- **DHCP Request**
- **DHCP ACK**
- **DHCP NAK**
- **DHCP Release**

---

## Tahap Implementasi DHCP

Pengamatan dilakukan menggunakan Wireshark untuk melihat proses komunikasi antara client dan DHCP Server. Dari hasil capture paket terlihat bahwa perangkat yang belum memiliki alamat IP akan memulai komunikasi dengan mengirimkan paket **DHCP Discover** secara broadcast. Karena client belum memperoleh konfigurasi jaringan, alamat sumber yang digunakan masih **0.0.0.0** dan alamat tujuan adalah **255.255.255.255**. Tujuan dari paket ini adalah mencari DHCP Server yang aktif pada jaringan.

Setelah menerima pesan Discover, DHCP Server memberikan balasan berupa **DHCP Offer** yang berisi informasi alamat IP yang dapat digunakan oleh client beserta konfigurasi jaringan lainnya. Client kemudian memilih penawaran tersebut dan mengirimkan **DHCP Request** sebagai tanda bahwa alamat IP tersebut ingin digunakan.

Tahap berikutnya adalah **DHCP ACK (Acknowledgement)**. Pada tahap ini server memberikan konfirmasi bahwa alamat IP telah resmi dialokasikan kepada client. Setelah menerima ACK, perangkat akan langsung mengonfigurasi alamat IP yang diberikan sehingga dapat mulai berkomunikasi dengan perangkat lain di dalam jaringan.

Selain proses pemberian alamat IP, hasil pengamatan juga menunjukkan adanya **DHCP Renewal**. Pada proses ini client yang masih menggunakan alamat IP sebelumnya menghubungi DHCP Server untuk memperpanjang masa berlaku (lease time) alamat IP tersebut. Jika permintaan disetujui, server kembali mengirimkan paket ACK sehingga client dapat terus menggunakan alamat IP yang sama tanpa harus mengulang seluruh proses DORA.

Selanjutnya juga terlihat proses **DHCP Release**, yaitu ketika client secara sengaja mengembalikan alamat IP yang sedang digunakan kepada DHCP Server. Setelah menerima pesan Release, server memasukkan kembali alamat IP tersebut ke dalam daftar alamat yang tersedia sehingga dapat digunakan oleh perangkat lain. Karena client sudah tidak lagi memiliki alamat IP, perangkat akan mengulangi kembali proses **Discover, Offer, Request, dan ACK** apabila ingin terhubung ke jaringan lagi.

---

## Kesimpulan

Berdasarkan hasil praktikum, dapat disimpulkan bahwa DHCP mempermudah proses konfigurasi jaringan dengan memberikan alamat IP secara otomatis kepada setiap client yang terhubung. Proses tersebut berlangsung melalui mekanisme **DORA (Discover, Offer, Request, dan ACK)** sehingga pembagian alamat IP dapat dilakukan secara sistematis dan terstruktur.

Selain proses pemberian alamat IP, DHCP juga mendukung mekanisme **Renewal** untuk memperpanjang masa sewa alamat IP serta **Release** untuk mengembalikan alamat IP ke server ketika sudah tidak digunakan. Dengan adanya fitur-fitur tersebut, pengelolaan alamat IP menjadi lebih efisien, mengurangi kesalahan konfigurasi manual, serta memudahkan administrasi jaringan yang memiliki banyak perangkat.