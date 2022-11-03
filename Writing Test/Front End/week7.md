# Writing Test Front-End Week 7

## **Prop Types**

### **Mengirim Data dengan Tipe Tertentu**
- Ketika kita mengirim data ke props, bisa saja kita memanipulasi data tersebut
- Jika tipe data tidak sama, maka hasil manipulasi data menjadi tidak sesuai
- Misalnya operasi penjumlahan antara data string dan number hasilnya akan berbeda

Contoh kasus
```
const Profile = ({name, age}) => {
    return (
        <>
            <p>{name}</p>
            <p>umur saya 5 tahun lagi adalah {age + 5}</p>
        </>
    )
}
```
- jika data yang dikirim pada age berupa string "20", maka akan ditampilkan 205
- jika data yang dikirim pada age berupa number 20, maka akan ditampilkan 25

### **Prop Types**
- Memungkinkan kita untuk memeriksa data props yang dikirim
- Jika tidak sesuai, maka akan ditampilkan error

### **Install & Import PropTypes**
- install prop types dengan command berikut
```
npm install prop-types
```
- import prop types dengan statement berikut
```
import PropTypes from 'prop-types';
```

### **Menggunakan Prop Types**
- Masukkan prop types ke dalam component
- Prop types ditulis di bagian bawah sebelum export
- Prop types ditulis dengan sintaks berikut:
```
namaComponent.propTypes = {};
```
Contoh penggunaan
```
const Profile = ({name, age}) => {
    return (
        <>
            <p>{name}</p>
            <p>umur saya 5 tahun lagi adalah {age + 5}</p>
        </>
    )
}

Profile.propTypes = {
    name: PropTypes.string,
    age: PropTypes.number
}
```
- jika data name yang diberikan bukan string dan data age bukan number, maka akan ada pesan error
```
<Profile name={'Rendra'} age={22} />
- Tidak akan ada error
```
```
<Profile name={'Rendra'} age={"22"} />
```
- Akan ada error karena data yang diberikan ke prop age bukanlah number

### **Prop Types Any**
- Gunakan keyword `any` agar bisa menerima berbagai data types
```
Profile.propTypes = {
    name: PropTypes.any,
    age: PropTypes.number
}
```
### **Prop Types isRequired**
- isRequired mewajibkan adanya data yang dikirim ke props
- Jika tidak ada data, maka akan ditampilkan error
```
Profile.propTypes = {
    name: PropTypes.any.isRequired,
    age: PropTypes.number
}
```

### **Prop Types One of Type**
- Dapat menerima data dengan beberapa opsi tipe yang ditentukan
- Jika sudah memenuhi salah satu tipe saja, maka tidak akan ada error
```
Profile.propTypes = {
    telefon: PropTypes.oneOfType([PropTypes.string, PropTypes.number])
}
```

### **Prop Types arrayOf**
- Kita tidak hanya dapat mengecek apakah data yang dikirim adalah array
- Kita juga bisa mengecek isi yang ada di dalam array tersebut dengan `arrayOf`
```
Profile.propTypes = {
    data: PropTypes.arrayOf(PropTypes.number)
}
```
Contoh kombinasi arrayOf dan oneOfType
```
Profile.propTypes = {
    data: PropTypes.arrayOf(
        PropTypes.oneOfType([PropTypes.number, PropTypes.string])
    )
}
```

### **Prop Types Shape**
- Kita tidak hanya dapat mengecek apakah data yang dikirim adalah object
- Kita juga bisa mengecek isi yang ada di dalam object tersebut dengan `shape`
```
Profile.propTypes = {
    data: PropTypes.shape({
        nama: PropTypes.string,
        age: PropTypes.number,
    })
}
```

### **Prop Types Exact**
- Shape memperbolehkan key lain yang dikirimkan di luar ketentuan shape
- Dengan `exact`, key pada object yang dikirimkan harus sama persis
- Jika mengirim object dengan isi key yang lebih atau berbeda dari ketentuan, maka akan muncul error
```
Profile.propTypes = {
    data: PropTypes.exact({
        nama: PropTypes.string,
        age: PropTypes.number,
    })
}
```
- Bisa juga digabungkan dengan isRequired agar data diwajibkan untuk dikirim
```
Profile.propTypes = {
    data: PropTypes.exact({
        nama: PropTypes.string,
        age: PropTypes.number,
    }).isRequired,
}
```

