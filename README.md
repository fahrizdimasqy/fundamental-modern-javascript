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

### Function
#### High Order Function
fungsi memanggil fungsi sebagai parameter/input
```javascript
Higher order function
function add(num1, num2) {
  return num1 + num2;
}

function substract(num1, num2) {
  return num1 - num2;
}

function multiply(num1, num2) {
  return num1 * num2;
}

function divide(num1, num2) {
  return num1 / num2;
}

function calculator(num1, num2, operator) {
  return operator(num1, num2);
}

calculator(3, 4, add)
```

#### Constructor Function
namanya ditulis huruf awal harus kpaital

```javascript
function BellBoy(name, age, hasWorkPermit, languages) {
//melakuan pencockan input/parameter dengan nama properti
this.name = name;
this.age = age;
this.hashWorkPermit = hasWorkPermit;
this.languages = languages;
}

//menginisialisasi object yang baru / membuat objek
var bellboy1 = new BellBoy("fahriz", 20, 2, ["Indonesia", "English"]);
console.log(BellBoy)

function HouseKeeper(yearsOfExpreince, name, cleaningRepertoire) {
  this.yearsOfExpreince = yearsOfExpreince;
  this.name = name;
  this.cleaningRepertoire = cleaningRepertoire;
  this.clean = function() {
    alert('Cleaning in progress.');
  }
}

var houseKeeper1 = new HouseKeeper(2, "test", "test")
houseKeeper1.clean();
```

##### Callback Function
```javascript
document.addEventListener("keypress", respondToKey(event));

function respondToKey(event) {
  console.log("Key Pressed");
}
```
document adalah high order function karena memiliki fungsi sebagai parameter atau input
disisi lain respondTokey adalah callback function karena menunggu setelah event terjadi baru fungsi tersebut di panggil kembali
dan di eksekusi

### Arrow Function
Arrow function adalah cara alternatif dalam menulis suatu fungsi pada Javascript. Cara ini diperkenalkan
sejak ES6.
Berikut ini sintaksnya:
```javascript
(argumen) => {
 return expression
}
// atau versi shorthand
(argumen) => expression
```
Sebelum ES6, kita menulis fungsi dengan cara sebagai berikut
```javascript
// fungsi tanpa argumen pada ES5
function getPrice() {
 return 25000
}
// atau bisa dengan gaya penulisan variabel
const getPrice = function () {
 return 25000
}
```
Fungsi tersebut dapat ditulis dengan menggunakan ES6 arrow function, menjadi sebagai berikut:
``javascript
// ES6: arrow function
const getPrice = () => {
 return 25000
}
// atau versi shorthand (singkat) dari arrow function
const getPrice = () => 25000
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
Apakah arrow function hanya untuk menyingkat penulisan fungsi?
Ternyata tidak, arrow function juga menyelesaikan masalah pada ruang lingkup keyword this. Keyword
this pada Javascript digunakan untuk menunjuk ke parent objek.
```javascript
const Web = {
 teks: 'hello',
 render: function () {
 console.log( 'menampilkan: ' + this.teks )
 }
}
console.log( Web.teks ) // hello
Web.render() // menampilkan: hello
```
Objek Web pada contoh diatas memiliki satu properti yaitu teks dan satu method yaitu render. Pada
method render, kita bisa mengakses properti teks dengan menggunakan perintah this.teks,
dimana this mengacu pada objek Web
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
Bagaimana jika kodenya kita ubah menjadi sebagai berikut:

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

contoh
```javascript
let user = ["fahriz", "dimas", "naruto", "sasuke", "natsu"];

let userUppercase = user.map((item) => item.toUpperCase());
console.log(userUppercase);
```
Pada setiap iterasinya, nilai dari variabel item akan diubah formatnya menjadi kapital dengan
menggunakan fungsi string toUpperCase() untuk kemudian dikembalikan nilainya.
Hasilnya, variabel array baru atau dalam hal ini usersUpperCase akan memiliki item array yang sama
dengan variabel users namun dengan format huruf kapital.

contoh dalam objek
```javascript
let users = [
 { name: 'Albert'},
 { name: 'Romy'},
 { name: 'Shinta'}
];
let usersUpperCase = users.map((item) => {
 let nameUpperCase = item.name.toUpperCase()
 return { name: nameUpperCase }
});
console.log(usersUpperCase); 
```
Dengan fungsi map() ini, kita juga bisa melakukan transformasi bentuk array of object menjadi bentuk
array biasa dengan cara mengekstraksi data pada setiap item.
Lihat contoh berikut:
```javascript
let users = [
 { id: 1, name: 'Albert' },
 { id: 2, name: 'Romy' },
 { id: 3, name: 'Shinta' },
];
let userIds = users.map((item) => return item.id)
console.log(userIds) // [ 1, 2, 3 ]
```

### Fungsi filter()
Sesuai dengan namanya, fungsi filter() ini digunakan untuk mem-filter atau menyaring suatu array.
Fungsi ini juga bersifat immutable. Adapun Format penulisannya hampir sama dengan fungsi map()
```javascript
const bilangan = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

let ganjil = bilangan.filter((item) => item % 2 === 1);
console.log(ganjil);
```
Contoh lain, misalnya kita hanya ingin menampilkan data user yang jenis kelaminnya laki-laki saja
```javascript
let users = [
 { id: 1, name: 'Albert', gender: 'male' },
 { id: 2, name: 'Romy', gender: 'male' },
 { id: 3, name: 'Shinta', gender: 'female' },
 { id: 4, name: 'Hendra', gender: 'male' },
 { id: 5, name: 'Fenny', gender: 'female' },
 { id: 6, name: 'Desta', gender: 'male' },
];
let maleUsers = users.filter((item) => {
 return (item.gender === 'male')
})
console.log(maleUsers)
/* hasilnya
[
 { id: 1, name: 'Albert', gender: 'male' },
 { id: 2, name: 'Romy', gender: 'male' },
 { id: 4, name: 'Hendra', gender: 'male' },
 { id: 6, name: 'Desta', gender: 'male' }
]
*/
```
### Fungsi reduce() ~3
Fungsi reduce() ini digunakan untuk melakukan operasi tertentu terhadap setiap item dari array. Fungsi
ini juga bersifat immutable.
Berikut ini sintaksnya:
```javascript
result = var_array.reduce((resutSebelumnya, item) => {
 return resutSebelumnya operator item
},
```

contoh dalam bentuk array:
```javascript
const bilangan = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

total = bilangan.reduce((sum, item) => sum + item, 0);
console.log(total);

rata2 = bilangan.reduce((sum, idx, item, array) => {
  sum = sum + idx;
  return idx === array.length - 1 ? sum / array.length : sum;
}, 0);
console.log(rata2);
```

