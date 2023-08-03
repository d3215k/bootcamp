[TOC]

# <b>14.</b> SQL

Structured Query Language (SQL) adalah bahasa yang digunakan untuk berinteraksi dengan database. SQL memungkinkan kita untuk mengakses, mengelola, dan mengambil data dari database.

## Membuat Tabel
Pertama, mari kita buat sebuah tabel di database untuk menyimpan data. Misalnya, kita akan membuat tabel "users" dengan kolom "id", "name", dan "age".
```sql
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50) NOT NULL,
    age INT
);
```

## Menyisipkan Data
Setelah tabel dibuat, kita dapat menyisipkan data ke dalamnya.
```sql
INSERT INTO users (name, age) VALUES ('John', 30);
INSERT INTO users (name, age) VALUES ('Jane', 25);
```

## Mengambil Data
Kita dapat menggunakan perintah SELECT untuk mengambil data dari tabel.
```sql
SELECT * FROM users;
```

Hasilnya akan seperti ini:
```
+----+-------+-----+
| id | name  | age |
+----+-------+-----+
| 1  | John  | 30  |
| 2  | Jane  | 25  |
+----+-------+-----+
```

## Menggunakan Kondisi
Kita juga dapat menggunakan kondisi untuk memfilter hasil yang diambil.
```sql
SELECT * FROM users WHERE age > 25;
```

Hasilnya
```
+----+-------+-----+
| id | name  | age |
+----+-------+-----+
| 1  | John  | 30  |
+----+-------+-----+
```

## Memperbarui Data
Perintah UPDATE digunakan untuk memperbarui data yang sudah ada dalam tabel.
```sql
UPDATE users SET age = 26 WHERE name = 'Jane';
```

Setelah perintah di atas dijalankan, data akan berubah menjadi:
```
+----+-------+-----+
| id | name  | age |
+----+-------+-----+
| 1  | John  | 30  |
| 2  | Jane  | 26  |
+----+-------+-----+
```

## Menghapus Data:
Perintah DELETE digunakan untuk menghapus data dari tabel.
```sql
DELETE FROM users WHERE id = 1;
```

Setelah perintah di atas dijalankan, data dengan id = 1 akan dihapus, dan hasilnya menjadi:
```
+----+-------+-----+
| id | name  | age |
+----+-------+-----+
| 2  | Jane  | 26  |
+----+-------+-----+
```

Itulah beberapa konsep fundamental SQL beserta contoh kode untuk masing-masing konsep. SQL sangat penting untuk berinteraksi dengan database dan mengambil data yang dibutuhkan.

[Lanjut ke ERD...](/basic/erd)
