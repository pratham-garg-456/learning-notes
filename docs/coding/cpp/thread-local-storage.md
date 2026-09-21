---
title: Thread Local Storage
---

# Thread Local Storage

## What is `thread_local`?

`thread_local` is a storage specifier in C++ that ensures each thread has its **own separate instance** of a variable. The variable's lifetime matches the thread's lifetime, so it is unique to each thread and independent of the other threads' values.

```cpp
#include <iostream>
#include <thread>

// Declare thread-local variable
thread_local int k = 0;

void threadTask(int id, int value) {
    k = value; // Assign a unique value for this thread
    std::cout << "Thread " << id << ": k = " << k
              << ", Address of k = " << &k << std::endl;
}

int main() {
    k = 42; // Set the value of k for the main thread
    std::cout << "Main thread: k = " << k
              << ", Address of k = " << &k << std::endl;

    // Create two threads, each working with its own thread-local `k`
    std::thread t1(threadTask, 1, 100);
    std::thread t2(threadTask, 2, 200);

    t1.join();
    t2.join();

    // Back in the main thread
    std::cout << "Main thread again: k = " << k
              << ", Address of k = " << &k << std::endl;

    return 0;
}
```

Sample output:

```text
Main thread: k = 42, Address of k = 00000224A98F81D4
Thread 1: k = 100, Address of k = Thread 200000224A9907044
: k = 200, Address of k = 00000224A9908B84
Main thread again: k = 42, Address of k = 00000224A98F81D4
```

!!! tip
    Note that the address of the storage location for `k` is different for each thread. The output is messy because the threads share the same `cout`.

## Related notes

- [Multithreading](multithreading.md)
- [Thread Class](thread-class.md)

## Practice Questions

??? question "1. What does thread_local do?"

    It gives each thread its own separate instance of the variable, with a lifetime matching the thread's. The value in one thread is independent of the values in other threads.

??? question "2. In the example, what is k in main after both threads have finished?"

    Still 42. The threads set their own copies of `k` to 100 and 200, and never touch main's copy.

??? question "3. What in the output proves the copies are separate?"

    The address of `k` is different in the main thread, thread 1, and thread 2.

??? question "4. Why is the sample output jumbled?"

    The two threads write to the same `std::cout` at the same time, so their output interleaves.