contoh dalam bentuk objek:
```javascript
const cart = [
 {id:1, name:'buku', qty:5, price:7000},
 {id:2, name:'pensil', qty:2, price:4000},
 {id:3, name:'rautan', qty:1, price:2000},
]
const totalBelanja = cart.reduce((total, item) => {
 return total + (item.qty * item.price)
}, 0)
console.log(totalBelanja) // 45000
```

## Spread Operator
Spread operator merupakan fitur yang digunakan untuk melakukan pemecahan atau ekstraksi item pada
suatu array atau string atau objek.
Sintaks spread operator menggunakan tanda tiga titik ....
```javascript
// string
let teks = 'Belajar Javascript'
console.log(teks) // Belajar Javascript
console.log(...teks) // B e l a j a r J a v a s c r i p t
// array
let menus = ['Bakso', 'Sate', 'Gado-gado']
console.log(menus) // [ 'Bakso', 'Sate', 'Gado-gado' ]
console.log(...menus) // Bakso Sate Gado-gado
```

### argument pada fungsi
```javascript
function hitung(a, b, c) {
  return a + b + c;
}

let bilangan = [1, 2, 3];
console.log(hitung(...bilangan));
//  6
```
### Array Concatenation
Kegunaan lain dari spread operator adalah untuk menggabungkan array, jika sebelumnya kita bisa
gunakan method concat pada array.
Perhatikan kode berikut:
```javascript
let arr1 = [0, 1, 2];
let arr2 = [3, 4, 5];
// menggunakan fungsi concat
let arrConcate = arr1.concat(arr2);
console.log(arrConcate); // [ 0, 1, 2, 3, 4, 5 ]
// menggunakan spread operator
let arrSpread = [...arr1, ...arr2];
console.log(arrSpread); // [ 0, 1, 2, 3, 4, 5 ]
```
Termasuk dalam hal menyisipkan array pada suatu array lain menjadi lebih mudah.
```javascript
let numbers1 = ['tiga', 'empat'];
let numbers2 = ['satu', 'dua', ...numbers1, 'lima'];
console.log( numbers2 ); // [ 'satu', 'dua', 'tiga', 'empat', 'lima' ]
```
### Object Concatenation 
Spread operator juga berguna untuk menggabungkan dua objek.
Tanpa spread operator, kita bisa menggunakan fungsi Object.assign().
```javascript
const user = { username: 'alex88', email: 'alex88@gmail.com' };
const profile = { name: 'Alexander', city: 'Moscow' };
const userProfile = Object.assign(user, profile);
console.log(userProfile)
/*
{
 username: 'alex88',
 email: 'alex88@gmail.com',
 name: 'Alexander',
 city: 'Moscow'
}
*/
const user = { username: 'alex88', email: 'alex88@gmail.com' };
const profile = { name: 'Alexander', city: 'Moscow' };
const userProfile = { ...user, ...profile };
console.log(userProfile);
/*
{
 username: 'alex88',
 email: 'alex88@gmail.com',
 name: 'Alexander',
 city: 'Moscow'
}
*/
```
Contoh lain, misalnya ingin meng-copy sebuah array ke variabel lain
```javascript
const user = { name: 'Andi' };
// cara biasa
const copyUser = Object.assign({}, user);
console.log(copyUser);
// spread operator
const copyUser2 = { ...user };
console.log(copyUser2);
```

## Destructuring Assignment 
Destructuring assignment merupakan fitur Javascript yang berfungsi memecah item atau properti dari
sebuah array atau objek ke dalam variabel yang berbeda.

### Array Destructuring
Sebagai contoh, kita akan memecah setiap items pada array menjadi sebuah variabel tersendiri.
Cara yang biasa dilakukan adalah sebagai berikut.

```javascript
const colors = ['merah', 'kuning', 'hijau']
// array destructuring
let [satu, dua, tiga] = colors
console.log(satu) // merah
console.log(dua) // kuning
console.log(tiga) // hijau
```

Kita juga bisa mengambil sebagian item saja dari array. Misalnya item satu dan dua saja
Selain itu, kita juga bisa melewati pengambilan sebagian item dari array. Misal kita ingin mengambil item
pada index satu dan tiga saja.

Terakhir, kita bisa memberikan nilai default pada item, sehingga ketika data item pada array itu ternyata
kosong maka variabel tersebut akan memiliki nilai defaultnya.
Contoh berikut menunjukkan bahwa item ke empat dari array colors sebenarnya tidak didefinisikan,
namun kita berikan nilai biru, sehingga ketika kita cetak variabel empat akan menghasilkan nilai biru
```javascript
const colors = ['merah', 'kuning', 'hijau']
let [satu, dua, tiga, empat='biru'] = colors
console.log(empat) // biru
```
## Object Destructuring
Sebagai contoh, kita akan memecah setiap properti pada objek menjadi sebuah variabel tersendiri. Cara
yang biasa dilakukan adalah sebagai berikut.

```javascript
const user = {
 name: 'Melodi',
 gender: 0,
 age: 24
}
// object destructuring
let { name, gender, age } = user
console.log(name) // Melodi
console.log(gender) // 0
console.log(age) // 24
```
Bentuk lain, jika variabel telah dideklarasikan sebelumnya alias bukan pada saat assignment maka
perlakuannya sedikit berbeda.
```javascript
let name, gender, age
let user = {
 name: 'Melodi',
 gender: 0,
 age: 24
};
// jika variabel telah dideklarasikan sebelumnya maka gunakan tanda
kurung ()
({name, gender, age} = user)
console.log(name) // Budi
console.log(gender) // Budi
console.log(age) // 20
```

