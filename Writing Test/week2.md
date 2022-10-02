# Writing Test Week 2

## **Summary Module 6 part II - Scope and Function**

### **Scope**

- Scope mengacu pada aksesibilitas suatu variabel
- Ibarat sebuah kendaraan, kendaraan pribadi seperti motor hanya bisa diakses oleh pemiliknya sendiri, sedangkan kendaraan umum seperti bus dapat diakses oleh semua orang

### **Blocks**

- Blocks merupakan kumpulan kode yang diapit oleh kurung kurawal

### **Global Scope**

- Variabel yang dideklarasikan di luar suatu blocks
- Dapat diakses dimanapun

  ```
  let angka = 1

  if(angka > 0){
      angka -= 1; //angka dapat diakses di dalam block
  } else {
      console.log("habis")
  }
  ```

### **Local Scope**

- Variabel yang dideklarasikan di dalam block
- Hanya dapat diakses di dalam block tersebut

```
function sum(a, b) {
    let total = a +b;
    return total;
}

console.log(total)
//akan terjadi error karena merupakan local scope
```

### **Function**

- Suatu blok kode yang dapat digunakan berulang kali
- Bertujuan untuk meningkatkan efisiensi penulisan

  ```
  function identifier(parameter) {
      statement;
  }

  identifier(argument);
  ```

### **Parameter dan Argumen**

- Dengan parameter, function dapat menerima input nilai untuk kemudian diproses dalam block
- Argumen merupakan nilai input yang diberikan ketika function dipanggil

  ```
  function sum(a, b) {
      return a + b; // a dan b adalah parameter
  }

  let total = sum(10, 20); // 10 dan 20 adalah argument
  ```

### **Default Parameter**

- Nilai default yang akan digunakan jika argumen tidak diberikan

  ```
  function greet(name="Rendra") {
      console.log(`Hello ${name}`)
  }

  greet() // akan menampilkan "Hello Rendra"
  greet("Pramana") // akan menampilkan "Hello Pramana"
  ```

### **Function Helper**

- Suatu function dapat digunakan di dalam function lainnya

  ```
  function multiplyByNineFifths(number) {
  return number * (9/5);
  };

  function getFahrenheit(celsius) {
  return multiplyByNineFifths(celsius) + 32;
  };

  getFahrenheit(15); // Returns 59
  ```

### **Arrow Function**

- Cara penulisan function yang baru pada ES6
- Berfungsi untuk memperingkas penulisan kode

- zero parameter

  ```
  const identifier = () => {};
  ```

- one parameter

  ```
  const identifier = param => {};
  ```

- two or more parameter

  ```
  const identifier = (param1, param2) => {};
  ```

- single line block

  ```
  const identifier = param => statement;
  ```

- multi line block

  ```
  const identifier = param => {
  statement1;
  statement2;
  statement3;
  return statement4;
  }
  ```

---

## **Summary Module 6 part III - Data Type Built in Prototype & Method**

### **Tipe Data Javascript**

- Javascript merupakan bahasa dengan tipe yang dinamis
- Dinamis: variabel dapat diberi atau diganti nilainya dengan tipe data yang berbeda-beda
- Terdapat dua tipe data pada Javascript, yaitu primitive dan non primitive

### **Tipe Data Primitive**

- Tipe data yang tidak dapat diubah behavior-nya
- Tidak memiliki method dan property
- Contoh tipe data primitive:
  - string: data berupa teks
  - number: data berupa angka
  - bigint: data berupa angka yang melebihi limit number
  - boolean: data logika bernilai true dan false
  - undefined: data kosong karena belum diinisialisasi
  - null: data yang sengaja dikosongkan

### **Tipe Data Non Primitive**

- Tipe data hasil penurunan tipe data primitive
- Disebut juga reference data type karena isinya hanyalah address, bukan nilai asli
- memiliki property dan method
- Object adalah tipe data non primitive pada Javascript

### **Object**

- Kumpulan dari properti dan method yang ditulis dalam pasangan key-value
- Properti diibaratkan informasi yang dimiliki object

  ```
  const person = {
    firstName:"John",
    lastName:"Doe",
    age:50,
    eyeColor:"blue"
  };
  ```

