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
