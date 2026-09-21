---
title: Constructors and Destructors
---

# Constructors and Destructors

## Constructors

### `explicit` keyword

It prevents the compiler from using a connstructor for implicit (automatic) conversion.

#### **Where to use `explicit`?**

With constructors or conversion operators that take a single argument, to avoid unintended implicit conversion.

#### **Why use it?**

To make us call constructor directly, instead of letting the compiler convert the types without our knowledge.

#### Example:

Without `explicit`

```cpp
class MyClass {
public:
    MyClass(int x) { /* ... */ }
};

void foo(MyClass m) { /* ... */ }

foo(42); // Allowed! int 42 is implicitly converted to MyClass
```

With `explicit`

```cpp
class MyClass {
public:
    explicit MyClass(int x) { /* ... */ }
};

void foo(MyClass m) { /* ... */ }

foo(42); // ERROR! Cannot implicitly convert int to MyClass
foo(MyClass(42)); // OK: Explicit conversion
```

!!! tip

    **Rule of Thumb:**

    Use `explicit` on single-argument constructors unless you specifically want implicit conversion.

## `noexcept` keyword

Tells the  compiler (and readers) that a function does not throw exceptions.

### When to use:

In the functions that are guaranteed never throw exceptions, especially

- Destructor
- Move constructor/assignment (when safe)
- Simple  getters/setters

### Why

- Helps the compiler optimize code.
- Makes your code’s exception guarantees explicit.
- Standard library containers rely on `noexcept` for certain optimizations.

### Example

```cpp
class MyClass {
public:
    int getValue() const noexcept { 
			   return value; 
    }  // Simple getter, won't throw

    void reset() noexcept {
        value = 0;  // Won't throw
    }

    void doSomething(); // Might throw, don't use noexcept here

private:
    int value = 0;
};
```

!!! tip

    Rule of Thumb:

    Use `noexcept` if you are sure your function and everything it calls will not throw.

    If you are not sure,**do not use `noexcept`**

## Practice Questions

??? question "1. What does the explicit keyword do?"

    It prevents the compiler from using a constructor (or conversion operator) for implicit conversion, so you must call the constructor directly.

??? question "2. What is the rule of thumb for explicit?"

    Use it on single-argument constructors unless you specifically want implicit conversion.

??? question "3. What does noexcept mean and when should you use it?"

    It tells the compiler and readers that a function does not throw. Use it when you are sure the function and everything it calls won't throw, such as destructors, safe move operations, and simple getters and setters.

??? question "4. Why does noexcept matter?"

    It helps the compiler optimize, makes exception guarantees explicit, and standard library containers rely on it for certain optimizations.
