---
title: Classes and Objects
---

# Classes and Objects

## Class

### Instance Variable

Data members that belongs to an object (instance) of a class.

```cpp
class MyClass {
public:
    int instanceVar; // Instance variable
};
```

### Class Variable (Static)

Class variable is shared among all objects of class.

```cpp
class MyClass {
public:
    static int classVar; // Class variable
};
// Definition outside the class:
int MyClass::classVar = 0;
```

#### Example:

??? note "Code"
    
    ```cpp
    #include <iostream>
    using namespace std;
    
    class Counter {
    public:
        int instanceCounter;           // Instance variable
        static int totalCounter;       // Class variable
    
        Counter() {
            instanceCounter = 0;
            totalCounter++;
        }
    
        void increment() {
            instanceCounter++;
        }
    };
    
    int Counter::totalCounter = 0; // Initialize static variable
    
    int main() {
        Counter c1, c2;
        c1.increment();
        c2.increment();
        c2.increment();
    
        cout << "c1.instanceCounter = " << c1.instanceCounter << endl; // 1
        cout << "c2.instanceCounter = " << c2.instanceCounter << endl; // 2
        cout << "Counter::totalCounter = " << Counter::totalCounter << endl; // 2
    
        return 0;
    }
    ```
    
??? note "Output"
    
    ```cpp
    c1.instanceCounter = 1
    c2.instanceCounter = 2
    Counter::totalCounter = 2
    ```
    

### Member Functions

Function that works on **objects of the class** and can **access** both instance (**non-satic**) and class (**static**) members

```cpp
class MyClass {
public:
    int data;
    void setData(int d) {  // Member function
        data = d;
    }
};
```

### Class Functions (Static)

Cannot operate on Object (instance) of a class and cannot access data members directly.

```cpp
class MyClass {
public:
    static void showMessage() {  // Static member function (class function)
        std::cout << "Hello from class function\n";
    }
};

// Usage:
MyClass::showMessage(); // Called without needing an object
```

#### Example:

??? note "Code"
    
    ```cpp
    #include <iostream>
    using namespace std;
    
    class Counter {
    public:
        int value; // Instance variable
    
        void increment() { // Member function
            value++;
        }
    
        static void printClassName() { // Static member function (class function)
            cout << "Class: Counter" << endl;
            // cout << value; // ERROR: Cannot access instance variable
        }
    };
    
    int main() {
        Counter c;
        c.value = 0;
        c.increment();
        cout << c.value << endl; // 1
    
        Counter::printClassName(); // Static function called via class
        c.printClassName();        // Also allowed, but not recommended
        return 0;
    }
    ```
    

!!! tip

    Don’t write `static` keyword when writting defination in `.c` file just need static keyword in `.h` file

## Practice Questions

??? question "1. What is an instance variable versus a class variable?"

    An instance variable belongs to one object. A class (static) variable is shared among all objects of the class.

??? question "2. What is the difference between a member function and a static function?"

    A member function works on an object and can access instance and static members. A static function can't operate on an instance or access instance data members directly.

??? question "3. In the Counter example, why is totalCounter 2 while c2.instanceCounter is 2 and c1 is 1?"

    `instanceCounter` is per object (c1 incremented once, c2 twice). `totalCounter` is shared and was incremented once per constructor call, and two objects were created.

??? question "4. Where do you write the static keyword?"

    Only in the header (`.h`) file declaration, not in the definition in the source file.
