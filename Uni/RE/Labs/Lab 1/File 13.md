**FIle x -> x**

File output: 
Binwalk output: 
``24            0x18            PDF document, version: "1.4"``


Strings and Cat: 

**-- Observations -- **

Cannot be opened with default reader, displays "document is damaged".


below the pdf header there seemed to be an jpg
deleted header and added the missing bytes for jpg

we get a weird tux that seems encrypted with ECB
![[Pasted image 20230224142014.png]]


