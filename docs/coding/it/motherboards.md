---
title: Motherboards
---

# Motherboards

A motherboard does two fundamental jobs:

- It distributes power from the power supply to every component.
- It acts as the communication highway between all parts.

## The chipset: Northbridge and Southbridge

The chipset is essentially a traffic control system: it decides how data flows between components. It was traditionally split into two chips.

**Northbridge** handled the fast, high-priority connections:

- CPU ↔ RAM
- CPU ↔ Graphics card

These needed to be fast because they constantly exchange huge amounts of data. The Northbridge sat very close to the CPU for speed.

**Southbridge** handled the slower, everyday connections (I/O):

- USB ports
- Audio
- Storage drives (hard drives, SSDs)
- PCI slots (Peripheral Component Interconnect)

## Expansion slots and PCIe

Motherboards have slots where you can plug in extra cards to add or upgrade functionality. Common examples:

- Graphics cards (for gaming or video editing)
- Sound cards
- Network cards
- NVMe SSD cards

**PCIe (PCI Express)** is the current standard for these slots. It uses **lanes**, like lanes on a highway: more lanes means more data can flow simultaneously. PCIe slots come in different sizes:

- **x1**: 1 lane, smallest slot, for simple cards like sound cards
- **x4**: 4 lanes, for some SSDs
- **x8**: 8 lanes
- **x16**: 16 lanes, largest slot, where the graphics card goes

## Form factor

Form factor is the physical size and shape of the motherboard. It matters because it:

- determines what case the motherboard fits in,
- determines how many slots and ports you get,
- affects airflow and cooling inside the case.

The main form factors:

- **ATX**: the full-size standard. Most desktop PCs use this. Offers the most expansion slots, RAM slots, and ports. Best for gaming PCs or workstations where you want maximum upgradeability.
- **Micro-ATX**: smaller than ATX, fewer expansion slots, but still fits most mid-size cases. A good balance of size and expandability.
- **Mini-ITX**: very small, designed for compact builds. Usually only 1 PCIe slot and 2 RAM slots. Great for small form factor PCs but limits future upgrades.

## Practice Questions

??? question "1. What are the two fundamental jobs of a motherboard?"

    Distributing power from the power supply to every component, and acting as the communication highway between all parts.

??? question "2. What did the Northbridge and Southbridge each handle?"

    The Northbridge handled fast, high-priority connections (CPU to RAM, CPU to graphics card) and sat close to the CPU. The Southbridge handled slower I/O: USB, audio, storage drives, and PCI slots.

??? question "3. What is a PCIe lane, and where does the graphics card go?"

    A lane is like a highway lane: more lanes let more data flow at once. Slots come as x1, x4, x8, and x16. The graphics card goes in the x16 slot.

??? question "4. What is form factor, and how do ATX, Micro-ATX, and Mini-ITX differ?"

    The physical size and shape of the motherboard, which sets what case it fits and how many slots and ports it has. ATX is full-size with the most expansion, Micro-ATX is smaller with fewer slots, and Mini-ITX is very small with usually 1 PCIe slot and 2 RAM slots.
