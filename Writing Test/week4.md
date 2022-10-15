# Writing Test Week 4

## **Javascript Asynchronous - Fetch & Async Await**

### **Server**
- Suatu perantara antara user dengan database
- Tiap user mengakses website, user mengirim request yang di-handle oleh server
- API: perantara user dengan server
- Analogi:
    - Pelanggan (user) memesan lewat pelayan (API)
    - Pelayan berkomunikasi dengan chef di dapur (server)
    - chef membuat masakan dengan mengambil bahan dari kulkas (database)
![FE dan BE](./images/FE%20dan%20BE.png)

- API biasanya berkomunikasi melalui JSON (Javascript Object Notation)
- JSON: seperti object tapi tiap key ditulis menggunakan tanda petik
- Digunakan untuk menyimpan data terstruktur

### **Menangkap Object Promise**
- Ada 2 cara penanganan Promise
    1. Menggunakan Then Catch
    1. Menggunakan Async Await

### **Async Function**
- Ditulis seperti function biasa tetapi diberi keyword async
- Await digunakan untuk menangkap Promise
- Await hanya berjalan pada async function

    ```
    async function asyncNonton() {}

    let asyncNonton = async () => {}
    ```
    ```
    //  Promise
    let nonton = (kondisi) => {
    return new Promise((resolve, reject) => {
        if (kondisi == "jalan") {
        resolve("nonton terpenuhi")
        }
        reject("batal nonton")
    })
    }

    //  Async Await
    async function asyncNonton() {
        let result = await nonton("jalan");
        console.log(result);
    }

    asyncNonton(); //   nonton terpenuhi
    ```

### **Error Handler**
- Gunakan `try ... catch` untuk menangani error
```
async function asyncNonton() {
    try {
        let result = await nonton();
        console.log(result);
    } catch (error) {
        console.log(error);
    }
}

asyncNonton(); //   batal nonton
```

### **Fetch**
- Method `fetch()` digunakan untuk mengambil data dari API
- Fetch mengembalikan data dalam bentuk object Promise
- Data tersebut kemudian dapat diproses dengan `then` dan `async ... await`

### **Fetch dengan Then**
```
fetch("https://digimon-api.vervel.app/api/digimon")
.then(result => {
    return result.json(); //    diibaratkan sebagai unboxing
})
.then(result => {
    console.log(result);
})
.catch(err => {
    console.log(err);
})
```
- method fetch mengambil data dari API digimon
- kemudian setelah seluruh data diterima, data di-unboxing menjadi json
- kemudian data json ditampilkan pada console
- jika terjadi error, maka tampilkan error

### **Fetch dengan Async Await**
```
let getDigimon = async () => {
    let response = await fetch("https://digimon-api.vervel.app/api/digimon");
    let result = await response.json();
    console.log(result);
}

getDigimon();
```

### **Menampilkan data pada HTML**
- Contoh menampilkan data dengan data array lokal
    ```
    let digimons = ["Agumon", "Gabumon", "Paimon"];
    let containerDigimon = document.getElementById("list-digimon");

    //  Gunakan looping untuk menampilkan data
    digimons.forEach(digimon => {
        containerDigimon.innerHTML += `<li>${digimon}</li>`
    })
    ```
- Contoh menampilkan data dengan data dari API
    ```
    let containerDigimon = document.getElementById("list-digimon");

    let getDigimon = async () => {
        let response = await fetch("https://digimon-api.vervel.app/api/digimon");
        let digimons = await response.json();

        digimons.forEach(digimon => {
            containerDigimon.innerHTML += 
                `<div>
                    <img src="${digimon.img}" width="200">
                    <h3>${digimon.name}</h3>
                </div>`
        })
    }

    getDigimon();
    ```

- Tips untuk mengecek apakah data sudah diterima
- Tidak perlu melakukan looping seluruh data
    ```
    let getDigimon = async () => {
        let response = await fetch("https://digimon-api.vervel.app/api/digimon");
        let digimons = await response.json();

        digimons.slice(0, 10).forEach(digimon => {
            console.log(digimon);
        })
    }

    getDigimon();
    ```

---

## **Git dan GitHub Lanjutan**

### **Memberi Akses Kolaborator**
- Untuk memungkinkan kolaborasi pada repo private, kita perlu menambahkan kolaborator
- Kolaborator dapat di-assing dengan dua kondisi
- Jika di repo masing masing:
    - settings > access > collaborators > add people
