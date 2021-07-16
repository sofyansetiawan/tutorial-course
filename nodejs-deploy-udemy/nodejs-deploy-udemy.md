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

    - Port standart http itu 80

    - Terminal yang terkoneksi dengan EC2

    - Install node.js dan nvm di EC2 `curl -o- https://raw.githubusercontent.com/creationix/v0.33.2/install.sh | bash`

      - Ada warning untuk keluar terminal (refresh)
      - Masuk lagi ke terminal jalankan lagi untuk masuk ke ec2 VM aws
      - `nvm --version` (gunakan nvm untuk management environment nodejs, jadi kita bisa menginstal beberapa versi node)
      - `nvm install node` atau kita bisa install versinya

    - Install Git `sudo yum install git`

      - Clone repository github ke es2, masuk ke project

    - Jalankan project `npm start` di 8080

    - Buka dashboard AWS lalu buka di browser public DNS ditambah 8080

      - Jika ada error, karena port 8080 belum dibuat

    - Cari di bagian Network & Security > Security Group

      - Cari group yang bukan default, Pilih, Action > Edit
      - Cari di bawah inbound
      - Tambahkan rule > Type Custom TCP masukkan port range 8080 > Save

    - Kita ingin aplikasi terus berjalan, walaupun koneksi sshnya di matikan di terminal

      - Membutuhkan PM2 agar aplikasi kita tetap berjalan
      - Killall dulu semua proses node yang berjalan di EC2 `killall -9 node`
      - Install PM2 `npm install -g pm2`
      - Masuk ke folder project
      - `pm2 start server.js` (Menjalankan melalui server.js - terdata)
      - `pm2 startup` (menjalankan pm2 yang dijalankan walaupun servernya terrestart / dihidupkan lagi)
      - `pm2 save` (save current process)

    - Pindah port dari 8080 ke 80 (default) agar tidak perlu akses URL portnya

    - Install nginx `sudo yum install nginx`

      - Install nginx `sudo amazon-linux-extra install nginx1.12`

    - Cek nginx `nginx -v`

    - Ke Security Group > Pilih grup lali tambahkan rule HTTP 80

      - Akan diarahkan ke default nginx default page
      - Jadi arahkan ke port 80 nya nginx
      - Ketika user masuk ke 80 maka akan diintercept nginx ke 8080 atau port yang sudah ditentukan

    - Ubah file configurasi nginx

      - `sudo nano /etc/nginx/nginx/conf`

      - Cari server lalu location tambahkan 

      - ```
        proxy_pass http//:127.0.0.1:8080;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_update;
        ```

      - Intercept semua trafik 8080 ke 127.0.0.1, server listening jika headernya match

      - CTRL + x untuk exit

    - Restart dulu `sudo service nginx restart`

    - `systemctl status nginx.service` (melihat sistem status)

    - Sudah bisa berfungsi (cek di URL)

  - Agar sistem yang sudah menggunakan nginx bisa berjalan ketika restart, jalankan `sudo chkconfig nginx on`

  - exit -> Aplikasi sudah berjalan walaupun sudah di close terminalnya

  

- Google Cloud Platform

  - Google Compute Engine (seperti EC2) -> IaaS satu virtual machine yang di host google
  - Kelebihan Compute Engine: Booting cepat, persistent, performance konsistem dan cepat, virtual service sangat fleksible dan integrated dan VM yang custom, harga fleksibel

- Environment Google Cloud Platform

  - Pasti akun google
  - console.cloud.google.com
  - Button di atas > New Project, nama "kodedeploy"
  - Menu > Compute Engine > VM Instance
    - Nama Kode deploy, Region defaut, Pilih CPU (kalau apps simple pilih micro)
    - Ada estimasi jika bayar $4.8/month
    - Boot image bisa pilih ubuntu (piluh LTS)
    - Check semua opsi firewall > Create
  - Instance sedang dibuat dan bisa dipilah progressnya
  - Masuk ke SSH bisa pilih di table > connect
    - Terminalnya ada di browser jadi tidak perlu pakai terminal laptop
  - Sudah masuk ke instance melalui terminal
    - Bisa jalankan command dasar ubuntu misal `sudo apt-get update`

- Deploy ke GCP
  - Ke terminal connect gcp

    - Install node.js dan npm `sudo apt-get install -y nodejs npm`
    - Clone repo ke GCP `git clone ...` > pindah ke project
    - Jalankan `npm start`

  - Masuk ke dashboard VM Instance > Buka external IP 8080 (maka error, karena belum buka port)

  - Pilih Menu > VPC Network > Firewall rule

    - List firewall rule > Pilih default
    - Tambahkan rule firewall di bagian tcp 8080 (pisahkan comma)
    - Masih error kalau masih pakai https kalau http bisa

  - Kembali ke terminal

    - Install nginx `sudo apt-get install nginx`
    - Test nginx sudah bisa `curl localhost` > html nginx
    - Setup nginx `cd /etc/nginx/sites-available/`
    - Backup dulu file default configurasi nginx `sudo mv default default.bak`
    - Buat 1 file default baru `sudo touch default` , `sudo nano default`

  -  Configurasi nya di default

  - ```
    server {
    	listen 80;
    	server_name 34.73.107.225;
    	location / {
    		proxy_pass http//:127.0.0.1:8080;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
    		proxy_set_header Host $host;
    		proxy_cache_bypass $http_update;
    	}
    }
    ```

    - Exit > jalankan sudo service nginx restart

  - Jalankan lagi, `npm start`, maka sudah tidak pakai port 8080 lagi

  - Install pm2 `sudo npm install -g pm2`

    - `touch pm2config.json` di project
    - Buka lalu tambahkan script

  - ```
    {
    	"app": [
    		{
    			"script": "./server.js",
    			"env": {
    				"NODE_ENV": "production",
    				"PORT": "8080"
    			}
    		}
    	]
    }
    ```

  - Jalankan `pm2 start pm2config.json` (Menjalankan melalui server.js - terdata)

  - `pm2 startup` (menjalankan pm2 yang dijalankan walaupun servernya terrestart / dihidupkan lagi)