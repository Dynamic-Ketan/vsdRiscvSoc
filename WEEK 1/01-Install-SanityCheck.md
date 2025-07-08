# 🚀 RISC-V Toolchain Setup Guide (rv32imac)

This guide walks you through installing and verifying the RISC-V GNU Toolchain (rv32imac) on a 64-bit Ubuntu system.

---

## 📦 Step 1: Extract the Toolchain

Open your terminal and run:

```bash
cd ~/Downloads
tar -xzvf riscv-toolchain-rv32imac-x86_64-ubuntu.tar.gz
```

## 🛠️ Step 2: Add the Toolchain to PATH

Append the following line to your shell configuration file:

```bash
echo 'export PATH=$PATH:$HOME/Downloads/opt/riscv/bin' >> ~/.bashrc
```

Then apply the change:

```bash
source ~/.bashrc
```

## ✅ Step 3: Verify the Installation

Run the following commands to check that the RISC-V tools are installed correctly:

```bash
riscv32-unknown-elf-gcc --version
riscv32-unknown-linux-gnu-gcc --version
```
Output:

```bash
riscv32-unknown-elf-gcc (g04696df096) 14.2.0
Copyright (C) 2024 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

riscv32-unknown-linux-gnu-gcc (GCC) 14.2.0
Copyright (C) 2024 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

![image](https://github.com/user-attachments/assets/1434f81c-c60f-426c-8a4d-3d73c2c88064)


