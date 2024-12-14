# Final-Project_OS_Server_System_Admin
Spesifikasi server yang digunakan 
- Ubuntu Server 22.04.5 LTS
- RAM 4GB
- Prosesor 4CPU
- Virtual Size 44GB


## 1. Instalasi OPEN SSH SERVER
Langkah 1: Lakukan Instalasi Paket SSH Server 
``` 
sudo apt install openssh-server -y 
```
Langkah 2: Mengaktifkan Layanan ssh server
```
sudo systemctl enable ssh
```
Langkah 3: Memulai Layanan SSH SERVER
```
sudo systemctl start ssh
```
Langkah 4: Cek ip ubuntu server
```
ip add
```
Langkah 5: Cek status SSH SERVER
```
sudo systemctl status ssh
```
Untuk melakukan remote menggunakan ssh gunakan perintah, Contoh ssh ghalih@123.456.789
```
ssh [username]@[ip addess]
```
## 2. Instalasi FTP SERVER
1. Instalasi FTP Server
Langkah 1. Masuk ke terminal Ubuntu dan instal layanan vsftpd:
Copy code
```
sudo apt update
sudo apt install vsftpd
```
Langkah 2. Pastikan layanan vsftpd berjalan:
Copy code
```
sudo systemctl start vsftpd
sudo systemctl enable vsftpd
```
2. Konfigurasi FTP Server
Langkah 1. Edit file konfigurasi vsftpd:
Copy code
```
sudo nano /etc/vsftpd.conf
```
# Langkah 3. edit file
anonymous_enable=NO
local_enable=YES
write_enable=YES

## 3. Instalasi WEB SERVER
Instalasi Apache2
Langkah 1: Instalasi Paket Apache2
```
apt update && apt upgrade
apt-get install apache2
```

Konfigurasi Apache2
Langkah 1: Buka File Konfigurasi Apache2
```
nano /etc/apache2/sites-available/000-default.conf
```

Langkah 2: Sesuaikan Konfigurasi dengan domain yang anda gunakan

Lengkah 3: Restart Layanan Apache2
```
systemctl restart apache2
```

Langkah 4: Cek Apache2
```
systemctl status apache2
```

Konfigurasi ufw
```
ufw allow in "Apache"
ufw status
```

Konfigurasi CMS Wordpress pada Apache2
Langkah 1: Melakukan Instalasi PHP
```
sudo apt install -y php libapache2-mod-php php-{common,xml,xmlrpc,curl,gd,imagick,cli,dev,imap,mbstring,opcache,soap,zip,intl}
```

cek versi php
```
php -v
```

Langkah 2: Melakukan Instalasi Database Server

Langkah 3: Buat Database untuk wordpress

login ke Database Terlebih dahulu:
```
mysql -u root -p
```

buat database untuk Wordpress dan berikan password sesuai keinginan anda
```
CREATE DATABASE wordpress;
CREATE USER 'wordpressuser'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpressuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

Langkah 4: Download dan Extract Paket Wordpress
```
cd /tmp && wget https://wordpress.org/latest.tar.gz
tar -xvf latest.tar.gz
```

Langkah 5: Salin direktori wordpress ke dalam direktori /var/www/html.
```
cp -R wordpress /var/www/html/
```

Langkah 6: Mengubah kepemilikan direktori /var/www/html/wordpress. dan Memodifikasi izin file.
```
chown -R www-data:www-data /var/www/html/wordpress/
chmod -R 755 /var/www/html/wordpress/
```

Langkah 8: Salin wp-config-sample.php dan ubah kepemilikan berkas wp-config.php.
```
cd /var/www/html/wordpress
cp wp-config-sample.php wp-config.php
chown www-data:www-data wp-config.php
```

Langkah 9: Edit file wp-config.php dan tambahkan baris di bawah ini pada file wp-config.php.
```
nano wp-config.php
```

Langkah 10: Tambahkan secure values dari wordpress secret key generator
```
curl -s https://api.wordpress.org/secret-key/1.1/salt/
```

Langkah 11: Konfigurasikan apache untuk memuat wordpress sebagai situs utama.
```
cd /etc/apache2/sites-available
cp 000-default.conf wordpress.conf
```

Masuk kedalam file wordpress.conf
```
nano wordpress.conf
``` 

Aktifkan WordPress.conf dan nonaktifkan 000-default.conf dan muat ulang layanan apache.
```
a2ensite wordpress.conf
a2dissite 000-default.conf
service apache2 reload
```

Langkah 12: Instalasi Admin Wordpress

Pilih Bahasa yang diinginkan 

Isi Nama situs,Password,dan Email 

Login dengan Akun yang sudah dibuat 

CMS sudah Berhasil diinstall 

Pengujian Konfigurasi Apache2


## 4. Instalasi DATABASE SERVER
1. Instalasi
Langkah 1:Installasi paket mariadb
```
sudo apt-get update
sudo apt-get install mariadb-server
```
Langkah 2:Untuk mengamankan installasi (Opsional)
```
sudo mysql_secure_installation
```

Langkah 3:Lakukan instalasi paket
```
sudo apt-get install phpmyadmin
```

Langkah 4:Restart ulang layanan
```
sudo systemctl restart apache2
```
## 5. Instalasi DNS SERVER
1. Instalasi BIND9
Langkah 1: Instalasi Paket bind9
```
apt update
apt-get install bind9
```
2. Konfigurasi BIND9
Langkah 1: copy file untuk Konfigurasi "Forward" dan "Reverse"
```
cd /etc/bind
cp db.local db.forward
cp db.127 db.reverse
```

Langkah 2: Konfigurasi file db.forward
```
nano db.forward
```

Langkah 3: Konfigurasi file db.reverse
```
nano db.reverse
```

Langkah 4: Buka Konfigurasi named.conf.local untuk konfigurasi DNS Zones
```
nano named.conf.local
```

Langkah 5: Konfigurasi Forwarders
```
nano named.conf.options
```

Langkah 6: Konfigurasi DNS diperangkat Server
```
nano /etc/resolv.conf
```

Langkah 7: Restart Layanan Bind9
```
systemctl restart bind9
```

3. Pengujian Konfigurasi DNS
Langkah 1: Instalasi paket dns resolver
```
apt-get install dnsutils
```
Langkah 2: Lakukan pengujian dengan nslookup
