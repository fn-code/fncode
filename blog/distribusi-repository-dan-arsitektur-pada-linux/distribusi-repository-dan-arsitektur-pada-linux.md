Kali ini saya akan membahas mengenai distribusi,repository,arsitektur pada linux.

Pertama yang kita bahas yaitu repository

### Pengertian Repository
Kumpulan dari berbagai macam aplikasi yang berasal di internet, dikumpulkan menjadi satu, dikemas pada media DVD (contohnya) termasuk didalamnya software aplikasi, games, multimedia, internet, office, themes.
Dengan file repository, Anda dapat melakukan instalasi program apa saja yang terdapat dalam repository Ubuntu tanpa perlu terhubung dengan Internet. Saat ini repository Ubuntu bisa di-download dan dimasukkan ke DVD sehingga dapat didistribusikan dengan mudah.

### Arsitektur sistem operasi Linux
Arsitektur sistem operasi UNIX/ Linux terdiri dari 4 komponen penting yaitu kernel, shell, utilitas, dan aplikasi (user program). Berikut penjelasan dari masing-masing komponen:

1. Kernel
   <br>Kernel merupakan inti dari sistem Linux, yang digunakan untuk mengontrol hardware dan membentuk berbagai fungsi peretas rendah.
2. Shell
<br>Shell adalah penerjemah (command line interpreter) pada Linux. Atau yang sering dikenal dengan terminal. Perangkat lunak inilah yamg menjadi jembatan antara user dan sistem Linux. User cukup memberikan perintah dan shell yang akan mengeksekusi perintah yang diberikan.
3. Utilitas
<br>Utilitas atau utility merupakan program yang disediakan sistem Linux untuk melaksanakan tugas tertentu.
4. Aplikasi (user program)
<br>dibuat oleh user, untuk memenuhi kebutuhan sendiri. Program-program tersebut dapat dibuat menggunakan utilitas, perintah built-in pada shell, atau dibuat mengguanakan bahasa pemrograman seperti java, C, C++, python dan berbagai development tool seperti Oracle dan Informix. Selain itu juga dapat berupa program paket yang dibeli dari developer software.

<hr>

### Distribusi linux
(singkatan dari distribusi Linux) adalah sebutan untuk sistem operasi komputer dan aplikasinya, merupakan keluargaUnix yang menggunakan kernel Linux. Distribusi Linux bisa berupa perangkat lunak bebas dan bisa juga berupa perangkat lunakkomersial seperti Red Hat Enterprise, SuSE, dan lain-lain.

Distro ini telah menghasilkan puluhan distro turunan, antara lain Ubuntu, Knoppix,Xandros, DSL, dan sebagainya.

#### Distribusi GNU/Linux itu terdapat 2 macam model distribusi packages, yaitu:
1. Binary Package
<br>Model ini dibuat untuk tujuan penggunaan secara umum, maksudnya penggunaan secara umum disini adalah agar dapat dijalankan di semua tipe dan arsitektur komputer. Biasanya distribusi ini juga tidak menggunakan opsi-opsi khusus yang terdapat di salah satu tipe atau arsitektur komputer tertentu. Sedangkan yang bisa dikategorikan dengan Binary Packages ini adalah semua packages yang ber-ekstensi *.deb, *.rpm, *.tgz dan *.txz, jadi jika menginstall sebuah aplikasi menggunakan repository maka itu berarti kita menginstall dari Binary Packages yang memang sudah disediakan untuk kebutuhan komputer kita.
2. Source Package
<br>Seperti pada namanya distribusi ini menyertakan file source code asli dari aplikasi-nya. Biasanya pihak pengembang pasti menyertakan atau menyediakan distribusi model ini untuk di download. Sedangkan untuk end-user, bisa menggunakan source code ini jika para pengembang tidak menyertakan Binary Packages untuk distribusi GNU/Linux yang digunakan .Coba bayangkan jika kita membuat sebuah aplikasi yang targetnya adalah Sistem Operasi GNU/Linux, installer model seperti apa yang akan kita pilih dengan banyak-ya distribusi GNU/Linux? Mau buat satu-persatu untuk tiap distribusi? Ya pasti capek kan, cara yang paling mudah yaitu, sediakan-lah source code dari aplikasi kita dan kemudian biarkan komunitas GNU/Linux sendiri yang membuatkan binary packages untuk aplikasi kita. Lebih gampang kan? Salah satu contoh dari source code adalah *tar.gz, *tar.bz, *tar.bz2, dll.