Disamping itu, kita bisa memberikan nilai default pada properti, sehingga ketika data properti pada objek
itu ternyata kosong maka variabel tersebut akan memiliki nilai defaultnya.
```javascript
const user = {
 name: 'Melodi',
 gender: 0,
 age: 24
}
let { name, born='Paris' } = user
console.log(name + ' lahir di ' + born) // Melodi lahir di Paris
```
Fitur ini juga dapat diterapkan pada props atau parameter sebuah fungsi. Berikut ini contoh dengan cara
biasa.
```javascript
const user = {
 name: 'Melodi',
 gender: 0,
 age: 24
}
const print = (props) => {
 console.log(props.name + ' umurnya ' + props.age + ' tahun')
}
print(user) // Melodi umurnya 24 tahun
```
Jika menggunakan fitur object destructuring akan menjadi sebagai berikut:
```javascript
const user = {
 name: 'Melodi',
 gender: 0,
 age: 24
}
const print = ({name, gender, age}) => {
 console.log(name + ' umurnya ' + age + ' tahun')
 }
print(user) // // Melodi umurnya 24 tahun
```
Sebuah objek juga bisa kita destrukturisasi kemudian propertinya di-assign ke variabel lain. Contoh
dengan cara biasa.
```javascript
const user = {
 name: 'Melodi',
 gender: 0,
 age: 24
}
const {name: nama, age: umur} = user
console.log(nama) // Melodi
console.log(umur) // 24
```
### Kombinasi Array & Object Destructuring
Array dari objek juga bisa kita destructuring, misalnya untuk mengambil properti name dari objek users
dengan item ke tiga.
```javascript
const users = [
 { id: 1, name: 'Anwar'},
 { id: 2, name: 'Doni'},
 { id: 3, name: 'Mila'}
]
let [,, { name }] = users
console.log(name) // Mila
```
### Kombinasi Destructuring Assignment & Spread Operator
Fitur destructuring assignment juga bisa digunakan bersama dengan fitur spread operator. Spread
operator yang diimplementasikan bersama dengan destructuring assignment inilah yang kemudian
disebut sebagai rest operator.
```javascript
const colors = ['merah', 'kuning', 'hijau']
let [satu, ...lainnya] = colors
console.log(satu) // merah
console.log(lainnya) // [ 'kuning', 'hijau' ]
```
contoh dalam objek
```javascript
const user = {
 name: 'Melodi',
 gender: 0,
 age: 24
};
let {name, ...lainnya} = user
console.log(name) // Melodi
console.log(lainnya) // { gender: 0, age: 24 }
```
## Modularisasi Javascript: Export & Import
Ketika aplikasi kita besar dan kompleks terkadang kita perlu memecah kode menjadi beberapa file yang
berbeda sesuai konteksnya, inilah yang kemudian disebut sebagai module.
Mulai ES6, Javascript kemudian memperkenalkan fitur module, di mana satu module adalah satu file.
Module dapat di-load dengan menggunakan keyword khusus yaitu export dan import.
Keyword export digunakan untuk menandai suatu variabel dan atau fungsi yang nantinya dapat diakses
dari luar module, sebagai contoh: buatlah file hello.js yang isinya sebagai berikut:

export
* helo.js
```javascript
//  hello.js
export function hello(user) {
 alert(`Hello, ${user}!`)
}
```
import
```javascript
 import { hello } from './hello.js'
 hello('Fuad') // akses fungsi hello pada module hello.
 ```
 Kita bisa juga mengaliaskan hasil import kita ke dalam sebuah variabel, misalnya:
 ```javascript
 import * as helper from './hello.js'
helper.hello('Fuad')
```
Jika kita hanya mengkespor satu variabel/function per module, maka kita bisa menggunakan keyword
default.
```javascript
export default function hello(user) {
 alert(`Hello, ${user}!`)
}
```
Lalu pada import menjadi sebagai berikut:
```javascript
import hello from './hello.js'
hello('Fuad')
```

## Asynchronous Programming 
### Callback
Callback adalah salah satu metode untuk menyisipkan fungsi pada sebuah argumen fungsi lainnya untuk
tujan dipanggil lagi dalam fungsi tersebut.
```javascript
function gretting(user, callback) {
  setTimeout(() => {
    callback(`hello ${user}`);
  }, 2000);
}
gretting("fahriz", (props) => console.log(props));
console.log("pertama");
```
Perhatikan bahwa argumen callback pada deklarasi fungsi merupakan fungsi callback yang mana saat
pemanggilan bisa kita akses sebagaimana fungsi biasa (props) => console.log(props).
Lalu, dari mana argumen props pada fungsi callback? atau apa nilainya?
Yap, argumen props pada callback, isinya sesuai dengan deklarasinya. Karena pada deklarasi fungsi
seperti ini callback(Selamat Pagi ${user}!) maka berarti nilai dari argumen props adalah teks
Selamat Pagi ${user}!.

contoh real case
```javascript
function load(url, callback) {
  let xhr = new XMLHttpRequest();
  xhr.onload = function () {
    callback(this.responseText);
  };
  xhr.open("GET", url, true);
  xhr.send();
}
load("https://jsonplaceholder.typicode.com/todos/1", (data) => {
  document.writeln(data);
});
document.writeln("loading ...");
```
### Promise
Promise merupakan fitur untuk proses asynchronous yang diperkenalkan mulai ES6. Pada sebuah
proses asynchronous setidaknya ada dua kemungkinan hasilnya yaitu: berhasil dan gagal.
Nah, promise ini memastikan ada hasil dari sebuah proses asynchronous tersebut, entah itu berhasil
atau gagal

```javascript
let promise = new Promise((resolve, reject) => {
  let xhr = new XMLHttpRequest();
  xhr.onload = function () {
    resolve(this.responseText);
  };
  xhr.onerror = function () {
    reject(`Network Error`);
  };
  xhr.open("GET", "https://jsonplaceholder.typicode.com/todos/1", true);
  xhr.send();
});
promise
  .then((result) => document.writeln(result))
  .catch((error) => document.writeln(error));
document.writeln("loading ...");
```

Terkait dengan request ke web service, Javascript sejak ES6 juga memperkenalkan fitur fetch yang
bekerja dengan menggunakan promise. Berikut ini contoh kode yang hasilnya sama dengan sebelumnya

```javascript
let promise = fetch("https://jsonplaceholder.typicode.com/todos/1");
promise
  .then((response) => response.json())
  .then((json) => document.writeln(JSON.stringify(json)))
  .catch((error) => document.writeln(error));
document.writeln("loading ...");
```

Method then dipanggil dua kali karena fitur fetch akan mengembalikan response dalam bentu object.
Nah untuk mengubahnya menjadi format JSON maka kita bisa gunakan method json() yang
mengembalikan promise juga sehingga kita gunakan method then yang kedua untuk mendapatkan data
response dalam format JSON.


### Promise
Fitur ini berfungsi seperti namanya, yaitu untuk membuat janji. Mari kita analogikan kembali dalam dunia nyata. Ketika kita memesan kopi kepada pelayan, maka secara tidak langsung pelayan tersebut berjanji kepada kita untuk membuatkan kopi kemudian menghidangkannya pada kita. Namun janji bisa hanya tinggal janji. Dalam dunia nyata pun, janji bisa juga tidak terpenuhi, entah itu karena kopi pesanan kita sedang kosong, atau mesin pembuat kopi itu sedang rusak.

