## **Task 1 : To compile the Object dump file and verify the output with the GCC output from Lab 1.**

**STEP 1:** Compile sum1ton.c into sum1ton.o for RISC-V with -Ofast optimization

riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sumton.o sumton.c
