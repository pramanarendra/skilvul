# Writing Test Front-End Week 7

## **React Context**

### **Apa Itu React Context**
- Context bertujuan untuk mengatasi prop drilling seperti redux
- Memungkinkan penyaluran data pada struktur tree tanpa perlu melalui props secara manual pada tiap level
- Digunakan untuk sharing data yang bersifat global
- Contoh: data user, tema, atau bahasa
- Bukan state management karena dia hanya mengatur alur pendistribusian data, bukan menyimpan state apapun

### **Langkah-Langkah Menggunakan Context**
**1. Buat Context Component**
- Import dan masukkan `createContext()` ke dalam variabel lalu diekspor
  ```
  import React, { createContext } from 'react'

  export const KeranjangCountContext = createContext()
  ```
**2. Buat Function Provider**
- Berikan parameter children yang nantinya akan menerima component lain yang bisa mengakses state
- Buat state yang digunakan untuk menampung data dinamis
- Return dalam bentuk provider
- Berikan atribut value yang berisi getter dan setter state
- Masukkan parameter children ke dalam provider pembungkusnya
  ```
  function KeranjangCountProvider({children}) {
    const [keranjangCount, setKeranjangCount] = useState(0)

    return (
      <KeranjangCountContext.Provider value={{keranjangCount, setKeranjangCount}}>
        {children}
      </KeranjangCountContext.Provider>
    )
  }

  export default KeranjangCountProvider
  ```

**3. Ambil dan Ubah Data dengan useContext**
- Gunakan `useContext` dan isikan argumen berupa context component yang telah dibuat
- Akses setter atau getter state seperti ketika mengakses object
  ```
  import React, { useContext } from 'react'

  function Keranjang() {
    const stateKeranjang = useContext(KeranjangCountContext)
    const totalKeranjang = stateKeranjang.keranjangCount

    return (
      <div>
        <span> {totalKeranjang}</span>
      </div>
    )
  }
  ```

  ```
  import React, { useContext, useState } from "react";
  import { KeranjangCountContext } from "../KeranjangCountProvider";

  function Counter() {
    const { keranjangCount, setKeranjangCount } = useContext(KeranjangCountContext)

    const increment = () => {
      setKeranjangCount(keranjangCount + 1)
    };

    const decrement = () => {
      setKeranjangCount(keranjangCount - 1)
    };

    return (
      <>
        <button onClick={decrement}>-</button>
        <span>{keranjangCount}</span>
        <button onClick={increment}>+</button>
      </>
    );
  }

  export default Counter;
  ```

---

## **React Context with useReducer**

### **Apa Itu useReducer**
- Merupakan alternatif dari useState
- Digunakan ketika memliki logika state yang kompleks
- Misalnya ketika state berikutnya bergantung pada state sebelumnya
- Lebih efisien ketika struktur tree cukup dalam
- Update tidak silakukan secara callback tetapi menggunakan dispatch
- Cara kerjanya mirip seperti Redux
- Tidak perlu instalasi tambahan selain React

### **Langkah-Langkah**
- Berikut adalah langkah-langkah penggunaan useReducer pada aplikasi counter
1. Buat context
    ```js
    export const CounteContext = createContext()
    ```
2. Buat initial state
    ```js
    const initialState = {
      count: 0
    }
    ```
3. Buat reducer
    ```js
    function reducer(state, action) {
      switch (action.type) {
        default: return state
      }
    }
    ```
4. Masukkan pada useReducer di dalam context
    ```js
    function CounterProvider({children}) {

      const [state, dispatch] = useReducer(reducer, initialState)

      return (
        <CounterContext.Provider value={{}}>
          {children}
        <CounterContext.Provider>
      )
    }
    ```
5. Buat action
    ```js
    const INCREMENT = "INCREMENT"
    const DECREMENT = "DECREMENT"

    function CounterProvider({children}) {

      ...

      const increment = () => {
        dispatch({type: INCREMENT})
      }

      const decrement = () => {
        dispatch({type: DECREMENT})
      }

      ...

    }
    ```
