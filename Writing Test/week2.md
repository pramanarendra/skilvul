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
