# vsd_SquadronMini-internship
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
