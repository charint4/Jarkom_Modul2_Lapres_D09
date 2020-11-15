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

5.

6.

7.

8.

9.

10.

11.

12.

13.

14.

15.

16.

17.
