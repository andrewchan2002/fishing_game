Here's the `README` file that describes the functionalities of `lab10.c`, `error.c`, and the relevant functions from `apue.h`.

---

# README

## Overview

This project consists of three main components: `lab10.c`, `error.c`, and the associated `apue.h` header file. Together, they implement a signal-driven fishing game and error handling functions for managing system calls and application errors.

### How to Build

You can use the provided `Makefile` to compile the source files and generate the executable. Simply run:

```bash
make
```

This will compile and link the necessary files, producing an executable file.

## Source Files

### 1. `lab10.c`
This file contains the main logic for a simple fishing game where signals (`SIGINT`, `SIGTSTP`, and `SIGALRM`) control various aspects of the gameplay. Here's an overview of the functions:

- **`main()`**: Initializes signal handlers for `SIGINT`, `SIGTSTP`, and `SIGALRM`. It then waits for user input or a signal to proceed with the game.
  
- **`put_pull_rod(int signum)`**: Handles the fishing actions. When `SIGINT` is received, the fishing rod can either be "put" into the water to wait for a fish or "pulled" to try and catch a fish. If the rod is pulled and the fish is caught, the number of caught fish increases.

- **`fish_eating(int signum)`**: Simulates the event of a fish biting the bait. When this signal (`SIGALRM`) is received, the player is notified that a fish is biting and should pull the rod to catch it.

- **`exit_game(int signum)`**: Handles the game exit when `SIGTSTP` is received. It prints the total number of caught fish before exiting the program.

### 2. `error.c`
This file defines various error-handling functions, useful when working with system calls. Here's an overview of the key functions:

- **`err_ret(const char *fmt, ...)`**: Prints a non-fatal error message related to a system call and returns to the caller. The error message includes the reason from `errno`.

- **`err_sys(const char *fmt, ...)`**: Prints a fatal error message related to a system call and terminates the program.

- **`err_exit(int error, const char *fmt, ...)`**: Prints a fatal error message unrelated to a system call (the error code is passed explicitly) and terminates the program.

- **`err_dump(const char *fmt, ...)`**: Prints a fatal error message related to a system call, dumps core, and terminates the program.

- **`err_msg(const char *fmt, ...)`**: Prints a non-fatal error message unrelated to a system call.

- **`err_quit(const char *fmt, ...)`**: Prints a fatal error message unrelated to a system call and terminates the program.

### 3. `apue.h`
This header file defines various utility macros, type definitions, and function prototypes commonly used in POSIX-compliant programs. Key aspects include:

- **Error Handling**: Functions like `err_ret`, `err_sys`, `err_quit`, and others for consistent and convenient error reporting.

- **Signal Handling**: Includes a type definition for signal handler functions (`Sigfunc`) and various utility functions for managing signals.

- **File and Directory Permissions**: Macros like `FILE_MODE` and `DIR_MODE` to define default permissions for new files and directories.

- **Terminal I/O**: Provides prototypes for functions dealing with terminal settings, such as `tty_raw`, `tty_reset`, and `tty_cbreak`.

- **Utility Functions**: Includes miscellaneous helper functions like `path_alloc`, `sleep_us`, `readn`, `writen`, and functions for working with pipes and file descriptors.

## Makefile

A simple `Makefile` is used to build the project. The `Makefile` compiles all the `.c` files and links them into a single executable. It should look something like this:

To compile and run the program:

```bash
make
./fishing_game
```

## Signal Controls

- **SIGINT (`Ctrl+C`)**: Used to simulate putting and pulling the fishing rod. The first `Ctrl+C` puts the rod into the water, and the second `Ctrl+C` pulls it out.
  
- **SIGTSTP (`Ctrl+Z`)**: Used to exit the game and display the total number of caught fish.

- **SIGALRM**: Simulates the action of a fish biting the bait. It is triggered after a random amount of time once the rod is put into the water.

---
