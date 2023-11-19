# Jarkom-Modul-3-B05-2023

## Praktikum Jarkom Modul 3
Group Members:
| NRP | Name |
| ------ | ------ |
|5025211028|Keysa Anadea Aqiva Ajie|
|5025221202|Hilmy Septian Nursyekha|

## Configuration

#### Aura
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.11.1.0
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 10.11.2.0
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 10.11.3.0
	netmask 255.255.255.0

auto eth4
iface eth4 inet static
	address 10.11.4.0
	netmask 255.255.255.0
```
#### Himmel
```
auto eth0
iface eth0 inet static
	address 10.11.1.1
	netmask 255.255.255.0
	gateway 10.11.1.0
```
#### Heiter
```
auto eth0
iface eth0 inet static
	address 10.11.1.2
	netmask 255.255.255.0
	gateway 10.11.1.0
```
#### Denken
```
auto eth0
iface eth0 inet static
	address 10.11.2.1
	netmask 255.255.255.0
	gateway 10.11.2.0
```
#### Eisen
```
auto eth0
iface eth0 inet static
	address 10.11.2.2
	netmask 255.255.255.0
	gateway 10.11.2.0
```
#### Lawine
```
auto eth0
iface eth0 inet static
	address 10.11.3.3
	netmask 255.255.255.0
	gateway 10.11.3.0
```
#### Linie
```
auto eth0
iface eth0 inet static
	address 10.11.3.2
	netmask 255.255.255.0
	gateway 10.11.3.0
```
#### Lugner
```
auto eth0
iface eth0 inet static
	address 10.11.3.1
	netmask 255.255.255.0
	gateway 10.11.3.0
```
#### Frieren
```
auto eth0
iface eth0 inet static
	address 10.11.4.3
	netmask 255.255.255.0
	gateway 10.11.4.0
```
#### Flamme
```
auto eth0
iface eth0 inet static
	address 10.11.4.2
	netmask 255.255.255.0
	gateway 10.11.4.0
```
#### Fern
```
auto eth0
iface eth0 inet static
	address 10.11.4.1
	netmask 255.255.255.0
	gateway 10.11.4.0
```
#### Sein, Stark, Revolte, dan Richter
```
auto eth0
iface eth0 inet dhcp
```

Masukkan command-command berikut ke dalam setiap node menggunakan `.bashrc` menggunakan `nano`
#### Heiter
```
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt-get install bind9 -y
```
#### Himmel
```
echo 'nameserver 10.11.1.2' > /etc/resolv.conf   
apt-get update
apt install isc-dhcp-server -y
```
#### Aura
```
apt-get update
apt install isc-dhcp-relay -y
```
#### Denken
```
echo 'nameserver 10.11.1.2' > /etc/resolv.conf
apt-get update
apt-get install mariadb-server -y
service mysql start
```
#### Eisen
```
echo 'nameserver 10.11.1.2' > /etc/resolv.conf
apt-get update
apt-get install apache2-utils -y
apt-get install nginx -y
apt-get install lynx -y

service nginx start
```
#### Lawine, Linie, dan Lugner
```
echo 'nameserver 10.11.1.2' > /etc/resolv.conf
apt-get update
apt-get install nginx -y
apt-get install wget -y
apt-get install unzip -y
apt-get install lynx -y
apt-get install htop -y
apt-get install apache2-utils -y
apt-get install php7.3-fpm php7.3-common php7.3-mysql php7.3-gmp php7.3-curl php7.3-intl php7.3-mbstring php7.3-xmlrpc php7.3-gd php7.3-xml php7.3-cli php7.3-zip -y

service nginx start
service php7.3-fpm start
```
#### Frieren, Flamme, dan Fern
```
echo 'nameserver 10.11.1.2' > /etc/resolv.conf
apt-get update
apt-get install lynx -y
apt-get install mariadb-client -y

apt-get install php8.0-mbstring php8.0-xml php8.0-cli   php8.0-common php8.0-intl php8.0-opcache php8.0-readline php8.0-mysql php8.0-fpm php8.0-curl unzip wget -y
apt-get install nginx -y

service nginx start
service php8.0-fpm start
```
#### Sein, Stark, Revolte, dan Richter
```
apt update
apt install lynx -y
apt install htop -y
apt install apache2-utils -y
apt-get install jq -y
```


## No 1
Lakukan konfigurasi sesuai dengan peta yang sudah diberikan!

### Lugner (PHP Worker)
```
auto eth0
iface eth0 inet static
	address 10.11.3.1
	netmask 255.255.255.0
	gateway 10.11.3.0
