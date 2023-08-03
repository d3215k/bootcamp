[TOC]

# <b>04.</b> Mengakses Database

Database adalah salah satu komponen krusial dalam pengembangan aplikasi modern, dan Laravel menyediakan lingkungan yang kuat dan efisien untuk berinteraksi dengan berbagai jenis database. Kami akan membahas cara mengatur koneksi database Anda menggunakan berkas .env, melakukan migrasi database, berinteraksi dengan Model Eloquent, dan menjalankan kueri database menggunakan Query Builder. 

## Konfigurasi
Untuk melakukan konfigurasi koneksi database pada Laravel, Anda perlu mengatur beberapa file utama. Berikut adalah langkah-langkah singkat untuk melakukan konfigurasi koneksi database pada Laravel:

#### Langkah 1: Buka File .env
Pertama, buka file .env di direktori root proyek Laravel Anda. File ini berisi konfigurasi lingkungan dan merupakan tempat untuk mengatur variabel lingkungan seperti koneksi database.

#### Langkah 2: Konfigurasi Variabel Lingkungan
Di file .env, atur variabel lingkungan untuk koneksi database Anda. Contoh konfigurasi:
```env filename=.env
DB_CONNECTION=mysql
DB_HOST=nama_host_database
DB_PORT=port_database
DB_DATABASE=nama_database
DB_USERNAME=username_database
DB_PASSWORD=password_database
```

Pastikan untuk mengganti nilai-nilai ini sesuai dengan informasi koneksi database Anda. Variabel DB_CONNECTION digunakan untuk menentukan jenis database (misalnya: mysql, pgsql, sqlite, dll.).

#### Langkah 3: Konfigurasi File database.php
Laravel memiliki file konfigurasi database.php di direktori config yang harus Anda periksa. Pastikan bahwa konfigurasi koneksi di dalam file ini sesuai dengan yang Anda tentukan di .env.

Jika Anda menggunakan MySQL sebagai contoh, pastikan bagian 'connections' untuk MySQL seperti berikut:
```php filename=config/database.php
'connections' => [
    'mysql' => [
        'driver' => 'mysql',
        'host' => env('DB_HOST', '127.0.0.1'),
        'port' => env('DB_PORT', '3306'),
        'database' => env('DB_DATABASE', 'forge'),
        'username' => env('DB_USERNAME', 'forge'),
        'password' => env('DB_PASSWORD', ''),
        // ...
    ],
    // ...
],
```

Laravel secara otomatis akan mengambil nilai dari file .env dan menggunakannya dalam konfigurasi ini jika nilai tidak ditemukan.

#### Langkah 4: Coba Koneksi Database
Setelah konfigurasi selesai, Anda dapat mencoba koneksi database dengan menjalankan perintah migrasi Laravel:
```
php artisan migrate
```
Perintah ini akan mencoba menghubungkan ke database yang telah Anda konfigurasi dan menjalankan migrasi yang telah Anda definisikan.


## Migration dan Schema Builder
Dalam pengembangan aplikasi web, struktur database yang baik sangat penting. Migration adalah fitur yang sangat berguna dalam Laravel yang memungkinkan Anda secara mudah mengelola skema database Anda secara terstruktur dan efisien. Schema builder di Laravel memungkinkan Anda untuk menggunakan sintaks ekspresif untuk mendefinisikan skema database, bahkan tanpa harus menulis SQL langsung.

#### Langkah 1: Membuat Migration
Pertama, mari kita buat migration baru dengan menjalankan perintah berikut di terminal:
```
php artisan make:migration create_tasks_table --create=tasks
```

Perintah di atas akan membuat berkas migrasi baru dalam direktori database/migrations. Gantilah nama_tabel dengan nama tabel yang ingin Anda buat.

