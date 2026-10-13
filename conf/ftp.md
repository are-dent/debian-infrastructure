[konsep ftp]
server -> wadah khusus <- client
server dan client bisa saling tukar data di wadah khusus

[langkah samba]
apt install samba

mkdir /usr/share/samba/public
mkdir /usr/share/samba/private

adduser sambal (bebas)
smbpasswd -a sambal -> buat password
chown -R sambal:sambal /srv/samba/private 
chmod -R 755 /srv/samba/private

nano /etc/samba/smbd.conf
#di bagian paling bawah

[public]
 path = /srv/samba/public
 browseable = yes
 writable = yes
 guest ok = yes
 
[private]
 path = /srv/samba/private
 browseable = yes
 read only = no
 valid users = sambal
 
#keluar

systemctl restart samba

--

[langkah proftpd]
apt install proftpd

sudah, tinggal test pakai filezilla (aplikasi)