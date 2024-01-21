# penggunaan filament
Jadi, kamu tahu nggak sih, Filament itu suatu bagian dalam Laravel yang membantu kita untuk mengatur data dalam model. Nah, agar Filament bisa bekerja lebih baik, kita perlu melepas "perlindungan" pada model-model kita. Jadi, model-model itu nggak akan terbatas dalam apa yang bisa diubah.
#### filamnet dapat berjalan pada 
- PHP 8.1+
- Laravel v10.0+
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
action nya
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


