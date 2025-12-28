# Asm-Buffered-IO

![Language: Assembly x86-64](https://img.shields.io/badge/Language-Assembly_x86--64-blue)
![Language: C](https://img.shields.io/badge/Language-C-blue)
![Platform: Linux](https://img.shields.io/badge/Platform-Linux-green)
![License: Personal/Educational](https://img.shields.io/badge/License-Personal_Use_Only-red)

**Asm-Buffered-IO** is a robust, low-level Input/Output library written in x86-64 Assembly. It provides efficient buffered reading and writing operations (integers, characters, and strings) and is designed for seamless interoperability with C.

This project serves as an educational demonstration of system-level programming, buffer management, and the System V AMD64 ABI calling conventions.

---

## 📖 Table of Contents

- [Features](#-features)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [API Reference](#-api-reference)
- [Internal Architecture](#-internal-architecture)
- [License](#-license)

---

## 🚀 Features

* **High-Performance Buffering**: Implements 1024-byte internal buffers for both input (`stdin`) and output (`stdout`) to minimize system calls.
* **Type Support**: Native handling for signed integers (`long long`), strings, and individual characters.
* **Whitespace Handling**: Intelligent parsing that skips whitespace (spaces, tabs, newlines) when reading integers.
* **C Interoperability**: Fully compatible with C programs via the `my_iolib.h` header.
* **Position Control**: Direct access to buffer cursors allows for advanced stream manipulation (rewinding, peeking).

---

## 📂 Project Structure

| File | Description |
| :--- | :--- |
| **`lab3_lib.s`** | Core library implementation in x86-64 Assembly. Contains all buffer logic. |
| **`my_iolib.h`** | C header file defining the function prototypes for integration. |
| **`Mprov64.s`** | Assembly test program. Demonstrates calling library functions from Assembly. |
| **`test_prog.c`** | C test program. Demonstrates calling library functions from C. |
| **`Makefile`** | Automated build script for compiling and linking all components. |

---

## 🛠 Getting Started

### Prerequisites

Ensure you have the following tools installed on your Linux system:
* **GCC** (GNU Compiler Collection)
* **GNU Assembler (as)** (part of binutils)
* **Make**

### Installation & Build

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/Mouaz7/Asm-Buffered-IO.git](https://github.com/Mouaz7/Asm-Buffered-IO.git)
    cd Asm-Buffered-IO
    ```

2.  **Compile the project:**
    Use the provided Makefile to build both the Assembly and C test executables.
    ```bash
    make
    ```

3.  **Run the Tests:**
    * **Assembly Test:**
        ```bash
        ./asmTest
        ```
    * **C Test:**
        ```bash
        ./cTest
        ```

4.  **Clean Up:**
    To remove compiled binaries and object files:
    ```bash
    make clean
    ```

---

## 📚 API Reference

The library exposes the following functions for use in C or Assembly:

### Input Functions

| Function | Signature (C) | Description |
| :--- | :--- | :--- |
| **`inImage`** | `void inImage()` | Refills the internal input buffer from `stdin` using `fgets`. Resets the buffer position to 0. |
| **`getInt`** | `long long getInt()` | Parses and returns a signed 64-bit integer from the input buffer. Skips whitespace automatically. |
| **`getText`** | `int getText(char *dest, int max)` | Reads a string into `dest` up to `max` characters. Stops at newline or buffer limit. |
| **`getChar`** | `void getChar()` | Reads a single character from the input buffer. |
| **`getInPos`** | `int getInPos()` | Returns the current cursor position in the input buffer. |
| **`setInPos`** | `void setInPos(int pos)` | Sets the cursor position in the input buffer. Clamped between 0 and Buffer Size. |

### Output Functions

| Function | Signature (C) | Description |
| :--- | :--- | :--- |
| **`outImage`** | `void outImage()` | Flushes the output buffer to `stdout` using `puts` and resets the position to 0. |
| **`putInt`** | `void putInt(long long val)` | Converts a signed 64-bit integer to a string and writes it to the output buffer. Auto-flushes if full. |
| **`putText`** | `void putText(char *str)` | Writes a null-terminated string to the output buffer. Auto-flushes if full. |
| **`putChar`** | `void putChar(char c)` | Writes a single character to the output buffer. Auto-flushes if full. |
| **`getOutPos`** | `int getOutPos()` | Returns the current cursor position in the output buffer. |
| **`setOutPos`** | `void setOutPos(int pos)` | Sets the cursor position in the output buffer. Useful for modifying pending output (e.g., removing trailing characters). |

---

## ⚙ Internal Architecture

The library manages memory using two static buffers defined in the `.data` section:
* **`inBuf`**: 1024 bytes (Input)
* **`outBuf`**: 1024 bytes (Output)

It bridges low-level Assembly with high-level OS streams by dynamically linking against `libc` standard functions:
* `fgets` is used for reading chunks of data.
* `puts` is used for flushing data to the terminal.

This hybrid approach ensures that the Assembly code remains portable across systems with compatible standard C libraries.

---

## ⚖ License

**Copyright (c) 2025 Mouaz7.** All rights reserved.

This source code and associated files are provided for **personal, educational, and demonstration purposes only**.

### Terms of Use:
1.  **No Commercial Use:** You may not use this code for commercial purposes.
2.  **No Redistribution:** You may not copy, modify, merge, publish, distribute, sublicense, or sell any part of the code without explicit permission.
3.  **Attribution:** You must retain this copyright notice in all copies or substantial portions of the software.

By accessing and using this repository, you agree to these terms.
