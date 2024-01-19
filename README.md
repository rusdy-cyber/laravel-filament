# penggunaan filament
Jadi, kamu tahu nggak sih, Filament itu suatu bagian dalam Laravel yang membantu kita untuk mengatur data dalam model. Nah, agar Filament bisa bekerja lebih baik, kita perlu melepas "perlindungan" pada model-model kita. Jadi, model-model itu nggak akan terbatas dalam apa yang bisa diubah.
### instalasi
```
composer require filament/filament
```
### membuat user acaount admin
```
 php artisan make:filament-user
```
masuk ke panel admin menggunakan /admin pada dns
contoh :
```
http://127.0.0.1:8000/admin
```
