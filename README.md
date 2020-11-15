# Jarkom_Modul2_Lapres_D09

### 05111840000058 Rafif Ridho
### 05111840000128 Muhammad Rivadhli Purnomo

### Soal

Semeru adalah salah satu gunung yang terkenal di Jawa Timur. Bibah adalah salah satu juru kunci
Semeru. Bibah ingin menyebarkan keindahan Semeru pada dunia sehingga dia membeli 3 buah server
yang berada di MALANG, MOJOKERTO dan PROBOLINGGO. Server MALANG akan digunakan
sebagai DNS Server Master, MOJOKERTO akan digunakan sebagai DNS Server Slave dan
PROBOLINGGO akan digunakan sebagai Web Server. Selain 3 server terdapat 2 klien yang digunakan
untuk testing oleh Bibah yaitu GRESIK dan SIDOARJO. Untuk menyambungkan semua jaringan
tersebut Bibah memberi router di SURABAYA.
Kalian diminta untuk membuat sebuah website utama dengan 

(1) alamat http://semeruyyy.pw yang memiliki 

(2) alias http://www.semeruyyy.pw, dan 

(3) subdomain http://penanjakan.semeruyyy.pw yang diatur DNS-nya pada MALANG dan mengarah ke IP Server PROBOLINGGO serta dibuatkan 

(4) reverse domain untuk domain utama. Untuk mengantisipasi server dicuri/rusak, Bibah minta dibuatkan

(5) DNS Server Slave pada MOJOKERTO agar Bibah tidak terganggu menikmati keindahan Semeru pada Website. Selain website utama Bibah juga meminta dibuatkan 

(6) subdomain dengan alamat http://gunung.semeruyyy.pw yang didelegasikan pada server MOJOKERTO dan mengarah ke IP Server PROBOLINGGO. Bibah juga ingin memberi petunjuk mendaki gunung semeru kepada anggota komunitas sehingga dia meminta dibuatkan 

(7) subdomain dengan nama http://naik.gunung.semeruyyy.pw, domain ini diarahkan ke IP Server PROBOLINGGO.
Setelah selesai membuat keseluruhan domain, kamu diminta untuk segera mengatur web server. 

(8) Domain http://semeruyyy.pw memiliki DocumentRoot pada /var/www/semeruyyy.pw. Awalnya web dapat diakses menggunakan alamat http://semeruyyy.pw/index.php/home. Karena dirasa alamat urlnya kurang bagus, maka 

(9) diaktifkan mod rewrite agar urlnya menjadi http://semeruyyy.pw/home.

(10) Web http://penanjakan.semeruyyy.pw akan digunakan untuk menyimpan assets file yang
memiliki DocumentRoot pada /var/www/penanjakan.semeruyyy.pw dan memiliki struktur
folder sebagai berikut:
/var/www/penanjakan.semeruyyy.pw

/public/javascripts
/public/css
/public/images
/errors

(11) Pada folder /public dibolehkan directory listing namun untuk folder yang berada di dalamnya tidak dibolehkan. 

(12) Untuk mengatasi HTTP Error code 404, disediakan file 404.html pada folder /errors untuk mengganti error default 404 dari Apache.

(13) Untuk mengakses file assets javascript awalnya harus menggunakan url http://penanjakan.semeruyyy.pw/public/javascripts. Karena terlalu panjang maka dibuatkan konfigurasi virtual host agar ketika mengakses file assets menjadi http://penanjakan.semeruyyy.pw/js. Untuk web http://gunung.semeruyyy.pw belum dapat dikonfigurasi pada web server karena
menunggu pengerjaan website selesai. 

(14) sedangkan web http://naik.gunung.semeruyyy.pw sudah bisa diakses hanya dengan menggunakan port 8888. DocumentRoot web berada pada /var/www/naik.gunung.semeruyyy.pw. Dikarenakan web http://naik.gunung.semeruyyy.pw bersifat private 