- Jika di organization
    - Anggota organisasi otomatis menjadi kolaborator
    - bisa bikin banyak repo di organization
    - bisa dibilang bikin akun untuk bersama

### **Role dalam GitHub**
- Team leader: mengatur pull request dari anggota
- Kolaborator: mengerjakan tugas di branch masing-masing

### **Inisialisasi Repo untuk Kolaborasi**
- Buat repository seperti biasa
- Add collaborators, jika dalam organization tidak perlu add collaborators
- Buat branch baru bernama `dev`

### **Branch Main dan Dev**
- Dalam suatu proyek, terdapat tahap development dan production
    - development: tahap pengembangan proyek
    - production: tahap perilisan proyek ke publik
- Branch dev digunakan ketika dalam stage development
- Branch main digunakan ketika dalam stage production
- Branch dev berguna untuk menampung segala macam cabang lain
- Jika tidak ada branch dev > fitur baru langsung masuk ke main > semua orang langsung bisa akses > masih banyak bug

### **Proses Berkolaborasi**
1. Melakukan clone pada repo kolaborasi
    - pakai perintah `git clone <https>`
    - untuk mendownload file repo ke lokal
1. Membuat branch dari dev
    - pindah ke branch dev dahulu dengan `git switch dev`
    - buat branch sesuai fitur yang ingin dibuat dengan `git branch <nama-branch>`
    - pindah ke branch yang telah dibuat dengan `git switch <nama-branch>`
    - perintah untuk pindah branch bisa menggunakan `switch` atau `checkout`
    - pengerjaan fitur dapat dimulai
1. Melakukan perubahan dan commit pada branch
    - lakukan perubahan pada branch masing-masing lalu push seperti biasa
    - `git add.` > `git commit -m <pesan>`
    - Sebelum `git push -u origin <nama branch>`, lakukan `git merge dev` untuk menghindari conflict
1. Lakukan pull request
    - pull request: permintaan menggabungkan branch yang kita buat ke branch lain
    - jika orang itu adalah anggota, harus lakukan assign ke team leader di menu pull request sebelah kanan
    - team leader mengecek apakah terdapat konflik pada request
    - jika pull request belum sesuai, dapat diberi komentar atau mengabari
    - jika sudah benar > merge pull request > bisa juga ditambahkan labels (opsional)
1. Lakukan `git pull` untuk mengambil update yang terjadi pada branch dev
    - bisa juga menggunakan `git fetch` + `git merge`
1. Ulangi kembali dari langkah ketiga hingga kelima

### **Conflict**
- conflict mungkin terjadi ketika melakukan merge branch
- terjadi ketika lebih dari satu pihak merubah baris yang sama
- conflict perlu diresolve sebelum di-merge
- pull request yang konflik dapat diberi commenct agar diperbaiki dahulu
    - lakukan `git pull`
    - lakukan `git merge dev` di branch
    - diskusikan conflict dengan pihak lain jika perlu
    - pilih opsi accept current change, accept incoming change, atau accept both change
    - lakukan push kembali
    - merge pull request

---
## **Responsive Web Design**

- Metode pembuatan desain web yang bertujuan untuk memberikan pengalaman yang optimal melalui berbagai perangkat
- Desain layout website dapat berubah mengikuti ukuran layar

### **Tools Pendukung**
- Untuk mensimulasikan ukuran layar pada website, dapat digunakan **chrome dev tools**
- Diakses dengan command `ctrl + shift + j`

### **Viewport**
- Area website yang dapat dilihat oleh user
- Tiap device memiliki ukuran viewport yang berbeda-beda
- Website yang tidak menggunakan meta viewport akan di-scale down sehingga tampilannya akan sangat kecil
- HTML5 memperkenalkan tag meta yang dapat diisi dengan informasi viewport
    ```
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    ```
    - `width=device-width`: lebar dari halaman akan disesuaikan dengan lebar device
    - `initial-scale=1.0`: halaman tidak dizoom ketika diakses karena nilai zoom-nya 1

### **CSS Units**
- Untuk mendefinisikan besaran suatu elemen dengan CSS, diperlukan sistem satuan ukur
- Perubahan ukuran biasanya dilakukan untuk mendukung responsivitas
- Unit pada CSS yang dikelompokkan menjadi 2 tipe
- Absolute unit: objek akan benar-benar ditampilkan sebesar satuan unit tersebut
    - cm, mm, px, pt
- Relative unit: nilai besaran objek relatif terhadap objek lain
    - em: relatif pada font size di elemen tersebut
    - rem: relatif terhadapat font size root (16px)
    - vw: relatif terhadap presentase ukuran lebar viewport
    - vh: relatif terhadap presentase ukuran panjang viewport

