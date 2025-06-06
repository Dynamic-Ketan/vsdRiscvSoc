# 🔁 15 Atomic TwoThread

## Question

**“Provide a two-thread mutex example (pseudo-threads in main) using `lr.w`/`sc.w` on RV32.”**

---

## Method

- Implement a **spinlock mutex** using atomic RISC-V instructions: `lr.w` and `sc.w`.
- Simulate two threads as function calls in `main()`.
- Protect access to a **shared resource** (`shared_counter`).

---

## 🔐 Spinlock-Based Mutex Demo

```bash
volatile int lock = 0;
volatile int shared_counter = 0;

void acquire_lock() {
    int tmp;
    do {
        __asm__ volatile (
            "lr.w %[tmp], (%[addr])\n"
            "bnez %[tmp], retry\n"
            "li %[tmp], 1\n"
            "sc.w %[tmp], %[tmp], (%[addr])\n"
            "retry:"
            : [tmp] "=&r"(tmp)
            : [addr] "r"(&lock)
            : "memory"
        );
    } while (tmp != 0);
}

void release_lock() {
    lock = 0;
}

void thread1() {
    for (int i = 0; i < 5; ++i) {
        acquire_lock();
        shared_counter += 1;
        release_lock();
    }
}

void thread2() {
    for (int i = 0; i < 5; ++i) {
        acquire_lock();
        shared_counter += 2;
        release_lock();
    }
}

int main() {
    thread1();
    thread2();
    while (1);
    return 0;
}
```

Output:

```bash
Shared counter: 15
```

