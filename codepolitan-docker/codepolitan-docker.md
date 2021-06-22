# Codepolitan Docker

## Pengenalan Docker

- Deploy apps biasanya bikin distributed apps (java jadi jar file, golang jadi binary file)
  - Aplikasi yang sudah dibuat di deploy ke server production
  - Sebelum deploy server diinstall OS, runtime, library, web server dan database
  
  
  
- Deploy dengan docker
  - Docker akan membundle semua aplikasi, web server, database, library, runtime dalam 1 package
  - Cukup 1 package itu di deploy ke server
  - Sehingga di server tidak perlu install database, web server, dsb (tidak ada waste)
  - Di server cukup operating systemnya
  - Kita bisa menjalankan lebih dari 1 package docker di server
  - Cukup deploy package dockernya
  
  
  
- Docker vs Virtual Machine
  - Docker tidak menerapkan virtual machine
  - Docker menggunakan container
  - Container vs Virtual Machine
  - Di Virtual Machine ada manager/hypervisor (cont. VMWare, VirtualBox)
  - Di virtual machine install OS, app dependency dan aplikasi
  - Container tidak ada operating system
  - Container akan menggunakan operating system dimana container dijalankan
  - Container akan meng isolate aplikasi dan dependency tanpa mempengaruhi ke operating systemnya
  - Maka container akan punya space lebih kecil dibanding VM karena minus operating system
  
  
  
- Install Docker
  - Docker CE (community edition) gratis kalau EE (Enterprice Edition) bayar
  - Daftar ke docker hub lalu login
  - Download docker CE di mac lalu install
  - Login melalui aplikasi docker dengan akun docker hub
  - Maka akan keluar di menu bar aplikasi docker sudah running
  - Untuk cek apa docker sudah running ketik di terminal -> `docker info` (informasi docker, running linux)
  - Docker sebenarnya basenya linux
  - `docker version` untuk versi dockernya
  
  
  
- Docker Architecture
  - Docker terdiri dari aplikasi docker client dan docker server (docker host/ docker daemon)
  - Docker client di local, docker server di server production kita (saat development docker server masih di laptop atau komputer kita)
  - Docker client di terminal terdiri dari perintah perintah docker (perintah client akan mengatur di docker server)
  - Docker server untuk manage container, manage image docker yang terkoneksi ke registry container
  
  
  
- Docker QnA
  - Yang di up ke server adalah image yang diupload ke container registry
  - Container mungkin iya atau tidak menggantikan VM, karena lebih efisien tinggal memanfaatkan OS di server tapi kalau multi OS pakai VM
  - Container memang yang paling cocok base OS Linux
  - Docker di OS windows tetap running base OS Linux
  - Cek memory docker di activity monitor
  
  
  
- Container Registry
  - Tempat digunakan menyimpan image docker (aplikasi yang dibundle jadi image)
  - Alasan menggunakan container registry. Karena kalau ingin menjalankan lebih dari 1 image (ketika dipasang ke 10 server akan ribet)
  - Docker server akan memanggil image di docker registry
  - Container registry ada banyak: Docker Hub, Google Container registry, AWS Elastic Container Registry (cek web masing masing)
  
  
  
- Image
  - Hasil distribution file bundle aplikasi kita
  - Image bukan aplikasi installer, image adalah aplikasi yang bisa langsung dirunning. Bukan ISO image.
  - Docker hub berisi image image opensource product untuk beberapa sistem seperti web server, mongodb, oracle, mysql, redis, dll.
  - Jadi tidak perlu membuat image
  - Terdapat tagging untuk melihat supportnya
  
  
  
- Container
  - Container adalah image yang kita running
  - Ketika image sudah kita running maka akan jadi container
  - Container adalah hasil instantiate dari Image
  - Kita bisa merunning beberapa image
  - Container bisa jalan, mati, diam
  - Container sudah dihapus, imagenya masih ada
  
  
  
- Mengambil Image dari Registry
  - `docker images` terdapat info image apa saja yang sudah dibuat di local
  - Contoh ambil image dari docker hub, cari mongodb, download lalu running dilocal sebagai container
  - Download dengan `docker pull mongo` nanti akan download latest version
  - Kalau ingin download tag/versi lain `docker pull mongo:4.1.2`
  
  
  
