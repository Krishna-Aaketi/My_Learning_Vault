# 📅 Makefile Learning Challenge

## 🔹 Day 1: First Makefile  
**Goal:** Understand target, dependencies, and commands.  

**Makefile (Day 1):**
```make
program: main.o add.o
	gcc main.o add.o -o program

main.o: main.c add.h
	gcc -c main.c

add.o: add.c add.h
	gcc -c add.c
```

**Run:**
```bash
make
./program
```

---

## 🔹 Day 2: Add Variables  
**Goal:** Avoid repeating compiler commands by using variables.  

**Makefile (Day 2):**
```make
CC = gcc
CFLAGS = -Wall

program: main.o add.o
	$(CC) $(CFLAGS) main.o add.o -o program

main.o: main.c add.h
	$(CC) $(CFLAGS) -c main.c

add.o: add.c add.h
	$(CC) $(CFLAGS) -c add.c
```

**Run:**
```bash
make
```

---

## 🔹 Day 3: Add Debug Flags  
**Goal:** Enable debugging and better warnings with `-g` and `-Wall`.  

**Makefile (Day 3):**
```make
CC = gcc
CFLAGS = -Wall -g

program: main.o add.o
	$(CC) $(CFLAGS) main.o add.o -o program

main.o: main.c add.h
	$(CC) $(CFLAGS) -c main.c

add.o: add.c add.h
	$(CC) $(CFLAGS) -c add.c
```

**Run:**
```bash
make
gdb ./program   # Now you can debug
```

---

## 🔹 Day 4: Add `clean` (Phony Target)  
**Goal:** Learn `.PHONY` targets (not files, but actions).  

**Makefile (Day 4):**
```make
CC = gcc
CFLAGS = -Wall -g

program: main.o add.o
	$(CC) $(CFLAGS) main.o add.o -o program

main.o: main.c add.h
	$(CC) $(CFLAGS) -c main.c

add.o: add.c add.h
	$(CC) $(CFLAGS) -c add.c

.PHONY: clean
clean:
	rm -f *.o program
```

**Run:**
```bash
make
./program
make clean
ls   # Only source files remain
```

---

### By **Day 4**, you now know:  
- Targets, dependencies, and commands  
- Variables (`CC`, `CFLAGS`)  
- Debugging flags  
- Phony targets (`clean`)  

