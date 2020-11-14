## Praktikum Modul 1
Kelompok D13
- 05111840000094 Rafi Nizar Abiyyi
- 05111740000192 Faishal Abiyyudzakir

<br>

### Soal 1
> membuat website utama dengan alamat **http://semerud13.pw**


![soal1-1](/imgs/no1-1.PNG)

buat zone semerud13.pw di uml malang
memiliki file bind pada /etc/bind/jarkom/semerud13.pw

![soal1-2](/imgs/no1-2.PNG)

isi file bind 

### Soal 2
> yang memiliki alias **http://www.semerud13.pw**

![soal2-1](/imgs/no2-1.PNG)

tambah record www CNAME mengarah ke semerud13.pw di bind semerud13.pw

### Soal 3
> memiliki subdomain **http:///penanjakan.semerud13.pw** yang diatur DNS-nya di pada **MALANG** dan mengarah ke IP server **PROBOLINGGO**

![soal3-1](/imgs/no3-1.PNG)

tambah record penanjakan A mengarah ke ip probolinggo di bind semerud13.pw

### Soal 4
> reverse domain untuk domain utama

![soal4-1](/imgs/no4-1.PNG)

tambah zone 79.151.10-in-addr.arpa di uml malang
memiliki file bind pada /etc/bind/jarkom/79.151.10-in-addr.arpa

![soal4-2](/imgs/no4-2.PNG)

isi file bind
tambah record byte terakhir milik ip probolinggo PTR ke semerud13.pw.

### Soal 5
> membuat DNS server Slave pada **MOJOKERTO**

![soal5-1](/imgs/no5-1.PNG)

edit named.conf.local di malang
edit zone tambah allowtransfer ke moker, also notify

![soal5-2](/imgs/no5-2.PNG)

edit named.conf.local di mojokerto
tambah zone, pake type slave, tambah masters

![soal5-3](/imgs/no5-3.PNG)

stop service bind9 di malang

![soal5-4](/imgs/no5-4.PNG)

(name server ngarah ke malang sama mojokerto)
coba ping di klien gresik

### Soal 6
> membuat subdomain dengan alamat http://gunung.semerud13.pw yang didelegasikan pada server **MOJOKERTO** dan mengarah ke IP server **PROBOLINGGO**

![soal6-1](/imgs/no6-1.PNG)

tambah record A ns ke ip moker, dan record gunung NS ke ns

![soal6-2](/imgs/no6-2.PNG)

edit named.conf.options
komen dnssec-validation auto;
tambah allow-query{any;};

![soal6-3](/imgs/no6-3.PNG)

tambah zone gunung.semerud13.pw di mojokerto

buat folder delegasi di /etc/bind

![soal6-4](/imgs/no6-4.PNG)

buat file gunung.semerud13.pw di /etc/bind/delegasi
buat record @ A mengarah ke probolinggo

### Soal 7
> subdomain dengan nama **http://naik.gunung.semerud13.pw** diarahkan ke IP server **PROBOLINGGO**

![soal7-1](/imgs/no7-1.PNG)

tambah record naik A ke ip probolinggo di gunung.semerud13.pw uml moker

### Soal 8
> domain **http://semerud13.pw** memiliki *Document Root* pada **/var/www/semerud13.pw**


install apache dan php5 pada uml probolinggo

![soal8-1](/imgs/no8-1.PNG)

setting site semerud13.pw

    ServerName semerud13.pw
    ServerAlias www.semerud13.pw
    DocumentRoot /var/www/semerud13.pw

![soal8-2](/imgs/no8-2.PNG)

/var/www nya semerud13, isinya index.php

### Soal 9
> aktifkan mod rewrite agar url dari **http://semerud13.pw/index.php/home** menjadi **http://semerud13.pw/home**

![soal9-1](/imgs/no9-1.PNG)

edit file semerud13.pw 

    AllowOverride All ditambahkan agar konfigurasi .htaccess dapat berjalan.
    +FollowSymLinks ditambahkan agar konfigurasi mod_rewrite dapat berjalan.
    -Multiviews ditambahkan agar konfigurasi mod_negotiation tidak dapat berjalan. mod_negotiation bisa 'rewrite' requests sehingga menimpa dan mengganggu mod_rewrite.

![soal9-2](/imgs/no9-2.PNG)

```
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^([^\.]+) $1.php [NC, L]
RewriteRule ^index.php/home /index [R=301,NC,L]
```

