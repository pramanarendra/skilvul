# Writing Test Front-End Week 6

## **React Part I - Intro to React**

### **Apa yang dirasakan ketika pakai Real DOM**
- bolak-balik liat nama id dan class
- repot saat mau pakai event
- sering create element

### **Node JS**
- Tiap web browser ada mesin dengan engine yang berbeda-beda untuk menjalankan Javascript
- Chrome pakai V8 engine
- Pada awalnya, Javascript hanya dapat jalan di web browser
- Muncul teknologi yang memungkinkan javscript bisa berjalan di luar web browser, yaitu Node.js
- Ada V8 engine juga di Node.js
- Node.js dipakai untuk menjalankan Javascript di environtment lain
- Ada juga NPM yang memungkinkan kita untuk menginstall library-library Javascript lainnya

### **Apa itu React**
- React merupakan library Javascript untuk membuat user interface
- Selain React ada Angular, Vue, Svelte, dll
- React dibuat oleh engineer facebook
- Dibuat karena alasan performa web
- Membuat aplikasi FE menjadi lebih cepat bahkan ketika menangani data yang banyak
- Cocok untuk menangani website dinamis dengan data yang berbeda-beda
- Komunitas React sangat besar
- Peluang di dunia kerja cukup besar
- Digunakan oleh perusahaan besar seperti netflix, instagram, facebook, airbnb

### **Declarative, Component Based, Learn Once Write Anywhere**
- Terdapat 3 sifat utama React:
    - **declarative**: Deklarasikan secara sederhana apa yang akan dibuat, React secara efisien mengupdate dan merender komponen yang diperlukan oleh data
    - **Component-based**: React dapat membuat komponen-komponen UI yang dapat digunakan kembali di berbagai tempat
    - **Learn Once, Write Anywhere**: Selain platform web, React juga dapat digunakan pada mobile juga dengan React Native

### **Instalasi React**
- Pastikan node.js dan npm sudah terinstall
- Cek dengan command `node -v` dan `npm -v`
- Jika nomor versi sudah tampil, maka sudah terinstall
- Buka direktori yang diinginkan lalu inisialisasi React dengan command berikut
    ```
    npx create-react-app <nama proyek>
    ```
- jalankan aplikasi degan `npm start`

### **Single Page App**
- SPA merupakan konsep dimana aplikasi berjalan di satu file HTML saja
- Komponen-komponen di dalamnya akan dimuat di dalam satu file tersebut
- Pada web tradisional, refresh akan dilakukan setiap melakukan request
- React memungkinkan kita untuk tidak memerlukan refresh tiap request

### **Virtual DOM**
- Web page biasa berinteraksi dengan Real DOM
- Dengan React, terdapat suatu perantara yang disebut dengan virtual DOM (replika dari DOM)
- Real DOM:
    - suatu node berubah -> seluruh node akan dirender ulang, semakin dinamis datanya -> semakin berat
- Virtual DOM
    - suatu node berubah -> hanya node yang berubah tersebut yang dirender

### **Struktur Folder**
- Folder node modules
    - Berisi package-package yang digunakan dalam proyek tersebut
- Folder public
    - berisi struktur web utama
    - ada file index.html dimana aplikasi kita akan berjalan
    - di dalamnya index.html ada suatu div dengan id root
    - komponen-komponen lainnya akan dimasukkan di dalam div tersebut
- Folder src
    - folder yang menjadi fokus pengerjaan proyek
    - di dalamnya ada file index.js
    - di dalamnya ada suatu perintah yang mengambil elemen dengan id root lalu dibentuk suatu virtual DOM
    ```
    const root = ReactDOM.createRoot(document.getElementById('root'));
    ```
    - lalu akan merender App
    ```
    root.render(
    <React.StrictMode>
        <App />
    </React.StrictMode>
    );
    ```
    - `<App />` merupakan komponen yang diimpor dari App.js
    - File App.js berisi function yang akan mengembalikan sintaks HTML
    - Apa yang dikembalikan dari App akan ditampilkan pada root

### **JSX**
- JSX memungkinkan kita untuk menulis sintaks HTML di dalam Javascript
- Hanya dapat me-return satu root HTML
- Bisa dibungkus dalam root menggunakan `<div></div>` atau react fragment `<></>`
- Nama function harus diawali huruf besar
- Di akhir file harus ditambahkan `export default <nama file>`
- File yang diekspor dapat kita gunakan berulang kali pada file yang berbeda
- Jika ingin dipakai di komponen lain, gunakan sintaks `import <nama file tanpa ekstensi> from <path>`
- Dipakai dengan sintaks `<Nama />`
- Keyword class sudah ada di Javascript, maka diganti dengan className
    ```
    import Home from './components/Home'
    import About from './components/About'

    function App() {
    let myName = "Handy"

    return (
        <div className="container">
        <h1>ini adalah APP milik {myName}</h1>

        <Home />

        <About />

        </div>
    );
    }

    export default App;
    ```

