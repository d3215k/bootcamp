[TOC]

# <b>07.</b> Collection

Collection dapat kita gunakan untuk memanipulasi array dan kumpulan data lainnya dengan cara yang lebih mudah dan elegan. Collection menyediakan berbagai metode bawaan yang memungkinkan Anda untuk melakukan transformasi, filter, mapping, sorting, dan operasi lainnya pada data tanpa perlu menulis banyak kode.

Collection memungkinkan Anda untuk melakukan banyak operasi data dengan cepat dan efisien, dan biasanya digunakan untuk memproses hasil query dari basis data atau data yang diterima dari request HTTP.

## Membuat Collection
Untuk membuat sebuah collection sangat sederhana seperti berikut
```php
$collection = collect([1, 2, 3]);
```

> **Note**
> Hasil dari query `Eloquent` selalu dikembalikan sebagai instance Collection.

## Beberapa Methode Collection
Berikut beberapa metode Collection yang sering digunakan:

#### push()
Metode push() digunakan untuk menambahkan elemen baru ke dalam Collection di bagian akhir.
```php
$collection = collect([1, 2, 3]);

$collection->push(4);

// Output: [1, 2, 3, 4]
```

#### put()
Metode put() digunakan untuk menambahkan elemen baru ke dalam Collection dengan kunci tertentu.
```php
$collection = collect(['name' => 'John', 'age' => 30]);

$collection->put('email', 'john@example.com');

// Output: ['name' => 'John', 'age' => 30, 'email' => 'john@example.com']
```

#### pop()
Metode pop() digunakan untuk menghapus dan mengambil elemen terakhir dari Collection.
```php
$collection = collect([1, 2, 3, 4]);

$lastElement = $collection->pop();
// Output: 4

// $collection sekarang: [1, 2, 3]
```

#### pull()
Metode pull() digunakan untuk menghapus dan mengambil elemen dari Collection berdasarkan kunci tertentu.
```php
$collection = collect(['name' => 'John', 'age' => 30]);

$age = $collection->pull('age');
// Output: 30

// $collection sekarang: ['name' => 'John']
```

#### toArray()
Metode toArray() digunakan untuk mengonversi Collection menjadi array biasa.
```php
$collection = collect([1, 2, 3]);

$array = $collection->toArray();

// Output: [1, 2, 3]
```

#### toJson()
Metode toJson() digunakan untuk mengonversi Collection menjadi string JSON.
```php
$collection = collect(['name' => 'John', 'age' => 30]);

$jsonString = $collection->toJson();

// Output: {"name":"John","age":30}
```

#### first()
Metode first() digunakan untuk mengambil elemen pertama dari Collection.
```php
$collection = collect([1, 2, 3, 4, 5]);

$firstElement = $collection->first();

// Output: 1
```

#### last()
Metode last() digunakan untuk mengambil elemen terakhir dari Collection.
```php
$collection = collect([1, 2, 3, 4, 5]);

$lastElement = $collection->last();

// Output: 5
```

#### map()
Metode `map()` digunakan untuk mengubah setiap elemen dalam Collection dengan fungsi tertentu.
```php
$collection = collect([1, 2, 3, 4, 5]);

$mapped = $collection->map(function ($item) {
    return $item * 2;
});

// Output: [2, 4, 6, 8, 10]
```

#### filter()
Metode filter() digunakan untuk memfilter elemen dalam Collection berdasarkan kriteria tertentu.
```php
$collection = collect([1, 2, 3, 4, 5]);

$filtered = $collection->filter(function ($item) {
    return $item % 2 == 0;
});

// Output: [2, 4]
```

#### sortBy()
Metode sortBy() digunakan untuk mengurutkan elemen dalam Collection berdasarkan kriteria tertentu.
```php
$collection = collect([
    ['name' => 'John', 'age' => 30],
    ['name' => 'Jane', 'age' => 25],
    ['name' => 'Tom', 'age' => 35],
]);

$sorted = $collection->sortBy('age');

// Output: [['name' => 'Jane', 'age' => 25], ['name' => 'John', 'age' => 30], ['name' => 'Tom', 'age' => 35]]
```

#### reduce()
Metode reduce() digunakan untuk menggabungkan elemen dalam Collection menjadi satu nilai tunggal.
```php
$collection = collect([1, 2, 3, 4, 5]);

$total = $collection->reduce(function ($carry, $item) {
    return $carry + $item;
}, 0);

// Output: 15
```

