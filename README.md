# MPLS-Core-w-PE--works-OK
MPLS Core Lab for GNS3 with 4 PE routers and 4 MPLS core routers

![alt tag](https://raw.githubusercontent.com/payozon/MPLS-Core-w-PE--works-OK/master/screenshot2.png)

### IOS Image Used
```
c7200-adventerprisek9_sna-mz.124-15.T1.image
```
### Adapters Config, Mem Config, Router Settings for GNS3

![alt tag](https://raw.githubusercontent.com/payozon/MPLS-Core-w-PE--works-OK/master/adapters-config.JPG)
![alt tag](https://raw.githubusercontent.com/payozon/MPLS-Core-w-PE--works-OK/master/mem-disk.JPG)
![alt tag](https://raw.githubusercontent.com/payozon/MPLS-Core-w-PE--works-OK/master/c7200-config.JPG)

## Config Filez list
### The MPLS on OSPF only no-BGP 4-routers CORE 

https://github.com/payozon/MPLS-Core-w-PE--works-OK/blob/master/.MPLS-Core-P1

https://github.com/payozon/MPLS-Core-w-PE--works-OK/blob/master/.MPLS-Core-P2

https://github.com/payozon/MPLS-Core-w-PE--works-OK/blob/master/.MPLS-Core-P3

https://github.com/payozon/MPLS-Core-w-PE--works-OK/blob/master/.MPLS-Core-P4

### The Provider's Edge 4x routers with BGP
https://github.com/payozon/MPLS-Core-w-PE--works-OK/blob/master/.MPLS-Core-PE1

https://github.com/payozon/MPLS-Core-w-PE--works-OK/blob/master/.MPLS-Core-PE2

https://github.com/payozon/MPLS-Core-w-PE--works-OK/blob/master/.MPLS-Core-PE3

https://github.com/payozon/MPLS-Core-w-PE--works-OK/blob/master/.MPLS-Core-PE4


## Topology Summary 
###  Connections between routers

![alt tag](https://raw.githubusercontent.com/payozon/MPLS-Core-w-PE--works-OK/master/topology-summary.JPG)

### Pull configs cmds
```
term len 0
sh run
```
### TAP interfaces install & masquerade for cloud connection
```
sudo nano /etc/network/interfaces
auto tap0
iface tap0 inet static
        address 172.16.254.254
        netmask 255.255.255.0
        pre-up  /sbin/ip tuntap add dev tap0 mode tap
        post-down /sbin/ip tuntap del dev tap0 mode tap
```

```
sudo ifup tap0
sudo iptables -t nat -A POSTROUTING -s 172.16.254.0/24 ! -d 172.16.254.0/24 -j MASQUERADE
```