```
### Fern (Laravel Worker)
```
auto eth0
iface eth0 inet static
	address 10.11.4.1
	netmask 255.255.255.0
	gateway 10.11.4.0
```
Selanjutnya pada DNS Server (Heiter), kita perlu menjalankan command dibawah ini
### Script
```
echo 'zone "riegel.canyon.b05.com" {
    type master;
    file "/etc/bind/sites/riegel.canyon.b05.com";
};

zone "granz.channel.b05.com" {
    type master;
    file "/etc/bind/sites/granz.channel.b05.com";
};

zone "1.11.10.in-addr.arpa" {
    type master;
    file "/etc/bind/sites/1.11.10.in-addr.arpa";
};' > /etc/bind/named.conf.local

mkdir -p /etc/bind/sites
cp /etc/bind/db.local /etc/bind/sites/riegel.canyon.b05.com
cp /etc/bind/db.local /etc/bind/sites/granz.channel.b05.com
cp /etc/bind/db.local /etc/bind/sites/1.11.10.in-addr.arpa

echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     riegel.canyon.b05.com. root.riegel.canyon.b05.com. (
                        2023111401      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      riegel.canyon.b05.com.
@       IN      A       10.11.4.6     ; IP Fern
www     IN      CNAME   riegel.canyon.b05.com.' > /etc/bind/sites/riegel.canyon.a09.com

echo '
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     granz.channel.b05.com. root.granz.channel.b05.com. (
                        2023111401      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      granz.channel.b05.com.
@       IN      A       10.11.3.6     ; IP Lugner
www     IN      CNAME   granz.channel.b05.com.' > /etc/bind/sites/granz.channel.b05.com

echo 'options {
      directory "/var/cache/bind";

      forwarders {
              192.168.122.1;
      };

      // dnssec-validation auto;
      allow-query{any;};
      auth-nxdomain no;    # conform to RFC1035
      listen-on-v6 { any; };
}; ' >/etc/bind/named.conf.options

service bind9 start
```
### Hasil
<img width="501" alt="Cuplikan layar 2023-11-16 182749" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/95b7a120-28fd-4f76-8fb4-3968cb4cd027">


## NO 2
Semua CLIENT harus menggunakan konfigurasi dari DHCP Server. Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.16 - [prefix IP].3.32 dan [prefix IP].3.64 - [prefix IP].3.80

### Script

```
echo 'subnet 10.11.1.0 netmask 255.255.255.0 {
}

subnet 10.11.2.0 netmask 255.255.255.0 {
}

subnet 10.11.3.0 netmask 255.255.255.0 {
    range 10.11.3.16 10.11.3.32;
    range 10.11.3.64 10.11.3.80;
    option routers 10.11.3.0;
}' > /etc/dhcp/dhcpd.conf
```

## NO 3
Client yang melalui Switch4 mendapatkan range IP dari [prefix IP].4.12 - [prefix IP].4.20 dan [prefix IP].4.160 - [prefix IP].4.168.

### Script
```
echo 'subnet 10.11.1.0 netmask 255.255.255.0 {
}

subnet 10.11.2.0 netmask 255.255.255.0 {
}

subnet 10.11.3.0 netmask 255.255.255.0 {
    range 10.11.3.16 10.11.3.32;
    range 10.11.3.64 10.11.3.80;
    option routers 10.11.3.0;
}

subnet 10.11.4.0 netmask 255.255.255.0 {
    range 10.11.4.12 10.11.4.20;
    range 10.11.4.160 10.11.4.168;
    option routers 10.11.4.0;
} ' > /etc/dhcp/dhcpd.conf
```

## NO 4
Client mendapatkan DNS dari Heiter dan dapat terhubung dengan internet melalui DNS tersebut

### Script
```
subnet 10.11.3.0 netmask 255.255.255.0 {
    ...
    option broadcast-address 10.11.3.255;
    option domain-name-servers 10.11.1.2;
    ...
}

subnet 10.11.4.0 netmask 255.255.255.0 {
    option broadcast-address 10.11.4.255;
    option domain-name-servers 10.11.1.2;
} 
```
lalu gunakan shell sebagai berikut
```
echo 'subnet 10.11.1.0 netmask 255.255.255.0 {
}

subnet 10.11.2.0 netmask 255.255.255.0 {
}

subnet 10.11.3.0 netmask 255.255.255.0 {
    range 10.11.3.16 10.11.3.32;
    range 10.11.3.64 10.11.3.80;
    option routers 10.11.3.0;
    option broadcast-address 10.11.3.255;
    option domain-name-servers 10.11.1.2;
}

