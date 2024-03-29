# Javascript Async

- Asyncronous
  - Syncronous -> eksekusi baris per baris
    - Proses syncronous disebut blocking (menunggu tiap eksekusi sebelumnya selesai, baru eksekusi setelahnya dijalankan)
    - Program di jalankan dalam thread
    - Thread adalah proses ringan terdiri id, counter, register, stack
    - Di browser, dijalankan di main thread (kalau sync)
  - Asyncronous
    - Proses asyncronous disebut non-blocking (tidak menunggu proses sebelumnya selesai. Dijalankan memang pasti ada yang duluan ketika call tapi sambil jalan paralel)
    - Ketika dijalankan async maka dijalankan oleh async thread
    - Async akan mengembalikan data melalui proses callback ke main thread
  - Callback
    - Memanggil kode dari proses asyncronous
    - Berupa bentuk function dipanggil ketika proses async sudah selesai atau ketika proses tertentu di async (untuk menandai progress)
    - Contohnya setTimeout (sekali), setInterval (periodik)
    - Gunakan live-server
    - Kalau misal cukup jalankan 1 function `setTimeOut(callback, 5000)` tapi kalau menjalankan kode lain `setTimeout(function() { //kodeapa; callback() }, 5000)`
  - AJAX
    - Asyncronous Javascript and XML (sekarang pakai json)
    - Dapat untuk mengambil data dari server setelah web tampil tanpa load ulang
    - Karena dulu request selalu render tampilan dan keseluruhan data (nanti bisa membebani resource server)
    - Dapat mengirim data ke server async di background
    - Ketika menerima data dari alamat mesin yang berbeda, maka akan kena CORS (dihalangi oleh browser untuk urusan keamanan), maka nyalakan CORS extension di browser (untuk development aja, kalau production tidak boleh karena bisa saja hacker melakukan phising, ngecall di localnya)
    - Ajax bersifat async maka tidak bisa ajax.responseText karena harus di callback
  - AJAX Callback
    - Gunakan ajax.onload
    - Bisa mendapatkan status
    - AJAX Error Callback
      - Dengan mengecek status 200 maka berhasil, maka proses lain maka error
  - Dynamic Callback
    - Menempatkan pemanggilan callback secara aggregation di argumentnnya, maka function utama tidak perlu diubah. Yang diubah adalah argument, parameter dan pemanggilan parameter di dalam
    - Jadi tidak hardcode ditulis secara composition
  - Promise
    - Permasalahan jika menemui callback hell
    - Proxy untuk sebuah nilai di masa depan future yang belum diketahui ketika pembuatan promise itu
    - Proxy untuk proses async dan lebih mirip kode sync
    - Penulisan kode menjadi lebih rapi dan mudah dibaca
    - state -> pending, fulfilled, rejected
    - result -> undefined, value, error
    - Untuk hasil reject bisa mengembalikan instance Error berisi value errornya atau keterangan
  - Promise Then
    - untuk mengambil resourse value yang sudah dibuat
    - Ketika sudah fulfilled/resolved
    - Membuat chain method (dengan retun data dari then sebelum nya, maka parameter callbacknya akan menjadi value dari return then sebelumnya)
  - Promise Catch
    - Ketika error
  - Promise Finally
    - Eksekusi kode ketika success atau error, ketika proses async tersebut
    - Function callback tidak ada parameter
  - Promise All
    - Ketika kita ingin memanggil proses async secara bersamaan dan ketika semuanya berhasil maka ke then, jika salah satu tidak berhasil maka catch error
    - Karena setiap proses async berjalan paralel maka promise all akan menunggu sampai semua prose async selesai
    - Menggabungkan promise-promise menjadi promise baru, hasilnya berisi array hasil promise promise tersebut
    - Jadi tidak membuat promise handle masing masing
    - Misalkan mencari 3 pencarian sekaligus
    - `Promise.all([promise1, promise2, promise3])`
  - Fetch API
    - API baru untuk melakukan AJAX
    - Fetch menggunakan promise (tidak perlu promise manual)
    - fetch terdiri dari url, config (header, method, request yang dikirim, mode, body)
    - Cek lengkapnya di dokumentasi
    - Defaultnya kalau mendapatkan datanya itu melalui kembalian body dari promisenya: Response (ubah dulu ke json)
      - Tambahkan di then return response.json()
  - Async await
    - Fitur baru untuk mempermudah penggunaan promise, ketika menggunakan promise dan callback yang banyak
    - Untuk mempermudah pembuatan kode promise
    - Gaya penulisannya seperti syncronous
    - Async menandakan function mengembalikan promise
    - Await digunakan untuk mendapatkan value hasil dari function async yang lain, yang di call di dalam function async tersebut
    - Await hanya bisa digunakan dalam async function
    - Jadi sebenarnya kode async await tersebut di translate oleh browser/server menjadi promise (tapi kita tidak perlu tahu soal itu)
    - Kalau ingin tahu coba di translate di babel.io
  - Async await error handler
    - Gunakan bungkus try-catch atau try-catch-finallly
    - Try seperti then, finally seperti finally di promise
    - Jika ada kesalahan di await atau salah kode di dalam try maka langsung ke catch
  - Web Worker
    - Javascript menggunakan single thread
    - Async tetap di 1 thread itu
    - Kemampuan 1 thread dalam mengelola bergantian beberapa pekerjaan disebut concurrent (thread setelah selesai, maka melanjutkan pekerjaan lain)
    - Kemampuan mengerjakan beberapa thread di sebut paralel (1 pekerjaan di kerjakan oleh beberapa orang, daripada 1 orang)
    - Untuk membuat paralel bisa menggunakan Web Worker (untuk browser modern)
    - Biasanya untuk eksekusi proses berat, tidak mengganggu main thread
    - Agar browser tidak freeze (sebenarnya javascript lagi proses berat, nanti akan normal kembali karena menggunakan main thread)
    - Web Worker akan mengeksekusi proses yang nantinya ketika selesai akan dikembalikan ke main thread
    - Web Worker adalah class maka perlu di instance
    - Tambahkan eventlistener di instance web worker
    - Kalau Web Worker not found kemungkinan browser yang digunakan belum support web worker
    - Agar UI tidak freeze di main threadnya

