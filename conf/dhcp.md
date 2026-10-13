[konsep dhcp]
server setting ip -> client dapet ip otomatis -> bisa komunikasi/saling bertukar data

[langkah]
masuk ke setting vm mu -> tambahkan network adapter -> setting ke custom vmnet 1 (host only)

kemudian masuk ke vm editor -> edit preferences -> disable dhcp untuk vmnet 1 -> masukkan subnet dari ip yang akan kamu gunakan sebagai service dhcp
#misal saya gunakan subnet 14.14.14.0 dan netmask 255.255.255.0

login ke vmware,

apt install isc-dhcp-server
#install layanan dhcp

nano /etc/network/interfaces
#lokasi pengaturan ip

tambahkan :
allow-hotplug ens37
iface ens37 inet static
 address 14.14.14.14
 netmask 255.255.255.0

#keluar

nano /etc/default/isc-dhcp-server
tambahkan 'ens37' pada
IPv4"" -> IPv4"ens37"

#keluar

nano /etc/dhcp/dhcpd.conf
cari baris #a slightly...
hapus semua pagar di bawah kalimat tersebut sejauh 1 paragraf

isi subnet = 14.14.14.0
netmask = 255.255.255.0
range = 14.14.14.24 14.14.14.44
option routers = 14.14.14.14
broadcast = 14.14.14.255

#keluar

systemctl restart networking isc-dhcp-server
#restart layanan

di pc client ketik windows + r, lalu masukkan ncpa.cpl
pastikan vmnet 1 dhcp dan tunggu client menerima ipnya