subnet 10.11.4.0 netmask 255.255.255.0 {
    range 10.11.4.12 10.11.4.20;
    range 10.11.4.160 10.11.4.168;
    option routers 10.11.4.0;
    option broadcast-address 10.11.4.255;
    option domain-name-servers 10.11.1.2;
} ' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server start
```
Command berikut pada Aura
```
echo '# Defaults for isc-dhcp-relay initscript
# sourced by /etc/init.d/isc-dhcp-relay
# installed at /etc/default/isc-dhcp-relay by the maintainer scripts

#
#This is a POSIX shell fragment
#

# What servers should the DHCP relay forward requests to?
SERVERS="10.1q.1.1"

# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
INTERFACES="eth1 eth2 eth3 eth4"

# Additional options that are passed to the DHCP relay daemon?
OPTIONS=""' > /etc/default/isc-dhcp-relay

service isc-dhcp-relay start 
```
Lalu pada file `/etc/sysctl.conf` lakukan uncommented pada `net.ipv4.ip_forward=1`
### Hasil
<img width="398" alt="Cuplikan layar 2023-11-19 204422" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/92ae8733-ad6c-4441-bcfc-3060e39e4ecf">

## NO 5
Kita dapat menjalankan command berikut pada DHCP Server
```
echo 'subnet 10.11.1.0 netmask 255.255.255.0 {
}

subnet 10.11.2.0 netmask 255.255.255.0 {
}

subnet 10.11.3.0 netmask 255.255.255.0 {
    range 10.11.3.16 10.11.3.32;
    range 10.11.3.64 10.11.3.80;
    option routers 10.11.3.0;
    option broadcast-address 10.11.3.255;
    option domain-name-servers 10.11.1.2;
    default-lease-time 180;
    max-lease-time 5760;
}

subnet 10.11.4.0 netmask 255.255.255.0 {
    range 10.11.4.12 10.11.4.20;
    range 10.11.4.160 10.11.4.168;
    option routers 10.11.4.0;
    option broadcast-address 10.11.4.255;
    option domain-name-servers 10.11.1.2;
    default-lease-time 720;
    max-lease-time 5760;
} ' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```
### Hasil
<img width="428" alt="Cuplikan layar 2023-11-19 193140" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/cb866b14-7eff-4970-93c8-bcee266ebef5">
<img width="434" alt="Cuplikan layar 2023-11-19 193212" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/90c53639-bec5-4070-9c28-9572715c037a">

## NO 6
Untuk melakukan konfigurasi tambahan sebagai berikut untuk melakukan download dan unzip menggunakan command `wget`

```
wget -O '/var/www/granz.channel.b05.com' 'https://drive.google.com/u/0/uc?id=1ViSkRq7SmwZgdK64eRbr5Fm1EGCTPrU1&export=download'
unzip -o /var/www/granz.channel.b05.com -d /var/www/
rm /var/www/granz.channel.b05.com
mv /var/www/modul-3 /var/www/granz.channel.b05.com
```
### Script

melakukan konfigurasi pada `nginx`
```
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/granz.channel.b05.com
ln -s /etc/nginx/sites-available/granz.channel.b05.com /etc/nginx/sites-enabled/
rm /etc/nginx/sites-enabled/default

echo 'server {
    listen 80;
    server_name _;

    root /var/www/granz.channel.b05.com;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.3-fpm.sock;  # Sesuaikan versi PHP dan socket
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}' > /etc/nginx/sites-available/granz.channel.b05.com

service nginx restart
```
### Hasil
<img width="539" alt="Cuplikan layar 2023-11-19 200456" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/163c2816-e297-4517-997b-d162fcc600b2">

## NO 7
Kepala suku dari Bredt Region memberikan resource server sebagai berikut: Lawine, 4GB, 2vCPU, dan 80 GB SSD. Linie, 2GB, 2vCPU, dan 50 GB SSD. Lugner 1GB, 1vCPU, dan 25 GB SSD. Aturlah agar Eisen dapat bekerja dengan maksimal, lalu lakukan testing dengan 1000 request dan 100 request/second.

Lakukan konfigurasi `Load Balancing` pada node `Eisen` sebagai berikut.
Buka kembali Node DNS Server dan arahkan domain tersebut pada IP `Load Balancer Eise`

