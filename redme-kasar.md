1. membuat website dengan alamat semeruyy.pw

1
buat zone semerud13.pw di uml malang
memiliki file bind pada /etc/bind/jarkom/semerud13.pw

2
isi file bind 

2. memiliki alias www.semeruyy.pw

1
tambah record www CNAME mengarah ke semerud13.pw di bind semerud13.pw

3. memiliki subdomain penanjakan.semeruyy.pw yang diatur dns nya pada malang dan mengarah ke ip server probolinggo

1
tambah record penanjakan A mengarah ke ip probolinggo di bind semerud13.pw

4. Reverse domain untuk domain utama

1
tambah zone 79.151.10-in-addr.arpa di uml malang
memiliki file bind pada /etc/bind/jarkom/79.151.10-in-addr.arpa

2
isi file bind
tambah record byte terakhir milik ip probolinggo PTR ke semerud13.pw.


5. Membuat mojokerto sebagai DNS Slave malang

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

6. Membuat subdomain gunung.semerud13.com yang didelegasika pada mojokerto dan mengarah ke probolinggo

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

7. buat subdomain naik.gunung.semerud13.pw ke server probolinggo

1
tambah record gunung A ke ip probolinggo di gunung.semerud13.pw uml moker

8. domain semerud13.pw memiliki documentroot pada /var/www/semerud13.pw


install apache dan php5 pada uml probolinggo

1
setting site semerud13.pw

2
/var/www nya semerud13, isinya index.php

9. aktifkan mod rewrite agar url menjadi http://semerud13.pw/home dari index.php/home

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

10. buat web penanjakan.semerud13.pw untuk menyimpat asset

1
buat site untuk penanjakan.semerud13.com dengan root /var/www/penanjakan.semerud13.pw

2
membuat folder public yang berisi javascripts, css, images. dan folder errors



11. folder public dapat di list namun folder dalam public tidak dapat di list

1
tambah Options +Indexes untuk root
tambah Options -Indexes untuk root/public/javascripts, root/public/javascripts, dan root/public/images

2,3,4
forbidden access

12. ganti default error 404 page apache dengan error/404.html

1
tambah ErroDocument 404 /errors/404.html

2
contoh

13. beri alias untuk penanjakan.semerud13.pw/public/javascripts menjadi penanjakan.semerud13.pw/js

1
tambah Alias "/js" "/var/www/penanjakan.semerud13.pw/public/javascripts"

14. Buat web gunung.semerud13.pw pada port 8888

1
buat site gunung.semerud13.pw di port 8888

2
tambah Listen 8888 di apache2/ports.conf

3
contoh

15. membuat naik.gunung.semerud13.pw memiliki autentikasi dengan username "semeru" dan password "kuynaikgunung"

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

16. IP probolinggo redirect ke semerud13.pw

1
edit file default dengan documentroot /var/www/default

2
buat file .htaccess di docroot yang berisi

RewriteEngine On
RewriteBase /
RewriteCond %{HTTP_HOST} ^10\.151\.79\.116$
RewriteRule ^(.*)$ http://semerud13.pw [R=301,L]

17. request pada penanjakan.semerud13.pw dengan substring "semeru" diarahkan ke public/images/semeru.jpg

1
ubah vhost pada penanjakan.semerud.13.pw agar dapat membaca htaccess

2
tambah modrewrite di docroot penanjakan.semerud13.pw

RewriteEngine On
RewriteCond %{REQUEST_URI} !/public/images/semeru.jpg
RewriteRule ^(.*)(public/images/(.*)(semeru)(.*))(.*)$ /public/images/semeru.jpg [R=301]