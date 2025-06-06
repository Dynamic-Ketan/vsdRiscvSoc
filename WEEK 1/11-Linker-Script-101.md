# 📦 11 Linker Script 101

## 🔧 Method:

Use a minimal linker script to explicitly control where .text and .data sections are placed in memory:

```bash
SECTIONS
{
    .text 0x00000000 :
    {
        *(.text*)
    }

    .data 0x10000000 :
    {
        *(.data*)
    }
}
```

## 📘 Discussion:
✅ Purpose of Linker Script:

The linker script controls how sections of code and data are placed in memory when building a bare-metal ELF file.

Here, .text is placed at 0x00000000 (typically Flash), and .data at 0x10000000 (typically SRAM).

✅ Flash vs SRAM:

Flash (ROM) is non-volatile, retains contents after power-off, and is usually used for executable code (.text).

SRAM (RAM) is volatile, faster, and used for modifiable data (.data).

Splitting .text and .data between Flash and SRAM is common in embedded systems to maximize efficiency and performance.
