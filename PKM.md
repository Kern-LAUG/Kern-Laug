# PKM – Kern Package Manager

## Overview

**PKM** is the package manager for the **Kern programming language**.
It allows you to install, update, remove, and create Kern packages and applications.

PKM downloads packages from **GitHub repositories** and verifies them using a required file called:

```
includemeinpkm.toml
```

---

# Features

* Install packages from GitHub
* Create Kern libraries and applications
* Update packages with version comparison
* Remove installed packages
* List installed packages
* Simple version checking system

---

# Requirements

Before installing PKM, make sure you have:

* Rust installed
* Git installed
* The Kern compiler (`kernc`) installed

---

# Installation

## 1. Build PKM

Navigate to the PKM project folder and build the release binary:

```
cargo build --release
```

After building, the compiled program will be located at:

```
target/release/pkm.exe
```

---

## 2. Move PKM to Kern Folder

Move the compiled executable to the PKM folder inside your Kern directory:

```
C:\Kern\pkm\pkm.exe
```

Example folder layout:

```
C:\Kern\
    kernc\
        kernc.exe
    pkm\
        pkm.exe
```

---

## 3. Add PKM to PATH

To run `pkm` from any terminal, add the PKM folder to your system PATH.

### Windows Instructions

1. Press **Windows + S**
2. Search **Environment Variables**
3. Click **Edit the system environment variables**
4. Click **Environment Variables**
5. Under **User variables**, find **Path**
6. Click **Edit**
7. Click **New**
8. Add the following path:

```
C:\Kern\pkm
```

9. Click **OK** on all windows.

Restart your terminal for the changes to apply.

You should now be able to run:

```
pkm
```

from any Command Prompt or PowerShell window.

---

# Commands

| Command                   | Description                                           |
| ------------------------- | ----------------------------------------------------- |
| `pkm list`                | List installed Kern packages in the current directory |
| `pkm install <user/repo>` | Install a package from GitHub                         |
| `pkm uninstall <package>` | Remove an installed package                           |
| `pkm createpak <name>`    | Create a new Kern library package                     |
| `pkm createapp <name>`    | Create a new Kern application                         |
| `pkm update <user/repo>`  | Update a package if a newer version exists            |

---

# Package Verification

PKM requires every package repository to contain the file:

```
includemeinpkm.toml
```

Example:

```
name = "math"
version = "1.0.0"
type = "lib"
```

Required fields:

| Field   | Description                                |
| ------- | ------------------------------------------ |
| name    | Package or app name                        |
| version | Version number                             |
| type    | `lib` for library or `app` for application |

If this file is missing or invalid, PKM will delete the downloaded repository.

---

# Example Library Package

```
math/
 ├ includemeinpkm.toml
 └ package.kern
```

Example `includemeinpkm.toml`:

```
name = "math"
version = "1.0.0"
type = "lib"
```

---

# Example Application

```
hello/
 ├ includemeinpkm.toml
 └ main.kern
```

Example `includemeinpkm.toml`:

```
name = "hello"
version = "0.1.0"
type = "app"
```

---

# Usage Examples

## Install a package

```
pkm install username/math
```

---

## Update a package

```
pkm update username/math
```

If the remote version is higher, PKM will reinstall the package.

If the local version is higher, PKM will ask if you want to downgrade.

---

## List packages

```
pkm list
```

---

## Remove a package

```
pkm uninstall math
```

---

## Create a library

```
pkm createpak math
```

Creates:

```
math/
 ├ includemeinpkm.toml
 └ package.kern
```

---

## Create an application

```
pkm createapp hello
```

Creates:

```
hello/
 ├ includemeinpkm.toml
 └ main.kern
```

---

# Version System

PKM uses **semantic versioning**:

```
MAJOR.MINOR.PATCH
```

Example:

```
1.0.0
1.1.0
1.1.2
2.0.0
```

Update rules:

| Local  | Remote | Action                |
| ------ | ------ | --------------------- |
| lower  | higher | update                |
| same   | same   | keep installed        |
| higher | lower  | ask user to downgrade |

---

# Example Workflow

Create an app:

```
pkm createapp hello
```

Install a library:

```
pkm install user/math
```

Compile the program:

```
kernc build main.kern
```

---

# Future Features

Planned improvements for PKM:

* Dependency installation
* Package publishing
* Package search
* Version locking
* Automatic dependency updates
* Offline package cache

---

# Notes

* PKM uses GitHub repositories as the package source.
* Git must be installed for PKM to download packages.
* PKM only installs repositories containing `includemeinpkm.toml`.
* PKM is designed specifically for the Kern programming ecosystem.
* **A:** Do not currently develop libraries for PKM yet, as the library system for Kern is not fully implemented.
* **B:** Inside the `pkm` folder there will be a `packages` folder. When libraries become available, it is recommended to install them there.
* **C:** Packages are installed into the directory where they will remain **until they are deleted or moved by the user**.
