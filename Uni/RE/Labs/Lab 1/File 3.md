
**File 3 -> DOCX(MSWord 2007)**


Analysis with file:
![[Pasted image 20230220211421.png]]

Analysis with binwalk:
                                                                               
┌──(kali㉿lahabrea)-[~/Downloads/unknown_FILES]
└─$ binwalk 3

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
1062          0x426           Zip archive data, at least v2.0 to extract, compressed size: 243, uncompressed size: 590, name: _rels/.rels
1866          0x74A           Zip archive data, at least v2.0 to extract, compressed size: 414, uncompressed size: 2074, name: word/_rels/document.xml.rels
2602          0xA2A           Zip archive data, at least v2.0 to extract, compressed size: 13568, uncompressed size: 137810, name: word/document.xml
16217         0x3F59          Zip archive data, at least v2.0 to extract, compressed size: 632, uncompressed size: 1608, name: word/footnotes.xml
16897         0x4201          Zip archive data, at least v2.0 to extract, compressed size: 615, uncompressed size: 1572, name: word/endnotes.xml
17559         0x4497          Zip archive data, at least v2.0 to extract, compressed size: 199046, uncompressed size: 386440, name: word/fonts/font3.odttf
216657        0x34E51         Zip archive data, at least v1.0 to extract, compressed size: 4693, uncompressed size: 4693, name: word/media/image3.png
221401        0x360D9         Zip archive data, at least v2.0 to extract, compressed size: 412062, uncompressed size: 700180, name: word/fonts/font5.odttf
633515        0x9AAAB         Zip archive data, at least v2.0 to extract, compressed size: 181018, uncompressed size: 353824, name: word/fonts/font1.odttf
814585        0xC6DF9         Zip archive data, at least v2.0 to extract, compressed size: 168660, uncompressed size: 333616, name: word/fonts/font2.odttf
983297        0xF0101         Zip archive data, at least v1.0 to extract, compressed size: 4625, uncompressed size: 4625, name: word/media/image4.png
987973        0xF1345         Zip archive data, at least v2.0 to extract, compressed size: 184676, uncompressed size: 356980, name: word/fonts/font4.odttf
1172701       0x11E4DD        Zip archive data, at least v2.0 to extract, compressed size: 119810, uncompressed size: 205748, name: word/fonts/font6.odttf
1292563       0x13B913        Zip archive data, at least v1.0 to extract, compressed size: 1526, uncompressed size: 1526, name: word/media/image2.png
1294140       0x13BF3C        Zip archive data, at least v1.0 to extract, compressed size: 311, uncompressed size: 311, name: word/media/image1.gif
1294502       0x13C0A6        Zip archive data, at least v2.0 to extract, compressed size: 1169, uncompressed size: 4376, name: word/theme/theme1.xml
1295722       0x13C56A        Zip archive data, at least v2.0 to extract, compressed size: 1297, uncompressed size: 4084, name: word/settings.xml
1297066       0x13CAAA        Zip archive data, at least v2.0 to extract, compressed size: 237, uncompressed size: 330, name: customXml/itemProps1.xml
1297397       0x13CBF5        Zip archive data, at least v2.0 to extract, compressed size: 225, uncompressed size: 341, name: customXml/itemProps2.xml
1297716       0x13CD34        Zip archive data, at least v2.0 to extract, compressed size: 138, uncompressed size: 216, name: customXml/item2.xml
1297943       0x13CE17        Zip archive data, at least v2.0 to extract, compressed size: 195, uncompressed size: 296, name: customXml/_rels/item2.xml.rels
1298462       0x13D01E        Zip archive data, at least v2.0 to extract, compressed size: 185, uncompressed size: 289, name: word/_rels/numbering.xml.rels
1298706       0x13D112        Zip archive data, at least v2.0 to extract, compressed size: 223, uncompressed size: 949, name: word/_rels/fontTable.xml.rels
1298988       0x13D22C        Zip archive data, at least v2.0 to extract, compressed size: 194, uncompressed size: 296, name: customXml/_rels/item1.xml.rels
1299506       0x13D432        Zip archive data, at least v2.0 to extract, compressed size: 140, uncompressed size: 192, name: customXml/item1.xml
1299735       0x13D517        Zip archive data, at least v2.0 to extract, compressed size: 428, uncompressed size: 800, name: docProps/core.xml
1300474       0x13D7FA        Zip archive data, at least v2.0 to extract, compressed size: 2373, uncompressed size: 21236, name: word/numbering.xml
1302895       0x13E16F        Zip archive data, at least v2.0 to extract, compressed size: 4905, uncompressed size: 40755, name: word/styles.xml
1307845       0x13F4C5        Zip archive data, at least v2.0 to extract, compressed size: 187, uncompressed size: 260, name: word/webSettings.xml
1308082       0x13F5B2        Zip archive data, at least v2.0 to extract, compressed size: 781, uncompressed size: 2576, name: word/fontTable.xml
1308911       0x13F8EF        Zip archive data, at least v2.0 to extract, compressed size: 494, uncompressed size: 1001, name: docProps/app.xml
1311859       0x140473        End of Zip archive, footer length: 22

--
This seems to be a doc(x) file, due to the presence of "word/".

After opening the file on a hex editor, we can see that the first two bytes are missing:
![[Pasted image 20230220212007.png]]
According to wikipedia, and based on previous suspicions:
![[Pasted image 20230220211956.png]]

the 3rd and 4th bytes match, and the correct signature for this file should be **50 4B 03 04**

After changing these bytes:
![[Pasted image 20230220212240.png]]

Opening it in Google Docs, we can see that this is a Calibre DOCX sample file.
![[Pasted image 20230220212541.png]]