- Method merupakan fungsi atau aksi yang dapat dijalankan objek

  ```
  const person = {
    firstName: "John",
    lastName: "Doe",
    id: 5566,
    fullName: function() {
      return this.firstName + " " + this.lastName;
    }
  };
  ```

### **Object Constructor**

- Diibaratkan sebagai blueprint dari object
- Misal object car dapat memproduksi berbagai jenis mobil

  ```
  function Car(model, color, year) {
    this.model = model;
    this.color = color;
    this.year = year;
  }

  const myCar = new Car('Avanza', 'Silver', 2015)
  const friendCar = new Car('Ertiga', 'White', 2018)
  ```

### **Prototype**

- Properti dan method yang selalu dimiliki oleh function dan object yang diwariskan ke satu sama lain
- Bisa juga membuat properti dan method baru ke dalam object
```
String.prototype.reverse = function(){
  let s = ""
  for (let i = String(this).length-1; i >= 0 ; i--) {
    s = s + String(this)[i]
  }

  return s
}

// method yg dimiliki oleh string
console.log("hallo".reverse())
```

### **Method**

- Fungsi yang dimiliki oleh object Javascript
- Ada banyak method yang tersedia oleh object bawaan Javascript

### **Contoh Build-in Property dan Method Javascript**
Object String
- `.length` mengembalikan panjang string
- `.toUpperCase()` mengubah string menjadi huruf kapital
- `.toLowerCase()` mengubah string menjadi huruf kecil
- `.charAt()` mengembalikan karakter pada indeks tertentu
- `.includes()` mengembalikan nilai true jika mengandung string tertentu
- `.split()` memecah string menjadi sub array

Object Number
- `isNaN()` mengembalikan nilai true jika data bukan berupa angka
- `toFixed` mengubah banyaknya bilangan di belakang koma

Math
- `.PI` mengembalikan nilai Phi
- `.abs()` mengubah angka menjadi nilai absolut
- `.ceil()` membulatkan angka ke atas
- `.floor()` membulatkan angka ke bawah
- `.round()` membulatkan angka
- `.random()` mengembalikan angka random

---

## **Summary Module 6 part IV - Introduction to DOM**

### **Document Object Model**
- Struktur dokumen HTML berupa object dengan susunan tree
- Object tersebut dapat diakses dan dimanipulasi dengan bahasa pemrograman
- Menjembatani HTML dan Javascript
- File HTML diparsing dan ditokenisasi oleh browser sehingga menghasilkan DOM

### **Proses Rendering DOM yang Optimal**
- Cantumkan tag script sedini mungkin agar script segera diunduh
- Agar proses unduhan tidak menghentikan parsing HTML, gunakan atribut `defer`
- Meskipun script telah selesai diunduh, ia tidak akan dijalankan sampai parsing HTML selesai
- Mengatasi masalah manipulasi DOM yang masih kosong karena belum diparsing

### **DOM Traversal**
- DOM memiliki struktur berupa node-node yang tergabung dalam sebuah tree
- node-node dapat berisi elemen-elemen penyusun HTML
- Node dan elemen tersebut dapat diakses melalui nama maupun relasinya dalam struktur tree

### **Traversing ke Bawah**
- `getElementByID()` mengembalikan elemen dengan id yang ditentukan
- `getElementsByClassName()` mengembalikan kumpulan elemen HTML yang memiliki class tertentu
- `getElementsByTagName()` mengembalikan kumpulan elemen HTML yang termasuk dalam tag tertentu
- `querySelector()` mengembalikan elemen pertama yang ditemui jika sesuai dengan spesifikasi
- `querySelectorAll()` mengembalikan kumpulan node yang sesuai dengan spesifikasi
- `.children` mengembalikan kumpulan elemen HTML yang merupakan anak dari elemen tersebut

### **Traversing ke Atas**
- `.parentElement` mengembalikan elemen parent dari elemen tersebut
- `.closest()` mengembalikan elemen yang sesuai dengan CSS selector dengan traverse ke atas

### **Traversing ke Samping**
- `.nextElementSibling` mengembalikan elemen selanjutnya yang masih setara levelnya dalam tree (sibling)
- `.previousElementSibling` mengembalikan elemen sebelumnya yang masih setara levelnya dalam tree

---

## **Summary Module 6 part V - DOM Manipulation**

### **HTML Elements**
- Objek elemen merupakan representasi dari elemen HTML seperti p, div, a, table
- Seperti object pada umumnya, HTML elements memiliki property dan methods

