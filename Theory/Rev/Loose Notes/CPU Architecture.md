
A Von-Neumann-based cpu architecture presents four units:
	- Memory
	- Control Unit
	- ALU (Arithmetic Logical Unit)
	- I/O 

ALU and CU are combined in the Central Processing Unit (well well well) - It is responsible for executing instructions (sequentially) & flow control.

Different Architectures:
	- x86/i386
	- x86-64/amd64
	- ARM

Each architecture has an Instruction Set Architecture (ISA)
	- CISC - Complex Instruction Set Computing
	- RISC - Reduced Instruction Set Computing
	- VLIW - Very Long Instruction Word
	- EPIC - Explicitly Parallel Instruction Computing

Instruction Cycle - How CPU processes instructions

1. FETCH
		- Read next instruction address from **Instruction Address Register** (IAR). It is loaded from Cache/RAM to **Instruction Register** (IR)
2. DECODE
	- Instruction is decoded
3. FETCH OPERANDS
	- If needed, operands are loaded from memory/cache to registers.
4. EXECUTE
5. UPDATE INSTRUCTION POINTER
	- (If no jump operation was done) IAR is increased by the len of the instruction, so that it points to the next instruction.
	
#### Data registers

|**32-bit Register**|**64-bit Register**|**Description**|
|---|---|---|
|`EAX`|`RAX`|Accumulator is used in input/output and for arithmetic operations|
|`EBX`|`RBX`|Base is used in indexed addressing|
|`ECX`|`RCX`|Counter is used to rotate instructions and count loops|
|`EDX`|`RDX`|Data is used for I/O and in arithmetic operations for multiply and divide operations involving large values|

---

#### Pointer registers

|**32-bit Register**|**64-bit Register**|**Description**|
|---|---|---|
|`EIP`|`RIP`|Instruction Pointer stores the offset address of the next instruction to be executed|
|`ESP`|`RSP`|Stack Pointer points to the *top* of the stack|
|`EBP`|`RBP`|Base Pointer is also known as `Stack Base Pointer` or `Frame Pointer` that points to the *base* of the stack|




### Calling a Function

`Stack Frames`  allocate the required memory in the stack for the corresponding function. A stack frame defines a frame of data with the beginning (`EBP`) and the end (`ESP`) that is pushed onto the stack when a function is called.
the first step is to store the `previous EBP` position on the stack, which can be restored after the function completes

---

#### Index registers

|**Register 32-bit**|**Register 64-bit**|**Description**|
|---|---|---|
|`ESI`|`RSI`|Source Index is used as a pointer from a source for string operations|
|`EDI`|`RDI`|Destination is used as a pointer to a destination for string operations|

#### Prologue

Setup for a function being called (inside the function itself (depending on calling convention))

```shell-session
(gdb) disas bowfunc 

Dump of assembler code for function bowfunc:
   0x0000054d <+0>:	    push   ebp       # <---- 1. Stores previous EBP
   0x0000054e <+1>:	    mov    ebp,esp   # <---- 2. Creates new Stack Frame
   0x00000550 <+3>:	    push   ebx
   0x00000551 <+4>:	    sub    esp,0x404 # <---- 3. Moves ESP to the top
   <...SNIP...>
   0x00000580 <+51>:	leave  
   0x00000581 <+52>:	ret    
```

These three instructions represent the so-called `Prologue`.

And to exit the function/stack frame the opposite is done

#### Epilogue

Epilogue

```shell-session
(gdb) disas bowfunc 

Dump of assembler code for function bowfunc:
   0x0000054d <+0>:	    push   ebp       
   0x0000054e <+1>:	    mov    ebp,esp   
   0x00000550 <+3>:	    push   ebx
   0x00000551 <+4>:	    sub    esp,0x404 
   <...SNIP...>
   0x00000580 <+51>:	leave  # <----------------------
   0x00000581 <+52>:	ret    # <--- Leave stack frame
```


During the epilogue, the `ESP` is replaced by the current `EBP`, and its value is reset to the value it had before in the prologue. The epilogue is relatively short.

### The call instruction

The `call` instruction is used to call a function and performs two operations:

1. it pushes the return address onto the `stack` so that the execution of the program can be continued after the function has successfully fulfilled its goal,
2. it changes the `instruction pointer` (`EIP`) to the call destination and starting execution there.

