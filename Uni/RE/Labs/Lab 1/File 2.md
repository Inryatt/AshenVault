**File 2 -> JPEG**

File 2 also had its magic bytes wiped. It ends in FF D9  (JPG End of Image marker) and there's two quantization tables present (Start with FF DB 00 43)

After inserting the magic bytes for JPEG, (FF D8 FF E0), we get the following:

$ file 2
2: JPEG image data, baseline, precision 8, 1000x627, components 3

However the image cannot be read. 

Copy pasting the header for file 1 before the marker for image start (FF DA) yields no results.
Since there's multiple quantization tables/hoffman tables, this is a progressive dct jpeg. Therefore, the correct magic bytes are **FF D8 FF C2.**

To analyze this file, this was used as reference:
[corkami jpeg (long)](https://github.com/corkami/formats/blob/master/image/jpeg.md)
[corkami jpeg (short)](https://github.com/corkami/pics/blob/master/binary/JPG.png) (TL;DR)


The file has:
2 Quantization Tables (FF DB)
1 Start of Frame (FF C0)
4 Hoffman Tables (FF C4)

...which is in line with what's described in the above mentioned corkami link.

The rest of the missing header will be added in, and the magic bytes changed back to FF D8 FF E0, due to exiftool recognizing it not as progressive dct but as baseline:

![[Pasted image 20230220210849.png]]

The image is fixed! 
![[Pasted image 20230220210920.png]]