### **Method and Property**

createElement()
- method untuk membuat suatu node elemen

createTextNode()
- method untuk membuat node berupa teks

append()
- method untuk menyisipkan node object atau string setelah child terakhir dari suatu elemen
- dapat menyisipkan string
- dapat menyisipkan lebih dari 1 node
  
appendChild()
- method untuk menyisipkan node setelah child terakhir dari suatu elemen
- tidak dapat menyisipkan string
- hanya dapat menyisipkan 1 node

innerText
- properti yang berisi konten teks dari suatu HTML element

innerHTML
- properti yang berisi konten dari suatu elemen HTML
- dapat menyisipkan tag HTML

textContent
- properti yang berisi konten teks dari suatu node element
- konten yang ditampilkan lebih lengkap dari innertext
- meliputi elemen script, style, dan hidden element

remove()
- method untuk menghapus suatu elemen dari dokumen

attributes
- properti yang berisi kumpulan atribut dari suatu elemen

getAttribute()
- method yang mengembalikan nilai dari suatu atribut

setAttribute(name , value)
- method yang dapat menambahkan atribut beserta nilainya 

hasAttribute()
- method yang mengembalikan nilai true jika atribut ada, false jika tidak

className
- properti yang berisi atribut class dari suatu elemen

classList
- properti yamg berisi kumpulan className dari suatu elemen
- classList.add()
  - menambahkan 1 atau lebih nilai properti class
- classList.remove()
  - menghapus 1 atau lebih nilai properti class
- classList.toggle()
  - menghapus(off) dan menambah(on) suatu class

Style
- object yang berisikan berbagai properti style dari suatu elemen
- color: mengakses nilai properti style color
- backgroundColor: mengakses nilai properti style background-color
- padding: mengakses nilai properti style padding

## **Summary Module 6 part VI - DOM Events**

### **Events**
- Suatu interaksi yang terjadi antara user dengan website
- click, scroll, focus, hover, submit

### **Contoh Events**
- click: terjadi ketika elemen ditekan
- submit: terjadi ketika suatu form dikirimkan
- focus: terjadi ketika elemen dalam kondisi fokus/aktif
- blur: kebalikan dari event focus
- hover: terjadi ketika pointer mouse bergerak menyentuh elemen
- change: terjadi ketika nilai suatu elemen diubah
- scroll: terjadi ketika scrollbar suatu elemen digulir

### **Cara Memberikan Events**
HTML Attribute
- Menuliskan event pada secaran langsung atribut di tag HTML yang hendak dimanipulasi
  ```
  <tag eventAttribute="handler"></tag> //syntax

  <h1 onclick="alert("Selamat Datang")">Klik Aku</h1>
  ```

Event Property
- Menuliskan event pada properti object yang kita miliki
  ```
  object.eventProperty = handler //syntax

  let paragraf = document.getElemenById("paragraf")

  paragraf.onclick = function () {
    alert("ini dari paragraf")
  }
  ```

addEventListener()
- Menuliskan event pada method addEventListener object yang kita miliki
  ```
  object.addEventListener("eventName", handler) //syntax

  button.addEventListener("click", function () {
    alert("Send this message?")
  })
  ```
### **Event property vs addEventListener()**
- addEventListener dapat menjalankan lebih dari 1 handler untuk tiap event pada object, event property hanya menjalankan 1
  ```
  button.addEventListener("click", function () {
    alert("Send this message?")
  })

  button.addEventListener("click", function () {
    confirm("Send this message?")
  })

  //keduanya akan dijalankan
  ```

### **Project DOM Sederhana - Counter**
```
//ambil elemen button untuk menambah counter
let btnIncrement = document.getElementById("increment")

//ambil elemen button untuk mengurangi counter
let btnDecrement = document.getElementById("decrement")

//ambil elemen untuk menampilkan counter
let counter = document.getElementById("counter")

//inisialisasi nilai untuk counter
let angka = 0

//buat event untuk menambah counter ketika button diklik
btnIncrement.addEventListener("click", function() {
  angka = angka + 1
  counter.innerText = angka
})

//buat event untuk mengurangi counter ketika button diklik
btnDecrement.addEventListener("click", function() {
  angka--
  counter.innerText = angka
})
```