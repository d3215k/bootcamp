[TOC]

# <b>04.</b> Edit Chirps

Kita tambahkan fitur untuk edit Chirps!

## Routing

Pertama kita ubah file routes untuk mengaktifkan `chirps.edit` dan `chirps.update` dari resource controller kita. route `chirps.edit` akan menampilkan form untuk edit Chirp, sementara route `chirps.update` akan menerima data dari form dan update model:

```php filename=routes/web.php
<?php
// [tl! collapse:start]
use App\Http\Controllers\ChirpController;
use Illuminate\Support\Facades\Route;

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

Route::get('/dashboard', function () {
    return view('dashboard');
})->middleware(['auth', 'verified'])->name('dashboard');
// [tl! collapse:end]
Route::resource('chirps', ChirpController::class)
    ->only(['index', 'store'])// [tl! remove]
    ->only(['index', 'store', 'edit', 'update'])// [tl! add]
    ->middleware(['auth', 'verified']);
// [tl! collapse:start]
require __DIR__.'/auth.php';
// [tl! collapse:end]
```

tabel route untuk controller ini sekarang akan terlihat seperti berikut:

| Verb      | URI                    | Action | Route Name    |
| --------- | ---------------------- | ------ | ------------- |
| GET       | `/chirps`              | index  | chirps.index  |
| POST      | `/chirps`              | store  | chirps.store  |
| GET       | `/chirps/{chirp}/edit` | edit   | chirps.edit   |
| PUT/PATCH | `/chirps/{chirp}`      | update | chirps.update |

## Menautkan ke halaman edit

Selanjutnya, hubungkan route `chirps.edit`. Kita akan menggunakan component `x-dropdown` yang juga sudah disediakan Breeze, yang mana ini hanya akan kita tampilkan ke pembuat Chirp-nya saja. Kita juga akan menampilkan indikator jika sebuah Chirp sudah di-edit dengan membandingkan kolom tanggal `created_at` dan  `updated-at`:

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

        <div class="mt-6 bg-white divide-y rounded-lg shadow-sm">
            @foreach ($chirps as $chirp)
                <div class="flex p-6 space-x-2">
                    <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 text-gray-600 -scale-x-100" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z" />
                    </svg>
                    <div class="flex-1">
                        <div class="flex items-center justify-between">
                            <div>
                                <span class="text-gray-800">{{ $chirp->user->name }}</span>
                                <small class="ml-2 text-sm text-gray-600">{{ $chirp->created_at->format('j M Y, g:i a') }}</small>
                                @unless ($chirp->created_at->eq($chirp->updated_at))<!-- [tl! add:start] -->
                                    <small class="text-sm text-gray-600"> &middot; {{ __('edited') }}</small>
                                @endunless<!-- [tl! add:end] -->
                            </div>
                            @if ($chirp->user->is(auth()->user()))<!-- [tl! add:start] -->
                                <x-dropdown>
                                    <x-slot name="trigger">
                                        <button>
                                            <svg xmlns="http://www.w3.org/2000/svg" class="w-4 h-4 text-gray-400" viewBox="0 0 20 20" fill="currentColor">
                                                <path d="M6 10a2 2 0 11-4 0 2 2 0 014 0zM12 10a2 2 0 11-4 0 2 2 0 014 0zM16 12a2 2 0 100-4 2 2 0 000 4z" />
                                            </svg>
                                        </button>
                                    </x-slot>
                                    <x-slot name="content">
                                        <x-dropdown-link :href="route('chirps.edit', $chirp)">
                                            {{ __('Edit') }}
                                        </x-dropdown-link>
                                    </x-slot>
                                </x-dropdown>
                            @endif<!-- [tl! add:end] -->
                        </div>
                        <p class="mt-4 text-lg text-gray-900">{{ $chirp->message }}</p>
                    </div>
                </div>
            @endforeach
        </div>
    </div>
</x-app-layout>
```

## Membuat edit form

Buat Blade view baru yang memuat sebuah form untuk edit Chirp. Mungkin akan mirip dengan form untuk membuat Chirp, yang membedakan kita akan post ke route `chirps.update` dan menggunakan directive `@method` untuk menentukan bahwa kita membuat request "PATCH". Kita juga mengisi terlebih dahulu field dengan pesan Chirp yang sekarang:

```blade filename=resources/views/chirps/edit.blade.php
<x-app-layout>
    <div class="max-w-2xl p-4 mx-auto sm:p-6 lg:p-8">
        <form method="POST" action="{{ route('chirps.update', $chirp) }}">
            @csrf
            @method('patch')
            <textarea
                name="message"
                class="block w-full border-gray-300 rounded-md shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50"
            >{{ old('message', $chirp->message) }}</textarea>
            <x-input-error :messages="$errors->get('message')" class="mt-2" />
            <div class="mt-4 space-x-2">
                <x-primary-button>{{ __('Save') }}</x-primary-button>
                <a href="{{ route('chirps.index') }}">{{ __('Cancel') }}</a>
            </div>
        </form>
    </div>