- Membuat Container
  - Untuk melihat container (image yang running) gunakan `docker container ls`
  - Defaultnya ketika kita setup docker belum ada image yang sudah jalan/container
  - Untuk melihat semua container (baik running, hold atau stop) `docker container ls --all`
  - Untuk membuat container dari image sudah sudah ada `docker container create mongo:4.1` (secara default akan membuat random name untuk container)
  - Kalau ingin container tidak random name (sesuai keinginan kita) `docker container create --name namacontainer mongo:4.1`
  - Akan keluar id dari container misal `28d414104dd288bbd55ecd15478e9b30df70f7da634f7047c479b80b1c3b72cc`
  - Untuk menjalankan container bisa gunakan id atau namacontainer
  - `docker container ls` belum ada container yang running
  - Kita bisa buat lebih dari 1 container dari image yang sama, tidak boleh pakai namacontainer sama
  
  
  
- Menjalankan container
  - Menjalankan container `docker container start mongoserver`
  - Cek lagi dengan `docker container ls`
  - Portnya ada di `27017`/tcp
  - Bisa gunakan GUI Mongo untuk test misal robomongo Robo3T
  - Buka Robo3T lalu masukkan koneksi localhost dengan port 27017, maka error
  - Karena kita mengakses diluar container, jadi ada 1 tahap yang belum export portnya supaya bisa diakses dari luar container (kalau program di dalam container bisa)
  
  
  
- Menghapus Container
  - `docker container rm mongoserver1`
  - Tapi jika yang diremove container yang masih running maka tidak bisa, pastikan container mati dulu/stop
  - Stop container `docker container stop mongoserver1 mongoserver2`
  - Jalankan lagi `docker container rm mongoserver1 mongoserver2`
  - Image tetap ada `docker images` -> container adalah instance dari image
  
  
  
- Membuka port container
  - Buat dulu container dari image dengan port yang diakses dari luar dan port dari container `docker container create --name mongoserver1 -p 8080:27017 mongo4.1`
  - 8080 adalah port yang bisa diakses dari luar container, 27017 adalah port container berjalan (program dalam container bisa akses port itu). Jangan lupa nama image dan tagsnya setelahnya
  - Buat juga untuk container mongoserver2 `docker container create --name mongoserver2 -p 8181:27017 mongo4.1`
  - Pastikan port akses luar antar container berbeda kecuali port sumber. (agak bingung)
  - `docker container ls --all` lalu jalankan `docker container start mongoserver1 mongoserver2`
  - Port yang diakses dari luar itu maksudnya akan di forward ke port container sumber
  - Buat koneksi di robo3t localhost 8080 mongoserver1, 8181 mongoserver2
  - Coba create database
  - Lalu untuk memastikan, matikan mongoserver1, disconect dari robo3t lalu buat connection baru maka akan gagal
  
  
  
- Hapus Image
  - `docker image rm mongo:4.1`
  - Saat dihapus, error karena ada container yang pakai image ini. Tidak bisa delete image kalau sedang ada container yang pakai (reference)
  - Bukan berarti ketika sudah membuat container, image akan berubah jadi container. Image bukan installer tapi seperti class dan container sebagai instance nya.
  - Stop dulu `docker container stop mongoserver1 mongoserver2` lalu remove `docker container rm mongoserver1 mongoserver2`
  
  
  
