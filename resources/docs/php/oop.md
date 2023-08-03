[TOC]

# <b>13.</b> Object Oriented Programming

Object-Oriented Programming (OOP) adalah paradigma pemrograman yang berfokus pada objek-objek dan interaksi di antara mereka. Dalam PHP, OOP memungkinkan Anda untuk membuat class, objek, properti, dan metode. 

## Membuat class
Pertama, mari buat sebuah class bernama `Person` yang akan merepresentasikan entitas orang dengan nama dan usia.
```php filename=person.php
class Person {
    public $name;
    public $age;

    public function __construct($name, $age) {
        $this->name = $name;
        $this->age = $age;
    }

    public function sayHello() {
        return "Halo, nama saya " . $this->name . " dan usia saya " . $this->age . " tahun.";
    }
}
```

## Membuat Objek
Selanjutnya, kita akan membuat objek dari class `Person`.
```php filename=index.php
require_once 'person.php';

$person1 = new Person("John", 30);
$person2 = new Person("Jane", 25);
```

## Mengakses Properti dan Metode
Kita dapat mengakses properti dan metode dari objek yang telah dibuat.
```php filename=index.php 
// (lanjutan)
echo $person1->name; // Output: John
echo $person2->age;  // Output: 25

echo $person1->sayHello(); // Output: Halo, nama saya John dan usia saya 30 tahun.
echo $person2->sayHello(); // Output: Halo, nama saya Jane dan usia saya 25 tahun.
```

## Pewarisan (Inheritance)
Pewarisan memungkinkan class turunan untuk mewarisi properti dan metode dari class induk.
```php filename=student.php
class Student extends Person {
    public $studentId;

    public function __construct($name, $age, $studentId) {
        parent::__construct($name, $age);
        $this->studentId = $studentId;
    }

    public function sayHello() {
        return "Halo, saya adalah seorang mahasiswa dengan nama " . $this->name . " dan usia " . $this->age . " tahun.";
    }
}
```

```php filename=index.php
// (lanjutan)
require_once 'student.php';

$student1 = new Student("Mike", 22, "12345");

echo $student1->sayHello(); // Output: Halo, saya adalah seorang mahasiswa dengan nama Mike dan usia 22 tahun.
```

Dalam contoh di atas, class `Student` merupakan class turunan dari class `Person`, dan kita meng-overwrite metode `sayHello()` untuk memberikan implementasi yang berbeda.

Ini adalah contoh sederhana mengenai OOP di PHP. OOP memungkinkan Anda untuk membuat kode yang lebih terstruktur, modular, dan mudah dipelihara dengan memanfaatkan konsep objek dan pewarisan.

[Lanjut ke SQL Database...](/basic/sql)
