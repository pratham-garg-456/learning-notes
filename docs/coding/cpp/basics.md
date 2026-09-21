---
title: Basics
---

# Basics

## What is a program, and why are we called programmers?

We use software like Chrome or YouTube on our phones and laptops every day. All of that software is made of one or more **programs**. A program is a set of instructions that does some well-defined task.

!!! tip "Let's simplify it"
    Imagine you're making a robot that can prepare a sandwich. You need to give it clear, step-by-step instructions. With a computer we are not asking it to make a sandwich, but to do something else, like adding two numbers together.

Programmers write these **instructions** in a programming language like C or C++.

## How does an application run on your computer?

When you open an app, the computer puts the app's instructions in RAM and lets the app take control. The app runs, gets information from you, shows you results, and finally stops running and gives control back to the computer.

## Information

The instructions and data we give the computer are stored in RAM as binary: 0s and 1s. Each 0 or 1 is a **bit**.

**Bits.** The most fundamental unit of a modern computer is the binary digit, or bit. A bit is either on or off: 1 is on, 0 is off.

**Bytes.** The fundamental addressable unit of RAM is the byte. One byte is 8 bits.

Each bit position has a value, and the byte's value is the sum of the positions that are on:

| Bit pattern (2⁷ … 2⁰) | How it adds up | Decimal |
| --- | --- | --- |
| `0 0 0 0 0 0 0 0` | | 0 |
| `0 0 0 0 0 0 0 1` | 2⁰ | 1 |
| `0 0 0 0 0 0 1 0` | 2¹ | 2 |
| `0 0 0 0 0 0 1 1` | 2¹ + 2⁰ | 3 |
| `0 0 0 0 0 1 0 0` | 2² | 4 |
| `0 0 1 1 1 0 0 0` | 2⁵ + 2⁴ + 2³ | 56 |
| `1 1 1 1 1 1 1 1` | 2⁷ + 2⁶ + 2⁵ + 2⁴ + 2³ + 2² + 2¹ + 2⁰ | 255 |

So to store 12, the computer stores `0 0 0 0 1 1 0 0`.

Everything we write gets converted into 0s and 1s.

> For example: 65 is stored as `01000001`. The letter `A` is also stored as `01000001`.

_Wait: if everything is turned into 0s and 1s, how does the computer know whether a pattern is an integer or a letter?_ Typed programming languages use a **type system** to interpret the bit streams in memory. C is a typed language.

!!! note "Definition"
    A type is a rule that defines how to store values in memory and which operations are admissible on those values.

## Addresses

Each byte of RAM has a unique address. Addressing starts at zero, is sequential, and ends at the size of RAM minus 1.

!!! tip
    Each byte, not each bit, has its own address. That is why we say RAM is **byte addressable**.

## Segmentation faults

The information in RAM serves different purposes. We are expected to read and write data, but not to execute it. Similarly, we are expected to execute program instructions, but not to write them. So some architectures give data read and write permissions, and instructions read and execute permissions.

This permission system helps trap errors while a program runs. An attempt to execute data or overwrite an instruction reports an error, because the access went to the wrong segment. We call such an error a **segmentation fault**. You will meet it while coding.

## Compilers

The computer only understands bits and bytes. Human-readable text can be converted to them: `1` becomes `00000001`, and `A` (65 in decimal) becomes `01000001`.

Whatever instructions and data we write in a programming language must be converted to computer language. The **compiler** does that for us.

![Compiler flow: source code to executable](https://cdn.hashnode.com/res/hashnode/image/upload/v1691898898280/7c196a64-0eda-4573-9701-fc43b680fc5f.png?auto=compress,format&format=webp)

!!! tip
    Programming languages demand more completeness and precision than human languages.

## Our first C program

A program that displays the phrase "This is C", in a source file named `hello.c`. Source files written in C end with `.c`.

```c
/* My first program           // comments introducing the source file
    hello.c
*/

#include <stdio.h>           // information about the printf identifier
int main(void)               // the starting point of the program
 {
    printf("This is C");     // send output to the screen

    return 0;                // return control to the operating system
 }
```

### Compiling on Linux

The C compiler that ships with Linux is called `gcc`. To create a binary version of the source code:

```bash
gcc hello.c
```

```text
hello.c (source code) --> gcc (compiler) --> a.out (executable file)
```

By default, `gcc` produces an output file named `a.out`. It contains all the machine language instructions needed to run the program. To run it:

```bash
./a.out
```

The output:

```text
This is C
```

### Documentation

We put **comments** in source code to document it and make it readable. C supports two styles, multi-line and inline. C compilers ignore all comments.

```c
/* My first program
   hello.c  */
```

```c
int main(void)               // the starting point of the program
```

### Program startup

Every C program includes a clause like `int main(void)`. Execution starts at this line, which we call the program's **entry point**.

```c
int main(void)           // program startup
{
    return 0;            // return to operating system
}
```

When the executable is loaded into RAM (`a.out` or `hello.exe`), the operating system transfers control to this entry point. The last statement (`return 0;`) before the closing brace transfers control back to the operating system.

### Program output

The following statement outputs "This is C" to the standard output device (the screen).

```c
printf("This is C");
```

The line before `int main(void)` tells the compiler that `printf` is a valid identifier.

```c
#include <stdio.h>           // information about the printf identifier
```

### Case sensitivity

C is case-sensitive. If we change `printf()` to `PRINTF()`, the compiler reports a syntax error.

## Extra reading: binary

- Binary is a system that uses bits (binary digits) to represent values.
- Each bit has one of two values, written 0 and 1. These correspond to:
    - Electrically: typically off/on, low/high voltage, or low/high current.
    - Logically: false or true.
- Binary numbers are resistant to errors, especially compared to analog voltages.
    - To represent 0 to 10 as an analog value, we could use 0 to 10 volts. But over a long cable there is signal loss: we could apply 10 volts at one end and observe only 9.1 volts at the other. Electromagnetic interference could also nudge the signal slightly.
    - If we use the same voltages and cable for a binary signal, where 0 volts is off ("0") and 10 volts is on ("1"), a signal degraded from 10 to 9.1 volts still counts as "1", and a 0 volt signal with stray interference of about 0.4 volts still counts as "0". Larger numbers need multiple bits, carried either in parallel (several wires side by side) or in sequence over one wire.

## Practice Questions

??? question "1. Why do we say RAM is byte addressable, and how many bits is that?"

    Every **byte** has its own unique address, not every bit. One byte is 8 bits. Addresses start at zero and run sequentially up to the size of RAM minus 1.

??? question "2. The bit pattern 01000001 could be the integer 65 or the letter A. How does the computer know which?"

    The **type system**. A type is a rule that defines how values are stored in memory and which operations are allowed on them. The same bits are interpreted according to the declared type of the variable.

??? question "3. How is the number 12 stored in one byte?"

    As `00001100`: the 2³ bit (8) and the 2² bit (4) are on, and 8 + 4 = 12.

??? question "4. What is a segmentation fault?"

    An error raised when a program accesses memory in the wrong way for its segment, such as trying to execute data or overwrite an instruction. Architectures give data read and write permissions and instructions read and execute permissions, so the violation is trapped.

??? question "5. What does a compiler do, and what is the default output file name from gcc?"

    It converts the source code we write into machine language the computer can run. `gcc hello.c` produces an executable named `a.out` by default, which you run with `./a.out`.

??? question "6. Why do computers use binary instead of, say, analog voltage levels?"

    Binary is resistant to errors. With only two states (low and high), a signal that degrades in transit or picks up noise is still read correctly. With analog levels, the same degradation changes the meaning of the value.
