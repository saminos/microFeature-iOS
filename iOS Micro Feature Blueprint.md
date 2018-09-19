# iOS Micro Feature Blueprint

Panduan untuk mengerjakan micro feature.



## Dependency

Sebagai *Dependency Inversion* modul ini hanya berisi *public interface* sebagai cara untuk berkomunikasi dengan *object* lain dengan lebih fleksibel

#### Catatan

1. untuk library dari cocoapods atau dari luar sebisa mungkin juga lewat dependency inversion.. jadi gak ada yang import library selain di dependency inversion biar suatu saat jika ada perubahan library yang di pake gak rewrite semua code yang menggunakan library tersebut.
2. harus research API (bukan *network API* tapi tentang *design pattern*) supaya kode jadi konsisten.

####Masalah

1. **module cycle** public interface jika butuh model harus import model? soalnya di sebelumnya ada model yang import dependency buat *modelable* takutnya kalau saling import jadi gak bisa build soalnya saling ketergantungan

####Solusi terdekat

1. **module cycle**
   * *model* tidak boleh import *dependency inversion* jadi *dependency inversion* boleh import *model*
   * interface *modelable* berarti di dalam modul model bukan di modul *dependency*



 ## Model

Model disini di bagi 2, model hasil response dari network yang setiap propertinya harus menggunakan constant `let` jadi gak boleh berubah dan yang kedua adalah model biasa yang berfungsi sebagai OOP semestinya.

1. **Response Model** model yang berfungsi untuk menerjemahkan data dari server
2. **Regular Model** model yang berfungsi sebagai representasi dari kumpulan objek

####Masalah

1. **penempatan model**: kepikiran untuk menempatkan model di modul *data* tapi jika ada controller lain yang hanya perlu model dan tidak perlu data itu harus import data

####Solusi terdekat

1. **penempatan model**
   * di pisah di jadikan satu modul sendiri
   * di modul data tapi untuk mengirim data ke viewController lain gak boleh menggunakan model respon



## Data

Manipulasi data baik yang dari *network* mapun *local storage* di tempatkan di modul ini.

####Catatan

untuk hasil network menggunakan `Result<GenericType>` dan apakah hasil dari local juga menggunakan objek tipe yang sama(?)



## Core

Core untuk utils / helper yang tidak berhubungan dengan UI, misal *extension* CGFloat itu tidak masuk di core karena itu berhubungan dengan UI.



## UI

Semua yang berhubungan dengan UI disini dari warna, font, button, *extension* yang berhubungan dengan *UI* dan lainnya

#### Note

Rencananya modul *UI* ini akan menerapkan ***Component Based Development*** dan atau ***Component Based Design***