6. Masukkan action pada switch
    ```js
    function reducer(state, action) {
      switch (action.type) {
        case INCREMENT:
          return {count: state.count + 1}
        case DECREMENT:
          return {count: state.count - 1}
        default: return state
      }
    }
    ```
7. Masukkan state pada useReducer dan function dispatch increment decrement dalam value provider
    ```js
    return (
      <CounterContext.Provider value={{ state, increment, decrement }}>
        {children}
      <CounterContext.Provider>
    )
    ```
8. Gunakan state dan action pada component lain
    ```js
    function Counter() {
      const {state, increment, decrement} = useContext(CounterContext);

      return (
        <div>
          <button onClick={decrement}>-</button>
          <span>{state.count}</span>
          <button onClick={increment}>+</button>
        </div>
      )
    }
    ```
---

## **React Testing**

### **Testing**
- Testing bertujuan untuk memastikan apakah hasil atau behavior program sesuai dengan ekspektasi

### **Tipe Testing**
**1. Manual**
- Melakukan testing secara langsung
- Bergantung pada keletiliat penguji
- Misalkan melakukan log pada console untuk mengetahui isi suatu variabel

**2. Automation**
- Membuat kode testing
- Kode tersebut yang melakukan pengujian
- Bergantung pada kualitas kode testing

### **Tipe-Tipe Automation Testing**
**1. Unit Testing**
- Melakukan pengujian pada bagian terkecil dari program
- Misalkan menguji function yang dibuat
- Bisa dilakukan oleh developer
- Costnya kecil dan prosesnya cepat

**2. Integration Testing**
- Melakukan testing bagian yang saling terhubung
- Misalkan melakukan testing antara aplikasi dengan database

**3. End-to-End Testing**
- Melakukan testing dari sisi pengguna
- Misalkan experience user ketika berpindah-pindah halaman
- Biasanya perlu seorang QA engineer dan software khusus
- Prosesnya lama dan costnya besar

### **Tools Testing**
- Jest: Library Javascript untuk melakukan testing
- React Testing Library: sudah include jest, unit test yang semi end-to-end

### **2 Cara Menulis Testing**
Buat fitur terlebih dahulu baru testing
  - Dilakukan untuk proses dan waktu yang terbatas

Buat testing dahulu lalu buat fitur
  - Proses lebih lama tetapi lebih terjamin

### **Test-Driven Development**
- TDD merupakan suatu siklus pengembangan program
- Terdiri atas red zone, green zone, dan blue zone
- Red zone: ketika kode belum memenuhi ekspektasi
- Green zone: ketika kode memenuhi ekspektasi
- ketika kode memenuhi ekspektasi
- Blue zone: proses optimasi kode ketika sudah melewati ekspektasi

#### **Membuat Testing**
- Menulis testing memerlukan proses yang lama
- Spesifikasi mengenai ekspektasi dan behavior program harus jelas
- Baik tidaknya program test ditentukan dari banyaknya case yang dites

### **Library Testing Jest**
**Instalasi Jest**
  ```
  npm install -D jest
  ```

**Testing dengan Jest**
```js
test('', () => {})
```
- Testing dilakukan dengan method test()
- Memiliki 2 parameter
- Parameter pertama berisi string bebas
- Parameter kedua berisi callback function yang berisi test yang akan dijalankan

**Contoh Testing dengan Jest**
- misal kita ingin membuat testing fungsi penjumlahan
1. Buat fungsi yang akan dicek
    ```js
    function sum(x, y) {
      return x + y
    }

    module.exports = sum
    ```

