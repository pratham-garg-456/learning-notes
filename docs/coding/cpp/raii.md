---
title: RAII
---

# RAII (Resource Acquisition Is Initialization)

RAII is a C++ concept where a **resource's lifecycle is tied to the lifetime of an object**. It ensures that resources such as memory, file handles, sockets, or database connections are properly managed by encapsulating them in objects.

## Example 1: memory management

Using `std::unique_ptr` to manage dynamically allocated memory:

```cpp
#include <iostream>
#include <memory>

void exampleRAII() {
    std::unique_ptr<int> ptr(new int(42)); // Acquire resource
    std::cout << "Value: " << *ptr << std::endl;
} // Resource automatically released when ptr goes out of scope

int main() {
    exampleRAII(); // No need to delete the memory manually
    return 0;
}
```

- `std::unique_ptr` encapsulates dynamic memory.
- Its destructor automatically deletes the memory when `ptr` goes out of scope.

## Example 2: file handling

RAII ensures proper handling of file resources:

```cpp
#include <iostream>
#include <fstream>
#include <string>

void readFile(const std::string& filename) {
    std::ifstream file(filename); // Acquire resource
    if (!file.is_open()) {
        throw std::runtime_error("Could not open file");
    }

    std::string line;
    while (std::getline(file, line)) {
        std::cout << line << std::endl;
    } // File automatically closed when 'file' goes out of scope
}

int main() {
    try {
        readFile("example.txt");
    } catch (const std::exception& e) {
        std::cerr << "Error: " << e.what() << std::endl;
    }
    return 0;
}
```

- `std::ifstream` opens a file in its constructor.
- Its destructor closes the file when `file` goes out of scope, so nothing leaks.

## Example 3: custom RAII wrapper

A custom RAII class for a raw resource (here, a C-style file handle):

```cpp
#include <iostream>
#include <cstdio>

class FileRAII {
    FILE* file;

public:
    FileRAII(const char* filename, const char* mode) {
        file = fopen(filename, mode); // Acquire resource
        if (!file) {
            throw std::runtime_error("Failed to open file");
        }
    }

    ~FileRAII() {
        if (file) {
            fclose(file); // Release resource
        }
    }

    FILE* get() { return file; }
};

int main() {
    try {
        FileRAII file("example.txt", "r");
        // Use file.get() for file operations...
        std::cout << "File successfully managed!" << std::endl;
    } catch (const std::exception& e) {
        std::cerr << e.what() << std::endl;
    }
    return 0;
}
```

- `FileRAII` wraps a raw `FILE*` resource.
- It ensures the file is closed when the `FileRAII` object goes out of scope.

## Common RAII classes in C++

1. **Memory management**: `std::unique_ptr`, `std::shared_ptr`
2. **File handling**: `std::ifstream`, `std::ofstream`
3. **Thread management**: `std::thread`
4. **Lock management**: `std::lock_guard`, `std::unique_lock`

## Practice Questions

??? question "1. What does RAII mean, and what problem does it solve?"

    Resource Acquisition Is Initialization: a resource's lifecycle is tied to the lifetime of an object. The resource is acquired in the constructor and released in the destructor, so memory, files, sockets and connections are cleaned up automatically, even when an exception is thrown.

??? question "2. In the FileRAII example, where is the file closed, and who calls it?"

    In the destructor `~FileRAII()`, which runs automatically when the `FileRAII` object goes out of scope. The programmer never calls `fclose` directly.

??? question "3. Why doesn't exampleRAII need a delete?"

    The memory is owned by a `std::unique_ptr`. When `ptr` goes out of scope at the end of the function, its destructor deletes the memory.

??? question "4. Name one RAII class each for memory, files, and locks."

    Memory: `std::unique_ptr` (or `std::shared_ptr`). Files: `std::ifstream` / `std::ofstream`. Locks: `std::lock_guard` (or `std::unique_lock`).
