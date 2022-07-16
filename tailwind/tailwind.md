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

- Resource untuk pattern background bisa gunakan -> heropatterns.com

  - Selalu sesuaikan foreground dan background color dengan pattern yang dibagai sebagai background
  - Heropattern berupa svg yang langsung paste ke css tanpa simpan asset bg

- Untuk mengakali new line untuk resolusi tertentu contohnya `<br class="sm:hidden">`

  - Case ini bisa terjadi ketika ada perbedaan antara chrome dan safari

# Tailwind Udemy

- Penggunaan lang pada html `<html lang="en">` berpengaruh juga pada style dari output html yang dirender oleh browser
- Di [tailwindui.com](http://tailwindui.com) terdapat predefined template yang bisa kita pakai (tapi harus bayar)
- Dark Mode
    - Tambahkan properti darkMode di tailwind.config.js
    - Nilainya ‘class’ (toggle class) atau `media` (tergantung setting dark mode di perangkat)
    - Tambahkan di body class dark
    - Misal apply nya `<h1 class="dark:yellow">`
    - Bisa juga di tambahkan pada @apply di tailwind.css
    - Jadi hanya dengan toggle class dark
- Gunakan purgecss untuk minimalkan css yang tidak diperlukan pada project tailwind
    - npm install @fullhuman/postcss-purgecss
    - Tambahkan pada tailwind.config.js properti purge pada dist
- Cek di package tailwindcss → stubs → defaultConfig.stub.js
    - Atau lihat di [unpkg.com](http://unpkg.com) route file tersebut
    - Disana terdapat semua default dari color, point, space, dll
    - Jika ingin custom suatu untuk menimpa default, di tailwind.config.js tambahkan properti di extends misal `spacing: { 13: ‘3.25rem’ }` , jika diluar extends maka akan menimpa semua properti
    - Contoh lain jika ingin custom screen misal namai phone, tablet, pc, large monitor, dll
- Untuk menambahkan pallete colour kamu sendiri
    - Tambahkan require tailwindss/color di tailwind.config.js
    - Tambahkan di theme > colors untuk nama nama alias colors mu
- Untuk gradient ada bg-gradient-to-b from-gray-900 to-gray-400 h-screen bg-green-200