Nah, Promise memiliki perilaku yang sama dengan analogi yang digambarkan tadi. Dalam promise terdapat 3 (tiga) kondisi, yakni:

Pending (Janji sedang dalam proses)
Fulfilled (Janji terpenuhi)
Rejected (Janji gagal terpenuhi)
Situs MDN mengatakan Promise merupakan sebuah objek yang digunakan untuk membuat sebuah perhitungan (kode) ditangguhkan dan berjalan secara asynchronous. Untuk membuat objek promise, kita gunakan keyword new diikuti dengan constructor dari Promise:

const coffee = new Promise();
Namun jika kita jalankan kode tersebut, akan mengakibatkan eror seperti ini:

/* ERROR: Promise resolver undefined is not a function */
Di dalam constructor Promise kita perlu menetapkan resolver function atau bisa disebut executor function di mana fungsi tersebut akan dijalankan secara otomatis ketika constructor Promise dipanggil.

```javascript
const executorFunction = (resolve, reject) => {
const isCoffeeMakerReady = true;
if(isCoffeeMakerReady) {
resolve("Kopi berhasil dibuat");
} else {
reject("Mesin Kopi tidak bisa digunakan!")
}
}
const makeCoffee = new Promise(executorFunction);
console.log(makeCoffee);
/* output:
Promise { 'Kopi berhasil dibuat' }
*/
```
Executor function dapat memiliki dua parameter, yang berfungsi sebagai resolve() dan reject()function. Berikut penjelasan detailnya:

resolve() merupakan parameter pertama pada executor function. Parameter ini merupakan fungsi yang dapat menerima satu parameter, biasanya kita gunakan untuk mengirimkan data ketika promise berhasil dilakukan. Ketika fungsi ini terpanggil, kondisi Promise akan berubah dari pending menjadi fulfilled.

reject() merupakan parameter kedua pada executor function. Parameter ini merupakan fungsi yang dapat menerima satu parameter yang digunakan untuk memberikan alasan mengapa Promise tidak dapat terpenuhi. Ketika fungsi ini terpanggil, kondisi Promise akan berubah dari pending menjadi rejected.

Executor function akan berjalan secara asynchronous hingga akhirnya kondisi Promise berubah dari pending menjadi fulfilled/rejected. Pada contoh kode di atas, berikut ini outputnya:

/* output:
Promise { 'Kopi berhasil dibuat' }
*/
Kenapa demikian? Executor function mengeksekusi resolve() dengan membawa data string “Kopi berhasil dibuat”. Coba kita ubah nilai dari variabel isCoffeeMakerReady menjadi false, maka executor function akan mengeksekusi reject() dengan membawa pesan rejection "Mesin Kopi tidak bisa digunakan!".

Dari output yang dihasilkan baik ketika fulfilled ataupun rejected masih berupa Promise, bukan nilai yang dibawa oleh fungsi resolve atau reject itu sendiri. Lantas bagaimana cara untuk mengakses nilai yang dibawa oleh fungsi-fungsi tersebut? Caranya adalah dengan menggunakan method .then() yang tersedia pada objek Promise.

onFulfilled and onRejected Functions
Untuk menangani nilai yang dikirimkan oleh resolve() ketika Promise onFulfilled, kita gunakan method .then() pada objek promise yang kita buat. Lalu di dalammethod .then() kita berikan parameter berupa function yang berguna sebagai handle callback.

```javascript
const executorFunction = (resolve, reject) => {
const isCoffeeMakerReady = true;
if(isCoffeeMakerReady) {
resolve("Kopi berhasil dibuat");
} else {
reject("Mesin Kopi tidak bisa digunakan!")
}
}
const handlerSuccess = resolvedValue => {
console.log(resolvedValue);
}
const makeCoffee = new Promise(executorFunction);
makeCoffee.then(handlerSuccess)
/* output:
Kopi berhasil dibuat
*/
```

makeCoffee merupakan objek promise yang akan menghasilkan resolve() dengan membawa nilai ‘Kopi berhasil dibuat’.
Lalu kita mendeklarasikan fungsi handlerSuccess() yang mencetak nilai dari parameternya.
Kemudian kita memanggil method .then() dari makeCoffee dan memberikan handlerSuccess sebagai parameternya.
etika makeCoffee terpenuhi (fulfilled), maka handlerSuccess() akan terpanggil dengan parameter nilai yang dibawa oleh resolve(). Sehingga output akan menghasilkan “Kopi berhasil dibuat”.
Namun bagaimana jika objek promise menghasilkan kondisi rejected? Bagaimana cara menangani nilai yang dikirimkan oleh reject()?

```javascript
const executorFunction = (resolve, reject) => {
const isCoffeeMakerReady = false;
if(isCoffeeMakerReady) {
resolve("Kopi berhasil dibuat");
} else {
reject("Mesin Kopi tidak bisa digunakan!")
}
}
const handlerSuccess = resolvedValue => {
console.log(resolvedValue);
}
const handlerRejected = rejectionReason => {
console.log(rejectionReason);
}
const makeCoffee = new Promise(executorFunction);
makeCoffee.then(handlerSuccess,handlerRejected);


/* output:
Mesin Kopi tidak bisa digunakan!
*/
```
onRejected with Catch Method
Method .catch() mirip seperti .then(). Namun method ini hanya menerima satu parameter function yang digunakan untuk rejected handler. Method .catch() ini akan terpanggil bilamana objek promise memiliki kondisi onRejected. Berikut contoh penggunaan dari method

```javascript
const executorFunction = (resolve, reject) => {
const isCoffeeMakerReady = false;
if(isCoffeeMakerReady) {
resolve("Kopi berhasil dibuat");
} else {
reject("Mesin Kopi tidak bisa digunakan!")
}
}
const handlerSuccess = resolvedValue => {
console.log(resolvedValue);
}
const handlerRejected = rejectionReason => {
console.log(rejectionReason);
}
const makeCoffee = new Promise(executorFunction);
makeCoffee.then(handlerSucces)
.catch(handlerRejected);


/* output:
Mesin Kopi tidak bisa digunakan!
*/
```

