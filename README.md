

Task 1: Performance Analysis of C Code Compilation

This task involved analyzing the performance of a simple C program (sum1ton.c) that calculates the sum of numbers from 1 to n. The analysis focused on comparing the code size and potential performance when compiled with different optimization levels using the RISC-V compiler.

Lab 1:

* The C code was compiled using the standard GCC compiler and executed to verify its functionality.
* The code and output are documented in files starting with "Lab 1."

Lab 2:

* The same C code was compiled using the RISC-V compiler with optimization level "O0" (no optimization).
* The resulting object file (sum1ton.o) was disassembled to analyze the generated assembly code.
* The number of instructions within the "main" function was counted.
* The process was repeated with optimization level "Ofast" to observe the impact of optimization on the number of instructions.
* The results, including assembly code snippets and instruction counts, are documented in files starting with "Lab 2."

Task 2:
Lab 3 :

The assembly language program for the file `sum1ton.o` was analyzed. The corresponding C code was compiled using both the GCC and RISC-V compilers, producing identical outputs. The Spike simulator was employed to execute the RISC-V compiled program. 


1. Object Dump Analysis:
   - Assembly code was extracted, and the Spike debugger was used to progress the program counter to memory address `100b0`. Subsequent instructions were executed manually.  

2. Register Behavior: 
   - Register `a2`:  
     Observed before and after modifications by the `lui` instruction, which loads the upper immediate bits (12-31) into the register.  
   - Register `a0`:  
     The `addi` instruction was used to perform hexadecimal addition on the value stored in the register.  




