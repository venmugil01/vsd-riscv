# vsd_Squadron
The VSDSquadron Mini-Internship is a hands-on journey into VLSI chip design and the RISC-V architecture using open-source tools. It involves working with the compact VSDSquadron Mini RISC-V Development Board, which features a 32-bit RISC-V core, 16KB of flash memory, 2KB of SRAM, and operates at 24MHz. With 15 GPIO pins and support for I2C, SPI, and USART communication protocols, it provides the perfect platform to explore hardware interfacing and build real-time embedded projects while gaining a deeper understanding of the RISC-V ecosystem.
<details>
<summary><b>Task 1:</b> Installing RISC-V toolchain and Refer to C and RISC-V based lab videos </summary>   
<br>
 C-Based Lab

 Program that gives the sum of n numbers using C in leafpad editor."sumofn.c" is the filename
 save that leafpad code(ctrl+s) and close the window(ctrl+w)
 
 then in terminal run the saved c program by the following commands
 ````
gcc sum1ton.c
./a.out 
````

 ./a.out is used to check the result 

 ![c_code](https://github.com/user-attachments/assets/ed0f9d60-8b29-430a-ac68-3a0c0a9056ba)

RISC-V Based Lab
----
Now we are compiling the same code in RISCV 
compiling using command ```cat sum1ton.c```

![image](https://github.com/user-attachments/assets/1b02db9d-56bb-487e-901c-a70e05957dab)

For compiling the above C code in RISCV use command 
```
 riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
```

Command breakdown : 
 ````
riscv64-unknown-elf-gcc        : This is the cross-compiler for the 64-bit RISC-V architecture that generates ELF (Executable and Linkable Format) binaries.

-mabi=lp64                   : Sets the ABI (Application Binary Interface) to 'lp64', meaning long and pointer types are 64 bits

-march=rv64i                 : Specifies the target RISC-V architecture variant (in this case, RV64I: a 64-bit base integer instruction set).

-o sum1ton.o                 : Defines 'sumofn.o' as the name of the output object file generated after compilation.
````
After this open a new tab and type the command 

`` riscv64-unknown-elf-objdump -d sum1ton.o | less``

After compiling we will get the Assembly language code of it and now we can seaarch for main part of the code by using ``/main``

and the Assembly language for main function of the code is as :

![image](https://github.com/user-attachments/assets/c154a908-7cad-4fa6-bdb3-60b4351bc485)

using O1 there are 11 instructions.

Now we will check number of instructions using ``-Ofast``:

![image](https://github.com/user-attachments/assets/d2270c3c-9ede-4df3-aff6-2b1d47f6293a)

Even using Ofast there are 11 instructions 

Difference between -O1 and -Ofast 

`-O1`Applies basic optimizations to improve performance without making compilation too slow or complex. It’s a safe and balanced option that sticks to standard C behavior.

`-Ofast`
Pushes the compiler to apply aggressive optimizations for maximum speed, even if it means ignoring some language rules or sacrificing portability. It can make code run faster, but may also change how certain calculations behave.

</details>

<details>
<summary><b>Task 2:</b> Performing SPIKE simulation and Debugging the C code Using spike  </summary>   
<br>
What is Spike simulation?
Spike is a RISC-V ISA simulator used to run and test RISC-V programs. GCC compiles C/C++ code for RISC-V, and Spike simulates its execution. The command spike pk sum1ton.o runs the compiled code to check if the instructions work correctly and to display the program output.

![1a](https://github.com/user-attachments/assets/aacb19e5-b6ff-491c-ac7f-f73b080638a5)

![image](https://github.com/user-attachments/assets/fc1a786b-20fc-42ff-8d2e-96c13c337250)

In Debugger we Debug the Assembly Language by following the each instruction .At the address of `100b4` the register value of stack point `sp` is `0x0000003ffffffb50` and after completion of instruction`sp, sp, -16` ,the new value of register stack pointer is `0x0000003ffffffb40`
Instruction: `lui a0, %hi(LC1)`

LUI is an instruction in the RISC-V architecture that loads a 20-bit immediate value into the upper 20 bits of a 32-bit or 64-bit register. The lower 12 bits of the register are set to zero.
In the example, the instruction loads the upper 20 bits of a label (LC1) into the register a0

` addi`
Add Immediate
![image](https://github.com/user-attachments/assets/e8b72f51-cee7-4706-9fec-226a7d1eb7e9)

 Instruction:` addi a0, a0, %lo(LC1)`
Purpose: The ADDI instruction adds an immediate value (12-bit constant) to the value in a source register (rs1) and stores the result in a destination register (rd).

Task: Write a simple C program for a basic application and compile it using RISC-V GCC and simulate with SPIKE.

Application: Countdown Timer

The goal is to create a countdown timer that starts from a given value and decreases by one every second until it reaches zero.

Program Requirements:

Initialize the timer with a starting value (e.g., 10 seconds).

Display the current countdown value.

Decrease the timer value by one every second.

Stop the countdown when the timer reaches zero.

C program in leafpad
![image](https://github.com/user-attachments/assets/afae49a6-a270-46f6-9cb0-4bb279d1905d)

compilation

![p2](https://github.com/user-attachments/assets/e599dc0d-d3d6-45d5-9441-4f37e5fa23ee)

Assembly language code
![image](https://github.com/user-attachments/assets/3eeaa1d8-a54a-46cb-9bf0-54535674f4ed)

Debugging
![image](https://github.com/user-attachments/assets/84221d44-5adf-440b-a336-4ca27a4e2287)

</details>

<details>
<summary><b>Task 3:</b> Various RISCV instruction type and 32 bit instruction code for instructions from application code  </summary>   
<br>

RISCV Instruction types
There are 6 types of instruction 
 1.  R-Type (Register Type)
 2.  I-Type (Immediate Type)
 3.  S-Type (Store Type)
 4.  U-Type (Branch Type)
 5.  B-Type (Upper Immediate Type)
 6.  J-Type (Jump Type)

The base RV32I ISA, there are four core instruction formats (R/I/S/U), as shown in Base instruction formats. All are a fixed 32 bits in length.
![image](https://github.com/user-attachments/assets/6e63b0e1-acc9-4865-89ee-ba02534357f3)

1.R-Type:
--
R-Type instructions are typically used for register-to-register operations

Breakdown of the Fields:

 1. Opcode (bits 6-0):
   The 7-bit opcode identifies the type of operation and the instruction format. For R-Type instructions, the opcode specifies that the instruction is register-based.

 2. rd( bits 11:7):
   This bit is used for designation register where the output of the operation is written.
   
 3. funct3( bits 14:12) :
   This 3 bit is used for differentiate between categories of operations within the same opcode.

   R type operations:
| **funct3** | **Operation**                      |
|------------|------------------------------------|
| `000`      | Add / Sub (depends on `funct7`)   |
| `001`      | Shift Left Logical (SLL)          |
| `010`      | Set Less Than (SLT)               |
| `011`      | Set Less Than Unsigned (SLTU)     |
| `100`      | XOR                               |
| `101`      | Shift Right (Logical/Arithmetic; depends on `funct7`) |
| `110`      | OR                                |
| `111`      | AND                               |

 4. rs1(bits 19:15) :
  It specifies the first source register for the operation.

 6. rs2(bits 24:20) :
  It specifies the second source register for the operation.

 8. funct7(bits 31:25) :
  It provides additional differentiation between instructions that use the same opcode and fuct3.

Examples for R Type operation.  

| **funct7**  | **funct3** | **Operation**                        |
|-------------|------------|--------------------------------------|
| `0000000`   | `000`      | Add                                 |
| `0100000`   | `000`      | Sub                                 |
| `0000000`   | `001`      | Shift Left Logical (SLL)            |
| `0000000`   | `010`      | Set Less Than (SLT)                 |
| `0000000`   | `011`      | Set Less Than Unsigned (SLTU)       |
| `0000000`   | `100`      | XOR                                 |
| `0000000`   | `101`      | Shift Right Logical (SRL)           |
| `0100000`   | `101`      | Shift Right Arithmetic (SRA)        |
| `0000000`   | `110`      | OR                                  |
| `0000000`   | `111`      | AND                                 |

2.I-Type :
--
I-Type instructions are used for operations that involve immediate (constant) values, including arithmetic with constants, memory access like load operations, and control flow instructions such as jumps.

Breakdown of the Fields:

 1. Opcode (bits 6–0):
  These 7 bits tell the processor what kind of instruction it is — for example, whether it's doing arithmetic, loading data from memory, or jumping to a different   part of the program.

 2. rd (bits 11–7):
  This is the register where the result of the instruction will be stored. Think of it as the "destination" for the output.

 3. funct3 (bits 14–12):
  These 3 bits further specify what the instruction should do — like whether it's an addition, a load, or something else.

 4. rs1 (bits 19–15):
  This tells the processor which register to use as the input or base value. For example, in a memory load, it might give the base address.

 5. imm[11:0] (bits 31–20):
  This 12-bit field provides a constant value that's used directly in the instruction — like an offset for accessing memory or a number to add.

I -Type instructions :
-
| **Instruction** | **opcode** | **funct3** | **Description**                       |
|-----------------|------------|------------|---------------------------------------|
| `addi`          | `0010011`  | `000`      | Add immediate to register (`rd = rs1 + imm`). |
| `slti`          | `0010011`  | `010`      | Set if less than immediate (signed). |
| `andi`          | `0010011`  | `111`      | Bitwise AND with immediate.          |
| `lw`            | `0000011`  | `010`      | Load word from memory.               |
| `lh`            | `0000011`  | `001`      | Load halfword from memory.           |
| `jalr`          | `1100111`  | `000`      | Jump and link register (indirect jump). |

3.S-Type:
--
S-Type instructions are mainly used to store data from a register into a specific memory location. They tell the processor where to save the value in memory.

Breakdown of the Fields:

 1. opcode (bits 6–0):
  Indicates the general type of operation being performed.

 2. imm[4:0] (bits 11–7):
  The lower 5 bits of the 12-bit immediate value, which acts as an offset.

 3. funct3 (bits 14–12):
  Specifies the kind of store operation, such as storing a byte, halfword, or word.

 4. rs1 (bits 19–15):
  The first source register, usually holding the base address for the memory operation.

 5. rs2 (bits 24–20):
  The register that contains the actual data value to be stored into memory.

 6. imm[11:5] (bits 31–25):
  The upper 7 bits of the 12-bit immediate offset.
  
Common S-Type Instructions
-
| **Instruction** | **opcode**  | **funct3** | **Description**                      |
|-----------------|-------------|------------|--------------------------------------|
| `sw`           | `0100011`   | `010`      | Store Word (32-bit).                |
| `sh`           | `0100011`   | `001`      | Store Halfword (16-bit).            |
| `sb`           | `0100011`   | `000`      | Store Byte (8-bit).                 |

4.U-Type :
--
U-Type format is used for instructions such as LUI (Load Upper Immediate) and AUIPC (Add Upper Immediate to PC). These instructions work with large immediate values, loading or adding a 20-bit constant to a register or the program counter.

Breakdown of the Fields:

 1. opcode (bits 6–0):
  Identifies the general type of operation.

 2. rd (bits 11–7):
  Specifies the destination register where the result will be stored.

 3. imm[31:12] (bits 31–12):
  A 20-bit immediate value used in the instruction. This constant is placed in the upper 20 bits of the destination register.
  
Common U-Type Instrutions:
--
| **Instruction** | **Opcode (Bits 6–0)** | **Description**                                         |
|------------------|-----------------------|---------------------------------------------------------|
| `LUI`            | `0110111`            | Load Upper Immediate                                    |
| `AUIPC`          | `0010111`            | Add Upper Immediate to Program Counter (PC)            |

There are two additional instruction formats — B-type and J-type — which are specifically designed to handle immediate values differently, mainly for branching and jumping operations.

5.B-Type:
-
![image](https://github.com/user-attachments/assets/0fd62649-f420-4856-a07e-7a7125da8e06)

B-Type instructions handle conditional branching. They check a condition (like equality or comparison), and if it's true, the program jumps to a new address using an offset. If not, it continues to the next instruction.

Breakdown of the Fields:

 1. opcode (bits 6–0):
  Identifies the overall type of operation (branch instruction).

 2. imm[11] (bit 7):
  A middle bit of the 12-bit offset used for the branch target.

 3. imm[4:1] (bits 11–8):
  Lower bits of the branch offset.

 4. funct3 (bits 14–12):
  Specifies the condition for branching (e.g., equal, less than).

 5. rs1 (bits 19–15):
  First register used for comparison.

 6. rs2 (bits 24–20):
  Second register used for comparison.

 7. imm[10:5] (bits 30–25):
  Higher bits of the offset, combined with other parts to form the full branch address.

 8. imm[12] (bit 31):
  Sign bit of the offset. A value of 1 means a backward jump; 0 means forward.

funct3 examples in B-Type:

| **Instruction** | **`funct3` Value** | **Condition**                   |
|------------------|---------------------|----------------------------------|
| `BEQ`           | `000`              | Branch if `rs1 == rs2`.         |
| `BNE`           | `001`              | Branch if `rs1 != rs2`.         |
| `BLT`           | `100`              | Branch if `rs1 < rs2` (signed). |
| `BGE`           | `101`              | Branch if `rs1 >= rs2` (signed).|
| `BLTU`          | `110`              | Branch if `rs1 < rs2` (unsigned).|
| `BGEU`          | `111`              | Branch if `rs1 >= rs2` (unsigned).|

6.J-Type:
-
![J_type](https://github.com/user-attachments/assets/bfa2965c-35f5-4399-a634-fbb7bfa65b2f)

J-Type instructions are used for unconditional jumps in the program. They control the flow by jumping directly to a specific address, often used for function calls or moving to a particular instruction in the code.

Breakdown of the Fields:

 1. opcode (bits 6–0):
  Tells the processor that this is a jump instruction.

 2. rd (bits 11–7):
  This register stores the return address (the next instruction’s address, usually PC + 4) so the program knows where to come back after the jump.

 3. imm[19:12] (bits 19–12):
  These bits make up part of the jump target address.

 4. imm[11] (bit 20):
  Another bit of the address you're jumping to.

 5. imm[10:1] (bits 30–21):
  These bits provide more of the jump offset — basically, how far to jump.

 6. imm[20] (bit 31):
  The top (sign) bit of the offset. It shows whether the jump is forward or backward in the code.

J-Type instructions:
-
| **Instruction** | **Opcode (Bits 6–0)** | **Registers** | **Description**                           |
|------------------|-----------------------|---------------|-------------------------------------------|
| `JAL`           | `1101111`            | `rd`          | Jump and Link: Save return address and jump to target address |

## 32-bit instructions from application (counterdown):

![image](https://github.com/user-attachments/assets/493387fe-dd5a-4919-9537-fd8949539db9)

1 . addi sp,sp -32
-
I-Type Instruction

imm[11:0] | rs1 | funct3 | rd | opcode

- *opcode* = 0010011

- *funct3* = 000 (addi)

- *rd* = x2 (sp)

- *rs1* = x2 (sp)

- *imm* = -32 (signed 12-bit: 111111111110)

32 - bit representation:

``11111111111000010 |  000  |   00010 |  0010011``

2.lw a5,12(sp)
-
I-Type Instruction

imm[11:0]  | rs1   | funct3 | rd    | opcode

- *imm[11:0]*	000000001100 (12)

- *rs1*	00010 (sp)

- *funct3*	010 (lw)

- *rd*	01111 (a5)

- *opcode*	0000011

32-bit representation:

``00000000110000010 | 010 | 01111 | 0000011``

3.jal ra,10184
-
J-Type (Jump)

imm[20|10:1|11|19:12] | rd | opcode

- *opcode* = 1101111

- *rd* = x1 (ra)

- *imm* = 10184

- *imm[20]* = 0

- *imm[10:1]* = 1111101000

- *imm[11]* = 1

- *imm[19:12]* = 1100

32-bit representation:

``000000110011001001 | 00001 | 1101111``

4.ld a5,88(a0)
-
I-Type (Load, RV64I)

imm[11:0] | rs1 | funct3 | rd | opcode

- *opcode* = 0000011

- *funct3* = 011 (ld)

- *rd* = x15 (a5)

- *rs1* = x10 (a0)

- *imm* = 88 (000000010110)

32 - bit representation:

``00000001011001010 |011 |   01111 |   0000011``

5.jalr a5
-
I-Type (Jump Register)

imm[11:0] | rs1 | funct3 | rd | opcode

- *opcode* = 1100111

- *funct3* = 000 (jalr)

- *rd* = x15 (a5)

- *rs1* = x15 (a5)

- *imm* = 0

32 - bit-representation:

``00000000000001111 | 000  |   01111  | 1100111``

6.srai s2,s2,0x3
-
I-Type Instruction

imm[11:0] | rs1 | funct3 | rd | opcode

- *imm[11:5]*	0100000

- *imm[4:0]*	00011 (shift amount = 3)

- *rs1*	10010 (s2)

- *funct3*	101 (srai)

- *rd*	10010 (s2)

- *opcode*	0010011

32 - bit representation:

``01000000001110010 | 101 | 10010 | 0010011``

7.bne s2, s1, 10330
-
B-Type (Conditional Branch)

imm[12|10:5] | rs2 | rs1 | funct3 | imm[4:1|11] | opcode

- *opcode* = 1100011


- *funct3* = 001 (bne)

- *rs1* = x18 (s2)

- *rs2* = x9 (s1)

- *imm* = 10330, split as:

- *imm[12]* = 1

- *imm[10:5]* = 100011

- *imm[4:1]* = 0101

- *imm[11]* = 0

32 - bit representation:

``1| 100011   |   01001  |10010 |  001  |  0101| 0  | 1100011``

8.auipc a5, 0xfffff0
---------
U-Type (Upper Immediate)

imm[31:12] | rd | opcode

- *opcode* = 0010111

- *rd* = x15 (a5)

- *imm* = 0xfffff0 (11111111111100000)

32 - bit representation:

``11111111111100000 | 01111 | 0010111``

9.beqz a5, 100c8 <register_fini+0x18>
-
beqz is a pseudo-instruction for beq a5, x0, offset.
It checks if a5 is equal to 0 (x0) and branches to the offset 100c8.

- *imm[12]*	1

- *imm[10:5]*	000110

- *rs2*	00000

- *rs1*	01111

- *funct3*	000

- *imm[4:1]*	1010

- *imm[11]*	1

- *opcode*	1100011

32-bit representation:

``10001000000011110 | 000 | 01010 | 1100011``

10.li a0, 0
-
I-Type Instruction

- *imm[11:0]*	000000000000 (0)

- *rs1*	00000 (zero)

- *funct3*	000 (addi)

- *rd*	01010 (a0)

- *opcode*	0010011

32-bit representation:

``00000000000000000 | 000 | 01010 | 0010011``

11.bnez s1, 102a0
-
B-Type Instruction

- *imm[12]*	0

- *imm[10:5]*	100010

- *rs2*	00000 (zero)

- *rs1*	01001 (s1)

- *funct3*	001 (bne)

- *imm[4:1]*	0001

- *imm[11]*	1

- *opcode*	1100011

32 - bit representation:

``00001000101010001 | 001 | 00101 | 1100011``

12.sd a6, 80(sp)
-
S-Type Instruction

- *imm[11:5]*	0000001

- *rs2*	00110 (a6)

- *rs1*	00001 (sp)

- *funct3*	011 (sd)

- *imm[4:0]*	01000

- *opcode*	0100011

32- bit representation:

``00000010011000001 | 011 | 00001 | 0100011``

13.lui a3, 0xffff
-
U-Type Instruction

*imm[31:12]*	111111111111

- *rd*	00011 (a3)

- *opcode*	0110111

32- bit representation:

``111111111111 | 00011 | 0110111``

14.or a2, a4, -4(a4)
-
R-Type Instruction

- *rs2*	00100 (a4)

- *rs1*	00100 (a4)

- *funct3*	000 (or)

- *rd*	00010 (a2)

- *funct7*	0000000

- *opcode*	0110011

32- bit representation:

``000000000100 | 00100 | 000 | 00010 | 0110011 ``

15.lbu a2,-4(a4)
-
I-Type  Instruction:

- *imm[11:0]*	111111111100

- *rs1*	01000 (a4)

- *funct3*	100 (lbu)

- *rd*	00010 (a2)

- *opcode*	0000011

32- bit reprsentation:

``111111111100 | 01000 | 100 | 00010 | 0000011``

</details>
<details>
<summary><b>Task 4:</b> Functional simulation of RISC-V Core Verilog netlist and Testbench </summary>   
<br>