---

## **React Part II - React Component**

### **React Component**
- Component: metode membagi UI dalam satuan-satuan yang lebih kecil yang reusable
- Component cukup dibuat sekali dan bisa dipakai berukang kali di tempat lain
- Contoh komponen adalah navbar, card, footer, dan masih banyak lagi

### **Vite**
- Tools untuk mempercepat set up environtment untuk menjalankan framework
- Command untuk instalasi:
    ```
    npm create vite@latest react-component --template react

    cd react-component

    npm install
    ```
- Waktu instalasi jauh lebih cepat
- Isi folder React app diminimalkan
- Command untuk menjalankan aplikasi:
    ```
    npm run dev
    ```

### **Link CSS dengan aplikasi React**
- Untuk menghubungkan file eksternal css ke jsx, gunakan import
    ```
    import <path file css>
    ```
- Bisa juga import file css di main App.jsx saja, tidak perlu per component
- Gunakan double curly bracket untuk menuliskan nilai pada atribut style
- Gunakan camel case untuk menuliskan properti CSS
    ```
    return (
    <div style={{ color: 'blue', lineHeight : 10, padding: 20 }}></div>
    )
    ```

### **Membuat Component**
- Buat folder components di dalam src
- Selalu buat folder, file, dan function component dengan diawali huruf kapital
- Bungkus component dalam function
- Tuliskan html component yang ingin dibuat
- Export file
    ```
    const ProfileCard = () => {
        return (
            <div>
                <h1>Rendra</h1>
                <p>Saya adalah seorang web developer</p>
            </div>
        )
    }

    export default ProfileCard;
    ```
- Tampilkan component pada App.jsx atau file lain dengan import dan panggil di dalam blok return
    ```
    import ProfileCard from './components/ProfileCard'

    function App() {

        return (
            <div className="App">
            <ProfileCard />
            </div>
        )
    }
    ```
- Ketika component pada ProfileCard.jsx diperbarui, seluruh file lain yang mengimpor component tersebut juga akan terubah tanpa perlu diperbarui satu per satu
- Import css-css component bisa dilakukan pada file App.jsx saja agar mudah dikelola
- Shortcut untuk membuat component adalah `rafce`

### **Props**
- Cara kerjanya mirip dengan parameter dalam suatu function
- Untuk mengirimkan data ke dalam component
- Memungkinkan tampilan yang dinamis berdasarkan data input
- Saat menggunakan component, kita dapat menambahkan banyak atribut dengan berbagai nilai
    ```
    <ProfileCard name={"Rendra"} job={"Web Developer"}/>
    <ProfileCard name={"Julia"} job={"UI/UX Designer"}/>
    ```
- Untuk mengakses nilai dan atribut itu ketik `props` pada function component
- Props dapat diakses seperti menggunakan object biasa
    ```
    const ProfileCard = (props) => {
        return (
            <div>
                <h1>{props.name}</h1>
                <p>Saya adalah seorang {props.job}</p>
            </div>
        )
    }
    ```
- Bisa juga menggunakan destructuring
    ```
    const ProfileCard = ({ name, age, job }) => {
        return (
            <div>
                <h1>Nama saya adalah {name}</h1>
                <p>Saya berumur {age} tahun</p>
                <p>Saya adalah seorang {job}</p>
            </div>
        )
    }
    ```
### **useState**
- Cara yang disarankan React untuk menyimpan suatu variabel yang dinamis
- Jika data hanya dideklarasikan seperti variabel biasa, ketika nilainya dimanipulasi, tampilannya di HTML tidak akan berubah
- Import useState dari React terlebih dahulu
    ```
    import { useState } from "react";
    ```
- useState terdiri atas variabel, function setter untuk merubah nilai, dan value awal di dalam useState
    ```
    function App() {
        const [count, setCount] = useState(0);

        return (
            <div className="App">
            <h2>{count}</h2>
            <button onClick={() => setCount(count + 1)}>Tambah</button>
            <button onClick={() => setCount(count - 1)}>Kurang</button>
            </div>
        )
    }
    ```
- Dalam kode tersebut, setiap button diklik, function setter akan dipanggil untuk mengubah state count

