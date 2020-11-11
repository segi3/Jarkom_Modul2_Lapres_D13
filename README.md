## Praktikum Modul 1
Kelompok D13
- 05111840000094 Rafi Nizar Abiyyi
- 05111740000192 Faishal Abiyyudzakir

<br>

### Soal 1
> membuat website utama dengan alamat **http://semerud13.pw**

1
buat zone semerud13.pw di uml malang
memiliki file bind pada /etc/bind/jarkom/semerud13.pw

2
isi file bind 

### Soal 2
> yang memiliki alias **http://www.semerud13.pw**

1
tambah record www CNAME mengarah ke semerud13.pw di bind semerud13.pw

### Soal 3
> memiliki subdomain **http:///penanjakan.semerud13.pw** yang diatur DNS-nya di pada **MALANG** dan mengarah ke IP server **PROBOLINGGO**

1
tambah record penanjakan A mengarah ke ip probolinggo di bind semerud13.pw

### Soal 4
> reverse domain untuk domain utama

1
tambah zone 79.151.10-in-addr.arpa di uml malang
memiliki file bind pada /etc/bind/jarkom/79.151.10-in-addr.arpa

2
isi file bind
tambah record byte terakhir milik ip probolinggo PTR ke semerud13.pw.

### Soal 5
> membuat DNS server Slave pada **MOJOKERTO**

1
edit named.conf.local di malang
edit zone tambah allowtransfer, also notify

2
edit named.conf.local di mojokerto
tambah zone, pake type slave, tambah masters

3
stop service bind9 di malang

4
(name server ngarah ke malang sama mojokerto)
coba ping di klien gresik

### Soal 6
> membuat subdomain dengan alamat http://gunung.semerud13.pw yang didelegasikan pada server **MOJOKERTO** dan mengarah ke IP server **PROBOLINGGO**

1
tambah record A ns_semeru ke ip moker, dan record gunung NS ke ns_semeru

2
edit named.conf.options
komen dnssec-validation auto;
tambah allow-query{any;};

3
tambah zone gunung.semerud13.pw di mojokerto

buat folder delegasi di /etc/bind

4
buat file gunung.semerud13.pw di /etc/bind/delegasi
buat record @ A mengarah ke probolinggo

### Soal 7
> subdomain dengan nama **http://naik.gunung.semerud13.pw** diarahkan ke IP server **PROBOLINGGO**

1
tambah record gunung A ke ip probolinggo di gunung.semerud13.pw uml moker

### Soal 8
> domain **http://semerud13.pw** memiliki *Document Root* pada **/var/www/semerud13.pw**


install apache dan php5 pada uml probolinggo

1
setting site semerud13.pw

2
/var/www nya semerud13, isinya index.php

### Soal 9
> aktifkan mod rewrite agar url dari **http://semerud13.pw/index.php/home** menjadi **http://semerud13.pw/home**

1
edit file semerud13.pw 

    AllowOverride All ditambahkan agar konfigurasi .htaccess dapat berjalan.
    +FollowSymLinks ditambahkan agar konfigurasi mod_rewrite dapat berjalan.
    -Multiviews ditambahkan agar konfigurasi mod_negotiation tidak dapat berjalan. mod_negotiation bisa 'rewrite' requests sehingga menimpa dan mengganggu mod_rewrite.

2
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^([^\.]+) $1.php [NC, L]

RewriteRule ^index.php/home /index [R=301,NC,L]

### Soal 10
> web **http://penanjakan.semerud13.pw** akan digunakan untuk menyimpan asset file yang memiliki *Document Root* pada **/var/www/penanjakan.semerud13.pw** dan memiliki struktur folder sebagai berikut

    /var/www/penanjakan.semerud13.pw
     |__ /public
     |    |__ /javascripts
     |    |__ /css
     |    |__ /images
     |__ /errors

1
buat site untuk penanjakan.semerud13.com dengan root /var/www/penanjakan.semerud13.pw

2
membuat folder public yang berisi javascripts, css, images. dan folder errors


### Soal 11
> Pada folder **/public** dibolehkan directory listing namun untuk folder yang berada di dalamnya tidak dibolehkan

1
tambah Options +Indexes untuk root
tambah Options -Indexes untuk root/public/javascripts, root/public/javascripts, dan root/public/images

2,3,4
forbidden access

### Soal 12
> untuk mengatasi HTTP error code 404, disediakan file 404.html pada folder **/errors** untuk mengganti error default 404 dari apache

1
tambah ErroDocument 404 /errors/404.html

2
contoh

### Soal 13
> untuk mengakses file asset javascript awalnya harus menggunakan url **http://penanjakan.semerud13.pw/public/javascripts**, karena terlalu panjang  maka dibuatkan konfigurasi virtual host agar ketika mengakses file asset menjadi **http://penanjakan.semerud13.pw/js**

1
tambah Alias "/js" "/var/www/penanjakan.semerud13.pw/public/javascripts"

### Soal 14
> buat **http://naik.gunung.semerud13.pw** pada port **8888** dengan *Document Root* pada **/var/www/naik.gunung.semerud13.pw**

1
buat site gunung.semerud13.pw di port 8888

2
tambah Listen 8888 di apache2/ports.conf

3
contoh

### Soal 15
> dikarenakan web bersifat private, **http://naik.gunung.semerud13.pw** diberi autentikasi dengan username `semeru` dan password `kuynaikgunung`

1
jalankan command htpasswrd -c /etc/apache/.htpasswd semeru

lalu akan ada promt password diisi dengan kuynaikgunung

akan menyimpan autentikasi yang ter enkripsi

2
tambahkan ini di documentroot
AuthType Basic
AuthName "Konten Terkunci"
AuthUserFile /etc/apache2/.htpasswd
Require valid-user

3,4,5
contoh

### Soal 16
> *IP PROBOLINGGO* dialihkan secara otomatis ke **http://semerud13.pw**

1
edit file default dengan documentroot /var/www/default

2
buat file .htaccess di docroot yang berisi

RewriteEngine On
RewriteBase /
RewriteCond %{HTTP_HOST} ^10\.151\.79\.116$
RewriteRule ^(.*)$ http://semerud13.pw [R=301,L]

### Soal 17
> request gambar yang memiliki substring `semeru` pada **/var/www/penanjakan.semerud13.pw/public/images** diarahkan menuju **semeru.jpg**

1
ubah vhost pada penanjakan.semerud.13.pw agar dapat membaca htaccess

2
tambah modrewrite di docroot penanjakan.semerud13.pw

RewriteEngine On
RewriteCond %{REQUEST_URI} !/public/images/semeru.jpg
RewriteRule ^(.*)(public/images/(.*)(semeru)(.*))(.*)$ /public/images/semeru.jpg [R=301]