---

## **React Router**

### **Apa itu React Router?**
- React router memungkinkan kita untuk berpindah-pindah halaman dalam single page app
- Ketika kita berpindah halaman tidak memerlukan reload
- Kita tidak benar-benar berpindah halaman, tetapi mengganti halaman dengan component lain sesuai rutenya

### **Tahap Instalasi**
- Install react router dom melalui CLI
    ```
    npm install react-router-dom@6
    ```
- import package tersebut ke main.jsx
    ```
    import { BrowserRouter } from "react-router-dom";
    ```
- Bungkus component app dalam tag BrowserRouter
- BrowserRouter memberitahu bahwa kita sedang memakai react router
- Elemen apapun yang dibungkus dengan BrowserRouter akan dapat menggunakan react router
    ```
    <BrowserRouter>
        <App />
    </BrowserRouter>,
    ```
- import komponen, komponen lain jika diperlukan
    ```
    import { Routes, Route, Link } from "react-router-dom";
    ```
- Routes: membungkus berbagai route yang ada
- Route: dipakai di dalam routes, berisi path yang kita tuju
- Link: memungkinkan kita untuk berpindah ke route yang berbeda

### **Route**
- Route ditulis di dalam Routes
- Di dalam tag Route terdapat atribut path dan element
- Path berisi informasi alamat rute
- Element berisi komponen yang ditampilkan ketika masuk ke rute tersebut

Contoh
```
import Home from './pages/Home'
import About from './pages/About'

...

<Routes>
    <Route path="/" element={<Home />} />
    <Route path="about" element={<About />} />
</Routes>
```
- Ketika mengakses url `/`, maka elemen Home akan ditampilkan
- Ketika mengakses url `/about`, maka elemen About akan ditampilkan
- Jangan lupa import element yang ditampilkan terlebih dahulu

### **Link**
- Link memiliki fungsi yang sama seperti anchor tag
- Memiliki atribut `to` yang berisi alamat rute yang dituju
    ```
    <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
    </nav>

    <Routes>
        <Route path="/" element={<Home />} />
        <Route path="about" element={<About />} />
    </Routes>
    ```
- Jika Home pada nav diklik, maka rute akan diarahkan ke path `/`, elemen Home akan ditampilkan
- Jika About pada nav diklik, maka rute akan diarahkan ke path `/about`, elemen About akan ditampilkan

### **Params**
- Memungkinkan untuk mengirim data ketika mengakses path
- Ditulis dengan keyword `:`

Contoh

- Misal di halaman yang memuat banyak produk, kita ingin ketika memilih salah satu produk, maka detail produk tersebut akan ditampilkan
- Kita perlu mengangkap id produk tersebut agar data yang diambil sesuai dengan produk yang kita pilih
- Maka kita berikan param id yang merepresentasikan id product pada database
    ```
    <Route path="products/:id" element={<Product />} />
    ```
    ```
    cobacoba.com/products/2
    ```
- Kita dapat menuliskan param maupun mengambil data dari param

### **useNavigate**
- Cara untuk berpindah halaman sekaligus mengirim data
- Dengan useNavigate, kita dapat mengirim data lewat param
    ```
    import {useNavigate} from 'react-router-dom'

    const navigation = useNavigate();

    navigation('/products/${id}')
    ```

Contoh
```
const Products = () => {
    
  // panggil useNavigate ke dalam variabel agar mudah dipakai
  const navigation = useNavigate();

  // data yang dipakai
  let data = [
    { id: 1, name: "Topi", },
    { id: 2, name: "Kemeja", },
    { id: 3, name: "Celana", },
  ];

  const handleDetail = (id) => {
    // bawa id product ke url ketika mengklik produk tersebut
    navigation(`/detail/${id}`);
  };

  return (
    <>
      <h1>Pilih Produk yang Kamu Inginkan</h1>
      {data.map((el) => {
        return (
          <div key={el.id}>
            <h2>Nama: {el.name}</h2>
            <button onClick={() => handleDetail(el.id)}>Detail</button>
          </div>
        );
      })}
    </>
  );
};
```
- Kita bisa membuat event onClick yang menjalankan useNavigate ketika diklik
- event handler onClick tersebut dapat diberi argumen id untuk kemudian diberikan kepada useNavigate

