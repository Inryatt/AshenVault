**FIle 16 -> x**

File output: 
Binwalk output: 



```bash                                                                                                             
┌──(kali㉿lahabrea)-[~/Downloads/unknown_FILES]
└─$ binwalk 16   

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PDF document, version: "1.5"
76            0x4C            Zlib compressed data, best compression
288           0x120           Zlib compressed data, best compression
11063         0x2B37          Zlib compressed data, best compression
11826         0x2E32          Zlib compressed data, best compression
128220        0x1F4DC         MySQL MISAM index file Version 3
184852        0x2D214         MySQL MISAM compressed data file Version 1

```

Strings and Cat: 

**-- Observations --**
![[Pasted image 20230224152901.png]]
pretty



File has a proper pdf inside, some compressed files and this ?????


/F8 9.9626 Tf 148.712 707.125 Td [(Hello)-333(w)27(orld!)]TJ 154.421 -567.87 Td [(1)]TJ
ET
                                 