[TOC]

# <b>02.</b> CSS 

CSS adalah _declarative language_ yang mengontrol tampilan dan tata letak elemen-elemen HTML di halaman web. Dengan CSS, Anda dapat mengubah warna, ukuran font, margin, padding, tata letak kolom, dan banyak lagi, untuk menciptakan tampilan visual yang menarik dan konsisten.

## Menghubungkan CSS dengan HTML

Untuk menggunakan CSS, Anda perlu menghubungkannya dengan halaman HTML Anda. Ada beberapa cara untuk melakukannya, tetapi cara paling umum adalah dengan menggunakan elemen `<link>` di dalam elemen `<head>` halaman HTML.
Contoh: `<link rel="stylesheet" href="styles.css">`

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
Selain menguasai dasar-dasar CSS, Anda juga dapat memanfaatkan CSS Framework untuk mempercepat proses pengembangan dan memberikan tampilan yang lebih modern pada halaman web Anda. CSS Framework adalah kumpulan gaya, komponen, dan aturan yang telah diprogram sebelumnya untuk membantu Anda dengan cepat merancang dan mengatur tampilan halaman web. Berikut adalah beberapa CSS Framework populer dan mengapa Tailwind CSS menjadi pilihan yang baik:

### Bootstrap
Bootstrap adalah salah satu CSS Framework yang paling populer dan komprehensif. Ini menawarkan berbagai komponen UI yang sudah jadi, seperti tombol, formulir, navigasi, dan banyak lagi. Bootstrap juga mendukung responsif web design dan memiliki dokumentasi yang kaya.

### Bulma
Bulma adalah CSS Framework yang ringan, fleksibel, dan mudah digunakan. Ini menggunakan gaya modern dengan struktur kelas yang intuitif. Bulma memiliki banyak komponen yang dapat langsung Anda gunakan untuk membangun tampilan halaman web yang menarik.

### Foundation
Foundation adalah CSS Framework lain yang kuat dan dapat disesuaikan. Ini menawarkan tata letak yang responsif, berbagai gaya tombol dan formulir, serta beragam komponen UI lainnya. Foundation cocok untuk proyek besar yang membutuhkan kontrol penuh atas tampilan halaman web.

### TailwindCSS
Namun, dari berbagai pilihan di atas, Tailwind CSS telah menjadi favorit bagi banyak pengembang karena pendekatannya yang unik dan sangat fleksibel dalam styling halaman web.

Berikut adalah alasan mengapa Tailwind CSS merupakan pilihan yang baik:

#### 1. Utility-First Approach

Tailwind CSS mengadopsi pendekatan "utility-first," yang berarti Anda menggabungkan kelas utilitas untuk mencapai gaya yang diinginkan. Ini memberikan fleksibilitas yang tinggi dan menghilangkan kebutuhan untuk menulis CSS khusus. Dengan menggunakan kelas-kelas utilitas yang sudah ada, Anda dapat dengan mudah mengatur tampilan elemen.

#### 2. Konfigurasi Kustom
Tailwind CSS memungkinkan Anda mengonfigurasi dan menyesuaikan tema tampilan Anda sesuai kebutuhan proyek. Anda dapat menyesuaikan warna, ukuran, margin, padding, dan banyak lagi dengan mudah melalui file konfigurasi.

#### 3. Responsif secara Bawaan
Tailwind CSS telah menyediakan kelas-kelas utilitas untuk pengaturan tampilan responsif secara bawaan. Anda dapat dengan mudah menyesuaikan tampilan halaman web Anda untuk berbagai ukuran layar dan perangkat.

#### 4. Dokumentasi Lengkap dan Komunitas yang Aktif
Tailwind CSS memiliki dokumentasi yang lengkap dan mudah diikuti. Selain itu, Tailwind CSS memiliki komunitas yang besar dan aktif, sehingga Anda dapat dengan mudah menemukan bantuan dan dukungan dari komunitas dalam perjalanan pengembangan Anda.

#### 5. Ringan dan Cepat
Tailwind CSS adalah CSS Framework yang ringan dan memiliki ukuran file yang kecil. Ini berarti halaman web Anda akan memuat dengan cepat dan memberikan pengalaman yang baik kepada pengguna.

[Lanjut ke Javascript...](/basic/js)