Dengan menggunakan method catch(), kita dapat menerapkan prinsip separation of concerns sekaligus membuat kodenya lebih rapi
### Async & Await
Async Await dalah fitur yang diperkenalkan pada ES2017, digunakan untuk membuat kode asynchronous
namun dengan cara synchronous sehingga lebih mudah dipahami.
Berikut ini sintaks penulisannya:
```javascript
async function getData(url) {
 let result = await fetch(url)
 console.log(result)
}
```
Kalo kita implementasikan pada kasus sebelumnya, maka kodenya menjadi sebagai berikut:
```javascript
const load = async () => {
 let response = await
fetch('https://jsonplaceholder.typicode.com/todos/1')
 let json = await response.json()
 document.writeln(JSON.stringify(json))
}
load()
document.writeln('loading ...')
```
Lalu bagaimana penanganan errornya? kita bisa gunakan try-catch biasa.
```javascript
const load = async () => {
 try {
 let response = await
fetch('https://jsonplaceholder.typicode.com/todos/1')
 let json = await response.json()
 document.writeln(JSON.stringify(json))
 } catch (error) {
 document.writeln(error) // contoh error : TypeError: Failed to
fetch
 }
}
load()
document.writeln('loading ...')
 ```
 ### Async-Await Syntax
 ```javascript
const getCoffee = () => {
            return new Promise((resolve, reject) => {
                const seeds = 100;
                setTimeout(() => {
                    if (seeds >= 10) {
                        resolve("Coffee didapatkan!");
                    } else {
                        reject("Biji kopi habis!")
                    }
                }, 1000)
            })
        }

        async function makeCoffee() {
            const coffee = await getCoffee();
            console.log(coffee);
        }
        makeCoffee();
        ```
Keyword async digunakan untuk memberitahu JavaScript untuk menjalankan fungsi makeCoffee()secara asynchronous. Lalu keyword await digunakan untuk menghentikan proses pembacaan kode selanjutnya sampai fungsi getCoffee() mengembalikan nilai promise resolve.

“Walaupun await menghentikan proses pembacaan kode selanjutnya pada fungsi makeCoffee. Tapi ini tidak akan mengganggu proses runtime sesungguhnya pada JavaScript (global). Karena fungsi makeCoffee berjalan secara asynchronous. Kita tidakdapat menggunakan await tanpa membuat function dalam scope-nya berjalan secara asynchronous.”

Handle onRejected using async/await
Perlu jadi catatan bahwa await hanya akan mengembalikan nilai jika promise berhasil dilakukan (onFulfilled). Lantas bagaimana jika promise gagal dilakukan (onRejected)? Kembali lagi kepada prinsip synchronous code. Kita dapat menangani sebuah eror atau tolakan dengan menggunakan try...catch.

Ketika menggunakan async/await, biasakan ketika mendapatkan resolved value dari sebuah promise, untuk menempatkannya di dalam block try
```javascript
const getCoffee = () => {
            return new Promise((resolve, reject) => {
                const seeds = 9;
                setTimeout(() => {
                    if (seeds >= 10) {
                        resolve("Coffee didapatkan!");
                    } else {
                        reject("Biji kopi habis!")
                    }
                }, 1000)
            })
        }

        async function makeCoffee() {
            try{
            const coffee = await getCoffee();
            console.log(coffee);
            } catch(rejectedReason) {
              console.log(rejectedReason);
            }
        }
        makeCoffee();
        /* output
        Biji kopi habis!
        */
        ```

## This Keyword
Perbedaan karakteristik dari arrow function dan regular function selanjutnya ada pada penggunaan keyword this. Penjelasan dari this sendiri menyusul di materi class. Namun kita akan bahas sedikit mengenai ini untuk menggambarkan perbedaan ketika this digunakan oleh arrow function dan regular function.
Jika sebuah regular function dipanggil dengan menggunakan keyword new. Maka nilainya akan menjadi objek, contohnya:
```javascript
function People(name, age, hobby) {
this.name = name;
this.age = age;
this.hobby = hobby;
}
const programmer = new People("John", 18, ["Coding", "Read book", "Ping-pong"]);
console.log(programmer.name);
console.log(programmer.age);
console.log(programmer.hobby);
/* output:
John
18
[ 'Coding', 'Read book', 'Ping-pong' ]
*/
```
Objek yang dibuat menggunakan function dengan keyword new, sama halnya seperti kita membuat objek seperti menggunakan objek literals { }.
```javascript
const programmer = {
name: "John",
age: 18,
hobby: ["Coding", "Read book", "Ping-Pong"]
}
console.log(programmer.name);
console.log(programmer.age);
console.log(programmer.hobby);
/* output:
John
18
[ 'Coding', 'Read book', 'Ping-pong' ]
*/
```

Jika sebuah regular function dipanggil dengan menggunakan keyword new. Maka nilainya akan menjadi objek, contohnya:
## OOP
Paradigma OOP selalu digambarkan dengan kehidupan nyata. Visualisasi di atas mencontohkan gambaran umum OOP di mana terdapat sebuah blueprint kucing, nilai yang dimiliki kucing, dan kemampuan yang dapat dilakukan olehnya. Dalam OOP blueprint tersebut dikenal dengan class (kelas), nilai yang dimiliki olehnya dikenal dengan properti, kemampuan yang dimilikinya dikenal sebagai behaviour/method dan realisasi dari sebuah blueprint tersebut disebut instance.

### A Class Before ES6
Sebelum ES6, Hal yang paling mendekati dengan class yaitu membuat sebuah objek menggunakan constructor function dan keyword new, lalu untuk menambahkan method kita gunakan konsep prototype.

```javascript
function Car(manufacture, color) {
this.manufacture = manufacture;
this.color = color;
this.enginesActive = false;
}
Car.prototype.startEngines = function () {
console.log('Mobil dinyalakan...');
this.enginesActive = true;
};
Car.prototype.info = function () {
console.log("Manufacture: " + this.manufacture);
console.log("Color: " + this.color);
console.log("Engines: " + this.manufacture ? "Active" : "Inactive");
}
var johnCar = new Car("Honda", "Red");
johnCar.startEngines();
johnCar.info();
/* output:
Mobil dinyalakan...
Manufacture: Honda
Color: Red
Engines active: true
*/
```
Pada kode di atas Car merupakan constructor function yang akan membuat instance Car baru setiapkan kode new Car() dieksekusi. Melalui Car.prototype, method startEngines() dan carInfo() diwarisi pada setiap instance Car yang dibuat, sehingga johnCar (sebagai instance Car) dapat mengakses kedua method tersebut. Teknik dasar ini yang digunakan dalam membuat class di JavaScript sebelum ES6.

