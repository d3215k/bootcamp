[TOC]

# <b>04.</b> CSS 

CSS adalah _declarative language_ yang mengontrol tampilan dan tata letak elemen-elemen HTML di halaman web. Dengan CSS, Anda dapat mengubah warna, ukuran font, margin, padding, tata letak kolom, dan banyak lagi, untuk menciptakan tampilan visual yang menarik dan konsisten.

## Menghubungkan CSS dengan HTML

Untuk menggunakan CSS, Anda perlu menghubungkannya dengan halaman HTML Anda. Ada beberapa cara untuk melakukannya, tetapi cara paling umum adalah dengan menggunakan elemen `<link>` di dalam elemen `<head>` halaman HTML.

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Judul Halaman</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>Selamat datang di halaman saya!</h1>
    <p>Ini adalah contoh paragraf.</p>
</body>
</html>
```

Anda dapat menggunakan atribut `style` pada elemen HTML untuk menentukan gaya langsung pada elemen tersebut.
```html
<!DOCTYPE html>
<html>
<head>
    <title>Judul Halaman</title>
</head>
<body>
    <h1 style="color: blue; font-size: 24px;">Ini adalah judul halaman dengan gaya inline</h1>
    <p style="color: green; font-size: 16px;">Ini adalah paragraf dengan gaya inline.</p>
</body>
</html>
``` 

Dalam contoh di atas, gaya CSS ditentukan langsung pada elemen `<h1>` dan `<p>` menggunakan atribut style. Anda dapat menambahkan gaya tambahan atau mengubah properti gaya secara langsung di dalam atribut style. Namun, cara ini lebih cocok untuk penggunaan yang sederhana dan pada kasus di mana Anda ingin menerapkan gaya khusus hanya pada elemen tertentu. Untuk proyek yang lebih besar dan kompleks, lebih baik menggunakan eksternal CSS yang terpisah untuk mempertahankan struktur dan keterbacaan kode yang lebih baik.

## Selektor CSS

CSS menggunakan selektor untuk menentukan elemen mana yang akan diberi gaya. Selektor dapat berupa tag HTML, kelas, ID, atau bahkan kombinasi dari beberapa elemen.
- Contoh selektor tag HTML: `h1`, `p`, `a`
- Contoh selektor kelas: `.nama-kelas`
- Contoh selektor ID: `#nama-id`

## Properti dan Nilai
Setiap selektor CSS memiliki properti yang menentukan gaya apa yang akan diberikan pada elemen yang dipilih. Properti diikuti oleh tanda titik dua dan diikuti oleh nilai yang menentukan bagaimana properti itu akan diaplikasikan.

```css
h1 { color: blue; }
```

## Komentar

Seperti pada HTML, Anda juga dapat menggunakan komentar dalam CSS untuk memberikan penjelasan atau catatan pada kode CSS Anda. Komentar diawali dengan `/*` dan diakhiri dengan `*/`.

## CSS Box Model

CSS Box Model adalah model yang mendefinisikan cara elemen HTML ditampilkan sebagai kotak dengan komponen-komponen seperti margin, border, padding, dan content. Memahami Box Model akan membantu Anda mengatur tata letak dan ruang antara elemen.

## Penggunaan Kelas dan ID

Anda dapat memberikan gaya kepada elemen-elemen tertentu dengan memberikan mereka atribut kelas atau ID dan menggunakan selektor kelas atau ID di CSS.

```html filename=index.html
<h1 class="judul-halaman">Judul Halaman</h1>
```

```css filename=style.css
.judul-halaman { color: red; }
```

## Pseudo-class dan Pseudo-element

Pseudo-class dan pseudo-element memungkinkan Anda memberikan gaya pada elemen dalam situasi tertentu. Misalnya, Anda dapat mengubah tampilan tautan saat mouse mengarahkannya menggunakan pseudo-class `:hover`.

## Respon Lebar Layar (Responsive Web Design)

CSS juga memungkinkan Anda untuk membuat halaman web responsif dengan menggunakan media query. Dengan media query, Anda dapat mengatur tampilan elemen berdasarkan ukuran layar, sehingga halaman web Anda dapat menyesuaikan diri dengan berbagai perangkat dan ukuran layar.

## Framewok CSS
Selain menguasai dasar-dasar CSS, Anda juga dapat memanfaatkan CSS Framework untuk mempercepat proses pengembangan dan memberikan tampilan yang lebih modern pada halaman web Anda. CSS Framework adalah kumpulan gaya, komponen, dan aturan yang telah diprogram sebelumnya untuk membantu Anda dengan cepat merancang dan mengatur tampilan halaman web. Beberapa CSS Framework populer diantaranya Bootstrap, Bulma, Foundation

## TailwindCSS
Namun, dari berbagai pilihan framework CSS yang sudah disebutkan di atas, Tailwind CSS telah menjadi favorit bagi banyak pengembang Laravel karena pendekatannya yang unik dan sangat fleksibel dalam styling halaman web.

> **Note**
> Pada pembelajaran ini kami menggunakan Tailwind CSS untuk Framework CSS-nya. Selain karena mudah untuk digunakan bahkan untuk pemula yang sedang belajar CSS, juga karena [Starter Kit Breeze](https://laravel.com/docs/10.x/starter-kits#breeze-and-blade) disediakan dengan Tailwind CSS.

Cobalah untuk mempelajari juga Tailwind CSS ini untuk kemudahan nanti dalam menulis css. Selain dari [dokumentasi resmi](https://tailwindcss.com/) yang sudah sangat lengkap, juga sudah banyak artikel dan video tutorial tentang TailwindCSS ini.


[Lanjut ke Javascript...](/basic/js)