### **Stateless & Stateful**
- Stateless: hanya memiliki prop atau tidak memiliki data dan tidak memiliki state
- Stateful: memiliki state atau memiliki data yang disimpan dan bisa mengirim state tersebut ke component
    - data yang dimaksud tidak harus menggunakan useState, hal-hal yang diimpor seperti image juga termasuk data
    - state disebut juga data lokal yang tinggal di komponen itu

### **React + Bootstrap**
- Kita dapat menggunakan Bootstrap pada React
- Instalasi:
    - Tambahkan dengan link CDN script dan style ke index.html seperti biasanya
    - Install Bootstrap dengan CLI melalui `npm install Bootstrap` lalu import ke main.jsx
        ```
        // Bootstrap CSS
        import "bootstrap/dist/css/bootstrap.min.css";
        // Bootstrap Bundle JS
        import "bootstrap/dist/js/bootstrap.bundle.min";
        ```
- Kita dapat langsung menggunakan komponen Bootstrap tapi perlu mengganti seluruh atribut `class` menjadi `className`
- Untuk mempercepat penggantian, bisa digunakan fitur find & replace dari vs code

### **React Bootstrap**
- Bootstrap dengan sintaks komponen yang telah disesuaikan dengan React
- Install dengan `npm install react-bootstrap bootstrap`
- Tambahkan import berikut di index.js atau App.js
    ```
    import 'bootstrap/dist/css/bootstrap.min.css';
    ```
- Bootstrap siap digunakan
- Import komponen yang diinginkan lalu masukkan ke dalam return
    ```
    import Button from 'react-bootstrap/Button';

    const Card = () => {
        return (
            <div>
                <Button variant="primary">Primary</Button>{' '}
            </div>
        )
    }
    ```

---

## **React Part III - Handling Events**

### **Review Prop & State**
- State: memiliki data yang tinggal di dalam suatu komponen
- Props: hanya menerima data dari komponen lain
![state & prop](../images/prop%20state.png)

### **Handling Event**
- untuk menambahkan event cukup tambahkan atribut event panggil function yang diinginkan
- tidak perlu menggunakan tanda kurung
    ```
    function Card() {
        const handleClick = () => {
            console.log("event klik berfungsi");
        }

        return (
            <div onClick={handleClick}>Klik Aku</div>
        )
    }
    ```

### **Event with Parameter**
- Untuk menuliskan event dengan parameter, harus dituliskan dalam callback function
- Jika tidak, function akan dijalankan meskipun event belum terjadi
    ```
    const Card = () => {

        const handleClick = (nama) => {
            console.log("Halo namaku " + nama);
        }

        return (
            <div>
                <div onClick={() => handleClick("Rendra")}>Klik Aku</div>
            </div>
        )
    }
    ```

### **Handling Array & Object State**
- Jika data state adalah array atau object, maka tidak bisa ditampilkan semua secara langsung
- Hanya bisa diakses dengan indeks dan key yang spesifik
- Atau bisa menggunakan map untuk melakukan iterasi dalam menampilkan state
- forEach tidak bisa dipakai karena perlu sesuatu untuk di-return agar bisa tampil
- Tiap child dalam list perlu ditambahkan suatu key yang unik ketika ditampilkan
- Agar ketika terjadi perubahan, hanya data dengan key yang spesifik yang akan dirender ulang
    ```
    const ProfileCard = () => {

        const [users, setUsers] = useState([
            { name: "Alpha", umur: 17 },
            { name: "Beta", umur: 18 },
            { name: "Charlie", umur: 19 },
            { name: "Delta", umur: 20 },
        ])

        return (
            <div>
                <h1>{users[0].name}</h1>

                <ul>
                    {users.map((item, index) => (
                        <li key={index}>
                            {item.name}, {item.umur}
                        </li>
                    ))}
                </ul>
            </div>
        )
    }
    ```

### **Conditional Rendering**
- Kita bisa memilih apakah suatu komponen ditampilkan menurut kondisi tertentu
- Misal user butuh melakukan login untuk mengakses fitur tertentu
- Dapat ditulis dengan statement conditional if-else biasanya atau ternary
    ```
    const Card = () => {

        const handleClick = (nama) => {
            console.log("Halo namaku " + nama);
        }

        const [login, setLogin] = useState(false);

        return (
            <div>
                <div onClick={() => setLogin(true)}>Login Sekarang</div>

                {login ? <p>Kamu sudah login</p> : <p>kamu belum login</p>}
            </div>
        )
    }
    ```
    ```
    const MailBox = (props) => {
        const newMessage = props.newMessage;

        return (
            <div>
                <p>Kotak Masuk:</p>
                {newMessage > 0 &&
                    <p>Kamu punya {newMessage} pesan baru</p>
                }
            </div>
        )
    }
    ```

