---
title: Pointers
---

# Pointers

## Pointer arithmetic

Subtracting an **integer** from a pointer (`p - i`) moves the pointer backward by `i` elements in memory.

Subtracting a **pointer** from another pointer (`p - r`) returns the number of elements (not bytes) between the two pointers.

- The result of subtracting two pointers is of type `ptrdiff_t`.
- `ptrdiff_t` is a signed integer type defined in `<cstddef>`. It represents the difference between two pointers in number of elements.

```cpp
// Pointer Subtraction
// pointerSubtraction.cpp

#include <iostream>
#include <cstddef>

int main()
{
    int a[] = {1,2,3,4,5}, i = 2, *p, *r;
    ptrdiff_t k;

    p = &a[4];
    r = &a[0];
    k = p - r; // difference between addresses
    std::cout << *(p - i) << std::endl; // value at address i types before *p
    std::cout << k << std::endl;
}
```

```text
3
4
```

## Terminology related to pointers

**Dangling pointer**: a pointer that does not point to a valid object, and consequently may make a program crash or behave oddly.

```cpp
char *p2;       /* dangling (uninitialized) pointer */

// Here, p2 may point to anywhere in memory and dereferencing can cause issues,
// possibly a segmentation fault
```

## Practice Questions

??? question "1. What does p - i do when p is a pointer and i is an integer?"

    It moves the pointer backward by `i` **elements** (not bytes) in memory.

??? question "2. What does p - r return when both are pointers, and what is its type?"

    The number of elements between the two pointers, of type `ptrdiff_t`, a signed integer type from `<cstddef>`.

??? question "3. In the example, why does the program print 3 and then 4?"

    `p` points to `a[4]` and `r` to `a[0]`. `*(p - 2)` is `a[2]`, which is 3. `p - r` is 4 elements.

??? question "4. What is a dangling pointer, and what can go wrong?"

    A pointer that does not point to a valid object, such as an uninitialized `char *p2;`. It may point anywhere in memory, so dereferencing it can crash the program or cause a segmentation fault.