### Script
```
echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     riegel.canyon.b05.com. root.riegel.canyon.b05.com. (
                        2023111401      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      riegel.canyon.b05.com.
@       IN      A       10.11.2.2     ; IP LB Eiken
www     IN      CNAME   riegel.canyon.b05.com.' > /etc/bind/sites/riegel.canyon.b05.com

echo '
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     granz.channel.b05.com. root.granz.channel.b05.com. (
                        2023111401      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      granz.channel.b05.com.
@       IN      A       10.11.2.2     ; IP LB Eiken
www     IN      CNAME   granz.channel.b05.com.' > /etc/bind/sites/granz.channel.b05.com
```
Lalu kembali ke node Eisen dan lakukan konfigurasi pada nginx sebagai berikut
```
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/lb_php

echo ' upstream worker {
    server 10.11.3.1;
    server 10.11.3.2;
    server 10.11.3.3;
}

server {
    listen 80;
    server_name granz.channel.b05.com www.granz.channel.b05.com;

    root /var/www/html;

    index index.html index.htm index.nginx-debian.html;

    server_name _;

    location / {
        proxy_pass http://worker;
    }
} ' > /etc/nginx/sites-available/lb_php

ln -s /etc/nginx/sites-available/lb_php /etc/nginx/sites-enabled/
rm /etc/nginx/sites-enabled/default

service nginx restart
```
Setelah melakukan setup, Jalankan perintah berikut pada client Revolte

```
ab -n 1000 -c 100 http://www.granz.channel.b05.com/
```

### Hasil





## NO 8
Karena diminta untuk menuliskan grimoire, buatlah analisis hasil testing dengan 200 request dan 10 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut: 1. Nama Algoritma Load Balancer; 2. Report hasil testing pada Apache Benchmark; 3.Grafik request per second untuk masing masing algoritma.

### Script
Jalankan perintah berikut pada client Revolte
```
ab -n 200 -c 10 http://www.granz.channel.b05.com/ 
```

### Hasil
#### Round Robin
<img width="412" alt="Cuplikan layar 2023-11-19 210413" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/63d71a75-bd08-4a16-977d-4287628f54e5">
<img width="402" alt="Cuplikan layar 2023-11-19 210435" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/53823f09-9a76-4788-a3c6-33d0dbbd6838">

#### Least Cont
<img width="409" alt="Cuplikan layar 2023-11-19 210512" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/845de39a-f67b-470c-887a-6767eab06dc7">
<img width="404" alt="Cuplikan layar 2023-11-19 210526" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/39cb3590-2f60-4c65-af20-861fc827fb49">


#### IP Hash
<img width="410" alt="Cuplikan layar 2023-11-19 210547" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/ca191667-e70a-463b-9598-afd5dfac1709">
<img width="407" alt="Cuplikan layar 2023-11-19 210559" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/88ce2c6a-d373-45af-af59-d7feddb8397b">


#### Generic Hash
<img width="406" alt="Cuplikan layar 2023-11-19 210649" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/2a496e54-6fa8-4a46-b0ee-e6f0a5d8afa6">
<img width="407" alt="Cuplikan layar 2023-11-19 210704" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/0b6a4229-e1d4-46b6-8c2a-fa4243972841">

## NO 9
Dengan menggunakan algoritma Round Robin, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 100 request dengan 10 request/second, kemudian tambahkan grafiknya pada grimoire.

### Script
Jalankan perintah berikut pada client Revolte
```
ab -n 100 -c 10 http://www.granz.channel.b05.com/ 
```

### Hasil

#### 3 Worker
<img width="407" alt="Cuplikan layar 2023-11-19 210749" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/4c7e0566-fe24-4895-9d20-8e116ca4d2fe">
<img width="406" alt="Cuplikan layar 2023-11-19 210800" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/21c03c54-f46e-47da-884e-e914c811254f">

#### 2 Worker
<img width="400" alt="Cuplikan layar 2023-11-19 211404" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/17ea57c2-3052-4e70-a31e-0f136a80bcc8">
<img width="406" alt="Cuplikan layar 2023-11-19 211417" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/8f953864-5f4c-424d-a5a9-1bd9cef22616">

#### 1 Worker
<img width="406" alt="Cuplikan layar 2023-11-19 211439" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/633111d2-3446-433b-910b-38db2edbaff5">
<img width="405" alt="Cuplikan layar 2023-11-19 211545" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/3fa10590-3298-4053-a496-5d6d73c1c1d2">

## NO 10
Selanjutnya coba tambahkan konfigurasi autentikasi di Load Balancer dengan dengan kombinasi username: “netics” dan password: “ajkyyy”, dengan yyy merupakan kode kelompok. Terakhir simpan file “htpasswd” nya di /etc/nginx/rahasisakita/.

 Lakukan beberapa konfigurasi 

 ### Script
 
 ```
mkdir /etc/nginx/rahasisakita
htpasswd -c /etc/nginx/rahasisakita/htpasswd netics ajkb05
```
dengan memasukkan password `ajkb05`.

Setelah memasukkan `password` dan menulis ulangnya, tambahkan command berikut pada setup `nginx`.

