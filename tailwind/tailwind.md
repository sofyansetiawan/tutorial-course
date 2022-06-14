# tailwind



Installation

- Pastikan nodejs versi terbaru
- npm init -y
- npm install tailwindcss postcss postcss-cli autoprefixer @fullhuman/postcss-purgecss
- npx tailwindcss init -p
  - tailwind.config.js (konfigurasi tailwind)
  - folder dist/ (distribution)
  - Type ! lalu TAB untuk dokumen html kosong
  - Library purgecss untuk menghapus css mana yang tidak terpakai (berguna untuk menghapus class tailwind yang tidak terpakai)

- Pasang styles di html dist

- Buat file tailwind.css

  - ```
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
    ```

- Tambahkan di package json

  - build dan watch perintah postcss tailwind ke dist

  - ```
    "build": "npx tailwindcss-cli@latest build -o dist/css/styles.css",
    
    "watch": "npx tailwindcss-cli@latest build -o dist/css/styles.css --watch"
    ```

- Tailwind terdiri dari 3

  - base (normalize untuk basic2 tag atau preset agar compatible untuk semua browser)
  - components (layouting, breakpoint, component form, dsb)
  - utilities (inetraktif, jarak, animasi)

- Tailwind css debug `npm i tailwindcss-debug-screens --save-dev`

  - Tambahkan ke dalam plugin tailwind.config.js
  - Tambahkan posisi debug nya di kiri atas di theme nya
  - Tambahkan di body class `debug-screens`
  - Maka akan keluar indikator lebar screen lg, md, xs, dsb

- Tailwind memudahkan untuk penggunaan x dan y dan angka untuk mempermudah identifikasi

- Tailwid juga menyediakan hasil matematika dari class misal `w-8/12` pada grid. Jadi menggunakan 8 dari 12

- Kita bisa tambahkan default value di tailwind.css sebagai @layer base dan @apply

- Tambahkan font dari google ke dalam folder asset atau dist compile

  - Tambahkan @font-face font-family dengan target relative ke /dist seperti import font-face css biasa ke dalam layer base file tailwind.css (css yang akan dicompile)

  - Tambahkan di tailwind.config.js 

  - ```
    extend: {
    fontFamily: {
    headLine: ['Oswald']
    }
    }
    ```

  - Tambahkan class ke element headline atau tambahkan ke tailwind css di bagian @apply

- Tambahkan color di theme > extend > colors > mainColor

  - Maka secara semantic akan menambahkan ke semua properti yang berhubungan color

- Extend adalah cara membuat properti2 dengan postfix lalu apply css nya sesuai categori

- Gunakan feathericon, material.io, zondicons, heropattern, heroicons untuk koleksi icon free (icon kecil), bg dan customized

  - Langsung copas content nya ke dalam kode html

- Gunakan class hover, focus, pseudoclass lain yang semantic di css tanpa selector tambahan `hover:bg-blue-100`

- Untuk response terdapat class untuk mengubah sesuai ukuran device misal `lg:bg-blue-200`