---
title: Primitive Data Types
---

# Primitive Data Types

There are two categories of fundamental types.

## Integral types

Integral types store **whole numbers** (no fractional part).

1. `bool` → 1 byte (`true` or `false`)
2. `char` → 1 byte (`'a'`, `'b'`, and so on)
3. `int` → 4 bytes (1, 2, ...)
    - `short` → 2 bytes
    - `long` → 4 bytes
    - `long long` → 8 bytes

Integers can be **signed** (positive and negative) or **unsigned** (positive only).

### Unsigned integers

They represent only positive numbers. The range of an unsigned integer is `0` to `2^bits - 1`, where `bits` is the number of bits. For example, an 8-bit unsigned integer ranges from 0 to 2⁸ - 1 = 255.

### Signed integers

They represent both positive and negative numbers. Computers store negative numbers using a method called **two's complement**.

??? note "Two's complement representation"

    In two's complement, the highest bit (the **most significant bit**, or MSB) represents the **sign**:

    - If the highest bit is **0**, the number is positive.
    - If the highest bit is **1**, the number is negative.

    For example, in 8 bits:

    - `1` is `00000001` (first bit 0, so positive)
    - `-1` is `11111111` (first bit 1, so negative)

??? note "How to get the binary of a negative number from the positive one"

    1. **Flip all the bits** (0 becomes 1, 1 becomes 0).
    2. **Add 1** to the result.

## Floating point types

Reference: [learncpp: floating point numbers](https://www.learncpp.com/cpp-tutorial/floating-point-numbers/)

Floating point types store **real numbers** (numbers with a fractional part).

1. `float` → 4 bytes (1.2, 1.9, ...), precision around 6 to 7 decimal digits.
2. `double` → 8 bytes (1.3, 1.4, ...), precision around 15 to 16 decimal digits.

Want to know how floating point numbers are stored in binary? See [Exposing Floating Point](https://ciechanow.ski/exposing-floating-point/).

### Floating point precision

**Outputting floating point values.** When outputting floating point numbers, `std::cout` has a default precision of 6.

```cpp
#include <iostream>

int main()
{
    std::cout << 9.87654321f << '\n';
    std::cout << 987.654321f << '\n';
    std::cout << 987654.321f << '\n';
    std::cout << 9876543.21f << '\n';
    std::cout << 0.0000987654321f << '\n';

    return 0;
}
```

Output:

```text
9.87654
987.654
987654
9.87654e+006
9.87654e-005
```

We can override the default precision with an **output manipulator** named `std::setprecision()`. Output manipulators change how data is output and are defined in the `<iomanip>` header.

```cpp
#include <iomanip> // for output manipulator std::setprecision()
#include <iostream>

int main()
{
    std::cout << std::setprecision(17); // show 17 digits of precision
    std::cout << 3.33333333333333333333333333333333333333f <<'\n'; // f suffix means float
    std::cout << 3.33333333333333333333333333333333333333 << '\n'; // no suffix means double

    return 0;
}
```

Output:

```text
3.3333332538604736
3.3333333333333335
```

We asked for 17 digits, but the numbers are clearly not precise to 17 digits. Floats are less precise than doubles, so the float has more error.

!!! tip
    Output manipulators (and input manipulators) are sticky: once set, they stay set. The one exception is `std::setw`.

**Rounding errors** occur when a number can't be stored precisely. This happens even with simple numbers like 0.1. Rounding errors are not the exception, they are the norm. Never assume your floating point numbers are exact.

A corollary: be wary of using floating point numbers for financial or currency data.

## Practice Questions

??? question "1. What is the range of an 8-bit unsigned integer, and where does that come from?"

    0 to 255. The range of an unsigned integer is `0` to `2^bits - 1`, so 2⁸ - 1 = 255.

??? question "2. How does a computer store a negative integer, and how do you get -1 from 1 in 8 bits?"

    With **two's complement**. Flip all the bits of the positive number, then add 1. For 1 (`00000001`): flip to `11111110`, add 1 to get `11111111`, which is -1. The highest bit (MSB) is the sign: 0 means positive, 1 means negative.

??? question "3. What is the difference between float and double?"

    A `float` is 4 bytes with about 6 to 7 decimal digits of precision. A `double` is 8 bytes with about 15 to 16 digits. Doubles are more precise, so they accumulate less rounding error.

??? question "4. Why can printing 3.33333333333333333333f with setprecision(17) show digits that are wrong?"

    Floating point numbers can't store most decimals exactly, so beyond the type's precision the extra printed digits are just the stored approximation, not the value you wrote. The float shows more error than the double.

??? question "5. Why should you be wary of floating point for money?"

    Rounding errors happen all the time, even for simple values like 0.1. Financial and currency data needs exact results, so floating point can quietly produce wrong totals.

??? question "6. What does it mean that output manipulators are sticky?"

    Once you set one (like `std::setprecision(17)`), it stays in effect for later output until you change it. `std::setw` is the exception.
