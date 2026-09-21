---
title: STL Good Practice
---

# STL Good Practice

## Good Practice

if you know the size of elements pre-allocate memory using `reserve()`

```cpp
// Bad Way
// Like packing a tiny suitcase, then buying bigger ones as you go
vector<int> numbers;
numbers.push_back(1);  // Suitcase size 1
numbers.push_back(2);  // Buy size 2 suitcase, move everything
numbers.push_back(3);  // Buy size 4 suitcase, move everything
numbers.push_back(4);  // Still fits
numbers.push_back(5);  // Buy size 8 suitcase, move everything
```

```cpp
// Better Way
// Like knowing you need 5 items, so buy the right size suitcase first
vector<int> numbers;
numbers.reserve(5);    // Buy size 5 suitcase upfront
numbers.push_back(1);  // Just pack
numbers.push_back(2);  // Just pack
numbers.push_back(3);  // Just pack
numbers.push_back(4);  // Just pack
numbers.push_back(5);  // Just pack
```

## Practice Questions

??? question "1. Why call reserve() on a vector when you know the size?"

    It allocates the memory once up front, so push_back doesn't repeatedly allocate bigger blocks and move everything.

??? question "2. What is the suitcase analogy?"

    Without reserve you keep buying bigger suitcases and repacking. With reserve you buy the right size first and just pack.
