# 🔟 Memory-Mapped I/O Demo

## 🔧 Method:

Declare a pointer to the memory-mapped GPIO register using a volatile qualifier to prevent compiler optimizations:

```bash
#include <stdint.h>

int main() {
    volatile uint32_t *gpio = (uint32_t *)0x10012000;
    *gpio = 0x1;  // Toggle GPIO pin HIGH
    return 0;
}
```

## 📘 Discussion:

✅ Use of volatile:

The volatile keyword tells the compiler not to optimize the access to the memory address.

This is crucial in memory-mapped I/O where writing to a specific address (like 0x10012000) has real hardware effects (e.g., turning on an LED).

Without volatile, the compiler might remove the write, assuming it's unnecessary if the value isn’t read back.

✅ Pointer Alignment:

gpio is declared as a pointer to a uint32_t (4 bytes), and the address 0x10012000 is 4-byte aligned.

This alignment is correct and safe for 32-bit memory-mapped register access.
