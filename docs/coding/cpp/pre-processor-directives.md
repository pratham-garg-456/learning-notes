---
title: Pre-processor Directives
---

# Pre-processor Directives

Pre-processor directives in C++ are instructions executed **before** the actual compilation begins. They prepare the source code by including files, defining macros, and selecting code conditionally. They are processed by the C++ pre-processor and always start with `#`.

The directives include:

- `#define`: defines a macro
- `#include`: inserts a file
- `#ifdef`: brackets conditional implementation
- `#ifndef`: brackets conditional implementation
- `#endif`: ends conditional implementation
- `#error`: sends an error message to `stdout`
- `#pragma`: passes a directive to the compiler or linker

## Macros

Macros define reusable code or text that is replaced before the program is compiled. The pre-processor performs the replacement.

### 1. Object-like macros

These replace a symbolic name with a constant value or text.

```cpp
#define SYMBOLIC_NAME Replacement_text
```

Example:

```cpp
#define PI 3.14159
double radius = 5;
double area = PI * radius * radius;
// Expanded to:
// double area = 3.14159 * radius * radius;
```

### 2. Function-like macros

These work like functions but are expanded directly as text.

```cpp
#define SQUARE(X) (X * X)
int result = SQUARE(5);
// Expanded to: (5 * 5)
```

!!! warning "Be careful: precedence issues"
    ```cpp
    #define SQUARE(X) X * X
    int result = SQUARE(2 + 3);
    // Expanded to:
    // int result = 2 + 3 * 2 + 3
    // int result = 2 + 6 + 3
    // int result = 11 (wrong!)
    ```

    **Fix:** wrap parameters in parentheses:

    ```cpp
    #define SQUARE(X) ((X) * (X))
    ```

### 3. Pre-defined macros

| Macro | Description |
| --- | --- |
| `__LINE__` | The current line number in the source file. |
| `__FILE__` | The name of the current source file. |
| `__DATE__` | The current date in "MMM DD YYYY" format. |
| `__TIME__` | The current time in "HH:MM:SS" format. |
| `__cplusplus` | Indicates the C++ standard version (e.g., 201103L for C++11). |

Example:

```cpp
std::cout << "This code is in file " << __FILE__
          << " at line " << __LINE__ << std::endl;
```

### Continuation of macros

If a macro spans multiple lines, use `\` to continue it.

```cpp
#define LARGE_TEXT "This is a long piece of text \
that spans multiple lines."
```

### Side effects and risks

Macros simply replace text, so unexpected side effects can occur.

```cpp
#define SQUARE(X) ((X) * (X))
int r = 3;
int result = SQUARE(r++);
// Expands to:
// int result = ((r++) * (r++))
```

**Fix:** avoid macros where side effects might occur. Use inline functions instead:

```cpp
inline int square(int x) {
    return x * x;
}
```

## `#include`

- `#include` inserts files into the code during pre-processing.
- It can include system libraries (with `< >`) or custom header files (with `" "`).
- It is good practice to use it for header files, which organize function declarations, constants, and other reusable components.

Example header file, `myheader.h`:

```cpp
#ifndef MYHEADER_H
#define MYHEADER_H

void greet(); // Function declaration

#endif
```

`main.cpp`:

```cpp
#include <iostream>
#include "myheader.h"

void greet() {
    std::cout << "Hello, world!" << std::endl;
}

int main() {
    greet();
    return 0;
}
```

## Conditional directives

Conditional directives include or exclude parts of code based on conditions, typically macro values. They are useful for platform-specific code, debugging, and preventing multiple definitions of the same entities. There are two types:

1. Logical directives
2. Definitional directives

### Logical directives

Logical directives control which block of code is included based on a condition, usually an expression that evaluates to true (non-zero) or false (zero).

```cpp
#if CONDITION
  // group of statements
#elif CONDITION
  // group of statements
#else
  // group of statements
#endif
```

Example:

```cpp
#define CASE_A 0
#define CASE_B 1
#define CASE_C 2

#define CASE CASE_C

#if CASE == CASE_A
  #include "case_a.h"
#elif CASE == CASE_B
  #include "case_b.h"
#elif CASE == CASE_C
  #include "case_c.h"
#endif
```

### Definitional directives

Definitional directives check whether a symbolic name (macro) exists and conditionally include code. There are two forms:

1. Definitional construct
2. Functional directive

#### 1. Definitional construct

It checks whether a macro has been defined with `#ifdef` (if defined) or `#ifndef` (if not defined).