- Membuat image docker sendiri dengan dockerfile
  - Clone contoh repo belajar docker di programmer zaman now
  - Jalankan `go run main.go` buka di localhost:8080
  - Buat file Dockerfile
  - Kita bisa menggunakan image yang sudah ada ke image yang akan dibuat
  - Daripada buat dari 0 untuk image golang ambil dari registry (docker hub), cari golang 1.11.4
  - Untuk menggunakan image dari registry di Dockerfile, tulis `FROM golang:1.11.4` (kalau sebelumnya sudah kita pull, berarti dari local)
  - Buat image dari golang, mengkopi semua file app ke dalam image
  - `COPY main.go /app/main.go` copy sumber ke tujuan directory aplikasi
  - Kemudian cara runningnya,`go run /app/main.go`, tapi kita harus memberitahu docker kalau ini dijalankan di commandline
  - `CMD ["go", "run", ""/app/main.go"]` perintahnya perlu dipisah dalam comma seperti array seperti process.argv
  - Built image dengan `docker build --tag app-golang:1.0 .` (berisi nama image dan tag/version)
  - Jalankan lagi `docker images` cek apakah image sudah ada
  - Kalau ada image golang lain bisa dihapus karena sudah jadi 1 dengan app-golang
  - Buat container `docker container create --name app1 -p 8080:8080 app-golang:1.0`
  - Jalankan `docker container start app1`
  - Cek `docker container ls` (otomatis menjalankan perintah golang) dan cek di browser 8080
  
  
  
- Upload image ke repository
  - Ke docker hub, create a repository, isi nama, pilih public (misalnya)
  - Untuk push ke repository -> docker push sofyansetiawan/app-golang:1.0
  - Tapi ada permasalahan tidak ada tag nya itu di local. Kita harus samakan image local dan nama repo.
  - ke Tags lalu tambahkan `docker tag app-golang:1.0 sofyansetiawan/app-golang`
  - Push ke repo `docker push sofyansetiawan/app-golang:1.0`
  - Kalau baru pertama gunakan docker di CLI perlu login dulu `docker login`
  - Ketika push image golang yang dipakai app-golang tidak terpush ke repo docker karena reference ke image disana. Makanya ukuran images yang diupload lebih kecil, berbeda dnegan images yang ada di local
  - Kalau dari server development / production, butuh image docker cukup docker pull imagenya
  
  
  
- Environment Variable di Docker
  - Environment variabel penting karena untuk membedakan konfigurasi antara production, testing dan development
  - Pastikan aplikasi sudah memanggil environment variable. 
  - Saat membuat image belum di atur env, karena mengatur env nanti di docker hub
  - Buat docker images
  - Membuat docker container dari image yang dibuat
  - Untuk melihat `docker container logs namacontainer`
  - Untuk menambahkan env di perintah container `docker container create --name namacontainer -p 8080:8080 -e NAMAVAR=Value namaimages:tags`
  - Untuk memastikan env variabel sudah ada di container `docker container inspect namacontainer`
  - Jalankan lagi containernya
  - Jika lebih dari 1 env variabel `... -e NAMAVAR=Value -e NAMAVAR=Value -e NAMAVAR=Value ...`
  
  
  
- Intergrasi container dnegan network
  - Siapkan 2 aplikasi yang membutuhkan 2 koneksi database redis dan mongo
  - Containernya ada 3: container aplikasi, redis dan mongo
  - Build aplikasinya misal java
  - Build image java-docker:1.0
  - Pull image redis:5 dan mongo:4-xenial pakai `docker pull`
  - Buat container redis dan mongo
  - Buat container java-docker dan isi env variabel yang dibutuhkan port, host untuk akses redis dan mongo
  - Start container mongo redis dan java-docker
  - Lihat logs status containernya
  - Ketika dijalankan akan error, karena kalau set env ke localhost maka akan mengakses localhost container java-docker itu sendiri bukan ke container luar mongo atau redis
  - Stop dan remove container java-docker
  - Ketika membuat container lagi java-docker dan mengganti env dari localhost ke mongo, maka akan error karena tidak mengenal host url bernama mongo
  - Maka harus dihubungkan dengan network antar container
  - Ingat container punya localhost sendiri2
  - Buat network 
  - ![Screen Shot 2021-06-22 at 03.47.04](/Users/sofyansetiawan/Tutorial/Bootcamp/tutorial-main/codepolitan-docker/image.png)
  - Kalau ingin memeriksa container masuk ke network mana lihat di `docker container inspect mongo `
  - Restart container untuk java-docker
  
  
  
