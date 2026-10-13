apt install wireguard-tools -y

mkdir -p /etc/wireguard
chmod 700 /etc/wireguard

umask 077

wg genkey | tee /etc/wireguard/server_private.key | wg pubkey > /etc/wireguard/server_public.key

open apk wireguard client

add tunnel -> empty tunnel
auto generate client public key
copy it

back to debian

nano /etc/wireguard/wg0.conf

[Interface]
 Address = 10.10.0.1/24
 ListenPort = 51820
 PrivateKey = <SERVER_PRIVATE_KEY>

[Peer]
 PublicKey = <CLIENT_PUBLIC_KEY>
 AllowedIPs = 10.10.0.2/32

#keluar

sysctl -w net.ipv4.ip_forward=1

grep -q '^net.ipv4.ip_forward=1$' /etc/sysctl.conf || echo 'net.ipv4.ip_forward=1' >> /etc/sysctl.conf

sysctl -p

sysctl net.ipv4.ip_forward (check)

cat /etc/wireguard/server_public.key

open wireguard on client

[Interface]
 Address = 10.10.0.2/24
 PrivateKey = <CLIENT_PRIVATE_KEY>
 DNS = 14.14.14.14

[Peer]
 PublicKey = <SERVER_PUBLIC_KEY>
 Endpoint = <SERVER_ENDPOINT>:51820
 AllowedIPs = 10.10.0.0/24, 14.14.14.14/24
 PersistentKeepalive = 25

enable

win + r = cmd

ping 10.10.0.1
ping 14.14.14.14

wg show


