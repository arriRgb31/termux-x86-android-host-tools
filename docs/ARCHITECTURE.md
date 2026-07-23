# Architecture

## Overview

This project provides a reproducible Android x86_64 host environment running on an Android ARM64 device.

Instead of using a physical x86_64 computer, the host environment is created with Termux, PRoot-Distro, Ubuntu x86_64, and QEMU User Mode.

---

## System Architecture

```
+------------------------------------------------------+
|                  Android ARM64 Device                |
+------------------------------------------------------+
                        │
                        ▼
                    Termux
                        │
                        ▼
                 PRoot-Distro
                        │
                        ▼
               Ubuntu 24.04 x86_64
                        │
                        ▼
             QEMU User Mode Emulator
                        │
                        ▼
          Android x86_64 Host Environment
                        │
                        ▼
        Android Build System (Soong/Ninja)
                        │
                        ▼
              Android Build Targets
```

---

## Components

### Android

Provides the Linux kernel and userspace required by Termux.

---

### Termux

Acts as the native userspace.

Responsibilities:

- Package manager
- Git
- Storage access
- Host utilities
- Launch environment

---

### PRoot-Distro

Creates a Linux userspace without requiring root.

Responsibilities:

- Ubuntu installation
- Filesystem isolation
- User environment

---

### Ubuntu x86_64

Provides a standard Linux environment expected by Android build tools.

Responsibilities:

- glibc
- apt
- build packages
- shell environment

---

### QEMU User Mode

Translates x86_64 instructions into ARM64 instructions.

Responsibilities:

- Execute x86_64 binaries
- Run Go compiler
- Run Java
- Execute Android host tools

---

### Android Host Tools

Includes:

- Go
- OpenJDK
- Ninja
- CMake
- Repo
- Git
- Python
- Android Bootstrap

---

### Android Build System

Responsible for:

- Blueprint
- Soong
- Ninja
- Make wrappers
- Build targets

---

## Project Scope

Included

- Android Host Environment
- Installation
- Configuration
- Verification
- Documentation

Excluded

- Device Trees
- Vendor Boot
- Recovery
- Kernel
- ROM Development
- Device-specific debugging

---

## Current Status

Implemented

- Termux
- Ubuntu x86_64
- QEMU User Mode
- Android Bootstrap
- lunch

In Progress

- Documentation
- Installation Scripts
- Verification Tools

Planned

- Automated Installer
- Validation Scripts
- Benchmarks
