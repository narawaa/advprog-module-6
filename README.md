Pemrograman Lanjut (Advanced Programming) 2024/2025 Genap

- Nama : Nashwa Ghania
- NPM : 2306241770
- Kelas : Pemrograman Lanjut - A

### Reflection 1: Milestone 1

Method handle_connection bertanggung jawab untuk menangani setiap koneksi yang masuk ke server. Saat sebuah koneksi diterima, method ini akan membaca data yang dikirim oleh client, yang biasanya berupa permintaan HTTP.

Pertama, BufReader digunakan untuk membungkus stream sehingga pembacaan data dari koneksi bisa dilakukan lebih efisien. Lalu, method .lines() digunakan untuk membaca data per baris dari request yang dikirim client. Karena .lines() menghasilkan nilai bertipe Result, setiap baris perlu diproses dengan .map(|result| result.unwrap()) agar mendapatkan teks sebenarnya.

Selanjutnya, .take_while(|line| !line.is_empty()) memastikan pembacaan berhenti saat menemukan baris kosong. Dalam HTTP, baris kosong menandakan akhir dari bagian header permintaan. Akhirnya, semua baris request yang telah dikumpulkan disimpan dalam sebuah vektor http_request dan ditampilkan di terminal menggunakan println!.

Secara sederhana, method ini membaca dan mencetak permintaan HTTP yang masuk ke server, tetapi belum melakukan respons balik ke client.

### Reflection 2: Milestone 2

![Commit 2 screen capture](/assets/images/commit2.png)

Dengan kode baru di handle_connection, server dapat membaca permintaan HTTP dari klien dan mengirimkan respons yang lebih lengkap. Pertama, permintaan yang masuk diproses menggunakan BufReader dan disimpan hingga menemukan baris kosong, menandakan akhir dari header HTTP. Setelah itu, server membaca isi file hello.html, menghitung panjangnya, dan menyusun respons HTTP yang berisi status "200 OK", header Content-Length, serta isi halaman. Respons ini kemudian dikirim ke klien menggunakan stream.write_all() sehingga ketika pengguna mengakses server, mereka mendapatkan halaman HTML yang telah disiapkan.
