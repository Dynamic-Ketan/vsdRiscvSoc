# 🛠️ Task 3: From C to Assembly (RV32IMC)
This task demonstrates how to generate the assembly (.s) file from a C program using the RISC-V toolchain for RV32IMC and explains key assembly prologue/epilogue instructions.

## 🛠️ Step 1: Generate Assembly (.s) File

Use the RISC-V GCC to compile the C file into an assembly file:

```bash
/home/ketan/tools/riscv/bin/riscv32-unknown-elf-gcc -S -O0 -march=rv32imc -mabi=ilp32 hello.c
```

This creates hello.s in the current directory.

## 👀 Step 2: View the Generated Assembly

To view the generated .s file:

```bash
cat hello.s
```

## 🔍 Step 3: Understand the Prologue & Epilogue

Output:

```bash
	.file	"hello.c"
	.option nopic
	.attribute arch, "rv32i2p1_m2p0_c2p0"
	.attribute unaligned_access, 0
	.attribute stack_align, 16
	.text
	.section	.rodata
	.align	2
.LC0:
	.string	"Hello, RISC-V!"
	.text
	.align	1
	.globl	main
	.type	main, @function
main:
	addi	sp,sp,-16
	sw	ra,12(sp)
	sw	s0,8(sp)
	addi	s0,sp,16
	lui	a5,%hi(.LC0)
	addi	a0,a5,%lo(.LC0)
	call	puts
	li	a5,0
	mv	a0,a5
	lw	ra,12(sp)
	lw	s0,8(sp)
	addi	sp,sp,16
	jr	ra
	.size	main, .-main
	.ident	"GCC: (g04696df096) 14.2.0"
	.section	.note.GNU-stack,"",@progbits
```

🟦 Prologue:

addi sp, sp, -16 → allocates 16 bytes on stack

sw ra, 12(sp) → saves return address

🟩 Epilogue:

lw ra, 12(sp) → restores return address

addi sp, sp, 16 → deallocates stack space

ret → returns from main
