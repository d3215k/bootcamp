[TOC]

# <b>13.</b> Validasi Data
Validasi data adalah langkah penting dalam pengembangan aplikasi web untuk memastikan bahwa data yang dimasukkan oleh pengguna sesuai dengan persyaratan tertentu sebelum disimpan atau diproses lebih lanjut. Laravel menyediakan fitur validasi yang kuat dan mudah digunakan.

## Membuat Validasi
Validasi dilakukan pada Controller atau Form Request. Di sini kita akan menggunakan Form Request untuk mengatur validasi.

#### Membuat Form Request
Untuk membuat Form Request, gunakan perintah artisan:
```
php artisan make:request StoreUserDataRequest
```

Perintah di atas akan membuat file `StoreUserDataRequest.php` di direktori `app/Http/Requests`.

#### Definisikan Aturan Validasi
Buka file StoreUserDataRequest.php dan tentukan aturan validasi pada method `rules()`.
```php
public function rules()
{
    return [
        'name' => 'required|string|max:255',
        'email' => 'required|email|unique:users,email',
        'password' => 'required|string|min:8|confirmed',
    ];
}
```

Pada contoh di atas, kita mendefinisikan beberapa aturan validasi untuk data yang akan dimasukkan pengguna.

## Menggunakan Validasi
#### Dalam Controller
Di dalam Controller, gunakan Form Request yang sudah dibuat untuk melakukan validasi data sebelum menyimpan atau memprosesnya.
```php
use App\Http\Requests\StoreUserDataRequest;

public function store(StoreUserDataRequest $request)
{
    // Data sudah valid, lanjutkan menyimpan atau memprosesnya
}
```

#### Dalam Form
Jika Anda ingin menampilkan pesan error untuk validasi di dalam form, Anda dapat menggunakan helper `@error` dalam template Blade.
```php
<form action="/user" method="post">
    @csrf
    <input type="text" name="name" value="{{ old('name') }}">
    @error('name')
        <div>{{ $message }}</div>
    @enderror

    <input type="email" name="email" value="{{ old('email') }}">
    @error('email')
        <div>{{ $message }}</div>
    @enderror

    <input type="password" name="password">
    @error('password')
        <div>{{ $message }}</div>
    @enderror

    <input type="password" name="password_confirmation">
    @error('password_confirmation')
        <div>{{ $message }}</div>
    @enderror

    <button type="submit">Simpan</button>
</form>
```

## Menggunakan Custom Pesan Error
Anda juga dapat menggunakan pesan error kustom untuk setiap aturan validasi. Buka file `StoreUserDataRequest.php` dan tambahkan method `messages()`.
```php
public function messages()
{
    return [
        'name.required' => 'Nama harus diisi.',
        'email.required' => 'Email harus diisi.',
        'email.email' => 'Format email tidak valid.',
        'email.unique' => 'Email sudah digunakan.',
        'password.required' => 'Password harus diisi.',
        'password.min' => 'Password minimal 8 karakter.',
        'password.confirmed' => 'Konfirmasi password tidak sesuai.',
    ];
}
```

Dengan mengikuti langkah-langkah di atas, Anda dapat dengan mudah melakukan validasi data di Laravel untuk memastikan bahwa data yang dimasukkan oleh pengguna sesuai dengan persyaratan yang Anda tentukan. Fitur validasi di Laravel membantu Anda dalam memastikan kualitas data dan mencegah kesalahan saat pengguna memasukkan informasi.

[Lanjut ke Case Study : Build Chirper...](/chirper/installation)