### **Properti max-width**
- Salah satu cara untuk membuat konten lebih responsif adalah properti max-width
- Misalkan pada sebuah gambar, jika tidak diberi properti max-width yang jelas, bisa saja gambar tersebut tidak discale down dan terpotong ketika dilihat pada device kecil
- Dengan menambahkan properti `max-width:100%`, gambar tidak akan terpotong karena selalu di-scaling agar seluruh gambar (100%) terlihat

### **Membuat Tampilan yang Responsive**
- Untuk membuat suatu website menjadi responsive, aturan CSS yang berbeda perlu diterapkan pada ukuran layar yang berbeda
- Perubahan aturan yang terjadi ketika lebar dari device berubah disebut dengan **breakpoint**
- Ada dua cara untuk melakukan hal tersebut
    - Membuat file CSS yang berbeda untuk tiap ukuran device
    - Menggunakan media query

### **Membuat File CSS yang Berbeda**
- File CSS yang berbeda dapat dibuat untuk tiap ukuran device
- Agar file bekerja pada ukuran layar tertentu, gunakan atribut `media` pada tag `link`
    ```
    <link rel="stylesheet" href="styles/main.css">
    <link rel="stylesheet" media="screen and (max-width: 500px) href="styles/mobile.css">
    ```

### **Media Query**
- Media query merupakan teknik pada CSS untuk mendukung responsivitas tanpa perlu membuat file lain
- Dengan media query, properti CSS dapat diatur untuk bekerja hanya dalam kondisi ukuran layar tertentu
    ```
    @media only screen and (max-width: 600px) {
    body {
        background-color: lightblue;
        }
    }
    ```
- warna background pada elemen body hanya akan berganti ketika ukuran layar sebesar 600px ke bawah

## **Bootstrap**
- Framework CSS untuk membuat website yang responsive dengan cepat
- Memiliki berbagai UI component dan utility class yang dapat langsung digunakan

### **Inisialisasi Bootstrap**
- Cukup tambahkan tag link pada head dan script pada body bagian bawah yang disediakan oleh bootsrtap ke file HTML
    ```
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-Zenh87qX5JnK2Jl0vWa8Ck2rdkQ2Bzep5IDxbcnCeuOxjzrPF/et3URy9Bv1WTRi" crossorigin="anonymous">
    
    ...

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-OERcA2EqjJCMA+/3y+gxIOqMEjwtxJY7qPCqsdltbNJuaOe923+mo//f6V8Qbsw3" crossorigin="anonymous"></script>
    ```

### **Bootstrap Components & Utility Classes**
- Bootsrtap menyediakan berbagai komponen UI dan utility yang dapat langsung dipakai dengan menuliskan class pada tag HTML
- Tiap komponen dan utilitas memiliki aturan class yang berbeda-beda
- Berikut adalah berbagai contoh classes yang ada di Bootstrap yang sering digunakan

### **Typography**
- Heading: membuat judul yang lebih besar dan tebal dari teks biasa
    - Ada class `.h1` hingga `.h6` mirip seperti tag heading HTML
        ```
        <p class="h1">Bootstrap heading</p>
        ```
- Display: bekerja seperti heading tetapi memiliki font-size yang lebih besar
    - Ada `.display-1` hingga `.display-6`
        ```
        <h1 class="display-1">Display 1</h1>
        ```
- Alignment: dapat membuat konten menjadi rata tengah maupun kanan
    - `text-center`: konten menjadi rata tengah
    - `text-end`: konten menjadi rata kanan

### **Images**
- Responsive img: membuat `max-width:100%` dan `height:auto` agar ukuran gambar mengikuti lebar layar
    - `.img-fluid`
        ```
        <img src="..." class="img-fluid" alt="...">
        ```
- Border radius: membuat sudut sudut objek menjadi lingkaran
    - `.rounded`
        ```
        <img src="..." class="rounded" alt="...">
        ```
- Alignment: mengatur layout dari gambar
    - `.float-start`: gambar berada di sisi kiri
    - `.float-end`: gambar berada di sisi kanan

### **Navbar**
- Bootsrtap menyediakan komponen navbar yang dapat dikostumisasi
- Navbar bootsrtap sudah responsive dengan adanya icon toggle ketika size device cukup kecil
- Contoh navbar:
    ```
    <nav class="navbar navbar-expand-lg bg-light">
    <div class="container-fluid">
        <a class="navbar-brand" href="#">Navbar</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
            <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="#">Home</a>
            </li>
            <li class="nav-item">
            <a class="nav-link" href="#">Features</a>
            </li>
            <li class="nav-item">
            <a class="nav-link" href="#">Pricing</a>
            </li>
        </ul>
        </div>
    </div>
    </nav>
    ```

