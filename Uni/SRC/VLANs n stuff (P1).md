VPCS
```
ip 10.0.x.10x/24 10.0.x.1
```
SW L3 A
```

```

R1
```
vlan database
vlan 1
vlan 2
vlan 3
exit
conf t
ip routin
int f1/15
switchp mod trunk
switchp trunk enc dot1q
int f0/0
no shut
ip addr 10.1.1.11 255.255.255.0
ip ospf 1 area 0
int vlan 1
no shut 
ip addre 10.0.0.1 255.255.255.0
ip ospf 1 area 0
int vlan 2
no shut 
ip addre 10.0.2.1 255.255.255.0
ip ospf 1 area 0
int vlan 3
no shut 
ip addre 10.0.3.1 255.255.255.0
ip ospf 1 area 0
exit
write
```

ex 21
```
...
int f1/13 - 15
channel-group 3 mode on
int port-channel 1
switchp mode trunk
...
```


TODO: install freeradius in the VMS, add VMS to gns3
