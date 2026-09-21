---
title: Storage
---

# Physical Storage: Hard Drives

## Data size units

**Byte** = 8 bits grouped together. Early computer engineers found that 8 bits was the most practical grouping for representing a single character (a letter, number, or symbol). For example, the letter "A" is stored as `01000001`: 8 bits, 1 byte.

Units scale up from there:

- **Kilobyte (KB)** = 1,024 bytes: a short text email
- **Megabyte (MB)** = 1,024 KB: a photo, or a short song
- **Gigabyte (GB)** = 1,024 MB: a movie, or several hundred photos
- **Terabyte (TB)** = 1,024 GB: a large hard drive's worth of files

**Why 1,024 and not 1,000?** Computers work in binary (powers of 2), and 1,024 is 2¹⁰, the closest power of 2 to 1,000.

## Hard disk drives (HDDs)

HDDs are the older, traditional type of storage. Inside the drive:

- **Platters**: circular metal disks coated with a magnetic material, stacked and spinning at high speed. Data is stored by magnetizing tiny spots on the surface: one magnetic direction is 1, the opposite is 0.
- **Read/write arm**: a mechanical arm with a tiny head at the tip that hovers nanometers above the spinning platter. It moves back and forth to read or write data at specific locations.
- **RPM (revolutions per minute)** measures how fast the platters spin:
    - 5,400 RPM: slower, found in budget drives and laptops (quieter, less power)
    - 7,200 RPM: standard desktop speed
    - 10,000 to 15,000 RPM: high-performance drives

Faster RPM means the data you need spins around to the read head faster, reducing wait time.

**The problem with HDDs** is their mechanical parts: if you drop a running HDD, the read arm can scratch the platter and destroy data. They are also slower because the drive physically has to spin and move the arm into position before it can read anything. That delay is called **seek time**.

## Solid state drives (SSDs)

SSDs store data completely differently, using **flash memory chips** (the same technology as USB drives, just faster and higher capacity). There are no moving parts.

Data is stored by trapping electrical charges inside microscopic transistors called **floating gate transistors**. Charge present is 1, no charge is 0.

??? note "What if somebody takes the electrical charge from an SSD, or why doesn't it leak?"

    **SSDs are designed to hold charge without power.** This is the key difference between SSDs and RAM. RAM is volatile and loses everything when power is off. SSDs use **NAND flash**, which is non-volatile: it is engineered to trap and hold electrical charges even with no power connected. The floating gate transistors act like a sealed container: once the charge is trapped, it stays without power to maintain it.

    **But charge does leak slowly.** The trapped charges in an SSD slowly leak away over time. This is called **data retention**.

    - A powered and regularly used SSD: many years
    - An SSD sitting unplugged in a drawer: typically 1 to 2 years before data starts degrading
    - In hot environments: even faster, because heat accelerates charge leakage

    This is why SSDs are actually **worse than HDDs for long-term unpowered storage**. An HDD stores data as magnetic patterns on metal that can last decades without power.

    **What happens when charge leaks.** When enough charge leaks from a cell that was storing a 1, the drive can no longer tell whether it was a 1 or a 0. That bit becomes unreadable or misread, and the file gets **corrupted**. Cells fail gradually, so you might notice small files becoming corrupted first, occasional read errors, and in severe cases the drive becoming unrecognizable.

    **How SSDs protect against this:**

    - **Error Correcting Code (ECC)**: the drive constantly checks its own data mathematically. If a few bits have drifted, ECC can detect and correct the error automatically.
    - **Wear leveling**: the drive spreads data evenly across all cells so no single area gets overused and degrades faster.
    - **Regular refresh**: when the SSD is connected and powered, the controller periodically reads cells and rewrites the charge back to full strength.

**Advantages over HDDs:**

- Much faster: no physical movement, data is accessed electronically in microseconds.
- More durable: dropping an SSD won't damage it since nothing is spinning.
- Silent: no mechanical noise.
- Lighter and smaller.

**The tradeoff** is cost: SSDs are significantly more expensive per gigabyte. A 4TB HDD might cost the same as a 1TB SSD.

**Hybrid drives (SSHDs)** tried to bridge the gap: a small amount of SSD flash acts as a cache for frequently used files, while the bulk of storage stays on cheaper spinning platters. They were a transitional solution and are now mostly obsolete as SSD prices have dropped.

## Storage interfaces

An interface is the connection standard: the language and physical connector the drive uses to talk to the motherboard.

### ATA and SATA

ATA (Advanced Technology Attachment) was the original standard for connecting hard drives. The modern version is **SATA (Serial ATA)**, which replaced the older parallel ATA standard. SATA uses a thin cable and is the most common interface for HDDs and standard SSDs today.

- **Hot swapping**: you can plug and unplug a SATA drive while the computer is running. Useful for external drive bays or servers.
- Straightforward, widely compatible, works with virtually every motherboard.
- Max speed around 600 MB/s: fast enough for HDDs and entry-level SSDs, but a bottleneck for high-end SSDs.

### NVMe (Non-Volatile Memory Express)

As SSDs got faster, SATA became the limiting factor, like pouring water through a straw when the drive could push it through a pipe. NVMe was designed specifically for fast SSDs. Instead of a SATA cable, NVMe drives plug directly into a PCIe expansion slot, either as a card or more commonly as an **M.2 stick** (a small rectangular drive that plugs directly onto the motherboard, no cable needed).

**Why NVMe is so much faster:**

- SATA max speed: about 600 MB/s
- NVMe max speed: 3,500 to 7,000+ MB/s

NVMe uses PCIe lanes directly, a much wider, faster highway than the SATA connection. It also uses a communication protocol designed from scratch for flash storage rather than recycling old protocols designed for slow spinning drives.

**When does it matter?** For everyday tasks like browsing and word processing you likely won't notice. For video editing, large file transfers, loading large games, or booting the operating system, NVMe is noticeably faster.

## Practice Questions

??? question "1. Why is a byte 8 bits, and why do storage units scale by 1,024?"

    8 bits was the most practical grouping for representing a single character (for example "A" is `01000001`). Computers work in powers of 2, and 1,024 is 2¹⁰, the closest power of 2 to 1,000.

??? question "2. How does an HDD store data, and what are its weaknesses?"

    As magnetized spots on spinning platters, read by a mechanical arm. Weaknesses: it is fragile (a drop can scratch the platter) and slower because of seek time, the physical spinning and arm movement needed before reading.

??? question "3. How does an SSD store data?"

    In flash memory chips, by trapping electrical charge in floating gate transistors (charge is 1, no charge is 0). It has no moving parts.

??? question "4. Why are SSDs worse than HDDs for long-term unpowered storage?"

    The trapped charge slowly leaks (data retention), typically after 1 to 2 years unplugged, faster in heat. HDD magnetic patterns can last decades.

??? question "5. How do SSDs protect data from charge leakage?"

    Error Correcting Code (ECC) to detect and fix drifted bits, wear leveling to spread use evenly, and regular refresh of charges while powered.

??? question "6. What is the difference between SATA and NVMe?"

    SATA connects through a cable and tops out around 600 MB/s, and supports hot swapping. NVMe plugs directly into PCIe (often as an M.2 stick), reaches 3,500 to 7,000+ MB/s, and uses a protocol designed for flash storage.
