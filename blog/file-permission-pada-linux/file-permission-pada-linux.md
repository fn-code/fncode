Kali ini saya akan membahas tentang file permission . Sebelum kita membahas tentang file permission kita harus tahu dulu apa itu file permission.

File permission adalah hak akses bagi user untuk membaca,menulis dan mengeksekusi sebuah file.
Di linux mempunyai 3 hak akses berbeda pada sebuah file, yaitu user (pemilik file) , group dan other

Kegunaan file permission tidak lain adalah untuk keamanan data, untuk menjaga file-file supaya hanya diakses user yang berkepentingan.


#### Berikut adalah tabel permission :

```
# Nilai Oktal

read = 4
write = 2
execute = 1
Total = 7
```

#### Dalam linux terbagi 3 kelas dalam pengaksesan file yaitu :

- user : Pengguna yang mempunyai hak dari suatu file (u).
- group : Grup yang memiliki hak dari suatu file (g).
- other : Pengguna lain yang berada dalam sistem (o).

#### Sifat dan tipe file terdiri atas tiga :
- read (r) : untuk membaca file.
- write (w) : untuk menulis file.
- execute (x) : untuk mengeksekusi file.


#### Contohnya angka numericnya:
```
0 = — -
1 = — x
2 = -w-
3 = -wx
4 = r —
5 = r-x
6 = rw-
7 = rwx
```

#### Dalam pembuatan izin file kita harus menggunakan perintah berikut:
1. Chmod merupakan sebuah perintah yang digunakan untuk menambah dan mengurangi ijin pemakai untuk mengakses file atau direktori. 

```Syntax : chmod <hak akses> <nama file>```

2. chown merupakan sebuah perintah yang digunakan mengganti owner dari suatu file atau direktori, perintah chown ini hanya dapat digunakan oleh root / super user.

```syntax : chown < nama user > < nama file >```

3. chgrp adalah perintah untuk merubah kepemilikan grup terhadap file atau direktori

```syntax : chgrp < nama group > < nama file >```

Untuk cara melihat sebuah permission sebuah file kita bisa melihatnya dengan
perintah di bash console dibawah ini
```shell
$ ls -l
```