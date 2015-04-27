# firmware
These images have GRE tunneling support compiled into the kernel.

The GRE tunnels work behind a NAT when using OpenWRT on the gateway router.  Not sure if stock firmwares will NAT GRE properly.

Example tunnel setup:
The key is optional but you need to use if you have mutiple tunnels.

[Side A]
ip tunnel add gretun mode gre remote [Side B WAN IP] local [Local IP, if behind NAT use the LAN ip of the device] ttl 255 [key XXXX]
ip link set gretun up
ip -4 addr add 172.30.0.1/24 dev gretun
ip route add 172.30.0.0/24 dev gretun

[Side B]
ip tunnel add gretun mode gre remote [Side A WAN IP] local [Local IP, if behind NAT use the LAN ip of the device] ttl 255 [key XXXX]
ip link set gretun up
ip -4 addr add 172.30.0.2/24 dev gretun
ip route add 172.30.0.0/24 dev gretuna

bmx6 setup:
bmx6 -c -i gretun

