
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





# gre tunnel
conf t
interface Tunnel1
ip address 10.1.1.1 255.255.255.252  
tunnel source Loopback0  
tunnel destination 200.0.0.2
tunnel mode gre ip
ip ospf 2 area 0

end
wr

# gre tunnel
conf t
interface Tunnel2
ip address 10.2.2.1 255.255.255.252  
ipv6 address 2001::3/64  
tunnel source Loopback0  
tunnel destination 200.0.0.3  
tunnel mode gre ip
ip ospf 2 area 0

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





# gre tunnel
conf t
interface Tunnel1
ip address 10.1.1.2 255.255.255.252  
tunnel source Loopback0  
tunnel destination 200.0.0.1
tunnel mode gre ip
ip ospf 2 area 0

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


conf t 
int tunnel 2
ip addr 10.2.2.2 255.255.255.255
ipv6 addr 2001::4/64
tunnel source Lo0
tunnel dest 200.0.0.1
tunnel mode gre ip
ip ospf 2 area 0
end
wr


```