---
## **React Lanjutan - Lifecycle & Hooks**

### **React Lifecycle**
- Komponen pada React memiliki **tiga siklus** utama:
    - Mounting: tahap ketika komponen muncul pada DOM
    - Update: komponen diperbarui ketika terdapat perubahan seperti dalam state atau props
    - Unmount: tahap ketika komponen dihapus dari DOM

### **React Hooks**
- Fitur yang ditambahkan pada React versi 16 di tahun 2018
- Fitur untuk memudahkan penggunaan functional component agar dapat menggunakan state dan lifecycle lainnya
- Kode akan lebih clean, singkat, dan mudah dipahami
- Pada versi lama, state dan lifecycle hanya ada pada class component
- Ditantadai dengan keyword `use`
- Contoh: useState, useEffect, useContext, dsb

### **useState**
- pada dasarnya sama seperti state biasa
- sebelum digunakan, perlu dimpor terlebih dahulu
    ```
    import { useState } from "react"
    ```
- terdiri atas variabel value, setter function, dan initial value
    ```
    const [count, setCounter] = useState(0);
    ```
- untuk mengaksesnya cukup tuliskan variabel value
    ```
    <div>{ count }</div>
    ```
- untuk mengupdate, gunakan setter function
    ```
    <button onClick={() => setCounter(count + 1)}>Increment</button>
    ```

### **useEffect**
- Ada efek samping yang bisa diberikan sebagai **respon** terhadap tiap-tiap lifecycle
- Contoh pemberian effect pada tiap cycle:
    - Ketika komponen di-mount: ambil data pakai fetch
    - Ketika komponen diperbarui: lakukan filter
    - Ketika komponen di-unmount: data state jangan diperbarui
- Untuk menggunakan useEffect, perlu diimpor terlebih dahulu
    ```
    import { useEffect } from "react";
    ```
- useEffect ditulis dengan **callback function**
    ```
    useEffect(() => {
        console.log("Efek dieksekusi");
    });
    ```
- Alur eksekusi:
    - jalankan apa perintah yang ada di dalam function component
    - jalankan yang ada di return function tesebut
    - jalankan useEffect

- Contoh useEffect
    - Pada proses mount ditampilkan loading skeleton
    - Setelah proses mount selesai akan ada side effect fetch data
    - Data dimasukkan ke dalam state lalu ditampilkan

- Secara **default**, useEffect akan ditampilkan setiap komponen **di-mount dan di-update**

- Contoh useEffect pada kode:
    ```
    const ListData = () => {

        const [isLoading, setIsLoading] = useState(false);

        console.log("komponen dipanggil")

        useEffect(() => {
            console.log("komponen telah di-mount")
        })

        return (
            <div>
                <button onClick={() => setIsLoading(!isLoading)}>Ubah State Loading</button>
                <p>{isLoading}</p>
            </div>
        )
    }
    ```
- tampilkan log komponen dipanggil
- render komponen yang ada pada return
- setelah dirender, berikan side effect berupa log teks komponen telah di-mount
- ketika state diperbarui, berikan side effect berupa log teks ke console
- fungsi akan dijalankan -> komponen di-mount -> side effect berjalan

### **Infinite Re-render**
- jika terdapat function setter di dalam useEffect, akan terjadi infinite re-render
- setelah di-mount -> useEffect berjalan -> fungsi setter berjalan -> render ulang -> useEffect berjalan -> dan seterusnya

### **useEffect pada Mount**
- tambahkan **kurung siku** di akhir agar effect hanya dijalankan sekali saja setelah di-mount
- ketika terjadi update, effect tidak akan dijalankan lagi
    ```
    useEffect(() => {
        console.log("Efek dieksekusi");
    }, []);
    ```

### **Contoh Langkah-Langkah Fetch Data dengan useEffect**

- siapkan state yang berisi array kosong
    ```
    const [digimons, setDigimons] = useState([]);
    ```
- buat useEffect dengan diakhiri kurung siku agar hanya dijalankan sekali
- install Axios dengan `npm install axios` untuk memudahkan fetch
- dengan Axios, kita tidak perlu melakukan "unboxing" data dari API
- lakukan fetch data lalu masukkan ke dalam state
    ```
    useEffect(() => {
        axios("https://digimon-api.vercel.app/api/digimon").then((res) => {
            setDigimons(res.data);
        });
    }, []);
    ```
