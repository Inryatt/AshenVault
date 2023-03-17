
### PC1
```
ip 10.2.2.100/24 10.2.2.10
write
```

### PC2

```
ip 200.2.2.100/24 200.2.2.10
write
```

### R1-In

```
conf t
int f0/0
ip addr 10.1.1.10 255.255.255.0
no shut
int f0/1
ip addr 10.2.2.10 255.255.255.0
no shut

ip route 0.0.0.0 0.0.0.0 10.1.1.1

end
write
```

### R2-Out

```
conf t
int f0/0
ip addr 200.1.1.10 255.255.255.0
no shut
int f0/1
ip addr 200.2.2.10 255.255.255.0
no shut

ip route 192.1.0.0 255.255.254.0 200.1.1.1

end
wr

```

### LB1

```
configure
set system host-name LB1  
set interfaces ethernet eth6 address 10.1.1.1/24  
set interfaces ethernet eth7 address 10.0.1.10/24  
set interfaces ethernet eth8 address 10.0.2.10/24  
set protocols static route 0.0.0.0/0 next-hop 10.0.1.1  
set protocols static route 0.0.0.0/0 next-hop 10.0.2.2  
set protocols static route 10.2.2.0/24 next-hop 10.1.1.10
commit  
save
exit
```

```
# load balancing
set load-balancing wan interface-health eth1 nexthop 10.0.1.1  
set load-balancing wan interface-health eth2 nexthop 10.0.2.2  
set load-balancing wan rule 1 inbound-interface eth0  
set load-balancing wan rule 1 interface eth1 weight 1  
set load-balancing wan rule 1 interface eth2 weight 1  
set load-balancing wan sticky-connections inbound  
set load-balancing wan disable-source-nat
```


### FW1

```
configure
set system host-name FW1  
set interfaces ethernet eth2 address 10.0.1.1/24  
set interfaces ethernet eth0 address 10.0.3.1/24  
set protocols static route 0.0.0.0/0 next-hop 10.0.3.10  
set protocols static route 10.2.2.0/24 next-hop 10.0.1.10  
commit  
save
exit
```

*dont think this is suposed to be done here!*
```
# NAT

configure  
set nat source rule 10 outbound-interface eth0  
set nat source rule 10 source address 10.0.0.0/8  
set nat source rule 10 translation address 192.1.0.1-192.1.0.10  
commit  
save
exit


```



### FW2

```
configure  
set system host-name FW2  
set interfaces ethernet eth0 address 10.0.4.2/24  
set interfaces ethernet eth2 address 10.0.2.2/24  

set protocols static route 0.0.0.0/0 next-hop 10.0.4.10  
set protocols static route 10.2.2.0/24 next-hop 10.0.2.10  
commit  
exit
```


*dont think this is suposed to be done here!*
```
# Add NAT
configure  
set nat source rule 10 outbound-interface eth0  
set nat source rule 10 source address 10.0.0.0/8  
set nat source rule 10 translation address 192.1.0.1-192.1.0.10  
commit  
save
exit
``` 


### LB2
```

configure
set system host-name LB2  
set interfaces ethernet eth6 address 200.1.1.1/24  
set interfaces ethernet eth7 address 10.0.3.10/24  
set interfaces ethernet eth8
address 10.0.4.10/24  
set protocols static route 200.2.2.0/24 next-hop 200.1.1.10  
set protocols static route 192.1.0.0/23 next-hop 10.0.3.1  
set protocols static route 192.1.0.0/23 next-hop 10.0.4.2
commit
save
exit
```

```
# load balancing
set load-balancing wan interface-health eth1 nexthop 10.0.3.1  
set load-balancing wan interface-health eth2 nexthop 10.0.4.2  
set load-balancing wan rule 1 inbound-interface eth0  
set load-balancing wan rule 1 interface eth1 weight 1  
set load-balancing wan rule 1 interface eth2 weight 1  
set load-balancing wan sticky-connections inbound  
set load-balancing wan disable-source-nat
```


*nat goes here????*

```

configure  
set nat source rule 10 outbound-interface eth0  
set nat source rule 10 source address 10.0.0.0/8  
set nat source rule 10 translation address 192.1.0.1-192.1.0.10  
commit  
save
exit
```



