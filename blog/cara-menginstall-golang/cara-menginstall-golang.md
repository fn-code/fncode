![Gopher image](https://golang.org/doc/gopher/fiveyears.jpg)
*Gopher image by [Renee French][rf], licensed under [Creative Commons 3.0 Attributions license][cc3-by].*

Sebelum mengintall golang saya akan menjelaskan apa itu golang terlibih dahulu. Golang adalah sebuah bahasa pemograman yang dikembangkan di ***Google*** oleh ***Robert Griesemer***, ***Rob Pike***, dan ***Ken Thompson*** pada tahun 2007 dan mulai diperkenalkan di publik tahun 2009. Bahasa pemograman ini paling banyak digunakan untuk pada bagian backend.

Langkah-langkah dalam menginstall bahasa pemograman GO atau Golang adalah sebagai berikut.

1. ***Download source atau binary release***
<br>Binary golang dapat di download disini. kalian dapat memilih binary sesuai jenis dan arsitektur operating sistem yang digunakan, mulai dari Linux, MacOS, dan Microsoft.
2. ***Pemasang Atau Pengistalan Go binary***
<br>Pasa sistem operasi linux, setelah binary go selesai di download, buka terminal dan masuk pada lokasi tempat binary go didownload, kemudian ketikan perintah

```shell
tar -C /usr/local -xzf go$VERSION.$OS-$ARCH.tar.gz
```

Setelah proses instalasi selesai set environtment variabel khusus pada sistem operasi linux.

```shell
export GOROOT=/usr/local/go
export PATH=$PATH:$GOROOT/bin
export GOPATH=/go
export GOBIN=/go/bin
```

Dan sedangkan pada windows anda klik atau open golang msi installer. dan ikuti langkah petunjuk untuk meninstall go. secara default lokasi folder instalasi go akan tersimpan di c:\Go. setelah proses instalasi pada windows selesai set environment variable windows untuk go yaitu: GOPATH,GOBIN, dan GOROOT. setelah itu restart komputer atau laptop anda untuk melihat perubahan.

3. ***Uji Coba Instalasi***
<br>Setelah proses instalasi selesai, buat sebuah folder sebai tempat project-project go yang akan kita buat. dalam folder tersebut buat kembali 3 folder dengan nama yaitu bin, pkg, dan src.

Selanjutnya buat go file dengan nama hello.go yang di simpan dalam folder src. seperti pada dibawah ini.

```go
package main

import (
  "fmt"
)

func main() {
  fmt.Println("hello from go")
}
```

Selanjutnya untuk menjalankan go program yaitu dengan cara ketikan perintah go run hello.go

Jika berhasil maka akan tampil pesan “hello from go”. dan proses instalasi go telah berhasil.