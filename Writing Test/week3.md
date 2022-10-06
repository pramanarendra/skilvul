# Writing Test Week 3

## **Javascript Array & Multi Array**

### **Array**
- Tipe data yang dapat menyimpan banyak data
- Untuk Js, tipe data yang disimpan dapat berbeda-beda
- Disusun dengan indeks yang berurutan
- Indeks dimulai dari angka 0

### **Membuat Array**
- Array ditandai dengan kurung siku
    ```
    let arr = [];

    let prov = ['Jawa Tengah', 'D.I. Yogyakarta', 'Jawa Barat', 'Banten']
    ```

### **Mengakses Array**
- Array diakses menurut indeksnya
    ```
    let prov = ['Jawa Tengah', 'D.I. Yogyakarta', 'Jawa Barat', 'Banten']

    console.log(prov[1]); //'D.I. Yogyakarta'
    ```

### **Update Array**
- Akses array lalu assign dengan nilai baru
    ```
    let prov = ['Jawa Tengah', 'D.I. Yogyakarta', 'Jawa Barat', 'Banten']

    prov[1] = 'Jawa Timur'
    console.log(prov);
    //['Jawa Tengah', 'Jawa Timur', 'Jawa Barat', 'Banten']
    ```

### **Const vs Let Array**
- const dan let sama-sama memungkinkan untuk update nilai
- let dapat mengubah seluruh array dengan array baru
- const tidak bisa mengubah array dengan array baru

    ```
    const arr = ['data1', 'data2', 'data3'];

    arr = ['arrBaru'];
    //Akan terjadi error
    ```

### **Array Properties**
- Ada banyak property bawaan dari Javascript
- yang sering digunakan adalah constructor, length, index, input, dan prototype
- `length`: mengetahui panjang isi array
    ```
    const arr = ['data1', 'data2', 'data3'];
    console.log(arr.length) //output: 3
    ```

### **Array Methods**
- Javascript menyediakan berbagai method bawaan
- `.push()`: menambah item pada akhir array
    ```
    let buah = ["jeruk", "apel", "anggur"];
    buah.push("pisang")

    console.log(buah);
    //["jeruk", "apel", "anggur", "pisang"];

    ```

- `.pop()`: menghapus item terakhir
    ```
    let buah = ["jeruk", "apel", "anggur"];
    buah.pop();

    console.log(buah);
    //["jeruk", "apel"]
    ```

- `.shift()`: menghapus item pertama
    ```
    let buah = ["jeruk", "apel", "anggur"];
    buah.shift();

    console.log(buah);
    //["jeruk", "apel"]
    ```

- `.unshift()`: menambah item pada awal array
    ```
    let buah = ["jeruk", "apel", "anggur"];
    buah.unshift("pisang");

    console.log(buah);
    //["pisang", "jeruk", "apel", "anggur"]
    ```
    - `.splice()`: menghapus atau menambah item pada indeks tertentu
    ```
    arr.splice(idx, delete, item1, ..., itemN);
    ```
    ```
    let buah = ["jeruk", "apel", "anggur", "pisang"];
    buah.splice(2, 0, "lemon");

    console.log(buah);
    //["jeruk", "apel", "lemon", "anggur", "pisang"]
    ```
    ```
    let buah = ["jeruk", "apel", "lemon", "anggur", "pisang"];
    buah.splice(2, 2);

    console.log(buah);
    //["jeruk", "apel", "pisang"];
    ```

- `.slice()`: menyalin item yang dipilih ke dalam array baru
    ```
    arr.slice(start, end)
    ```
    - elemen start akan diambil
    - elemen end tidak diambil
    ```
    let buah = ["jeruk", "apel", "lemon", "anggur", "pisang"];
    let fav = buah.slice(1, 3);

    console.log(fav)
    //["apel", "lemon"]
    ```

- `.sort()`: mengurutkan data pada array
    ```
    let arr = [1, 5, 6, 7, 4];
    arr.sort();

    console.log(arr);
    //[1, 4, 5, 6, 7]
    ```

### **Looping in Array**
- ada beberapa cara untuk looping array

