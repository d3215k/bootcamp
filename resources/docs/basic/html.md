[TOC]

# <b>02.</b> HTML

HTML (HyperText Markup Language) adalah bahasa markah yang digunakan untuk membuat struktur dan konten dasar halaman web. Halaman web Anda akan terdiri dari elemen HTML yang mengelilingi teks, gambar, tautan, video, dan elemen-elemen lain yang ingin Anda tampilkan.

## Struktur Dasar HTML
Setiap halaman web dimulai dengan elemen `<html>`, yang merupakan elemen induk dari seluruh halaman. Di dalamnya, kita memiliki dua bagian utama, yaitu elemen `<head>` dan elemen `<body>`.
Elemen `<head>` berisi informasi tentang halaman, seperti judul halaman (elemen `<title>`), referensi ke berkas CSS atau JavaScript, dan meta informasi lainnya.
Elemen `<body>` berisi semua konten yang ingin ditampilkan di halaman web, seperti teks, gambar, tautan, dan elemen-elemen lainnya.

```html filename=index.html
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

## Elemen dan Tag
Setiap elemen HTML dibungkus dalam tag. Tag terdiri dari tanda kurung sudut (<>) yang mengelilingi nama elemen. Ada tag pembuka (opening tag) dan tag penutup (closing tag). Misalnya, untuk membuat paragraf, kita menggunakan tag pembuka `<p>` dan tag penutup `</p>`.

Beberapa elemen tidak memerlukan penutup karena mereka dianggap sebagai elemen mandiri yang tidak memiliki konten yang ditempatkan di dalamnya. Elemen-elemen ini disebut self-closing tags. Misalnya, untuk menyisipkan gambar, kita menggunakan tag `<img>` dengan format tag tunggal.

```html
<h1>judul artikel</h1>
<img scr='./images1.png' alt='Deskripsi Gambar'>
<hr>
<p>tag paragraf menggunakan tag pembuka dan penutup</p>
```

Namun, elemen-elemen yang memerlukan penutup harus selalu ditutup dengan menggunakan closing tag untuk mengikuti standar HTML dan memastikan dokumen tetap valid.


## Atribut

Atribut memberikan informasi tambahan tentang elemen dan ditambahkan dalam tag pembuka. Misalnya, pada elemen `<a>`, kita menggunakan atribut href untuk menentukan URL tautan.

```html
<a href="https://www.example.com">Tautan Contoh</a>
```

## Menggunakan Komentar

Anda dapat menyisipkan komentar di dalam kode HTML untuk memberikan penjelasan atau catatan yang hanya terlihat oleh pengembang dan tidak akan ditampilkan di halaman web. Komentar dimulai dengan `<!--` dan diakhiri dengan `-->`.
```html
<!-- Ini adalah contoh komentar -->
```

## Elemen Umum dalam HTML

Beberapa elemen umum dalam HTML antara lain:

Elemen `<h1>`, `<h2>`, ..., `<h6>` menampilkan judul atau heading dengan tingkat kepentingan yang berbeda.

```html
<h1>Judul Utama (H1)</h1>
<h2>Sub Judul (H2)</h2>
<h3>Judul di dalam Sub Judul (H3)</h3>
```

Elemen `<p>` digunakan untuk menampilkan paragraf teks.
```html
<p>Ini adalah contoh paragraf.</p>
```

Elemen `<a>` membuat tautan atau hyperlink ke halaman atau alamat URL lain.
```html
<a href="https://www.contohweb.com">Kunjungi ContohWeb.com</a>
```

Elemen `<img>` untuk menyisipkan gambar pada halaman web.
```html
<img src="gambar.jpg" alt="Deskripsi gambar">
```

Elemen `<ul>` dan `<ol>` untuk membuat daftar tak berurutan dan berurutan.
```html
<ul>
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ul>

<ol>
    <li>Langkah 1</li>
    <li>Langkah 2</li>
    <li>Langkah 3</li>
</ol>
```

`<table>`, `<tr>`, `<th>`, `<td>` Elemen-elemen ini digunakan untuk membuat tabel.
```html
<table>
    <tr>
        <th>Nama</th>
        <th>Usia</th>
    </tr>
    <tr>
        <td>John</td>
        <td>25</td>
    </tr>
    <tr>
        <td>Jane</td>
        <td>30</td>
    </tr>
</table>
```

`<form>`, `<input>`, `<button>`: Elemen-elemen ini digunakan untuk membuat formulir dan elemen input.
```html
<form action="/submit" method="post">
    <label for="nama">Nama:</label>
    <input type="text" id="nama" name="nama" required>
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required>
    <button type="submit">Kirim</button>
</form>
```

`<div>` dan `<span>`: Elemen-elemen ini digunakan untuk mengelompokkan konten dan memberikan gaya atau manipulasi JavaScript.
```html
<div>
    <h3>Ini adalah judul dalam div</h3>
    <p>Ini adalah paragraf dalam div</p>
</div>

<p>Contoh teks <span style="color: red;">ditebalkan</span> dengan span.</p>
```

## Semantik HTML

Semantik HTML adalah konsep yang penting dalam membangun halaman web. Itu berarti menggunakan elemen HTML sesuai dengan arti dan makna mereka. Misalnya, mengggunakan `<header>` untuk bagian header halaman, `<nav>` untuk menu navigasi, `<main>` untuk konten utama halaman, dan sebagainya. Ini membantu mesin pencari dan pembaca layar memahami struktur halaman Anda dengan lebih baik.

```html
<header>
    <h1>Header Situs</h1>
    <nav>
        <ul>
            <li><a href="#home">Beranda</a></li>
            <li><a href="#about">Tentang Kami</a></li>
            <li><a href="#contact">Kontak</a></li>
        </ul>
    </nav>
</header>

<main>
    <section id="home">
        <h2>Selamat Datang di Situs Kami</h2>
        <p>Ini adalah halaman beranda.</p>
    </section>

    <section id="about">
        <h2>Tentang Kami</h2>
        <p>Kami adalah tim yang berdedikasi dalam pembuatan konten edukatif.</p>
    </section>
</main>

<footer>
    <p>Hak Cipta © 2023 ContohWeb.com. Seluruh hak cipta dilindungi.</p>
</footer>

```

[Lanjut ke CSS...](/basic/css)
