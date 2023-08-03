[TOC]

# <b>02.</b> Controller
Controller adalah komponen penting dalam arsitektur MVC (Model-View-Controller) di Laravel. Controller bertanggung jawab untuk menerima permintaan dari pengguna, memproses data dari Model, dan menampilkan tampilan (View) kepada pengguna.

### Membuat Controller
Pertama, buat controller baru dengan perintah artisan:
```
php artisan make:controller UserController
```

Perintah di atas akan membuat file UserController.php di direktori app/Http/Controllers.

### Definisikan Controller
Buka file UserController.php dan definisikan controller dengan menurunkannya dari Controller bawaan Laravel.
```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class UserController extends Controller
{
    //
}
```

### Menambahkan Method
Tambahkan method dalam controller untuk mengelola permintaan dari pengguna. Misalnya, tambahkan method index() untuk menampilkan daftar pengguna:
```php
public function index()
{
    // Proses data dari Model jika diperlukan
    $users = User::all();

    // Tampilkan view dengan data pengguna
    return view('users.index', compact('users'));
}
```

### Route ke Controller
Buka file routes/web.php dan route permintaan ke controller. Misalnya, kita akan route permintaan ke method index() dalam UserController:
```php
use App\Http\Controllers\UserController;

Route::get('/users', [UserController::class, 'index']);
```

Sekarang ketika pengguna mengakses /users, permintaan akan diarahkan ke method index() dalam UserController.


## Restful Resource Controller
Selain controller biasa, Laravel juga menyediakan Restful Resource Controller yang memudahkan dalam mengelola operasi CRUD (Create, Read, Update, Delete) pada Model Anda. Berikut adalah langkah-langkah untuk menggunakan Restful Resource Controller di Laravel:
#### Membuat Restful Resource Controller
Pertama, buat Restful Resource Controller dengan perintah artisan:
```
php artisan make:controller UserController --resource
```

Perintah di atas akan membuat file UserController.php di direktori app/Http/Controllers dengan implementasi Restful Resource Controller.

#### Definisikan Resource Controller
Buka file UserController.php dan pastikan bahwa controller ini menggunakan use Illuminate\Routing\Controller; sebagai parent class. Controller ini akan memiliki beberapa method bawaan seperti `index()`, `create()`, `store()`, `show()`, `edit()`, `update()`, dan `destroy()`.

#### Route ke Resource Controller
Buka file `routes/web.php` dan route permintaan ke Restful Resource Controller. Misalnya, kita akan route permintaan ke UserController:
```php
use App\Http\Controllers\UserController;

Route::resource('users', UserController::class);
```

Sekarang Anda telah terhubung dengan keseluruhan Restful Resource Controller. Berikut adalah daftar route yang dapat diakses:

- `GET /users` : Menampilkan daftar pengguna (index).
- `GET /users/create` : Menampilkan form untuk membuat pengguna baru (create).
- `POST /users` : Menyimpan data pengguna baru (store).
- `GET /users/{id}` : Menampilkan detail pengguna tertentu (show).
- `GET /users/{id}/edit` : Menampilkan form untuk mengedit pengguna (edit).
- `PUT/PATCH /users/{id}` : Memperbarui data pengguna tertentu (update).
- `DELETE /users/{id}` : Menghapus data pengguna tertentu (destroy).

Dengan menggunakan Restful Resource Controller, Anda dapat mengatur operasi CRUD pada Model Anda dengan lebih mudah dan efisien. Controller ini membantu dalam mengatur route dengan lebih terstruktur, meningkatkan kinerja aplikasi, dan memisahkan logika bisnis dari kode tampilan Anda.

## Invokable Controller
Invokable Controller adalah tipe controller khusus di Laravel yang memungkinkan Anda untuk menggunakan controller sebagai sebuah fungsi yang dapat dipanggil langsung, tanpa harus mendefinisikan method tertentu seperti pada controller biasa. Dengan menggunakan Invokable Controller, Anda dapat membuat kode lebih sederhana dan mudah dibaca. Berikut adalah langkah-langkah untuk menggunakan Invokable Controller di Laravel:
#### Membuat Invokable Controller
Pertama, buat Invokable Controller dengan perintah artisan:
```
php artisan make:controller UserController --invokable
```

Perintah di atas akan membuat file `UserController.php` di direktori `app/Http/Controllers` dengan implementasi Invokable Controller.

#### Definisikan Invokable Controller
Buka file UserController.php dan ubah parent class dari Controller menjadi Illuminate\Routing\Controller dan implementasinya menjadi `__invoke()`.

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class UserController extends Controller
{
    public function __invoke()
    {
        // Kode untuk dipanggil saat controller di-invoked
        return view('users.index');
    }
}
```

#### Route ke Invokable Controller
Buka file `routes/web.php` dan route permintaan ke Invokable Controller. Misalnya, kita akan route permintaan ke UserController:
```php
use App\Http\Controllers\UserController;

Route::get('/users', UserController::class);
```

Sekarang ketika pengguna mengakses /users, permintaan akan diarahkan langsung ke `__invoke()` method dalam UserController.

#### Menerima Parameter (Opsional)
Jika Anda ingin menerima parameter dalam Invokable Controller, cukup tambahkan parameter pada `__invoke()` method.

```php
class UserController extends Controller
{
    public function __invoke($id)
    {
        // Kode untuk dipanggil saat controller di-invoked dengan parameter id
        return view('users.show', ['id' => $id]);
    }
}
```
