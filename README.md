# fundamental-modern-javascript
## template literal

```javascriot
let nama = "fahriz";
console.log(`hello ${nama}`);
```
```javascript
// javascript expression
let x = 10;
let y = 5;
console.log(`hasil dari x * y adalah ${x * y}`);
```

### variabel dan fungsi pada es6 let dan const
```javascript
var a = 20;
/*Namun sebaliknya, variabel x yang dideklarasikan di luar fungsi, dapat diakses dari dalam fungsi. Pada
contoh tersebut, variabel x memiliki scope global karena bisa diakses dari manapun, sedangkan variabel
y scopenya fungsi karena hanya bisa diakses di lingkup fungsi tersebut saja */
function test() {
  var b = 10;
  //   variabel b tidak bisa di akses karena beda scope, karena b di deklarasikan didalam fungsi test sehingga tidak dapat di panggil diluar fungsi
  return a;
}
console.log(test());
console.log(b);
```
```javascript
let x1 = 20;
let y1 = 0;
if (x1 === 20) {
  y1 = 10;
}
console.log(x1);
console.log(y1);
```

```javascript
// iterasi
let i = 200;
for (let i = 0; i <= 5; i++) {
  console.log(i); //akan menghasilkan 1-5 karena variabel i hanya ada pada for
}
// jika memanggilnya di luar for maka akan tampil deklarasi sebelumnya yaiyu 200
console.log(i);

//nilai constanta  tidak berlaku pada pada objek
const person = {
  name: "Fuad",
  age: 35,
};
person.name = "Hafid";
console.log(person);
```

Pada contoh di atas, kita masih bisa menmodifikasi properti name dari objek person meskipun objek
tersebut telah di deklarasikan sebagai konstanta. Nah, untuk membuat agar sebuah objek benar-benar
sebagai konstanta atau nilainya termasuk propertinya tidak dapat diubah lagi maka kita bisa
menyiasatinya dengan menggunakan method freeze

```javascript
const person1 = Object.freeze({
  name: "Fuad",
  age: 35,
});
person1.name = "Hafid";
console.log(person1);
```

```javascript
// arrow function
const getPrice = () => 25000;
// console.log(getPrice);
```

```javascript
// fungsi dengan argumen lebih dari satu
function multiply(a, b) {
  return a * b;
}
```

```javascript
// ES6: arrow function
const multiply = (a, b) => a * b;
```

```javascript
// Sebagaimana fungsi pada umumnya, kita juga bisa memberikan nilai default pada argumen
// ES6: arrow function
const increment = (x = 1) => ++x;
```

```javascript
// reguler function
const Web = {
  teks: "hello",
  render: function () {
    console.log("menampilkan: " + this.teks);
  },
};
console.log(Web.teks); // hello
Web.render();
```

Objek Web pada contoh diatas memiliki satu properti yaitu teks dan satu method yaitu render. Pada
method render, kita bisa mengakses properti teks dengan menggunakan perintah this.teks,
dimana this mengacu pada objek Web.


```javascript
const Web = {
  teks: "hello",
  render: function () {
    setTimeout(function () {
      console.log("menampilkan: " + this.teks);
    }, 1000);
  },
};
console.log(Web.teks); // hello
Web.render();
```

Perbedaanya adalah pada method render, kita tambahkan fungsi setTimeout untuk memberikan jeda
selama 1 detik sebelum menjalankan perintah console.log( 'menampilkan: ' + this.teks ).
Mungkin kita berfikir bahwa kode diatas akan berjalan dengan baik, namun ternyata setelah dijalankan
hasilnya:
hello
menampilkan: undefined
Ternyata this disitu mengacu pada objek Timeout bukan Web. Pemanggilan this hanya bisa dalam
satu level saja, karena this dipanggil di dalam fungsi setTimeout maka otomatis parent terdekatnya
adalah Timeout, meskipun juga berada di dalam objek Web.

```javascript
const Web = {
  teks: "hello",
  render: function () {
    setTimeout(() => {
      console.log("menampilkan: " + this.teks);
    }, 1000);
  },
};
console.log(Web.teks); // hello
Web.render();
```
Dengan menggunakan format arrow function maka konteks this tidak lagi mengacu pada objek
Timeout melainkan objek Web.
```javasript
const Web = {
  teks: "hello",
  render: () => {
    setTimeout(() => {
      console.log("menampilkan: " + this.teks);
    }, 1000);
  },
};
console.log(Web.teks);
Web.render();
```
Wah, mengapa this.teks menghasilkan undefined?
Hal ini disebabkan karena konteks this disitu menjadi tidak mengacu pada objek Web melainkan
mengacu ke objek di atasnya lagi atau jika kita jalankan pada console browser maka this mengacu
pada objek Window.

## Conditional Operator 
Conditional operator ini digunakan ketika kita harus menjalankan statemen berdasarkan kondisi tertentu,
umumnya kita bisa menggunakan if-else atau switch.
Ada dua bentuk conditional operator yang akan kita bahas yaitu ternary operator dan short circuit
evaluation.

