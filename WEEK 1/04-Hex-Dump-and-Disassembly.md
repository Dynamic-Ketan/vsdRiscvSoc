# 🛠️ Task 4: Hex Dump & Disassembly

This task demonstrates how to convert an ELF file into a raw hex file and how to disassemble it using `objdump`. It also explains the meaning of each column in the disassembly output.

---

## 🛠️ Step 1: Disassemble the ELF File

Run the following command to disassemble the `hello.elf` file and save the output to `hello.dump`:

```bash
/home/ketan/tools/riscv/bin/riscv32-unknown-elf-objdump -d hello.elf > hello.dump
```

## 🛠️ Step 2: Convert ELF to Raw Hex
Use objcopy to convert the ELF file into an Intel HEX format file (hello.hex):

```bash
/home/ketan/tools/riscv/bin/riscv32-unknown-elf-objcopy -O ihex hello.elf hello.hex
```

## 🔍 Step 3: Understand the Disassembly Output
Open hello.dump and observe one instruction line

```bash
cat hello.dump
```

Output:

```bash
000100b4 <exit>:
   100b4:	1141                	addi	sp,sp,-16
   100b6:	4581                	li	a1,0
   100b8:	c422                	sw	s0,8(sp)
   100ba:	c606                	sw	ra,12(sp)
```

Explanation of each field:

| Column       | Meaning                           |
|--------------|---------------------------------|
| 000100b4     | Address of the instruction       |
| 1141         | Machine code opcode (in hex)     |
| addi         | Mnemonic (assembly instruction) |
| sp, sp, -16  | Operands (registers and values)  |

The address is where the instruction resides in memory.

The opcode is the raw machine code.

The mnemonic is the human-readable instruction.

The operands specify the registers and immediate values used.

![image](https://github.com/user-attachments/assets/3951504e-586d-43f7-8c1d-7689d0401165)
