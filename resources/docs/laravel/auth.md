[TOC]

# <b>02.</b> Auth

## Authentication

Authentication (autentikasi) adalah proses untuk memverifikasi identitas pengguna, yaitu memastikan bahwa pengguna yang mencoba mengakses aplikasi adalah pengguna yang sah dan memiliki izin untuk melakukannya. Dalam konteks web, autentikasi biasanya dilakukan dengan meminta pengguna untuk memasukkan kredensial seperti nama pengguna (username) dan kata sandi (password).

Dalam Laravel, fitur autentikasi memungkinkan Anda untuk mengelola proses autentikasi dengan mudah. Ini mencakup pengaturan untuk login, logout, pengelolaan sesi, dan verifikasi kredensial pengguna.

## Authorization

Authorization (otorisasi) adalah proses untuk memverifikasi hak akses pengguna setelah proses autentikasi. Artinya, setelah pengguna terautentikasi, aplikasi perlu memeriksa apakah pengguna tersebut memiliki izin untuk melakukan aksi tertentu dalam aplikasi, misalnya mengakses halaman tertentu, melakukan operasi CRUD, atau mengeksekusi tindakan lain yang memerlukan izin khusus.

Dalam Laravel, fitur otorisasi memungkinkan Anda untuk mengelola proses otorisasi dengan mudah. Anda dapat menggunakan middleware, kebijakan (policies), atau gate untuk mengontrol akses dan hak pengguna dalam aplikasi.

#### Perbedaan antara Authentication dan Authorization:

Authentication memverifikasi identitas pengguna, yaitu memastikan bahwa pengguna adalah pengguna yang sah dengan kredensial yang valid.
Authorization memverifikasi hak akses pengguna setelah autentikasi berhasil, yaitu memastikan bahwa pengguna memiliki izin untuk melakukan aksi tertentu dalam aplikasi.
Contoh: Ketika seorang pengguna (username dan password telah terverifikasi) ingin mengakses halaman admin di aplikasi web (misalnya /admin), maka autentikasi akan memverifikasi identitas pengguna, dan otorisasi akan memeriksa apakah pengguna tersebut memiliki izin untuk mengakses halaman admin sebelum mengizinkannya untuk melihat halaman tersebut.

Laravel menyediakan banyak fitur bawaan untuk mengelola autentikasi dan otorisasi secara mudah. Fitur autentikasi menggunakan guard dan provider untuk mengatur autentikasi. Sedangkan untuk otorisasi, Anda dapat menggunakan middleware, kebijakan (policies), atau gate untuk mengontrol akses ke route, controller, atau tindakan tertentu.

Dengan memanfaatkan fitur-fitur ini, Anda dapat dengan mudah mengelola autentikasi dan otorisasi dalam aplikasi Laravel Anda, dan menjaga keamanan dan integritas data dengan lebih baik.
