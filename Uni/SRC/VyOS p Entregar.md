## IPs
PC1 - 10.2.2.100

R1 - f0/1 - 10.2.2.10
	 - f0/0 - 10.1.1.10

PC2 - 200.2.2.100

R2 - F0/0 - 200.1.1.10
	 - F0/1 - 200.2.2.10

LB1A - eth0 - 10.1.1.21
		    eth1 - 10.1.1.31
		    eth2 - 10.0.1.11  10.2.1.11
		    eth3 - 10.0.1.21   10.3.1.21 
		    
LB1B - eth0 - 10.1.1.22
			eth1 - 10.0.1.32
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


### PC1
```
ip 10.2.2.100/24 10.2.2.10
write
```

### R1 (In)


```
conf t
int f0/0
ip addr 10.1.1.10 255.255.255.0
no shut
int f0/1
ip addr 10.2.2.10 255.255.255.0
no shut

ip route 0.0.0.0 0.0.0.0 10.1.1.11
# ip route 0.0.0.0 0.0.0.0 10.1.1.12
end
write
```




### LB1A

```
configure
set system host-name LB1A
set interfaces ethernet eth0 address 10.1.1.11/24  
set interfaces ethernet eth1 address 10.1.0.11/24  
set interfaces ethernet eth2 address 10.1.2.11/24  
set interfaces ethernet eth3 address 10.1.3.11/24  

set protocols static route 0.0.0.0/0 next-hop 10.1.3.13
set protocols static route 0.0.0.0/0 next-hop 10.1.2.14
set protocols static route 10.2.2.0/24 next-hop 10.1.1.10


#vrrp

set high-availability vrrp group LB1Cluster vrid 10  
set high-availability vrrp group LB1Cluster interface eth1
set high-availability vrrp group LB1Cluster virtual-address 192.168.100.1/24 
set high-availability vrrp sync-group LB1Cluster member LB1Cluster  
set high-availability vrrp group LB1Cluster rfc3768-compatibility


# conntrack sync

set service conntrack-sync accept-protocol 'tcp,udp,icmp'  
set service conntrack-sync failover-mechanism vrrp sync-group LB1Cluster  
set service conntrack-sync interface eth1  
set service conntrack-sync mcast-group 225.0.0.50  
set service conntrack-sync disable-external-cache


# load balancing

set load-balancing wan interface-health eth3 nexthop 10.1.3.13 
set load-balancing wan interface-health eth2 nexthop 10.1.2.14 
set load-balancing wan rule 1 inbound-interface eth0  
set load-balancing wan rule 1 interface eth3 weight 1  
set load-balancing wan rule 1 interface eth2 weight 1 
set load-balancing wan sticky-connections inbound  
set load-balancing wan disable-source-nat
commit  
save
exit
```



### LB1B
```
configure
set system host-name LB1B
set interfaces ethernet eth0 address 10.1.1.12/24  
set interfaces ethernet eth1 address 10.1.0.12/24  
set interfaces ethernet eth2 address 10.1.4.12/24  
set interfaces ethernet eth3 address 10.1.3.12/24  
set protocols static route 0.0.0.0/0 next-hop 10.1.4.13
set protocols static route 0.0.0.0/0 next-hop 10.1.3.14
set protocols static route 10.2.2.0/24 next-hop 10.1.1.10

#vrrp

set high-availability vrrp group LB1Cluster vrid 10  
set high-availability vrrp group LB1Cluster interface eth1
set high-availability vrrp group LB1Cluster virtual-address 192.168.100.1/24 
set high-availability vrrp sync-group LB1Cluster member LB1Cluster  
set high-availability vrrp group LB1Cluster rfc3768-compatibility


#conntrack sinc

set service conntrack-sync accept-protocol 'tcp,udp,icmp'  
set service conntrack-sync failover-mechanism vrrp sync-group LB1Cluster  
set service conntrack-sync interface eth1  
set service conntrack-sync mcast-group 225.0.0.50  
set service conntrack-sync disable-external-cache


# load balancing

set load-balancing wan interface-health eth3 nexthop 10.1.3.14
set load-balancing wan interface-health eth2 nexthop 10.1.4.13 
set load-balancing wan rule 1 inbound-interface eth0  
set load-balancing wan rule 1 interface eth3 weight 1  
set load-balancing wan rule 1 interface eth2 weight 1 
set load-balancing wan sticky-connections inbound  
set load-balancing wan disable-source-nat
commit  
save
exit
```


### FW1
```

configure
set system host-name FW1  
set interfaces ethernet eth0 address 10.2.0.13/24  
set interfaces ethernet eth1 address 10.2.1.13/24  
set interfaces ethernet eth2 address 10.1.4.13/24  
set interfaces ethernet eth3 address 10.1.3.13/24  
set protocols static route 0.0.0.0/0 next-hop 10.2.0.16
# set protocols static route 0.0.0.0/0 next-hop 10.2.1.16  
set protocols static route 10.2.2.0/24 next-hop 10.1.3.11
# set protocols static route 10.2.2.0/24 next-hop 10.1.4.12  
commit  
save
exit
```



