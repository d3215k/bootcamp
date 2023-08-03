[TOC]

# <b>06.</b> Notifications & Events

Kita buat Chirper ke level yang lebih keren lagi dengan fitur mengirim [email notifications](https://laravel.com/docs/notifications#introduction) saat Chirp baru dibuat.

Selain dukungan untuk mengirim email, Laravel menyediakan dukungan untuk mengirimkan notifikasi melalui berbagai saluran pengiriman, termasuk email, SMS, dan Slack. Selain itu, berbagai saluran notifikasi buatan komunitas telah dibuat untuk mengirimkan notifikasi ke banyak saluran berbeda! Notifikasi juga dapat disimpan dalam database sehingga dapat ditampilkan di antarmuka web kita.

## Membuat notification

Artisan dapat, lagi-lagi, melakukan semua kerja keras untuk kita dengan command berikut: 

```shell
php artisan make:notification NewChirp
```

Hal ini akan membuat sebuah notifikasi baru di `app/Notifications/NewChirp.php` yang siap untuk kita sesuaikan.

Buka class `NewChirp` dan izinkan untuk meneripa `Chirp` yang baru saja dibuat, lalu sesuaikan pesan untuk menyeertakan nama penulis dan cuplikan dari pesan:

```php filename=app/Notifications/NewChirp.php
<?php
namespace App\Notifications;

use App\Models\Chirp;// [tl! add]
use Illuminate\Bus\Queueable;
use Illuminate\Support\Str;// [tl! add]
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Notifications\Messages\MailMessage;
use Illuminate\Notifications\Notification;

class NewChirp extends Notification
{
    use Queueable;

    /**
     * Create a new notification instance.
     */
    public function __construct()// [tl! remove]
    public function __construct(public Chirp $chirp)// [tl! add]
    {
        //
    }
    // [tl! collapse:start]
    /**
     * Get the notification's delivery channels.
     *
     * @return array<int, string>
     */
    public function via(object $notifiable): array
    {
        return ['mail'];
    }
    // [tl! collapse:end]
    /**
     * Get the mail representation of the notification.
     */
    public function toMail(object $notifiable): MailMessage
    {
        return (new MailMessage)
                    ->line('The introduction to the notification.')// [tl! remove]
                    ->action('Notification Action', url('/'))// [tl! remove]
                    ->subject("New Chirp from {$this->chirp->user->name}")// [tl! add]
                    ->greeting("New Chirp from {$this->chirp->user->name}")// [tl! add]
                    ->line(Str::limit($this->chirp->message, 50))// [tl! add]
                    ->action('Go to Chirper', url('/'))// [tl! add]
                    ->line('Thank you for using our application!');
    }
    // [tl! collapse:start]
    /**
     * Get the array representation of the notification.
     *
     * @return array<string, mixed>
     */
    public function toArray(object $notifiable): array
    {
        return [
            //
        ];
    }
    // [tl! collapse:end]
}
```

Kita dapat mengirimkan notifikasi langsung dari methode `store` pada class `ChirpController`, tetapi hal itu menambah lebih banyak pekerjaan untuk controller, yang pada gilirannya dapat memperlambat permintaan, terutama karena karena kita akan buat query ke database dan mengirim email.

Alih-alih, kita kirim event notification yang dapat di listen untuk proses di background queue agar aplikasi kita tetap cepat.

## Membuat event

Events menjadi cara yang baik untuk memisahkan berbagai aspek di aplikasi, karena satu event dapat memiliki beberapa listener yang tidak bergantung satu sama lain.

Mari buat event baru kita dengan command berikut:

```shell
php artisan make:event ChirpCreated
```

Hal ini akan membuat sebuah class event baru di `app/Events/ChirpCreated.php`.

Karena kita akan mengirimkan event untuk setiap Chirp yang baru dibuat, mari perbarui event `ChirpCreated` untuk menerima `Chirp` yang baru dibuat sehingga kita dapat meneruskannya ke notification:

```php filename=app/Events/ChirpCreated.php
<?php

namespace App\Events;

use App\Models\Chirp;// [tl! add]
use Illuminate\Broadcasting\Channel;
use Illuminate\Broadcasting\InteractsWithSockets;
use Illuminate\Broadcasting\PresenceChannel;
use Illuminate\Broadcasting\PrivateChannel;
use Illuminate\Contracts\Broadcasting\ShouldBroadcast;
use Illuminate\Foundation\Events\Dispatchable;
use Illuminate\Queue\SerializesModels;

class ChirpCreated
{
    use Dispatchable, InteractsWithSockets, SerializesModels;

    /**
     * Create a new event instance.
     */
    public function __construct()// [tl! remove]
    public function __construct(public Chirp $chirp)// [tl! add]
    {
        //
    }
    // [tl! collapse:start]
    /**
     * Get the channels the event should broadcast on.
     */
    public function broadcastOn(): array
    {
        return [
            new PrivateChannel('channel-name'),
        ];
    }
    // [tl! collapse:end]
}
```

## Mengirimkan event

Sekrang kita usdah punya class event, kita sudah siap untuk mengirimkannya kapanpun sebuah Chirp dibuat.Kamu mungkin [dispatch events](https://laravel.com/docs/events#dispatching-events) dimanapun dalam siklus hidup aplikasi, tetapi karena event kita akan terkait dengan pembuatan model Eloquent, kita dapat mengonfigurasi model `Chirp` untuk mengirimkan event.

```php filename=app/Models/Chirp.php
<?php

namespace App\Models;

use App\Events\ChirpCreated;// [tl! add]
use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\BelongsTo;

class Chirp extends Model
{
    use HasFactory;

    protected $fillable = [
        'message',
    ];

    protected $dispatchesEvents = [// [tl! add:start]
        'created' => ChirpCreated::class,
    ];// [tl! add:end]

    public function user(): BelongsTo
    {
        return $this->belongsTo(User::class);
    }
}
```

Sekarang setiap kali `Chirp` baru dibuat, event `ChirpCreated` akan dikirim.

## Membuat event listener

Sekarang kita sudah bisa mengirimkan event, maka sekarang buat listener untuk event tersebut yang kemudian mengirim notification kita. 

Kita buat sebuah listener yang subscribes ke event `ChirpCreated`:

```sail
php artisan make:listener SendChirpCreatedNotifications --event=ChirpCreated
```

Listener baru akan ditempatkan di `app/Listeners/SendChirpCreatedNotifications.php`. Kita update listener-nya untuk mengirimkan notifikasi kita.

```php filename=app/Listeners/SendChirpCreatedNotifications.php
<?php

namespace App\Listeners;

use App\Events\ChirpCreated;
use App\Models\User;// [tl! add]
use App\Notifications\NewChirp;// [tl! add]
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Queue\InteractsWithQueue;

class SendChirpCreatedNotifications// [tl! remove]
class SendChirpCreatedNotifications implements ShouldQueue// [tl! add]
{
    // [tl! collapse:start]
    /**
     * Create the event listener.
     */
    public function __construct()
    {
        //
    }
    // [tl! collapse:end]
    /**
     * Handle the event.
     */
    public function handle(ChirpCreated $event): void
    {
        //
        foreach (User::whereNot('id', $event->chirp->user_id)->cursor() as $user) {// [tl! remove:-1,1 add:start]
            $user->notify(new NewChirp($event->chirp));
        }// [tl! add:end]
    }
}
```

Kita telah menandai listener dengan interface `ShouldQueue`, yang memberitahu Laravel bahwa listener harus dijalankan dalam [queue](https://laravel.com/docs/queues). Secara default, antrian secara "sync" akan digunakan untuk memproses jobs secara sinkron; namun, kita dapat mengonfigurasi queue worker untuk memproses jobs di latar belakang.

Kita juga telah mengonfigurasi listener untuk mengirim notifications ke setiap pengguna di platform, kecuali pembuat Chirp. Pada kenyataannya, ini mungkin mengganggu user, jadi Anda mungkin ingin menerapkan fitur "following" agar user hanya menerima notification untuk akun yang mereka ikuti.

Kita juga mengunakan [database cursor](https://laravel.com/docs/eloquent#cursors) untuk menghindari dari load semua user ke memori sekaligus.

> **Note**
> Dalam aplikasi yang sudah benar digunakan, Anda harus menambahkan fitur bagi user untuk berhenti berlangganan notifikasi seperti ini.

### Mendaftarkan event listener

Terakhir, kita bind event listener ke event tersebut. Ini akan memberitahu Laravel untuk memanggil event listener kita saat suat event dikirim. Kita bisa melakukan ini di class `EventServiceProvider`:

```php filename=App\Providers\EventServiceProvider.php
<?php

namespace App\Providers;

use App\Events\ChirpCreated;// [tl! add]
use App\Listeners\SendChirpCreatedNotifications;// [tl! add]
use Illuminate\Auth\Events\Registered;
use Illuminate\Auth\Listeners\SendEmailVerificationNotification;
use Illuminate\Foundation\Support\Providers\EventServiceProvider as ServiceProvider;
use Illuminate\Support\Facades\Event;

class EventServiceProvider extends ServiceProvider
{
    /**
     * The event to listener mappings for the application.
     *
     * @var array<class-string, array<int, class-string>>
     */
    protected $listen = [
        ChirpCreated::class => [// [tl! add:start]
            SendChirpCreatedNotifications::class,
        ],// [tl! add:end]

        Registered::class => [
            SendEmailVerificationNotification::class,
        ],
    ];
    // [tl! collapse:start]
    /**
     * Register any events for your application.
     */
    public function boot(): void
    {
        //
    }

    /**
     * Determine if events and listeners should be automatically discovered.
     */
    public function shouldDiscoverEvents(): bool
    {
        return false;
    }
    // [tl! collapse:end]
}
```

## Testing it out

Anda dapat menggunakan tool email local seperti [Mailpit](https://github.com/axllent/mailpit) untuk menangkap email apapun yang datang dari aplikasi kita sehingga kita dapat melihatnya.

Alternatifnya, Anda dapat mengonfigurasi Laravel untuk menulis email ke file log dengan mengedit file `.env` dan mengubah variabel `MAIL_MAILER` ke `log`. Secara default, email akan ditulis ke file log yang terletak di `storage/logs/laravel.log`.

Kita telah mengonfigurasi notification untuk tidak dikirim ke pembuat Chirp, jadi pastikan untuk mendaftarkan setidaknya dua user akun. Kemudian, lanjutkan dan posting Chirp baru untuk memicu notifikasi.

Jika Anda menggunakan Mailpit, buka halaman [http://localhost:8025/](http://localhost:8025/), dimana anda akan menemukan notifikasi untuk Chirp baru yang baru saja anda buat!

<img src="/img/screenshots/mailpit.png" alt="Mailpit" class="border rounded-lg shadow-lg dark:border-none" />

### Mengirim email di production

Untuk mengirim email yang benar-benar digunakan dalam aplikasi yang sudah dipakai, anda akan memerlukan server SMTP, atau penyedia email transaksional, seperti Mailgun, Postmark, atau Amazon SES. Laravel mendukung semua ini. Informasi lebih lanjut, lihat [Mail documentation](https://laravel.com/docs/mail#introduction).

[Lanjut ke penutup...](/conclusion)