### **useParams**
- Kita dapat menangkap params yang ada pada path url dengan `useParams`
- Params akan ditangkap dalam bentuk object
```
import { useParams } from 'react-router-dom'

// misal kita berada di url products/2

const { id }  = useParams();
console.log(id);

// maka akan tampil angka 2 pada console
```
- Data dari params dapat diambil untuk kemudian dipakai atau dimanipulasi
- Misal untuk menampilkan data dengan id yang cocok, kita bisa gunakan method filter pada params yang telah diambil
```
const { id }  = useParams();

...

return (
    <>
      {detailInfo
        .filter((el) => el.id === +id)
        .map((el) => {
          return (
            <div key={el.id}>
              <h2>Name: {el.name}</h2>
              <h2>Address: {el.address}</h2>
              <h2>Hobby: {el.hobby}</h2>
            </div>
          );
        })}
    </>
  );
```

### **Nested Route**
- Misal kita memiliki path 'sekolah.com/about'
- Pada path tersebut, terdapat beberapa path lanjutan seperti 'ajarin.com/about/student', 'sekolah.com/about/teacher'
- Tanpa nested route maka akan ditulis sebagai berikut
    ```
    <Route path="/about" element={<About />} />
    <Route path="/about/student" element={<Student />} />
    <Route path="/about/teacher" element={<Teacher />} />
    ```
- Dengan nested route, kita tidak perlu menuliskan parent path
    ```
    <Route path="/about" element={<About />}>
        <Route path="student" element={<Student />} />
        <Route path="teacher" element={<Teacher />} />
    </Route>
    ```

### **Outlet**
- Kita tidak dapat langsung mengakses nested path
- Parent dari nested route tersebut perlu kita beri Outlet
- Ini dilakukan agar child dideteksi oleh parent
    ```
    import {Outlet} from 'react-router-dom'

    ...

    return (
        <>
            <Outlet />
            <h1>Halaman About</h1>
        </>
    )
    ```

### **Index**
- Index memungkinkan kita untuk memprioritaskan child Route dari child lainnya
- Ketika salah satu child Route memiliki atribut index, maka secara default ialah yang akan ditampilkan
- Tidak perlu menuliskan path karena path-nya sama dengan parent
```
<Route path="/about" element={<About />}>
    <Route index element={<School />} />
    <Route path="student" element={<Student />} />
    <Route path="teacher" element={<Teacher />} />
</Route>
```
- Ketika kita mengakses path `/about`, maka elemen School juga akan ditampilkan

### **Memanggil Child Route di Route Selain Parent**
- Cukup gabungkan path dari parent dan child ketika ingin mengaksesnya
    ```
    <Route path="/about" element={<About />}>
        <Route path="student" element={<Student />} />
        <Route path="teacher" element={<Teacher />} />
        <Route index element={<School />} />
    </Route>
    ```
    ```
    // Component lain
    <Link to={about/student}>About Student</Link>
    ```

---

## **React Redux**

### **Latar Belakang Masalah**
- Misalkan terdapat data yang dibutuhkan oleh berbagai nested component
- Data tersebut diterima menggunakan props
- Props diberikan pada parent, lalu diberikan pada child, lalu diberikan pada child dari child tersebut, dan seterusnya
- Ketika terdapat perubahan pada props parent, maka props pada nested component perlu diganti juga
- Hal tersebut akan semakin rumit ketika terdapat banyak sekali nested component yang menerima data tersebut
- Masalah ini disebut dengan **props drilling**
![prop drilling](../images/prop%20drilling.png)

### **Solusi Props Drilling**
- Data disimpan ke dalam satu pusat yang independen
- Data tidak perlu dioper antara parent dan child
- Tiap component bisa langsung mengambil data dari pusat tersebut
- Solusi tersebut dinamakan dengan **state management**
![state management](../images/state%20management.png)
- Contoh tools state management:
    - Redux
    - Context
    - Jotai
    - Zustand

### **Instalasi Redux**
- Jalankan command berikut pada folder react app
    ```
    npm install react-redux
    ```
