# **LAB 1:**

## **Task 1 : Compiling a C program using GCC and RISC-V**

**STEP 1:** Create a file in editor in Linux environment

![s0](https://github.com/user-attachments/assets/2579e3bb-2e9c-4806-8f93-6601cff88121)

**STEP 2:** Write your code in leafpad and save it

![s1](https://github.com/user-attachments/assets/05d04e05-9b15-4e7c-9616-d45edaaf0f4f)

**STEP 3:** Compile your code using gcc compiler in the terminal window

![s2](https://github.com/user-attachments/assets/2568a685-d390-4f7c-a1e1-910578236ce4)

**STEP 4:** Once you've finished compiling your code, the next step is to run the executable file in your terminal to view its output.

![s3](https://github.com/user-attachments/assets/854f0cdd-09a1-45a6-b5eb-9f62a2600b42)

**Final Output along with Code:**

![s4](https://github.com/user-attachments/assets/21afb510-b79e-4b97-a0eb-ba57cc9d2d26)

## **Task 2 : Compile and run a C program using a RISC-V compiler, optimizing the compilation with -O1 and -Ofast**

**STEP 1:** Write a c program sum1ton on leafpad and save it. Enter a command cat sum1ton.c to view its contents in the terminal.

![1](https://github.com/user-attachments/assets/bfcc7bcd-15aa-4342-870f-fa317551bd25)

**STEP 2:** Compile the C program using the RISC-V compiler with **-O1** optimization.

![2](https://github.com/user-attachments/assets/15abca9b-87b6-497d-adcf-1ae24bf3ea99)

**STEP 3:** Now we enter a command that is used to display information about object files. Since that is long list we use less in the command.

![4a](https://github.com/user-attachments/assets/88ad32f1-b2d0-4638-a69a-4fc01eea9023)

**STEP 4:** We are interested in the main section of the information displayed. Therefore we type main and get the following information.

![3](https://github.com/user-attachments/assets/e6cd9366-a5df-4b40-8b4b-da3129cbd927)

**OBSERVATION 1: There are 14 lines of opcode in main section** 

**STEP 5:** Now again compile the same program using RISC - V compiler but now optimise the compilation using **-Ofast** optimization.

![3b](https://github.com/user-attachments/assets/adad17db-ca14-45f4-b8e4-3077b3c09c05)

**STEP 6:** Similar to the step 3 we enter a command and get another list. The main section of ofast looks as shown in the image.

![4](https://github.com/user-attachments/assets/858d515d-f8b5-49b7-af2a-79da66d20a9e)

**OBSERVATION 2: There are 11 lines of opcode in main section**

**Conclusion: We get an optimized compilation using -Ofast.**

# **LAB 2:**

## **Task 1 : To compile the Object dump file and verify the output with the GCC output from Lab 1.**

**STEP 1:** Compile sum1ton.c (C source file) into sum1ton.o (Object file) for RISC-V with -Ofast optimization.
``` bash
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sumton.o sumton.c
```

**STEP 2:** Get the Object dump using following command.
``` bash
riscv64-unknown-elf-objdump -d sumton.o | less
```
We get the following output:

![2a](https://github.com/user-attachments/assets/3a431303-1d62-4135-9d6d-0b747380d6a6)

**STEP 3:** Execute the compiled sum1ton.o (object file) using Spike.
``` bash
spike pk sumton.o
```
We get the following output:

![2b](https://github.com/user-attachments/assets/643b5ae2-305a-4336-ac65-668a8b5a052d)

## **Task 2 : To debug the main function and observe register values**

**STEP 1:** Run the assembly code in sum1ton.o on the Spike simulator in debug mode.
``` bash
spike -d pk sumton.o
```
To execute until start of main use following command:
```bash
until pc 0 100b0
```
![2c](https://github.com/user-attachments/assets/3411e913-96df-454e-b13f-4f0c434f119c)

**STEP 2:** Run the following Commands and Observe the Register Values.
```bash
reg 0 a2
reg 0 sp
```

**FINAL OUTPUT:**

<img width="715" alt="Screenshot 2024-07-21 234052" src="https://github.com/user-attachments/assets/0191ffa6-1ef5-45de-90b6-aefbdf1f53ef">


# **LAB 3:** 

## **TASK 1: Identifying Instruction Format**
The task is to identify different types of instructions based on the provided guidelines. This identification is done using a 32-bit code, with each instruction type having its unique format.

### RISC-V Instruction Formats

Instruction formats in RISC-V act as a 'contract' between the assembly language and the hardware. When an assembly instruction is executed, the hardware understands exactly what to do based on this contract. Each instruction type has a specific format, defined by a series of 0s and 1s, that includes details such as the type of operation and the location of data.

#### 1) R-Type (Register)
 R-type instructions handle all arithmetic and logical operations involving three registers. 
 
 The format includes fields for two source registers, one destination register, a function code, and an opcode.

 Instruction format is as follows:

<img width="538" alt="Screenshot 2024-07-28 170104" src="https://github.com/user-attachments/assets/ae16efea-a976-44c2-9ca1-7078d5814a00">

- **funct7 (7 bits):** Function code for additional instruction differentiation.
- **rs2 (5 bits):** Second source register.
- **rs1 (5 bits):** First source register.
- **funct3 (3 bits):** Function code for primary instruction differentiation.
- **rd (5 bits):** Destination register.
- **opcode (7 bits):** Basic operation code for R-type instructions (0110011 for integer operations).

**Examples:** ADD, SUB, OR, XOR

#### 2) I-Type (Immediate)
These instructions perform arithmetic with immediate values, load operations, and certain branch instructions.

I-type instructions involve operations with an immediate value and one or two registers. 

Instruction format is as follows:

<img width="528" alt="Screenshot 2024-07-28 171319" src="https://github.com/user-attachments/assets/0a532019-7b7c-4b33-a5ee-f90a56420177">

- **immediate (12 bits):** Immediate value used for operations.
- **rs1 (5 bits):** Source register.
- **funct3 (3 bits):** Function code for instruction differentiation.
- **rd (5 bits):** Destination register.
- **opcode (7 bits):** Basic operation code for I-type instructions.

#### 3) S-Type (Store)
S-type instructions are used for store operations, where data is stored from a register into memory. 

The format includes fields for two source registers, an immediate value determining the memory offset, a function code, and an opcode.

Instruction format is as follows:

<img width="522" alt="Screenshot 2024-07-28 171843" src="https://github.com/user-attachments/assets/44fee5c1-e67a-42d3-a147-6a634aa6b965">

- **imm[11:5] (7 bits):** Upper 7 bits of the immediate value.
- **rs2 (5 bits):** Second source register (contains the data to be stored).
- **rs1 (5 bits):** First source register (base address register).
- **funct3 (3 bits):** Function code for instruction differentiation.
- **imm[4:0] (5 bits):** Lower 5 bits of the immediate value.
- **opcode (7 bits):** Basic operation code for S-type instructions.

#### 4) B-Type (Branch)
B-type instructions are used for conditional branch operations.

These instructions alter the flow of execution based on comparisons between two registers.

Instruction format is as follows:

<img width="520" alt="Screenshot 2024-07-28 171920" src="https://github.com/user-attachments/assets/4a11d921-b87a-435d-a5e2-2406f7071e11">

- **imm[12] (1 bit):** The 12th bit of the immediate value.
- **imm[10:5] (6 bits):** The 10th to 5th bits of the immediate value.
- **rs2 (5 bits):** Second source register.
- **rs1 (5 bits):** First source register.
- **funct3 (3 bits):** Function code for instruction differentiation.
- **imm[4:1] (4 bits):** The 4th to 1st bits of the immediate value.
- **imm[11] (1 bit):** The 11th bit of the immediate value.
- **opcode (7 bits):** Basic operation code for B-type instructions.

#### 5) U-Type (Upper Immediate)
U-type instructions handle operations involving large immediate values, typically for loading upper immediate values or computing addresses.

Instruction format is as follows:

<img width="518" alt="Screenshot 2024-07-28 171959" src="https://github.com/user-attachments/assets/0a5238e0-9a70-4944-911e-97a7e925e49b">

- **immediate[31:12] (20 bits):** The upper 20 bits of the immediate value.
- **rd (5 bits):** Destination register.
- **opcode (7 bits):** Operation code for U-type instructions.

The immediate value is stored in the upper 20 bits of a 32-bit word, with the lower 12 bits set to zero when used in calculations.

#### 6) J-Type (Jump)
J-type instructions are used for jump operations, allowing for altering the program control flow by jumping to a specified address.

These are typically used for unconditional jumps, such as calling functions or implementing loops.

Instruction format is as follows:

<img width="521" alt="Screenshot 2024-07-28 172109" src="https://github.com/user-attachments/assets/e158ade7-6748-4ba0-9adf-84b5f67d2410">

- **imm[20] (1 bit):** The 20th bit of the immediate value.
- **imm[10:1] (10 bits):** The 10th to 1st bits of the immediate value.
- **imm[11] (1 bit):** The 11th bit of the immediate value.
- **imm[19:12] (8 bits):** The 19th to 12th bits of the immediate value.
- **rd (5 bits):** Destination register where the return address is stored.
- **opcode (7 bits):** Operation code for J-type instructions.

## **TASK 2: Decoding each Instruction Provided**

- **ADD r8, r9, r10**
  - Opcode: 0110011
  - rd = r8 = 01000
  - rs1 = r9 = 01001
  - rs2 = r10 = 01010
  - funct3: 000
  - funct7: 0000000
  - **R-Type**
  - 32-bit Instruction: `0000000_01010_01001_000_01000_0110011`

- **SUB r10, r8, r9**
  - Opcode: 0110011
  - rd = r10 = 01010
  - rs1 = r8 = 01000
  - rs2 = r9 = 01001
  - funct3: 000
  - funct7: 0100000
  - **R-Type**
  - 32-bit Instruction: `0100000_01001_01000_000_01010_0110011`

- **AND r9, r8, r10**
  - Opcode: 0110011
  - rd = r9 = 01001
  - rs1 = r8 = 01000
  - rs2 = r10 = 01010
  - funct3: 111
  - funct7: 0000000
  - **R-Type**
  - 32-bit Instruction: `0000000_01010_01000_111_01001_0110011`

- **OR r8, r9, r5**
  - Opcode: 0110011
  - rd = r8 = 01000
  - rs1 = r9 = 01001
  - rs2 = r5 = 00101
  - funct3: 110
  - funct7: 0000000
  - **R-Type**
  - 32-bit Instruction: `0000000_00101_01001_110_01000_0110011`

- **XOR r8, r8, r4**
  - Opcode: 0110011
  - rd = r8 = 01000
  - rs1 = r8 = 01000
  - rs2 = r4 = 00100
  - funct3: 100
  - funct7: 0000000
  - **R-Type**
  - 32-bit Instruction: `0000000_00100_01000_100_01000_0110011`

- **SLT r0, r1, r4**
  - Opcode: 0110011
  - rd = r0 = 00000
  - rs1 = r1 = 00001
  - rs2 = r4 = 00100
  - funct3: 010
  - funct7: 0000000
  - **R-Type**
  - 32-bit Instruction: `0000000_00100_00001_010_00000_0110011`

- **ADDI r2, r2, 5**
  - Opcode: 0010011
  - rd = r2 = 00010
  - rs1 = r2 = 00010
  - immediate: 000000000101
  - funct3: 000
  - **I-Type**
  - 32-bit Instruction: `000000000101_00010_000_00010_0010011`

- **SW r2, r0, 4**
  - Opcode: 0100011
  - rs2 = r2 = 00010
  - rs1 = r0 = 00000
  - imm[11:5]: 0000000
  - imm[4:0]: 00100
  - funct3: 010
  - **S-Type**
  - 32-bit Instruction: `0000000_00010_00000_010_00100_0100011`

- **SRL r6, r1, r1**
  - Opcode: 0110011
  - rd = r6 = 00110
  - rs1 = r1 = 00001
  - rs2 = r1 = 00001
  - funct3: 101
  - funct7: 0000000
  - **R-Type**
  - 32-bit Instruction: `0000000_00001_00001_101_00110_0110011`

- **BNE r0, r0, 20**
  - Opcode: 1100011
  - rs1 = r0 = 00000
  - rs2 = r0 = 00000
  - imm[12|10:5|4:1|11]: 0000000 00000 00010 0
  - funct3: 001
  - **B-Type**
  - 32-bit Instruction: `0000000_00000_00000_001_00010_0000000_1100011`

- **BEQ r0, r0, 15**
  - Opcode: 1100011
  - rs1 = r0 = 00000
  - rs2 = r0 = 00000
  - imm[12|10:5|4:1|11]: 0000000 00000 00001 1
  - funct3: 000
  - **B-Type**
  - 32-bit Instruction: `0000000_00000_00000_000_00001_0000000_1100011`

- **LW r3, r1, 2**
  - Opcode: 0000011
  - rd = r3 = 00011
  - rs1 = r1 = 00001
  - immediate: 000000000010
  - funct3: 010
  - **I-Type**
  - 32-bit Instruction: `000000000010_00001_010_00011_0000011`
 
- **SLL r5, r1, r1**
  - Opcode: 0110011
  - rd = r5 = 00101
  - rs1 = r1 = 00001
  - rs2 = r1 = 00001
  - funct3: 001
  - funct7: 0000000
  - **R-Type**
  - 32-bit Instruction: `0000000_00001_00001_001_00101_0110011`
 
## **TASK 2: Executing assembly instructions based on a provided Verilog code within a RISC-V processor.**
Firstly for the provided verilog code there is some variations in the ISA followed by RISCV and the hardcoded ISA. The differences are shown in the table below:

| Operation            | Standard RISC-V ISA | Hardcoded ISA  |
|----------------------|----------------------|----------------|
| ADD R6, R2, R1       | 32'h00110333         | 32'h02208300   |
| SUB R7, R1, R2       | 32'h402083b3         | 32'h02209380   |
| AND R8, R1, R3       | 32'h0030f433         | 32'h0230a400   |
| OR R9, R2, R5        | 32'h005164b3         | 32'h02513480   |
| XOR R10, R1, R4      | 32'h0040c533         | 32'h0240c500   |
| SLT R1, R2, R4       | 32'h0045a0b3         | 32'h02415580   |
| ADDI R12, R4, 5      | 32'h004120b3         | 32'h00520600   |
| BEQ R0, R0, 15       | 32'h00000f63         | 32'h00f00002   |
| SW R3, R1, 2         | 32'h0030a123         | 32'h00209181   |
| LW R13, R1, 2        | 32'h0020a683         | 32'h00208681   |
| SRL R16, R14, R2     | 32'h0030a123         | 32'h00271803   |
| SLL R15, R1, R2      | 32'h002097b3         | 32'h00208783   |

Now for the custom instructions provided:

| Operation             | RISC-V ISA  | Bit Pattern (RISC-V)              |
|-----------------------|-------------|-----------------------------------|
| ADD r1, r2, r3        | 32'h006100B3 | 0000000 00110 00010 000 00001 0110011 |
| SUB r3, r1, r2        | 32'h40208333 | 0100000 00010 00001 000 00110 0110011 |
| AND r2, r1, r3        | 32'h0230a400 | 0000000 00011 00001 111 00010 0110011 |
| OR r8, r2, r5         | 32'h0030F133 | 0000000 00101 00010 110 01000 0110011 |
| XOR r8, r1, r4        | 32'h0040C433 | 0000000 00100 00001 100 01000 0110011 |
| SLT r10, r2, r4       | 32'h00412633 | 0000000 00100 00010 010 01100 0110011 |
| ADDI r12, r3, 5       | 32'h00508313 | 000000000101 00001 000 00110 0010011  |
| SW r3, r1, 4          | 32'h00205223 | 0000000 00100 00001 010 0100 0100011  |
| SRL r16, r11, r2      | 32'h0025D833 | 0000000 00010 01011 101 10000 0110011 |
| BNE r0, r1, 20        | 32'h02101A63 | 0 000001 00001 00000 001 1010 0 1100011 |
| LW r13, r11, 2        | 32'h000969A1 | 000000000010 01011 010 01101 00001 |
| SLL r15, r11, r2      | 32'h002597B3 | 0000000 00010 01011 001 01111 0110011 |
| BEQ r0, r0, 15        | 32'h00000F63 | 0 000000 00000 00000 000 1111 0 1100011 |
