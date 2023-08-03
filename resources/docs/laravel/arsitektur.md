[TOC]

# <b>02.</b> Arsitektur

Arsitektur Laravel didasarkan pada pola desain Model-View-Controller (MVC), yang membantu dalam pemisahan logika aplikasi menjadi tiga komponen utama:

## Model
- Model merupakan representasi dari data dan aturan bisnis aplikasi.
- Bertanggung jawab untuk mengakses dan memanipulasi data pada basis data.
- Biasanya, model berisi metode-metode untuk melakukan operasi CRUD (Create, Read, Update, Delete) pada data.
- Model juga berperan sebagai jembatan antara data dalam basis data dengan logika bisnis pada aplikasi.

## View
- View merupakan tampilan atau antarmuka pengguna dari aplikasi.
- Bertanggung jawab untuk menampilkan informasi kepada pengguna dalam bentuk yang dapat dipahami dan menarik.
- Biasanya, view ditulis dalam kode HTML, dan dapat menggunakan templating untuk menggabungkan data dari model ke dalam tampilan.

## Controller
- Controller bertindak sebagai perantara antara model dan view.
- Bertanggung jawab untuk menangani permintaan dari pengguna dan mengambil data dari model yang sesuai.
- Controller juga melakukan pemrosesan logika bisnis tertentu sebelum mengirimkan data ke view untuk ditampilkan.

Proses alur kerja dalam arsitektur Laravel adalah sebagai berikut:
1. Pengguna membuat permintaan melalui browser atau aplikasi.
2. Permintaan tersebut ditangkap oleh Laravel dan diteruskan ke rute yang sesuai berdasarkan definisi rute yang ada.
3. Rute kemudian mengarahkan permintaan ke controller yang sesuai.
4. Controller berinteraksi dengan model untuk mengambil atau memanipulasi data yang diperlukan.
5. Setelah mendapatkan data dari model, controller mengirimkan data tersebut ke view yang sesuai.
6. View menggunakan data yang diterima untuk merender halaman HTML yang akhirnya dikirim kembali kepada pengguna.
7. Dengan adanya pemisahan logika dalam tiga komponen utama ini, arsitektur Laravel membuat kode lebih terorganisir, 8. mudah dipelihara, dan mudah dikembangkan secara tim. Ini memungkinkan pengembang untuk fokus pada aspek tertentu tanpa harus terjebak dalam kompleksitas keseluruhan aplikasi.

Penggunaan pola desain Model-View-Controller (MVC) di Laravel memfasilitasi aplikasi yang lebih mudah diatur, memungkinkan pengembangan secara modular, dan mempermudah dalam melakukan pengujian dan perubahan.
