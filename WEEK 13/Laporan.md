# Laporan Praktikum Modul 13

## Caching ARP

**Address Resolution Protocol (ARP)** merupakan protokol yang digunakan untuk menerjemahkan alamat **IP Address** menjadi **MAC Address** pada jaringan lokal. Ketika sebuah perangkat ingin berkomunikasi dengan perangkat lain dalam satu jaringan, perangkat tersebut harus mengetahui MAC Address dari tujuan agar data dapat dikirim melalui layer data link. Apabila informasi tersebut belum tersedia, maka ARP akan melakukan proses pencarian terlebih dahulu.

Untuk mempercepat proses komunikasi, sistem operasi menyediakan **ARP Cache**, yaitu tempat penyimpanan sementara hasil pemetaan antara IP Address dan MAC Address. Dengan adanya cache ini, komputer tidak perlu mengirimkan ARP Request berulang kali ketika akan berkomunikasi dengan perangkat yang sama. Hal tersebut dapat mengurangi lalu lintas broadcast pada jaringan sekaligus meningkatkan efisiensi komunikasi.

Sebelum melakukan pengamatan, ARP Cache terlebih dahulu dihapus agar proses pencarian alamat MAC dapat diamati kembali sejak awal.

- Pada **Windows (MS-DOS)** digunakan perintah:

  `arp -d *`

- Sedangkan pada **Linux, Unix, maupun macOS**, perintah yang digunakan juga:

  `arp -d *`

  Namun, perintah tersebut harus dijalankan menggunakan hak akses **root** atau **administrator**.

---

## ARP

Setelah ARP Cache berhasil dihapus, proses pengamatan dilakukan menggunakan Wireshark. Browser kemudian digunakan untuk mengakses halaman web yang berada pada server **gaia.cs.umass.edu** sehingga komputer harus melakukan komunikasi dengan gateway terlebih dahulu. Agar proses analisis lebih mudah, hanya paket **ARP** yang ditampilkan menggunakan filter pada Wireshark sehingga paket dari protokol lain tidak ikut terlihat.

Berdasarkan hasil pengamatan, proses pertama yang muncul adalah **ARP Request**. Pada tahap ini komputer belum mengetahui alamat MAC dari perangkat tujuan sehingga paket dikirim menggunakan metode **broadcast** ke seluruh perangkat dalam jaringan lokal. Hal tersebut ditandai dengan alamat tujuan Ethernet **ff:ff:ff:ff:ff:ff**, yang berarti seluruh perangkat pada jaringan menerima paket tersebut.

Di dalam paket ARP Request juga terlihat bahwa alamat MAC tujuan masih bernilai **00:00:00:00:00:00**. Nilai tersebut menunjukkan bahwa komputer belum mengetahui alamat fisik dari perangkat yang memiliki **IP Address 192.168.1.1**. Oleh karena itu, komputer mengirimkan pertanyaan kepada seluruh perangkat dalam jaringan dengan tujuan mencari siapa yang memiliki alamat IP tersebut.

Tidak lama setelah ARP Request dikirim, perangkat yang memiliki **IP Address 192.168.1.1** memberikan balasan berupa **ARP Reply**. Pada paket balasan tersebut, perangkat menginformasikan bahwa alamat IP **192.168.1.1** dipetakan dengan **MAC Address 84:3c:99:9a:ec:8d**. Berbeda dengan ARP Request yang dikirim secara broadcast, ARP Reply dikirim langsung (**unicast**) kepada komputer yang meminta informasi sehingga hanya pengirim awal yang menerima balasan tersebut.

Setelah proses ARP Reply diterima, komputer kemudian menyimpan pasangan **IP Address** dan **MAC Address** tersebut ke dalam **ARP Cache**. Penyimpanan ini bertujuan agar komunikasi berikutnya dengan perangkat yang sama dapat dilakukan secara langsung tanpa perlu mengirimkan ARP Request lagi. Dengan demikian, proses pengiriman data menjadi lebih cepat karena komputer sudah mengetahui alamat fisik tujuan yang harus digunakan pada setiap frame Ethernet.

Melalui hasil pengamatan tersebut dapat diketahui bahwa perangkat dengan **IP Address 192.168.1.1** memiliki **MAC Address 84:3c:99:9a:ec:8d**. Informasi inilah yang kemudian digunakan oleh komputer selama masih tersimpan di dalam ARP Cache.

---

## Kesimpulan

Berdasarkan praktikum yang telah dilakukan, dapat dipahami bahwa **ARP** memiliki peran penting dalam proses komunikasi pada jaringan lokal karena bertugas menerjemahkan **IP Address** menjadi **MAC Address**. Ketika alamat MAC belum diketahui, komputer akan mengirimkan **ARP Request** secara broadcast untuk mencari perangkat yang memiliki alamat IP tujuan. Setelah perangkat tujuan memberikan **ARP Reply**, informasi tersebut akan digunakan sebagai acuan dalam proses komunikasi selanjutnya.

Selain itu, hasil pemetaan alamat IP dan MAC akan disimpan sementara di dalam **ARP Cache** sehingga komputer tidak perlu melakukan proses pencarian ulang setiap kali berkomunikasi dengan perangkat yang sama. Mekanisme ini membuat komunikasi jaringan menjadi lebih cepat, mengurangi jumlah paket broadcast yang dikirim, serta meningkatkan efisiensi pertukaran data pada jaringan lokal.