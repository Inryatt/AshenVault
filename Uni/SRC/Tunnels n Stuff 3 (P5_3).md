
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
int tunnel10
ip addr 10.10.10.1 255.255.255.0
ip nhrp network-id 1
tunnel source lo0
tunnel mode gre multipoint
tunnel key 1
end
wr


# conf t
# ip route 192.168.2.0 255.255.255.0 10.10.10.2
# ip route 192.168.3.0 255.255.255.0 10.10.10.3


conf t 
int tunnel10
ip ospf 2 area 0
ip ospf 2 area 0
ip nhrp map multicast dynamic
ip ospf network broadcast
ip ospf priority 2

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


int tunnel10
ip addr 10.10.10.2 255.255.255.0
ip addr 10.10.10.3 255.255.255.0

ip nhrp network-id 1
ip nhrp nhs 10.10.10.1
ip nhrp map 10.10.10.1 200.0.0.1

tunnel source Lo0
tunnel mode gre multipoint 
tunnel key 1
end 
wr


conf t
# ip route 192.168.1.0 255.255.255.0 10.10.10.1
# ip route 192.168.3.0 255.255.255.0 10.10.10.3

interface tunnel10
ip ospf 2 area 0
ip nhrp map multicast 200.0.0.1
ip ospf network broadcast
ip ospf priority 0


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


conf t

int f1/0
no shut
ip addr 200.3.3.10 255.255.255.0
ip ospf 1 area 0
end
wr



conf t
# ip route 192.168.1.0 255.255.255.0 10.10.10.1
# ip route 192.168.2.0 255.255.255.0 10.10.10.2



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

int tunnel10
ip addr 10.10.10.3 255.255.255.0
ip nhrp networl-id 1
ip nhrp nhs 10.10.10.1
ip nhrp map 10.10.10.1 200.0.0.1
tunnel source lo0
tunnel mode gre multipoint
tunnel key 1
exit

# ip route 192.168.1.0 255.255.255.0 10.10.10.1
# ip route 192.168.2.0 255.255.255.0 10.10.10.2

conf t 
interface tunnel10
ip ospf 2 area 0
ip nhrp map multicast 200.0.0.1
ip ospf network broadcast
ip ospf priority 0

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