#### each()
Metode each() digunakan untuk melakukan iterasi pada setiap elemen dalam Collection.
```php
$collection = collect([1, 2, 3, 4, 5]);

$collection->each(function ($item) {
    echo $item . ' ';
});

// Output: 1 2 3 4 5
```

#### contains()
Metode contains() digunakan untuk mengecek apakah data tertentu ada dalam Collection.
```php
$collection = collect([1, 2, 3, 4, 5]);

if ($collection->contains(3)) {
    echo 'Data found!';
}

// Output: Data found!
```

#### pluck()
Metode pluck() digunakan untuk mengambil nilai dari suatu kolom tertentu dari setiap elemen dalam Collection.
```php
$collection = collect([
    ['name' => 'John', 'age' => 30],
    ['name' => 'Jane', 'age' => 25],
]);

$names = $collection->pluck('name');

// Output: ['John', 'Jane']
```

#### count()
Metode count() digunakan untuk menghitung jumlah elemen dalam Collection.
```php
$collection = collect([1, 2, 3, 4, 5]);

$count = $collection->count();

// Output: 5
```

#### sum()
Metode sum() digunakan untuk menghitung jumlah total dari setiap elemen dalam Collection.
```php
$collection = collect([1, 2, 3, 4, 5]);

$total = $collection->sum();

// Output: 15
```

#### isEmpty()
Metode isEmpty() digunakan untuk mengecek apakah Collection kosong atau tidak.
```php
$collection = collect([]);

if ($collection->isEmpty()) {
    echo 'Collection is empty!';
}

// Output: Collection is empty!
```

#### merge()
Metode merge() digunakan untuk menggabungkan dua atau lebih Collection menjadi satu.
```php
$collection1 = collect([1, 2, 3]);
$collection2 = collect([4, 5, 6]);

$merged = $collection1->merge($collection2);

// Output: [1, 2, 3, 4, 5, 6]
```

#### unique()
Metode unique() digunakan untuk menghapus elemen duplikat dari Collection.
```php
$collection = collect([1, 2, 2, 3, 3, 4, 5]);

$unique = $collection->unique();

// Output: [1, 2, 3, 4, 5]
```

#### slice()
Metode slice() digunakan untuk memotong (mengambil) sebagian elemen dari Collection.
```php
$collection = collect([1, 2, 3, 4, 5]);

$sliced = $collection->slice(1, 3);

// Output: [2, 3, 4]
```

#### flatten()
Metode flatten() digunakan untuk "mendatar" (menggabungkan) nested Collection.
```php
$collection = collect([
    [1, 2, 3],
    [4, 5, 6],
]);

$flattened = $collection->flatten();

// Output: [1, 2, 3, 4, 5, 6]
```

#### take()
Metode take() digunakan untuk mengambil sejumlah elemen teratas dari Collection.
```php
$collection = collect([1, 2, 3, 4, 5]);

$firstTwo = $collection->take(2);

// Output: [1, 2]
```

#### reverse()
Metode reverse() digunakan untuk membalik urutan elemen dalam Collection.
```php
$collection = collect([1, 2, 3, 4, 5]);

$reversed = $collection->reverse();

// Output: [5, 4, 3, 2, 1]
```

#### whereIn()
Metode whereIn() digunakan untuk memfilter elemen dalam Collection berdasarkan nilai yang ada dalam array yang diberikan.

```php
$collection = collect([
    ['id' => 1, 'name' => 'John'],
    ['id' => 2, 'name' => 'Jane'],
    ['id' => 3, 'name' => 'Tom'],
]);

$filtered = $collection->whereIn('id', [1, 2]);

// Output: [['id' => 1, 'name' => 'John'], ['id' => 2, 'name' => 'Jane']]
```

#### avg()
Metode avg() digunakan untuk menghitung rata-rata dari setiap elemen dalam Collection.
```php
$collection = collect([1, 2, 3, 4, 5]);

$average = $collection->avg();

// Output: 3
```

Dengan menggunakan metode-metode Collection di atas, Anda dapat dengan mudah dan efisien memanipulasi dan melakukan operasi pada data dalam aplikasi Laravel Anda. Collection merupakan fitur yang sangat kuat dan serbaguna dalam pengembangan aplikasi, yang dapat membantu meningkatkan produktivitas Anda dalam memproses data.
