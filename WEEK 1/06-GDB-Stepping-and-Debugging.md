# ✅ 6. Stepping with GDB

## 🛠️ Step 1: Start GDB with ELF

```bash
riscv32-unknown-elf-gdb hello.elf
```

Starts GDB with your program loaded.

## 🛠️ Step 2: Connect to Simulator

```bash
(gdb) target sim
```

Connects GDB to the built-in RISC-V simulator.

## 🛠️ Step 3: Set Breakpoint at main

```bash
(gdb) break main
```

## 🛠️ Step 4: Run the Program

```bash
(gdb) run
```

## 🛠️ Step 5: Step Through the Program
Step one machine instruction at a time:

```bash
(gdb) step
```

## 🛠️ Step 6: Inspect Registers
Inspect all general-purpose registers:

```bash
(gdb) info registers
```

## Output:
```bash
ra             0x0      0
sp             0x800000 0x800000
gp             0x0      0
tp             0x0      0
```

## 🛠️ Step 7: Disassemble the Code
Disassemble code around current PC:

```bash
(gdb) disassemble
```

## Output:

```bash
Dump of assembler code for function main:
   0x00010178 <main>:
   0x00010178:  addi    sp,sp,-16
   0x0001017c:  sw      ra,12(sp)
   0x00010180:  sw      s0,8(sp)
   0x00010184:  addi    s0,sp,16
```

## 🛠️ Step 8: Continue Execution
Run until the program finishes:

```bash
(gdb) continue
```

## Output:
```bash 
Hello, RISC-V!
[Inferior 1 (process) exited normally]
```

## 🛠️ Step 9: Quit GDB

```bash
(gdb) quit
```



