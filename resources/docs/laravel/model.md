[TOC]

# <b>01.</b> Model

Dalam konsep Model-View-Controller (MVC) di Laravel, Model merupakan bagian yang bertanggung jawab untuk mengelola data dan interaksi dengan basis data. Model merepresentasikan tabel-tabel dalam basis data dan menyediakan metode-metode untuk melakukan operasi seperti menyimpan, mengambil, memperbarui, dan menghapus data.

#### Representasi Tabel
Model merepresentasikan struktur tabel dalam basis data. Nama Model biasanya berbentuk singular dari nama tabel yang sesuai. Misalnya, Model "User" merepresentasikan tabel "users". Ini memudahkan Anda dalam berinteraksi dengan tabel dan mengelola data.

#### Query Builder
Model menyediakan antarmuka yang nyaman untuk berinteraksi dengan basis data menggunakan Query Builder. Anda dapat menggunakan berbagai metode bawaan untuk membuat query seperti mengambil data, menyimpan data baru, memperbarui data, dan menghapus data dari tabel terkait.

#### Validasi Data
Model memungkinkan Anda mendefinisikan aturan validasi yang harus dipatuhi oleh data sebelum disimpan ke dalam basis data. Anda dapat menentukan aturan validasi untuk setiap kolom dalam Model, sehingga memastikan bahwa data yang disimpan adalah valid dan sesuai dengan persyaratan aplikasi.

#### Relasi Eloquent
Model memungkinkan Anda mendefinisikan relasi antara Model ini dengan Model lain menggunakan fitur Eloquent di Laravel. Ini mempermudah mengakses data terkait melalui relasi tersebut. Contohnya, jika setiap "Task" memiliki satu "User" yang menanganinya, Anda dapat mendefinisikan relasi tersebut dalam Model "Task".

#### Event & Observer
Model juga mendukung fitur Event dan Observer. Anda dapat mendefinisikan Event yang akan dipicu ketika terjadi aksi tertentu pada Model, seperti ketika data disimpan atau dihapus. Observer memungkinkan Anda untuk mengamati peristiwa Model dan menangani tindakan yang sesuai.

#### Soft Deletes
Model mendukung soft deletes, yang memungkinkan Anda untuk "menghapus" data dari basis data dengan menandainya sebagai tidak aktif tanpa benar-benar menghapusnya secara permanen. Data yang dihapus secara lembut masih dapat diakses dan diambil kembali jika diperlukan.

#### Timestamps Otomatis
Model secara otomatis menyediakan kemampuan untuk mengelola kolom timestamp seperti "created_at" dan "updated_at". Ketika data disimpan atau diperbarui, nilai timestamp akan diperbarui secara otomatis.

Model dalam Laravel memungkinkan Anda untuk mengatur struktur basis data dengan lebih mudah, melakukan operasi CRUD dengan cepat, serta mengakses data terkait dengan mudah. Ini adalah salah satu pilar utama dalam pengembangan aplikasi web dengan Laravel yang kuat dan efisien.

## Membuat Model
Misalnya, jika Anda ingin membuat Model untuk tabel "tasks", gunakan perintah berikut:
```
php artisan make:model Task
```

Model akan dibuat dalam direktori app/Models jika menggunakan Laravel 8 ke atas. Jika Anda menggunakan Laravel sebelum versi 8, Model akan dibuat di direktori app.
```php filename=app/Models/Task.php
namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Task extends Model
{
    use HasFactory;

    // ...
}
```

## CRUD dengan Model Eloquent
```php
use App\Models\Task;
use App\Models\User;
use Illuminate\Http\Request;

// Menampilkan semua data tasks
Route::get('/tasks', function () {
    $tasks = Task::all();
    return $tasks;
});

// Menampilkan data task berdasarkan ID
Route::get('/tasks/{id}', function ($id) {
    $task = Task::find($id);
    return $task;
});

// Menyimpan data task baru
Route::post('/tasks', function (Request $request) {
    $task = new Task();
    $task->name = $request->input('name');
    $task->description = $request->input('description');
    $task->finished = $request->input('finished', false);
    $task->save();

    return response()->json(['message' => 'Task created successfully'], 201);
});

// Memperbarui data task berdasarkan ID
Route::put('/tasks/{id}', function (Request $request, $id) {
    $task = Task::find($id);
    if (!$task) {
        return response()->json(['message' => 'Task not found'], 404);
    }

    $task->name = $request->input('name');
    $task->description = $request->input('description');
    $task->finished = $request->input('finished', false);
    $task->save();

    return response()->json(['message' => 'Task updated successfully']);
});

// Menghapus data task berdasarkan ID
Route::delete('/tasks/{id}', function ($id) {
    $task = Task::find($id);
    if (!$task) {
        return response()->json(['message' => 'Task not found'], 404);
    }

    $task->delete();

    return response()->json(['message' => 'Task deleted successfully']);
});
```

Pada contoh di atas, kita menggunakan Model "Task" untuk melakukan operasi CRUD pada tabel "tasks". Model "Task" memanfaatkan fitur Eloquent di Laravel yang memungkinkan kita untuk menyederhanakan operasi database dengan mudah dan ringkas.

Pastikan Anda telah menyesuaikan routing dan validasi data sesuai dengan kebutuhan aplikasi Anda. Dalam contoh ini, kita hanya memberikan contoh implementasi CRUD tanpa melibatkan view untuk kesederhanaan.
