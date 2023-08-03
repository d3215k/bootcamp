[TOC]

# <b>10.</b> Request & Response

Request dan Response adalah dua aspek penting dalam pengembangan aplikasi web di Laravel. Request digunakan untuk mengambil data yang dikirim oleh pengguna melalui form atau parameter URL. Response digunakan untuk mengirimkan balasan dari server kembali kepada pengguna. Berikut adalah penjelasan tentang Request dan Response di Laravel beserta contoh penggunaannya:

## Request
#### Menerima Data dari Form
Untuk mengambil data yang dikirim melalui form POST, Anda dapat menggunakan objek Request pada controller. Pastikan Anda sudah mengimpor class Request di bagian atas controller.
```php
use Illuminate\Http\Request;

public function store(Request $request)
{
    $name = $request->input('name');
    $email = $request->input('email');
    
    // Proses data lebih lanjut atau simpan ke database
}
```

#### Menerima Data dari Parameter URL
Jika Anda ingin mengambil data dari parameter URL (misalnya menggunakan GET method), Anda juga dapat menggunakan objek Request pada controller.
```php
use Illuminate\Http\Request;

public function show(Request $request, $id)
{
    $name = $request->query('name');
    // atau
    $name = $request->input('name');

    // Lakukan operasi berdasarkan $id dan $name
}
```

## Response di Laravel
#### Mengirimkan Tampilan (View)
Untuk mengirimkan tampilan (view) sebagai response, Anda dapat menggunakan helper view(). Tampilan ini akan dikompilasi dengan Blade, jika menggunakan ekstensi .blade.php.
```php
public function index()
{
    $data = ['name' => 'John', 'age' => 30];
    return view('users.index', $data);
}
```

#### Mengirimkan Data dalam Bentuk JSON
Jika Anda ingin mengirimkan data dalam bentuk JSON sebagai response (misalnya untuk API), Anda dapat menggunakan method json().
```php
public function apiData()
{
    $data = ['name' => 'John', 'age' => 30];
    return response()->json($data);
}
```

#### Mengirimkan Response dengan Header Kustom
Anda dapat menambahkan header kustom pada response menggunakan method header().
```php
public function downloadFile()
{
    $file = public_path('files/sample.pdf');
    return response()->download($file, 'sample.pdf', ['Content-Type' => 'application/pdf']);
}
```

#### Mengirimkan Response dengan Kode Status Khusus
Anda juga dapat mengatur kode status khusus pada response menggunakan method status().
```php
public function notFound()
{
    return response('Data not found', 404);
}
```

Dengan menggunakan Request dan Response di Laravel, Anda dapat dengan mudah mengambil data dari pengguna dan memberikan respons yang sesuai kepada mereka. Request membantu Anda dalam mengelola data masukan dari pengguna, sedangkan Response memungkinkan Anda untuk memberikan respons dalam berbagai bentuk seperti tampilan (view) atau data JSON.

[Lanjut ke Middleware...](/laravel/middleware)
