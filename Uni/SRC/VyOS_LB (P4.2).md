
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





/ offtopic


## IPs
PC1 - 10.2.2.100
R1 - f0/1 - 10.2.2.10
	 - f0/0 - 10.1.1.10

PC2 - 200.2.2.100

R2 - F0/0 - 200.1.1.10
	 - F0/1 - 200.2.2.10

LB1A - eth0 - 10.1.1.21
		    eth1 - 10.1.1.31
		    eth2 - 10.0.1.11 10.2.1.11
		    eth3 - 10.0.1.21  10.3.1.21 
		    
LB1B - eth0 - 10.1.1.22
			eth1 - 10.1.1.32
			eth2 - 10.0.1.12
			eth3 - 10.0.1.22
			
FW1 -  eth0 -  10.0.2.11
		   eth1 -  10.0.2.21
		   eth2 -  10.0.1.13
		   eth3 -  10.0.1.23
		   
FW2 -  eth0 -  10.0.2.12
		   eth1 -  10.0.2.22
		   eth2 -  10.0.1.14
		   eth3 -  10.0.1.24
		   
LB2A - eth0 -  10.0.2.13
		   eth1 -  10.0.2.23
		   eth2 -  200.1.1.11
		   eth3 -  200.1.1.21
		   
LB2B - eth0 -  10.0.2.14
		   eth1 -  10.0.2.24
		   eth2 -  200.1.1.12
		   eth3 -  200.1.1.22
sudo cp /opt/vyatta/etc/config.boot.default /config/config.boot && reboot


## IPs 2
PC1 - 10.2.2.100

R1 - f0/1 - 10.2.2.10
	 - f0/0 - 10.1.1.10

PC2 - 200.2.2.100

R2 - F0/0 - 200.1.1.10
	 - F0/1 - 200.2.2.10

LB1A - eth0 - 10.1.1.11
		    eth1 - 10.1.0.11
		    eth2 - 10.1.2.11
		    eth3 - 10.1.3.11 
		    
LB1B - eth0 - 10.1.1.12
			eth1 - 10.1.0.12
			eth2 - 10.1.4.12
			eth3 - 10.1.3.12
			
FW1 -  eth0 -  10.2.0.13
		   eth1 -  10.2.1.13
		   eth2 -  10.1.4.13
		   eth3 -  10.1.3.13
		   
FW2 -  eth0 -  10.2.4.14
		   eth1 -  10.2.3.14
		   eth2 -  10.1.2.14
		   eth3 -  10.1.3.14
		   
LB2A - eth0 -  10.2.0.16
		   eth1 -  10.2.3.16
		   eth2 -  10.2.4.16
		   eth3 -  200.1.1.16
		   
LB2B - eth0 -  10.2.4.15
		   eth1 -  10.2.1.15
		   eth2 -  10.2.4.15
		   eth3 -  200.1.1.15