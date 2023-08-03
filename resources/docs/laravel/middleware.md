[TOC]

# <b>01.</b> Middleware

Middleware adalah fitur yang sangat kuat di Laravel yang memungkinkan Anda untuk melakukan tindakan sebelum atau setelah permintaan (request) diproses oleh controller. Middleware membantu Anda untuk memfilter, mengotentikasi, atau melakukan tindakan lainnya terhadap permintaan sebelum mencapai controller. 

Middleware adalah lapisan antara permintaan (request) dan controller di Laravel. Setiap permintaan yang masuk melewati satu atau beberapa middleware sebelum mencapai tujuan akhir, yaitu controller. Middleware dapat melakukan berbagai tindakan seperti verifikasi otentikasi, mengatur header, logging, dan lain-lain.

## Membuat Middleware
#### Membuat Middleware Baru
Untuk membuat middleware baru, Anda dapat menggunakan perintah artisan:
```
php artisan make:middleware MyMiddleware
```

Perintah di atas akan membuat file MyMiddleware.php di direktori app/Http/Middleware.

#### Mengimplementasikan Middleware
Buka file MyMiddleware.php dan implementasikan logic yang diinginkan. Middleware harus mengimplementasikan method handle yang akan dijalankan untuk setiap permintaan.
```php
<?php

namespace App\Http\Middleware;

use Closure;

class MyMiddleware
{
    public function handle($request, Closure $next)
    {
        // Lakukan tindakan sebelum permintaan mencapai controller
        
        $response = $next($request);
        
        // Lakukan tindakan setelah permintaan diproses oleh controller
        
        return $response;
    }
}
```

## Menggunakan Middleware
#### Registrasi Middleware
Anda harus mendaftarkan middleware di dalam file app/Http/Kernel.php agar dapat digunakan di aplikasi.
```php
protected $middleware = [
    //...
    \App\Http\Middleware\MyMiddleware::class,
];
```

Anda juga dapat mendaftarkan middleware dalam grup middleware agar diterapkan hanya pada route tertentu.

```php
protected $middlewareGroups = [
    'web' => [
        //...
        \App\Http\Middleware\MyMiddleware::class,
    ],
];
```

#### Menggunakan Middleware pada Route
Anda dapat menambahkan middleware pada route tertentu atau grup route dengan cara sebagai berikut:

```php
Route::get('/user', function () {
    //
})->middleware('MyMiddleware');
```

atau pada group route:
```php
Route::middleware(['auth', 'MyMiddleware'])->group(function () {
    // Route yang menggunakan middleware 'auth' dan 'MyMiddleware'
});
```

## Middleware Built-in di Laravel
Laravel menyediakan beberapa middleware built-in yang sangat bermanfaat, seperti:

- `auth`: Untuk mengotentikasi pengguna sebelum akses diberikan.
- `guest`: Memastikan bahwa pengguna belum masuk sebelum mengakses route tertentu.
- `throttle`: Untuk membatasi jumlah permintaan yang dapat dilakukan oleh pengguna dalam waktu tertentu.

Anda dapat menggunakan middleware built-in ini dengan mudah dengan menyertakan nama middleware saat mendefinisikan route.

```php
Route::get('/profile', function () {
    // Route ini memerlukan autentikasi, pengguna harus masuk sebelum mengakses halaman profil
})->middleware('auth');
```

Dengan menggunakan middleware di Laravel, Anda dapat mengontrol dan melindungi route serta mengatur tindakan yang harus dijalankan sebelum atau setelah permintaan mencapai controller. Middleware membantu Anda dalam meningkatkan keamanan, kehandalan, dan efisiensi aplikasi Anda dengan memisahkan tugas-tugas tertentu menjadi lapisan terpisah.
