Pemrograman Lanjut (Advanced Programming) 2024/2025 Genap

- Nama : Nashwa Ghania
- NPM : 2306241770
- Kelas : Pemrograman Lanjut - A

### Reflection 1

Method handle_connection bertanggung jawab untuk menangani setiap koneksi yang masuk ke server. Saat sebuah koneksi diterima, method ini akan membaca data yang dikirim oleh client, yang biasanya berupa permintaan HTTP.

Pertama, BufReader digunakan untuk membungkus stream, sehingga pembacaan data dari koneksi bisa dilakukan lebih efisien. Lalu, method .lines() digunakan untuk membaca data per baris dari request yang dikirim client. Karena .lines() menghasilkan nilai bertipe Result, setiap baris perlu diproses dengan .map(|result| result.unwrap()) agar mendapatkan teks sebenarnya.

Selanjutnya, .take_while(|line| !line.is_empty()) memastikan pembacaan berhenti saat menemukan baris kosong. Dalam HTTP, baris kosong menandakan akhir dari bagian header permintaan. Akhirnya, semua baris request yang telah dikumpulkan disimpan dalam sebuah vektor http_request dan ditampilkan di terminal menggunakan println!.

Secara sederhana, method ini membaca dan mencetak permintaan HTTP yang masuk ke server, tetapi belum melakukan respons balik ke client.