```
echo ' upstream worker {
    server 10.11.3.1;
    server 10.11.3.2;
    server 10.11.3.3;
}

server {
    listen 80;
    server_name granz.channel.b05.com www.granz.channel.b05.com;

    root /var/www/html;

    index index.html index.htm index.nginx-debian.html;

    server_name _;

    location / {
        proxy_pass http://worker;
auth_basic "Restricted Content";
auth_basic_user_file /etc/nginx/rahasisakita/htpasswd;
    }
} ' > /etc/nginx/sites-available/lb_php

service nginx restart
```

### Hasil
<img width="409" alt="Cuplikan layar 2023-11-19 211635" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/a0581351-8153-4bd8-af20-e6a5ee25e431">
<img width="406" alt="Cuplikan layar 2023-11-19 211652" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/c8513144-7f3e-4ba0-a8de-c70d3638e73c">
<img width="409" alt="Cuplikan layar 2023-11-19 211706" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/848af814-ce0e-490f-bb21-d0e6fe7bd246">
<img width="409" alt="Cuplikan layar 2023-11-19 211719" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/277b1fa4-55bd-4aef-af4c-259ce9fbaef4">

## NO 11
Lalu buat untuk setiap request yang mengandung /its akan di proxy passing menuju halaman https://www.its.ac.id. (11) hint: (proxy_pass).

 Lakukan beberapa konfigurasi tambahan pada nginx sebagai berikut

 ### Script
```
location ~ /its {
    proxy_pass https://www.its.ac.id;
    proxy_set_header Host www.its.ac.id;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}
 ```
dan juga
```
echo ' upstream worker {
    server 10.11.3.1;
    server 10.11.3.2;
    server 10.11.3.3;
}

server {
    listen 80;
    server_name granz.channel.b05.com www.granz.channel.b05.com;

    root /var/www/html;

    index index.html index.htm index.nginx-debian.html;

    server_name _;

    location / {
        proxy_pass http://worker;
auth_basic "Restricted Content";
auth_basic_user_file /etc/nginx/rahasisakita/htpasswd;
    }
 location ~ /its {
        proxy_pass https://www.its.ac.id;
        proxy_set_header Host www.its.ac.id;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}' > /etc/nginx/sites-available/lb_php
service nginx  restart 
```
Lakukan testing pada client Revolte dengan menggunakan perintah berikut
```
lynx www.granz.channel.b05.com/its
```

### Hasil
<img width="416" alt="Cuplikan layar 2023-11-19 211755" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/751b237a-7f3e-4732-9a3e-0dd3ec0147fe">


## NO 12
Selanjutnya Load Balancer ini hanya boleh diakses oleh client dengan IP [Prefix IP].3.69, [Prefix IP].3.70, [Prefix IP].4.167, dan [Prefix IP].4.168.

Menambahkan beberapa konfigurasi berikut di `nginx` 

### Script

```
echo 'upstream worker {
    server 10.11.3.1;
    server 10.11.3.2;
    server 10.11.3.3;
}

server {
    listen 80;
    server_name granz.channel.b05.com www.granz.channel.b05.com;

    root /var/www/html;
    index index.html index.htm index.nginx-debian.html;

    location / {
        allow 10.11.3.69;
        allow 10.11.3.70;
        allow 10.11.4.167;
        allow 10.11.4.168;
        deny all;
        proxy_pass http://worker;
    }

    location ~ /its {
        proxy_pass https://www.its.ac.id;
        proxy_set_header Host www.its.ac.id;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}' > /etc/nginx/sites-available/lb_php

service nginx restart
```

## NO 13
Semua data yang diperlukan, diatur pada Denken dan harus dapat diakses oleh Frieren, Flamme, dan Fern.

Buka Database Server nya yaitu `Denken` kemudian lakukan konfigurasi sebagai berikut

### Script

```
# Db akan diakses oleh 3 worker, maka 
echo '# This group is read both by the client and the server
# use it for options that affect everything
[client-server]

# Import all .cnf files from configuration directory
!includedir /etc/mysql/conf.d/
!includedir /etc/mysql/mariadb.conf.d/

# Options affecting the MySQL server (mysqld)
[mysqld]
skip-networking=0
skip-bind-address
' > /etc/mysql/my.cnf
```
mengganti `[bind-address]` pada file `/etc/mysql/mariadb.conf.d/50-server.cnf` menjadi `0.0.0.0`
```
cd /etc/mysql/mariadb.conf.d/50-server.cnf

# Changes
bind-address            = 0.0.0.0
```
Kemudian, lakukan beberapa perintah berikut
```
service mysql start
mysql -u root -p
Enter password: 

CREATE USER 'kelompokb05'@'%' IDENTIFIED BY 'passwordb05';
CREATE USER 'kelompokb05'@'localhost' IDENTIFIED BY 'passwordb05';
CREATE DATABASE dbkelompokb05;
GRANT ALL PRIVILEGES ON *.* TO 'kelompokb05'@'%';
GRANT ALL PRIVILEGES ON *.* TO 'kelompokb05'@'localhost';
FLUSH PRIVILEGES;
```

