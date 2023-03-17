**File 4 -> a TOTALLY NORMAL ZIP no sus**

Analysis with File:
![[Pasted image 20230220212656.png]]

Analysis with Binwalk:
![[Pasted image 20230220212805.png]]

Magic bytes: **50 4B 03 04**
This is yet another zip file. This time, binwalk cannot detect any files, which means it's likely an actually compressed file.
Opening it with a hex editor reveals it to be quite random in its structure, further supporting this idea.
mf
this is a zip bomb

![[Pasted image 20230220213159.png]]

thank you linux

it was sus
![[Pasted image 20230220213226.png]]
rude.