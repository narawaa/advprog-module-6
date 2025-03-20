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

### Reflection 3: Milestone 3

![Commit 3 screen capture](/assets/images/commit3.png)

Dengan kode baru setelah refactoring, pemisahan antara respons untuk halaman utama dan halaman 404 menjadi lebih rapi dan efisien. Sebelumnya, ada dua blok kode yang hampir sama untuk menangani respons "200 OK" dan "404 NOT FOUND", yang membuat kode lebih panjang dan sulit dikelola. Setelah refactoring, pemilihan status dan file dilakukan dalam satu blok dengan menggunakan if request_line == "GET / HTTP/1.1" sehingga mengurangi duplikasi. Ini membuat kode lebih ringkas, mudah dibaca, dan lebih fleksibel.

### Reflection 4: Milestone 4

Saat mengakses 127.0.0.1/sleep, server menunggu 5 detik sebelum merespons karena thread::sleep(). Jika membuka dua browser dan mencoba /sleep di satu serta / di lainnya, permintaan kedua akan tertunda. Ini menunjukkan bahwa server menangani permintaan secara berurutan (blocking), yang bisa menyebabkan keterlambatan jika banyak pengguna mengaksesnya sekaligus.

### Reflection 5: Milestone 5

ThreadPool bekerja dengan membuat sejumlah thread worker yang siap menangani tugas. Saat ada tugas baru, tugas tersebut dikirim melalui channel ke salah satu worker yang tersedia. Worker mengambil tugas, menjalankannya, lalu kembali siap menerima tugas berikutnya. Jika ThreadPool dihentikan, semua worker akan menyelesaikan tugas yang tersisa sebelum ditutup. Ini membantu menjalankan banyak tugas secara paralel tanpa harus membuat thread baru setiap kali ada tugas.

### Bonus

Menggunakan build sebagai pengganti new agar fungsi lebih deskriptif dan menunjukkan bahwa kita sedang membangun objek ThreadPool. Dilakukan juga validasi agar ukuran thread pool tidak nol, yang bisa menyebabkan error saat dijalankan. Dengan menambahkan pesan log saat pembuatan thread pool, kita bisa memahami lebih jelas kapan dan bagaimana worker threads dibuat.