- Install redux core
    ```
    npm install redux
    ```

### **Langkah-Langkah Menggunakan Redux**
**1. Setup store sebagai pusat data**
- Buat folder redux dan buat folder store di dalamnya
- Buat file index.js, setup store di file tersebut
- Gunakan function `createStore`
    ```
    import { createStore } from 'redux'

    let store = createStore(() => {})
    ```
**2. Buat function reducer**
- Buat folder reducer di dalam folder redux tadi
- Buat file js untuk menampung reducer, misal chartReducer.js
- Inisialisasi data yang akan dipakai dan reducer
    ```
    const initialState = {
        keranjang: 0
    }

    function chartReducer(state = initialState, action) {
        switch (action.type) {
            default: 
                return state
        }
    }
    ```
- Ada 2 parameter pada function reducer, yaitu state dan action
- State mengacu pada data yang akan diberikan ketika dipanggil oleh suatu component
- Set initial state menjadi default state dari reducer
- Switch nantinya digunakan untuk memilih action terhadap state
- Action merupakan suatu kegiatan untuk memanipulasi data
- Panggil function reducer ke store yang telah dibuat
    ```
    let store = createStore(chartReducer)
    ```
**3. Buat agar store dapat diakses component dengan provider**
- Kita perlu memberitahu bahwa store tersedia untuk component yang membutuhkan
- Tools tersebut dinamakan dengan **Provider**
- Provider disediakan oleh react-redux
- Di file main.jsx, import provider
- Bungkus component App di dalam Provider agar store dapat diakses seluruh component di dalamnya
    ```
    import {Provider} from 'react-redux'
    import store from '.redux/store'

    ...

    <Provider store={store}>
        <App />
    </ Provider>
    ```
### **Mengambil Data dari Store**
- Ambil data dari store menggunakan hooks `useSelector`
    ```
    // file component yang membutuhkan data di store

    const { keranjang } = useSelector(state => state)
    ```
- useSelector akan mengambil data dari store
- Di dalam store ada function reducer
- Karena tidak melakukan action apapun, reducer akan mengembalikan nilai state default

### **Membuat Action**
- Buat folder action di dalam folder redux dan buat file js untuk menampung action
- Pada dasarnya, action adalah sebuah object dengan properti type
    ```
    export const INCREMENT_CHART = "INCREMENT_CHART"
    export const DECREMENT_CHART = "DECREMENT_CHART"

    export function incrementChart() {
        return {
            type: INCREMENT_CHART
        }
    }

    export function decrementChart() {
        return {
            type: DECREMENT_CHART
        }
    }
    ```
- Import action ke file reducer
- Tambahkan action pada switch
- Pada tiap-tiap case, kita dapat melakukan manipulasi state sesuai yang diinginkan
    ```
    const initialState = {
        keranjang: 0
    }

    function chartReducer(state = initialState, action) {
        switch (action.type) {
            case INCREMENT_CHART:
                return {
                    keranjang: state.keranjang + 1
                }
            case DECREMENT_CHART:
                return {
                    keranjang: state.keranjang - 1
                }
            default: 
                return state
        }
    }
    ```

### **Mengakses Action dengan useDispatch**
- Buat component yang ingin menjalankan action
- Pada contoh ini, component counter ingin menggunakan action increment dan decrement pada state
    ```
    function Counter = () => {
        const [count, setCount] = useState(0);

        const increment = ()  => {
            setCount(count + 1)
        }

        const decrement = () => {
            setCount(count - 1)
        }

        return (
            <>
                <button onClick={decrement}>-</button>
                <span>{count}</span>
                <button onClick={increment}>+</button>
            </>
        )
    }
    ```
- Untuk menjalankan action, kita membutuhkan hooks **useDispatch**
- import useDispatch dan action-action yang telah dibuat tadi
    ```
    import {useDispatch} from 'react-redux'
    import {incrementChart, decrementChart} from '../redux/action/chartAction'
    ```
- Jalankan action di dalam useDispatch
    ```
    const dispatch = useDispatch();
    const [count, setCount] = useState(0);

    const increment = ()  => {
        dispatch(incrementChart())
        setCount(count + 1)
    }

    const decrement = ()  => {
        dispatch(decrementChart())
        setCount(count + 1)
    }
    ```