### ES6 Classes
Dengan hadirnya class pada ES6, pembuatan class di JavaScript menjadi lebih mudah dan juga penulisannya mirip seperti bahasa pemrograman lain berbasis class. Pembuatan class pada ES6 menggunakan keyword class itu sendiri kemudian diikuti dengan nama class-nya.
```javascript
class Car {
// Sama seperti function constructor
constructor(manufacture, color) {
this.manufacture = manufacture;
this.color = color;
this.enginesActive = false;
}
// Sama seperti Car.prototype.startEngine
startEngines() {
console.log('Mobil dinyalanakan...');
this.enginesActive = true;
}
// Sama seperti car.prototype.info
info() {
console.log(`Manufacture: ${this.manufacture}`);
console.log(`Color: ${this.color}`);
console.log(`Engines: ${this.manufacture ? "Active" : "Inactive"}`);
}
}
const johnCar = new Car("Honda", "Red");
johnCar.startEngines();
johnCar.info();
/* output:
Mobil dinyalanakan...
Manufacture: Honda
Color: Red
engines active: true
```

### Constructor
Deklarasi class menggunakan ES6 memiliki sifat yang sama seperti pembuatan class menggunakan function constructor (seperti contoh sebelumnya). Namun alih-alihmenggunakan function constructordalam menginisialisasi propertinya, class ini memisahkan constructornya dan ditempatkan pada body class menggunakan method spesial yang dinamakan constructor.
```javascript
class Car {
constructor(manufacture, color) {
this.manufacture = manufacture;
this.color = color;
this.enginesActive = false;
}
}
```
constructor biasanya hanya digunakan untuk menetapkan nilai awal pada properti berdasarkan nilai yang dikirimkan pada constructor. Namun sebenarnya kita juga dapat menuliskan logika di dalam constructor jika memang kita memerlukan beberapa kondisi sebelum nilai properti diinisialisasi.constructor biasanya hanya digunakan untuk menetapkan nilai awal pada properti berdasarkan nilai yang dikirimkan pada constructor. Namun sebenarnya kita juga dapat menuliskan logika di dalam constructor jika memang kita memerlukan beberapa kondisi sebelum nilai properti diinisialisasi. Kita juga melihat penggunaan this pada constructor. Konteks dalam class, keyword this merujuk pada instance dari class tersebut. Sehingga this dapat digunakan untuk mengelola properti yang terdapat pada instance.

Kita juga melihat penggunaan this pada constructor. Konteks dalam class, keyword this merujuk pada instance dari class tersebut. Sehingga this dapat digunakan untuk mengelola properti yang terdapat pada instance.

### Instance
Setelah kita membuat class pada JavaScript, lantas bagaimana cara membuat instance dari class tersebut? Tapi sebelumnya, apa itu instance? Instance merupakan objek yang memiliki properti dan method yang telah ditentukan oleh blueprint-nya (class), atau singkatnya adalah objek yang merupakan hasil realisasi dari sebuah blueprint.

Sama seperti constructor function, untuk membuat instance dari class pada ES6 kita gunakan keyword new.
```javascript
class Car {
constructor(manufacture, color) {
this.manufacture = manufacture;
this.color = color;
this.enginesActive = false;
}
}
const johnCar = new Car("Honda", "Red");
```
Pembuatan class menggunakan ES6 lebih ketat dibandingkan dengan constructor function, di mana dalam pembuatan instance wajib menggunakan keyword new.

Kita juga dapat membuat banyak instance dari class yang sama, dan tentunya objek yang kita buat memiliki karakteristik (properti dan method) yang sama. Walaupun sama, namun nilai dari propertinya bersifat unik atau bisa saja berbeda.
```javascript
class Car {
constructor(manufacture, color) {
this.manufacture = manufacture;
this.color = color;
this.enginesActive = false;
}
}
const johnCar = new Car("Honda", "Red");
const adamCar = new Car("Tesla", "Black");
console.log(johnCar.manufacture);
console.log(adamCar.manufacture);
/* output:
Honda
Tesla
*/
```
Variabel johnCar dan adamCar merupakan sebuah objek dari Car. Tentu keduanya akan memiliki properti manufacture, color, dan enginesActive. Namun pada output kita melihat bahwa nilai dari properti kedua objek tersebut berbeda, karena kita dapat memberikan nilai yang berbeda pada saat objeknya dibuat.

Property Accessor
Melalui objek class kita juga dapat mengubah nilai properti seperti ini:
```javascript
class Car {
constructor(manufacture, color) {
this.manufacture = manufacture;
this.color = color;
this.enginesActive = false;
}
}
const johnCar = new Car("Honda", "Red");
console.log(`Warna mobil: ${johnCar.color}`); // output -> Warna Mobil: Red
johnCar.color = "White"; // Mengubah nilai properti color menjadi white
console.log(`Warna mobil: ${johnCar.color}`); // output -> Warna Mobil: White
```
Dengan class kita juga dapat mengimplementasi getter/setter sebuah properti menjadi sebuah method seperti ini:
```javascript
class Car {
constructor(manufacture, color) {
this.manufacture = manufacture;
this._color = color;
this.enginesActive = false;
}
get color() {
return `Warna mobile ${this._color}`;
}
set color(value) {
console.log(`Warna mobil diubah dari ${this._color} menjadi ${value}`);
this._color = value;
}
}
const johnCar = new Car("Honda", "Red");
console.log(johnCar.color); // output -> Warna Mobil: Red
johnCar.color = "White"; // Mengubah nilai properti color menjadi white
console.log(johnCar.color); // output -> Warna Mobil: White
```
Perhatikan juga ketika kita menerapkan getter/setter pada properti class. Kita perlu mengubah atau membedakan penamaan properti aslinya dengan property accessor yang kita buat. Berdasarkan code convention yang ada kita perlu mengubah properti asli class-nya dengan menambahkan underscore di depan nama propertinya (_color). Tanda underscore berfungsi sebagai tanda bahwa properti _color tidak sebaiknya diakses langsung, namun harus melalui property accessor(getter/setter).


### Method
Untuk menambahkan method pada class, kita juga cukup menuliskannya pada body class, tidak perlu melalui prototype seperti menggunakan constructor function.
```javascript
class Car {
constructor(manufacture, color) {
this.manufacture = manufacture;
this.color = color;
this.enginesActive = false;
}
startEngines() {
console.log("Mesin dinyalakan");
this.enginesActive = true;
}
info() {
console.log(`Manufacture: ${this.manufacture}`);
console.log(`Color: ${this.color}`);
console.log(`Engines: ${this.manufacture ? "Active" : "Inactive"}`);}
}
const johnCar = new Car("Honda", "Red");
johnCar.startEngines();
johnCar.info();
/* output:
Mesin dinyalakan
Manufacture: Honda
Color: Red
Engines: Active
*/
```
Dengan menggunakan class, walaupun kita menuliskan method pada body class, namun method tersebut tetap berada pada prototype chain miliki instance yang terbuat. Kita bisa melihat bagaimana objek yang dibuat menggunakan class pada console browser.

