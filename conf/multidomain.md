[konsep multi domain]
14.14.14.14 = nomaden.org & dromarkhet.com

cd /etc/bind
cp db.local db.forkhet

-seperti langkah dns- (tambahkan path khusus di named.conf.default-zones)

nano /etc/resolvconf/re(tab)/head
tambahkan :
nameserver 14.14.14.14
search dromarkhet.com

#keluar

cd /etc/nginx/sites-available
cp nomaden dromarkhet

-ubah nama domain-

systemctl restart networking bind9 nginx

