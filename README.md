**Task 1 : Compiling a C program using GCC and RISC-V**

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

**Task 2 : Compile and run a C program using a RISC-V compiler, optimizing the compilation with -O1 and -Ofast**

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




