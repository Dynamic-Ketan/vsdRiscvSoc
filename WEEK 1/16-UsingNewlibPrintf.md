# 🛠️ Task 16: Using Newlib `printf` Without an OS

This task shows how to **redirect `printf` output to UART** in a **bare-metal RISC-V** program by retargeting the `_write()` syscall.

---

## ✅ Goal

Make `printf()` work without an OS by:

- Implementing `_write()` manually.
- Linking against `newlib` without startup files.
- Sending characters to memory-mapped UART at `0x10000000`.

---

## 🧩 Step-by-Step Instructions

### 🧾 Step 1: Create `hello1.c`

This is your main application file using `printf()`:

```bash
#include <stdio.h>

int main() {
    printf("Hello from RISC-V using printf!\n");
    return 0;
}
```

## 🔧 Step 2: Create syscalls.c

Redirect the _write() syscall to send characters to UART:

```bash
#define UART0 ((volatile unsigned char *)0x10000000)

int _write(int fd, char *buf, int len) {
    for (int i = 0; i < len; i++) {
        UART0[0] = buf[i];
    }
    return len;
}
```

## 🧵 Step 3: Create start.S

Startup code to set the stack and jump to main():

```bash
.section .text
.globl _start
_start:
    la sp, _stack_top
    call main
1:  j 1b    // infinite loop after main returns
```

## 📐 Step 4: Create link.ld

Basic linker script to define memory layout:

```bash
ENTRY(_start)

SECTIONS {
    . = 0x80000000;

    .text : { *(.text*) }

    .data : { *(.data*) }

    .bss : {
        *(.bss*)
        *(COMMON)
    }

    . = ALIGN(4);
    . = . + 0x1000; /* 4 KB stack */
    _stack_top = .;
}
```

## 🛠️ Step 5: Compile the ELF File

Use the RISC-V GCC toolchain:

```bash
riscv32-unknown-elf-gcc -march=rv32imac -mabi=ilp32 -nostartfiles \
  -T link.ld start.S hello.c syscalls.c -o hello.elf
```

## ▶️ Step 6: Run in QEMU

```bash
qemu-system-riscv32 -nographic -machine sifive_e -kernel hello.elf
```

## 🧪 Output

```bash
/home/ketan/tools/riscv/lib/gcc/riscv32-unknown-elf/15.1.0/../../../../riscv32-unknown-elf/bin/ld: warning: hello.elf has a LOAD segment with RWX permissions
ketan@ketan-VirtualBox:~/riscv-labs$ qemu-system-riscv32 -nographic -machine sifive_e -kernel hello.elf
```

