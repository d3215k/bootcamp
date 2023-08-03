# Laravel Bootcamp

## Requirement

Menggunakan Framework PHP Laravel 10.\*, maka minimum server system requirement diantaranya:

-   PHP >= 8.1
-   Composer 2.2.0

dan lebih lengkapnya bisa dilihat di halaman :
https://laravel.com/docs/10.x/deployment

## Instalasi

Install Dependencies

```bash
composer install
```

Copy dan atur koneksi database di .env

```bash
cp .env.example .env
```

Generate App Key

```bash
php artisan key:generate
```

Jalankan Aplikasi

```bash
php artisan serve
```
