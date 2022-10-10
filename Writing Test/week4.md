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