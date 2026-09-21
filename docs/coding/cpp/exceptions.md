---
title: Exceptions
---

# Exceptions

## Exceptions

Exceptions are used for error handling. When an exceptional (error) situation occurs, an exception can be **thrown** and then **caught** by a handler.

```cpp
#include <iostream>
using namespace std;

int divide(int a, int b) {
    if (b == 0)
        throw "Division by zero!"; // Throwing a C-style string as exception
    return a / b;
}

int main() {
    try {
        cout << divide(10, 0) << endl;
    } catch (const char* msg) {
        cout << "Exception caught: " << msg << endl;
    }
    return 0;
}
```

## `std::exception`

Header `<stdexcept>`

```cpp
#include <iostream>
#include <stdexcept>

int divide(int a, int b) {
    if (b == 0) throw std::runtime_error("Division by zero!");
    return a / b;
}

int main() {
    try {
        int result = divide(10, 0);
        std::cout << result << std::endl;
    } catch (const std::exception& e) {
        std::cout << "Caught exception: " << e.what() << std::endl;
    }
    return 0;
}
```

## Here’s a simple guide to different types of exceptions in C++ and when to use each:

---

### 1. `std::runtime_error`

- **When to use:** For errors that happen during program execution and are not necessarily programming mistakes (e.g., file not found, network error, invalid user input).
- **Example:**
    
    ```cpp
    if (!file.is_open()) {
        throw std::runtime_error("Could not open file");
    }
    
    ```
    

---

### 2. `std::logic_error`

- **When to use:** For errors that are due to a bug in the program logic (e.g., calling a method in the wrong state, invalid argument).
- **Example:**
    
    ```cpp
    if (index < 0) {
        throw std::logic_error("Index cannot be negative");
    }
    
    ```
    

---

### 3. `std::invalid_argument`

- **When to use:** When a function receives an argument that is not valid.
- **Example:**
    
    ```cpp
    if (name.empty()) {
        throw std::invalid_argument("Name cannot be empty");
    }
    
    ```
    

---

### 4. `std::out_of_range`

- **When to use:** When an argument is outside the allowed range (e.g., accessing a vector with an invalid index).
- **Example:**
    
    ```cpp
    if (index >= vec.size()) {
        throw std::out_of_range("Index out of range");
    }
    
    ```
    

---

### 5. `std::length_error`

- **When to use:** When an operation would create an object that is too large.
- **Example:**
    
    ```cpp
    if (newSize > MAX_SIZE) {
        throw std::length_error("Too big");
    }
    
    ```
    

---

### 6. `std::overflow_error` / `std::underflow_error`

- **When to use:** For arithmetic overflows or underflows.
- **Example:**
    
    ```cpp
    if (a > MAX_INT - b) {
        throw std::overflow_error("Integer overflow");
    }
    
    ```
    

---

### 7. `std::bad_alloc`

- **When to use:** When memory allocation fails (usually thrown by `new` automatically).
- **Example:**
    
    ```cpp
    int* arr = new int[1000000000]; // throws std::bad_alloc if not enough memory
    
    ```
    

---

### 8. Custom Exceptions

- **When to use:** For application-specific errors that don’t fit standard exceptions.
- **Example:**
    
    ```cpp
    class MyCustomError : public std::runtime_error {
    public:
        MyCustomError(const std::string& msg) : std::runtime_error(msg) {}
    };
    
    ```
    

---

**Summary Table:**

| Exception Type | Use For |
| --- | --- |
| runtime_error | Unexpected runtime problems |
| logic_error | Programming mistakes |
| invalid_argument | Bad function arguments |
| out_of_range | Index/argument out of allowed range |
| length_error | Object too large |
| overflow_error | Arithmetic overflow |
| underflow_error | Arithmetic underflow |
| bad_alloc | Memory allocation failure |
| custom | App-specific errors |

---

**Tip:**

Use the most specific exception type that matches the error. This makes your code easier to debug and handle!

## Practice Questions

??? question "1. What is an exception?"

    A way to handle errors: when an exceptional situation occurs, an exception is thrown and then caught by a handler.

??? question "2. When do you use runtime_error and when logic_error?"

    `runtime_error` for problems during execution that are not necessarily programming mistakes (file not found, invalid input). `logic_error` for bugs in the program logic.

??? question "3. What are invalid_argument and out_of_range for?"

    `invalid_argument` when a function receives an invalid argument. `out_of_range` when an argument is outside the allowed range, like a bad vector index.

??? question "4. When is bad_alloc thrown?"

    When memory allocation fails, usually thrown automatically by `new`.

??? question "5. What is the tip for choosing an exception type?"

    Use the most specific type that matches the error, which makes code easier to debug and handle.