Looping `for...of`

- Tidak perlu menuliskan initial, condition, dan post expression
    ```
    let fruits = ["jeruk", "apel", "lemon", "anggur", "pisang"];

    for(let fruit of fruits) {
        console.log(fruit);
    }
    ```
Method `.map()`

- Melakukan perulangan dengan membuat array baru
- Gunakan jika ingin memanipulasi nilai
    ```
    let nums = [1, 2, 3, 4, 5];

    let quadratic = nums.map(num => {
        return num*num;
    });

    console.log(quadratic);
    //[1, 4, 9, 16, 25]
    ```

Method `.forEach()`

- Mirip seperti perulangan biasa
- Gunakan jika ingin menampilkan atau menyimpan data saja
    ```
    let fruits = ["jeruk", "apel", "lemon", "anggur", "pisang"];

    fruits.forEach(fruit => {
        console.log(fruit);
    })
    ```

### **Multidimensional Array**
- Array yang ada di dalam array
- Dapat dibayangkan sebagai baris dan kolom pada tabel
- baris: length dari array
- kolom: isi tiap sub array
- Analogi baris dan kolom hanya berlaku untuk array 2D
```
let item = [
    ["Kaos", 10],
    ["Jeans", 3],
    ["Topi", 1]
];
```

### **Akses Multidimensional Array**
```
let item = [
    ["Kaos", 10],
    ["Jeans", 3],
    ["Topi", 1]
];

console.log(item[1][0])
//ambil data ke-1 pada array: ["Jeans", 3]
//ambil data ke-0 pada sub array: "Jeans"
```

### **Multidimensional Array Method**
- Sama seperti array biasa, ada method built-in yang tersedia
```
let item = [
    ["Kaos", 10],
    ["Jeans", 3],
    ["Topi", 1]
];

item.push(["Kaos Kaki", 8]);

console.log(item);
//  [
//      ["Kaos", 10],
//      ["Jeans", 3],
//      ["Topi", 1],
//      ["Kaos Kaki", 8]
//  ];
```

### **Looping Multidimensional Array**
- Sama seperti array biasa
- Jika ingin melakukan looping hingga sub array, gunakan nested loop
```
let items = [
    ["Kaos", 10],
    ["Jeans", 3],
    ["Topi", 1]
];

items.forEach(baris => {
    baris.forEach(kolom => {
        console.log(kolom)
    })
});

//  Kaos
//  10
//  Jeans
//  3
//  Topi
//  1
```

---
## **Object**
- Tipe data non primitive
- Dapat berisi berbagai tipe data primitive + non
- Terdiri dari property dan method
- Disusun dalam format key-value
- Property: informasi mengenai object
- Method: fungsi yang dapat dijalankan oleh object
- Dianalogikan seperti apa yang ada di sekitar kita
- Object kucing
    - properi: kaki 4, gigi taring, berbulu, dst
    - method: berburu, makan, bersuara, dst

### **Deklarasi Object**

- Diassign dengan tanda kurung kurawal
- Tiap property dan method diakhiri tanda koma
- Key-value terakhir tidak perlu koma
- Key dengan tanda spasi perlu diapit tanda petik
    ```
    let nama_obj = {}

    let nama_obj = {
        key1: "value1",
        key2: "value2"
    };
    ``` 

### **Mengakses Object**
1. Dot Notation
    ```
    object.property;
    ```

1. Bracket Notation
    ```
    object["nama property"]
    ```
    - untuk mengakses key yang punya tanda spasi
    - untuk memanggil lewat variabel
    ```
    let properti = "nama property";
    obj[properti];
    ```

### **Menambah Properti Baru**
- Akses properti baru lalu assign nilainya
    ```
    obj.newProp = value;

    let buku = {
        judul: "Hujan",
        penulis: "Tere Liye"
    };

    buku.tahun = 2020; //properti tahun ditambahkan
    buku["nama penerbit"] = "Gramedia"; //properti nama penerbit ditambahkan
    ```