### FW2
```

configure
set system host-name FW2  
set interfaces ethernet eth0 address 10.2.4.14/24  
set interfaces ethernet eth1 address 10.2.3.14/24  
set interfaces ethernet eth2 address 10.1.2.14/24  
set interfaces ethernet eth3 address 10.1.3.14/24  
set protocols static route 0.0.0.0/0 next-hop 10.2.4.15
# set protocols static route 0.0.0.0/0 next-hop 10.2.3.16
# set protocols static route 10.2.2.0/24 next-hop 10.1.2.11
set protocols static route 10.2.2.0/24 next-hop 10.1.3.12  
commit  
save
exit

```




### LB2A

```
configure
set system host-name LB2A
set interfaces ethernet eth0 address 10.2.0.16/24  
set interfaces ethernet eth1 address 10.2.3.16/24  
set interfaces ethernet eth2 address 10.2.4.16/24  
set interfaces ethernet eth3 address 200.1.1.16/24  
set protocols static route 0.0.0.0/0 next-hop 200.1.1.10  
set protocols static route 10.2.2.0/24 next-hop 10.2.0.13
set protocols static route 10.2.2.0/24 next-hop 10.2.3.14

#vrrp
set high-availability vrrp group LB2Cluster vrid 10  
set high-availability vrrp group LB2Cluster interface eth2
set high-availability vrrp group LB2Cluster virtual-address 192.168.100.1/24 
set high-availability vrrp sync-group LB2Cluster member LB2Cluster  
set high-availability vrrp group LB2Cluster rfc3768-compatibility

# conntrack sync
set service conntrack-sync accept-protocol 'tcp,udp,icmp'  
set service conntrack-sync failover-mechanism vrrp sync-group LB2Cluster  
set service conntrack-sync interface eth2  
set service conntrack-sync mcast-group 225.0.0.50  
set service conntrack-sync disable-external-cache

# load balancing


set load-balancing wan interface-health eth0 nexthop 10.2.0.13  
set load-balancing wan interface-health eth1 nexthop 10.2.3.14
set load-balancing wan rule 1 inbound-interface eth3  
set load-balancing wan rule 1 interface eth0 weight 1  
set load-balancing wan rule 1 interface eth1 weight 1 
set load-balancing wan sticky-connections inbound  
set load-balancing wan disable-source-nat

# Nat/pat

set nat source rule 10 outbound-interface eth3
set nat source rule 10 source address 10.0.0.0/8  
set nat source rule 10 translation address 192.1.0.1-192.1.0.10
commit  
save
exit

```

### LB2B


```
configure
set system host-name LB2B
set interfaces ethernet eth0 address 10.2.4.15/24  
set interfaces ethernet eth1 address 10.2.1.15/24  
set interfaces ethernet eth2 address 10.2.4.15/24  
set interfaces ethernet eth3 address 200.1.1.15/24  

set protocols static route 0.0.0.0/0 next-hop 200.1.1.10
set protocols static route 10.2.2.0/24 next-hop 10.2.4.14
set protocols static route 10.2.2.0/24 next-hop 10.2.1.13

#vrrp

set high-availability vrrp group LB2Cluster vrid 10  
set high-availability vrrp group LB2Cluster interface eth2
set high-availability vrrp group LB2Cluster virtual-address 192.168.100.1/24 
set high-availability vrrp sync-group LB2Cluster member LB2Cluster  
set high-availability vrrp group LB2Cluster rfc3768-compatibility


# conntrack sync

set service conntrack-sync accept-protocol 'tcp,udp,icmp'  
set service conntrack-sync failover-mechanism vrrp sync-group LB2Cluster  
set service conntrack-sync interface eth2  
set service conntrack-sync mcast-group 225.0.0.50  
set service conntrack-sync disable-external-cache

# load balancing

set load-balancing wan interface-health eth0 nexthop 10.2.4.14
set load-balancing wan interface-health eth1 nexthop 10.2.1.13
set load-balancing wan rule 1 inbound-interface eth3  
set load-balancing wan rule 1 interface eth0 weight 1  
set load-balancing wan rule 1 interface eth1 weight 1 
set load-balancing wan sticky-connections inbound  
set load-balancing wan disable-source-nat


# Nat/pat
  
set nat source rule 10 outbound-interface eth3
set nat source rule 10 source address 10.0.0.0/8  
set nat source rule 10 translation address 100.64.0.10-100.64.0.20
commit  
save
exit

```

vyos

### R2


```
conf t
int f0/0
ip addr 200.1.1.10 255.255.255.0
no shut
int f0/1
ip addr 200.2.2.10 255.255.255.0
no shut

# ip route 192.1.0.0 255.255.254.0 200.1.1.16
ip route 192.1.0.0 255.255.254.0 200.1.1.15

end
wr

```


### PC2
```
ip 200.2.2.100/24 200.2.2.10
write
```

vyos
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

sudo cp /opt/vyatta/etc/config.boot.default /config/config.boot 