# ⚡ 13 Interrupt Primer

## Question

**Demonstrate how to enable the machine-timer interrupt (MTIP) and write a simple handler in C/asm.**

## Answer Highlights

### 1. Enabling the Machine-Timer Interrupt
- Write the desired compare value to the `mtimecmp` register (memory-mapped timer compare register).
- Set the Machine Interrupt Enable (`mie`) register’s timer interrupt bit (`MTIE`).
- Enable global interrupts by setting the Machine Status Register (`mstatus`) Interrupt Enable bit (`MIE`).

### 2. Writing the Interrupt Service Routine (ISR)
- Use `__attribute__((interrupt))` in C for the ISR function to ensure proper prologue/epilogue.
- Alternatively, write a “naked” ISR in assembly with explicit context saving/restoring.

### 3. Polling and Handling
- When the timer interrupt fires, the handler runs.
- Inside the ISR, clear or update `mtimecmp` to schedule the next interrupt.
- Return from interrupt properly to resume normal execution.