(15) Bibah meminta kamu membuat web http://naik.gunung.semeruyyy.pw agar diberi autentikasi password dengan username “semeru” dan password “kuynaikgunung” supaya
aman dan tidak sembarang orang bisa mengaksesnya. Saat Bibah mengunjungi IP PROBOLINGGO, yang muncul bukan web utama http://semeruyyy.pw melainkan laman default Apache yang bertuliskan “It works!”. 

(16) Karena dirasa kurang profesional, maka setiap Bibah mengunjungi IP PROBOLINGGO akan dialihkan secara otomatis ke http://semeruyyy.pw.

(17) Karena pengunjung pada /var/www/penanjakan.semeruyyy.pw/public/images sangat banyak maka semua request gambar yang memiliki substring “semeru” akan diarahkan menuju semeru.jpg.

### Jawaban

1. Pertama membuat domain dengan mengisikan konfigurasi untuk semerud09.pw di MALANG seperti berikut

![img](/img/1.1.jpg)

- Buat folder jarkom di dalam /etc/bind, lalu copykan file db.local pada path /etc/bind ke dalam folder jarkom
- Kemudian buka file semerud09.pw dan edit seperti gambar berikut

![img](/img/1.2.jpg)

- Setelah di restart bind9 nya dan dicoba hasilnya,

![img](/img/1.3.jpg)

2. Menambahkan Alias

![img](/img/2.1.jpg)

- Kemudian hasilnya coba diping

![img](/img/2.2.jpg)

3. Membuat Subdomain

![img](/img/3.1.jpg)

- Hasil pingnya : 

![img](/img/3.2.jpg)

4. Membuat Reverse Domain

- Tambahkan konfigurasi berikut ke dalam file named.conf.local

![img](/img/4.1.jpg)

- Copykan file db.local pada path /etc/bind ke dalam folder jarkom
- Edit File 79.151.10.in-addr.arpa menjadi seperti gambar di bawah ini

![img](/img/4.2.jpg)

- Setelah itu restart Malang dan jika dicoba pada Gresik hasilnya

![img](/img/4.3.jpg)

### Revisi

5. Membuat DNS Server Slave
- Edit file /etc/bind/named.conf.local dan sesuaikan dengan syntax berikut

![img](/img/5.1.jpg)

- Kemudian buka file /etc/bind/named.conf.local pada MOJOKERTO dan tambahkan syntax berikut:

![img](/img/5.2.jpg)

-  Untuk testing kita matikan malang dengan service bind9 stop, lalu kita test seperti no 4

![img](/img/5.4.jpg)

6. Membuat subdomain di delagasikan ke MOJOKERTO dan mengarah ke PROBOLINGGO
- Ubah pada MALANG dengan menambahkan subdomain baru

![img](/img/6.1.jpg)

- Kemudian edit file /etc/bind/named.conf.options pada MALANG, comment dnssec-validation auto; dan tambahkan baris berikut pada /etc/bind/named.conf.options

![img](/img/6.2.jpg)

- Pada MOJOKERTO edit file /etc/bind/named.conf.options seperti gmbar berikut

![img](/img/6.3.jpg)

- Kemudian buat direktori dengan nama delegasi lalu copy db.local
- Kemudian edit file gunung.semerud09.pw menjadi seperti dibawah ini

![img](/img/6.4.jpg)

- Lalu coba ping di gresik

![img](/img/6.4.jpg)


7. Membuat subdomain naik.gunung.semerud09.pw

- Pada MOJOKERTO ditambahkan konfigurasi sebagai berikut

![img](/img/7.1.jpg)

- Lalu kita coba ping di gresik

![img](/img/7.2.jpg)


8. Mengatur webserver untuk Domain semerUd09.pw

- Menambahkan ServerName dan DocumentRoot

![img](/img/8.1.jpg)

- Lalu untuk melihat hasilnya dapat diakses dengan browser semerud09.pw

