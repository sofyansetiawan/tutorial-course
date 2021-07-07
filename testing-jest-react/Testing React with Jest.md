# Testing React with Jest

- create react app

  - memudahkan pembuatan aplikasi react
  - Sudah termasuk (tanpa setup rumit)
    - configurasi
    - webpack dan babel
    - web server
    - testing library
  - Download versi terakhir create react app dan ikuti instruksi install nya dan menjalankannya dalam `npx create-react-app`
  - Menjalankannya dengan `npm start`

- npm test

  - Masuk dalam watch mode
  - Ketik A untuk menjalankan semua test
  - Ketik Q untuk keluar dari test
  - Di file `App.test.js`
    - render => membuat virtual DOM, contohnya JSX App.jsx
    - screen => global object untuk akses virtual DOM
    - Berasal dari @testing-library/ react
    - `screen.getByText(/learn react/i)` => mencari dan element text yang mengandung konten learn react dalam regex case-insensitive
    - `expect(linkElement).toBeInTheDocument()` => disebut assertion (yang menyebabkan test menjadi berhasil atau gagal)
    - Terdapat error jika gagal berisi keterangan kenapa gagal, lokasi dan berapa test yang gagal

- Assetion

  - expect => global variabel untuk memulai assertion
  - expect argument => subject dari assertion
  - matcher => jenis assertion sesuai atau tidak subject dengan nilai argument. Berasal dari jest-dom
  - matcher argument => berisi argument pembanding dengan subject sesuai atau tidak
  - Contoh assertion:
    - element.textContent
      - toBe
    - elementsArray
      - toHaveLength
  - jest dom sudah termasuk dalam create react app
    - src/superTests.js => import package yang dibutuhkan oleh react untuk setiap test yang ada, misal test untuk masing masing page dan component react
    - DOM-based matcher
      - toBeVisible()
      - toBeChecked()
      - dll

- Jest

  - Jest react test library
    - rendering component ke virtual DOM
    - mencari virtual DOM
    - interaksi dengan virtual DOM
  - Jest sebuah test runner, ada test runner lain: mocha, chai, jasmine
  - Watch mode
    - Setiap perubahan akan menjalankan test (setiap file disave)
    - git commit -am "keterangan"
    - Jika tidak ada perubahan setelah commit terakhir, maka tidak ada test
    - Tapi tetap bisa jalankan A (test all)

- Test

  - test terdiri dari keterangan string
  - test function berupa callback
  - Apa saja yang menyebabkan error akan, akan menghentikan test. Jika tidak ada error maka pass

- TDD (test driven development)

  - Menulis test sebelum menulis kode program, menulis kode program tujuannya supaya pass test (maka kualitas softwarenya bagus)
  - Red-green function test fail baru menulis kode (write shell function -> write tests -> test failed -> write code -> test pass)
  - TDD membuat kode program sesuai keinginan dan spesifikasi yang detail, efektif dan mudah memahami flow dan maksud program secara pendekatan kode

- React Testing Library

  - Membuat virtual DOM
  - Testing tanpa browser secara otomatis
  - Type test
    - Unit Test -> test kode, block function yang terisolasi
    - Integration test -> antar unit atau microservices
    - Functional Test -> bagian dari software (behaviour bukan unit kode)
    - End to End test -> Browser dan server secara real misal menggunakan tools seperti selenium

- Simple Colour App

  - React memberitahu jika ada role salah, maka menampilkan role apa saja do component yang sedang di test
  - Setiap error dari testing library menampilkan juga output
  - Assertion (mis. expect) bisa lebih dari 1
  - fireEvent -> Cara berinteraksi seperti addEventListener pada DOM. Jadi jest mensimulasikan jika event dijalankan
  - Jika test gagal maka ada panah merah, menunjukkan dibagian kode apa test gagalnya (matcher)
  - Cara membuat toggle value state yang mudah, buat variabel berisi ternary 2 value secara toggle lalu setState berdasarkan variabel tersebut

- Manual Acceptance Testing

  - Testing melalui apps di browser

- Testing checkbox

  - Menggunakan useState boolean untuk button, button disabled atau tidak berdasarkan state
  - Peubahnya di onChange setDisabled e.target.checked
  - Default checked mengambil value initial state
  - aria-checked untuk kebutuhan aksesibilitas untuk screen reader
  - Untuk test tinggal expect apakah button ketika checkbox di click, antara toBeDisabled atau toBeEnabled
  - Checkbox tidak punya isi, maka tidak bisa menggunakan name dalam getByRole. Gunakan label maka test berhasil.

- Testing style

  - Gunakan .toHaveStyle('background-color: blue')

