
When a program is in execution, its segments are mapped to memory
![[Pasted image 20230627144503.png]]

## .text
Contains the assembler instructions of the program.

>[!danger] **READ-ONLY**
> Writing to this area will result in a segfault!


## .data
**Global** and **Static** variables, explicitly initialized by the program.

## .bss
Statically allocated variables, **represented by 0 bits**.

## Heap
Grows from lower to higher memory addresses

## Stack

![[Pasted image 20230630141218.png]]

Control symbols and data mixed together.

Grows from higher to lower memory addresses.
Last-In-First-Out data structure.
Stores return addresses, parameters, and sometimes frame pointers.
C/C++ locals are stored here.
Contents accessed via **stack pointer.**

**DEP/ASLR** protect this area of memory

**DEP** - Data Execution Prevention marks regions of memory as read only - where user input is stored. Memory is marked as NX (non-executable)
**ASLR** - Address Space Layout Randomization scrambles where everything is stopped in order to make ROP more difficult.