### Inheritance
Dalam gambaran dunia nyata, banyak objek yang berbeda tetapi punya kesamaan atau kemiripan tertentu. Contohnya mobil dengan motor memiliki banyak kesamaan karena objek tersebut merupakan kendaraan. Mobil merupakan kendaraan darat begitu juga dengan motor. Mungkin yang membedakan objek tersebut adalah jumlah roda dan kapasitas penumpang yang dapat ditampung.

Sama halnya pada OOP, beberapa objek yang berbeda bisa saja memiliki kesamaan dalam hal tertentu. Di situlah konsep inheritance atau pewarisan harus diterapkan. Pewarisan dapat mencegah kita melakukan perulangan kode.

Dengan teknik inheritance, kita bisa mengelompokkan properti dan method yang sama. Caranya dengan membuat sebuah kelas baru yang nantinya akan diturunkan sifatnya pada

Ketika class Vehicle telah dibuat, kelas lainnya dapat melakukan extends pada kelas tersebut untuk mewarisi sifatnya. Dalam pewarisan, class Vehicle dapat disebut sebagai super atau parent class. Kelas yang mewarisi sifat dari parent class disebut dengan child class.
```javascript
class Vechile {
            constructor(licensePlate, manufacture) {
                this.licensePlate = licensePlate;
                this.manufacture = manufacture;
                this.engineActive = false;
            }
            startEnggines() {
                console.log(`Mesin kendaraan ${this.licensePlate} dinyalakan!`);
            }

            info() {
                console.log(`Nomor Kendaraan: ${this.licensePlate}`);
                console.log(`Manufacture: ${this.manufacture}`);
                console.log(`Mesin: ${this.engineActive ? "Active": "Inactive"}`);
            }

            parking() {
                console.log(`Kendaraan ${this.licensePlate} parkir!`);
            }
        }
        class Car extends Vechile {
            constructor(lisencePlate, manufacture, wheels) {
                super(lisencePlate, manufacture);
                this.wheels = wheels;
            }
            droveOff() {
                console.log(`Kendaraan ${this.licensePlate} melaju!`);
            }
            openDoor() {
                console.log(`Membuka pintu!`);
            }

        }
        const car = new Car("hahaha", "honda", 4);
        car.startEnggines();
```
Dalam melakukan pewarisan kelas, tidak ada tingkatan yang membatasinya. Maksudnya, kita dapat mewariskan sifat kelas A pada kelas B, lalu kelas B mewarisi sifatnya kembali pada kelas C dan selanjutnya. Sama halnya dengan Nenek kita mewarisi sifatnya kepada orang tua kita kemudian orang tua kita mewarisi sifatnya kepada kita.

Static Method
Seluruh kendaraan pasti butuh yang namanya perawatan bukan? Jika iya, tentu kita perlu membuat method repair untuk memperbaiki kendaraan tersebut. Dalam analogi dunia nyata, ketika kendaraan mengalami kerusakan maka kendaraan tersebut akan diperbaiki di bengkel (factory), sehingga kita perlu membuat class baru yang berperan sebagai factory, sebutlah class tersebut VehicleFactory. Di dalam kelas VehicleFactory terdapat satu method repair() yang dapat menerima banyak kendaraan sebagai parameternya.

sebelum ada static method
```javascript
class Vehicle {
constructor(licensePlate, manufacture) {
this.licensePlate = licensePlate;
this.manufacture = manufacture;
this.engineActive = false;
}
/*
kode lainnya
*/
}
/* kode lainnya dalam pembuatan class Car,
Motorcycle, dsb. */
class VehicleFactory {
repair(vehicles) {
vehicles.forEach(vehicle => {
console.log(`Kendaraan ${vehicle.licensePlate} sedang melakukan perawatan`)
})
}
}
const johnCar = new Car("H121S", "Honda", 4);
const dimasCar = new Car("TA1408K", "Tesla", 4);
/* Membuat instance untuk memanggil fungsi repair */
const vehicleFactory = new VehicleFactory();
vehicleFactory.repair([johnCar, dimasCar]);
```
Static method merupakan method yang tidak dapat dipanggil oleh instance dari class, namun dapat dipanggil melalui class-nya sendiri.
```javascript
class Vehicle {
constructor(licensePlate, manufacture) {
this.licensePlate = licensePlate;
this.manufacture = manufacture;
this.engineActive = false;
}
/*
kode lainnya
*/
}
/* kode lainnya dalam pembuatan class Car,
Motorcycle, dsb. */
class VehicleFactory {
static repair(vehicles) {
vehicles.forEach(vehicle => {
console.log(`Kendaraan ${vehicle.licensePlate} sedang melakukan perawatan`)
})
}
}
lass VehicleFactory {
static repair(vehicles) {
vehicles.forEach(vehicle => {
console.log(`Kendaraan ${vehicle.licensePlate} sedang melakukan perawatan`)
})
}
}
const johnCar = new Car("H121S", "Honda", 4);
const dimasCar = new Car("TA1408K", "Tesla", 4);
/* Pemanggilan method repair langsung dari class-nya */
VehicleFactory.repair([johnCar, dimasCar]);
```

### Web Component
Web component merupakan salah satu fitur yang ditetapkan standar World Wide Web Consortium (W3C). Fitur ini memudahkan developer dalam membuat komponen UI websitenya menjadi lebih modular.

Web component bersifat reusable. Bahkan dapat digunakan walaupun kita menggunakan framework sekalipun. Apa pasal? Web component dibangun tak lain menggunakan JS/HTML/CSS murni. Terdapat dua API penting dalam menerapkan web component, yakni:

Custom Elements: Digunakan untuk membuat elemen baru (custom element). Kita juga bisa menentukan perilaku element tersebut sesuai kebutuhan.

Shadow DOM: Digunakan untuk membuat HTML element terenkapsulasi dari gangguan luar. Biasanya digunakan pada custom element, agar elemen tersebut tidak terpengaruh oleh styling yang ditetapkan di luar dari custom elemen-nya.

### Custom Element
HTML memberikan kemudahan dalam mengatur struktur website.

HTMLElement merupakan interface yang merepresentasikan
HTMLElement merupakan interface yang merepresentasikan element HTML. Interface ini biasanya diterapkan pada class JavaScript sehingga terbentuklah element HTML baru melalui class tersebut (custom element).
```javascript
class ImageFigure extends HTMLElement {
}
customElements.define("image-figure", ImageFigure);
```
customElements merupakan global variable yang digunakan untuk mendefinisikan custom elementdan memberitahu bahwa terdapat HTML tag baru. Di dalam customElements terdapat method yang bernama define(). Di sinilah kita meletakan tag name baru kemudian diikuti dengan JavaScript class yang menerapkan sifat HTMLElement.

