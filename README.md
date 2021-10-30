# Jarkom-Modul-2-C02-2021
## 1. Membuat topologi seperti disoal
![image](https://user-images.githubusercontent.com/31591861/139530901-8e9b99db-2517-47a3-bfb5-b7d560583c86.png)

## Jawaban
Lakukan setting network masing-masing node: 

**Foosha (sebagai Router)**
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.15.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 10.15.2.1
	netmask 255.255.255.0
```

**Loguetown**
```
auto eth0
iface eth0 inet static
	address 10.15.1.2
	netmask 255.255.255.0
	gateway 10.15.1.1
```

**Alabasta**
```
auto eth0
iface eth0 inet static
	address 10.15.1.3
	netmask 255.255.255.0
	gateway 10.15.1.1
```

**EniesLobby**
```
auto eth0
iface eth0 inet static
	address 10.15.2.2
	netmask 255.255.255.0
	gateway 10.15.2.1
```

**Water7**
```
auto eth0
iface eth0 inet static
	address 10.15.2.3
	netmask 255.255.255.0
	gateway 10.15.2.1
```

**Skypie**
```
auto eth0
iface eth0 inet static
	address 10.15.2.4
	netmask 255.255.255.0
	gateway 10.15.2.1
```
`iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.15.0.0/16` pada Foosha.
`echo nameserver 10.15.1.1 > /etc/resolv.conf` pada node ubuntu yang lain.

Lalu restart semua node dan akses dapat ditest dengan mengeping ke google!

![image](https://user-images.githubusercontent.com/31591861/139531071-bf6fdadd-01dd-40ff-bdf2-20a220e95b66.png)


## 2. Luffy ingin menghubungi Franky yang berada di `EniesLobby` dengan denden mushi. Kalian diminta Luffy untuk membuat website utama dengan mengakses `franky.yyy.com` dengan alias `www.franky.yyy.com` pada folder kaizoku.

## Jawaban

Lakukan kedua command ini untuk menginstall bind9
```
apt-get update
apt-get install bind9 -y
```

Lalu edit file named.conf.local dengan menambahkan
```
zone "franky.c02.com" {
        type master;
        file "/etc/bind/kaizoku/franky.c02.com";
};
```
Jangan lupa membuat folder kaizoku dengan menggunakan
`mkdir /etc/bind/kaizoku`

Setelah itu copy file `db.local` ke `/etc/bind/kaizoku/franky.c02.com` dengan menggunakan command `cp /etc/bind/db.local /etc/bind/kaizoku/franky.c02.com`

Edit file `/etc/bind/kaizoku/franky.c02.com` dengan
```
;
;BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     franky.c02.com. root.franky.c02.com. (
                     2021100401         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      franky.c02.com. 
@       IN      A       10.15.2.4 ;Enieslobby
WWW     IN      CNAME   franky.c02.com.
```

Tambahkan
```
//dnssec-validation auto;
allow-query{any;};
```

Setelah itu restart bind dengan command `service bind9 restart`

![image](https://user-images.githubusercontent.com/31591861/139531407-a5326ee5-ebd9-4db3-af62-2835d6cbb1ad.png)

## 3. Setelah melakukan konfigurasi server, maka dilakukan konfigurasi Webserver. Pertama dengan webserver www.franky.yyy.com. Pertama, luffy membutuhkan webserver dengan DocumentRoot pada /var/www/franky.yyy.com.

## Jawaban


## 4. Setelah melakukan konfigurasi server, maka dilakukan konfigurasi Webserver. Pertama dengan webserver www.franky.yyy.com. Pertama, luffy membutuhkan webserver dengan DocumentRoot pada /var/www/franky.yyy.com.

## Jawaban


## 5. Setelah melakukan konfigurasi server, maka dilakukan konfigurasi Webserver. Pertama dengan webserver www.franky.yyy.com. Pertama, luffy membutuhkan webserver dengan DocumentRoot pada /var/www/franky.yyy.com.

## Jawaban


## 6. Setelah melakukan konfigurasi server, maka dilakukan konfigurasi Webserver. Pertama dengan webserver www.franky.yyy.com. Pertama, luffy membutuhkan webserver dengan DocumentRoot pada /var/www/franky.yyy.com.

## Jawaban


## 7. Setelah melakukan konfigurasi server, maka dilakukan konfigurasi Webserver. Pertama dengan webserver www.franky.yyy.com. Pertama, luffy membutuhkan webserver dengan DocumentRoot pada /var/www/franky.yyy.com.

## Jawaban


## 8. Setelah melakukan konfigurasi server, maka dilakukan konfigurasi Webserver. Pertama dengan webserver www.franky.yyy.com. Pertama, luffy membutuhkan webserver dengan DocumentRoot pada /var/www/franky.yyy.com.

## Jawaban
Pertama, install apache2 dengan `apt-get install apache2` dan install php dengan `apt-get install php`.
Berikut adalah untuk konfigurasi dari franky.c02.com.conf. Mengganti documentRoot dan menambahkan serverName dan serverAlias sesuai format soal, yaitu franky.c02.com
![image](https://user-images.githubusercontent.com/73484021/139518473-41ad689a-12fd-4464-b0ef-af1cf7b1602f.png).<br>
Buat direktori baru dengan `mkdir franky.c02.com` pada `/var/www`. Jalankan perintah `franky.c02.com`.

## 9. Setelah itu, Luffy juga membutuhkan agar url www.franky.yyy.com/index.php/home dapat menjadi menjadi www.franky.yyy.com/home. 

## Jawaban
Install wget dan unzip dengan `apt-get install wget` dan `apt-get install unzip` untuk mendownload zip dari github. Download zip dari github dengan wget link address dan `unzip franky.zip`.
Masuk ke folder franky yang telah di unzip dan copy file tersebut ke `/var/www/franky.c02.com`. Masuk ke direktori `/var/www/franky.c02.com`. Jalankan perintah `a2enmod rewrite` dan buat file baru `.htaccess` dengan konfigurasi berikut :<br>
![image](https://user-images.githubusercontent.com/73484021/139518738-63142796-2c6e-48ec-8f11-501f63725141.png)<br>
Lalu masuk ke direktori `/etc/apache2/sites-available` dan edit `franky.c02.com.conf` untuk menambahkan konfigurasi berikut untuk module rewrite :<br>
![image](https://user-images.githubusercontent.com/73484021/139518801-f9486d07-882a-4962-a24c-3b2d292e7258.png)<br>
Testing pada Loguetown dengan `lynx www.franky.c02.com/home` maka hasilnya akan muncul bounty seperti berikut :<br>
![image](https://user-images.githubusercontent.com/73484021/139518840-94730159-0b65-4cc6-918c-976e8f4a3276.png)

## 10. Setelah itu, pada subdomain www.super.franky.yyy.com, Luffy membutuhkan penyimpanan aset yang memiliki DocumentRoot pada /var/www/super.franky.yyy.com .

## Jawaban
Berikut adalah untuk konfigurasi dari super.franky.c02.com.conf. Mengganti documentRoot dan menambahkan serverName dan serverAlias sesuai format soal, yaitu super.franky.c02.com<br>
![image](https://user-images.githubusercontent.com/73484021/139518871-61ab59c6-f6b9-4b86-90ea-cf8b9b9085a7.png)<br>
Buat direktori baru dengan `mkdir super.franky.c02.com` pada `/var/www`. Jalankan perintah `a2ensite super.franky.c02.com`.

## 11. Akan tetapi, pada folder /public, Luffy ingin hanya dapat melakukan directory listing saja.

## Jawaban
Buat directory `super.franky.c02.com` pada `/var/www`.
Berikut adalah untuk konfigurasi dari super.franky.c02.com.conf. Tambahkan konfigurasi berikut untuk directory listing.<br>
![image](https://user-images.githubusercontent.com/73484021/139518916-3646d168-b1f8-4e9d-921e-f8f6ce970ae5.png)<br>
Download zip dari github dengan wget link address dan `unzip super.franky.zip`. Masuk ke folder super.franky yang telah di unzip dan copy file tersebut ke `/var/www/super.franky.c02.com`. 
Lalu, testing pada Loguetown dengan `lynx www.super.franky.c02.com/public` maka hasilnya akan seperti berikut :<br>
![image](https://user-images.githubusercontent.com/73484021/139518987-2d4adfd6-3fb1-44e7-89e6-fecb048cecfd.png)

## 12. Tidak hanya itu, Luffy juga menyiapkan error file 404.html pada folder /error untuk mengganti error kode pada apache .

## Jawaban
Tambahkan konfigurasi `ErrorDocument 404 /error/404.html` pada konfigurasi `super.franky.c02.com.conf`. Lalu, dapat di testing pada Loguetown dengan `lynx www.super.franky.c02.com/testerror`. Maka akan muncul seperti berikut :<br>
![image](https://user-images.githubusercontent.com/73484021/139519055-cda6f0a7-3340-4c68-a111-fb9341dbdca3.png)

## 13. Luffy juga meminta Nami untuk dibuatkan konfigurasi virtual host. Virtual host ini bertujuan untuk dapat mengakses file asset www.super.franky.yyy.com/public/js menjadi www.super.franky.yyy.com/js. 

## Jawaban
Tambahkan konfigurasi berikut pada `super.franky.c02.com.conf` :<br>
![image](https://user-images.githubusercontent.com/73484021/139519083-50dfdc98-925f-4c95-a47c-4356729616cf.png)<br>
Untuk dapat mengakses `www.super.franky.yyy.com/public/js` menjadi `www.super.franky.yyy.com/js` saja. Lalu dapat di testing di Loguetown dengan `lynx www.super.franky.c02.com/js`. Maka hasilnya seperti berikut :<br>
![image](https://user-images.githubusercontent.com/73484021/139519115-3218fa41-5242-4e14-932d-ebdd15bd8455.png)


## 14. Luffy meminta untuk web www.general.mecha.franky.yyy.com hanya bisa diakses dengan port 15000 dan port 15500

## Jawaban
Masuk ke /etc/apache2/sites-available/
```cd /etc/apache2/sites-available/```
Lalu copy file 000-default.conf ke file baru general.mecha.franky.c02.com.conf
```cp 000-default.conf general.mecha.franky.c02.com.conf```
Ubah isi general.mecha.franky.c02.com.conf dengan :
```
<VirtualHost *:15000 *:15500>
ServerName general.mecha.franky.c02.com
ServerAdmin webmaster@localhost
DocumentRoot /var/www/general.mecha.franky.c02.com
ServerAlias www.general.mecha.franky.c02.com
```
Untuk di dalam script.sh bisa langsung cat dari /root/general.mecha.franky.c02.com.conf ke /etc/apache2/sites-available/general.mecha.franky.c02.com.conf karena settingan conf sudah disimpan di /root
```cat /root/general.mecha.franky.c02.com.conf > /etc/apache2/sites-available/general.mecha.franky.c02.com.conf```

Kembali ke folder sebelumnya yakni /etc/apache2/ . Lalu Masukkan listen untuk port 15000 dan 15500 
```cd ..```
Tambahkan berikut pada ports.conf
```
...
Listen 15000
Listen 15500
...
```
Jika pada script.sh bisa langsung cat file ports.conf pada /root karena settingan sudah disimpan
```cat /root/ports.conf > /etc/apache2/ports.conf```

Buat folder baru untuk project webnya, lalu copy seluruh isi dari hasil unzip file general.mecha.franky.zip ke /var/www/general.mecha.franky.c02.com secara rekursif 
```
mkdir /var/www/general.mecha.franky.c02.com
cp -R /root/general.mecha.franky/* /var/www/general.mecha.franky.c02.com
```

Lalu aktifkan dengan a2ensite web general.mecha.franky.c02.com tadi, dan restart apache
```
a2ensite general.mecha.franky.c02.com
service apache2 restart
```

Untuk mengecek hasilnya bisa dicoba pada Loguetown dengan :
```Lynx general.mecha.franky.c02.com:15000``` 
dan
```Lynx general.mecha.franky.c02.com:15500``` 

Berikut adalah hasilnya :

## 15. Autentikasi username luffy dan password onepiece dan file di /var/www/general.mecha.franky.yyy

## Jawaban
Buka file /etc/apache2/sites-available/general.mecha.franky.c02.conf
```
cd /etc/apache2/sites-available/
vi general.mecha.franky.c02.com.conf
```
Tambahkan dengan settingan berikut :
```
...
<Directory "/var/www/general.mecha.franky.c02.com">
    AuthType Basic
    AuthName "Restricted Content"
    AuthUserFile /etc/apache2/.htpasswd
    Require valid-user
</Directory>
...
```
Untuk file pada script.sh langsung cat dari /root/general.mecha.franky.c02.com.conf ke /etc/apache2/sites-available/general.mecha.franky.c02.com.conf karena settingan sudah disimpan
```cat /root/general.mecha.franky.c02.com.conf > /etc/apache2/sites-available/general.mecha.franky.c02.com.conf```

Buat username luffy dengan password onepiece untuk mengakses web general.mecha.franky.c02.com. Lalu restart apache
```
htpasswd -c /etc/apache2/.htpasswd luffy onepiece
service apache2 restart
```

Tes dengan membuka kembali menggunakan
```Lynx general.mecha.franky.c02.com:15000``` 
dan 
```Lynx general.mecha.franky.c02.com:15500``` 

Berikut adalah hasilnya, Masukkan username :

Masukkan Password :

Situs berhasil diakses :

## 16. Setiap kali mengakses IP Skypie akan dialihkan secara otomatis ke www.franky.yyy.com

## Jawaban
Masuk ke dalam /var/www/html. Lalu buat file .htaccess disana. 
```cd /var/www/html/```
Kemudian tuliskan konfigurasi berikut pada .htaccess nya. NB :[IP Prefix].2.4
```
RewriteEngine On
RewriteBase /
RewriteCond %{HTTP_HOST} ^10\.15\.2\.4$
RewriteRule ^(.*)$ http://www.franky.c02.com/$1 [L,R=301]
```
Pada script.sh langsung cat /root/htaccess.txt ke /var/www/html/.htaccess , karena settingan sudah sudah disimpan
```cat /root/htaccess.txt > /var/www/html/.htaccess```

Lalu restart apache
```service apache2 restart```
Tes dengan `lynx 10.15.2.4` pada Loguetown, Maka akan langung di akses www.franky.c02.com :

## 17. Mengarahkan request gambar dari client yang memiliki substring 'franky' di super.franky.yyy.com ke file franky.png

## Jawaban
Masuk ke dalam /var/www/super.franky.c02.com , Lalu buat file .htaccess disana. 
```cd /var/www/super.franky.c02.com```

Isikan .htaccess dengan konfigurasi berikut : 
```
RewriteEngine On
RewriteRule (.*)franky(.*)(\.jpg|\.png|\.gif)$ http://super.franky.c02.com/public/images/franky.png [L,R=301]
```
RewriteRule akan melakukan redirect 301 dari request dengan regex yang telah dibuat untuk menuju path yang memiliki substring franky dan melanjutkan request yang berupa gambar ke file franky.png
Pada script.sh langsung cat /root/super-franky-htaccess.txt ke /var/www/super.franky.c02.com/.htaccess , karena settingan sudah sudah disimpan.
```cat /root/super-franky-htaccess.txt > /var/www/super.franky.c02.com/.htaccess```

Lalu restart apache
```service apache2 restart```

Test dengan file yang memiliki substring franky :

Test dengan file yang tidak memiliki substring franky :
