# Jarkom-Modul-2-C02-2021

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


