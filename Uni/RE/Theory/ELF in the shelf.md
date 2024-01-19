## The Process™

Preprocessing -> Compiling -> ? -> Linking

### gcc tips n' tricks™
`gcc -E -o <name> <file.c>->` preprocess
`gcc -masm intel -S -o <name.s> <file.c>` -> compile to asm (intel)
`gcc -c -o <name.o> <file.c>` -> compile to object (binary)

`ldd`  -> see which libraries are linked in ELF
`nm` -> list symbols from object file


	undefined objects -> N existe no nosso programa, definted by dynamic linker

![[Pasted image 20230324163850.png]]

whats a symbol? names that id addrs of a binary
since only symbols in .dyntab are needed the others can be removed -> **stripping**
(binary size goes down) (tbm inclui debug symbols e stuff)

## Object Sections
![[Pasted image 20230324164546.png]]
