# 🛠️ Task 5: ABI & Register Cheat-Sheet (RV32)

## Question
List all 32 RV32 integer registers with their ABI names and typical calling-convention roles.

## Answer Outline

| Register Number | ABI Name | Role / Usage                     |
|-----------------|----------|--------------------------------|
| x0              | zero     | Hardwired zero                  |
| x1              | ra       | Return address                 |
| x2              | sp       | Stack pointer                 |
| x3              | gp       | Global pointer                |
| x4              | tp       | Thread pointer                |
| x5-x7           | t0-t2    | Temporaries (caller-saved)    |
| x8              | s0/fp    | Saved register / frame pointer (callee-saved) |
| x9              | s1       | Saved register (callee-saved)  |
| x10-x17         | a0-a7    | Function arguments / return values |
| x18-x27         | s2-s11   | Saved registers (callee-saved) |
| x28-x31         | t3-t6    | Temporaries (caller-saved)    |

## Calling Convention Summary

- **a0-a7**: Used for passing arguments and returning values from functions.  
- **s-registers (s0-s11)**: Callee-saved registers, meaning the called function must preserve their values.  
- **t-registers (t0-t6)**: Caller-saved registers, meaning the caller must save them if needed across calls.

