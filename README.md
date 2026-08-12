# CVFS

Customised Virtual File System — a from-scratch simulation of core Linux file system internals, implemented entirely in C.

## Overview

Marvellous CVFS is a custom implementation of a Virtual File System (VFS) that simulates the core functionality of the Linux file system, entirely in memory. It ships with its own interactive shell, giving a Linux-like file handling experience — `creat`, `read`, `write`, `stat`, `unlink`, `ls` — without touching the real OS file system.

The project was built as a systems programming exercise to gain hands-on understanding of:

- System calls and how they're implemented under the hood
- File handling and I/O offset management
- Manual memory management (`malloc` / `free`)
- Core OS data structures used by real file systems

## Key Features

- **Custom shell interface** — interactive `Marvellous CVFS :>` prompt with Linux-style commands for file operations
- **System call simulation** — self-written implementations of `creat`, `read`, `write`, `stat`, and `unlink`
- **OS data structures** — Incore Inode Table (DILB), File Table, UAREA, User File Descriptor Table (UFDT)
- **Platform independent** — pure standard C, compiles and runs anywhere a C compiler is available
- **Built-in help system** — `help` and `man <command>` mimic Linux manual pages from within the shell

## Architecture

| Component | Role |
|---|---|
| Boot Block | Holds boot-time metadata for the simulated file system |
| Super Block | Tracks total and free inode counts |
| Inode (DILB) | Linked list of inodes — name, size, type, permissions, reference count, data buffer |
| UAREA / UFDT | Simulated per-process user area mapping file descriptors to open files |
| File Table | Tracks read/write offsets and access mode, links back to its inode |

On startup, CVFS initializes the UAREA, superblock, and inode list, then enters an interactive command loop that parses and dispatches commands to the corresponding file operations.

## Supported Commands

| Command | Description |
|---|---|
| `help` | Display the list of available commands |
| `man <command>` | Display the manual page for a specific command |
| `clear` | Clear the terminal screen |
| `ls` | List the names of all existing files |
| `ls -a` | List all files with inode number and file size |
| `creat <file_name> <permission>` | Create a new file — permission: `1`=Read, `2`=Write, `3`=Read+Write |
| `stat <file_name>` | Display statistical information about a file |
| `write <fd>` | Write data into the file identified by the given file descriptor |
| `read <fd> <size>` | Read the given number of bytes from a file |
| `unlink <file_name>` | Delete an existing file |
| `exit` | Terminate the CVFS shell |

Note: file creation uses `creat` (not `create`) and deletion uses `unlink` (not `rm`), matching standard Unix system call naming conventions.



## Getting Started

### Prerequisites

- A C compiler (`gcc` or equivalent)
- Any OS with a POSIX-compatible C environment (Linux/macOS natively, WSL/MinGW on Windows)

### Build

```
gcc CVFS_CODE.c -o cvfs
```

### Run

```
./cvfs
```

## Example Usage

```
Marvellous CVFS : > creat Demo.txt 3
File succesfully created with FD : 3

Marvellous CVFS : > write 3
Enter the data that you want to write into the file
Jay Ganesh
11 bytes gets succesfully written into the file

Marvellous CVFS : > read 3 11
Read operation is succesful
Data from file is :
Jay Ganesh

Marvellous CVFS : > ls
Demo.txt

Marvellous CVFS : > unlink Demo.txt

Marvellous CVFS : > exit
Thank you for using Marvellous CVFS
Deallocating all resources of Marvellous CVFS
```

## Project Structure

```
CVFS_PROJECT/
├── CVFS_CODE.c   # Complete implementation of the virtual file system
└── README.md     # Project documentation
```

## Learning Outcomes

- Deep understanding of Linux File System internals
- Practical knowledge of OS data structures (inode, file tables, UAREA)
- Strong grasp of system programming in C
- Hands-on experience with shell design and command interpretation
- Applied low-level logic building for OS-like environments

## Author

Yash Avinash Mirge


 
#NOTE -: This project is a work in progress. Further advancements and features may be added over time, and the current version is not final.

<div align="center">

⭐ If this repository helped you learn or revise C, consider giving it a star!

</div>

