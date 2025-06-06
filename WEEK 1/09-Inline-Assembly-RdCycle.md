# 09 Inline Assembly Basics

## ✍️ Method

Here is a simple implementation of the function in C using GCC inline assembly:

```bash
#include <stdint.h>

static inline uint32_t rdcycle(void) {
    uint32_t c;
    asm volatile ("csrr %0, cycle" : "=r"(c));
    return c;
}

int main() {
    uint32_t cycle = rdcycle();
    while (1);
    return 0;
}

```

## 🧠 Explanation of Constraints and Keywords

| Part               | Explanation                                                                                                                                              |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `asm volatile`     | Prevents compiler from optimizing or reordering the assembly instruction. Ensures it runs exactly where placed.                                          |
| `"csrr %0, cycle"` | Assembly instruction: read CSR `cycle` into the register `%0` (an output placeholder).                                                                   |
| `: "=r"(c)`        | Output operand constraint: `=r` means "write-only" (`=`) and use any general-purpose register (`r`) for variable `c`. The compiler chooses the register. |
| `: `               | No input operands (empty).                                                                                                                               |
| `: `               | No clobbered registers declared here (the instruction only writes to the output register).                                                               |

## 🔎 Additional Notes

cycle CSR (0xC00) counts CPU clock cycles since reset on RISC-V.

Using volatile ensures the instruction is not removed or reordered by optimization.

The constraint "=r"(c) tells GCC to store the CSR value into the C variable c using a register.

No input operands or clobbers are needed because csrr reads the CSR and writes only the output register.