### Soal 10
> web **http://penanjakan.semerud13.pw** akan digunakan untuk menyimpan asset file yang memiliki *Document Root* pada **/var/www/penanjakan.semerud13.pw** dan memiliki struktur folder sebagai berikut

    /var/www/penanjakan.semerud13.pw
     |__ /public
     |    |__ /javascripts
     |    |__ /css
     |    |__ /images
     |__ /errors

![soal10-1](/imgs/no10-1.PNG)

buat site untuk penanjakan.semerud13.com dengan root /var/www/penanjakan.semerud13.pw

![soal10-2](/imgs/no10-2.PNG)

membuat folder public yang berisi javascripts, css, images. dan folder errors


### Soal 11
> Pada folder **/public** dibolehkan directory listing namun untuk folder yang berada di dalamnya tidak dibolehkan

![soal11-1](/imgs/no11-1.PNG)

tambah Options +Indexes untuk root
tambah Options -Indexes untuk root/public/javascripts, root/public/javascripts, dan root/public/images

2,3,4
![soal11-2](/imgs/no11-2.PNG)

![soal11-3](/imgs/no11-3.PNG)

![soal11-4](/imgs/no11-4.PNG)

forbidden access

### Soal 12
> untuk mengatasi HTTP error code 404, disediakan file 404.html pada folder **/errors** untuk mengganti error default 404 dari apache

![soal12-1](/imgs/no12-1.PNG)

tambah ErroDocument 404 /errors/404.html

![soal12-2](/imgs/no12-2.PNG)

contoh

### Soal 13
> untuk mengakses file asset javascript awalnya harus menggunakan url **http://penanjakan.semerud13.pw/public/javascripts**, karena terlalu panjang  maka dibuatkan konfigurasi virtual host agar ketika mengakses file asset menjadi **http://penanjakan.semerud13.pw/js**

![soal13-1](/imgs/no13-1.PNG)

tambah Alias "/js" "/var/www/penanjakan.semerud13.pw/public/javascripts"

### Soal 14
> buat **http://naik.gunung.semerud13.pw** pada port **8888** dengan *Document Root* pada **/var/www/naik.gunung.semerud13.pw**

![soal14-1](/imgs/no14-1.PNG)

buat site gunung.semerud13.pw di port 8888

![soal14-2](/imgs/no14-2.PNG)

tambah Listen 8888 di apache2/ports.conf

![soal14-3](/imgs/no14-3.PNG)

contoh

### Soal 15
> dikarenakan web bersifat private, **http://naik.gunung.semerud13.pw** diberi autentikasi dengan username `semeru` dan password `kuynaikgunung`

![soal15-1](/imgs/no15-1.PNG)

jalankan command htpasswrd -c /etc/apache/.htpasswd semeru

lalu akan ada promt password diisi dengan kuynaikgunung

akan menyimpan autentikasi yang ter enkripsi

![soal15-2](/imgs/no15-2.PNG)

tambahkan ini di documentroot
AuthType Basic
AuthName "Konten Terkunci"
AuthUserFile /etc/apache2/.htpasswd
Require valid-user

3,4
![soal15-3](/imgs/no15-3.PNG)

![soal15-4](/imgs/no15-4.PNG)

contoh

### Soal 16
> *IP PROBOLINGGO* dialihkan secara otomatis ke **http://semerud13.pw**

![soal16-1](/imgs/no16-1.PNG)

edit file default dengan documentroot /var/www/default

![soal16-2](/imgs/no16-2.PNG)

buat file .htaccess di docroot yang berisi

RewriteEngine On
RewriteBase /
RewriteCond %{HTTP_HOST} ^10\.151\.79\.116$
RewriteRule ^(.*)$ http://semerud13.pw [R=301,L]

### Soal 17
> request gambar yang memiliki substring `semeru` pada **/var/www/penanjakan.semerud13.pw/public/images** diarahkan menuju **semeru.jpg**

![soal17-1](/imgs/no17-1.PNG)

ubah vhost pada penanjakan.semerud.13.pw agar dapat membaca htaccess

2
![soal17-2](/imgs/no17-2.PNG)

tambah modrewrite di docroot penanjakan.semerud13.pw

```
RewriteEngine On
RewriteCond %{REQUEST_URI} !/public/images/semeru.jpg
RewriteRule ^(.*)(public/images/(.*)(semeru)(.*))(.*)$ /public/images/semeru.jpg [R=301]
```

