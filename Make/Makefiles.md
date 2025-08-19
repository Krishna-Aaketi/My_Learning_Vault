# Make and Makefiles

## 🔹 What is `make`?

`make` is a **build automation tool** in Linux/Unix.

It reads instructions from a file (called a **Makefile**) and decides:

-  What needs to be built  
-  Which commands to run  
-  When to rebuild files (only if sources changed)  

**In short**:  
- `make` saves you from typing long `gcc ...` commands every time.  
- It also saves time by recompiling **only what changed**, not everything.  

---

## 🔹 What is a Makefile?

A **Makefile** is just a text file with build rules.  
It tells `make` how to **compile and link** your program.  

### Structure of a Rule in Makefile:
```c
target: dependencies
<TAB>command
```
- **target** → the file to be created (like `program`, `main.o`, or even `clean`).  
- **dependencies** → files that must exist/are required to build the target.  
- **command** → shell command to build the target (**must start with a TAB**).  
---

## 🔹 Example

Suppose you have `main.c`:

### Without Make:
```c
gcc main.c -o hello
./hello
```
### With Makefile (Makefile content):
```c
hello: main.c
	gcc main.c -o hello
```
### Now just run:
```c
make
./hello
```
- `make` sees `hello` depends on `main.c`.  
- If `main.c` changes → recompile.  
- If not → do nothing.  

---

## 🔹 Why Use Make & Makefiles?

-  **Automation** → no need to type long compile commands.  
-  **Efficiency** → rebuilds only changed files.  
-  **Scalability** → handles projects with 100s of files.  
-  **Flexibility** → can define extra tasks (`clean`, `install`, `test`, etc.).  
