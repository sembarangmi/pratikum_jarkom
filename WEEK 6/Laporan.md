# Laporan Praktikum Jarkom Week 6

## TCP

## Menangkap Transfer TCP dalam Jumlah Besar dari Komputer Pribadi ke Remote Server

Pada percobaan ini dilakukan pengiriman file dari komputer klien menuju server menggunakan protokol TCP. Seluruh aktivitas komunikasi diamati menggunakan Wireshark untuk melihat bagaimana proses transfer data berlangsung.

Langkah-langkah percobaan:

1. Jalankan aplikasi Wireshark.
2. Buka browser kemudian akses halaman berikut.

   `http://gaia.cs.umass.edu/wireshark-labs/TCP-wireshark-file1.html`

3. Setelah halaman berhasil dimuat, pilih file **alice.txt** kemudian lakukan proses upload.
4. Perhatikan paket-paket yang muncul pada Wireshark selama proses pengiriman berlangsung.
5. Setelah proses selesai, hentikan capture dan lakukan analisis terhadap paket TCP yang telah direkam.

### Penjelasan

Pada awal komunikasi terlihat browser mengirimkan **HTTP GET Request** untuk meminta halaman upload dari server **gaia.cs.umass.edu**. Setelah file **alice.txt** dipilih, browser mengirimkan data menggunakan metode **HTTP POST**.

Karena ukuran file cukup besar, data tidak dikirim dalam satu paket, melainkan dibagi menjadi beberapa segmen TCP. Mekanisme ini bertujuan agar proses pengiriman lebih andal dan seluruh data dapat diterima dengan baik oleh server.

Setelah semua segmen berhasil diterima, server mengirimkan respons **HTTP/1.1 200 OK** sebagai tanda bahwa proses upload telah berhasil diselesaikan.

---

## Tampilan Awal pada Captured Trace

## Question

### 1. Berapa alamat IP dan nomor port TCP yang digunakan oleh komputer klien (sumber) untuk mentransfer file ke gaia.cs.umass.edu?

**Jawaban:**

Berdasarkan hasil analisis paket pada Wireshark, alamat IP komputer klien adalah **10.218.13.38**, sedangkan nomor port TCP yang digunakan untuk koneksi tersebut adalah **52789**.