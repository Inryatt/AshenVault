**FIle 8 -> Lenna (an image)/ art**
possible pgm?

File output:  'data'
Binwalk output: None
Strings and Cat: Lots of long, incoherent strings.

**-- Observations -- **

First 1024 bytes are filler, with a certain pattern.
![[Pasted image 20230221170017.png]]

The entropy of the file is overall low:
![[Pasted image 20230221170721.png]]

According to Cyberchef, the entropy of the file is around 3.5 - matching with normal text.

After tinkering with the visualization on Veles, the text present seems to be, in fact, an image.


![[Pasted image 20230221184656.png]]
To obtain this, the number of columns was adjusted so that the first batch of coherent gibberish became a single line (from 00 00 00 00 to FF FF FF 00 )

![[Screenshot from 2023-02-21 20-23-06.png]]
this is the image hidden, presumably tiled. (I cant get a bigger screenshot :c )

ITS UPSIDE DOWN

![[Pasted image 20230222103436.png]]

after further research (inquiring local finn) it seems this is a famous image known as the Lena Image ( but still inverted)

![[Pasted image 20230222103519.png]]

which has some quite interesting lore surrounding it

https://www.youtube.com/watch?v=yCdwm2vo09I
(Source: Saga <3 )

Since the image seems to be repeated (originally thought a bug), yet each instance of it being comprised of different ASCII characters, this may be a proper (yet obscure) image format, uncompressed.


https://people.sc.fsu.edu/~jburkardt/data/pgmb/pgmb.html
https://people.sc.fsu.edu/~jburkardt/data/data.html
