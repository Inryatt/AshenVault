
ESW1
```
conf t
aaa new-model
aaa authent dot1x deafault group radius
dot1x system-auth-control
radius-server host 10.0.0.100 auth-port 1812 key radiuskey
int f1/0
dot1x port-control auto
end 
wr


``` 

```




```


