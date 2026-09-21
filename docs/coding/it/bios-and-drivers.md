---
title: Drivers and BIOS
---

# Drivers and BIOS

## Device communication and drivers

The CPU is extremely powerful but very specific: it only understands its own language (machine code, binary instructions). Every external device (keyboard, mouse, printer, webcam) is built by a different manufacturer using different technology and speaks its own language.

**That translator is a driver.** A driver is a small program that sits between the CPU and a specific device. It:

- translates the device's signals into instructions the CPU understands,
- tells the CPU what the device is capable of,
- manages the back-and-forth communication between them.

This is why Windows says "installing drivers" when you plug in a new device: it is finding and setting up that translator program. And it is why a device sometimes doesn't work properly: the driver is missing, outdated, or corrupted.

### Where do drivers come from?

- **Built into the operating system**: common devices like basic keyboards and mice have generic drivers already included in Windows, Mac, and Linux.
- **Downloaded from the manufacturer's website**: for specialized devices like graphics cards, printers, or gaming peripherals that need more specific instructions.
- **Found through Windows Update**: modern Windows searches for drivers automatically when new hardware is connected.

## BIOS (Basic Input/Output System)

BIOS is the first program that runs when you power on a computer. It lives on a permanent chip on the motherboard, checks that all hardware is working, and then hands control over to the operating system.

**Why it works that way.** The CPU needs something to tell it what to do the moment electricity arrives. It can't just find Windows on its own. BIOS is that something. It exists completely independently of the operating system, which is why your computer can still run BIOS checks even if Windows is broken or deleted.

### The boot sequence, step by step

1. Power button pressed → the CPU wakes up.
2. The CPU immediately reads BIOS from the ROM chip.
3. BIOS runs POST, which checks all hardware.
4. BIOS finds a bootable drive with an operating system.
5. BIOS hands control to the OS bootloader.
6. Windows or macOS takes over.

### Key components

| Thing | What it is | One-line purpose |
| --- | --- | --- |
| ROM chip | Permanent motherboard chip | Stores BIOS firmware permanently |
| CMOS chip | Settings storage chip | Saves your custom BIOS settings |
| CMOS battery | Small coin cell on the motherboard | Keeps settings alive when unplugged |
| POST | Hardware health check | Verifies everything works before booting |
| Beep codes | Audio error signals | Diagnoses failures when the screen isn't working |
| Boot order | Device startup sequence | Tells BIOS which drive to load the OS from |

### BIOS vs UEFI

| | BIOS | UEFI |
| --- | --- | --- |
| Age | 1980s | Post 2012 |
| Drive size limit | 2TB max | No practical limit |
| Interface | Text only, keyboard | Graphical, mouse support |
| Boot speed | Slower | Much faster |
| Security | Basic | Secure Boot built in |
| Architecture | 16-bit, old | 64-bit, modern |

Both do the same fundamental job; UEFI just does it better. Most people still call it BIOS casually even when it is actually UEFI.

**Analogy:** BIOS is like a building security guard who checks everything before opening the doors for business. It doesn't matter what's happening inside the offices; the guard does the checks first regardless.

### Why IT professionals need to know this

- Reimaging a computer: change the boot order to boot from USB.
- Hardware failures: listen to POST beep codes to identify which component failed.
- Computer won't start: check BIOS first to see whether hardware is even being detected.
- Security: set BIOS passwords and enable Secure Boot.
- Virtual machines: enable the virtualization setting in BIOS.

### Questions I had

- **What runs before BIOS?** Nothing. BIOS is literally the first code the CPU reads. It is hardwired into the ROM chip so it is always there waiting.
- **What happens if the CMOS battery dies?** The computer loses the date and time and resets to default settings every time it powers off. A common sign is the PC showing the wrong date on startup.
- **Why beep codes instead of showing an error?** POST runs before the display is even initialized, and the screen might be the thing that's broken, so audio is the only output available.
- **What if the speaker is broken too?** BIOS has three fallback methods:
    - **POST card**: plugs into a PCIe slot and shows a 2-digit error code on a small LED display. The most reliable, since it reads directly from the motherboard.
    - **Onboard LEDs**: modern motherboards have built-in lights labeled CPU, RAM, GPU, BOOT. Whichever stays lit is the component that failed.
    - **UEFI error log**: logs what failed during boot, readable once the system partially works.

The broader IT lesson: never rely on a single diagnostic method, because the tool you're using to diagnose might itself be the broken thing.

## Practice Questions

??? question "1. What is a driver and why do devices need one?"

    A small program between the CPU and a specific device that translates the device's signals into instructions the CPU understands, tells the CPU what the device can do, and manages communication. The CPU only speaks machine code while each device speaks its own language.

??? question "2. Where do drivers come from?"

    Built into the operating system (generic drivers for common devices), downloaded from the manufacturer for specialized devices, or found automatically through Windows Update.

??? question "3. What is BIOS and why does the CPU need it?"

    The first program that runs at power-on, stored permanently on a ROM chip. The CPU needs something to tell it what to do the moment electricity arrives. BIOS checks hardware and then hands control to the operating system, and it works independently of the OS.

??? question "4. List the boot sequence."

    Power button, CPU wakes, CPU reads BIOS from ROM, BIOS runs POST, BIOS finds a bootable drive, BIOS hands control to the OS bootloader, and the OS takes over.

??? question "5. What do the CMOS chip and CMOS battery do, and what happens if the battery dies?"

    The CMOS chip saves your custom BIOS settings and the battery keeps them alive when unplugged. If it dies, the computer loses the date and time and resets to default settings every time it powers off.

??? question "6. Why does BIOS use beep codes, and what are the fallbacks if the speaker is broken?"

    POST runs before the display is initialized, so audio may be the only output. Fallbacks: a POST card in a PCIe slot showing an error code, onboard LEDs labeled CPU, RAM, GPU, BOOT, and the UEFI error log.

??? question "7. How does UEFI differ from BIOS?"

    UEFI is newer (post 2012), has no practical drive size limit (BIOS max 2TB), has a graphical interface with mouse support, boots much faster, includes Secure Boot, and is 64-bit rather than 16-bit.
