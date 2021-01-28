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
