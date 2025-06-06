# Task 7: Running Under an Emulator (QEMU)

This guide shows you how to run a bare-metal RISC-V ELF executable on an emulator and print output to the UART console.

## ✍️ Step 1: Prepare your Bare-metal ELF

Make sure your ELF binary is compiled for RV32IMC with UART output implemented (e.g., writing characters to UART at 0x10000000).

```bash
#define UART0 ((volatile unsigned char *)0x10000000)

void print_uart(const char *s) {
    while ( ) {
        *UART0 = *s++;
    }
}

int main() {
    print_uart("Hello, RISC-V!\n");
    while (1);
    return 0;
}
```

## 🛠️ Step 2: Compile your ELF binary

Use the cross-compiler with no standard library and your linker script:

```bash
/home/ketan/tools/riscv/bin/riscv32-unknown-elf-gcc -march=rv32imac -mabi=ilp32 -nostdlib -T link.ld start.S hello.c -o hello.elf
```

## 🏃‍♂️ Step 3: Run your ELF in QEMU (SiFive E-board machine)

Use QEMU with these options to emulate the SiFive E-class board, redirect UART output to your terminal, and skip firmware:

```bash
qemu-system-riscv32 -nographic -machine sifive_e -kernel hello.elf -bios none -serial mon:stdio
```

Expected Behavior:

Program runs silently (infinite loop).
No crash = ✅ success.
To exit QEMU: Press Ctrl + A, then X.

