[TOC]

# <b>02.</b> ERD

Entity-Relationship Diagram (ERD) adalah representasi grafis dari struktur basis data yang digunakan untuk memodelkan hubungan antara entitas atau objek dalam suatu sistem. ERD memanfaatkan simbol-simbol khusus untuk menggambarkan tabel, kolom, hubungan, dan kunci dalam basis data. Berikut adalah tutorial singkat tentang ERD dan contoh ERD untuk sistem manajemen perpustakaan:

## Entitas
Entitas dalam ERD mewakili objek atau konsep dalam sistem yang akan disimpan dalam tabel. Contoh entitas dalam sistem manajemen perpustakaan mungkin mencakup "buku," "anggota perpustakaan," dan "peminjaman."

## Atribut
Setiap entitas memiliki atribut yang mendefinisikan karakteristik atau properti dari entitas tersebut. Contoh atribut untuk entitas "buku" bisa berupa "judul," "pengarang," "penerbit," dan "tahun terbit."

## Relasi
Relasi atau hubungan menggambarkan keterkaitan antara entitas. Ada tiga jenis relasi utama dalam ERD:
- `One-to-One (1:1)`: Satu entitas pada satu sisi relasi terkait dengan satu entitas pada sisi lainnya.
- `One-to-Many (1:N)`: Satu entitas pada satu sisi relasi terkait dengan banyak entitas pada sisi lainnya.
- `Many-to-Many (N:N)`: Banyak entitas pada satu sisi relasi terkait dengan banyak entitas pada sisi lainnya.

## Kunci
Kunci dalam ERD adalah atribut atau kombinasi atribut yang digunakan untuk mengidentifikasi secara unik setiap baris dalam tabel. Ada dua jenis kunci utama dalam ERD:
1. Primary Key: Kunci utama yang unik untuk setiap entitas dan digunakan sebagai acuan utama untuk mengidentifikasi baris.
2. Foreign Key: Kunci dari entitas lain yang digunakan untuk membentuk hubungan antara tabel.
Contoh ERD untuk Sistem Manajemen Perpustakaan:

Dalam contoh ERD ini, kita akan memodelkan sistem manajemen perpustakaan yang memiliki entitas "buku," "anggota perpustakaan," dan "peminjaman."

```
+--------------+
|    Buku      |
+--------------+
| id (PK)      |
| judul        |
| pengarang    |
| penerbit     |
| tahun_terbit |
+--------------+

+--------------------+
|  AnggotaPerpustakaan |
+--------------------+
| id (PK)              |
| nama                 |
| alamat               |
| telepon              |
+--------------------+

+------------------+
|    Peminjaman    |
+------------------+
| id (PK)          |
| tanggal_pinjam   |
| tanggal_kembali  |
| id_buku (FK)     |
| id_anggota (FK)  |
+------------------+
```

Tabel "Buku" memiliki atribut id sebagai primary key (PK), dan atribut lainnya seperti judul, pengarang, penerbit, dan tahun_terbit.

Tabel "AnggotaPerpustakaan" memiliki atribut id sebagai primary key (PK), dan atribut lainnya seperti nama, alamat, dan telepon.

Tabel "Peminjaman" memiliki atribut id sebagai primary key (PK), dan atribut tanggal_pinjam dan tanggal_kembali untuk mencatat informasi peminjaman. Tabel ini juga memiliki foreign key (FK) id_buku dan id_anggota yang menghubungkannya dengan tabel "Buku" dan "AnggotaPerpustakaan."

ERD di atas memberikan gambaran tentang bagaimana entitas dan hubungan antara entitas diatur dalam sistem manajemen perpustakaan. ERD membantu menggambarkan struktur basis data dengan jelas sehingga dapat membantu dalam perancangan dan pengembangan sistem.

[Lanjut ke Git...](/basic/git)
