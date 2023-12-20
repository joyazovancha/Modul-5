# Modul 5
## Penjelasan
### Topologi 
![gambar](https://github.com/joyazovancha/Modul-5/assets/145383781/99f74b64-5ecc-4a99-894f-d176ffc7c41c)

### Perhitungan IP VLSM
  Dibawah ini merupakan penjumlahan dari setiap subnetmask dan total ipnya

  
  ![AWAL](https://github.com/joyazovancha/Modul-5/assets/145383781/137fe36a-66eb-41c5-920b-500ed3d6ec6d)


  
  Lalu lanjut untuk pembuatan tree VLSM

  
  ![TREE VLSM](https://github.com/joyazovancha/Modul-5/assets/145383781/c32bef29-6f6c-4f4e-a64a-9f12ea6e6e17)


  Setelah itu untuk pembagian rute tiap subnet
  
  ![TABLE](https://github.com/joyazovancha/Modul-5/assets/145383781/02c5c119-1889-432f-ba66-c5b1e6fe516d)

  ### DHCP Server
  Tugas berikutnya adalah memberikan ip pada subnet SchwerMountain, LaubHills, TurkRegion, dan GrobeForest menggunakan bantuan DHCP.
  Disini saya membuat script bernama init.sh yang berisi konfigurasi DHCP seperti ini :
  ```
  subnet 'NID' netmask 'Netmask' {
    range 'IP_Awal' 'IP_Akhir';
    option routers 'iP_Gateway';
    option broadcast-address 'IP_Broadcast';
    option domain-name-servers 'DNS_yang_diinginkan';
    default-lease-time 'Waktu';
    max-lease-time 'Waktu';
  }
```
  Lalu laukan script diatas dilakukan untuk keempat subnet seperti contoh dibawah ini : 
  
  ![Screenshot (1492)](https://github.com/joyazovancha/Modul-5/assets/145383781/2d7df98f-9e12-4160-9c1d-bc757808cded)

  ### Soal 1
  Setelah mengonfigurasi dhcp lanjut ke soal 1 yaitu membuat topologi kita dapat mengakses ke luar. Disini saya menggunakan script bernama nomor1.sh :

  ![Screenshot (1493)](https://github.com/joyazovancha/Modul-5/assets/145383781/fb91e6c1-b6bd-4cdb-ba99-21fed535e279)

  Setelah kita run script diatas lalu kita coba ping google.com

  ![Screenshot (1494)](https://github.com/joyazovancha/Modul-5/assets/145383781/b2f65dc6-f701-477b-9fb1-f4deddd5833f)

  Dapat dilihat bahwa topologi saya berhasil connect ke internet.
  
  ### Soal 2
  Di soal 2 ini saya diminta untuk mendrop semua paket yang berasal dari port TCP dan UDP kecuali port 8080 dari TCP.
  Disini saya membuat script bernama nomor1.sh yang saya run di Grobeforest :

  ![Screenshot (1495)](https://github.com/joyazovancha/Modul-5/assets/145383781/8e918173-c88c-46fd-bc28-3a204321367b)

  Setelah itu kita run saja script tersebut dan hasilnya dapat dilihat dibawah ini menggunakan 
  ```
  iptables -L
  ```
  
![Screenshot (1496)](https://github.com/joyazovancha/Modul-5/assets/145383781/cc80fdb8-ae99-4371-b8c0-fb233ca6238e)

Setelah itu saya coba akses grobeforest dari luar menggunakan port 8080 menggunakan : 
```
nc -l -p 8080
```
Setelah itu saya akan coba mengaksesnya menggunakan Heiter dengan command dibawah ini 
```
nc 192.221.4.6 8080
```

Berikut dibawah ini hasilnya 
Dari Heiter

![Screenshot (1497)](https://github.com/joyazovancha/Modul-5/assets/145383781/0c2399c9-7c72-46fc-b3d2-8bcf6dffc8e6)


Di Grobeforest

![Screenshot (1498)](https://github.com/joyazovancha/Modul-5/assets/145383781/243ec891-58a0-470a-b0ec-b2579203a4dd)

### Soal 3
Disini saya diminta untuk membatasi DHCP dan DNS server hanya dapat dilakukan 3 ping secara bersamaan. 
Dibawah ini saya membuat script di revolte yang berisi sebagai berikut


![Screenshot (1499)](https://github.com/joyazovancha/Modul-5/assets/145383781/0a3bcf2c-be16-4132-b767-c90caae2591d)

```
--conlimit-above 3
```
Teks diatas berfungsi untuk membatasi koneksi maksimal 3 saja. Setelah itu run scriptnya.

![Screenshot (1500)](https://github.com/joyazovancha/Modul-5/assets/145383781/215cf406-be67-41ad-b269-e38722ef6d71)

Dapat dilihat dari screenshot diatas bahwa script yang saya jalankan berhasil. Lalu saya cek melalui ping dengan 4 device.


![Screenshot (1502)](https://github.com/joyazovancha/Modul-5/assets/145383781/88e82d7f-f735-4dcb-a226-eab22d4c777d)

Dapat dilihat ketika saya mencoba ping yang ke empat yaitu di Heiter, heiter tidak dapat memping Revolte.

### Soal 4
Pada soal 4 kali ini saya diminta untuk membatasi koneksi SSH pada Webserver hanya pada warga Grobeforest.
Disini saya membuat script bernama nomor4.sh yang bertujuan untuk warga Grobeforest saja 


![Screenshot (1503)](https://github.com/joyazovancha/Modul-5/assets/145383781/44f899bc-8e72-43c3-8677-4df16d005979)

Setelah itu saya run scriptnya lalu saya buka port 22 di Sein menggunakan 
```
nc -l -p 22
```
Setelah itu saya masuk melalui Grobeforest menggunakan ip dari sein
```
nmap 192.221.4.2
```

Dapat dilihat hasil dibawah ini bahwa hasilnya open

![Screenshot (1504)](https://github.com/joyazovancha/Modul-5/assets/145383781/e46be148-3b38-4e66-b05a-0d218e82fcdc)

Kita juga bisa memastikan dengan menggunakan pada sein untuk melihat policynya
```
iptables -L
```
![Screenshot (1506)](https://github.com/joyazovancha/Modul-5/assets/145383781/9edd3564-c876-4cc0-bd02-d6e5fe772e00)

Kita juga bisa mencoba menyambungkan ke sein menggunakan Turk Region untuk memvalidasi apakah policy yang kita tulis berfungsi 

![Screenshot (1505)](https://github.com/joyazovancha/Modul-5/assets/145383781/dc67bf73-df8b-4fb0-8db2-289080463a24)

Dapat dilihat pada gambar diatas bahwa Turkregion "filtered" dan tidak ada open.

### Soal 5 dan 6
Disini saya diminta untuk memberikan akses menuju web server hanya pada jam 08.00-16.00, ditambah pada jam 12.00 - 13.00 dilarang, dan pada hari jumat untuk 12.00 13.00 dilarang juga.
Saya membuat script bernama nomor56.sh yang berisi dibawah ini : 

![Screenshot (1508)](https://github.com/joyazovancha/Modul-5/assets/145383781/a7e6e31c-193e-47de-8edd-563440b96289)

Di script diatas saya juga menambahkan kondisi dimana jika 3 kondisi tersebut tidak dipenuhi dan akan di drop
```
iptables -A INPUT -p tcp --dport 22 -j DROP
```
Setelah itu kita run scriptnya dan cek hasilnya menggunakan 
```
iptables -L
```

![Screenshot (1509)](https://github.com/joyazovancha/Modul-5/assets/145383781/a007631e-7918-49fc-bc42-7b6ed3845d83)


Dapat diliha dari gambar diatas bahwa script berfungsi dengan baik
Setelah itu saya coba open port di Sein dengan 
```
nc -l -p 22
```
Dan saya coba akses di jam di topologinya yaiut jam 00:45:38 menggunakan 
```
nmap 192.221.4.2 22
```

![Screenshot (1510)](https://github.com/joyazovancha/Modul-5/assets/145383781/32734a31-fcb4-4acc-aa42-5ff780471fbc)

Dapat dilihat pada hasil diatas bahwa Grobeforest tidak dapat mengakses Sein pada jam 00:45:38

Setelah itu kita coba untuk jam yang open, disini saya mencoba jam 09.00 pada hari Rabu menggunakan : 
```
date -u 1220090023
```

Setelah berhasil kita coba mengakses Sein 

![Screenshot (1511)](https://github.com/joyazovancha/Modul-5/assets/145383781/646f1653-c5da-4467-85a4-1255a816ffe8)

Dapat dilihat pada gambar diatas bahwa open.

  
  
  