### Hasil
#### Denken
<img width="409" alt="Cuplikan layar 2023-11-19 211901" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/5c2047cf-5f43-414b-8740-f37f05abd0c6">
<img width="409" alt="Cuplikan layar 2023-11-19 211936" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/b0dc18da-3e76-4013-bd5c-0424f5d91e8e">

#### Fern
<img width="408" alt="Cuplikan layar 2023-11-19 212043" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/d6179e74-ddfc-44e6-89a9-7c9f85f4d940">

## NO 14
Frieren, Flamme, dan Fern memiliki Granz Channel sesuai dengan quest guide berikut. Jangan lupa melakukan instalasi PHP8.0 dan Composer.

### Script
Install composer
```
wget https://getcomposer.org/download/2.0.13/composer.phar
chmod +x composer.phar
mv composer.phar /usr/local/bin/composer
```
Install `git` dan lakukan clonning
```
apt-get install git -y
cd /var/www && git clone https://github.com/martuafernando/laravel praktikum-jarkom
cd /var/www/laravel-praktikum-jarkom && composer update
```

Lakukan konfigurasi sebagai berikut pada masing-masing worker
```

cd /var/www/laravel-praktikum-jarkom && cp .env.example .env
echo 'APP_NAME=Laravel
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=192.173.2.1
DB_PORT=3306
DB_DATABASE=dbkelompokb05
DB_USERNAME=kelompokb05
DB_PASSWORD=passwordab05

BROADCAST_DRIVER=log
CACHE_DRIVER=file
FILESYSTEM_DISK=local
QUEUE_CONNECTION=sync
SESSION_DRIVER=file
SESSION_LIFETIME=120

MEMCACHED_HOST=127.0.0.1

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_MAILER=smtp
MAIL_HOST=mailpit
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=
AWS_USE_PATH_STYLE_ENDPOINT=false

PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
PUSHER_HOST=
PUSHER_PORT=443
PUSHER_SCHEME=https
PUSHER_APP_CLUSTER=mt1

VITE_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
VITE_PUSHER_HOST="${PUSHER_HOST}"
VITE_PUSHER_PORT="${PUSHER_PORT}"
VITE_PUSHER_SCHEME="${PUSHER_SCHEME}"
VITE_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"' > /var/www/laravel-praktikum-jarkom/.env
cd /var/www/laravel-praktikum-jarkom && php artisan key:generate
cd /var/www/laravel-praktikum-jarkom && php artisan config:cache
cd /var/www/laravel-praktikum-jarkom && php artisan migrate
cd /var/www/laravel-praktikum-jarkom && php artisan db:seed
cd /var/www/laravel-praktikum-jarkom && php artisan storage:link
cd /var/www/laravel-praktikum-jarkom && php artisan jwt:secret
cd /var/www/laravel-praktikum-jarkom && php artisan config:clear
chown -R www-data.www-data /var/www/laravel-praktikum-jarkom/storage

echo 'server {
    listen 8001;

    root /var/www/laravel-praktikum-jarkom/public;

    index index.php index.html index.htm;
    server_name _;

    location / {
            try_files $uri $uri/ /index.php?$query_string;
    }

    # pass PHP scripts to FastCGI server
    location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/var/run/php/php8.0-fpm.sock;
    }

location ~ /\.ht {
            deny all;
    }

    error_log /var/log/nginx/implementasi_error.log;
    access_log /var/log/nginx/implementasi_access.log;
}
' > /etc/nginx/sites-available/laravel-worker
ln -s /etc/nginx/sites-available/laravel-worker /etc/nginx/sites-enabled/
chown -R www-data.www-data /var/www/laravel-praktikum-jarkom/storage
service php8.0-fpm restart
service nginx restart
```
Lakukan konfigurasi `nginx` sebagai berikut pada masing-masing worker dan sesuaikan portnya
```
10.11.4.1:8001; # Fern 
10.11.4.2:8002; # Flamme
10.11.4.3:8003; # Frieren
```
konfigurasi `nginx`
```
echo 'server {
    listen <X>;

    root /var/www/laravel-praktikum-jarkom/public;

    index index.php index.html index.htm;
    server_name _;

    location / {
            try_files $uri $uri/ /index.php?$query_string;
    }

    # pass PHP scripts to FastCGI server
    location ~ \.php$ {
      include snippets/fastcgi-php.conf;
      fastcgi_pass unix:/var/run/php/php8.0-fpm.sock;
    }

    location ~ /\.ht {
            deny all;
    }

    error_log /var/log/nginx/implementasi_error.log;
    access_log /var/log/nginx/implementasi_access.log;
}' > /etc/nginx/sites-available/laravel-worker
```
Lakukan testing pada worker
```
lynx localhost:[PORT]
```

