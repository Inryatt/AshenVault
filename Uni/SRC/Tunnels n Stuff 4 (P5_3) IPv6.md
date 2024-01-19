! falta meter os ips nas interfaces :clown: 
! mas nao me apetece so
# R1
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



conf t
int tunnel 20
ipv6 address 2001::1/64
ipv6 nhrp network-id 2
ipv6 nhrp map multicast dynamic
tunnel source Loopback0
tunnel mode gre multipoint
tunnel key 2
ipv6 ospf 2 area 0
ipv6 ospf network broadcast
ipv6 ospf priority 2

end
wr


```

# R2
```

conf t
ipv6 unicast-routing  
interface Loopback 0  
ip address 200.0.0.2 255.255.255.255  
ip ospf 1 area 0  
interface FastEthernet0/0  
ip address 200.2.2.2 255.255.255.0  
ip ospf 1 area 0  
no shut   
interface FastEthernet0/1  
ip address 192.168.2.2 255.255.255.0  
ipv6 address 2001:2:2::2/64  
no shut 
end
wr


int tunnel20
ipv6 address 2001::2/64 ! Router 2
ipv6 address 2001::3/64 ! Router 3)
ipv6 nhrp nhs 2001::1
ipv6 nhrp map 2001::1/64 200.0.0.1
ipv6 nhrp map multicast 200.0.0.1
ipv6 nhrp network-id 2
tunnel source Loopback0
tunnel mode gre multipoint
tunnel key 2
ipv6 ospf network broadcast
ipv6 ospf priority 0
ipv6 ospf 2 area 0



end
wr


```

# R3/A
```


conf t
ipv6 unicast-routing  
interface FastEthernet0/0  
ip address 200.1.1.10 255.255.255.0  
ip ospf 1 area 0  
no shut   
interface FastEthernet0/1  
ip address 200.2.2.10 255.255.255.0  
no shut 
int f1/0
no shut
ip addr 200.3.3.10 255.255.255.0
ip ospf 1 area 0
end
wr

int tunnel20
ipv6 address 2001::2/64 ! Router 2
ipv6 address 2001::3/64 ! Router 3)
ipv6 nhrp nhs 2001::1
ipv6 nhrp map 2001::1/64 200.0.0.1
ipv6 nhrp map multicast 200.0.0.1
ipv6 nhrp network-id 2
tunnel source Loopback0
tunnel mode gre multipoint
tunnel key 2
ipv6 ospf network broadcast
ipv6 ospf priority 0
ipv6 ospf 2 area 0

end
wr




```

# R4
```

conf t
ipv6 unicast-routing
int Lo0
ip addr 200.0.0.3 255.255.255.255
ip ospf 1 area 0

int f0/1
no shut 
ip addr 192.168.3.3 255.255.255.0
ip ospf 2 area 0
ipv6 enable 
ipv6 addr 2001:3:3::3/64
ipv6 ospf 2 area 0
int f0/0
no shut 
ip addr 200.3.3.3. 255.255.255.0
ip ospf 1 area 0
end 
wr


ipv6 address 2001::2/64 ! Router 2
ipv6 address 2001::3/64 ! Router 3)
ipv6 nhrp nhs 2001::1
ipv6 nhrp map 2001::1/64 200.0.0.1
ipv6 nhrp map multicast 200.0.0.1
ipv6 nhrp network-id 2
tunnel source Loopback0
tunnel mode gre multipoint
tunnel key 2
ipv6 ospf network broadcast
ipv6 ospf priority 0

ipv6 ospf 2 area 0
end

wr

```


## PC 1
```
ip 192.168.1.100
save

```

## PC 2
```
ip 192.168.2.100
save

```

## PC 3
```
ip 192.168.3.100
save

```

