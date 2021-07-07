# Typescript

- Typescript = Javascript + Type System
  - Karena javascript lumayan aneh dengan debug error yang sulit
- Type System => Mempermudah menangkap error, validasi dan meningkatkan kualitas kode
  - Anggap typescript seperti teman pair programming yang membetulkan kodemu
- Typescript mengubah bahasa ketika di compile oleh typescript compiler ke javascript
- Belajar https://www.typescriptlang.org/play



- Environment Typescript

  - Install `npm install -g typescript ts-node`

    - ts-node untuk run typescript dalam 1 perintah commandline 

  - Jalankan `tsc`

    - untuk help tambahkan `--help`

  - VSCode Setup untuk typescript

    - code path -> view > command pallete > install code to path
    - Extension Prettier
    - Preference > Setting > Check format on save && check prettier single quote && tab size 2 && hide actibity bar

    

- First Project Typescript menangkap bugs

  - https://jsonplaceholder.typicode.com/ (cari resourses dibawah - pilih todo)

  - Gunakan todo/1 untuk memilih salah satu data

  - mkdir fetchjson , cd fetchjson

  - npm init -y , npm install axios , code .

  - Buat index.ts

  - Buat program untuk fetch dari jsonplaceholder

  - Kita tidak bisa menjalankan typescript dari nodejs langsung. Jadi harus compile file ke javascript

  - tsc index.ts lalu node index.js

    - Shorthandnya ts-node index.ts

  - Nice format

    - Dengan template literal tapi akan error (karena typescript akan menghindarkan dari kerancuan nama variabel dan nama properti data yang diterima)
    - Tambahkan interface untuk memastikan data yang dipakai sesuai, seperti object template
    - Interface harus diterapkan untuk menyimpan nilai, interface tidak harus diterapkan ke semua data, cukup data yang dibutuhkan
    - Tandai data sesuai interface dengan `as`
    - Prettify akan memberi warning jika tidak menerapkan interface

  - Parameter di function harus punya tipe data (agar tidak sembarang mengisi tipe data untuk menghindari kesalahan ketika memproses di function)

    - Jika mengisi tipe data salah di argument, maka ada peringatan error
    - Peringatan biasanya berisi kenapa error di pop-upnya
    - Seringnya adalah salah urutan argument

    

  - Type System

    - Syntax + Features

      - Type adalah cara merefer ke properti berbeda dan function dimana nilai itu berada

        - Value di JS dan TS adalah assign ke variabel dalam bentuk string, number, array, object, class, function, dll
        - Semua function, class, array, object punya type
        - Misal string punya banyak method. Cont. includes(), indexOf(), dll
        - Interface merupakan salah satu Type
        - `response.data as Todo` berarti response.data ber type Todo
        - Interface yang kita buat berarti kita membuat Type sendiri selain yang type default dari Javascript

      - Kenapa Types Penting

        - Primitive Types: number, string, boolean, void, undefined, null, string, synbol
        - Object types: function, class, object, array
        - Type digunakan untuk typescript untuk menganalisa jenis error
        - Type digunakan agar engineer lain mudah memahami codebase dan alurnya (agar tidak sembarang menulis penamaan variabel dan function yang tanpa filter harus diisi tipe apa)

      - Contoh Type

        - Typescript memberi saran properti atau method ketika sudah initiasi, jika menulis properti salah maka ada tanda error
        - Object di typescript tidak bisa ditambahkan properti diluar object (karena akan merusak susunan object) maka akan error
        - Jika instance dari class mengakses method atau properti yang tidak ada dari class, maka error. Maka tetap harus ditulis dalam class

        

    - Type Annotation & Intefere

      - Type annotation adalah kode untuk memberitahu typescript tipe dari nilai sebuah variabel
        - developer memberitahu typescript
      - Type interfere adalah Typescript tahu tipe apa sebuah nilai
        - typescript menebak tipe
      - Jika kita menentukan tipe data dari variabel, lalu assign dengan tipe data lain maka error. Jika sejenis maka masih bisa
        - undefined dan null punya nilai yang sama dengan jenisnya
        - Date maka new Date()
      - Jika berupa array maka harus tipe dan []. Misal `let names: string[]` (jadi tidak membuat array tapi assign nya harus array of string)
      - Instance harus bertipe classnya. `let car: Car = new Car()`
      - Object literal lumayan ribet karena harus menggunakan { } berisi semua properti dan tipe datanya dipisah ; dan menulis properti dan value masing masing. Sifatnya seperti function di typescript
        - Jadi nama properti harus sama
      - Function di typescript butuh jenis type data di setiap parameter, tulis tipe data argumen (input) juga dan apa output nya return atau tidak. Misal jika tidak return gunakan void
        - Bagian awal function adalah type annotation, belakang adalah type interfere. Di awal adalah description
      - Inference
        - Perbedaan type inference atau langsung menulis tipe datanya

    - Design Pattern

