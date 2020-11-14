## Praktikum Modul 1
Kelompok D13
- 05111840000094 Rafi Nizar Abiyyi
- 05111740000192 Faishal Abiyyudzakir

<br>

### Soal 1
> membuat website utama dengan alamat **http://semerud13.pw**


![soal1-1](/imgs/no1-1.PNG)

Buat zone `semerud13.pw` di uml **MALANG** yang memiliki file bind pada `/etc/bind/jarkom/semerud13.pw`

![soal1-2](/imgs/no1-2.PNG)

bind diarahkan ke IP **PROBOLINGGO**

<br>

### Soal 2
> yang memiliki alias **http://www.semerud13.pw**

![soal2-1](/imgs/no2-1.PNG)

tambah record `CNAME` dengan nama `www` mengarah ke `semerud13.pw.` pada file bind `semerud13.pw`

<br>

### Soal 3
> memiliki subdomain **http:///penanjakan.semerud13.pw** yang diatur DNS-nya di pada **MALANG** dan mengarah ke IP server **PROBOLINGGO**

![soal3-1](/imgs/no3-1.PNG)

tambah record `A` dengan nama `penanjakan` mengarah ke ip probolinggo pada file bind `semerud13.pw`

<br>

### Soal 4
> reverse domain untuk domain utama

![soal4-1](/imgs/no4-1.PNG)

Tambah zone `79.151.10-in-addr.arpa` di uml **MALANG** yang memiliki file bind pada `/etc/bind/jarkom/79.151.10-in-addr.arpa`


![soal4-2](/imgs/no4-2.PNG)

Tambah record `PTR` byte terakhir milik ip **PROBOLIGGO**  ke `semerud13.pw.`

<br>

### Soal 5
> membuat DNS server Slave pada **MOJOKERTO**

![soal5-1](/imgs/no5-1.PNG)

Pada `named.conf.local` di uml **MALANG** edit zone `semerud13.pw` tambah `allow-transfer` ke IP **MOJOKERTO** dan `notify`

![soal5-2](/imgs/no5-2.PNG)

Pada named.conf.local di mojokerto tambah zone `semerud13.pw` dengan `type slave` dan tambah `masters` IP **MALANG**

![soal5-3](/imgs/no5-3.PNG)

Stop service bind9 di malang

![soal5-4](/imgs/no5-4.PNG)

Ping dari klien **GRESIK** (nameserver mengarah ke **MALANG** dan **MOJOKERTO**)


<br>

### Soal 6
> membuat subdomain dengan alamat http://gunung.semerud13.pw yang didelegasikan pada server **MOJOKERTO** dan mengarah ke IP server **PROBOLINGGO**

![soal6-1](/imgs/no6-1.PNG)

tambah record A ns ke ip moker, dan record gunung NS ke ns
Tambah record `A` dengan nama `ns` mengarah ke IP **MOJOKERTO** dan record `NS` dengan nama gunung mengarah ke `ns`

![soal6-2](/imgs/no6-2.PNG)

Edit named.conf.options

- komen `dnssec-validation auto;`
- tambah `allow-query{any;};`

![soal6-3](/imgs/no6-3.PNG)

Buat zone `gunung.semerud13.pw` di uml **MOJOKERTO** yang memiliki file bind di `/etc/bind/delegasi/gunung.semerud13.pw`

![soal6-4](/imgs/no6-4.PNG)

Buat file bind `/etc/bind/delegasi/gunung.semerud13.pw` dan buat record `A` mengarah ke IP **PROBOLINGGO**

<br>

### Soal 7
> subdomain dengan nama **http://naik.gunung.semerud13.pw** diarahkan ke IP server **PROBOLINGGO**

![soal7-1](/imgs/no7-1.PNG)

Tambah record `A` nama `naik` ke ip **PROBOLINGGO** pada bind `gunung.semerud13.pw` uml **PROBOLINGGO**

<br>

### Soal 8
> domain **http://semerud13.pw** memiliki *Document Root* pada **/var/www/semerud13.pw**


install apache2 dan php5 pada uml probolinggo

![soal8-1](/imgs/no8-1.PNG)

Buat virtual host `/etc/apache2/sites-avaiable/semerud13.pw` dengan setting:
```
ServerName semerud13.pw
ServerAlias www.semerud13.pw
DocumentRoot /var/www/semerud13.pw
```

![soal8-2](/imgs/no8-2.PNG)

Buat document root untuk domain utama di `/var/www/semerud13.pw`

<br>

### Soal 9
> aktifkan mod rewrite agar url dari **http://semerud13.pw/index.php/home** menjadi **http://semerud13.pw/home**

![soal9-1](/imgs/no9-1.PNG)

Aktifkan mod rewrite dengan `a2enmod` dan buat virtual host dapat membaca `.htaccess`
```
AllowOverride All
Options +FollowSymLinks
Options -Multiviews
```

![soal9-2](/imgs/no9-2.PNG)

