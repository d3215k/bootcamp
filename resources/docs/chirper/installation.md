[TOC]

# <b>02.</b> Installation

## Installing Laravel

### Install Cepat dengan Composer

Jika sudah meng-install PHP dan Composer di local machine, kita bisa langsung membuat project Laravel baru dengan
Composer:

```shell
composer create-project laravel/laravel chirper
```

Setelah project dibuat, jalankan server local development dari Laravel menggunakan Laravel Artisan CLI:

```none
cd chirper

php artisan serve
```

Setelah Server Artisan developmentnya dijalankan, aplikasi dapat kita akses dengan web browser di
[http://localhost:8000](http://localhost:8000).

<img src="/img/screenshots/fresh.png" alt="A fresh Laravel installation" class="border rounded-lg shadow-lg dark:hidden" />
<img src="/img/screenshots/fresh-dark.png" alt="A fresh Laravel installation" class="hidden border-gray-700 rounded-lg shadow-lg dark:block" />

Biar lebih sederhana, kita gunakan SQLite untuk menyimpan data. Cara set di Laravel untuk menggunakan SQLite daripada MySQL, perbaharui file `.env` dengan hapus semua variable `DB_*` kecuali `DB_CONNECTION`, atur menjadi `sqlite`:

```ini
DB_CONNECTION=sqlite
```

## Install Laravel Breeze

Selanjutnya, kita gunakan starter-kit [Laravel Breeze](https://laravel.com/docs/starter-kits#laravel-breeze) yang sudah memuat semua fitur autentikasi Laravel, seperti login, registrasi, pengaturan ulang kata sandi, verifikasi email, dan konfirmasi kata sandi. Setelah diinstal, Kita juga dapat menyesuaikan komponen sesuai dengan kebutuhan.

Laravel Breeze menyediakan beberapa pilihan untuk view-nya, mulai dari Blade templates, atau [Vue](https://vuejs.org/) dan [React](https://reactjs.org/) dengan [Inertia](https://inertiajs.com/). Untuk tutorial ini, kita akan menggunakan Blade

Buka terminal di folder project `chirper` dan install dengan pilihan stack-nya Blade menggunakan command berikut:

```shell
composer require laravel/breeze --dev

php artisan breeze:install blade
```

Breeze akan meng-install dan sekaligus mengkonfigurasi front-end dependencies, kita hanya tinggal menjalankan Vite development server untuk seara otomatis meng-compile CSS kita dan refresh browser saat kita melakukan perubahan di Blade template:

```shell
npm run dev
```

Terakhir, buka lagi tab terminal lainnya di directory project `chirper` dan jalankan database migrations:

```shell
php artisan migrate
```

Jika kita refresh project aplikasi Laravel di browser, seharusnya bisa kita lihat ada link "Register" di bagian kanan-atas. Cobalah klik dan kita akan bisa melihat form registrasi yang disediakan oleh Laravel Breeze

<img src="/img/screenshots/register.png" alt="Laravel registration page" class="border rounded-lg shadow-lg dark:border-none" />

Coba daftar dan log in!

[Continue to start creating Chirps...](/chirper/creating-chirps)
