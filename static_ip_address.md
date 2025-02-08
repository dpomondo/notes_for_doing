###### Find Raspberry Pi's current `ip4` address:
```
    hostname -I
```
###### Find the `ip4` address of the router:
 ```
    ip r
```
The results will look something like this:
```
    default via 192.168.10.1 dev eth0 proto dhcp src 192.168.10.67 metric 100
    192.168.10.0/24 dev eth0 proto kernel scope link src 192.168.10.67 metric 100
```
The  `ip4` address is after the `default via` will be the address of the router.
###### Find the address of the DNS server
```
    grep "nameserver" /etc/resolv.conf
```
###### Open the dhcpcd configuration file
```
    vi /etc/dhcpcd.conf
```
Add the following information:
```
    interface [INTERFACE]
    static_routers=[ROUTER IP]
    static domain_name_servers=[DNS IP]
    static ip_address=[STATIC IP ADDRESS YOU WANT]/24
```
The current dhcpcd file looks like this:
```
    interface wlan0
    static_routers=192.168.10.1
    static domain_name_servers=192.168.10.1
    inform ip_address=192.168.10.67/24
```
