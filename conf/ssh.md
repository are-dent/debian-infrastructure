[konsep ssh]
komputer kita -> jarak jauh -> server
"jadi komputer kita bisa akses server tanpa dari servernya langsung"

[langkah]
apt install openssh-server

nano /etc/ssh/sshd_config

hapus pagar pada #port 22 kemudian bisa ubah port sesuai keinginan

lalu hapus juga pagar pada #PermitRootLogin dan ubah juga kalimat selanjutnya menjadi yes

#keluar

systemctl restart ssh

lalu uji coba lewat cmd milik client
ketik : ssh root@14.14.14.14 -p 22
ketik : yes