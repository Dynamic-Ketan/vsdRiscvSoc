# 📝 Task 8: Exploring GCC Optimisation

## 🛠️ Step 1: Compile the Same File with Different Optimization Flags

Run these two commands to generate assembly .s files

```bash
gcc -O0 -S hello.c -o hello_O0.s
gcc -O2 -S hello.c -o hello_O2.s
```

## 🔍 Step 2: Compare the Assembly Listings Side-by-Side

Command line diff side-by-side:

```bash
diff -y hello_O0.s hello_O2.s | less
```

## 🧠 Step 3: Key Differences to Look For and Why They Occur

| Optimization Aspect       | `-O0` Output                                | `-O2` Output                      | Explanation                                                    |
| ------------------------- | ------------------------------------------- | --------------------------------- | -------------------------------------------------------------- |
| **Dead Code Elimination** | Variables and code are kept even if unused  | Unused variables and code removed | Saves space and CPU time by eliminating redundant instructions |
| **Register Allocation**   | Heavy stack usage, more memory loads/stores | Registers used efficiently        | Reduces memory accesses, speeds up execution                   |
| **Function Inlining**     | Functions called explicitly                 | Small functions may be inlined    | Removes call overhead, enables further optimization            |
| **Instruction Count**     | More, straightforward instructions          | Fewer, optimized instructions     | Optimized code is smaller and faster                           |
| **Stack Frame Setup**     | Full prologue and epilogue                  | Simplified or omitted if possible | Avoids unnecessary setup/teardown for efficiency               |