Setelah mendefinisikan custom element, barulah ia siap digunakan pada berkas HTML. Kita cukup menuliskan tagnya layaknya elemen HTML biasa.
```javascript
<image-figure></image-figure>
```
Jangan lupa lampirkan script pada berkas yang digunakan untuk menuliskan class ImageFigure.
```
<script src="image-figure.js"></script>
```
Berikut kode lengkapnya:

* index.html
```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width">
<title>My First Custom Element</title>
</head>
<body>
<image-figure></image-figure>
<script src="image-figure.js"></script>
</body>
</html>
```
```javascript
class ImageFigure extends HTMLElement {}
customElements.define("image-figure", ImageFigure);
```
Coba jalankan kode di atas pada browser, kita tidak akan mendapatkan apapun.
Sampai saat ini, element <image-figure> berperan layaknya
element <div> ataupun <span> yang tidak memiliki fungsi khusus. Karena kita
belum menetapkan seperti apa jadinya element baru ini.
  
Life Cycle of Custom Element
Ketika sebuah JavaScript class mewarisi sifat dari HTMLElement maka class tersebut akan memiliki siklus hidup layaknya sebuah elemen HTML. Kita dapat menerapkan logika pada setiap siklus hidup yang ada dengan memanfaatkanlifecycle callbacks yang ada. Berikut ini lifecycle callbacks yang ada pada HTMLElemen

* connectedCallback() : Akan terpanggil setiap kali elemen berhasil ditambahkan ke dokumen HTML (DOM). Callback ini merupakan tempat yang tepat untuk menjalankan konfigurasi awal seperti mendapatkan data, atau mengatur attribute.

* disconnectedCallback() : Akan terpanggil setiap kali elemen dikeluarkan (remove()) dari DOM. Callback ini merupakan tempat yang tepat untuk membersihkan data yang masih disimpan pada elemen. Bisa itu event, state, ataupun objek.

* attributeChangedCallback() : Akan terpanggil setiap kali nilai atribut yang di- observe melalui fungsi static get observedAttributes diubah. Callback ini bisa kita manfaatkan untuk memuat ulang data yang ditampilkan oleh elemen.

* adoptedCallback() : Akan terpanggil setiap kali elemen dipindahkan pada dokumen baru. Kita relatif jarang menggunakan callback ini, namun jika kita memanfaatkan tag <iframe> maka callback ini akan terpanggil.

Ketika kita mengimplementasikan constructor pada custom element, kita wajib memanggil method super(). Jika tidak, maka akan menghasilkan error:

ReferenceError: Must call super constructor in derived class before accessing '
this' or returning from derived constructor
Terdapat dua cara membuat instance dari custom element. Yang pertama adalah menggunakan nama tagnya langsung yang dituliskan pada kode HTML. Contohnya:
```
<body>
<image-figure></image-figure>
</body>
```
Lalu cara kedua adalah dengan menggunakan sintaks JavaScript. Sama seperti membuat element HTML biasa, kita gunakan method document.createElement dalam membuat elemen baru.
```javascript
const imageFigureElement = document.createElement("image-figure");
document.body.appendChild(imageFigureElement
```
* index.html
```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width">
<title>Element life cycle</title>
</head> 
<body>
<image-figure></image-figure>
<script src="my-custom-element.js"></script>
<script src="main.js"></script>
</body>
</html>
```
* image-figure.js
```javascript
class ImageFigure extends HTMLElement {
constructor() {
super();
console.log("constructed!")
}
connectedCallback() {
console.log("connected!");
}
disconnectedCallback() {
console.log("disconnected!");
}
adoptedCallback() {
console.log("adopted!");
}
attributeChangedCallback(name, oldValue, newValue) {
console.log(`Attribute: ${name} changed!`);
}
static get observedAttributes() {
return ["caption"];
}
}
customElements.define("image-figure", ImageFigure);
```
* main.js
```javascript
let imageFigureElement = document.querySelector("image-figure");
if (!imageFigureElement) {
imageFigureElement = document.createElement("image-figure");
document.body.appendChild(imageFigureElement);
}
setTimeout(() => {
imageFigureElement.setAttribute("caption", "Gambar 1");
}, 1000);
setTimeout(() => {
imageFigureElement.remove();
 }, 3000);
```
Implementasi lifecycle callback pada custom element bersifat opsional. Kita tidak perlu menuliskannya jika memang tidak diperlukan.

Implementasi lifecycle callback pada custom element bersifat opsional. Kita tidak perlu menuliskannya jika memang tidak diperlukan.

### Custom element attribute and method

### Fetch Basic Usage
Seperti yang sudah kita ketahui, fetch memanfaatkan promise dalam melakukan tugasnya, sehingga network request yang dibuat menggunakan fetch akan selalu berjalan asynchronous.

Network request dilakukan pada saat fungsi fetch() tereksekusi.
```javascript
fetch('http://example.com/movies.json')
  .then(response => response.json())
  .then(data => console.log(data));
  catch (error => {
    console.log(error)});
fetch("https://web-server-book-dicoding.appspot.com/list")
```
Jika request berhasil diproses oleh server, fungsi fetch() akan mengembalikan promise resolve dan membawa response object di dalamnya. Namun nilai response yang dibawa resolve belum sebagai data JSON yang kita butuhkan, melainkan informasi mengenai response itu sendiri, seperti status code, target url, headers, dsb. Maka dari itu, untuk mendapatkan data JSON yang dibutuhkan, kita perlu mengubah response object ke dalam bentuk JSON dengan memanggil method .json().

```javascript
fetch('http://example.com/movies.json')
  .then(response => response.json())
  ```
Method .json() juga mengembalikan nilai Promise, sehingga kita membutuhkan chaining promisedengan menambahkan .then() untuk mendapatkan data JSON yang sesungguhnya.
```javascript
fetch('http://example.com/movies.json')
  .then(response => response.json())
  .then(data => console.log(data));
  ```
Lalu jangan lupa juga untuk menambahkan block catch() pada akhir chaining promise untuk menangani apabila rejected promise terjadi baik karena fungsi fetch() atau json().
```javascript
fetch('http://example.com/movies.json')
  .then(response => response.json())
  .then(data => console.log(data));
  catch (error => {
    console.log(error)});
fetch Asycn/await
async function getBooks() {
try {
    const response = await fetch("https://web-server-book-dicoding.appspot.com/list");
    const responseJson = await response.json();
    console.log(responseJson);
} catch (error) {
console.log(error);
    }
}
getBooks();
```
