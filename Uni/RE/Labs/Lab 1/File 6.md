**FIle 6 -> PNG**

File output: "data"
Binwalk output: "Zlib compressed data, compressed"
Strings and Cat: Gibberish

File couldn't be unzipped.

Upon opening in hex editor, first 4 bytes have been wiped but at start of file is present the string "IHDR".

Googling this leads to [this page](http://www.libpng.org/pub/png/spec/1.2/PNG-Chunks.html)

""A valid PNG image must contain an IHDR chunk, one or more IDAT chunks, and an IEND chunk.""

![[Pasted image 20230221161811.png]]
IHDR and IDAT can be cleanly seen here in the file, suggesting it is a PNG.
The IEND is also present at the end.

The magic bytes of a PNG are **`89 50 4E 47 0D 0A 1A 0A`** .

Half of those are missing, and were patched in.

Result:
![[Pasted image 20230221162105.png]]