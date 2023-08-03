[TOC]

# <b>07.</b> Git

Git adalah sebuah sistem kontrol versi yang digunakan untuk mengelola perubahan dalam kode sumber proyek perangkat lunak.

### Memulai Repository Baru
Untuk memulai sebuah repository baru, gunakan perintah `git init`:
```shell
$ git init
```

### Mengonfigurasi Identitas
Sebelum mulai berkontribusi dalam repository, pastikan Anda mengatur nama dan alamat email Anda untuk identitas:
```shell
$ git config --global user.name "Nama Anda"
$ git config --global user.email "email@anda.com"
```

### Menambahkan File ke Staging Area
Untuk menambahkan file ke staging area (persiapan untuk commit), gunakan perintah `git add`:
```shell
$ git add file1.txt file2.txt
```

### Membuat Commit
Setelah file-file ditambahkan ke staging area, lakukan commit untuk menyimpan perubahan tersebut ke dalam repository:
```shell
$ git commit -m "Deskripsi commit"
```

### Melihat Status Perubahan
Untuk melihat status perubahan dalam repository, gunakan perintah `git status`:
```shell
$ git status
```

### Melihat Riwayat Commit
Untuk melihat riwayat commit dalam repository, gunakan perintah `git log`:
```shell
$ git log
```

### Membatalkan Perubahan pada File
Jika Anda ingin membatalkan perubahan pada file yang belum di-staging, gunakan perintah `git checkout`:
```shell
$ git checkout file.txt
```

### Membatalkan Staging pada File
Jika Anda ingin membatalkan staging pada file yang sudah di-staging, gunakan perintah `git reset`:
```shell
$ git reset file.txt
```

### Menggabungkan Cabang (Branch)
Untuk menggabungkan perubahan dari satu cabang ke cabang utama (biasanya `master`), gunakan perintah `git merge`:
```shell
$ git checkout master
$ git merge feature-branch
```

### Mengambil Perubahan dari Repository Jarak Jauh
Untuk mengambil perubahan dari repository jarak jauh (seperti GitHub), gunakan perintah `git pull`:
```shell
$ git pull origin main
```

### Mengirim Perubahan ke Repository Jarak Jauh
Untuk mengirim perubahan ke repository jarak jauh, gunakan perintah `git push`:
```shell
$ git push origin main
```

### Melihat Perbedaan antara File
Untuk melihat perbedaan antara versi file yang sudah di-commit dengan yang diubah namun belum di-staging, gunakan perintah `git diff`:
```shell
$ git diff file.txt
```

### Membuat Cabang (Branch) Baru
Untuk membuat cabang baru, gunakan perintah `git branch`:
```shell
$ git branch new-feature
```

### Pindah ke Cabang (Branch) Lain
Untuk pindah ke cabang (branch) lain, gunakan perintah `git checkout`:
```shell
$ git checkout feature-branch
```

### Menghapus Cabang (Branch)
Jika Anda sudah selesai dengan suatu cabang, Anda bisa menghapusnya menggunakan perintah `git branch -d`:
```shell
$ git branch -d feature-branch
```

[Lanjut ke PHP Basic...](/php/basic)
