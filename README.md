

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


Task 3:

![image](https://github.com/user-attachments/assets/26aab526-da87-4cc2-bda4-5976b1ddb326)



RISC-V instructions are typically represented using different instruction formats, each with a specific field layout:

R-type: For register-to-register operations (e.g., add, sub, and, or, xor)

opcode (7 bits): Identifies the instruction type (e.g., 0110011 for R-type).
rd (5 bits): Destination register.
funct3 (3 bits): Further specifies the operation within the R-type group.
rs1 (5 bits): First source register.
rs2 (5 bits): Second source register.
funct7 (7 bits): Provides additional information for specific R-type

I-type: For immediate operations (e.g., addi, slli) and load instructions (e.g., lb, lh, lw)
opcode (7 bits): Identifies the instruction type.
rd (5 bits): Destination register.
funct3 (3 bits): Further specifies the operation within the I-type group.
rs1 (5 bits): First source register.
imm[11:0] (12 bits): Immediate value.

S-type: For store instructions (e.g., sb, sh, sw)
opcode (7 bits): Identifies the instruction type.
imm[4:0] (5 bits): Lower 5 bits of the immediate offset.
rs1 (5 bits): Base register.
funct3 (3 bits): Further specifies the store operation (e.g., byte, halfword, word).
rs2 (5 bits): Source register.
imm[11:5] (7 bits): Upper 7 bits of the immediate offset.

B-type: For branch instructions (e.g., beq, bne, blt, bge)
opcode (7 bits): Identifies the instruction type.
rs1 (5 bits): First source register.
rs2 (5 bits): Second source register.
funct3 (3 bits): Further specifies the branch condition.
imm[12/11:5] (7 bits): Branch offset.
imm[4:1/11] (5 bits): Branch offset.

U-type: For instructions with a 20-bit immediate (e.g., auipc, lui)
opcode (7 bits): Identifies the instruction type.
rd (5 bits): Destination register.
imm[31:12] (20 bits): Immediate value.

J-type: For unconditional jumps (e.g., jal, jalr)
opcode (7 bits): Identifies the instruction type.
rd (5 bits): Destination register.
imm[20/19:12] (10 bits): Jump target address.
imm[11] (1 bit): Jump target address.
imm[19:20] (2 bits): Jump target address.
imm[10:1] (10 bits): Jump target address.

Unique RISC-V Instructions Identified :
Based on the analysis of the assembly code, I identified the following unique RISC-V instructions:

1.	addi
2.	sd
3.	li
4.	jal
5.	ld
6.	ret
7.	mv
8.	beqz
9.	jalr
10.	jr
11.	bltz
12.	neg
13.	sll
14.	and
15.	sub


Example: Decoding "addi x3, x1, 5"

opcode (7 bits): 0010011 (I-type opcode for addi)
rd (5 bits): 00011 (register x3)
funct3 (3 bits): 000 (for addi)
rs1 (5 bits): 00001 (register x1)
imm[11:0] (12 bits): 000000000101 (decimal 5)
This instruction adds the immediate value 5 to the value in register x1 and stores the result in register x3.

Task 4:

5-Stage RISC Pipeline Implementation and Simulation

This report discusses the implementation of a 5-stage RISC pipeline using Verilog. The design simulates a basic RISC processor architecture comprising instruction fetch, decode, execution, memory access, and write-back stages. The simulation is carried out using Icarus Verilog (Iverilog) and GTKWave, which provide a comprehensive environment for digital design verification.

---

Pipeline Stages

1. Instruction Fetch (IF):
   - Fetches the instruction from memory.
   - Computes the next program counter (NPC).
   - Key Signals: `IF_ID_IR` (Instruction Register), `IF_ID_NPC` (Next Program Counter).

2. Instruction Decode (ID):
   - Decodes the instruction to identify the operation and operands.
   - Reads register values.
   - Key Signals: `ID_EX_A` (Source Register), `ID_EX_B` (Destination Register), `ID_EX_IMMEDIATE` (Immediate Value), `ID_EX_IR` (Instruction Register).

3. Execute (EX):
   - Executes the operation using the ALU.
   - Produces outputs such as `EX_MEM_ALUOUT` (ALU Result) and `EX_MEM_IR` (Instruction Details).

4. Memory Access (MEM):
   - Handles memory-related instructions (loads/stores).
   - Key Signals: `MEM_WB_ALUOUT` (ALU Result for Memory), `MEM_WB_LDM` (Loaded Data from Memory).

5. Write Back (WB):
   - Writes the results back to the register file.
   - Key Signal: `WB_OUT` (Write-Back Output).

---

Design Implementation
- The Verilog code defines a parameterized RISC pipeline.
- Registers and memories (`REG` and `MEM`) are initialized for operations.
- The design supports arithmetic (ADD, SUB), logical (AND, OR), memory operations (LW, SW), branching (BEQ, BNE), and shifting (SLL, SRL).
- Control signals such as `EX_MEM_COND` and `BR_EN` handle branching logic.

---

Testbench
- The testbench initializes the pipeline with a clock (`clk`) and reset (`RN`) signals.
- A `.vcd` file (`iiitb_rv32i.vcd`) is generated to record the simulation results.
- Key simulation commands include:
  - `initial begin` to initialize variables.
  - `always #3 clk = !clk` for generating the clock.
  - `$dumpfile` and `$dumpvars` for simulation output.
  - `$finish` to terminate the simulation.

---

Simulation and Debugging
- Iverilog compiles and simulates the Verilog code, generating a `.vcd` file.
- GTKWave visualizes signal transitions and provides insights into the pipeline behavior.

---

The 5-stage RISC pipeline efficiently handles instruction execution through systematic stages, leveraging overlapping operations for higher throughput. The simulation and debugging process, facilitated by Iverilog and GTKWave, ensures correct functionality and performance validation of the design.




