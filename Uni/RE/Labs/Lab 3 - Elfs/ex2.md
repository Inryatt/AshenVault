disassembly of plt:
```

Disassembly of section .plt.sec:

0000000000001280 <gzclose@plt>:
    1280:	f3 0f 1e fa          	endbr64
    1284:	f2 ff 25 2d 4c 00 00 	bnd jmp QWORD PTR [rip+0x4c2d]        # 5eb8 <gzclose@Base>
    128b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

0000000000001290 <free@plt>:
    1290:	f3 0f 1e fa          	endbr64
    1294:	f2 ff 25 25 4c 00 00 	bnd jmp QWORD PTR [rip+0x4c25]        # 5ec0 <free@GLIBC_2.2.5>
    129b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

00000000000012a0 <compress@plt>:
    12a0:	f3 0f 1e fa          	endbr64
    12a4:	f2 ff 25 1d 4c 00 00 	bnd jmp QWORD PTR [rip+0x4c1d]        # 5ec8 <compress@Base>
    12ab:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

00000000000012b0 <inflate@plt>:
    12b0:	f3 0f 1e fa          	endbr64
    12b4:	f2 ff 25 15 4c 00 00 	bnd jmp QWORD PTR [rip+0x4c15]        # 5ed0 <inflate@Base>
    12bb:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

00000000000012c0 <puts@plt>:
    12c0:	f3 0f 1e fa          	endbr64
    12c4:	f2 ff 25 0d 4c 00 00 	bnd jmp QWORD PTR [rip+0x4c0d]        # 5ed8 <puts@GLIBC_2.2.5>
    12cb:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

00000000000012d0 <gzgets@plt>:
    12d0:	f3 0f 1e fa          	endbr64
    12d4:	f2 ff 25 05 4c 00 00 	bnd jmp QWORD PTR [rip+0x4c05]        # 5ee0 <gzgets@Base>
    12db:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

00000000000012e0 <gzgetc@plt>:
    12e0:	f3 0f 1e fa          	endbr64
    12e4:	f2 ff 25 fd 4b 00 00 	bnd jmp QWORD PTR [rip+0x4bfd]        # 5ee8 <gzgetc@Base>
    12eb:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

00000000000012f0 <gzungetc@plt>:
    12f0:	f3 0f 1e fa          	endbr64
    12f4:	f2 ff 25 f5 4b 00 00 	bnd jmp QWORD PTR [rip+0x4bf5]        # 5ef0 <gzungetc@ZLIB_1.2.0.2>
    12fb:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

0000000000001300 <gzprintf@plt>:
    1300:	f3 0f 1e fa          	endbr64
    1304:	f2 ff 25 ed 4b 00 00 	bnd jmp QWORD PTR [rip+0x4bed]        # 5ef8 <gzprintf@Base>
    130b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

0000000000001310 <uncompress@plt>:
    1310:	f3 0f 1e fa          	endbr64
    1314:	f2 ff 25 e5 4b 00 00 	bnd jmp QWORD PTR [rip+0x4be5]        # 5f00 <uncompress@Base>
    131b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

0000000000001320 <strlen@plt>:
    1320:	f3 0f 1e fa          	endbr64
    1324:	f2 ff 25 dd 4b 00 00 	bnd jmp QWORD PTR [rip+0x4bdd]        # 5f08 <strlen@GLIBC_2.2.5>
    132b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

0000000000001330 <__stack_chk_fail@plt>:
    1330:	f3 0f 1e fa          	endbr64
    1334:	f2 ff 25 d5 4b 00 00 	bnd jmp QWORD PTR [rip+0x4bd5]        # 5f10 <__stack_chk_fail@GLIBC_2.4>
    133b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

0000000000001340 <gzseek@plt>:
    1340:	f3 0f 1e fa          	endbr64
    1344:	f2 ff 25 cd 4b 00 00 	bnd jmp QWORD PTR [rip+0x4bcd]        # 5f18 <gzseek@Base>
    134b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

0000000000001350 <printf@plt>:
    1350:	f3 0f 1e fa          	endbr64
    1354:	f2 ff 25 c5 4b 00 00 	bnd jmp QWORD PTR [rip+0x4bc5]        # 5f20 <printf@GLIBC_2.2.5>
    135b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

0000000000001360 <deflate@plt>:
    1360:	f3 0f 1e fa          	endbr64
    1364:	f2 ff 25 bd 4b 00 00 	bnd jmp QWORD PTR [rip+0x4bbd]        # 5f28 <deflate@Base>
    136b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

0000000000001370 <deflateParams@plt>:
    1370:	f3 0f 1e fa          	endbr64
    1374:	f2 ff 25 b5 4b 00 00 	bnd jmp QWORD PTR [rip+0x4bb5]        # 5f30 <deflateParams@Base>
    137b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

0000000000001380 <calloc@plt>:
    1380:	f3 0f 1e fa          	endbr64
    1384:	f2 ff 25 ad 4b 00 00 	bnd jmp QWORD PTR [rip+0x4bad]        # 5f38 <calloc@GLIBC_2.2.5>
    138b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

0000000000001390 <strcmp@plt>:
    1390:	f3 0f 1e fa          	endbr64
    1394:	f2 ff 25 a5 4b 00 00 	bnd jmp QWORD PTR [rip+0x4ba5]        # 5f40 <strcmp@GLIBC_2.2.5>
    139b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

00000000000013a0 <deflateInit_@plt>:
    13a0:	f3 0f 1e fa          	endbr64
    13a4:	f2 ff 25 9d 4b 00 00 	bnd jmp QWORD PTR [rip+0x4b9d]        # 5f48 <deflateInit_@Base>
    13ab:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

00000000000013b0 <gzread@plt>:
    13b0:	f3 0f 1e fa          	endbr64
    13b4:	f2 ff 25 95 4b 00 00 	bnd jmp QWORD PTR [rip+0x4b95]        # 5f50 <gzread@Base>
    13bb:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

00000000000013c0 <fprintf@plt>:
    13c0:	f3 0f 1e fa          	endbr64
    13c4:	f2 ff 25 8d 4b 00 00 	bnd jmp QWORD PTR [rip+0x4b8d]        # 5f58 <fprintf@GLIBC_2.2.5>
    13cb:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

00000000000013d0 <inflateEnd@plt>:
    13d0:	f3 0f 1e fa          	endbr64
    13d4:	f2 ff 25 85 4b 00 00 	bnd jmp QWORD PTR [rip+0x4b85]        # 5f60 <inflateEnd@Base>
    13db:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

00000000000013e0 <gzputs@plt>:
    13e0:	f3 0f 1e fa          	endbr64
    13e4:	f2 ff 25 7d 4b 00 00 	bnd jmp QWORD PTR [rip+0x4b7d]        # 5f68 <gzputs@Base>
    13eb:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

00000000000013f0 <inflateSetDictionary@plt>:
    13f0:	f3 0f 1e fa          	endbr64
    13f4:	f2 ff 25 75 4b 00 00 	bnd jmp QWORD PTR [rip+0x4b75]        # 5f70 <inflateSetDictionary@Base>
    13fb:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

0000000000001400 <gzerror@plt>:
    1400:	f3 0f 1e fa          	endbr64
    1404:	f2 ff 25 6d 4b 00 00 	bnd jmp QWORD PTR [rip+0x4b6d]        # 5f78 <gzerror@Base>
    140b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

0000000000001410 <gzputc@plt>:
    1410:	f3 0f 1e fa          	endbr64
    1414:	f2 ff 25 65 4b 00 00 	bnd jmp QWORD PTR [rip+0x4b65]        # 5f80 <gzputc@Base>
    141b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

0000000000001420 <deflateEnd@plt>:
    1420:	f3 0f 1e fa          	endbr64
    1424:	f2 ff 25 5d 4b 00 00 	bnd jmp QWORD PTR [rip+0x4b5d]        # 5f88 <deflateEnd@Base>
    142b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

0000000000001430 <inflateInit_@plt>:
    1430:	f3 0f 1e fa          	endbr64
    1434:	f2 ff 25 55 4b 00 00 	bnd jmp QWORD PTR [rip+0x4b55]        # 5f90 <inflateInit_@Base>
    143b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

0000000000001440 <gzopen@plt>:
    1440:	f3 0f 1e fa          	endbr64
    1444:	f2 ff 25 4d 4b 00 00 	bnd jmp QWORD PTR [rip+0x4b4d]        # 5f98 <gzopen@Base>
    144b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

0000000000001450 <zlibVersion@plt>:
    1450:	f3 0f 1e fa          	endbr64
    1454:	f2 ff 25 45 4b 00 00 	bnd jmp QWORD PTR [rip+0x4b45]        # 5fa0 <zlibVersion@Base>
    145b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

0000000000001460 <exit@plt>:
    1460:	f3 0f 1e fa          	endbr64
    1464:	f2 ff 25 3d 4b 00 00 	bnd jmp QWORD PTR [rip+0x4b3d]        # 5fa8 <exit@GLIBC_2.2.5>
    146b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

0000000000001470 <fwrite@plt>:
    1470:	f3 0f 1e fa          	endbr64
    1474:	f2 ff 25 35 4b 00 00 	bnd jmp QWORD PTR [rip+0x4b35]        # 5fb0 <fwrite@GLIBC_2.2.5>
    147b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

0000000000001480 <gztell@plt>:
    1480:	f3 0f 1e fa          	endbr64
    1484:	f2 ff 25 2d 4b 00 00 	bnd jmp QWORD PTR [rip+0x4b2d]        # 5fb8 <gztell@Base>
    148b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

0000000000001490 <zlibCompileFlags@plt>:
    1490:	f3 0f 1e fa          	endbr64
    1494:	f2 ff 25 25 4b 00 00 	bnd jmp QWORD PTR [rip+0x4b25]        # 5fc0 <zlibCompileFlags@ZLIB_1.2.0.2>
    149b:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

00000000000014a0 <deflateSetDictionary@plt>:
    14a0:	f3 0f 1e fa          	endbr64
    14a4:	f2 ff 25 1d 4b 00 00 	bnd jmp QWORD PTR [rip+0x4b1d]        # 5fc8 <deflateSetDictionary@Base>
    14ab:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]

00000000000014b0 <inflateSync@plt>:
    14b0:	f3 0f 1e fa          	endbr64
    14b4:	f2 ff 25 15 4b 00 00 	bnd jmp QWORD PTR [rip+0x4b15]        # 5fd0 <inflateSync@Base>
    14bb:	0f 1f 44 00 00       	nop    DWORD PTR [rax+rax*1+0x0]
```


