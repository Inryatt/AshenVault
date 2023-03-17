**File 5 -> PDF**

File output:
![[Pasted image 20230220213827.png]]
(i bet this is either a polyglot, or an issue of PoC||GTFO)
Binwalk output:

                                                                          
┌──(kali㉿lahabrea)-[~/Downloads/unknown_FILES]
└─$ binwalk 5

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
6             0x6             PDF document, version: "1.5"
11818         0x2E2A          PDF document, version: "1.6"
11889         0x2E71          Zlib compressed data, default compression
12484         0x30C4          JPEG image data, JFIF standard 1.01
76376         0x12A58         Zlib compressed data, default compression
100370        0x18812         JPEG image data, JFIF standard 1.01
106033        0x19E31         Zlib compressed data, default compression
110013        0x1ADBD         JPEG image data, JFIF standard 1.01
146190        0x23B0E         Zlib compressed data, default compression
158266        0x26A3A         Zlib compressed data, default compression
158463        0x26AFF         Zlib compressed data, default compression
159174        0x26DC6         JPEG image data, JFIF standard 1.01
159914        0x270AA         Zlib compressed data, default compression
162490        0x27ABA         JPEG image data, JFIF standard 1.01
164325        0x281E5         Zlib compressed data, default compression
167285        0x28D75         JPEG image data, JFIF standard 1.01
168539        0x2925B         Zlib compressed data, default compression
172023        0x29FF7         JPEG image data, JFIF standard 1.01
172727        0x2A2B7         Zlib compressed data, default compression
174784        0x2AAC0         JPEG image data, JFIF standard 1.01
266521        0x41119         JPEG image data, JFIF standard 1.01
354391        0x56857         Zlib compressed data, default compression
384961        0x5DFC1         Zlib compressed data, default compression
385416        0x5E188         JPEG image data, JFIF standard 1.01
503819        0x7B00B         Zlib compressed data, default compression
543003        0x8491B         Zlib compressed data, default compression
543203        0x849E3         Zlib compressed data, default compression
543938        0x84CC2         JPEG image data, JFIF standard 1.01
552236        0x86D2C         JPEG image data, JFIF standard 1.01
555950        0x87BAE         Microsoft executable, MS-DOS
622558        0x97FDE         Certificate in DER format (x509 v3), header length: 4, sequence length: 12418
622560        0x97FE0         Certificate in DER format (x509 v3), header length: 4, sequence length: 12418
684531        0xA71F3         Zlib compressed data, default compression
684729        0xA72B9         Zlib compressed data, default compression
685405        0xA755D         JPEG image data, JFIF standard 1.01
887231        0xD89BF         Zlib compressed data, default compression
887429        0xD8A85         Zlib compressed data, default compression
888140        0xD8D4C         JPEG image data, JFIF standard 1.01
917933        0xE01AD         JPEG image data, JFIF standard 1.01
1058852       0x102824        Zlib compressed data, default compression
1059050       0x1028EA        Zlib compressed data, default compression
1060137       0x102D29        JPEG image data, JFIF standard 1.01
1174392       0x11EB78        Zlib compressed data, default compression
1174590       0x11EC3E        Zlib compressed data, default compression
1175600       0x11F030        Zlib compressed data, default compression
1175798       0x11F0F6        Zlib compressed data, default compression
1176358       0x11F326        Zlib compressed data, default compression
1176558       0x11F3EE        Zlib compressed data, default compression
1177572       0x11F7E4        Zlib compressed data, default compression
1177770       0x11F8AA        Zlib compressed data, default compression
1178575       0x11FBCF        JPEG image data, JFIF standard 1.01
1248306       0x130C32        JPEG image data, JFIF standard 1.01
1250530       0x1314E2        Zlib compressed data, default compression
1252151       0x131B37        Zlib compressed data, default compression
1252478       0x131C7E        Zlib compressed data, default compression
1252658       0x131D32        Zlib compressed data, default compression
1253445       0x132045        JPEG image data, JFIF standard 1.01
1304146       0x13E652        Zlib compressed data, default compression
1304476       0x13E79C        Zlib compressed data, default compression
1304661       0x13E855        Zlib compressed data, default compression
1305448       0x13EB68        JPEG image data, JFIF standard 1.01
1367884       0x14DF4C        Zlib compressed data, default compression
1368213       0x14E095        Zlib compressed data, default compression
1368396       0x14E14C        Zlib compressed data, default compression
1369191       0x14E467        JPEG image data, JFIF standard 1.01
1621096       0x18BC68        Zlib compressed data, default compression
1622304       0x18C120        JPEG image data, JFIF standard 1.01
1628741       0x18DA45        Zlib compressed data, default compression
1629972       0x18DF14        Zlib compressed data, default compression
1630302       0x18E05E        Zlib compressed data, default compression
1630486       0x18E116        Zlib compressed data, default compression
1631061       0x18E355        JPEG image data, JFIF standard 1.01
1710922       0x1A1B4A        Zlib compressed data, default compression
1711252       0x1A1C94        Zlib compressed data, default compression
1711463       0x1A1D67        Zlib compressed data, default compression
1712122       0x1A1FFA        Zlib compressed data, default compression
1712323       0x1A20C3        Zlib compressed data, default compression
1713052       0x1A239C        JPEG image data, JFIF standard 1.01
1950801       0x1DC451        Zlib compressed data, default compression
1951945       0x1DC8C9        JPEG image data, JFIF standard 1.01
1958019       0x1DE083        Zlib compressed data, default compression
1959186       0x1DE512        Zlib compressed data, default compression
1959514       0x1DE65A        Zlib compressed data, default compression
1959701       0x1DE715        Zlib compressed data, default compression
1960570       0x1DEA7A        JPEG image data, JFIF standard 1.01
2077094       0x1FB1A6        Zlib compressed data, default compression
2077423       0x1FB2EF        Zlib compressed data, default compression
2077606       0x1FB3A6        Zlib compressed data, default compression
2078146       0x1FB5C2        JPEG image data, JFIF standard 1.01
2099575       0x200977        mcrypt 2.5 encrypted data, algorithm: "k", keysize: 146 bytes, mode: "L",
2261275       0x22811B        Zlib compressed data, default compression
2261604       0x228264        Zlib compressed data, default compression
2261786       0x22831A        Zlib compressed data, default compression
2262699       0x2286AB        JPEG image data, JFIF standard 1.01
2334618       0x239F9A        Zlib compressed data, default compression
2334948       0x23A0E4        Zlib compressed data, default compression
2335129       0x23A199        Zlib compressed data, default compression
2335704       0x23A3D8        Zlib compressed data, default compression
2335904       0x23A4A0        Zlib compressed data, default compression
2336500       0x23A6F4        Zlib compressed data, default compression
2337379       0x23AA63        JPEG image data, JFIF standard 1.01
2345811       0x23CB53        Zlib compressed data, default compression
2351721       0x23E269        Zlib compressed data, default compression
2351920       0x23E330        Zlib compressed data, default compression
2352422       0x23E526        Zlib compressed data, default compression
2352625       0x23E5F1        Zlib compressed data, default compression
2353273       0x23E879        Zlib compressed data, default compression
2353603       0x23E9C3        Zlib compressed data, default compression
2353784       0x23EA78        Zlib compressed data, default compression
2354919       0x23EEE7        Zlib compressed data, default compression
2355686       0x23F1E6        Zlib compressed data, default compression
2357434       0x23F8BA        Zlib compressed data, default compression
2357906       0x23FA92        Zlib compressed data, default compression
2367855       0x24216F        Zlib compressed data, default compression
2368850       0x242552        Zlib compressed data, default compression
2376857       0x244499        Zlib compressed data, default compression
2377754       0x24481A        Zlib compressed data, default compression
2382113       0x245921        Zlib compressed data, default compression
2382706       0x245B72        Zlib compressed data, default compression
2389241       0x2474F9        Zlib compressed data, default compression
2389864       0x247768        Zlib compressed data, default compression
2392731       0x24829B        Zlib compressed data, default compression
2393458       0x248572        Zlib compressed data, default compression
2397116       0x2493BC        Zlib compressed data, default compression
2397917       0x2496DD        Zlib compressed data, default compression
2402059       0x24A70B        Zlib compressed data, default compression
2402980       0x24AAA4        Zlib compressed data, default compression
2404831       0x24B1DF        Zlib compressed data, default compression



There are many files inside this one file.
Simply opening it yields this set of slides/Pdf:
![[Pasted image 20230220214054.png]]
(OxOPOSEC nice)

Opening it with an hex editor, it appears to be a PDF.
A file signature is present at 0x06: 25 50 44 46 -- a PDF.

![[Pasted image 20230220215719.png]]
