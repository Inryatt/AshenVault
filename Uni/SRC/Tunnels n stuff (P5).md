
PC1
```
ip 192.168.1.100/24 192.168.1.1
ip 2001:1:1::100 2001:1:1::1
wr
```


PC2
```
ip 192.168.2.100/24 192.168.2.2
ip 2001:2:2::100 2001:2:2::2
wr
```

PC3

```
ip 192.168.3.100/24 192.168.3.3
ip 2001:3:3::100 2001:3:3:::3
wr
```



R1
```
conf t
ipv6 unicast-routing  
interface Loopback 0  
ip address 200.0.0.1 255.255.255.255  
ip ospf 1 area 0  
interface FastEthernet0/0  
ip address 200.1.1.1 255.255.255.0  
ip ospf 1 area 0  
no shut   
interface FastEthernet0/1  
ip address 192.168.1.1 255.255.255.0  
ipv6 address 2001:1:1::1/64  
no shut 
end
wr



# gre tunnel
conf t
interface Tunnel1  
ip address 10.1.1.1 255.255.255.252  
ipv6 address 2001::1/64  
tunnel source Loopback0  
tunnel destination 200.0.0.2  
tunnel mode gre ip

end
wr

```

```
# Static Routing
conf t
ip route 192.168.2.0 255.255.255.0 Tunnel1
ipv6 route 2001:2:2::/64 Tunnel1

end 
wr

```

```
# Route Maps
conf t
no ip route 192.168.2.0 255.255.255.0 Tunnel1
no ipv6 route 2001:2:2::/64 Tunnel1
end

clear ip route *

conf t
ipv6 access-list L101
sequence 20 permit ipv6 2001:1:1::/64 2001:2:2::/64
access-list 100 permit ip 192.168.1.0 0.0.0.255 192.168.2.0 0.0.0.255

route-map routeT1 permit 10  
match ip address 100  
set ip next-hop 10.1.1.2  

route-map route6T1 permit 10  
match ipv6 address L101  
set ipv6 next-hop 2001::2  

interface FastEthernet0/1  
ip policy route-map routeT1 
ipv6 policy route-map route6T1
end 
wr

```



```

# dynmic routing
conf t
interface FastEthernet0/1
no ip policy route-map routeT1
no ipv6 policy route-map route6T1

interface Tunnel1
ip ospf 2 area 0
ipv6 ospf 2 area 0
interface FastEthernet0/1
ip ospf 2 area 0
ipv6 ospf 2 area 0
end
wr
```

```


conf t
interface Tunnel2  
ip address 10.2.2.1 255.255.255.252  
tunnel source Loopback0  
tunnel destination 200.0.0.3
tunnel mode gre ip
end 
wr

# for 2nd exercise
conf t
interface Tunnel2  
ip ospf 2 area 0
end
wr

```


R2
```
conf t
ipv6 unicast-routing  
interface Loopback 0  
ip address 200.0.0.2 255.255.255.255  
ip ospf 1 area 0  
interface f0/0  
ip address 200.2.2.2 255.255.255.0  
ip ospf 1 area 0  
no shut   
interface f0/1  
ip address 192.168.2.2 255.255.255.0  
ipv6 address 2001:2:2::2/64  
no shut 
end 
wr



# gre tunnel
conf t
interface Tunnel1  
ip address 10.1.1.2 255.255.255.252  
ipv6 address 2001::2/64  
tunnel source Loopback0  
tunnel destination 200.0.0.1  
tunnel mode gre ip
end 
wr

# static routes

conf t
ip route 192.168.1.0 255.255.255.0 Tunnel1
ipv6 route 2001:1:1::/64 Tunnel1y


end
wr
```

```

# Route Maps
conf t
no ip route 192.168.1.0 255.255.255.0 Tunnel1
no ipv6 route 2001:1:1::/64 Tunnel1
end

clear ip route *

conf t
ipv6 access-list L101
sequence 20 permit ipv6 2001:2:2::/64 2001:1:1::/64
access-list 100 permit ip 192.168.2.0 0.0.0.255 192.168.1.0 0.0.0.255

route-map routeT1 permit 10  
match ip address 100  
set ip next-hop 10.1.1.1  

route-map route6T1 permit 10  
match ipv6 address L101  
set ipv6 next-hop 2001::1  

interface FastEthernet0/1  
ip policy route-map routeT1 
ipv6 policy route-map route6T1
end 
wr

```


```

# dynamic routing
conf t
interface FastEthernet0/1
no ip policy route-map routeT1
no ipv6 policy route-map route6T1

interface Tunnel1
ip ospf 2 area 0
ipv6 ospf 2 area 0
interface FastEthernet0/1
ip ospf 2 area 0
ipv6 ospf 2 area 0
end
wr
```



R3
```
conf t
ipv6 unicast-routing  
interface Loopback 0  
ip address 200.0.0.3 255.255.255.255  
ip ospf 1 area 0  
interface f0/0  
ip address 200.3.3.3 255.255.255.0  
ip ospf 1 area 0  
no shut   
interface f0/1  
ip address 192.168.3.3 255.255.255.0  

no shut 
end 
wr



conf t
interface Tunnel2  
ip address 10.2.2.2 255.255.255.252  
tunnel source Loopback0  
tunnel destination 200.0.0.1
tunnel mode gre ip
end 
wr



conf t
interface Tunnel2  
ip ospf 2 area 0  
interface FastEthernet0/1  
ip ospf 2 area 0

end
wr

```


RA
```
conf t
interface FastEthernet0/0  
ip address 200.1.1.10 255.255.255.0  
ip ospf 1 area 0  
no shut   
interface FastEthernet0/1  
ip address 200.2.2.10 255.255.255.0  
ip ospf 1 area 0  
no shut 

interface FastEthernet1/0
ip address 200.3.3.10 255.255.255.0  
ip ospf 1 area 0  
no shut 

end 
wr
```



