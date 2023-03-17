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

ip route 0.0.0.0 0.0.0.0 10.1.1.2

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


### FW1

```
configure
set system host-name FW1  
set interfaces ethernet eth0 address 200.1.1.1/24  
set interfaces ethernet eth2 address 10.1.1.1/24  
set interfaces ethernet eth5 address 10.0.0.1/24  
set protocols static route 0.0.0.0/0 next-hop 200.1.1.10  
set protocols static route 10.2.2.0/24 next-hop 10.1.1.10  
commit  
save
exit
```

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

```
# Set VRRP
configure
set high-availability vrrp group FWCluster vrid 10  
set high-availability vrrp group FWCluster interface eth5  
set high-availability vrrp group FWCluster virtual-address 192.168.100.1/24  
set high-availability vrrp sync-group FWCluster member FWCluster  
set high-availability vrrp group FWCluster rfc3768-compatibility
set service conntrack-sync accept-protocol 'tcp,udp,icmp'  
set service conntrack-sync failover-mechanism vrrp sync-group FWCluster  
set service conntrack-sync interface eth5  
set service conntrack-sync mcast-group 225.0.0.50  
set service conntrack-sync disable-external-cache
commit  
save
exit

```


```
# Flow Control rules
configure
set firewall name FROM-INSIDE-TO-OUTSIDE rule 10 action accept
set firewall name FROM-INSIDE-TO-OUTSIDE rule 10 protocol udp
set firewall name FROM-INSIDE-TO-OUTSIDE rule 10 destination port 5000-6000
commit
save
exit

```

### FW2

```
configure  
set system host-name FW2  
set interfaces ethernet eth0 address 200.1.1.2/24  
set interfaces ethernet eth2 address 10.1.1.2/24  
set interfaces ethernet eth5 address 10.0.0.2/24  
set protocols static route 0.0.0.0/0 next-hop 200.1.1.10  
set protocols static route 10.2.2.0/24 next-hop 10.1.1.10  
commit  
exit
```

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

```

#Set VRRP

configure
set high-availability vrrp group FWCluster vrid 10  
set high-availability vrrp group FWCluster interface eth5  
set high-availability vrrp group FWCluster virtual-address 192.168.100.1/24  
set high-availability vrrp sync-group FWCluster member FWCluster  
set high-availability vrrp group FWCluster rfc3768-compatibility
set service conntrack-sync accept-protocol 'tcp,udp,icmp'  
set service conntrack-sync failover-mechanism vrrp sync-group FWCluster  
set service conntrack-sync interface eth5  
set service conntrack-sync mcast-group 225.0.0.50  
set service conntrack-sync disable-external-cache
commit  
save
exit
```

```
# Flow Control rules

configure
set firewall name FROM-INSIDE-TO-OUTSIDE rule 10 action accept
set firewall name FROM-INSIDE-TO-OUTSIDE rule 10 protocol udp
set firewall name FROM-INSIDE-TO-OUTSIDE rule 10 destination port 5000-6000
commit
save
exit


```

```
# just a test (it works :) )

configure
set firewall name FROM-INSIDE-TO-OUTSIDE rule 20 action drop
set firewall name FROM-INSIDE-TO-OUTSIDE rule 20 protocol tcp
set firewall name FROM-INSIDE-TO-OUTSIDE rule 20 destination port 1000-2000
commit
save
exit
```
