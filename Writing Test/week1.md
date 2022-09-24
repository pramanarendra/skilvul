# Writing Test Week 1

## **Summary Module 1 - Unix Command Line**

### **Shell**

- Program yang memungkinkan kita untuk berinteraksi atau memberi perintah pada sistem komputer

### **Command Line Interface**

- CLI mengacu pada Shell yang berbasis teks
- Contoh CLI: bash dan cmd
- Ada juga Shell berbasis gambar yang bernama GUI seperti file manager

### **Cara Mengakses CLI**

- Gunakan aplikasi pengakses CLI (Terminal Emulator)
- Buka aplikasi cmd atau powershell untuk Windows atau bash untuk Linux dan MacOS

### **File System Structure**

- Sebuah sistem yang mengatur struktur penyimpanan data
- Windows dan Unix memiliki struktur file seperti pohon
  ![file system structure](./images/file%20system%20structure.png)

### **Perintah-Perintah pada CLI**

- Melihat Current Working Directory

  - Print Working Directory
    ```
    pwd
    ```
    ![pwd](./images/pwd.png)

- Melihat Isi Directory

  - Lists
    ```
    ls
    ls -a
    ```
    ![ls](./images/ls.png)

- Berpindah Directory

  - Change Directory

    ```
    cd <directory>
    ```

    ![cd](./images/cd.png)

  - tanda '..' artinya memilih direktori di atasnya (parent)
  - tanda '.' artinya memilih direktori saat itu

- Melihat Isi File

  - head: melihat file dari baris paling awal
  - tail: melihat file dari baris paling akhir
  - cat: melihat isi file
    ```
    head -n <number of line> <source>
    tail -n <number of line> <source>
    cat <file yang dituju>
    ```
    ![cat](./images/cat.png)

- Membuat File & Directory

  - touch: membuat file
  - mkdir: membuat direktori
    ```
    touch <file name>
    mkdir <directory name>
    ```
    ![create](./images/create.png)

- Menyalin File & Directory

  - cp: menyalin file
  - cp -R: menyalin direktori
    ```
    cp <source> <destination>
    cp -R <source> <destination>
    ```
    ![copy](./images/copy.png)

- Memindahkan dan Merename File & Directory

  - mv: memindah atau menyalin file
  - mv -R: memindah atau menyalin direktori

    ```
    mv <source> <target>
    mv <old-name> <new-name>
    ```

    ![rename](./images/rename.png)

- Menghapus File & Directory
  - rm: menghapus file
  - rm -R atau rm -d: menghapus direktori
  ```
  rm <source>
  rm -R <source>
  ```
  ![remove](./images/remove.png)

---

## **Summary Module 2 - Git & GitHub Dasar**

### **Git**

- Git pada dasarnya ada suatu version control system
- Aplikasi yang melacak setiap perubahan yang terjadi pada file atau folder

### **GitHub**

- GitHub pada dasarnya merupakan version control system dengan layanan penyimpanan cloud

### **Perbedaan Git dan GitHub**

- Git disimpan secara lokal, GitHub disimpan dalam cloud
- Git diakses secara offline, GitHub diakses secara online

### **Tujuan Penggunaan Git dan GitHub**

- Sangat dibutuhkan sebagai platform kolaborasi antar programmer
- Dapat mencatat seluruh perubahan dan siapa pengubahnya
- Dapat menyimpan file secara efektif
- Memungkinkan programmer untuk mengerjakan projek secara paralel

### **Alur Git dan GitHub**

- Download Git dan ikuti proses instalasinya
- Cek apakah Git berhasil terinstall dengan command `git --version`
- Lakukan konfigurasi nama dan email sesuai GitHub
  ```
  $ git config --global user.name "John Doe"
  $ git config --global user.email "email@example.com"
  ```
- Cek keberhasilan konfigurasi dengan `git config --list`

### **Git Repository**

- Repository merupakan tempat atau direktori dimana projek kita dibuat
- Repository dibuat dengan perintah `git init <project-name>` atau `git init .` jika folder sudah dibuat

### **Git Status**

- Perintah `git status` memungkinkan kita untuk memantau kondisi perubahan yang terjadi pada tracked dan untracked file
- Terdapat 3 macam kondisi pada file
  - modified: terdapat perubahan yang belum ditandai dan belum disimpan
  - staged: perubahan sudah titandai tetapi belum disimpan
  - commited: perubahan disimpan dalam version control system
    ![git status](./images/git-status.png)

### **Git Add**

