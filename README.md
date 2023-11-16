# Jarkom-Modul-3-B05-2023

## No 1
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
