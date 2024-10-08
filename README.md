# Jarkom-Modul-2-IT38-2024

## Anggota Kelompok
### Rafael Gunawan (5027231019)
### Randist Prawanda Putra (5027231059)
<hr>

## Topologi (2)
![image](https://github.com/user-attachments/assets/7a25912d-792d-476d-bc68-7a9baf9f870b)

# Soal
Sebuah kerajaan besar di Indonesia sedang mengalami pertempuran dengan penjajah. Kerajaan tersebut adalah Sriwijaya. Karena merasa terdesak Sriwijaya meminta bantuan pada Majapahit untuk mempertahankan wilayahnya. Pertempuran besar tersebut berada di Nusantara. Untuk topologi lihat pada link ini.

## Soal 1
Untuk mempersiapkan peperangan World War MMXXIV (Iya sebanyak itu), Sriwijaya membuat dua kotanya menjadi web server yaitu Tanjungkulai, dan Bedahulu, serta Sriwijaya sendiri akan menjadi DNS Master. Kemudian karena merasa terdesak, Majapahit memberikan bantuan dan menjadikan kerajaannya (Majapahit) menjadi DNS Slave. 

    Nusantara
    auto eth0
    iface eth0 inet dhcp
    
    auto eth1
    iface eth1 inet static
      address 10.82.1.1
      netmask 255.255.255.0
    
    auto eth2  
    iface eth2 inet static
      address 10.82.2.1
      netmask 255.255.255.0
    
    auto eth3
    iface eth3 inet static
       address 10.82.3.1
       netmask 255.255.255.0
    
    up iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.82.0.0/16

    
    Sriwijaya
    auto eth0
    iface eth0 inet static
      address 10.82.1.2
      netmask 255.255.255.0
      gateway 10.82.1.1
      up echo nameserver 192.168.122.1 > /etc/resolv.conf
    
    
    Albert Einstein
    auto eth0
    iface eth0 inet static
      address 10.82.2.2
      netmask 255.255.255.0
      gateway 10.82.2.1
      up echo nameserver 192.168.122.1 > /etc/resolv.conf
      up echo nameserver 10.82.1.2 > /etc/resolv.conf
    
    
    Tanjungkulai
    auto eth0 
    iface eth0 inet static 
      address 10.82.2.3
      netmask 255.255.255.0
      gateway 10.82.2.1
      up echo nameserver 192.168.122.1 > /etc/resolv.conf
    
    
    Bedahulu
    auto eth0
    iface eth0 inet static
      address 10.82.2.4
      netmask 255.255.255.0
      gateway 10.82.2.1
      up echo nameserver 192.168.122.1 > /etc/resolv.conf
    
    
    Kotalingga
    auto eth0
    iface eth0 inet static
      address 10.82.2.5
      netmask 255.255.255.0
      gateway 10.82.2.1
      up echo nameserver 192.168.122.1 > /etc/resolv.conf
    
    
    Majapahit
    auto eth0 
    iface eth0 inet static 
      address 10.82.3.2
      netmask 255.255.255.0
      gateway 10.82.3.1
      up echo nameserver 192.168.122.1 > /etc/resolv.conf
    
    
    Hayamwuruk
    auto eth0
    iface eth0 inet static
      address 10.82.3.3
      netmask 255.255.255.0
      gateway 10.82.3.1
      up echo nameserver 192.168.122.1 > /etc/resolv.conf
    
    
    Solok
    auto eth0
    iface eth0 inet static
      address 10.82.3.4
      netmask 255.255.255.0
      gateway 10.82.3.1
      up echo nameserver 192.168.122.1 > /etc/resolv.conf
    
    
    Srikandi
    auto eth0
    iface eth0 inet static
      address 10.82.3.5
      netmask 255.255.255.0
      gateway 10.82.3.1
      up echo nameserver 192.168.122.1 > /etc/resolv.conf

## Soal 2
Karena para pasukan membutuhkan koordinasi untuk melancarkan serangannya, maka buatlah sebuah domain yang mengarah ke Solok dengan alamat sudarsana.xxxx.com dengan alias www.sudarsana.xxxx.com, dimana xxxx merupakan kode kelompok. Contoh: sudarsana.it01.com.
#### Console Sriwijaya
1. ``apt update && apt install bind9 dnsutils -y``
2. ``cd /etc/bind``
3. ``nano named.conf.local``
   ```
   zone "sudarsana.it38.com" {
       type master;
   file "/etc/bind/it38/sudarsana.it38.com";
   };
4. ``mkdir it38``
5. ``cd it38``
6. ``cp ../db.local sudarsana.it38.com``
7. ``nano sudarsana.it38.com``
   ```
    ;
    ; BIND data file for local loopback interface
    ;
    $TTL    604800
    @       IN      SOA     sudarsana.it38.com. root.sudarsana.it38.com. (
                                  2         ; Serial
                             604800         ; Refresh
                              86400         ; Retry
                            2419200         ; Expire
                             604800 )       ; Negative Cache TTL
    ;
    @       IN      NS      sudarsana.it38.com.
    @       IN      A       10.82.3.4
    @       IN      AAAA    ::1
    www     IN      CNAME   sudarsana.it38.com.
8. ``service bind9 restart``
9. ``ping www.sudarsana.it38.com`` <br>
    ![image](https://github.com/user-attachments/assets/26165bf3-e3f2-4fe6-b4a3-b23eec8e2731)

## Soal 3
Para pasukan juga perlu mengetahui mana titik yang akan diserang, sehingga dibutuhkan domain lain yaitu pasopati.xxxx.com dengan alias www.pasopati.xxxx.com yang mengarah ke Kotalingga.
#### Console Sriwijaya
1. ``cd /etc/bind``
2. ``nano named.conf.local``
    ```
   zone "sudarsana.it38.com" {
      type master;
      file "/etc/bind/it38/sudarsana.it38.com";
    };
    
    zone "pasopati.it38.com" {
      type master;
      file "/etc/bind/it38/pasopati.it38.com";
    };
3. ``cd it38``
4. ``nano pasopati.it38.com``
    ```
    ;
    ; BIND data file for local loopback interface
    ;
    $TTL    604800
    @       IN      SOA     pasopati.it38.com. root.pasopati.it38.com. (
                                  2         ; Serial
                             604800         ; Refresh
                              86400         ; Retry
                            2419200         ; Expire
                             604800 )       ; Negative Cache TTL
    ;
    @       IN      NS      pasopati.it38.com.
    @       IN      A       10.82.2.5
    @       IN      AAAA    ::1
    www     IN      CNAME   pasopati.it38.com.
5. ``service bind9 restart``
6. ``ping pasopati.it38.com`` <br>
   ![image](https://github.com/user-attachments/assets/db2facc1-e19d-4b43-b68d-89f60cfeab33)

## Soal 4
Markas pusat meminta dibuatnya domain khusus untuk menaruh informasi persenjataan dan suplai yang tersebar. Informasi dan suplai meme terbaru tersebut mengarah ke Tanjungkulai dan domain yang ingin digunakan adalah rujapala.xxxx.com dengan alias www.rujapala.xxxx.com.
#### Console Sriwijaya
1. ``cd /etc/bind``
2. ``nano named.conf.local``
    ```
   zone "sudarsana.it38.com" {
      type master;
      file "/etc/bind/it38/sudarsana.it38.com";
    };
    
    zone "pasopati.it38.com" {
      type master;
      file "/etc/bind/it38/pasopati.it38.com";
    };

    zone "rujapala.it38.com" {
      type master;
      file "/etc/bind/it38/rujapala.it38.com";
    };
3. ``cd it38``
4. ``nano rujapala.it38.com``
    ```
    ;
    ; BIND data file for local loopback interface
    ;
    $TTL    604800
    @       IN      SOA     rujapala.it38.com. root.rujapala.it38.com. (
                                  2         ; Serial
                             604800         ; Refresh
                              86400         ; Retry
                            2419200         ; Expire
                             604800 )       ; Negative Cache TTL
    ;
    @       IN      NS      rujapala.it38.com.
    @       IN      A       10.82.2.3
    @       IN      AAAA    ::1
    www     IN      CNAME   rujapala.it38.com.
5. ``service bind9 restart``
6. ``ping rujapala.it38.com`` <br>
![image](https://github.com/user-attachments/assets/96c27360-9961-4e28-8926-a5c78d72324a)

## Soal 5
Pastikan domain-domain tersebut dapat diakses oleh seluruh komputer (client) yang berada di Nusantara.
#### Console Albert Einstein
1. ``ping www.sudarsana.it38.com``
2. ``ping www.pasopati.it27.com``
3. ``ping.www.rujapala.it27.com`` <br>
![image](https://github.com/user-attachments/assets/26165bf3-e3f2-4fe6-b4a3-b23eec8e2731) <br>
![image](https://github.com/user-attachments/assets/db2facc1-e19d-4b43-b68d-89f60cfeab33) <br>
![image](https://github.com/user-attachments/assets/96c27360-9961-4e28-8926-a5c78d72324a) <br>

## Soal 6
Beberapa daerah memiliki keterbatasan yang menyebabkan hanya dapat mengakses domain secara langsung melalui alamat IP domain tersebut. Karena daerah tersebut tidak diketahui secara spesifik, pastikan semua komputer (client) dapat mengakses domain pasopati.xxxx.com melalui alamat IP Kotalingga (Notes: menggunakan pointer record).
#### Console Sriwijaya
1. ``cd /etc/bind``
2. ``nano named.conf.local``
   ```
   zone "2.82.10.in-addr.arpa" {
      type master;
      file "/etc/bind/it38/2.82.10.in-addr.arpa";
    };
3. ``cd it38``
4. ``nano 2.82.10.in-addr.arpa``
    ```
    ;
    ; BIND data file for local loopback interface
    ;
    $TTL    604800
    @       IN      SOA     pasopati.it38.com. root.pasopati.it38.com. (
                                  2         ; Serial
                             604800         ; Refresh
                              86400         ; Retry
                            2419200         ; Expire
                             604800 )       ; Negative Cache TTL
    ;
    2.82.10.in-addr.arpa    IN    NS    pasopati.it38.com.
    5                       IN    PTR   pasopati.it38.com.
5. ``service bind9 restart``

#### Console Albert Einstein
6. ``apt install dnsutils -y``
7. ``host -t PTR 10.82.2.5`` <br>
![image](https://github.com/user-attachments/assets/acbae1a8-25d4-4a08-a6e2-6c6468132554) 

## Soal 7
Akhir-akhir ini seringkali terjadi serangan brainrot ke DNS Server Utama, sebagai tindakan antisipasi kamu diperintahkan untuk membuat DNS Slave di Majapahit untuk semua domain yang sudah dibuat sebelumnya yang mengarah ke Sriwijaya.
#### Console Majapahit
1. ``apt install bind9 dnsutils -y``
2. ``cd /etc/bind``
3. ``nano named.conf.local``
    ```
    zone "sudarsana.it38.com" {
            type slave;
            masters {10.82.1.2;};
            file "/var/lib/bind/it38/sudarsana.it38.com";
    };
    
    zone "pasopati.it38.com" {
            type slave;
            masters {10.82.1.2;};
            file "/var/lib/bind/it38/pasopati.it38.com";
    };
    
    zone "rujapala.it38.com" {
            type slave;
            masters {10.82.1.2;};
            file "/var/lib/bind/it38/rujapala.it38.com";
    };
    
    zone "2.82.10.in-addr.arpa" {
            type slave;
            masters {10.82.1.2;};
            file "/var/lib/bind/it38/2.82.10.in-addr.arpa";
    };
4. ``service bind9 restart``

#### Console Albert Einstein
5. ``Masukan nameserver DNS slavenya nameserver IP Majapahit di /etc/resolv.conf``

#### Console Majapahit
6. ``service bind9 stop``

#### Console Albert Einstein
7. ``ping sudarsana.it38.com`` <br>
![image](https://github.com/user-attachments/assets/96c27360-9961-4e28-8926-a5c78d72324a)

## Soal 8
Kamu juga diperintahkan untuk membuat subdomain khusus melacak kekuatan tersembunyi di Ohio dengan subdomain cakra.sudarsana.xxxx.com yang mengarah ke Bedahulu.
#### Console Sriwijaya
1. ``cd /etc/bind/it38``
2. ``nano sudarsana.it38.com``
   ```
    ;
    ; BIND data file for local loopback interface
    ;
    $TTL    604800
    @       IN      SOA     sudarsana.it38.com. root.sudarsana.it38.com. (
                                  2         ; Serial
                             604800         ; Refresh
                              86400         ; Retry
                            2419200         ; Expire
                             604800 )       ; Negative Cache TTL
    ;
    @       IN      NS      sudarsana.it38.com.
    @       IN      A       10.82.3.4
    @       IN      AAAA    ::1
    www     IN      CNAME   sudarsana.it38.com.
    cakra   IN      A       10.82.2.4
#### Console Albert Einstein
3. ``ping cakra.sudarsana.it38.com`` <br>
![image](https://github.com/user-attachments/assets/c7a3b435-a7d8-456d-8a7a-07e44402b19e)

## Soal 9
Karena terjadi serangan DDOS oleh shikanoko nokonoko koshitantan (NUN), sehingga sistem komunikasinya terhalang. Untuk melindungi warga, kita diperlukan untuk membuat sistem peringatan dari siren man oleh Frekuensi Freak dan memasukkannya ke subdomain panah.pasopati.xxxx.com dalam folder panah dan pastikan dapat diakses secara mudah dengan menambahkan alias www.panah.pasopati.xxxx.com dan mendelegasikan subdomain tersebut ke Majapahit dengan alamat IP menuju radar di Kotalingga.
#### Console Sriwijaya
1. ``cd /etc/bind/it38``
2. ``nano pasopati.it38.com``
    ```
    ;
    ; BIND data file for local loopback interface
    ;
    $TTL    604800
    @       IN      SOA     pasopati.it38.com. root.pasopati.it38.com. (
                                  2         ; Serial
                             604800         ; Refresh
                              86400         ; Retry
                            2419200         ; Expire
                             604800 )       ; Negative Cache TTL
    ;
    @       IN      NS      pasopati.it38.com.
    @       IN      A       10.82.2.5
    @       IN      AAAA    ::1
    ns1     IN      A       10.82.3.2
    panah   IN      NS      ns1
    www     IN      CNAME   pasopati.it38.com.
3. ``nano /etc/bind/named.conf.options`` <br>
![image](https://github.com/user-attachments/assets/9fb8494f-30c9-4d63-970d-6b4e3c2da4b0)
4. ``nano named.conf.local``
    ```
    zone "pasopati.it38.com" {
            type master;
            notify yes;
            also-notify {10.82.3.2;};
            allow-transfer {10.82.3.2;};
            file "/etc/bind/it38/pasopati.it38.com";
    };
5. ``service bind9 restart``

#### Console Majapahit
6. ``cd /etc/bind``
7. ``nano named.conf.options`` <br>
![image](https://github.com/user-attachments/assets/305fb060-6e01-4785-a287-f5afa344024a)
8. ``nano named.conf.local``
    ```
    zone "panah.pasopati.it38.com" {
            type master;
            file "/etc/bind/panah/panah.pasopati.it38.com";
    };
9. ``mkdir panah``
10. ``cd panah``
11. ``nano panah.pasopati.it38.com``
    ```
    ;
    ; BIND data file for local loopback interface
    ;
    $TTL    604800
    @       IN      SOA     panah.pasopati.it38.com. root.panah.pasopati.it38.com. (
                                  2         ; Serial
                             604800         ; Refresh
                              86400         ; Retry
                            2419200         ; Expire
                             604800 )       ; Negative Cache TTL
    ;
    @       IN      NS      panah.pasopati.it38.com.
    www     IN      CNAME   panah.pasopati.it38.com
    @       IN      A       10.82.2.5
    @       IN      AAAA    ::1
12. ``service bind9 restart``

#### Console Albert Einstein
13. ``ping panah.pasopati.it38.com`` <br>
![image](https://github.com/user-attachments/assets/61532a9d-05ab-409f-b387-b13ba6b41ff1)

## Soal 10
Markas juga meminta catatan kapan saja meme brain rot akan dijatuhkan, maka buatlah subdomain baru di subdomain panah yaitu log.panah.pasopati.xxxx.com serta aliasnya www.log.panah.pasopati.xxxx.com yang juga mengarah ke Kotalingga.
#### Console Majapahit
1. ``cd /etc/bind``
2. ``nano named.conf.local``
    ```
    zone "log.panah.pasopati.it38.com" {
            type master;
            file "/etc/bind/panah/log.panah.pasopati.it38.com";
    };
3. ``cd panah``
4. ``nano log.panah.pasopati.it17.com``
    ```
    ;
    ; BIND data file for local loopback interface
    ;
    $TTL    604800
    @       IN      SOA     panah.pasopati.it38.com. root.panah.pasopati.it38.com. (
                                  2         ; Serial
                             604800         ; Refresh
                              86400         ; Retry
                            2419200         ; Expire
                             604800 )       ; Negative Cache TTL
    ;
    @       IN      NS      log.panah.pasopati.it38.com.
    @       IN      A       10.82.2.5
    @       IN      AAAA    ::1
    www     IN      CNAME   panah.pasopati.it38.com.
5. ``service bind9 restart``

#### Console Albert Einstein
6. ``ping log.panah.pasopati.it38.com`` <br>
![image](https://github.com/user-attachments/assets/98c030f1-169a-4f40-9378-4fe000ce7a3e)

## Soal 11
Setelah pertempuran mereda, warga IT dapat kembali mengakses jaringan luar dan menikmati meme brainrot terbaru, tetapi hanya warga Majapahit saja yang dapat mengakses jaringan luar secara langsung. Buatlah konfigurasi agar warga IT yang berada diluar Majapahit dapat mengakses jaringan luar melalui DNS Server Majapahit.
1. ``Hapus line nameserver 192.168.122.1 di /etc/resolv.conf di salah satu nodes kecuali Majapahit dan Nusantara``

#### Console Majapahit
2. ``cd /etc/bind``
3. ``nano named.conf.options`` <br>
![image](https://github.com/user-attachments/assets/ce2bec9a-99a8-4246-8522-5cf3945e9001)
4. ``service bind9 restart``

#### Console Bebas (tidak ada nameserver 192.168.122.1)
5. ``ping x.com`` <br>
![image](https://github.com/user-attachments/assets/31f21664-77d2-4ad2-924a-18db914bcfde)

## Soal 12
Karena pusat ingin sebuah laman web yang ingin digunakan untuk memantau kondisi kota lainnya maka deploy laman web ini (cek resource yg lb) pada Kotalingga menggunakan apache.
#### Console Kotalingga
1. ``apt-get update && apt-get install apache2 libapache2-mod-php7.0 php php-mcrypt php-mysql wget unzip lynx -y``
2. ``cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/pasopati.it38.com.conf``
3. ``nano /etc/apache2/mods-enabled/dir.conf`` <br>
    ```
    <IfModule mod_dir.c>
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
    </IfModule>'
4. ``nano /etc/apache2/sites-available/it22.conf``
    ```
   <VirtualHost *:80>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/it38
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>'
5. ``a2ensite it38``
6. ``mkdir -p /var/www/it38``
7. ``wget --no-check-certificate 'https://docs.google.com/uc?export=download&id=1xn03kTB27K872cokqwEIlk8Zb121HnfB' -O /tmp/lb.zip``
8. ``unzip -o /tmp/lb.zip -d /tmp``
9. ``mv /tmp/worker/* /var/www/it38/ -f``
10. ``a2dissite 000-default.conf``
11. ``service apache2 restart``
12. ``lynx http://localhost`` <br>
![image](https://github.com/user-attachments/assets/6f0ed969-c592-4446-b032-0964cbcf1c29)

## Soal 13
Karena Sriwijaya dan Majapahit memenangkan pertempuran ini dan memiliki banyak uang dari hasil penjarahan (sebanyak 35 juta, belum dipotong pajak) maka pusat meminta kita memasang load balancer untuk membagikan uangnya pada web nya, dengan Kotalingga, Bedahulu, Tanjungkulai sebagai worker dan Solok sebagai Load Balancer menggunakan apache sebagai web server nya dan load balancer nya.
#### Console Solok
1. ``apt-get update && apt-get install apache2 -y``
2. ``a2enmod proxy proxy_balancer proxy_http lbmethod_byrequests lbmethod_bytraffic lbmethod_bybusyness rewrite``
3. ``nano /etc/apache2/sites-available/000-default.conf``
    ```
   <VirtualHost *:80>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/it38
    
        <Proxy "balancer://mycluster">
            BalancerMember http://10.82.2.5 loadfactor=1
            BalancerMember http://10.82.2.4 loadfactor=1
            BalancerMember http://10.82.2.3 loadfactor=1
        </Proxy>
    
        ProxyPass "/" "balancer://mycluster/"
        ProxyPassReverse "/" "balancer://mycluster/"
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>
4. ``service apache2 restart``
5. ``lynx http://localhost`` <br>
![image](https://github.com/user-attachments/assets/444a440a-cfc3-401e-abb3-d50451d8548a)

## Soal 14
Selama melakukan penjarahan mereka melihat bagaimana web server luar negeri, hal ini membuat mereka iri, dengki, sirik dan ingin flexing sehingga meminta agar web server dan load balancer nya diubah menjadi nginx.

## Soal 15
Markas pusat meminta laporan hasil benchmark dengan menggunakan apache benchmark dari load balancer dengan 2 web server yang berbeda tersebut dan meminta secara detail dengan ketentuan:
Nama Algoritma Load Balancer
Report hasil testing apache benchmark 
Grafik request per second untuk masing masing algoritma. 
Analisis
Meme terbaik kalian (terserah ( ͡° ͜ʖ ͡°)) 🤓

## Soal 16
Karena dirasa kurang aman dari brainrot karena masih memakai IP, markas ingin akses ke Solok memakai solok.xxxx.com dengan alias www.solok.xxxx.com (sesuai web server terbaik hasil analisis kalian).

## Soal 17
Agar aman, buatlah konfigurasi agar solok.xxx.com hanya dapat diakses melalui port sebesar π x 10^4 = (phi nya desimal) dan 2000 + 2000 log 10 (10) +700 - π = ?.

## Soal 18
Apa bila ada yang mencoba mengakses IP solok akan secara otomatis dialihkan ke www.solok.xxxx.com.

## Soal 19
Karena probset sudah kehabisan ide masuk ke salah satu worker buatkan akses direktori listing yang mengarah ke resource worker2.

## Soal 20
Worker tersebut harus dapat di akses dengan sekiantterimakasih.xxxx.com dengan alias www.sekiantterimakasih.xxxx.com.
