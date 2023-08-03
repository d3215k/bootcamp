[TOC]

# <b>06.</b> Relationship

Dalam pengembangan aplikasi web, seringkali data dalam basis data terkait dengan data lain. Sebagai contoh, satu pengguna dapat memiliki banyak postingan atau satu pesanan dapat terdiri dari beberapa produk. Konsep relationship atau hubungan dalam Laravel adalah cara yang digunakan untuk mendefinisikan dan mengatur hubungan antara tabel-tabel dalam basis data.

Laravel menyediakan Eloquent, ORM (Object-Relational Mapping) yang kuat, untuk mengelola hubungan antara Model dengan Model lainnya. Eloquent memungkinkan Anda mendefinisikan berbagai jenis relasi, seperti "one to one", "one to many", "many to many", dan lain-lain.

Beberapa jenis relationship yang didukung oleh Eloquent meliputi:

- `One to One`: Relasi di mana satu baris dalam satu tabel berhubungan dengan satu baris dalam tabel lain.
- `One to Many`: Relasi di mana satu baris dalam satu tabel berhubungan dengan banyak baris dalam tabel lain.
- `Many to Many`: Relasi di mana banyak baris dalam satu tabel berhubungan dengan banyak baris dalam tabel lain melalui tabel perantara (pivot table).
- `Has One Through`: Relasi yang memungkinkan Anda mengakses data dari model ketiga melalui model kedua.
- `Has Many Through`: Relasi yang memungkinkan Anda mengakses banyak data dari model ketiga melalui model kedua.

Dalam aplikasi manajemen tugas, satu pengguna dapat memiliki banyak tugas. Untuk mengatur hubungan ini, kita akan menggunakan konsep "one to many" (satu-ke-banyak) dengan memanfaatkan fitur relationship atau hubungan dalam Laravel.

Pada contoh ini, kita sudah memiliki tabel "users" untuk menyimpan data pengguna dan tabel "tasks" untuk menyimpan data tugas. Namun, kita akan menambahkan kolom relasi "user_id" pada tabel "tasks" sebagai foreign key untuk menunjukkan hubungan antara tugas dengan pengguna.

Pertama, buatlah migrasi untuk tabel "tasks" dengan menambahkan kolom "user_id":
```
php artisan make:migration add_user_id_to_tasks_table --table=tasks
```

Kemudian, buka file migrasi yang baru saja dibuat di direktori database/migrations dan edit isinya:
```php
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class AddUserIdToTasksTable extends Migration
{
    public function up()
    {
        Schema::table('tasks', function (Blueprint $table) {
            $table->unsignedBigInteger('user_id'); // Kolom untuk foreign key
            $table->foreign('user_id')->references('id')->on('users');
        });
    }

    public function down()
    {
        Schema::table('tasks', function (Blueprint $table) {
            $table->dropForeign(['user_id']);
            $table->dropColumn('user_id');
        });
    }
}
```

Setelah menambahkan kolom "user_id" pada tabel "tasks", kita perlu mengatur relasi "one to many" antara Model "User" dan "Task".
```php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    public function tasks()
    {
        return $this->hasMany(Task::class);
    }
}
```

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Task extends Model
{
    public function user()
    {
        return $this->belongsTo(User::class);
    }
}
```

Dengan konfigurasi relasi di atas, Anda dapat dengan mudah mengakses tugas-tugas (tasks) dari pengguna tertentu atau mengakses pengguna yang memiliki suatu tugas.
```php
// Mendapatkan pengguna dari suatu tugas (task)
$task = Task::find(1);
$user = $task->user; // Mendapatkan instance dari Model User

// Mendapatkan tugas-tugas dari suatu pengguna
$user = User::find(1);
$tasks = $user->tasks; // Mendapatkan koleksi tugas-tugas dari Model Task
```

Dengan menggunakan fitur relationship Eloquent di Laravel, pengaturan dan penggunaan relasi "one to many" antara Model "User" dan "Task" dapat diimplementasikan dengan mudah. Fitur ini mempermudah analisis dan pengelolaan data terkait dalam aplikasi Laravel Anda, sehingga memudahkan dalam membangun aplikasi yang lebih kompleks dan efisien.