- `#ifdef SYMBOLIC_NAME` includes the following block if `SYMBOLIC_NAME` is defined.
- `#ifndef SYMBOLIC_NAME` includes the following block if `SYMBOLIC_NAME` is **not** defined.

Example: preventing multiple inclusions.

```cpp
#ifndef SHAPE_H
#define SHAPE_H
// Header content for Shape.h

class Shape {
public:
  virtual double volume() const;
};

#endif // SHAPE_H
```

Example: conditional debugging code.

```cpp
#define DEBUG

int main() {
  // production instructions

  #ifdef DEBUG
  // debugging code, prints extra information
  #endif

  // production instructions
}
```

- If `DEBUG` is defined, the debugging code is included.
- If `DEBUG` is not defined (for example, `#define DEBUG` is commented out), the debugging code is excluded.

#### 2. Functional directive

It uses the `defined` operator to check whether a macro has been defined, often inside `#if`.

```cpp
#if defined(SYMBOLIC_NAME)
  group of statements
#endif
```

`defined(SYMBOLIC_NAME)` is true if the macro has been defined and false if not.

Example: compound logical expressions. You can combine several `defined` checks with `&&` and `||`.

```cpp
#if defined(DEBUG) && defined(VERBOSE)
  // Code to include if both DEBUG and VERBOSE are defined
#elif defined(DEBUG)
  // Code to include if only DEBUG is defined
#endif
```

#### Choosing between them

- Use **definitional constructs** (`#ifdef`, `#ifndef`) for straightforward single-macro checks or include guards in header files.
- Use **functional directives** (`#if defined()`) when the condition needs multiple checks or combinations of logical expressions.

## `#error`

**Purpose.** Generates a custom error message during pre-processing. Helpful for alerting the programmer about unsupported configurations, missing definitions, or invalid conditions.

```cpp
#error <message>
```

**Behavior.** When the pre-processor reaches `#error`, it stops further processing and outputs the message to standard output (`stdout`).

**Use cases**

1. Identifying unsupported compilers or platforms.
2. Debugging or enforcing required conditions.
3. Alerting about incomplete or missing functionality.

Example:

```cpp
#ifndef SUPPORTED_FEATURE
#error "The required feature is not supported!"
#endif
```

## `#pragma`

**Purpose.** Issues special instructions or configuration settings to the compiler or linker. Its effect is compiler-specific.

```cpp
#pragma <command>
```

**Common uses**

- Controlling warnings.
- Enabling or disabling optimizations.
- Managing memory alignment or packing.
- Linking specific libraries.

**Examples**

1. Disabling a warning:

    ```cpp
    #pragma warning(disable : 4996) // Disable deprecation warning
    ```

2. Setting memory alignment:

    ```cpp
    #pragma pack(push, 1) // Set memory alignment to 1-byte boundaries
    struct MyStruct {
        char a;
        int b;
    };
    #pragma pack(pop) // Restore previous alignment
    ```

3. Linking libraries (Visual Studio):

    ```cpp
    #pragma comment(lib, "user32.lib") // Link user32.lib
    ```

**Limitations**

- The functionality of `#pragma` varies across compilers.
- It is non-portable: directives written for one compiler might not work with another.

## Practice Questions

??? question "1. When does the pre-processor run, and what do directives start with?"

    Before the actual compilation begins. Every directive starts with `#`.

??? question "2. Why is #define SQUARE(X) X * X dangerous, and what are the fixes?"

    It is plain text substitution, so `SQUARE(2 + 3)` expands to `2 + 3 * 2 + 3`, which is 11 instead of 25. Wrap each parameter and the whole expansion in parentheses: `((X) * (X))`. Even then `SQUARE(r++)` expands to two increments, so prefer an inline function.

??? question "3. What are include guards and how do they work?"

    A pattern using `#ifndef NAME`, `#define NAME`, and `#endif` around a header's contents. The first time the header is included the name is not yet defined, so the contents are used and the name gets defined. Later includes skip the contents, preventing multiple definitions.

??? question "4. When would you use #if defined() instead of #ifdef?"

    When the condition combines several checks, for example `#if defined(DEBUG) && defined(VERBOSE)`. For a single-macro check or an include guard, `#ifdef` and `#ifndef` are enough.

??? question "5. What does #error do, and when is it useful?"

    It stops pre-processing and prints a custom message. It is useful for flagging unsupported compilers or platforms, missing definitions, or invalid configurations.

??? question "6. Why is #pragma a portability risk?"

    Its behavior is compiler-specific. A directive that works on one compiler may be ignored or fail on another.
