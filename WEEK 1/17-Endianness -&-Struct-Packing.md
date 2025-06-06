# 🛠️ Task 17: Endianness & Struct Packing

This task demonstrates how to verify the endianness of a RISC-V system (RV32) using a C union trick to inspect memory layout byte by byte.

---

## ❓ Question

“Is RV32 little-endian by default? Show me how to verify byte ordering with a union trick in C.”

---

## ✅ Answer Summary

- Yes, **RV32 is little-endian by default**.
- We can use a `union` of `uint32_t` and a byte array `uint8_t[4]` to view the individual byte order of a known word.

---

### 🧾 Step 1: Create a C File

```bash
#define UART0 ((volatile unsigned char *)0x10000000)
#include <stdint.h>  // For uint32_t, uint8_t
void print_uart(const char *s) {
    while (*s) {
        *UART0 = *s++;
    }
}
char nibble_to_hex(uint8_t nibble) {
    return (nibble < 10) ? ('0' + nibble) : ('A' + nibble - 10);
}
void print_byte_hex(uint8_t byte) {
    char hex[3];
    hex[0] = nibble_to_hex(byte >> 4);
    hex[1] = nibble_to_hex(byte & 0x0F);
    hex[2] = '\0';
    print_uart(hex);
}
int main() {
    union {
        uint32_t value;
        uint8_t bytes[4];
    } u;
    u.value = 0x01020304;
    print_uart("Endian Test:\n");
    for (int i = 0; i < 4; i++) {
        print_uart("Byte ");
        *UART0 = '0' + i;
        print_uart(": 0x");
        print_byte_hex(u.bytes[i]);
        print_uart("\n");
    }
    while (1);  // Loop forever
    return 0;
}
```

🧵 Step 2: Compile the Code (for your simulator or native)
For bare-metal RISC-V, use something like:

```bash
riscv32-unknown-elf-gcc -march=rv32imac -mabi=ilp32 -nostdlib -T link.ld start.S endian_test.c -o endian.elf
```

▶️ Step 3: Run on QEMU
```bash
qemu-system-riscv32 -nographic -machine sifive_e -kernel endian.elf
```

🧾 Output

```bash
ketan@ketan-VirtualBox:~/riscv-labs$ riscv32-unknown-elf-gcc -march=rv32imac -mabi=ilp32 -nostdlib -T link.ld start.S endian_test.c -o endian.elf
ketan@ketan-VirtualBox:~/riscv-labs$ qemu-system-riscv32 -nographic -machine sifive_e -kernel endian.elf
QEMU: Terminated
```
