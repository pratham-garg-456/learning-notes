---
title: Algorithms: find_if_not
---

# Algorithms: find_if_not

## `find_if_not`

Finds the first element in a range for which the predicate returns `false`.

example:

```cpp
auto start = find_if_not(str.begin(), str.end(), ::isspace); //Finds the first character that is **not** a whitespace from the beginning.
auto end = find_if_not(str.rbegin(), str.rend(), ::isspace).base(); // Finds the first character that is **not** a whitespace from the end (using a reverse iterator), then converts it back to a forward iterator with `.base()`.
```

## Practice Questions

??? question "1. What does find_if_not do?"

    Finds the first element in a range for which the predicate returns false.

??? question "2. How does the example trim whitespace from both ends?"

    `find_if_not(str.begin(), str.end(), ::isspace)` finds the first non-space character. Doing the same with reverse iterators and calling `.base()` converts the result back to a forward iterator for the end.