- Docker Compose

  - Mempermudah kita membuat dan manage container dengan kasus misal harus membuat banyak container

  - Jadi bisa membuat automasi membuat container, network, menentukan env

  - Jadi buat 1 file lalu dipanggil daripada manual satu persatu

  - https://docs.docker.com/compose/

  - File yang akan terbuat adalah yml (lebih simple daripada json)

  - Cari version terbaru dari container di docs docker

  - Container dimasukkan dalam attribute services

  - Berisi properti nama servicenya isinya container_name, image, ports

  - Docker compose butuh container lain untuk bisa jalan, jadi container yang mengenerate container lain dengan attributes depends_on redis mongo. Jadi sebelum membuat container java-docker, pastikan redis dan mongo sudah terbuat dan running

  - Attribute untuk environment variabel bisa dipasang disana

  - Bisa juga networks diberi nama lalu setiap attribute container tadi 

  - ![Screen Shot 2021-06-22 at 20.53.00](/Users/sofyansetiawan/Tutorial/Bootcamp/tutorial-main/codepolitan-docker/image3.png)

    ![Screen Shot 2021-06-22 at 20.53.20](/Users/sofyansetiawan/Tutorial/Bootcamp/tutorial-main/codepolitan-docker/image2.png)

  - Menjalankan running `docker-compose.yml`  ketikkan `docker-compose up -d ` (up: create dan start container, down: menghapus dan membuat lagi dan start - ini hati2)

  - Pakai -d untuk daemon (jadi lognya gak tampil), tapi kalau ingin melihat progress pakai `docker container logs java-docker`



- Manage data di Docker
  - Aplikasi yang bagus itu stateless (tidak menyimpan data)
  - Tapi kadang ada aplikasi yang statefull (misal database)
  - Kita tidak menyimpan data di dalam container (karena kalau container didelete datanya juga ke delete)
  - Docker storage ada volumens (seperti harddisk baru)
  - Cek di dockerhub mongodb di dokumentasi bawah ada cara menyimpan data di `/data/db`
  - Untuk manage volume -> `docker volume`
  - Membuat volume -> `docker volume create mongo_data`
  - Jadi ketika create container mongo `docker container create --name mongo -p 27017:27017 -v mongo_data:/data/db mongo:4-xenial` (pakai -v, mongo_data adalah docker volume, dan tentukan path data disimpan)
  - Walaupun container dihapus, selama membuat container merujuk ke path volume tsb maka data bisa diakses
  - Untuk mencoba data di local (karena volume tidak bisa melihat data) bisa pakai bind-mount
  - Caranya sediakan folder untuk tempat mount data, jadi nama volume diganti pathnya `docker container create --name mongo -p 27017:27017 -v /usr/sofyan/Desktop/mongo_data:/data/db mongo:4-xenial`
  - Untuk docker volume itu manage, migrate lebih mudah. Tapi kalau bind-mount itu kita harus manage sendiri dan rumit



- Masuk ke Docker Container

  - Kalau butuh install db yang harus di dalam container (misal mongo tidak bisa diinstall di windows, otomatis harus di container)
  - Perintah -> `docker exec -t -i redis /bin/bash`
    - -t adalah tty, -i interaktif (bisa memasukkan perintah/path setelahnya)
    - Masuk ke folder /bin/bash
  - Kita akan masuk ke terminal container di folder tujuan. Misal jika sudah ada redis didalamnya kita bisa ketikkan perintah redis-cli untuk akses data redis dalam containernya
  - Untuk keluar dari terminal container (keluar container) ketika `exit`

  

- Membersihkan Sampah

  - Kalau kita ingin menghapus sisa sisa container, image dan sebagainya
  - `docker image prune` menghapus image yang tidak terpakai (kecuali ada container yang pakai image itu)
  - `docker volume prune`
  - `docker container prune` (untuk container yang sudah stop)
  - `docker network prune`
  - `docker system prune` (untuk semua yang tidak dipakai volumen, prune, network)
  - `docker system ds` -> jumlah container, image, tanpa hapus volumen dll
  - `docker system prune -a --volume` -> semua termasuk volume
  - Misal ketika kita sudah selesai up docker image ke repository kita bisa bersihkan