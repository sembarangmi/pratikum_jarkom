# Laporan Praktikum Modul 10

## Menangkap Paket dari Eksekusi Traceroute

Pada praktikum ini dilakukan pengujian menggunakan perintah **tracert** untuk mengetahui jalur yang dilalui paket data dari komputer lokal menuju server **gaia.cs.umass.edu**. Seluruh proses komunikasi diamati menggunakan Wireshark sehingga setiap paket yang melewati router dapat dianalisis.

---

## IPv4 Dasar

Untuk mengamati paket yang berkaitan dengan traceroute, digunakan filter **icmp** pada Wireshark. Filter tersebut akan menampilkan paket **ICMP Echo Request** yang dikirim oleh host serta paket **ICMP Time Exceeded** yang dikirim oleh router ketika nilai **Time To Live (TTL)** habis.

Pada tahap awal, komputer mengirimkan paket **Echo Request** dengan nilai **TTL = 1**. Nilai tersebut sengaja dibuat kecil agar paket berhenti pada router pertama. Ketika nilai TTL habis, router akan membuang paket tersebut dan mengirimkan pesan **ICMP Time Exceeded** sebagai balasan ke komputer pengirim.

Dari hasil pengamatan terlihat bahwa router pertama dengan alamat IP **192.168.100.1** mengirimkan balasan **ICMP Type 11 (Time Exceeded)**. Hal ini menunjukkan bahwa paket tidak dapat diteruskan karena nilai TTL telah mencapai nol, sekaligus memberikan informasi mengenai hop pertama pada jalur komunikasi.

Selanjutnya sistem secara otomatis menaikkan nilai **TTL menjadi 2** dan mengirimkan paket kembali. Dengan nilai TTL yang lebih besar, paket berhasil melewati router pertama dan mencapai router berikutnya. Proses ini terus berulang dengan penambahan nilai TTL hingga paket akhirnya mencapai server tujuan. Melalui mekanisme tersebut, seluruh jalur yang dilewati paket dapat diketahui satu per satu.

---

## IPv6

Pada pengamatan paket **IPv6**, terlihat bahwa format alamat sumber (**Source Address**) maupun alamat tujuan (**Destination Address**) menggunakan panjang **128-bit** dalam bentuk heksadesimal. Format ini berbeda dengan IPv4 yang hanya menggunakan alamat sepanjang **32-bit**.

Selain itu, pada IPv6 istilah **Time To Live (TTL)** sudah tidak digunakan lagi dan digantikan oleh **Hop Limit**. Fungsi keduanya tetap sama, yaitu membatasi jumlah hop yang dapat dilewati sebuah paket agar tidak terus berputar di jaringan.

Header IPv6 juga memiliki struktur yang lebih sederhana dibandingkan IPv4. Beberapa field yang terdapat pada IPv4, seperti **Header Checksum** dan informasi fragmentasi, tidak lagi ditempatkan pada header utama, melainkan dipindahkan ke extension header apabila diperlukan. Dengan desain tersebut, proses forwarding paket oleh router menjadi lebih ringan sehingga kinerja jaringan menjadi lebih efisien.

---

## Kesimpulan

Berdasarkan praktikum yang telah dilakukan, dapat dipahami bahwa proses **traceroute** memanfaatkan nilai **TTL** pada IPv4 atau **Hop Limit** pada IPv6 untuk mengetahui jalur yang dilewati paket menuju tujuan. Setiap kali nilai tersebut habis di sebuah router, perangkat tersebut akan mengirimkan pesan **ICMP Time Exceeded**, sehingga komputer dapat mengidentifikasi setiap hop yang dilewati.

Selain itu, hasil pengamatan juga menunjukkan bahwa **IPv6** memiliki struktur header yang lebih sederhana dibandingkan **IPv4**. Penyederhanaan tersebut membuat proses routing menjadi lebih cepat dan efisien, sehingga IPv6 lebih siap digunakan untuk mendukung kebutuhan komunikasi pada jaringan modern.