2. Buat file testing app.test.js
3. Buat program testing di dalamnya
    ```js
    test('testing fungsi penjumlahan', () => {
      expect(sum(0,0)).toBe(0)
      expect(sum(0,1)).toBe(1)
      expect(sum(1,1)).toBe(2)
      expect(sum(2,2)).toBe(4)
    })
    ```
    - Gunakan method test()
    - Isikan test dengan berbagai ekspektasi case-case yang terjadi
    - Gunakan method expect dengan argumen fungsi yang dites
    - Gunakan toBe untuk menuliskan ekspektasi hasil dari fungsi tersebut
4. Jalankan Testing dengan Jest
    ```
    "scripts": {
      "test": "jest"
    }
    ```
    - Tambahkan script di package.json
    ```
    npm run test
    ```
    - Jalankan script test tersebut
    - Akan muncul berbagai keterangan mengenai case-case yang kita buat
    - Case yang normal akan diberi keterangan passed
    - Jika ada case yang salah, maka akan ditampilak informasi seperti expected result dan received data

### **Jest Matchers**
- Pengecekan nilai dengan Jest dapat dilakukan dengan banyak cara
- Salah satu yang paling sederhana adalah expect dengan toBe
- Beberapa matchers lainnya yang umum dipakai:
  - Truthiness: toBeNull, toBeUndifined
  - Numbers: toBeGreaterThan, toBeLessThan
  - Strings: .not.toMatch, .toMatch
  - Array: toContain

### **jest --coverage**
- Untuk mencari tahu seberapa banyak bagian program yang sudah dites
- Akan menampilkan informasi banyak statement, branch, functions, dan lines yang telah dites
  ```
  "scripts": {
    "test": "jest --coverage"
  }
  ```

### **React Testing Library**
- Testing library yang tersedia pada React
- Berisi paket-paket yang dapat melakukan tes komponen UI dalam sudut pandang user
- Sudah secara otomatis terinstall pada react
- File App.test.js adalah file testing tersebut
  ```js
  test('render learn react link', () => {
    render(<App />);
    const linkElement = screen.getByText(/learn react/i);
    expect(linkElement).toBeInTheDocument();
  })
  ```
  Penjelasan:

  - render komponen App -> cari apakah ada tulisan learn react -> ekspektasinya, elemen itu ada di dokumen

- Jalankan testing dengan
  ```
  npm run test
  ```

### **Test Block**
- Tahapan test pada RTL terdiri atas beberapa langkah, yaitu
  1. render component yang akan dites
  2. cari elemen dengan screen getby...
  3. interaksi dengan elemen tersebut (opsional)
  4. menyatakan hasil tes

### **Describe Block**
- Kumpulan dari test block

### **Query**
- Terdapat berbagai query yang bisa digunakan pada RTL
- Salah satu yang paling umum adalah getByText
- Contoh:
  ```js
  import {render, screen} from '@testing-library/react'
  import Counter from './Counter'

  test('render counter', () => {
    render(<Counter />)
    const decrementBtn = screen.getByText("-")
    const incrementBtn = screen.getByText("+")

    expect(decrementBtn).toBeInTheDocument()
    expect(incrementBtn).toBeInTheDocument()
  })
  ```

### **Access by Everyone**
- Query yang dapat elemen yang tampak
- getByRole, getByLabelText, getByPlaceholderText, getByText

### **Semantic Queries**
- Query yang tidak dapat dilakukan melalui role atau text
- Misalnya pada data teks yang dinamis
- getByTextId

### **fire event**
- Program mensimulasikan seolah-olah menjadi user yang menjalankan event pada browser
- Seperti event click, hover, dan focus
- Contoh testing pada counter
  ```
  test('increment button test', () => {
    render(<Counter />)
    const incrementBtn = screen.getByText("+")
    const count = screen.getByText("0")

    expect(count.textContent).toBe("0")
    
    fireEvent.click(incrementBtn)
    expect(count.textContent).toBe("1")
  })
  ```
- fireEvent click akan mensimulasikan ketika increment button diklik
- kemudian akan dicek apakah nilainya berubah dari 0 menjadi 1