![img](/img/8.2.jpg)

9. Menghilangkan index.php

- Aktifkan a2enmod rewrite

![img](/img/9.1.jpg)

- Lalu edit file .htaccess dan isikan seperti berikut

![img](/img/9.2.jpg)

- Lalu untuk melihat hasilnya tinggal di coba untuk semerud09.pw/home

![img](/img/9.3.jpg)


10. Mensetting penanjakan.semerud09.pw

- Ekstrak file ke folder penanjakan.semerud09.pw

![img](/img/10.1.jpg)

- Tambahkan ServerName dan DocumentRoot penanjakan.semerud09.pw  

![img](/img/10.2.jpg)


- Hasilnya jika dibuka 

![img](/img/10.3.jpg)

11. Listing pada /public tanpa public/*

- Tambahkan Option +Indexes untuk directory penanjakan.semerud09.pw/public, dan tambahkan Option -Indexes untuk directory penanjakan.semerud09.pw/public/*

![img](/img/11.1.jpg)

- Hasilnya saat mengakses penanjakan.semerubd09.pw/public/

![img](/img/11.2.jpg)

- Hasilnya saat mengakses penanjakan.semerud09.pw/public/css/

![img](/img/11.3.jpg)

12. Merubah error page dengan 404.html

- Dengan menambahkan ErrorDocument 404 /errors/404.html

![img](/img/12.1.jpg)

- Lalu apache di restart

![img](/img/12.2.jpg)

- Hasilnya saat mengakses link yang tidak ada

![img](/img/12.3.jpg)

13. Mengubah inisial untuk folder javascript

- Dengan menambahkan Alias dengan memberinya alias "/js"

![img](/img/13.1.jpg)

- Lalu restart apache

![img](/img/13.2.jpg)

- Hasilnya saat mengakses penanjakan.semerud09.pw/js

![img](/img/13.3.jpg)

14. Membuat naik.gunung.semerud09.pw di port 8888

- Setting virtual host di port 8888, tambahkan server name dan document root untuk naik.gunung.semerud09.pw

![img](/img/14.1.jpg)

- Lalu pada ports.conf untuk pot 8888

![img](/img/14.2.jpg)

- Restart apache

![img](/img/14.3.jpg)

- Hasilnya jika mengakases naik.gunung.semerud09.pw:8888

![img](/img/14.4.jpg)

15. Memberikan Auth pada naik.gunung.semerud09.pw

- Membuat user "semeru" dan password "kuynaikgunung" dengan perintah dibawah

![img](/img/15.1.jpg)

- Tambahkan Auth untuk directory naik.gunung.semerud09.pw

![img](/img/15.2.jpg)

- Restart apache

![img](/img/15.3.jpg)

- Hasilnya saat mengakses naik.gunung.semerud09.pw:8888

![img](/img/15.4.jpg)

- Setelah memasukkan username dan password yang sesuai

![img](/img/15.5.jpg)

16. Mengarahkan ke ip probolinggo yaitu 10.151.79.84

![img](/img/16.1.jpg)

- Ubah .htaccess  default pada probolinggo untuk meredirect ip probolinggo ke semerud09.pw

![img](/img/16.2.jpg)

- Ganti allowoverride none jadi all untuk direktori /var/www/

![img](/img/16.3.jpg)

- Restart apache

![img](/img/16.4.jpg)

- Hasilnya saat mengakses 10.151.79.84

![img](/img/16.5.jpg)

17. Mengubah semua gambar yang mengandung "semeru" ke semeru.jpg

- Awal

![img](/img/17.1.jpg)

- Ubah file .htaccess seperti berikut

![img](/img/17.2.jpg)

- Tambahkan AllowOverride All untuk directory penanjakan.semerud09.pw

![img](/img/17.3.jpg)

- Semua akses file gambar yang mengandung "semeru" akan diarahkan ke semeru.jpg

![img](/img/17.4.jpg)