### Hasil
<img width="410" alt="Cuplikan layar 2023-11-19 212116" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/08097069-de15-4c00-af9c-e8365262ae4d">

## NO 15
Granz Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire. Untuk POST /api/auth/register.

Perlu dilakukan pengujian dengan `Apache Benchmark` pada salah satu `worker`. Beberapa `worker` Laravel, yaitu Fern, untuk diuji oleh klien `Revolte`. Sebelum testing, kami menggunakan file `.json` sebagai bantuan, yang akan berfungsi sebagai `body` yang dikirim ke endpoint `/api/auth/register`. Berikut adalah rinciannya:

### Script
```
echo '
{
  "username": "kelompokb05",
  "password": "passwordb05"
}' > register_data.json
```
Lakukan testing pada `Revolte` dengan
```
ab -n 100 -c 10 -T 'application/json' -p register_data.json -g register_results2.data http://10.11.4.1:8001/api/auth/register
```

### Hasil
<img width="341" alt="Cuplikan layar 2023-11-19 212216" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/0539a8df-d0e4-4380-8813-63ddcb9a3f6d">
<img width="339" alt="Cuplikan layar 2023-11-19 212227" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/e34fa82f-532b-4982-813d-654bd43d9e2b">

## NO 16
Granz Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire. Untuk POST /api/auth/login.


Diperlukan pengujian menggunakan `Apache Benchmark` pada satu worker tertentu.  Yang akan digunakan adalah worker Laravel, yaitu `Fern`, yang akan diuji oleh klien `Revolte`. Sebelum memulai pengujian, kami menggunakan bantuan file `.json` sebagai `body` yang akan dikirim ke endpoint `/api/auth/login`.

### Script
```
echo '
{
  "username": "kelompokb05",
  "password": "passwordb05"
}' > login_data.json
```
Lakukan testing pada `Revolte`
```
ab -n 100 -c 10 -T 'application/json' -p register_data.json -g register_results2.data http://10.11.4.1:8001/api/auth/login
```

### Hasil
<img width="340" alt="Cuplikan layar 2023-11-19 212247" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/8a5e3240-9888-417f-83c7-04d53bb1d678">

## NO 17
Granz Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire. Untuk GET /api/me.

Lakukan testing menggunakan `Apache Benchmark` pada salah satu worker, yaitu `Fern` yang akan ditesting oleh `Revolte`.

### Script
Dapatkan tokennya terlebih dahulu sebelum mengakses endpoint `/api/me`
```
curl -X POST -H "Content-Type: application/json" -d @register_data.json http://10.11.4.1:8001/api/auth/login > login_output.txt
```
Kemudian run command berikut untuk set `token`
```
token=$(cat login_output.txt | jq -r '.token')
```
Lalu, run command berikut unruk testing
```
ab -n 100 -c 10 -H "Authorization: Bearer $token" http://10.11.4.1:8001/api/me
```

### Hasil
<img width="339" alt="Cuplikan layar 2023-11-19 212310" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/7493ca84-7db6-4037-8354-8005118d06e9">
<img width="397" alt="Cuplikan layar 2023-11-19 212339" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/7dc7e71d-7987-4cbe-9673-b1eb27859b9d">
<img width="409" alt="Cuplikan layar 2023-11-19 212354" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/b52dd710-ceca-4100-9ee1-546a1ce0aab1">

## NO 18
Untuk memastikan ketiganya bekerja sama secara adil untuk mengatur Granz Channel maka implementasikan Proxy Bind pada Eisen untuk mengaitkan IP dari Frieren, Flamme, dan Fern.

Gunakan implementasi dari Load Balancing karena sesuai dengan definisi nya yaitu keseimbangan beban kerja. Maka dari itu, berikut merupakan konfigurasi `nginx`

