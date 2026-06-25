# Laporan praktikum jarkom modul 4 dan 5 gabungan

## Nslookup

**Nslookup** merupakan perintah yang digunakan untuk memperoleh informasi mengenai DNS (Domain Name System), seperti alamat IP suatu domain, DNS server yang bertanggung jawab terhadap domain tersebut, maupun informasi DNS lainnya.

Langkah-langkah percobaan:

1. Buka Command Prompt atau Terminal pada komputer.
2. Jalankan perintah berikut untuk mengetahui alamat IP dari domain MIT.

   `nslookup www.mit.edu`

3. Selanjutnya jalankan perintah berikut untuk melihat Name Server (NS) yang mengelola domain MIT.

   `nslookup -type=NS mit.edu`

4. Terakhir, jalankan perintah berikut menggunakan DNS Google.

   `nslookup www.aiit.or.kr 8.8.8.8`

### Penjelasan

Perintah **nslookup www.mit.edu** digunakan untuk mengetahui alamat IP dari domain **www.mit.edu**, yaitu **23.15.150.186**. Selanjutnya, perintah **nslookup -type=NS mit.edu** menampilkan daftar Name Server yang bertanggung jawab mengelola domain MIT. Sementara itu, perintah **nslookup www.aiit.or.kr 8.8.8.8** menggunakan DNS Google (8.8.8.8) untuk memperoleh alamat IP dari **www.aiit.or.kr**, yaitu **104.21.74.8** dan **172.67.152.120**.

---

## Question

### 1. Jalankan nslookup untuk mendapatkan alamat IP dari server web di Asia. Berapa alamat IP server tersebut?

**Jawaban:**

Alamat IP server web di Asia yang diperoleh dari hasil **nslookup** adalah **34.36.102.170**.

### 2. Jalankan nslookup agar dapat mengetahui server DNS otoritatif untuk universitas di Eropa.

**Jawaban:**

Berdasarkan hasil **nslookup**, server DNS otoritatif untuk domain Universitas Oxford antara lain **dns0.ox.ac.uk** beserta beberapa Name Server lainnya yang bertugas mengelola domain tersebut.

### 3. Jalankan nslookup untuk mencari informasi server email Yahoo! Mail melalui salah satu server yang diperoleh pada soal nomor 2. Berapa alamat IP-nya?

**Jawaban:**

Alamat IP server email Yahoo! Mail tidak berhasil diperoleh melalui **dns0.ox.ac.uk**. Hal ini karena **dns0.ox.ac.uk** merupakan Authoritative Name Server milik domain Oxford, sehingga tidak berfungsi sebagai Recursive DNS Resolver untuk melakukan pencarian domain lain.

---

## Ipconfig

**Ipconfig** adalah perintah pada sistem operasi Windows yang digunakan untuk melihat konfigurasi jaringan yang sedang digunakan oleh komputer, seperti alamat IP, DNS Server, MAC Address, hingga informasi DHCP.

Langkah-langkah percobaan:

1. Buka Command Prompt.
2. Jalankan perintah berikut.

   `ipconfig /all`

3. Selanjutnya jalankan perintah berikut.

   `ipconfig /displaydns`

4. Terakhir jalankan perintah berikut.

   `ipconfig /flushdns`

### Penjelasan

Perintah **ipconfig /all** digunakan untuk menampilkan informasi konfigurasi jaringan secara lengkap, seperti alamat IP, Physical Address (MAC Address), DNS Server, serta informasi DHCP.

Perintah **ipconfig /displaydns** digunakan untuk melihat seluruh DNS cache yang tersimpan pada komputer.

Sedangkan **ipconfig /flushdns** digunakan untuk menghapus seluruh DNS cache sehingga komputer akan melakukan pencarian DNS kembali ketika mengakses suatu domain.