Isi mod rewrite: 
```
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^([^\.]+) $1.php [NC, L]
RewriteRule ^index.php/home /index [R=301,NC,L]
```

<br>

### Soal 10
> web **http://penanjakan.semerud13.pw** akan digunakan untuk menyimpan asset file yang memiliki *Document Root* pada **/var/www/penanjakan.semerud13.pw** dan memiliki struktur folder sebagai berikut
```
    /var/www/penanjakan.semerud13.pw
     |__ /public
     |    |__ /javascripts
     |    |__ /css
     |    |__ /images
     |__ /errors
```
![soal10-1](/imgs/no10-1.PNG)

Buat virtual host `/etc/apache2/sites-available/penanjakan.semerud13.pw` dengan document root pada `/var/www/penanjakan.semerud13.pw`

![soal10-2](/imgs/no10-2.PNG)

Membuat folder public yang berisi javascripts, css, images. dan folder errors

<br>

### Soal 11
> Pada folder **/public** dibolehkan directory listing namun untuk folder yang berada di dalamnya tidak dibolehkan

![soal11-1](/imgs/no11-1.PNG)

Pada virtual host **penanjakan.semerud13.pw**:
- tambah Options +Indexes untuk `root`
- tambah Options -Indexes untuk `root/public/javascripts`, `root/public/javascripts`, dan `root/public/images`

Forbidden Access

![soal11-2](/imgs/no11-2.PNG)

![soal11-3](/imgs/no11-3.PNG)

![soal11-4](/imgs/no11-4.PNG)

<br>

### Soal 12
> untuk mengatasi HTTP error code 404, disediakan file 404.html pada folder **/errors** untuk mengganti error default 404 dari apache

![soal12-1](/imgs/no12-1.PNG)

Pada virtual host  **penanjakan.semerud13.pw** tambah:
```
ErroDocument 404 /errors/404.html
```

![soal12-2](/imgs/no12-2.PNG)

<br>

### Soal 13
> untuk mengakses file asset javascript awalnya harus menggunakan url **http://penanjakan.semerud13.pw/public/javascripts**, karena terlalu panjang  maka dibuatkan konfigurasi virtual host agar ketika mengakses file asset menjadi **http://penanjakan.semerud13.pw/js**

![soal13-1](/imgs/no13-1.PNG)

Pada virtual host  **penanjakan.semerud13.pw** tambah
```
Alias "/js" "/var/www/penanjakan.semerud13.pw/public/javascripts"
```

<br>

### Soal 14
> buat **http://naik.gunung.semerud13.pw** pada port **8888** dengan *Document Root* pada **/var/www/naik.gunung.semerud13.pw**

![soal14-1](/imgs/no14-1.PNG)

Buat virtual host `/etc/apache2/sites-available/gunung.semerud13.pw` dengan document root pada `/var/www/gunung.semerud13.pw` di port `8888`

![soal14-2](/imgs/no14-2.PNG)

tambah `Listen 8888` di `apache2/ports.conf`

![soal14-3](/imgs/no14-3.PNG)

<br>

### Soal 15
> dikarenakan web bersifat private, **http://naik.gunung.semerud13.pw** diberi autentikasi dengan username `semeru` dan password `kuynaikgunung`

![soal15-1](/imgs/no15-1.PNG)

Jalankan command
```
htpasswrd -c /etc/apache/.htpasswd semeru
```
untuk membuat user `semeru` yang kemudian akan di promt password dan isi dengan `kuynaikgunung`

Akan menyimpan autentikasi yang ter enkripsi

![soal15-2](/imgs/no15-2.PNG)

Pada virtual host **naik.gunung.semerud13.pw** tambahkan pada root:
```
AuthType Basic
AuthName "Konten Terkunci"
AuthUserFile /etc/apache2/.htpasswd
Require valid-user
```
![soal15-3](/imgs/no15-3.PNG)

![soal15-4](/imgs/no15-4.PNG)

<br>

### Soal 16
> *IP PROBOLINGGO* dialihkan secara otomatis ke **http://semerud13.pw**

![soal16-1](/imgs/no16-1.PNG)

Edit virtual host default agar dapat mengakses `.htaccess` dan memiliki document root pada `/var/www/default`

![soal16-2](/imgs/no16-2.PNG)

buat file .htaccess di document root yang berisi:

```
RewriteEngine On
RewriteRule ^(.*)$ http://semerud13.pw [R=301,L]
```

<br>

### Soal 17
> request gambar yang memiliki substring `semeru` pada **/var/www/penanjakan.semerud13.pw/public/images** diarahkan menuju **semeru.jpg**

![soal17-1](/imgs/no17-1.PNG)

Pada virtual host **semerud13.pw** buat dapat membaca `.htaccess`

![soal17-2](/imgs/no17-2.PNG)

buat file .htaccess di document root yang berisi:

```
RewriteEngine On
RewriteCond %{REQUEST_URI} !/public/images/semeru.jpg
RewriteRule ^(.*)(public/images/(.*)(semeru)(.*))(.*)$ /public/images/semeru.jpg [R=301]
```