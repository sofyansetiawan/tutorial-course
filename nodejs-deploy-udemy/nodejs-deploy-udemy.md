# Node.js Deployment

- Perbedaan Heroku vs AWS-GCP

  - Heroku sebagai kontraktor jadi ketika aplikasi di deploy, maka otomatis semua yang melaksanakan running apps, maintain adalah heroku. Kita tidak tahu proses disana dan tidak ada custom yang banyak.
  - AWS - GCP sebagai semi kontraktor tapi lebih ke tools dan storage yang harus kita custom dengan rumit supaya kita bisa menjalanlan aplikasi secara lebih terperinci mengenai pembagian, prevent error, maintain, custom yang sangat banyak

- AWS dan GCP

  - Storage - S3 (Static file hasil deployment dan asset)

  - Database - RDS (Postgre, Mysql, MSSQL) dan cloud SQL

  - Computing Cloud  EC2 dan Compute Engine

    - Instance virtual server (yang mengatur dan menjalankan storage dan RDS)
    - Bisa membuat banyak instance dan menghapusnya

  - Cloud Computing

    - Membuat kita bisa mengakses resource yang ondemand (sesuai permintaan) yang kita tidak harus memiliki fisik tapi dipegang pihak ketiga

  - Cloud Service 3 tipe

    - Infrastructure as a service (IaaS): Fundamental resource seperti computing, storage, networking. Jadi seperti menggunakan EC2 sebagai compute engine
    - Platform as a service (PaaS): Menyediakan platform untuk mendeploy. Seperti apache beanstalk, atau heroku atau app engine kalau di GCP
    - Software as a Service (SaaS): Mengkombinasikan infra dan software di cloud. Jadi contohnya software bisa dijalankan di browser langsung dipakai dan bekerja disana. Contohnya google app, office 365

    

- Heroku

  - Tanpa memikirkan infrastruktur, karena Plarform as a Service (tanpa memikirkan secara requrement teknis low level proteksi database, performance, dll..) jadi lumayan cepat tidak perlu sulit manage
  - Menggunakan version control command
  - Proses (dyno) terisolasi

- Environment Setup Heroku

  - Buat akun heroku
  - Dashboard berisi virtual yang menjalankan sistem dan databasenya (berisi informasi bagaimana aplikasi dijalankan dengan command, log, dsb)
  - Download heroku CLI

- Deploy Heroku

  - heroku login (login ke browser) atau heroku login -i (login dari cli)
  - git add dan commit perubahan
  - heroku create namaaplikasi (pakai lowercase)
    - Akan muncul URL dari tempat aplikasi
  - git push heroku master
  - Jika ada error lihat logsnya (Coba cek port dinamisnya)

  

- AWS

  - EC2 Elastic Computing Cloud : menyewa 1 tempat untuk compute di run di infra AWS. Instance (virtual machine) dijalankan di EC2. Seperti server beneran
  - Configurasi virtual machine lumayan mudah
  - Instance bisa scalable
  - Bayar apa yang kita pakai

- Environment AWS

  - Membuat akun AWS (aws.amazon.com)
  - Free tier selama 12 bulan
  - Isi payment information dengan mengisi kartu credit (EC2 biasanya $5/month)
  - Akan diberikan kode dari operator AWS (sudah terregistrasi)
  - Masuk ke AWS Management Console
    - Berisi semua service yang disediakan AWS
  - Klik EC2 (berisi semua instance) -> Launch Instance
    - Pilih amazon machine image (OS) -> Pilih Amazon Linux 2 AMI
    - Instance type -> Standart saja (free tier)
    - Langsung ke Review and Launch
    - Mendapatkan private key pair agar bisa konek ke instance melalui SSL
    - Download key
    - Launch Instance -> View Instance (state pending sampai hijau running)
    - Ada public IP bisa akses dan bisa di redirect ke domain
  - Koneksi via SSL
    - Pilih connect (kalau mac tidak perlu putty)
    - Cari lokasi file private key lalu ganti permission
    - Copy kode ssh ke terminal lalu jalankan
    - Langsung masuk ke virtual machine
      - Karena berbasis linux untuk instalasi gunakan `apt-get`
  - Deploy ke AWS