### **Mengupdate Nilai Properti**
- Akses properti lalu assing nilai yang baru
    ```
    let hewan = {
        nama: "kucing",
        kaki: 4,
        warna: "putih"
    };

    hewan.nama = "kelinci"; //properti nama berubah menjadi kelinci
    hewan["kaki"] = 2; //properti kaki berubah menjadi 2
    ```

### **Menghapus Properti**
- Gunakan keyword delete diikuti akses properti
    ```
    delete hewan.warna;
    ```

### **Method**
- Suatu fungi yang ada di dalam object
- Penulisan sama seperti sebelumnya tapi diassing dengan function
- Cara akses sama seperti sebelumnya tapi diakhiri tanda kurung
    ```
    const greeting = {
        welcome: function() {
            return "Selamat Datang";
        },
        afterPay: function() {
            return "Pembayaran Berhasil";
        }
    };

    console.log(greeting.welcome())
    ```

### **Built In Method**
- Method object yang sudah disediakan oleh Javascript
- `Object.keys(obj)`: mengembalikan kunci-kunci pada object
- `Object.values(obj)`: mengembalikan nilai-nilai pada object
- Masih banyak lagi built in method lainnya
    ```
    //object
    const siswa = {
        nama: "Rendra",
        umur: 19,
        hobi: "ngoding"
    }

    let arr = Object.keys(siswa); //[nama, umur, hobi]
    let val = Object.values(siswa); //["Rendra", 19, "ngoding"]
    ```

### **Nested Object**
- Object dapat berisi tipe data non primitive
- Object dapat menyimpan object di dalamnya
    ```
    let buku = {
        judul: "Deep Learning",
        tahun: 2015,
        penulis: {
            penulis1: {
                nama: "Ian Goodfellow",
                umur: 42
            },
            penulis2: {
                nama: "Yoshua Bengio"
                umur: 35
            }

        }
    }
    ```

### **Mengambil Nilai Nested Object**
- Sama seperti sebelumnya tetapi ditulis secara berantai
- Dapat dirantai dengan dot notation maupun bracket notation
    ```
    buku.penulis.penulis1.nama; //"Ian Goodfellow"
    ```

### **Loop in Object**
- Looping object dapat dipermudah dengan statement `for ... in`
    ```
    for(let var in obj) {
        console.log(obj[var])
    }

    //looping pada object penulis, yaitu penulis1 dan penulis2
    for(let key in buku.penulis) {
        console.log(buku.penulis[key])
    }

    //looping pada object penulis1, yaitu nama dan umur
    for(let key in buku.penulis.penulis1) {
        console.log(buku.penulis.penulis1[key])
    }
    ```

### **Array of Object**
- Array yang menampung sekumpulan object
    ```
    [{obj1}, {obj2}, {obj3}]
    ```
- Diakses dengan kombinasi rantai akses array dan object
    ```
    arr[idx].prop
    ```
- Untuk mempermudah akses, dapat digunakan looping `for ... in`, method `forEach`, atau method `.map()`

    ```
    let users = [
        {
            nama: "Rendra",
            umur: 19,
            alamat: "Yogyakarta"
        },

        {
            nama: "Putri",
            umur: 20,
            alamat: "Bogor"
        },

        {
            nama: "Olivia"
            umur: 20,
            alamat: "Semarang"
        }
    ];
    ```

    ```
    for (let property in users) {
    console.log(users[property]);
    }

    users.forEach((val) => {
    console.log(val);
    })

    let data = users.map((user) => {
        console.log(user);
    })
    ```

---
## **Modules & Rekursive**

### **Modules**
- Suatu cara untuk memisahkan code ke dalam file yang berbeda-beda
- Tiap file dapat terhubung satu sama lain
- File dapat dipisah menurut fungsionalitasnya
- Code maintenance jadi lebih mudah

### **Export**
- Cara untuk mengekspor function atau variable untuk digunakan di luar file tersebut
    ```
    export ... ;
    ```
    ```
    //file internasional.js

    export let motor = ["suzuki", "Honda", "Kawasaki"];
    ```

### **Import**
- Cara untuk mengimpor function atau variable dari file lain ke file tujuan
    ```
    import ... from <source>
    ```
    ```
    //file lokal.js
    
    import { motor } from "./internasional.js";
    ```
