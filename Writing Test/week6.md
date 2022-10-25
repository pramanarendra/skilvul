# Writing Test Week 6

## **React**

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