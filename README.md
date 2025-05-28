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













