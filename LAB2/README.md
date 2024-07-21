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
