# 🔌 Booting Process in Computer Systems

---

## 🔹 Definition
The **booting process** is the sequence of operations that a computer system performs after power is turned on,  
to initialize hardware and load the **Operating System (OS)** into RAM for execution.

---

## 🔹 Types of Booting
- **Cold Boot** – Starting the computer after it was completely powered off.  
- **Warm Boot** – Restarting the system without turning off the power (e.g., pressing **Ctrl+Alt+Del**).

---

## 🔹 Steps in Booting Process (General System)

### 1. Power On
- When you press the power button, the system receives electrical power.  
- Hardware components (**CPU, RAM, I/O devices**) get initialized.  

### 2. POST (Power-On Self-Test)
- **BIOS/UEFI** checks if essential hardware is working (RAM, CPU, keyboard, storage, etc.).  
- If an error is found, it shows a **beep code** or error message.  

### 3. Load BIOS/UEFI Firmware
- **BIOS/UEFI firmware** is stored in ROM/flash memory on the motherboard.  
- Provides low-level instructions to initialize hardware and locate a bootable device.  

### 4. Select Boot Device
- BIOS/UEFI checks the **boot order** (HDD, SSD, USB, network, etc.).  
- It finds the device with a **bootloader**.  

### 5. Load Bootloader
- The bootloader (**GRUB, LILO, Windows Boot Manager**) is loaded from the **boot sector (MBR/GPT)**.  
- Its job: **load the kernel** of the operating system.  

### 6. Kernel Loading
- The bootloader loads the **OS kernel** into RAM.  
- Kernel initializes:  
  - Memory management  
  - Process scheduling  
  - Drivers  
  - Core services  

### 7. Init/Systemd Execution
- After the kernel is ready, it starts the **first user-space process**:  
  - `init` or `systemd` in **Linux**  
  - `smss.exe` in **Windows**  
- These processes start system services and daemons.  

### 8. User Login
- A **login prompt** or **GUI** appears.  
- The user can now interact with the system.  

---

