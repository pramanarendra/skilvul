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