- Perintah `git add` memungkinkan kita untuk mengubah status untracked file menjadi unmodified (staged)
- Perintah `git add <source>` ditujukan untuk file yang spesifik, sedangkan `git add .` ditujukan untuk seluruh direktori

### **Git Commit**

- Perintah `git commit -m <commit-message>` memungkinkan kita untuk menyimpan perubahan pada virtual control system secara permanen

### **Git Log**

- Perintah `git log` memungkinkan kita untuk mendapat log mengenai siapa yang merubah, dan kapan perubahan terjadi
- Perintah `git log --oneline` dapat menampilkan log dengan lebih singkat
- Log dapat dilihat berdasarkan nomor versi, file, dan author

### **Mengecek Perubahan Isi File**

- Perintah `git diff` memungkinkan kita untuk mengetahui baris yang berubah pada file

### **Membatalkan Perubahan**

- Status belum stagged dan belum commited
  - Gunakan perintah `git checkout <source>`
- Status sudah stagged dan belum commited
  - Gunakan perintah `git reset <source>`
  - Akhiri dengan perintah `git checkout <source>`
- Status sudah commited
  - Gunakan perintah `git checkout <commit-code> <source>`
  - Tambahkan `git reset <source>`
  - Bisa juga menggunakan `git revert -n <commit-code>`

### **Publikasi Aplikasi ke Github**

- Buat akun
- Buat repo baru dan sesuaikan setting repo dengan kebutuhan
- Jalankan perintah `git remote add origin <link>`
- Upload file dari lokal dengan `git push -u origin main`

### **Cloning Github ke Local**

- Gunakan perintah `git clone <link>`

---

## **Summary Module 3 - HTML**

### **HTML**

- HTML kependekan dari Hypertext Markup Language
- Berfungsi untuk menampilkan konten pada browser
- Konten berupa teks, gambar, video, link, audio, dsb

### **Tools Pendukung HTML**

- Browser: google chrome, mozilla firefox, microsoft edge
- Code editor: visual studio code, sublime text, atom

### **Dasar-Dasar HTML**

- Struktur HTML

  ```
  <!DOCTYPE html>
  <html>
    <head>
      <meta>
      <title></title>
    </head>
    <body>
      <p>This is a paragraph</p>
    </body>
  </html>
  ```

  - HTML ditulis dalam tingkatan-tingkatan (nested)
  - Elemen yang berada di dalam elemen lain disebut child
  - Elemen yang berada di atas elemen lain disebut parent

- Elemen HTML

  - Segala bagian HTML yang tersusun atas opening tag, content, dan closing tag

- Anatomi HTML

  ```
  <p>This is a paragraph</p>
  ```

  - Elemen HTML terdiri atas 3 bagian, yaitu opening tag, content, dan closing tag
  - Ada elemen yang tidak memiliki closing tag atau content seperti img, input, dan br

- Atribut HTML

  ```
  <img id="logo" src="./asset/logo.png">
  ```

  - Properti yang dimiliki oleh elemen HTML

- Komentar HTML

  ```
  <!--Ini adalah komentar-->
  ```

  - Bagian dari HTML yang tidak ditampilkan pada browser
  - Berfungsi untuk menjelaskan kode

### **Menjalankan HTML**

- Cara 1
  - Copy path dimana file HTML berada
  - Paste path di browser
- Cara 2
  - Install ekstensi VS code bernama live server
  - Buka file HTML menggunakan VS code
  - Tekan Go Live di bagian kanan bawah

### **Tag yang Populer**

```
<img src="" alt="">
```

- menampilkan gambar

```
<video>
  <source src="" type="">
</video>
```

- menampilkan video

```
<table>
  <tr>
    <th></th>
    <th></th>
    <th></th>
  </tr>

  <tr>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>

```

- membuat tabel

```
<form>
  <label for=""></label>
  <input type="" name="">
</form>
```

### **Semantic HTML**

- Tag-tag HTML yang memiliki arti atau memberikan konteks pada struktur web
- Contohnya adalah header, nav, section, article, aside, footer
- `<div class="header">` dapat diganti dengan tag `<header>`
- Kegunaan Semantic HTML:

  - Dapat meningkatkan aksesibilitas
  - Meningkatkan SEO
  - Lebih mudah dimaintain

### **Deploy HTML**

- Deployment adalah proses untuk mempublikasikan aplikasi kita sehingga dapat diakses pihak lain
- Dalam konteks aplikasi web, kita perlu men-deploy ke server
- Deployment HTML dapat menggunakan tools bernama Netlify
- Tahap deployment Netlify:
  - Buat akun Netlify
  - Pilih add new site
  - Pilih sumber file
  - Deploy aplikasi
