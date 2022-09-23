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
