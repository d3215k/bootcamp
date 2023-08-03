[TOC]

# <b>02.</b> Routing

Routing adalah proses menentukan bagaimana aplikasi Laravel merespons permintaan HTTP dari pengguna. Ketika pengguna mengakses URL tertentu di aplikasi Anda, Laravel akan menggunakan routing untuk menentukan tindakan apa yang harus diambil dan bagaimana menangani permintaan tersebut.

Baik, mari kita mulai dengan tentang routing di Laravel dengan contoh response yang sederhana.

### Langkah 1: Membuat Rute Dasar
Buka file routes/web.php. Di sini, Anda akan menentukan rute HTTP untuk aplikasi web Anda. Misalnya, mari kita tambahkan rute untuk halaman utama:
```php
Route::get('/', function () {
    return 'Selamat datang di halaman utama!';
});
```

Kode di atas menentukan bahwa ketika pengguna mengakses URL utama (biasanya domain Anda), aplikasi akan merespons dengan teks "Selamat datang di halaman utama!".

### Langkah 2: Menjalankan Aplikasi
Pastikan Anda sudah menjalankan server pengembangan Laravel. Jika belum, jalankan perintah berikut di terminal atau command prompt:
```
php artisan serve
```

Laravel akan berjalan di server lokal pada alamat http://localhost:8000 atau alamat lain yang ditampilkan di terminal.

### Langkah 3: Menguji Rute
Buka browser Anda dan akses alamat http://localhost:8000 atau alamat yang sesuai dengan server lokal yang berjalan. Anda akan melihat teks "Selamat datang di halaman utama!" tampil di layar.

### Langkah 4: Menanggapi Permintaan dengan View
Selain mengirimkan teks, Anda juga dapat merespons permintaan dengan view. Misalnya, buatlah file view dengan nama welcome.blade.php di dalam folder resources/views dan tambahkan konten berikut:
```html filename=welcome.blade.php
<!DOCTYPE html>
<html>
<head>
    <title>Selamat Datang</title>
</head>
<body>
    <h1>Selamat datang di halaman utama!</h1>
</body>
</html>
```

Kemudian, ubah rute pada routes/web.php untuk merespons dengan view tersebut:
```php filename=routes/web.php
Route::get('/', function () {
    return view('welcome');
});
```

Sekarang, ketika pengguna mengakses URL utama, aplikasi akan merespons dengan menampilkan halaman view welcome.blade.php.

### Langkah 5: Menggunakan Parameter dalam Rute
Anda juga dapat menentukan rute dengan parameter yang diambil dari URL. Misalnya, jika Anda ingin menampilkan informasi tentang pengguna berdasarkan ID mereka, Anda bisa melakukannya seperti ini:
```php filename=routes/web.php
Route::get('/user/{id}', function ($id) {
    return 'Ini adalah halaman untuk pengguna dengan ID: ' . $id;
});
```

Kemudian, ketika pengguna mengakses URL seperti http://localhost:8000/user/1, aplikasi akan menampilkan teks "Ini adalah halaman untuk pengguna dengan ID: 1".
