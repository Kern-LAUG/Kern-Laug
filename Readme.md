# Kern Programming Language

## Overview

Kern is a lightweight programming language with **Python-like syntax and Rust-level performance**.

Kern works by **transpiling `.kern` files into Rust code**, then compiling them using `rustc` to produce executable programs.

Currently Kern targets **Windows** and generates `.exe` binaries.

---

# Features

### `fn main`

Defines the entry point of a Kern program.

```kern
fn main {
```

---

### Variables

Kern supports **immutable** and **mutable** variables.

#### Immutable variable

```kern
let name = "Kern"
```

#### Mutable variable

```kern
let mut counter = 5
```

---

### `print`

Outputs text or variables to the console.

```kern
print "Hello"
print name
```

---

### `pause`

Pauses execution until the user presses **Enter**.

```kern
pause
```

---

### Block Closing

Blocks are closed with:

```kern
}
```

---

# Limitations

The following features are **not yet supported**:

* Arrays or lists
* Loops (`for`, `while`, `repeat`)
* Conditionals (`if`, `else`)
* Functions beyond `fn main`
* User input
* Error reporting for invalid syntax

Unsupported lines may be ignored during transpilation.

---

# Installation

## 1. Prerequisites

Make sure the following are installed:

* Rust
* Visual Studio Build Tools 2022 (required for compiling Rust on Windows)

Install Rust:

https://www.rust-lang.org/tools/install

---

## 2. Folder Setup

Place the Kern folder in:

```
C:\Kern\
```

Example structure:

```
C:\Kern\
    compiler\
        kernc.exe
```

---

## 3. Add Kern to PATH

1. Press **Windows + S**
2. Search **Environment Variables**
3. Click **Edit the system environment variables**
4. Click **Environment Variables**
5. Under **User variables**, select **Path**
6. Click **Edit → New**
7. Add:

```
C:\Kern\compiler\
```

8. Click **OK** on all windows.

---

## 4. Restart Terminal

Open a **new Command Prompt or PowerShell** for the PATH changes to apply.

---

# Commands

| Command                   | Description                       |
| ------------------------- | --------------------------------- |
| `kernc build <file.kern>` | Transpile and compile to `.exe`   |
| `kernc run <file.kern>`   | Compile and run program           |
| `kernc clean <file.kern>` | Remove generated `.rs` and `.exe` |

---

# Usage Examples

## Build a Kern program

```cmd
kernc build main.kern
```

---

## Run a Kern program

```cmd
kernc run main.kern
```

---

## Clean generated files

```cmd
kernc clean main.kern
```

---

# Example Kern Program

```kern
fn main {
    let name = "Kern"
    let mut number = 5

    print name
    print number

    pause
}
```

---

# Transpiled Rust Code

The Kern compiler generates Rust code like this:

```rust
fn main() {
    let name = "Kern";
    let mut number = 5;

    println!("{}", name);
    println!("{}", number);

    use std::io::{self, Write};
    print!("Press Enter to continue...");
    io::stdout().flush().unwrap();

    let mut input = String::new();
    io::stdin().read_line(&mut input).ok();
}
```

The code is compiled using:

```
rustc main.rs
```

---

# Roadmap / Future Features

Planned improvements for Kern:

* Arrays and lists
* Loops (`for`, `while`, `repeat`)
* Conditionals (`if`, `else`)
* User input support
* Multiple functions
* Error handling
* Debugging tools
* Cross-platform compilation (Linux / macOS)
* Improved syntax parser

---

# Notes

* Kern currently **only supports Windows**
* The compiler generates `.exe` files
* Rust (`rustc`) must be installed
* Make sure the `compiler` directory is in your **PATH** so `kernc` can run from any terminal
