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

# Understanding Makefile Basics
---
## 🔹 1. What is a Target?
- A **target** is usually the name of a file to be created (like an executable or `.o` file).  
- It can also be a **label for an action** (like `clean`).  

**Examples:**
```make
program: main.o add.o   # "program" is the target
main.o: main.c add.h    # "main.o" is the target
clean:                  # "clean" is a phony target (not a file)
```

**Target = What do you want to build?**

---

## 🔹 2. What are Dependencies?
- Dependencies are the files that the target depends on.  
- If any dependency changes, `make` will rebuild the target.  

### Example:
```make
main.o: main.c add.h
```
**Target = `main.o`**  
**Dependencies = `main.c` and `add.h`**

- If either `main.c` or `add.h` changes → `main.o` must be rebuilt.  

---

## 🔹 3. Commands (Recipes)

After target and dependencies, you write the command(s) (indented with **TAB**).  

###  Example:
```make
main.o: main.c add.h
	gcc -c main.c
```
- If `main.c` or `add.h` changes → run `gcc -c main.c` to rebuild `main.o`.  

---

## 🔹 4. Putting It Together

```make
program: main.o add.o
	gcc main.o add.o -o program
```
- Target = program

- Dependencies = main.o and add.o

- Command = gcc main.o add.o -o program

### So:

- If main.o or add.o is newer (modified) → rebuild program.

- If program already exists and is up to date → make does nothing.