- import pakai nama lain denga keyword `as`
    ```
    import {motor as motorImpor} from "./internasional.js";
    ```

### **Multiple Export**
- Gunakan kurung kurawal dan koma sebagai pemisah
    ```
    let motor = ["suzuki", "Honda", "Kawasaki"];
    let smartphone = ["samsung", "iphone". "Huawei"];

    export {motor, smartphone};
    ```

### **Multiple Import**
- Gunakan tanda koma untuk memisahkan import
    ```
    //file internasional.js

    let motor = ["suzuki", "Honda", "Kawasaki"];
    let smartphone = ["samsung", "iphone". "Huawei"];

    export {motor, smartphone};

    //file lokal.js

    import {motor, smartphone} from "./internasional.js";
    ```

### **Export Default**
- Secara default akan mengekspor yang data yang dipilih
- Hanya bisa 1 hal yang diekspor
- Diimpor tanpa kurung kurawal
- Nama impor bebas untuk diganti tanpa keyword `as`
    ```
    //file internasional.js

    export let motor = ["suzuki", "Honda", "Kawasaki"];
    export let smartphone = ["samsung", "iphone". "Huawei"];
    let komik = ["manga", "manhwa", "manhua"];

    export default komik;

    //file lokal.js

    import bacaan, {motor, smartphone} from "./internasional.js";
    console.log(bacaan); //["manga", "manhwa", "manhua"]
    ```

### **Export Function**
- Caranya sama seperti export dan import variabel

    ```
    //file internasional.js
    export function greeting() {
        console.log("Hello")
    };

    //file lokal.js
    import {greeting} from "./internasional.js";

    greeting(); //Hello
    ```

### **File Script di HTML**
- Tambahkan attribute `type="module"` pada tag script
- File tersebut dikatakan sebagai script utama
- File tersebut hanya bisa melakukan import, tidak bisa export

### **Aturan Urutan Module**
- Yang bawah dapat diakses yang atas tapi tidak sebaliknya
- Misal terdapat 3 module dengan urutan sbb
    ```
    <script src="file1.js" type="module"></script>
    <script src="file2.js" type="module"></script>
    <script src="file3.js" type="module"></script>
    ```
- file1.js tidak bisa diakses oleh file2.js, file2.js tidak bisa diakses oleh file3.js
- file3.js dapat diakses oleh file2.js, file2.js bisa diakses oleh file1.js

### **Aturan Import Module**
- Kalau file1.js sudah melakukan import dari file2.js, maka file2.js tidak dapat melakukan import dari file1.js
- Berlaku sebaliknya

### **Recursive**
- Function yang memanggil dirinya sendiri hingga kondisi tertentu
- Terdiri dari base case dan recursive case
- Base case: kondisi ketika function berhenti
- Recursive case: kondisi ketika function memanggil dirinya sendiri
- Pemanggilan diri sendiri selalu diikuti dengan pengurangan atau pemecahan data
- Biasanya digunakan untuk permasalahan matematis

### **Kasus Deret Angka**
```
function deretAngka(n) {
    if(n == 1) {
        console.log(n)
    } else {
        deretAngka(n)
        console.log(n);
    }
}

deretAngka(10);

//output: 1 2 3 4 5 6 7 8 9 10
```

### **Kasus Bilangan fibonacci**
- Bilangan yang berasal dari penjumlahan 2 bilangan sebelumnya
- 0, 1, 1, 2, 3, 5, 8, 13, dst
```
function fibonacci(num) {
    if(num < 2) {
        return num;
    }
    else {
        return fibonacci(num-1) + fibonacci(num - 2);
    }
}

fibonacci(5) //return: 5
fibbonaci(6) //return: 8
```

### **Kasus Faktorial**
- Perkalian dari angka 1 hingga bilangan ke-n
- 5! = 5 * 4 * 3 * 2 * 1 = 120
```
function faktorial(n) {
    if(n == 1) {
        return 1;
    } else {
        return n*faktorial(n-1);
    }
}

faktorial(5); //output: 120
```