### **Cards**
- Container dari suatu konten
- Biasanya memuat gambar, deskripsi singkat, dan link
- Contoh card:
    ```
    <div class="card" style="width: 18rem;">
    <img src="..." class="card-img-top" alt="...">
    <div class="card-body">
        <h5 class="card-title">Card title</h5>
        <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
        <a href="#" class="btn btn-primary">Go somewhere</a>
    </div>
    </div>
    ```

### **Modals**
- Suatu dialog singkat yang dapat digunakan untuk notifikasi, alert, dan info lainnya
- Dialog biasanya hanya memiliki dua opsi, ya atau tidak
- Contoh modals:
    ```
    <div class="modal" tabindex="-1">
    <div class="modal-dialog">
        <div class="modal-content">
        <div class="modal-header">
            <h5 class="modal-title">Modal title</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
            <p>Modal body text goes here.</p>
        </div>
        <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
            <button type="button" class="btn btn-primary">Save changes</button>
        </div>
        </div>
    </div>
    </div>
    ```

### **Breakpoints**
- Bootstrap menyediakan beberapa variabel breakpoint dengan ukuran tertentu
    - `sm` = 576px
    - `md` = 768px
    - `lg` = 992px
    - `xl` = 1200px
    - `xxl` = 1400px

### **Container**
- Komponen dasar Bootstrap yang membungkus, memberi padding, dan mengatur alingment sesuai lebar device
    - `.container` mengatur max-width pada tiap breakpoint
    - `.container-{breakpoint}` width selalu 100% hingga breakpoint yang dituliskan
    - `.container-fluid` width selalu 100% pada seluruh breakpoint
- Contoh container:
    ```
    <div class="container-md">100% wide until medium breakpoint</div>
    ```

### **Grid System**
- Pengaturan layout berdasarkan sistem grid
- Tersusun atas baris dan kolom
- Banyak kolom maksimal adalah 12
- Misal terdapat 3 konten dengan lebar yang sama, berikan col-4 pada tiap konten
- Contoh grid:
    ```
    <div class="container text-center">
    <div class="row">
        <div class="col">col</div>
        <div class="col">col</div>
        <div class="col">col</div>
        <div class="col">col</div>
    </div>
    <div class="row">
        <div class="col-8">col-8</div>
        <div class="col-4">col-4</div>
    </div>
    </div>
    ```

### **Other Utilities & Components**
- Masih banyak komponen UI lainnya yang dapat digunakan
- Semua komponen tersebut dapat dilihat pada dokumentasi Bootstrap
- Dalam menggunakan Bootstrap, dokumentasi menjadi teman kita ketika ingin mencari sesuatu
- Dokumentasi Bootstrap dapat diakses pada [link](https://getbootstrap.com/docs/5.2) ini

---
## **Mock API**

### **Apa itu Mock API**
- Kita bisa mensimulasikan pembuatan API dengan mudah
- Data-data buatan bisa diinputkan melalui tools tersebut

### **Langkah-langkah**
1. Registrasi dengan Google atau GitHub
1. Buat project baru dan isi keterangannya
    ![mock api](./images/mock%20api%20create.png)
1. Masuk ke dalam project dan buat resource baru
    ![mock api new resource](./images/mock%20api%20new%20resource.png)
1. Masukkan data-data sesuai kebutuhan
    ![mock api define data](./images/mock%20api%20define%20data.png)
    - Kita dapat menentukan nama key dan tipe data di dalamnya
    - Mock API juga menyediakan data dummy agar kita tidak perlu membuat data sendiri dengan Faker.js
1. Banyaknya jumlah data dapat kita manipulasi sesuai kebutuhan
    ![mock api add data](./images/mock%20api%20add%20data.png)
1. Isi dari data juga dapat kita manipulasi
    ![mock api edit data](./images/mock%20api%20edit%20data.png)
    - Jangan lupa back up data di lokasi lain
    - Jika jumlah data terubah, isi dari data bisa saja direset
1. Klik pada nama data, maka akan diarahkan menuju link API
    ![mock api link](./images/mock%20api%20link.png)
1. Link API tersebut dapat langsung digunakan pada project kita dengan asynchronous Javascript