```asm



Disassembly of section .plt:

0000000000001020 <.plt>:
    1020:	ff 35 82 4e 00 00    	push   QWORD PTR [rip+0x4e82]        # 5ea8 <_GLOBAL_OFFSET_TABLE_+0x8>
    1026:	f2 ff 25 83 4e 00 00 	bnd jmp QWORD PTR [rip+0x4e83]        # 5eb0 <_GLOBAL_OFFSET_TABLE_+0x10>
    102d:	0f 1f 00             	nop    DWORD PTR [rax]
    1030:	f3 0f 1e fa          	endbr64
    1034:	68 00 00 00 00       	push   0x0
    1039:	f2 e9 e1 ff ff ff    	bnd jmp 1020 <_init+0x20>
    103f:	90                   	nop
    1040:	f3 0f 1e fa          	endbr64
    1044:	68 01 00 00 00       	push   0x1
    1049:	f2 e9 d1 ff ff ff    	bnd jmp 1020 <_init+0x20>
    104f:	90                   	nop
    1050:	f3 0f 1e fa          	endbr64
    1054:	68 02 00 00 00       	push   0x2
    1059:	f2 e9 c1 ff ff ff    	bnd jmp 1020 <_init+0x20>
    105f:	90                   	nop
    1060:	f3 0f 1e fa          	endbr64
    1064:	68 03 00 00 00       	push   0x3
    1069:	f2 e9 b1 ff ff ff    	bnd jmp 1020 <_init+0x20>
    106f:	90                   	nop
    1070:	f3 0f 1e fa          	endbr64
    1074:	68 04 00 00 00       	push   0x4
    1079:	f2 e9 a1 ff ff ff    	bnd jmp 1020 <_init+0x20>
    107f:	90                   	nop
    1080:	f3 0f 1e fa          	endbr64
    1084:	68 05 00 00 00       	push   0x5
    1089:	f2 e9 91 ff ff ff    	bnd jmp 1020 <_init+0x20>
    108f:	90                   	nop
    1090:	f3 0f 1e fa          	endbr64
    1094:	68 06 00 00 00       	push   0x6
    1099:	f2 e9 81 ff ff ff    	bnd jmp 1020 <_init+0x20>
    109f:	90                   	nop
    10a0:	f3 0f 1e fa          	endbr64
    10a4:	68 07 00 00 00       	push   0x7
    10a9:	f2 e9 71 ff ff ff    	bnd jmp 1020 <_init+0x20>
    10af:	90                   	nop
    10b0:	f3 0f 1e fa          	endbr64
    10b4:	68 08 00 00 00       	push   0x8
    10b9:	f2 e9 61 ff ff ff    	bnd jmp 1020 <_init+0x20>
    10bf:	90                   	nop
    10c0:	f3 0f 1e fa          	endbr64
    10c4:	68 09 00 00 00       	push   0x9
    10c9:	f2 e9 51 ff ff ff    	bnd jmp 1020 <_init+0x20>
    10cf:	90                   	nop
    10d0:	f3 0f 1e fa          	endbr64
    10d4:	68 0a 00 00 00       	push   0xa
    10d9:	f2 e9 41 ff ff ff    	bnd jmp 1020 <_init+0x20>
    10df:	90                   	nop
    10e0:	f3 0f 1e fa          	endbr64
    10e4:	68 0b 00 00 00       	push   0xb
    10e9:	f2 e9 31 ff ff ff    	bnd jmp 1020 <_init+0x20>
    10ef:	90                   	nop
    10f0:	f3 0f 1e fa          	endbr64
    10f4:	68 0c 00 00 00       	push   0xc
    10f9:	f2 e9 21 ff ff ff    	bnd jmp 1020 <_init+0x20>
    10ff:	90                   	nop
    1100:	f3 0f 1e fa          	endbr64
    1104:	68 0d 00 00 00       	push   0xd
    1109:	f2 e9 11 ff ff ff    	bnd jmp 1020 <_init+0x20>
    110f:	90                   	nop
    1110:	f3 0f 1e fa          	endbr64
    1114:	68 0e 00 00 00       	push   0xe
    1119:	f2 e9 01 ff ff ff    	bnd jmp 1020 <_init+0x20>
    111f:	90                   	nop
    1120:	f3 0f 1e fa          	endbr64
    1124:	68 0f 00 00 00       	push   0xf
    1129:	f2 e9 f1 fe ff ff    	bnd jmp 1020 <_init+0x20>
    112f:	90                   	nop
    1130:	f3 0f 1e fa          	endbr64
    1134:	68 10 00 00 00       	push   0x10
    1139:	f2 e9 e1 fe ff ff    	bnd jmp 1020 <_init+0x20>
    113f:	90                   	nop
    1140:	f3 0f 1e fa          	endbr64
    1144:	68 11 00 00 00       	push   0x11
    1149:	f2 e9 d1 fe ff ff    	bnd jmp 1020 <_init+0x20>
    114f:	90                   	nop
    1150:	f3 0f 1e fa          	endbr64
    1154:	68 12 00 00 00       	push   0x12
    1159:	f2 e9 c1 fe ff ff    	bnd jmp 1020 <_init+0x20>
    115f:	90                   	nop
    1160:	f3 0f 1e fa          	endbr64
    1164:	68 13 00 00 00       	push   0x13
    1169:	f2 e9 b1 fe ff ff    	bnd jmp 1020 <_init+0x20>
    116f:	90                   	nop
    1170:	f3 0f 1e fa          	endbr64
    1174:	68 14 00 00 00       	push   0x14
    1179:	f2 e9 a1 fe ff ff    	bnd jmp 1020 <_init+0x20>
    117f:	90                   	nop
    1180:	f3 0f 1e fa          	endbr64
    1184:	68 15 00 00 00       	push   0x15
    1189:	f2 e9 91 fe ff ff    	bnd jmp 1020 <_init+0x20>
    118f:	90                   	nop
    1190:	f3 0f 1e fa          	endbr64
    1194:	68 16 00 00 00       	push   0x16
    1199:	f2 e9 81 fe ff ff    	bnd jmp 1020 <_init+0x20>
    119f:	90                   	nop
    11a0:	f3 0f 1e fa          	endbr64
    11a4:	68 17 00 00 00       	push   0x17
    11a9:	f2 e9 71 fe ff ff    	bnd jmp 1020 <_init+0x20>
    11af:	90                   	nop
    11b0:	f3 0f 1e fa          	endbr64
    11b4:	68 18 00 00 00       	push   0x18
    11b9:	f2 e9 61 fe ff ff    	bnd jmp 1020 <_init+0x20>
    11bf:	90                   	nop
    11c0:	f3 0f 1e fa          	endbr64
    11c4:	68 19 00 00 00       	push   0x19
    11c9:	f2 e9 51 fe ff ff    	bnd jmp 1020 <_init+0x20>
    11cf:	90                   	nop
    11d0:	f3 0f 1e fa          	endbr64
    11d4:	68 1a 00 00 00       	push   0x1a
    11d9:	f2 e9 41 fe ff ff    	bnd jmp 1020 <_init+0x20>
    11df:	90                   	nop
    11e0:	f3 0f 1e fa          	endbr64
    11e4:	68 1b 00 00 00       	push   0x1b
    11e9:	f2 e9 31 fe ff ff    	bnd jmp 1020 <_init+0x20>
    11ef:	90                   	nop
    11f0:	f3 0f 1e fa          	endbr64
    11f4:	68 1c 00 00 00       	push   0x1c
    11f9:	f2 e9 21 fe ff ff    	bnd jmp 1020 <_init+0x20>
    11ff:	90                   	nop
    1200:	f3 0f 1e fa          	endbr64
    1204:	68 1d 00 00 00       	push   0x1d
    1209:	f2 e9 11 fe ff ff    	bnd jmp 1020 <_init+0x20>
    120f:	90                   	nop
    1210:	f3 0f 1e fa          	endbr64
    1214:	68 1e 00 00 00       	push   0x1e
    1219:	f2 e9 01 fe ff ff    	bnd jmp 1020 <_init+0x20>
    121f:	90                   	nop
    1220:	f3 0f 1e fa          	endbr64
    1224:	68 1f 00 00 00       	push   0x1f
    1229:	f2 e9 f1 fd ff ff    	bnd jmp 1020 <_init+0x20>
    122f:	90                   	nop
    1230:	f3 0f 1e fa          	endbr64
    1234:	68 20 00 00 00       	push   0x20
    1239:	f2 e9 e1 fd ff ff    	bnd jmp 1020 <_init+0x20>
    123f:	90                   	nop
    1240:	f3 0f 1e fa          	endbr64
    1244:	68 21 00 00 00       	push   0x21
    1249:	f2 e9 d1 fd ff ff    	bnd jmp 1020 <_init+0x20>
    124f:	90                   	nop
    1250:	f3 0f 1e fa          	endbr64
    1254:	68 22 00 00 00       	push   0x22
    1259:	f2 e9 c1 fd ff ff    	bnd jmp 1020 <_init+0x20>
    125f:	90                   	nop
    1260:	f3 0f 1e fa          	endbr64
    1264:	68 23 00 00 00       	push   0x23
    1269:	f2 e9 b1 fd ff ff    	bnd jmp 1020 <_init+0x20>
    126f:	90                   	nop


```
