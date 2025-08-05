# GDB – GNU Debugger (Full Detailed Explanation)

## 🔷 1. What is GDB?
GDB (GNU Debugger) is a powerful open-source debugging tool used to analyze and control the execution of C, C++, and Assembly programs. It allows you to:

- Inspect variables and memory
- Set breakpoints and watchpoints
- Step through source code
- Debug both user space and embedded applications
- Analyze core dumps
- Attach to a running process

## 🔷 2. Why GDB?
Memory corruption, segmentation faults, and logic bugs are hard to catch by just reading code or using printf. GDB helps you:

- Trace runtime errors
- Understand program flow
- Examine variable values at any point
- Modify variables and control program execution during debugging

## 🔷 3. GDB Architecture Overview
GDB operates in two modes:

- **Local Debugging**: Debug your own compiled program
- **Remote Debugging**: Debug a target program running on another system (via `gdbserver`)

### 🔹 Flow:

```
[Source Code] → [Compile with -g] → [Run in GDB] → [Breakpoints/Inspect/Modify/Step]
```

## 🔷 4. How to Install GDB

### Ubuntu/Debian:

```bash
sudo apt install gdb
```

### Fedora/RHEL:

```bash
sudo dnf install gdb
```

### macOS:

```bash
brew install gdb
```

## 🔷 5. Compiling for GDB (With Debug Symbols)
Use `-g` to include debug information:

```bash
gcc -g myprog.c -o myprog
```

Avoid `-O2` or `-O3` during debugging as it optimizes away variables.

## 🔷 6. Starting GDB

```bash
gdb ./myprog
```

Or:

```bash
gdb
(gdb) file myprog
(gdb) run
```

## 🔷 7. Core Commands in GDB

| Command     | Purpose                               |
|-------------|----------------------------------------|
| run         | Start program                          |
| break or b  | Set a breakpoint                       |
| next or n   | Step over (line by line)               |
| step or s   | Step into functions                    |
| continue or c | Resume execution until next breakpoint |
| print or p  | Print variable or expression           |
| list or l   | Show source code                       |
| info locals | Show local variables                   |
| backtrace or bt | Show function call stack          |
| watch       | Watch a variable for changes           |
| quit        | Exit GDB                               |

## 🔷 8. Practical Example

### ➤ Code: `buggy.c`

```c
#include <stdio.h>

int main() {
    int a = 5, b = 0;
    int c = a / b;  // divide by zero
    printf("Result: %d\n", c);
    return 0;
}
```

### ➤ Compile and Debug:

```bash
gcc -g buggy.c -o buggy
gdb ./buggy
```

### ➤ Inside GDB:

```bash
(gdb) break main
(gdb) run
(gdb) next
(gdb) print a
(gdb) print b
(gdb) backtrace
```

## 🔷 9. Inspecting and Modifying Data

```bash
(gdb) print var
(gdb) set var = 10
```

## 🔷 10. Breakpoints, Watchpoints, Catchpoints

### 🔹 Breakpoints:

```bash
(gdb) break main
(gdb) break 12
(gdb) delete 1
```

### 🔹 Conditional Breakpoints:

```bash
(gdb) break 20 if x > 100
```

### 🔹 Watchpoints:

```bash
(gdb) watch x
```

## 🔷 11. Backtrace (Call Stack)

```bash
(gdb) backtrace
#0  main at main.c:5
```

Use `frame`, `up`, `down` to navigate.

## 🔷 12. Debugging Segmentation Fault

```bash
gdb ./myprog
(gdb) run
# Crashes with SIGSEGV
(gdb) backtrace
(gdb) list
```

## 🔷 13. Examining Memory

```bash
(gdb) x/4x &var        # View 4 words in hex
(gdb) x/s ptr          # View string at ptr
(gdb) x/20xb ptr       # View 20 bytes at address
```

## 🔷 14. Debugging Core Dumps

Enable core dumps:

```bash
ulimit -c unlimited
```

Run program (will crash and create core file).

Load into GDB:

```bash
gdb ./myprog core
(gdb) backtrace
(gdb) list
```

## 🔷 15. Remote Debugging with gdbserver

### On Target (e.g. ARM board):

```bash
gdbserver :1234 ./myprog
```

### On Host:

```bash
arm-linux-gnueabi-gdb myprog
(gdb) target remote <IP>:1234
(gdb) break main
(gdb) continue
```

## 🔷 16. TUI Mode (Text UI)

```bash
gdb -tui ./myprog
```

Press Ctrl+X + A to switch views.

## 🔷 17. Scripting with GDB

```bash
# script.gdb
break main
run
backtrace
quit
```

Run it:

```bash
gdb -x script.gdb ./myprog
```

## 🔷 18. GDB with Makefiles

```make
CFLAGS += -g
```

## 🔷 19. GDB Shortcuts and Tips

| Shortcut        | Effect                        |
|-----------------|-------------------------------|
| Ctrl+C          | Interrupt program             |
| Ctrl+D          | Exit GDB                      |
| set pagination off | No "press enter" prompts  |
| info break      | List breakpoints              |
| disas           | Show disassembly              |


# GDB (GNU Debugger) Interview Questions and Answers

## 1. What is GDB?
**Answer:** GDB is the GNU Debugger, used for debugging C, C++, and Assembly programs. It helps in examining code behavior during execution, setting breakpoints, inspecting variables, and analyzing crashes.

## 2. How do you compile a program to debug it with GDB?
**Answer:** Use the `-g` flag with gcc or g++ to include debug symbols: `gcc -g file.c -o file`.

## 3. How do you start GDB with a binary?
**Answer:** `gdb ./binary_name`

