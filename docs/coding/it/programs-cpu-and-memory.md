---
title: Programs, the CPU, and the Memory
---

# Programs, the CPU, and the Memory

- Programs are sets of instructions stored on hard drives.
- The **CPU** processes these instructions, but to access them quickly we load them into **RAM** (short-term memory).
- Data travels inside the computer via the **external data bus (EDB)**, a set of wires carrying binary signals.
- Inside the CPU there are **registers** that temporarily hold data for processing tasks like addition.
- The **memory controller chip (MCC)** bridges the CPU and RAM, fetching specific instructions as requested.
- The **address bus** connects the CPU with the MCC and sends the address of the data. The MCC then looks up that address in RAM.

## Cache

Cache is a smaller, faster memory than RAM that stores frequently used data to speed up processing.

### How it works

1. The CPU needs data, so it checks **L1** (smallest and fastest) first.
2. Not there? It checks **L2**.
3. Not there? It checks **L3**, which is slower (but 2x faster than RAM).
4. Still not there? It goes all the way to **RAM** (slow).

The goal is to always find data as early as possible, ideally in L1, so the CPU never has to wait.

### Who owns what

- **L1 and L2**: each CPU core has its own private cache.
- **L3**: shared across all cores in the CPU.

## CPU clock and performance

- **The clock is a rhythm.** Every tick tells the CPU to do its next tiny action, billions of times per second.
- **GHz is the speed of that rhythm.** 3 GHz means 3 billion ticks per second.
- **Tasks are pre-sliced.** No task is ever too big for one tick. Everything is broken down into guaranteed-to-finish micro-steps before the clock starts.
- **Slow tasks use pipelining.** The CPU overlaps multiple tasks like an assembly line so no tick is wasted.
- **Overclocking is a faster rhythm.** More work per second, but more heat as a side effect.

!!! tip "Clock speed isn't everything"
    Two CPUs at the same GHz can perform very differently because of **IPC** (Instructions Per Cycle).

    **Performance = Clock Speed × IPC × Number of Cores**

    A CPU that does 2 instructions per cycle at 3 GHz beats one that does 1 instruction per cycle at 4 GHz. This is why a modern Apple M-series chip at 3.5 GHz can outperform older Intel chips at 4.5 GHz.

## Practice Questions

??? question "1. Why are programs loaded into RAM before the CPU runs them?"

    Storage is slow. RAM is short-term memory that the CPU can access quickly.

??? question "2. What do the address bus and the memory controller chip do together?"

    The address bus carries the address of the data from the CPU to the memory controller chip (MCC), and the MCC looks up that address in RAM and fetches the data.

??? question "3. In what order does the CPU check its caches, and which are private to a core?"

    L1, then L2, then L3, then RAM. L1 and L2 are private to each core, and L3 is shared across all cores.

??? question "4. Why can a 3 GHz CPU beat a 4 GHz CPU?"

    Performance is clock speed × instructions per cycle (IPC) × cores. A CPU doing 2 instructions per cycle at 3 GHz beats one doing 1 instruction per cycle at 4 GHz.

??? question "5. What does overclocking do, and what is its side effect?"

    It makes the clock rhythm faster, so more work is done per second, but it produces more heat.
