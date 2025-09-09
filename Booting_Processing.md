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

# ⚙️ Booting Process in an SoC (Qualcomm / ARM / Jetson Example)

---

## 🔹 1. Power-On Reset (PoR)
- When you press power or apply supply, the SoC’s internal circuits **reset**.  
- All **registers, CPU, and peripherals** go to a known default state.  
- Ensures the chip starts clean (**no leftover data from before**).  

---

## 🔹 2. Boot ROM
- Every SoC (Qualcomm, ARM, Nvidia Jetson, etc.) has a **tiny mask-programmed ROM code** built inside the chip.  

**Purpose:**
- Runs immediately after reset.  
- Initializes very basic hardware (**CPU core, internal SRAM**).  
- Looks for a **bootable image** in predefined sources:  
  - eMMC, SD card, NAND, SPI flash, USB, UART  
- Loads the **Primary Bootloader** into RAM and jumps to it.  

👉 Think of Boot ROM as the **“first helper”** that finds the bootloader.  

---

## 🔹 3. Primary Bootloader (PBL / SBL1)
- First software loaded from external storage.  

**Responsibilities:**
- Initialize **system clock** and basic **power configuration**.  
- Set up **DDR (external RAM)** for larger programs.  
- Do minimal **security checks** (digital signatures in secure boot).  
- Loads the **Secondary Bootloader**.  

---

## 🔹 4. Secondary Bootloader (SBL2 / XBL / U-Boot / LK)
- A bigger and more **feature-rich bootloader**.  

**Responsibilities:**
- Initialize peripherals (**UART, I2C, SPI, USB, display**).  
- Set up storage drivers (**eMMC, SD, flash**).  
- Perform **secure boot checks** if enabled.  
- Provide a **shell/console** (e.g., U-Boot lets you type commands).  
- Load the **OS kernel** into DDR and pass arguments (like **device tree** in Linux).  

---

## 🔹 5. OS Kernel
- The **Linux / Android / RTOS kernel** is copied into RAM and executed.  

**Responsibilities:**
- Initialize **process scheduling**, **memory management**, and **device drivers**.  
- Mount the **root filesystem (rootfs)**.  
- Prepare environment for **user applications**.  

---

## 🔹 6. Init / Services
- The kernel starts the **init process** (PID 1 in Linux/Android).  

**Init (or systemd) Responsibilities:**
- Start background **services (daemons)**.  
- Mount additional filesystems.  
- Launch user applications (**Android → Zygote → system apps**).  

✅ At this stage, the system is **ready for use**.  

---

## 📌 Example: Android Boot Sequence on Qualcomm SoC
1. **PoR**  
2. **Boot ROM** → finds storage  
3. **PBL (SBL1)** → init clocks, DDR  
4. **SBL2 / XBL** → load TrustZone + U-Boot / ABL  
5. **Kernel (Linux)** → init drivers, mount rootfs  
6. **Init → Zygote → Android services → Launcher**  

---