#### Langkah 2: Definisikan Skema Tabel
Buka berkas migrasi yang baru saja dibuat. Di dalam fungsi up(), Anda dapat menggunakan schema builder untuk mendefinisikan skema tabel. Misalnya, Anda dapat menambahkan kolom, mengatur kunci utama, indeks, dan lain-lain. Contoh untuk membuat tabel pengguna sederhana:
```php
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreateTasksTable extends Migration
{
    public function up()
    {
        Schema::create('tasks', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->text('description')->nullable();
            $table->timestamps();
        });
    }

    public function down()
    {
        Schema::dropIfExists('tasks');
    }
}
```

#### Langkah 3: Jalankan Migrasi
Untuk menerapkan perubahan skema tabel ke database, jalankan perintah migrasi:
```
php artisan migrate
```

Perintah ini akan menjalankan semua migrasi yang belum dijalankan sebelumnya, menciptakan tabel yang baru didefinisikan dan memperbarui struktur database.

#### Langkah 4: Rollback Migrasi
Jika Anda ingin mengembalikan migrasi, Anda dapat menggunakan perintah rollback:
```
php artisan migrate:rollback
```

Perintah ini akan menghapus migrasi terakhir yang telah dijalankan.

#### Langkah 5: Menambahkan Kolom Baru
Jika Anda perlu menambahkan kolom baru ke tabel yang sudah ada, Anda bisa membuat migrasi baru dengan perintah berikut:
```
php artisan make:migration add_finished_to_tasks_table --table=tasks
```

Kemudian, Anda bisa mengedit berkas migrasi baru ini untuk menambahkan kolom yang diinginkan.
```php
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class AddFinishedToTasksTable extends Migration
{
    public function up()
    {
        Schema::table('tasks', function (Blueprint $table) {
            $table->boolean('finished')->default(false);
        });
    }

    public function down()
    {
        Schema::table('tasks', function (Blueprint $table) {
            $table->dropColumn('finished');
        });
    }
}
```

#### Langkah 6: Lainnya
Schema builder di Laravel mendukung banyak opsi lainnya seperti mengubah kolom, menghapus kolom, menambahkan indeks, mengubah tipe data, dan banyak lagi. Anda dapat mengeksplorasi dokumentasi resmi Laravel untuk lebih lanjut tentang Schema Builder.

Dengan menggunakan migrasi dan schema builder, Anda dapat dengan mudah mengelola skema database Anda secara terstruktur dan aman, memastikan bahwa aplikasi Laravel Anda selalu berjalan sesuai dengan harapan.

## Query Builder
implementasi CRUD menggunakan Query Builder di Laravel
```php filename=routes/web.php
use Illuminate\Support\Facades\DB;
use Illuminate\Http\Request;

Route::get('/tasks', function () {
    $tasks = DB::table('tasks')->get();
    return $tasks;
});

Route::get('/tasks/{id}', function ($id) {
    $task = DB::table('tasks')->find($id);
    return $task;
});

Route::post('/tasks', function (Request $request) {
    DB::table('tasks')->insert([
        'name' => $request->input('name'),
        'description' => $request->input('description'),
        'created_at' => now(),
        'updated_at' => now(),
    ]);
    return response()->json(['message' => 'Task created successfully'], 201);
});

Route::put('/tasks/{id}', function (Request $request, $id) {
    DB::table('tasks')->where('id', $id)->update([
        'name' => $request->input('name'),
        'description' => $request->input('description'),
        'updated_at' => now(),
    ]);
    return response()->json(['message' => 'Task updated successfully']);
});

Route::delete('/tasks/{id}', function ($id) {
    DB::table('tasks')->where('id', $id)->delete();
    return response()->json(['message' => 'Task deleted successfully']);
});
```

Pada contoh di atas, kita menggunakan Query Builder di dalam fungsi closure pada setiap rute untuk melakukan operasi CRUD pada tabel "tasks". Hasil dari setiap operasi akan dikembalikan sebagai JSON response.

Pastikan Anda telah mengatur routing dan mengelola validasi data sesuai dengan kebutuhan aplikasi Anda. Dalam contoh ini, kita hanya memberikan contoh implementasi CRUD tanpa melibatkan view untuk kesederhanaan.

[Lanjut ke Model...](/laravel/model)

