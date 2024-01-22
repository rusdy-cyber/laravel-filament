<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

<p align="center">
<a href="https://github.com/laravel/framework/actions"><img src="https://github.com/laravel/framework/workflows/tests/badge.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>

## Tentang Laravel • [dokumentasi penggunaan](https://github.com/rusdy-cyber/web)
Laravel adalah kerangka aplikasi web dengan sintaksis yang ekspresif dan elegan. Kami percaya pengembangan harus menjadi pengalaman yang menyenangkan dan kreatif agar benar-benar memuaskan. Laravel menghilangkan kesulitan dalam pengembangan dengan memudahkan tugas-tugas umum yang digunakan di banyak proyek web



<p align="center">
    <img src="https://github.com/filamentphp/filament/assets/41773797/8d5a0b12-4643-4b5c-964a-56f0db91b90a" alt="Banner" style="width: 100%; max-width: 800px;" />
</p>

<p align="center">
    <a href="https://github.com/filamentphp/filament/actions"><img alt="Tests passing" src="https://img.shields.io/badge/Tests-passing-green?style=for-the-badge&logo=github"></a>
    <a href="https://laravel.com"><img alt="Laravel v10.x" src="https://img.shields.io/badge/Laravel-v10.x-FF2D20?style=for-the-badge&logo=laravel"></a>
    <a href="https://livewire.laravel.com"><img alt="Livewire v3.x" src="https://img.shields.io/badge/Livewire-v3.x-FB70A9?style=for-the-badge"></a>
    <a href="https://php.net"><img alt="PHP 8.1" src="https://img.shields.io/badge/PHP-8.1-777BB4?style=for-the-badge&logo=php"></a>
</p>


# penggunaan filament
Filament adalah kumpulan komponen full-stack untuk mempercepat pengembangan Laravel. Mereka dirancang dengan indah, intuitif untuk digunakan, dan dapat diperluas sepenuhnya - titik awal yang sempurna untuk aplikasi Laravel Anda berikutnya. Mengapa membuang-buang waktu untuk membuat fitur yang sama berulang kali?
#### filamnet dapat berjalan pada 
- PHP 8.1+
- Laravel v10.0+
### Panel Builder • [Documentation](https://filamentphp.com/docs/panels) • [Demo](https://demo.filamentphp.com)
Panel Builder adalah fondasi Filamen. Menggabungkan semua paket bersama-sama, memungkinkan Anda dengan cepat membangun panel admin Laravel, aplikasi yang berhubungan dengan pelanggan, platform Perangkat Lunak sebagai Layanan, dan banyak lagi. Filament membuat antarmuka berbasis CRUD khusus terasa mudah untuk dibuat dan diterapkan.
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
### membuat model
```
php artisan make:model section -m
```
### membuat tabel di panel
```
composer require doctrine/dbal --dev
```
### membuat resourcs menu pada panel
```
php artisan make:filament-resource Customer --generate
```
### jika ingin resource  yang sederhana
```
 php artisan make:filament-resource setting --simple
```
action untuk meampilkan data saat di eedit
```
Tables\Actions\EditAction::make()->form(function (Setting $record){
                    switch($record->type){
                        case 'text' :
                            return [Forms\Components\RichEditor::make('value')->label(
                                $record->label)];
                            break;
                    }
                }),
```
### membuat card 1 baris
ubah pada resources filament
```
return $form
            ->schema([
                Card::make()->schema([

                   
                    ]),
```
### membuat link untuk menampilkan gambar
dan merubah url link pada .env ke ip dan port yang di pakai
```
php artisan storage:link
```
### edit section agar ketika foto di hapus maka record juga terhapus pada panel admin
```
protected function getActions(): array
    {
        return [
            Actions\DeleteAction::make()->after(
                function(section $record){
                    if($record->thumbnail){
                        Storage::disk('public')->delete($record->thumbnail);
                    }
                }
            ),
        ];
    }
```
menghapus menggunakan bulk
```
->bulkActions([
                Tables\Actions\DeleteBulkAction::make()->after(function (Collection 
                $records){
                    foreach($records as $key => $value){
                        if($value->tumbnail){
                            Storage::disk('public')->delete($value->tumbnail);

                        }
                    }
                }),
            ]);
```
menghapus rekord yang berada di model
```
use HasFactory;
    protected $fillable = ['title','thumbnail','content','post_as'];

    protected static function boot()
    {
        parent::boot();
        static::updating(function($model){
            if($model->isDirty('thumbnail') && ($model->getOriginal('thumbnail') !== null)){
                Storage::disk('public')->delete(($model->getOriginal('thumbnail')));
            }
        });
    }
```
membuat agar helpers dapat di jalankan
```
composer dump-autoload
```




