---
title: The string Library
---

# The string Library

## `string()`

The below constructor is used to make string from iterators
`template <class InputIterator>  string  (InputIterator first, InputIterator last);`

Useage:

```cpp
 string Utilities::removeSpace(const string& str) {
    auto start = find_if_not(str.begin(), str.end(), ::isspace);
    if (start == str.end()) return "";
    auto end = find_if_not(str.rbegin(), str.rend(), ::isspace).base();
    return string(start, end);
}
```

## `stoi`

convert string into integer

## `stoul`

convert string into unsigned long

## `find`

Find the position of the string

| *string (1)* | `size_t find (const string& str, size_t pos = 0) const noexcept;` |
| --- | --- |
| *c-string (2)* | `size_t find (const char* s, size_t pos = 0) const;` |
| *buffer (3)* | `size_t find (const char* s, size_t pos, size_type n) const;` |
| *character (4)* | `size_t find (char c, size_t pos = 0) const noexcept;` |

## `find_first_not_of`

| *string (1)* | `size_t find_first_not_of (const string& str, size_t pos = 0) const noexcept;` |
| --- | --- |
| *c-string (2)* | `size_t find_first_not_of (const char* s, size_t pos = 0) const;` |
| *buffer (3)* | `size_t find_first_not_of (const char* s, size_t pos, size_t n) const;` |
| *character (4)* | `size_t find_first_not_of (char c, size_t pos = 0) const noexcept;` |

```cpp
// string::find_first_not_of
#include <iostream>       // std::cout
#include <string>         // std::string
#include <cstddef>        // std::size_t

int main ()
{
  std::string str ("look for non-alphabetic characters...");

  std::size_t found = str.find_first_not_of("abcdefghijklmnopqrstuvwxyz ");

  if (found!=std::string::npos)
  {
    std::cout << "The first non-alphabetic character is " << str[found];
    std::cout << " at position " << found << '\n';
  }

  return 0;
}
```

## Practice Questions

??? question "1. How do you build a string from a range of iterators?"

    Use the constructor `string(first, last)`, as in the `removeSpace` example that trims whitespace.

??? question "2. What do stoi and stoul do?"

    `stoi` converts a string to an integer, and `stoul` converts it to an unsigned long.

??? question "3. What does find_first_not_of return?"

    The position of the first character that is not in the given set, or `string::npos` if there is none.