## 4. How do you run a program in GDB?
**Answer:** Use the `run` command inside GDB.

## 5. What command sets a breakpoint in GDB?
**Answer:** `break` or `b`. Example: `break main`

## 6. How do you list source code in GDB?
**Answer:** Use the `list` or `l` command.

## 7. What's the difference between `next` and `step`?
**Answer:** `next` steps over function calls; `step` steps into functions.

## 8. How do you print a variable in GDB?
**Answer:** Use `print var_name` or `p var_name`.

## 9. What does `backtrace` do?
**Answer:** Shows the call stack (function call trace).

## 10. How do you continue execution after a breakpoint?
**Answer:** Use the `continue` or `c` command.

## 11. How do you watch a variable for changes?
**Answer:** Use `watch var_name`.

## 12. What is a core dump?
**Answer:** A file containing the memory image of a crashed program, used for post-mortem debugging.

## 13. How do you analyze a core dump with GDB?
**Answer:** `gdb ./binary core`

## 14. How do you delete a breakpoint?
**Answer:** Use `delete <breakpoint_number>`.

## 15. How to get a list of breakpoints?
**Answer:** Use `info breakpoints` or `i b`.

## 16. What is `set pagination off`?
**Answer:** Disables GDB's page-by-page output display.

## 17. How to examine memory in GDB?
**Answer:** Use `x` command. Example: `x/4x &var`

## 18. How do you change a variable’s value in GDB?
**Answer:** Use `set var = value`. Example: `set x = 5`

## 19. What is `frame` in GDB?
**Answer:** Displays the current stack frame info.

## 20. How do you step out of a function?
**Answer:** Use `finish` command.

## 21. Can GDB be used to debug multithreaded programs?
**Answer:** Yes, GDB supports thread-aware debugging.

## 22. What does `info threads` show?
**Answer:** Lists all threads currently running.

## 23. How to switch between threads in GDB?
**Answer:** Use `thread <thread_number>`.

## 24. What is TUI mode?
**Answer:** Text User Interface mode; shows source code and registers together. Use `gdb -tui`.

## 25. How to run a GDB script?
**Answer:** `gdb -x script.gdb binary`

## 26. How do you log GDB output?
**Answer:** `set logging on` and `set logging file output.txt`

## 27. What is remote debugging in GDB?
**Answer:** Debugging a program running on another system using `gdbserver`.

## 28. How to start remote debugging?
**Answer:** `target remote <ip>:<port>`

## 29. What is `disas` command?
**Answer:** Disassembles current function.

## 30. Can you debug stripped binaries in GDB?
**Answer:** Only partially; without symbols you can't trace source-level code.

## 31. What is `info registers`?
**Answer:** Displays CPU register values.

## 32. What is `info locals`?
**Answer:** Lists local variables in the current function.

## 33. How to call a function manually in GDB?
**Answer:** Use `call function_name()`.

## 34. What is `layout src`?
**Answer:** Shows source view in TUI mode.

## 35. How do you view assembly instructions?
**Answer:** Use `disassemble` or `layout asm`.

## 36. What is `bt full`?
**Answer:** Shows full backtrace with variable values.

## 37. What is `source` command in GDB?
**Answer:** Executes commands from a file. Equivalent to `-x`.

## 38. How to quit GDB?
**Answer:** Use `quit` or `q`.

## 39. What is the purpose of `core` file?
**Answer:** To debug a program post-crash using GDB.

## 40. How do you enable core dumps?
**Answer:** Use `ulimit -c unlimited`.

## 41. How do you debug a segmentation fault?
**Answer:** Run in GDB, check the `backtrace` when it crashes.

## 42. What’s the difference between `info args` and `info locals`?
**Answer:** `info args` shows function arguments; `info locals` shows local variables.

## 43. How do you set a conditional breakpoint?
**Answer:** `break <line> if <condition>`

## 44. Can you debug optimized code?
**Answer:** It's possible, but variable info may be removed. Prefer `-O0` with `-g`.

## 45. How do you get disassembly for an address?
**Answer:** Use `x/i <address>`.

## 46. How do you restart the program in GDB?
**Answer:** Use `run` again after `kill` or `start`.

## 47. What is `info symbol <address>`?
**Answer:** Shows which symbol is at the given address.

## 48. How do you detach from a process in GDB?
**Answer:** Use `detach` command.

## 49. What is the `start` command?
**Answer:** Starts program and stops at `main`.

## 50. How do you debug a running process?
**Answer:** Use `gdb -p <pid>` to attach.

## 51. How do you suppress pagination permanently?
**Answer:** Add `set pagination off` to `.gdbinit`.

## 52. What is `.gdbinit`?
**Answer:** A file with custom GDB configurations that run on startup.


### ✅ Q1: What happens when you use print in GDB?
It evaluates the variable or expression and prints its value at runtime.

### ✅ Q2: How do you debug a crash using GDB?
- Compile with `-g`
- Run the program in GDB
- When it crashes, use:
  - `backtrace` to find call stack
  - `list` to show code
  - `print` to inspect variables

### ✅ Q3: What's the difference between step and next?
- `step`: Enters into function calls
- `next`: Executes the function call in one step

## ✅ Summary
| Feature               | Description               |
|-----------------------|---------------------------|
| Supports C/C++/ASM    | Yes                       |
| Breakpoint/Watchpoint | Yes                       |
| Core Dump Analysis    | Yes                       |
| Remote Debugging      | Yes                       |
| TUI Mode              | Yes                       |
| Disassembly View      | Yes                       |
| Multithread Debugging | Yes                       |
| Scriptable            | Yes                       |
