Next.js Masterclass

- Next.js sebagai FE dan BE development framework

- Next.js punya keuntungan memudahkan SSR (server side rendering)

- Next.js bisa di deploy di vercel

- Tools untuk test performance PageSpeed Insight dan GTMetrix

- Next.js (React Framework) support Typescript

  - Routing based file -> kalau react biasa Routing dengan pass Component

  - Jadi routing dibuat dengan file baik param dynamic maupun fixed

  - Server Side Rendering (kalau di react data di baru render di client) maka strukturnya tidak terlihat jadi tidak baik SEO. Kalau render di server halaman sudah siap secara struktur dan datanya baru di kirim ke client (client tidak perlu render)

- Untuk backend API terdapat di pages/api, middleware, controller dan sebagainya

- Install Next.js

  - `npx create-next-app .` (folder yang sama / kosong)
  - default akan script next dan dependency next react dan react-dom
  - Jalankan build (untuk build app production) dan start (untuk menjalankan production, bukan dev)

- Backend Development

  - `npm install next-connect` (untuk routing dan middleware) bisa tanpa next-connect
  - Untuk tahu tentang penggunaan next-connect cek di github next.js/examples/api-routes/pages/api/people/[id].js
  - Bikin controller, bikin func req, res dan return status dan jsonnya dan export
    - Di folder api bikin file lalu import `import nc from 'next-connect'` func dari controller
    - `handler.nc()` lalu `handler.get(func_dari_controller)`
    - Bisa gunakan `handler.use(middleware).get(func_dari_controller)`
    - Jangan lupa `export default handler`

- Pakai variabel di postman di tab environment lalu bisa pindah-pindah environment dengan variabel yang sama tapi valuenya akan beda

- Buat folder config jika berhubungan setting koneksi database, firebase, 3rdparty dan sebagainya

- Jika berhubungan dengan database selalu import confignya di route

- `next.config.env` sebagai env untuk environment next.js

  - Harus gunakan module.exports lalu masukkan di object env trus property nya berupa string
  - Masukkan nilai seperti port, IP, connection, APIkey, token login dsb
  - Setiap perubahan di file ini perlu di restart servernya

- Buat folder config untuk config database, misal dbConnect.js untuk mongoDB

  - Masukkan env variabel di next.config.js
  - Gunakan next-connect sebagai pengganti express

- Selebihnya, semua pelajaran seperti Phase 1 hacktiv8 untuk controller, model, dsb

- Buat folder utils, gunakan sebagai penampung seeder.js

  - Buat folder data, untuk menyimpan data.json

- Untuk menggunakan update database gunakan PUT

- Buat class untuk ErrorHandler yang extends Error dengan harus ada statusCode, message and content

  - Buatkan middleware untuk error handler

- Buat folder middlewares

  - Buat error handler defaultnya 500 jika error code tidak ada

- Buat middleware berupa catchAsyncError agar menyederhanakan route endpoint tidak perlu menuliskan try catch di dalamnya dengan bentuk callback dan isi promise

- Handler error message harus lebih spesifik berdasarkan Validation dan ID error, misal error name, error path
  - Misalkan jika 400 harus pesannya apa, resource not found atau gimana
  - Tujuannya agar error mudah dipahami

- Jika tidak menggunakan ORM, bisa buat class utils/apiFeatures berisi class dengan constructor dengan prop query (Room.find()) dan queryString (req.query)
  - Berisi method search()
  - Gunakan $regex dan $options pada Mongo untuk memudahkan pencarian dynamic
  - Tujuannya untuk mengurangi penulisan ORM
  - Tambahkan juga method untuk pagination (bisa cek caranya di kode pekerjaan)

- Frontend HTML Template
  - Custom document di next documentation (override document default di next)
  - Buat di pages/_document.js (Taruh dari doc next template custom)
  - Import Document dan semua component2 dari next/document yang di pakai di template
  - Tambahkan style, head dan script external di component masing2
  - Buat Header dan Footer component berisi react func component seperti biasa
  - Layout berisi component dari Header dan Footer
  - Gunakan import next/head untuk mendapatkan SEO func
  - Wrap children dari prop Layout di dalam header dan footer

- Homepage
  - Home.module.css berarti itu aturan module css dari next di import ke component terkait
  - Kalau ingin mengubah style global, cukup ubah di globals.css karena sudah diimport di index.js
  - Jika home di dalam layout, maka home menjadi propnya

- Fetch Data
  - Untuk testing gunakan jsonplaceholder.typicode.com
  - Import next/link untuk gunakan komponen <link>
  - getStaticProps ketika build/load pertama, code dimasukkan ke dalam badan function
    - Bersifat pre-rendered, cocok untuk SEO
    - Gunakan fetch async
    - Gunakan untuk fetch data utama (misal tabel data / bukan detail (dinamis))
  - getServerSideProps
    - Buatkan [id].js untuk detail
    - Untuk memanfaatkan id atau param pakai context sebagai param function getServerSideProps lalu bisa pakai context.params.id
    - Gunakan untuk fectch dinamis setiap hit (misal detail data dari id param)
  - getStaticPath digunakan jika user ingin bypass dari URL (misal bookmark). Bukan by click dari halaman atau link next
    -

- Redux (state management)
  - Action : function untuk fetch / post data
  - Dispatch : function untuk call action berdasarkan type
  - Type : Constant yang dipakai sebagai condition state
  - Install redux dev tools
  - Install `npm i redux redux-thunk redux-devtools-extension react-redux next-redux-wrapper --save`
  - Buat folder redux (reducer, action, constants)
  - Buat store.js (config redux)

  - Jika ada error, tambahkan di reducer untuk case clear error

  - npm i next-absolute-url (untuk menghindari menulis localhost:3000 dsb ke semua fetch dan post axios) passing origin ke axios