- buat looping untuk menampilkan data pada DOM di bagian return
    ```
    digimons.map((item, index) => (
        <div key={index} onClick={() => clickDigimon(item)}>
        <img src={item.img} alt="" width={200} />
        <h2>{item.name}</h2>
        </div>
    ))

    ```
Tahapan yang terjadi:
- komponen di-mount tapi state masih kosong
- ambil data dari API
- isi state dengan data tersebut
- render ulang untuk memperbarui tampilan dengan data yang sudah ada

### **Targeted Effects**
- kita dapat menambahkan variabel di kurung siku
- useEffect hanya akan terjadi jika terdapat perubahan pada variabel tersebut
    ```
    const Toggle = () => {

        const [toggle1, setToggle1] = useState(false);
        const [toggle2, setToggle2] = useState(false);

        useEffect(() => {
            console.log("Effect dipicu oleh toggle 2")
        }, [toggle2])

        return (
            <div>
                <button onClick={() => setToggle1(!toggle1)}>Toggle 1</button>
                <button onClick={() => setToggle2(!toggle2)}>Toggle 2</button>
            </div>
        )
    }
    ```
- dalam kasus tersebut, effect hanya dijalankan ketika terdapat perubahan pada toggle2

### **useEffects unmount**
- biasanya digunakan untuk membersihkan data
- ditulis dengan return pada useEffect
    ```
    useEffect(() => {
        console.log("Effect dipicu oleh toggle 2");

        return () => {
            console.log("unmount")
        }
    }, [toggle2])
    ```

---

## **React Form**
- Digunakan untuk menangkap input data dari user untuk kemudian disimpan atau dimanipulasi

Langkah-langkah:

- siapkan tag form, label, dan input seperti HTML biasa
- penulisan atribut name pada label diganti dengan htmlFor
    ```
    <label htmlFor="name">Name</label>
    ```
- buat state dengan initial value kosong untuk tiap input form
    ```
    const [name, setName] = useState(" ");
    const [address, setAddress] = useState(" ");
    ```
- inisialisasi atribut value dengan nilai state
    ```
    <input type="text" value={name} />
    ```
- gunakan event onChange untuk menangkap event dari user
- ubah nilai setState untuk menampung input ev.target.value ke state
    ```
    <input type="text" value={name} onChange={(ev) => setName(ev.target.value)} />
    ```
- untuk menangkap event submit, bisa digunakan onSubmit
- taruh onsubmit di tag form, bukan di button
    ```
    <form action="" onSubmit={handleSubmit}>
    ```
- buat button dengan type submit
    ```
    <button type="submit">Submit</button>
    ```
- buat function handler yang akan ditaruh pada onSubmit
- isi function handler untuk menangkap input
- reset input agar bisa melakukan input kembali
    ```
    const handleSubmit = (ev) => {
        ev.preventDefault();
        alert(`nama: ${name} alamat: ${address}`)
        setName("");
        setAddress("");
    }
    ```
- buat state sebagai tempat menampung data
- pakai function setter untuk menampung data pada function handler submit
    ```
    const [data, setData] = useState({});

    const handleSubmit = (ev) => {
        ev.preventDefault();
        setData({ name, address })
        setName("");
        setAddress("");
    }
    ```

### **Mengambil Input dengan Tipe Option**
- buat input dengan tag select dan option
- buat state untuk menampung option
- inisialisasi value tag select dengan state
- buat value tiap-tiap option, tidak perlu inisialisasi atribut value
- berikan event handler onChange
- gunakan setter function untuk menangkap value
    ```
    <select value={program} onChange={(e) => setProgram(e.target.value)}>
        <option value="">select program</option>
        <option value="KM">KM</option>
        <option value="SIC">SIC</option>
        <option value="Amman">Amman</option>
    </select>
    ```

### **Post Data dengan Axios**
- install axios dengan npm
    ```
    npm install axios
    ```
- import axios ke dalam component
    ```
    import axios from "axios";
    ```
- siapkan database atau API untuk tempat post data
- gunakan method post lalu isi dengan link API dan state yang akan dikirim
- gunakan method then untuk mereset nilai state agar bisa digunakan kembali
- tangkap error dengan method catch
    ```
    axios
        .post("http://localhost:3000/student", {
        name,
        address,
        program,
        })
        .then(() => {
        setData({ name, address, program });
        setName("");
        setAddress("");
        setProgram("");
        })
        .catch((err) => {
        console.log(err);
        });
    };
    ```
