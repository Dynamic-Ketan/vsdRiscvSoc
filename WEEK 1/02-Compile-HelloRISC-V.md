# 🛠️ Task 2: Compile “Hello, RISC-V” (Minimal C Program for RV32IMC)
This guide shows you how to write and cross-compile a minimal C “Hello World” program for the RV32IMC RISC-V architecture and verify the resulting ELF file.

## ✍️ Step 1: Write the Minimal C Program
Create a file named hello.c with the following content:

#include <stdio.h>

```bash
int main() {
    printf("Hello, RISC-V\n");
    return 0;
}
```

## 🛠️ Step 2: Cross-Compile the Program
Run the following command to compile hello.c for the RV32IMC architecture with the ilp32 ABI:

```bash
/home/ketan/tools/riscv/bin/riscv32-unknown-elf-gcc -o hello.elf /home/ketan/hello.c
```

## ✅ Step 3: Verify the ELF File
Check that the output file hello.elf is a 32-bit RISC-V executable:

```bash
file hello.elf
```

Output:

```bash
hello.elf: ELF 32-bit LSB executable, UCB RISC-V, RVC, soft-float ABI, version 1 (SYSV), statically linked, not stripped
```
