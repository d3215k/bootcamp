[TOC]

# <b>03.</b> Menampilkan Chirps

Pada tahap sebelumnya kita sudah menambahkan fitur untuk membuat Chirps, sekarang kita siap untuk menampilkannya!

## Mengambil Chirps

Ubah method `index` di class `ChirpController` untuk mengambil Chirps dari semua user ke halaman index:

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
    /**
     * Display a listing of the resource.
     */
    public function index(): View
    {
        return view('chirps.index');// [tl! remove]
        return view('chirps.index', [// [tl! add:start]
            'chirps' => Chirp::with('user')->latest()->get(),
        ]);// [tl! add:end]
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
    public function store(Request $request): RedirectResponse
    {
        $validated = $request->validateWithBag('store', [
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

Disini kita menggunakan methode Eloquent `with` untuk [eager-load](https://laravel.com/docs/eloquent-relationships#eager-loading) setiap Chirps beserta user-nya. Kita juga menggunakan scope `latest` untuk mengembalikan records dengan posisi urutan kronologis terbalik.

> **Note**
> Mengambil langsung semua Chirps sekaligus sangat tidak baik pada saat nanti production. Cobalah juga untuk lihat dan pelajari [pagination](https://laravel.com/docs/pagination) dari laravel untuk meningkatkan kinerja aplikasi.

## Menghubungkan users to Chirps

Kita mungkin sudah membuat relasi `user` sehingga kita bisa menampilkan nama pembuat Chirp-nya. Akan tetapi, relasi Chirp `user` belum kita buat. Untuk memperbaiki ini, kita tambahkan relasi ["belongs to"](https://laravel.com/docs/eloquent-relationships#one-to-many-inverse) pada model `Chirp`:

```php filename=app/Models/Chirp.php
<?php
// [tl! collapse:start]
namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;// [tl! collapse:end]
use Illuminate\Database\Eloquent\Relations\BelongsTo;// [tl! add]

class Chirp extends Model
{
    // [tl! collapse:start]
    use HasFactory;

    protected $fillable = [
        'message',
    ];
    // [tl! collapse:end]
    public function user(): BelongsTo// [tl! add:start]
    {
        return $this->belongsTo(User::class);
    }// [tl! add:end]
}
```

Relasi ini adalah kebalikan dari relasi "has many" yang sebelumnya sudah kita buat di model `User`.

## Update view

Selanjutkan, kita ubah component `chirps.index` untuk menampilkan Chirps di bagian bawah form:

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
            <x-input-error :messages="$errors->store->get('message')" class="mt-2" />
            <x-primary-button class="mt-4">{{ __('Chirp') }}</x-primary-button>
        </form>

        <div class="mt-6 bg-white divide-y rounded-lg shadow-sm"><!-- [tl! add:start] -->
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
                            </div>
                        </div>
                        <p class="mt-4 text-lg text-gray-900">{{ $chirp->message }}</p>
                    </div>
                </div>
            @endforeach
        </div><!-- [tl! add:end] -->
    </div>
</x-app-layout>
```

Sekarang coba buka browser untuk melihat pesan yang sebelumnya sudah kita buat!

<img src="/img/screenshots/chirp-index-blade.png" alt="Chirp listing" class="border rounded-lg shadow-lg dark:border-none" />

Silahkan tambah beberapa Chirp lagi, atau coba daftar dan buat akun lain dan mulai percakapan!

[Lanjut untuk fitur edit Chirps...](/chirper/editing-chirps)
