**File 1 -> JFIF (JPEG)**

### \[**--Methodology--**]
File: No results ('data')
Strings: 
![[Pasted image 20230219185331.png]]

File Signature: 00000000: 0000 0000 0010 4a46 4946 0001 0100 0001  ......JFIF......

Observations: 
Magic Bytes have been wiped, which leads to 'file' not being able to detect what is the correct filetype. However, the text JFIF gives us a very good clue. The start and end-of-image markers match with the ones of a jfif jpg/jpeg as well (FF DA and FF D9). [source](https://en.wikipedia.org/wiki/JPEG_File_Interchange_Format)

After inserting the magic bytes corresponding to those of a JFIF JPEG (FF D8 FF E0), running file on it yields us the following:

┌──(kali㉿lahabrea)-[~/Downloads/unknown_FILES]
└─$ file 1_altered 
1_altered: JPEG image data, JFIF standard 1.01, aspect ratio, density 1x1, segment length 16, progressive, precision 8, 630x354, components 3

Binwalk doesn't point towards the presence of any other file hidden. (and the end image IS at the end of the file) and 30kb is consistent with an image would be expected to be

This is the image contained within the file: (ha-ha)
![[Pasted image 20230219185148.png]]

