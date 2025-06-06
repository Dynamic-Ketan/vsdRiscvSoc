# 🔄 14 rv32imac vs rv32imc – What’s the “A”?

## Question

**Explain the ‘A’ (atomic) extension in `rv32imac`. What instructions are added and why are they useful?**

## Answer Highlights

### 1. What is the 'A' Extension?

The `'A'` in `rv32imac` stands for **Atomic** instructions.

- This extension adds **special instructions** to perform atomic memory operations — that is, operations that **cannot be interrupted** mid-way.
- It ensures **data integrity** when multiple cores or threads try to access the same memory simultaneously.
- This is especially important in **multithreaded programs**, **operating systems**, and **synchronization** mechanisms.

---

### 2. Key Instructions Introduced

The Atomic extension includes two main categories:

#### a. Load-Reserved / Store-Conditional Pair
These are used for building custom atomic operations:

- `lr.w` – **Load Reserved Word**: Reads a word and reserves the address.
- `sc.w` – **Store Conditional Word**: Writes a word only if the reservation is still valid (i.e., no one else wrote to that address since the `lr.w`).

This pattern forms the **basis of lock-free synchronization**.

#### b. Atomic Memory Operations (AMO)
These are one-instruction atomic read-modify-writes:

- `amoadd.w` – Atomically add a value to memory.
- `amoswap.w` – Atomically swap values.
- `amoor.w`, `amoand.w`, `amoxor.w`, etc. – Perform bitwise operations atomically.

Each of these follows this format:

```assembly
amoadd.w rd, rs2, (rs1)
