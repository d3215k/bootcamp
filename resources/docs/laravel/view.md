[TOC]

# <b>01.</b> View

View merupakan salah satu komponen penting dalam arsitektur MVC (Model-View-Controller) di Laravel. View bertanggung jawab untuk menampilkan data kepada pengguna dalam bentuk tampilan web. Di Laravel, View biasanya ditulis menggunakan file berbasis Blade (.blade.php). 

### Membuat View
Pertama, buat file view di direktori `resources/views`. Misalnya, kita ingin membuat view untuk menampilkan halaman selamat datang, nama file menggunakan `welcome.blade.php`

```html filename=resources/views/welcome.blade.php
<!DOCTYPE html>
<html>
<head>
    <title>Selamat Datang</title>
</head>
<body>
    <h1>Halo, Selamat Datang di Aplikasi Kami!</h1>
</body>
</html>
```

### Menggunakan View di Route
Selanjutnya, kita akan menggunakan view yang telah dibuat di dalam route. Buka file routes/web.php dan tambahkan kode berikut:
```php
use Illuminate\Support\Facades\Route;

Route::get('/', function () {
    return view('welcome');
});
```

Pada contoh di atas, ketika pengguna mengakses root URL (/), maka akan menampilkan view `welcome.blade.php`.

### Meneruskan Data ke View
Kita juga dapat meneruskan data dari controller ke view menggunakan fungsi view(). Contohnya, kita ingin menampilkan data nama dan usia dalam view:
```php filename=routes/web/php
use Illuminate\Support\Facades\Route;

Route::get('/', function () {
    $data = [
        'name' => 'John',
        'age' => 30,
    ];

    return view('welcome', $data);
});
```
```php filename=resources/views/welcome.blade.php
<!DOCTYPE html>
<html>
<head>
    <title>Selamat Datang</title>
</head>
<body>
    <h1>Halo, Selamat Datang, {{ $name }}!</h1>
    <p>Usia: {{ $age }}</p>
</body>
</html>
```

## Blade Templating
Blade menyediakan fitur templating yang memungkinkan Anda untuk membuat tampilan yang lebih dinamis. Contoh, buat layout sederhana yang digunakan oleh beberapa halaman:
```php filename=resources/views/layout.blade.php
<!DOCTYPE html>
<html>
<head>
    <title>@yield('title', 'Default Title')</title>
</head>
<body>
    @yield('content')
</body>
</html>
```
```php filename=resources/views/welcome.blade.php
@extends('layout')

@section('title', 'Selamat Datang')

@section('content')
    <h1>Halo, Selamat Datang, {{ $name }}!</h1>
    <p>Usia: {{ $age }}</p>
@endsection
```

## Blade Directive
Blade juga menyediakan beberapa directive yang sangat berguna, seperti `@if`, `@foreach`, `@forelse`, `@while`, dan yang lainnya.
```php
@if($count > 0)
    <p>Ada {{ $count }} data.</p>
@else
    <p>Tidak ada data.</p>
@endif

@foreach($users as $user)
    <p>{{ $user->name }}</p>
@endforeach
```

## Blade Component
Blade Component adalah fitur yang memungkinkan Anda untuk membuat komponen tampilan yang dapat digunakan kembali dalam berbagai bagian aplikasi Laravel Anda. Dengan menggunakan Blade Component, Anda dapat memisahkan dan mengorganisir kode tampilan Anda dengan lebih baik, meningkatkan reusable code, dan memudahkan dalam perawatan.

### Membuat Blade Component
Pertama, buat komponen tampilan baru dengan perintah artisan:
```
php artisan make:component Button
```

Perintah di atas akan membuat file Button.php di direktori app/View/Components, dan juga file blade view untuk komponen tersebut di direktori resources/views/components.

Definisikan Komponen
Buka file app/View/Components/Button.php dan definisikan komponen tersebut:

```php
<?php

namespace App\View\Components;

use Illuminate\View\Component;

class Button extends Component
{
    /**
     * Create a new component instance.
     *
     * @return void
     */
    public function __construct()
    {
        //
    }

    /**
     * Get the view / contents that represent the component.
     *
     * @return \Illuminate\Contracts\View\View|string
     */
    public function render()
    {
        return view('components.button');
    }
}
```

### Tulis Blade View untuk Komponen
Buka file resources/views/components/button.blade.php dan tulis tampilan untuk komponen Button:
```php
<button {{ $attributes->merge(['class' => 'bg-blue-500 text-white font-bold py-2 px-4 rounded']) }}>
    {{ $slot }}
</button>
```

### Menggunakan Blade Component
Anda dapat menggunakan komponen Button yang baru saja Anda buat di berbagai bagian tampilan aplikasi Anda.
```php
<x-button>Click Me!</x-button>
<x-button class="bg-red-500">Delete</x-button>
```

### Menerima Parameter di Komponen
Anda juga dapat mengirimkan data dan parameter ke komponen untuk digunakan dalam tampilan.

Misalnya, jika Anda ingin menambahkan warna latar belakang dan teks pada tombol:
```php
// app/View/Components/Button.php
public $background;
public $color;

public function __construct($background = 'bg-blue-500', $color = 'text-white')
{
    $this->background = $background;
    $this->color = $color;
}

// resources/views/components/button.blade.php
<button {{ $attributes->merge(['class' => "$background $color font-bold py-2 px-4 rounded"]) }}>
    {{ $slot }}
</button>
```

Kemudian Anda bisa menggunakan komponen dengan parameter seperti ini:
```php
<x-button background="bg-red-500" color="text-white">Delete</x-button>
```

Dengan Blade Component, Anda dapat menciptakan komponen tampilan yang dapat digunakan kembali dengan mudah dan fleksibel di berbagai bagian aplikasi Anda. Hal ini membantu mempercepat pengembangan, meningkatkan efisiensi, dan meningkatkan kualitas kode tampilan Anda.
