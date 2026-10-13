[konsep dns]
ip <-> domain
example : 14.14.14.14 = nomaden.org

[langkah]
apt install bind9 dnsutils resolvconf

cd /etc/bind/
cp db.local db.forden 
#forden -> forward nomaden
cp db.127 db.reverse

nano db.forden
ubah semua localhost menjadi nama domain (nomaden.org) pastikan setelah org ada . (org.)

ubah semua AAAA menjadi A (ipv6 -> ipv4)
ubah ip sesuai dengan yang kamu set 14.14.14.14

#keluar

nano db.reverse

seperti tadi, ubah semua localhost.
di bagian paling kiri "1.0.0" ubah jadi oktet ke 4 ip server yaitu "14"

#keluar

nano named.conf.default-zones
-ubah localhost jadi nama domain
-ubah path nya
-ubah ip pada reverse jadi 3 oktet pertama (14.14.14.in-addr.arpa)

#keluar

nano /etc/hosts
tambahkan 14.14.14.14 (tab) nomaden.org

#keluar

nano /etc/resolvconf/re(tab)/head
tambahkan :
-nameserver 8.8.8.8
-nameserver 14.14.14.14
-search nomaden.org

#keluar

systemctl restart networking bind9

nslookup nomaden.org 14.14.14.14
bila berhasil

di pc client ketik windows + r, lalu masukkan ncpa.cpl -> klik vmnet 1 -> properties -> ipv4 -> properties -> tambahkan ip server pada dns -> disable enable