### Ternary Operator
Ternary operator atau conditional ternary operator mengacu pada bentuk pendek dari logika if, dimana
kita bisa menuliskannya dalam satu statemen saja.
```javascript
// cara biasa
if (statemen) benar else salah
// ternary operator
statement ? benar : salah
```
```javascript
const nilai = 80
console.log((nilai >= 75) ? 'Lulus' : 'Tidak Lulus')
```
### Short-circuit Evaluation
Short-circuit evaluation artinya pengujian atau evaluasi yang minimal terhadap ekpresi boolean (operator
logika AND && dan OR ||). Evaluasi terhadap ekspresi dilakukan dari kiri ke kanan.
ekspresi1 && ekspresi2
Pada logika AND, evaluasi akan bernilai true hanya jika ekpresi pertama dan kedua bernilai true.
Contoh kedua pada logika OR.
ekspresi1 || ekspresi2
Pada logika OR, evaluasi akan bernilai true hanya jika salah satu saja dari ekpresi bernilai true.

Perhatikan contoh berikut:
```javascript
const auth = true
console.log(auth && 'Selamat datang!') // Selamat datang!
```
Kode di atas artinya jika variabel auth bernilai true maka teks Selamat datang! akan ditampilkan

Perhatikan juga contoh kedua ini:
```javascript
const user = {
 nama: 'Arif',
 umur: 25
}
console.log(user.pekerjaan || 'Pengangguran') // Pengangguran
```
Jika properti pekerjaan tidak didefinisikan maka akan ditampilkan teks Pengangguran
```javascript
const user2 = {
 nama: 'Budi',
 umur: 27,
 pekerjaan: 'Programmer'
}
console.log(user2.pekerjaan || 'Pengangguran') // Programmer
```
Jika properti pekerjaan didefinisikan maka akan ditampilkan nilai dari properti tersebut.
### Optional Chaining
kita memiliki sebuah objek user1 yang memiliki beberapa properti.
```javascript
const user1 = {
 name: 'Burhan',
 street: 'Jl. Jenderal Soedirman 50',
 city: 'Jakarta',
} 
```
Untuk mengakses properti pada objek user maka kita bisa menggunakan karakter titik setelah nama
objek dan diikuti dengan nama propertinya.

```javascript
console.log(user1.name) // Burhan
console.log(user1.street) // Jl. Jenderal Soedirman 50
console.log(user1.city) // Jakarta
```
Disamping menggunakan karakter titik, kita juga bisa mengakses properti pada objek menggunakan
format array
```javascript
console.log(user1['name']) // Burhan
```
Bentuk array ini akan sangat berguna jika nama propertinya bersifat dinamis

Cara mengakses properti dengan menggunakan titik maupun dengan format array ini juga berlaku pada
nested property atau properti yang bertingkat.

```javascript
const user2 = {
 name: 'Doni',
 addrees: {
 street: 'Jl. Dago 30',
 city: 'Bandung'
 }
}
console.log(user2.name) // Doni
console.log(user2.addrees.street) // Jl Dago 30
console.log(user2['addrees']['city']) // Bandung
```
Cara mengakses properti secara bertingkat inilah yang kemudian disebut sebagai chaining.
Lalu apa itu optional chaining?
Optional chaining merupakan bentuk opsional pada pengaksesan suatu properti secara bertingkat


Nah untuk mencegah fatal error itu, kita perlu mengecek terlebih dahulu variabel user3 sebelum kita
akses properti name-nya. Cara singkatnya kita bisa gunakan short-circuit-evaluation and.

```javascript
const user3 = null
console.log(user3 && user3.name) // undefine
```
Kode di atas apabila kita jalankan akan menghasilkan undefined tanpa muncul error. Dengan cara ini
kode kita akan lebih aman dari kemungkinan terjadinya error.

Namun Javascript juga memiliki cara yang lebih singkat lagi untuk mengatasi hal ini yaitu dengan
menggunakan apa yang disebut sebagai optional chaining
Yaitu dengan menambahkan karakter tanda tanya ? sebelum karakter titik pada chaining.

```javascript
const user3 = null
console.log(user3?.name) // undefined
```
Pada kasus nested properti maka optional chaining ini juga berlaku.
```javascript
const user3 = null
console.log(user3?.name) // undefined
console.log(user3?.addrees?.street) // undefined
```

Lalu bagaimana dengan chaining yang menggunakan format array ?
Untuk format array maka gunakan karakter tanda tanya diikuti spasi ?., sebagaimana contoh berikut:
```javascript
const user3 = null
console.log(user3?.['name']) // undefined
console.log(user3?.['addrees']?.['city']) // undefined
```

## Fungsi Pada Array 
### Fungsi map()
Fungsi map() digunakan untuk memetakan suatu array dan melakukan operasi tertentu pada setiap
itemnya kemudian mengembalikan array baru
