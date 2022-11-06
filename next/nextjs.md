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
