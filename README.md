# Jarkom-Modul-3-B05-2023

## Configuration

#### Aura
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.11.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 10.11.2.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 10.11.3.1
	netmask 255.255.255.0

auto eth4
iface eth4 inet static
	address 10.11.4.1
	netmask 255.255.255.0
```
#### Himmel
```
auto eth0
iface eth0 inet static
	address 10.11.1.2
	netmask 255.255.255.0
	gateway 10.11.1.1
```
#### Heiter
```
auto eth0
iface eth0 inet static
	address 10.11.1.3
	netmask 255.255.255.0
	gateway 10.11.1.1
```
#### Denken
```
auto eth0
iface eth0 inet static
	address 10.11.2.2
	netmask 255.255.255.0
	gateway 10.11.2.1
```
#### Eisen
```
auto eth0
iface eth0 inet static
	address 10.11.2.3
	netmask 255.255.255.0
	gateway 10.11.2.1
```
#### Lawine
```
auto eth0
iface eth0 inet static
	address 10.11.3.4
	netmask 255.255.255.0
	gateway 10.11.3.1
```
#### Linie
```
auto eth0
iface eth0 inet static
	address 10.11.3.5
	netmask 255.255.255.0
	gateway 10.11.3.1
```
#### Lugner
```
auto eth0
iface eth0 inet static
	address 10.11.3.6
	netmask 255.255.255.0
	gateway 10.11.3.1
```
#### Frieren
```
auto eth0
iface eth0 inet static
	address 10.11.4.4
	netmask 255.255.255.0
	gateway 10.11.4.1
```
#### Flamme
```
auto eth0
iface eth0 inet static
	address 10.11.4.5
	netmask 255.255.255.0
	gateway 10.11.4.1
```
#### Fern
```
auto eth0
iface eth0 inet static
	address 10.11.4.6
	netmask 255.255.255.0
	gateway 10.11.4.1
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

## NO 6
```
wget -O '/var/www/granz.channel.b05.com' 'https://drive.google.com/u/0/uc?id=1ViSkRq7SmwZgdK64eRbr5Fm1EGCTPrU1&export=download'
unzip -o /var/www/granz.channel.b05.com -d /var/www/
rm /var/www/granz.channel.b05.com
mv /var/www/modul-3 /var/www/granz.channel.b05.com
```
