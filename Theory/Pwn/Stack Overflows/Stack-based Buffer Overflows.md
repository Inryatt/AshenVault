## Taking Control of the Instruction Pointer
EIP/RIP

![[Pasted image 20230628122204.png]]

Writing out-of-bounds allows to write on top of the EIP, overwriting it.

How?
1. **Determine the Offset** - how many bytes do we need to overwrite the buffer?
2. 