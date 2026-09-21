---
title: Thread Class
---

# Thread Class

The `thread` library provides support for creating and managing threads that execute concurrently.

The `thread` class defines an object that represents a single thread of execution in a process. A thread object is either joinable or not joinable.

```cpp
// Thread Class
// thread.cpp

#include <iostream>
#include <string>
#include <thread>

void task(const std::string& str)
{
    std::cout << str + " says Hi\n";
}

int main()
{
    // spawn child thread t1
    std::thread t1(task, "t1");

    // spawn child thread t2
    std::thread t2(task, "t2");

    // continue executing main thread
    task("main");

    // synchronize - IMPORTANT!
    t2.join();
    t1.join();
}
```

!!! tip
    The synchronization step is necessary. Had we neglected to `join()` the spawned threads to the main thread, the result would be undefined.

The three threads (main, t1 and t2) run independently, and any of them can finish printing first, so the order of the output is random. But main waits for t1 and t2 to finish before ending itself, because t1 and t2 are joined to it.

## Related notes

- [Multithreading](multithreading.md)
- [Future Library](future-library.md)

## Practice Questions

??? question "1. What does std::thread represent?"

    A single thread of execution in a process. A thread object is either joinable or not joinable.

??? question "2. Why must you call join() on a spawned thread?"

    `join()` synchronizes the spawned thread with the thread that created it: the caller waits for it to finish. If you don't join, the result is undefined.

??? question "3. Why can the output of the example appear in a different order each run?"

    main, t1 and t2 run independently, and any of them can finish printing first. Only the ending is ordered: main waits for t1 and t2 before it finishes.