### Script
```
echo 'upstream worker {
    server 10.11.4.1:8001;
    server 10.11.4.2:8002;
    server 10.11.4.3:8003;
}

server {
    listen 80;
    server_name riegel.canyon.b05.com www.riegel.canyon.b05.com;

    location / {
proxy_bind 192.177.2.2;
        proxy_pass http://worker;
    }
} 
' > /etc/nginx/sites-available/laravel-worker

ln -s /etc/nginx/sites-available/laravel-worker /etc/nginx/sites-enabled/laravel-worker

service nginx restart
```
Lakukan testing pada `Revolte
```
ab -n 100 -c 10 -p login_data.json -T application/json http://www.riegel.canyon.b05.com/api/auth/login
```

### Hasil
<img width="339" alt="Cuplikan layar 2023-11-19 212432" src="https://github.com/hilmy1509/Jarkom-Modul-3-B05-2023/assets/115638253/d3f257ab-3a61-4652-af19-71c4a4a3e375">

## NO 19
Untuk meningkatkan performa dari Worker, coba implementasikan PHP-FPM pada Frieren, Flamme, dan Fern. Untuk testing kinerja naikkan -> pm.max_children, pm.start_servers, pm.min_spare_servers, pm.max_spare_servers sebanyak tiga percobaan dan lakukan testing sebanyak 100 request dengan 10 request/second kemudian berikan hasil analisisnya pada Grimoire.

Terdapat 4 konfigurasi pada `package manager` untuk tiap `worker`

### Script
#### 1
```
# Setup Awal
echo '[www]
user = www-data
group = www-data
listen = /run/php/php8.0-fpm.sock
listen.owner = www-data
listen.group = www-data
php_admin_value[disable_functions] = exec,passthru,shell_exec,system
php_admin_flag[allow_url_fopen] = off

; Choose how the process manager will control the number of child processes.

pm = dynamic
pm.max_children = 5
pm.start_servers = 2
pm.min_spare_servers = 1
pm.max_spare_servers = 3' > /etc/php/8.0/fpm/pool.d/www.conf

service php8.0-fpm restart
```
#### 2
```
echo '[www]
user = www-data
group = www-data
listen = /run/php/php8.0-fpm.sock
listen.owner = www-data
listen.group = www-data
php_admin_value[disable_functions] = exec,passthru,shell_exec,system
php_admin_flag[allow_url_fopen] = off

; Choose how the process manager will control the number of child processes.

pm = dynamic
pm.max_children = 25
pm.start_servers = 5
pm.min_spare_servers = 3
pm.max_spare_servers = 10' > /etc/php/8.0/fpm/pool.d/www.conf

service php8.0-fpm restart
```
#### 3
```
echo '[www]
user = www-data
group = www-data
listen = /run/php/php8.0-fpm.sock
listen.owner = www-data
listen.group = www-data
php_admin_value[disable_functions] = exec,passthru,shell_exec,system
php_admin_flag[allow_url_fopen] = off

; Choose how the process manager will control the number of child processes.

pm = dynamic
pm.max_children = 50
pm.start_servers = 8
pm.min_spare_servers = 5
pm.max_spare_servers = 15' > /etc/php/8.0/fpm/pool.d/www.conf

service php8.0-fpm restart
```
#### 4
```
echo '[www]
user = www-data
group = www-data
listen = /run/php/php8.0-fpm.sock
listen.owner = www-data
listen.group = www-data
php_admin_value[disable_functions] = exec,passthru,shell_exec,system
php_admin_flag[allow_url_fopen] = off

; Choose how the process manager will control the number of child processes.

pm = dynamic
pm.max_children = 75
pm.start_servers = 10
pm.min_spare_servers = 5
pm.max_spare_servers = 20' > /etc/php/8.0/fpm/pool.d/www.conf

service php8.0-fpm restart
```

## NO 20
Nampaknya hanya menggunakan PHP-FPM tidak cukup untuk meningkatkan performa dari worker maka implementasikan Least-Conn pada Eisen. Untuk testing kinerja dari worker tersebut dilakukan sebanyak 100 request dengan 10 request/second. 

Karena konfigurasi sebelumnya pada setiap `worker`, khususnya pada `package manager`, tidak memberikan hasil yang memadai untuk meningkatkan kinerja `worker`, maka ditambahkan algoritma pada `load balancer` menggunakan metode `Least-connection`. Algoritma ini memberikan prioritas kepada node dengan beban kinerja paling rendah. Node master secara akurat mencatat beban dan kinerja dari setiap node, kemudian memberikan prioritas kepada yang memiliki beban terendah. Dengan demikian, diharapkan tidak ada server yang memiliki beban kinerja yang rendah.

### Script
```
echo 'upstream worker {
    least_conn;
    server 10.11.4.1:8001;
    server 10.11.4.2:8002;
    server 10.11.4.3:8003;
}

server {
    listen 80;
    server_name riegel.canyon.a09.com www.riegel.canyon.a09.com;

    location / {
        proxy_pass http://worker;
    }
} 
' > /etc/nginx/sites-available/laravel-worker

service nginx restart
```