- Penggunaan function

  - Import function dari App.js lalu gunakan di test misalnya replaceCamelWithCapital dengan regex dan gunakan juga function itu diimplementasi ke aplikasi

  

- ESLint dan Prettier

  - ESLint -> Linter, Prettier -> Formatting

    - ESLint -> menandai jika ada error, tidak konsisten dari rule, dan memberi rekomendasi kode yang tepat ketika error atau kode belum selesai di tulis lengkap dll
    - Prettier -> otomatis merapikan kode, baik itu space, indentasi

  - Linter bermanfaat untuk best practice koding

  - `npm install eslint-plugin-testing-library eslint-plugin-jest-dom`

  - Hapus eslint config di package.json

    - Buat .eslintrc.json
    - Tambahkan plugin testinglibrary dan jest dom
    - extends react-app, jest dan semua testing library

  - ESLint Untuk di VSCode

    - Buat folder .vscode file settings.json
    - Masukkan kode untuk opsi linter
    - Ketika di VSCode lalu mengetikkan kode yang kurang sesuai rule, maka otomatis eslint akan memberikan suggestion dan tanda garis merah di kode
    - Ketika di save, maka suggestion akan mengkoreksi kode kita secara otomatis
    - Jangan lupa .ignore .vscode dan eslintcache

  - Prettier VSCode

    - Masukkan di .vscode > settings.json
    - Masukkan default formatter masukkan prettier
    - Dan formatOnSave true

    

  - Testing pada Server

    - Menggunakan mock server worker untuk melakukan simulasi response server tanpa menjalankan server (tapi tetap membutuhkan function function di server)
    - Untuk simulasi aplikasi
      - intall eslint-plugin-testing-library eslint-plugin-jest-dom
      - Pasang seperti simulasi berikutnya di vscode

  - Testing menambahkan react bootstrap

    - `npm install react-bootstrap bootstrap`
    - Tambahkan di public/index.html script ke bootstrap
    - Tambahkan css bootstrap ke index.js
    - Ubah body menjadi teal

  - SummaryForm

    - Untuk kasus yang lebih kompleks buatkan step by step testing aplikasi dengan daftar secara kronologis
    - Organisasi di letakkan di setiap komponen dengan .test.js
    - Selalu diingat jika unable to find, maka mungkin element belum dibuat, tidak dirender atau belum selesai render dalam kasus (async)

  - User Event lebih baik dari Fire Event (dalam hal interaksi dengan UI)

    - https://testing-library.com/docs/ecosystem-user-event
    - type untuk mengetik ke input form
    - Coba unhover dan hover
    - Install dulu packagenya

  - Penggunaan Command Get, Query dan Find

    - get => expect element ada di DOM
    - query => expect element tidak ada di DOM
    - find => expect element yang akan muncul di DOM (async) menunggu dulu
      - All jika ingin mencari target di DOM lebih dari 1
      - Menghasilkan hasil array
    - Role (most prefered)
    - AltText (untuk image)
    - Form (PlaceholderText, LabelText, DisplayValue)
    - Misal untuk kasus ini menggunakan => queryAllByText

  - Prioritas testing berdasarkan Query (assistive), Semantic Query (inconsistency), TestID (kurang bagus)  

  - Ke Program SummaryForm

    - Jika ada kasus popover maka perlu gunakan waitFor kasus async (komponent belum ada atau periksa ketika akan tidak ada) - ketika ada DELAY
    - Overlay di bootstrap popover untuk clicknya tidak perlu kalau kita mau hover

  - Error: react state update should be wrapped into act()

    - react update element sebelum test selesai
    - follow saran act()
    - Terdapat perubahan async
    - Tunggu await sampai render, baru kemudian jalankan test (jadi di test harus waiting dulu element)
    - Gunakan await waitForElementToBeRemoved, jangan lupa async function
    - Lanjut

    

  - Mock Service Worker

    - Tujuan
      - Intercept network call
      - Mengembalikan response tertentu
    - UI yang di test tidak mengirimkan request ke server tapi sudah dihalangi oleh mock service worker, lalu mock mengirimkan response tertentu ke handler request UI test
    - Jadi requestnya tidak akan ke server
    - install `npm install msw`
    - Membuat test server
      - Test server harus listen semua server dan mereset test
    - Buat folder mock di src, handler.js
      - import { rest } from 'msw'
      - Misal menggunakan rest.get untuk melakukan mimik seperti request dan ctx mengembalikan response yang diingikan
    - Buat di src/mock/server.js
      - Import handler dan mock/node
      - SetupTest.js tambahkan beforeall untuk server.listen(), dll
    - toEqual bisa untuk array misal range toEqual(['string1', 'string2']) seperti contain / enum
    - Install axios, import ke UI, gunakan useEffect
      - UseEffect dependency terjadi jika di array nya mengandung sesuai yang nilainya berubah, jika kosong maka dia hanya di jalankan 1 kali
    - Ketika misal tidak ada element yang ditampilkan di struktur html mungkin belum ter-render
      - Komponent terupdate setelah test tersebut dijalankan
      - Async harus maka butuh await findBy..sampai element terrender
    - Mock Service Worker
      - membuat handler
      - membuat server
      - update setup untuk listen ke request
      - Reset setiap handler setiap test
    - Role dari komponent (misal di bootstrap bisa kita dapatkan ketika inspect element). Komponen alert di Bootstrap punya role alert
    - it.only() untuk menjalankan 1 test saja, test lain akan di skip
    - it.skip() untuk skip test tersebut, test lain akan jalan
    - Untuk menjalankan 1 file saja, ketika npm test jalan, ketik P, ketikkan nama file
    - Jika menunggu 2 server call, maka await screen.find.. bisa error atau misal cuma 1 yang terrender
      - Karena menunggu selama ada minimal 1 sudah ditemukan, maka langsung mengembalikan, padahal masih ada lagi yang mau terrender
    - Gunakan `await waitFor(async () => {}`, callbacknya gunakan await
    - Ketik C untuk clear dan menjalankan lagi

    

    - React Context
      - createContext -> untuk menghindari prop drilling cukup mengcakup component dalam provider
      - Penggunaan useMemo untuk menghindari pattern useEffect dan useState
      - Kadang menggunakan constant berupa object di file lain untuk diexport menghindari melanggar SOLID
      - Perlu diingat jika komponent tidak diletakkan dalam provider maka tidak dapat memanfaatkan context valuenya (dan menghasilkan error)
      - Gunakan wrapper saat render daripada melulis parent di rendernya (misal jika banyak parent, seperti router, redux provider dan view)
    - Customer Render secara global
      - Ke dokumentasi testing-library > react testing library > setup
      - Kalau menggunakan global, import semua provider lalu semua provider yang dibutuhkan akan menyediakan context, value redux dsb ke komponen yang dirender
      - Export dan import semua ke komponent test
    - Gunakan userEvent daripada fireEvent
    - Error unmounted 
      - Skip auto cleanup lihat di dokumentasi react testing library untuk skipping auto cleanup (tidak rekom)
      - Mock useEffect tidak direkomendasikan
    - Tips
      - Menambahkan await ke akhir untuk menghindari errors
    - Functional Test catch
      - Implementasi call POST via useEffect di orderconfirmation dengan Mock Service Worker 
    - Debugging Tips
      - screen.debug() untuk melihat DOM
      - Kalau getBy membutuhkan proses async gunakan await findBy
      - Baca output error
        - Langsung baca error di assertion
        - Copas error ke stackoverflow
        - Pre writen code
      - Error umum
        - Tidak bisa menemukan role (kadang tidak ada element, atau element dengan role itu)
        - Update not wrapped in act (karena ada update di component ketika tets selesai. Gunakan await findby)
        - Cant perform react state on unmounted component (karena ada update di component ketika tets selesai. Gunakan await findby)
        - Copy dan comment di bagian error
        - Bandingkan dengan code yang benar
    - Jest Mocks as Props
      - Mungkin membutuhkan props ketika rendering di test
      - Misal validator PropTypes
      - Misal user bisa mengetikkan salah input
      - `jest.fn()` untuk menghindari error, tidak menjalankan apapun (sebagai placeholder)
      - jest.fn bisa sebagai value props component ketika render mock di jest
      - Karena yang penting function/method yang di assign, terpanggil oleh test tapi tidak menjalankan apapun
    - Standard Questing to Ask ketika test
      - What to Render? (komponen yang lebih kecil)
      - Pass props
      - Wrap komponent (misal provider)
      - What to test
      - Bagaimana cara test (querynya)
      - Apakah ada proses menunggu sampai tampil atau hilang (async)
      - Berapa komponen yang perlu di test
    - Latihan
      - Confirm loading
      - Tunggu komponen menghilang
      - Berpindah page
      - Validasi input user
    - Pelajari
      - waitForElementToBeRemoved
        - await
        - misalnya modal
      - Tidak harus selalu TDD
    - Penggunakan disabled atau enabled
      - Gunakan toBeDisabled() dan toBeEnabled()
      - userEvent(inputnya, 'valunya string')
    - Invalid Input
      - Ke Dokumentasi react-bootstrap forms validation native
      - Misal di react bootstrap terdapat class invalid pada inputnya
      - Gunakan toHaveClass()
      - Untuk props yang perlu ditulis tapi tidak ingin error gunakan jest.fn()

  

