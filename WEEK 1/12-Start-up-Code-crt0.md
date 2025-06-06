# 🚀 12 Start-up Code & crt0

## Question

**What does `crt0.S` typically do in a bare-metal RISC-V program and where do I get one?**

## Answer Highlights

### 1. Startup Responsibilities
- Sets up the **stack pointer**.
- Zeroes the **`.bss`** section (uninitialized data).
- Calls the **`main()`** function.

### 2. Post-main Behavior
- Enters an **infinite loop** if `main()` returns to prevent running into invalid code.

### 3. Where to Find `crt0.S`
- Device-specific examples are available in many RISC-V SDKs (e.g., SiFive SDK).
- Generic startup files can be found in open-source libraries like **Newlib**.