</x-app-layout>
```

## Update controller

Ubah method `edit` di `ChirpController` untuk menampilkan form. Laravel secara otomatis akan mengambil model Chirp dari database menggunakan [route model binding](https://laravel.com/docs/9.x/routing#route-model-binding) jadi kita bisa meneruskannya ke view.

Kita juga update method `update` untuk mem-validasi request dan update database.

Meskipun kita hanya menampilkan tombol edit ke pembuat Chirp-nya, kita masih perlu untuk memastikan user hanya dapat mengakses routes yang diizinkan:

```php filename=app/Http/Controllers/ChirpController.php
<?php
// [tl! collapse:start]
namespace App\Http\Controllers;

use App\Models\Chirp;
use Illuminate\Http\RedirectResponse;
use Illuminate\Http\Request;
use Illuminate\Http\Response;
use Illuminate\View\View;
// [tl! collapse:end]
class ChirpController extends Controller
{
    // [tl! collapse:start]
    /**
     * Display a listing of the resource.
     */
    public function index(): View
    {
        return view('chirps.index', [
            'chirps' => Chirp::with('user')->latest()->get(),
        ]);
    }

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
    public function store(Request $request): RedirectResponse
    {
        $validated = $request->validate([
            'message' => 'required|string|max:255',
        ]);

        $request->user()->chirps()->create($validated);

        return redirect(route('chirps.index'));
    }

    /**
     * Display the specified resource.
     */
    public function show(Chirp $chirp)
    {
        //
    }
    // [tl! collapse:end]
    /**
     * Show the form for editing the specified resource.
     */
    public function edit(Chirp $chirp)// [tl! remove]
    public function edit(Chirp $chirp): View// [tl! add]
    {
        //
        $this->authorize('update', $chirp);// [tl! remove:-1,1 add:start]

        return view('chirps.edit', [
            'chirp' => $chirp,
        ]);// [tl! add:end]
    }
    /**
     * Update the specified resource in storage.
     */
    public function update(Request $request, Chirp $chirp)// [tl! remove]
    public function update(Request $request, Chirp $chirp): RedirectResponse// [tl! add]
    {
        //
        $this->authorize('update', $chirp);// [tl! remove:-1,1 add:start]

        $validated = $request->validate([
            'message' => 'required|string|max:255',
        ]);

        $chirp->update($validated);

        return redirect(route('chirps.index'));// [tl! add:end]
    }
    // [tl! collapse:start]
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

> **Note**
> Kamu mungkin melihat ada duplikat validation rules untuk method `store`. Sebenarnya bisa juga dipertimbangkan untuk meng-ektraksi-nya menggunakan Laravel [Form Request Validation](https://laravel.com/docs/validation#form-request-validation), yang mana ini akan membuatnya mudah untuk digunakan kembali dan menjaga controllers kita tetap ramping.

## Authorization

Secara default, method `authorize` akan mencegah _everyone_ dari kemampuan untuk update Chirp. Kita dapat mengatur siapa yang diperbolehkan untuk meng-update-nya dengan membuat sebuah [Model Policy](https://laravel.com/docs/authorization#creating-policies) dengan perintah berikut:

```shell
php artisan make:policy ChirpPolicy --model=Chirp
```

Hal ini akan membuat class policy di `app/Policies/ChirpPolicy.php` yang mana kita dapat update untuk menentukan hanya pembuatnya yang dapat meng-update sebuah Chirp tersebut:

```php filename=app/Policies/ChirpPolicy.php
<?php
// [tl! collapse:start]
namespace App\Policies;

use App\Models\Chirp;
use App\Models\User;
use Illuminate\Auth\Access\HandlesAuthorization;
// [tl! collapse:end]
class ChirpPolicy
{
    // [tl! collapse:start]
    use HandlesAuthorization;

    /**
     * Determine whether the user can view any models.
     */
    public function viewAny(User $user): bool
    {
        //
    }

    /**
     * Determine whether the user can view the model.
     */
    public function view(User $user, Chirp $chirp): bool
    {
        //
    }

    /**
     * Determine whether the user can create models.
     */
    public function create(User $user): bool
    {
        //
    }
    // [tl! collapse:end]
    /**
     * Determine whether the user can update the model.
     */
    public function update(User $user, Chirp $chirp): bool
    {
        //
        return $chirp->user()->is($user);// [tl! remove:-1,1 add]
    }
    // [tl! collapse:start]
    /**
     * Determine whether the user can delete the model.
     */
    public function delete(User $user, Chirp $chirp): bool
    {
        //
    }

    /**
     * Determine whether the user can restore the model.
     */
    public function restore(User $user, Chirp $chirp): bool
    {
        //
    }

    /**
     * Determine whether the user can permanently delete the model.
     */
    public function forceDelete(User $user, Chirp $chirp): bool
    {
        //
    }
    // [tl! collapse:end]
}
```

## Testing it out

Waktunya untuk test! Cobalah untuk edit beberapa Chirps menggunakan menu dropdown. Jika kamu mendaftarkan user akun lain, kamu akan melihat bahwa hanya pembuat Chirp tersebut saja yang dapat melakukan edit.

<img src="/img/screenshots/chirp-editted-blade.png" alt="An editted chirp" class="border rounded-lg shadow-lg dark:border-none" />

[Lanjut ke bagian untuk hapus Chirps...](/chirper/deleting-chirps)
