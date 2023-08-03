[TOC]

# <b>02.</b> Membuat Chirps

Sekarang kita sudah siap untuk membangun aplikasi! Mulai dengan menambah fitur supaya user bisa menambahkan pesan singkat yang kita sebut _Chirps_.

## Models, migrations, and controllers

Untuk fitur tambah chirps, kita perlu membuat models, migrations, dan controllers. Kita jelajahi masing-masing konsep ini sedikit lebih dalam:

-   [Models](https://laravel.com/docs/eloquent) menyediakan interface yang powerful dan menyenangkan bagi kita untuk berinteraksi dengan tabel di database Anda.
-   [Migrations](https://laravel.com/docs/migrations) memungkinkan kita untuk dengan mudah membuat dan memodifikasi tabel di database. Ini akan memastikan bahwa struktur database yang sama ada di mana pun aplikasi berjalan.
-   [Controllers](https://laravel.com/docs/controllers) bertanggung jawab untuk memproses request yang diajukan ke aplikasi dan mengembalikan response.

Hampir setiap fitur yang kita buat akan melibatkan semua bagian ini yang bekerja bersama secara harmonis, untungnya ada perintah `artisan make:model` yang dapat mempermudah kita membuat semuanya sekaligus.

Kita buat model, migrations, dan resource controller untuk aplikasi Chirps kita dengan command berikut:

```shell
php artisan make:model -mrc Chirp
```

> **Note**
> Kita bisa lihat semua pilihan yang tersedia, dengan menjalankan perintah `php artisan make:model --help`

Perintah ini akan membuatkan kita tiga file berikut:

-   `app/Models/Chirp.php` - Eloquent model.
-   `database/migrations/<timestamp>_create_chirps_table.php` - Migration database yang akan membuat tabel database.
-   `app/Http/Controller/ChirpController.php` - Pengontrol HTTP yang akan menerima request dan mengembalikan respons.

## Routing

Kita perlu membuat URLS untuk controller. Bisa kita lakukan dengan menambahkan "routes", yang diatur pada directory `routes` project kita. Karena yang akan kita gunakan adalah resource controller, kita dapat menggunakan satu statement `Route::resource()` untuk mendefinisikan semua routes yang mengikuti struktur URL konvensional.

Untuk memulainya, kita akan mengaktifkan dua routes :

-   route `index` akan menampilkan form dan daftar Chiprs.
-   route `store` akan digunakan untuk menyimpan Chirps baru.

Kita juga menambahkan dua [middleware](https://laravel.com/docs/middleware):

-   Middleware `auth` memastikan hanya user yang sudah log-in yang bisa akses.
-   Middleware `verified` digunakan jika kita ingin mengaktifkan  [email verification](https://laravel.com/docs/verification).

```php filename=routes/web.php
<?php

use App\Http\Controllers\ChirpController;// [tl! add]
use Illuminate\Support\Facades\Route;
// [tl! collapse:start]
/*
|--------------------------------------------------------------------------
| Web Routes
|--------------------------------------------------------------------------
|
| Here is where you can register web routes for your application. These
| routes are loaded by the RouteServiceProvider within a group which
| contains the "web" middleware group. Now create something great!
|
*/

Route::get('/', function () {
    return view('welcome');
});
// [tl! collapse:end]
Route::get('/dashboard', function () {
    return view('dashboard');
})->middleware(['auth', 'verified'])->name('dashboard');

Route::resource('chirps', ChirpController::class)// [tl! add:start]
    ->only(['index', 'store'])
    ->middleware(['auth', 'verified']);// [tl! add:end]

require __DIR__.'/auth.php';
```

Hal ini akan membuat routes berikut:

| Verb | URI       | Action | Route Name   |
| ---- | --------- | ------ | ------------ |
| GET  | `/chirps` | index  | chirps.index |
| POST | `/chirps` | store  | chirps.store |

> **Note**
> Untuk melihat semua routes yang ada di aplikasi, kita dapat menjalankan command `php artisan route:list`

Kita test routes dan controller-nya dengan coba mengembalikan pesan test dari method `index` di class `ChirpController`:

```php filename=app/Http/Controllers/ChirpController.php
<?php
// [tl! collapse:start]
namespace App\Http\Controllers;

use App\Models\Chirp;
use Illuminate\Http\Request; // [tl! collapse:end]
use Illuminate\Http\Response; // [tl! 1 add]

class ChirpController extends Controller
{
    /**
     * Display a listing of the resource.
     */
    public function index()
    public function index(): Response // [tl! remove:-1,1 add]
    {
        //
        return response('Hai Laravel!');// [tl! remove:-1,1 add]
    }
    // [tl! collapse:start]
    /**
     * Show the form for creating a new resource.
     */
    public function create()
    {
        //
    }

    /**
     * Store a newly created resource in storage.
     */
    public function store(Request $request)
    {
        //
    }

    /**
     * Display the specified resource.
     */
    public function show(Chirp $chirp)
    {
        //
    }

    /**
     * Show the form for editing the specified resource.
     */
    public function edit(Chirp $chirp)
    {
        //
    }

    /**
     * Update the specified resource in storage.
     */
    public function update(Request $request, Chirp $chirp)
    {
        //
    }

    /**
     * Remove the specified resource from storage.
     */
    public function destroy(Chirp $chirp)
    {
        //
    }
    // [tl! collapse:end]
}
```

Jika sebelumnya sudah login, seharusnya bisa kita lihat pesannya dengan buka halaman [http://localhost:8000/chirps](http://localhost:8000/chirps)

## Blade

Masih belum ada yang menarik? Ok, kita lanjut coba ubah method `index` di class `ChirpController` untuk me-render sebuah Blade view:

```php filename=app/Http/Controllers/ChirpController.php
<?php
// [tl! collapse:start]

namespace App\Http\Controllers;

use App\Models\Chirp;
use Illuminate\Http\Request;
use Illuminate\Http\Response;// [tl! collapse:end]
use Illuminate\View\View;// [tl! add]

class ChirpController extends Controller
{
    /**
     * Display a listing of the resource.
     */
    public function index(): Response// [tl! remove]
    public function index(): View// [tl! add]
    {
        return response('Hello, World!');// [tl! remove]
        return view('chirps.index');// [tl! add]
    }
    // [tl! collapse:start]
    /**
     * Show the form for creating a new resource.
     */
    public function create()
    {
        //
    }

    /**
     * Store a newly created resource in storage.
     */
    public function store(Request $request)
    {
        //
    }

    /**
     * Display the specified resource.
     */
    public function show(Chirp $chirp)
    {
        //
    }

    /**
     * Show the form for editing the specified resource.
     */
    public function edit(Chirp $chirp)
    {
        //
    }

    /**
     * Update the specified resource in storage.
     */
    public function update(Request $request, Chirp $chirp)
    {
        //
    }

    /**
     * Remove the specified resource from storage.
     */
    public function destroy(Chirp $chirp)
    {
        //
    }
    // [tl! collapse:end]
}
```

Buat juga Blade view yang memuat form untuk membuat Chirps baru:

```blade filename=resources/views/chirps/index.blade.php
<x-app-layout>
    <div class="max-w-2xl p-4 mx-auto sm:p-6 lg:p-8">
        <form method="POST" action="{{ route('chirps.store') }}">
            @csrf
            <textarea
                name="message"
                placeholder="{{ __('What\'s on your mind?') }}"
                class="block w-full border-gray-300 rounded-md shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50"
            >{{ old('message') }}</textarea>
            <x-input-error :messages="$errors->get('message')" class="mt-2" />
            <x-primary-button class="mt-4">{{ __('Chirp') }}</x-primary-button>
        </form>
    </div>
</x-app-layout>
```

Itu dia! sekarang coba Refresh halaman di browser untuk lihat form yang di-render bersama dengan default layout yang disediakan oleh Breeze!

<img src="/img/screenshots/chirp-form.png" alt="Chirp form" class="border rounded-lg shadow-lg dark:border-none" />

Jika tampilnya tidak seperti yang di atas, coba untuk stop dan start Vite development server dari Tailwindnya untuk mendeteksi class CSS di file baru yang baru saja kita buat.

Sekarang, perubahan yang kita buat di Blade template akan secara otomatis langsung tampil di browser bila kita menjalakan Vite development server-nya dengan menjalankan `npm run dev`.

## Navigation menu

Mari luangkan waktu sejenak untuk menambahkan tautan ke menu navigasi yang disediakan oleh Breeze.

Ubah di component `navigation.blade.php` yang disediakan oleh Breeze untuk menambah menu di screen desktop:

```blade filename=resources/views/layouts/navigation.blade.php
<div class="hidden space-x-8 sm:-my-px sm:ml-10 sm:flex">
    <x-nav-link :href="route('dashboard')" :active="request()->routeIs('dashboard')">
        {{ __('Dashboard') }}
    </x-nav-link>
    <x-nav-link :href="route('chirps.index')" :active="request()->routeIs('chirps.index')"><!-- [tl! add:start] -->
        {{ __('Chirps') }}
    </x-nav-link><!-- [tl! add:end] -->
</div>
```

Dan juga untuk screen mobile-nya:

```blade filename=resources/views/layouts/navigation.blade.php
<div class="pt-2 pb-3 space-y-1">
    <x-responsive-nav-link :href="route('dashboard')" :active="request()->routeIs('dashboard')">
        {{ __('Dashboard') }}
    </x-responsive-nav-link>
    <x-responsive-nav-link :href="route('chirps.index')" :active="request()->routeIs('chirps.index')"><!-- [tl! add:start] -->
        {{ __('Chirps') }}
    </x-responsive-nav-link><!-- [tl! add:end] -->
</div>
```

## Menyimpan Chirp

Form sudah kita atur untuk mengirim pesannya ke route `chirps.store` yang sebelumnya sudah kita buat. Kita ubah method `store` di class `ChirpController` untuk mem-validasi data dan membuatkan kita Chirp baru:

```php filename=app/Http/Controllers/ChirpController.php
<?php
// [tl! collapse:start]
namespace App\Http\Controllers;

use App\Models\Chirp;// [tl! collapse:end]
use Illuminate\Http\RedirectResponse;// [tl! add:0,1]
use Illuminate\Http\Request;
use Illuminate\Http\Response;
use Illuminate\View\View;

class ChirpController extends Controller
{
    // [tl! collapse:start]
    /**
     * Display a listing of the resource.
     */
    public function index(): View
    {
        return view('chirps.index');
    }

    /**
     * Show the form for creating a new resource.
     */
    public function create()
    {
        //
    }
    // [tl! collapse:end]
    /**
     * Store a newly created resource in storage.
     */
    public function store(Request $request)// [tl! remove]
    public function store(Request $request): RedirectResponse// [tl! add]
    {
        //
        $validated = $request->validate([// [tl! remove:-1,1 add:start]
            'message' => 'required|string|max:255',
        ]);

        $request->user()->chirps()->create($validated);

        return redirect(route('chirps.index'));// [tl! add:end]
    }
    // [tl! collapse:start]
    /**
     * Display the specified resource.
     */
    public function show(Chirp $chirp)
    {
        //
    }

    /**
     * Show the form for editing the specified resource.
     */
    public function edit(Chirp $chirp)
    {
        //
    }

    /**
     * Update the specified resource in storage.
     */
    public function update(Request $request, Chirp $chirp)
    {
        //
    }

    /**
     * Remove the specified resource from storage.
     */
    public function destroy(Chirp $chirp)
    {
        //
    }
    // [tl! collapse:end]
}
```

Kita menggunakan fitur validasi Laravel yang sangat powerful untuk memastikan bahwa pengguna memberikan pesan dan tidak akan melebihi batas 255 karakter dari kolom database yang akan kita buat.

Kita kemudian membuat record baru yang mana pemiliknya adalah user yang sedang logged in dengan memanfaatkan relasi `chirps`. Kita akan definiskan relasi-nya nanti setelah ini.

Akhirnya, kita tambahkan respon redirect untuk membawa user kembali ke route `chirps.index`.

## Membuat relationship

Kalau kita lihat di langkah sebelumnya, kita memanggil method `chirps` pada objek `$request->user()`. Kita perlu untuk membuat method ini di model `User` untuk membuat definisi relasi ["has many"](https://laravel.com/docs/eloquent-relationships#one-to-many)

```php filename=app/Models/User.php
<?php
// [tl! collapse:start]
namespace App\Models;

// use Illuminate\Contracts\Auth\MustVerifyEmail;
use Illuminate\Database\Eloquent\Factories\HasFactory;// [tl! collapse:end]
use Illuminate\Database\Eloquent\Relations\HasMany;// [tl! add]
use Illuminate\Foundation\Auth\User as Authenticatable;
use Illuminate\Notifications\Notifiable;
use Laravel\Sanctum\HasApiTokens;

class User extends Authenticatable
{
    // [tl! collapse:start]
    use HasApiTokens, HasFactory, Notifiable;

    /**
     * The attributes that are mass assignable.
     *
     * @var array<int, string>
     */
    protected $fillable = [
        'name',
        'email',
        'password',
    ];

    /**
     * The attributes that should be hidden for serialization.
     *
     * @var array<int, string>
     */
    protected $hidden = [
        'password',
        'remember_token',
    ];

    /**
     * The attributes that should be cast.
     *
     * @var array<string, string>
     */
    protected $casts = [
        'email_verified_at' => 'datetime',
    ];
    // [tl! collapse:end]
    public function chirps(): HasMany// [tl! add:start]
    {
        return $this->hasMany(Chirp::class);
    }// [tl! add:end]
}
```

> **Note**
> Laravel menyediakan berbagai jenis relasi model yang bisa baca selengkapnya di halaman dokumentasi [Eloquent Relationships](https://laravel.com/docs/eloquent-relationships).

## Mass assignment protection

Meneruskan semua data dari request ke model tentu sangat beresiko. Bayangkan jika kita punya halaman yang user dapat edit profile mereka. Jika kita ambil semua request ke model, kemudian user dapat edit _semua_ kolom sesuka mereka, seperti misalnya kolom `is_admin`. Ini kita menyebutnya [mass assignment vulnerability](https://en.wikipedia.org/wiki/Mass_assignment_vulnerability).

Laravel membantu kita menjaga dari kejadian yang tidak disengaja seperti ini dengan mem-blokir mass assignment secara default. Mass assignment juga sangat membuat kita nyaman, karena kita tidak harus menetapkan setiap atribut satu per satu. Kita dapat mengaktifkan mass assignment untuk attribute yang aman dengan menandai mereka sebagai "fillable".

Kita tambahkan properti `$fillable` ke model `Chirp` untuk mengaktifkan mass-assignment untuk attribute `message`:

```php filename=app/Models/Chirp.php
<?php
// [tl! collapse:start]
namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;
// [tl! collapse:end]
class Chirp extends Model
{
    // [tl! collapse:start]
    use HasFactory;
    // [tl! collapse:end]
    protected $fillable = [// [tl! add:start]
        'message',
    ];// [tl! add:end]
}
```

Baca lebih lengkap mengenai Laravel mass assignment di halaman [dokumentasi](https://laravel.com/docs/eloquent#mass-assignment).

## Update file migration

Yang masih belum kita buat adalah kolom tambahan di database kita untuk menyimpan relasi antara `Chirp` dan `User` dan message-nya sendiri. Masih ingat database migration yang sebelumnya pernah kita buat? Sekarang waktunya buat file itu dan tambahkan beberapa kolom tambahannya:

```php filename=databases/migration/TIMESTAMP_create_chirps_table.php
<?php
// [tl! collapse:start]
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;
// [tl! collapse:end]
return new class extends Migration
{
    /**
     * Run the migrations.
     */
    public function up(): void
    {
        Schema::create('chirps', function (Blueprint $table) {
            $table->id();
            $table->foreignId('user_id')->constrained()->cascadeOnDelete();// [tl! add]
            $table->string('message');// [tl! add]
            $table->timestamps();
        });
    }
    // [tl! collapse:start]
    /**
     * Reverse the migrations.
     */
    public function down(): void
    {
        Schema::dropIfExists('chirps');
    }
    // [tl! collapse:end]
};
```

Kita belum menjalankan migrasi database sejak migration ini dibuat, jadi langsung bisa kita jalankan sekarang dengan:

```shell
php artisan migrate
```

> **Warning**
> Setiap migrasi database hanya akan dijalankan satu kali. Untuk membuat perubahan tambahan pada tabel, Anda harus membuat migrasi lain. Selama pengembangan, Anda mungkin ingin memperbarui migrasi yang belum digunakan dan membangun kembali database Anda dari awal menggunakan perintah `php artisan migrate:fresh`.

## Testing it out

Sekarang kita sudah bisa mengirimkan sebuah Chirp menggunakan form yang baru saja kita buat! Tapi untuk sekarang, kita masih belum bisa lihat hasilnya karena Chirp yang sudah dibuat belum kita buat tampil di halaman.

<img src="/img/screenshots/chirp-form-filled.png" alt="Chirp form" class="border rounded-lg shadow-lg dark:border-none" />

Coba kosongkan kota isian pesan-nya, atau masukkan lebih dari 255 karakter, maka kita bisa lihat kegunaan dari validasi.

### Artisan Tinker

Sekarang waktu yang tepat untuk belajar mengenai [Artisan Tinker](https://laravel.com/docs/artisan#tinker), sebuah _REPL_ ([Read-eval-print loop](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop)) yang menjadi tempat kita dapat mengeksekusi kode PHP di aplikasi Laravel kita.

di terminal, mulai sesi baru tinker dengan perintah:

```shell
php artisan tinker
```

Selanjutnya, jalankan kode berikut untuk menampilkan Chirps yang ada di database:

```
\App\Model\Chirp::all();
```

```
=> Illuminate\Database\Eloquent\Collection {#4512
     all: [
       App\Models\Chirp {#4514
         id: 1,
         user_id: 1,
         message: "I'm building Chirper with Laravel!",
         created_at: "2022-08-24 13:37:00",
         updated_at: "2022-08-24 13:37:00",
       },
     ],
   }
```

Kita bisa keluar dari Tinker dengan menggunakan perintah `exit`, atau dengan menekan tombol <kbd>Ctrl</kbd> + <kbd>c</kbd>.

[Lanjut untuk mulai menampilkan Chirps...](/chirper/showing-chirps)
