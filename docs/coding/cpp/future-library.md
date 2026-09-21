---
title: Future Library
---

# `future` Library

The `<future>` library in C++ provides a mechanism for asynchronous programming and **inter-thread communication** by letting tasks share values through **shared states**. It is especially useful in multithreading, where you might compute a value in one thread and retrieve it in another.

![Provider and future sharing a value](https://advoop.sdds.ca/assets/images/future-c5a76a02c68df33889aab4d113efddb7.png)

## Core concepts

1. **Shared state**
    - A shared state holds a value (or an exception) that is passed between a provider (for example a thread, `std::promise`, `std::packaged_task`, or `std::async()`) and a consumer (`std::future`).
    - The shared state survives as long as either the provider or the consumer exists.
2. **Provider**
    - Creates the shared state and sets a value in it.
3. **Future object**
    - A `std::future` object is associated with the shared state and can retrieve the value once it becomes available.
4. **Synchronization**
    - Futures act as a synchronization point between tasks, ensuring a thread waits for the shared state to be ready before accessing it.

## Promise and future

Here the promise object is passed to the thread along with the function pointer and its remaining arguments.

```cpp
#include <iostream>
#include <future>
#include <thread>

void compute_sum(std::promise<int>&& prom, int a, int b) {
    std::this_thread::sleep_for(std::chrono::seconds(2)); // Simulate work
    prom.set_value(a + b); // Set the value in the shared state
}

int main() {
    // Create a promise and a future
    std::promise<int> prom;
    std::future<int> fut = prom.get_future();

    // Launch a thread to compute the sum
    std::thread t(compute_sum, std::move(prom), 5, 10);

    std::cout << "Waiting for the result...\n";

    // Retrieve the result
    std::cout << "The result is: " << fut.get() << std::endl;

    t.join();
    return 0;
}
```

```cpp
// Promise - Future
// promise_future.cpp

#include <iostream>
#include <thread>
#include <future>

void task(std::promise<double>& p)
{
    p.set_value(12.34);
}

int main()
{
    std::promise<double> p;
    std::future<double> f = p.get_future();
    std::thread t(task, std::ref(p));
    std::cout << "Value = " << f.get()<< std::endl;
    t.join();
}
```

!!! tip "std::ref vs std::move"
    | Aspect | `std::ref` | `std::move` |
    | --- | --- | --- |
    | **Promise ownership** | Remains with the main thread | Transferred to the thread function |
    | **Promise accessibility** | Accessible in both main and thread function | Accessible only in the thread function |
    | **Use case** | Shared access; main thread keeps control | Exclusive ownership by the thread |
    | **Thread safety** | Care needed if multiple threads access it | Safer, as only one thread owns the object |

## Packaged task

It packages the task together with the shared state. Calling the `packaged_task` executes the task, either with the `()` operator or implicitly in a separate thread.

```cpp
// Packaged Task
// packaged_task.cpp

#include <iostream>
#include <thread>
#include <future>

double task(double x) { return x * 2; }

int main()
{
    std::packaged_task<double(double)> pt(task);

    auto f = pt.get_future();
    pt(10);

    //OR

    // Launch the task in a separate thread
    std::thread t(std::move(pt), 16.0);


    double r = f.get();

    std::cout << "Result = " << r << std::endl;
}
```

!!! tip
    If you use the thread way, don't forget to join the thread in main with `t.join()`.

## async()

It launches `task()` asynchronously and returns the future object associated with the shared state.

```cpp
// Asynchronous Launch
// async.cpp

#include <iostream>
#include <thread>
#include <future>

double task(double x) { return x * 2; }

int main()
{
    std::future<double> f = std::async(task, 10);
    double r = f.get();
    std::cout << "Result = " << r << std::endl;
}
```

### When to use `std::async`

- When you need to perform tasks asynchronously with minimal boilerplate.
- When you need the result of the task and prefer `std::future` for synchronization.
- When you want automatic thread management without creating explicit `std::thread` objects.

### Advantages of `std::async`

1. **Simple syntax**: launching asynchronous tasks is straightforward.
2. **Built-in synchronization**: result retrieval is synchronized using `std::future`.
3. **Flexible launch policies**: supports both asynchronous and deferred execution.
4. **Automatic resource management**: threads created by `std::async` are automatically joined.

### Comparison of `std::async`, `std::packaged_task` and `std::promise`

| Feature | `std::async` | `std::packaged_task` | `std::promise` |
| --- | --- | --- | --- |
| **Ease of use** | Simplifies task launch | Requires manual task wrapping | Requires manual value setting |
| **Thread management** | Automatic | Manual | Manual |
| **Future integration** | Automatically provides `std::future` | Explicitly provides `std::future` | Requires explicit `std::future` |
| **Use case** | When you want a quick async task | When task execution must be controlled | When shared state needs custom control |

`std::async` is perfect for quick, asynchronous operations with minimal manual effort. It is less flexible than `std::packaged_task` or `std::promise`, but its simplicity often makes it the best choice.

## Checking the validity of a future and how it changes

```cpp
// Future Class Template - Explicit Asynchronous Launch
// future_async.cpp

#include <iostream>
#include <future>

double get() { return 12.34; }

int main()
{
    std::future<double> f; // default ctor
    std::future<double> g = std::async(get); // move-ctor

    std::cout << "After Construction" << std::endl;
    std::cout << (f.valid() ? "f is valid" : "f is not valid") << std::endl;
    std::cout << (g.valid() ? "g is valid" : "g is not valid") << std::endl;

    f = std::move(g); // move-assignment

    std::cout << "After Assignment" << std::endl;
    std::cout << (f.valid() ? "f is valid" : "f is not valid") << std::endl;
    std::cout << (g.valid() ? "g is valid" : "g is not valid") << std::endl;

    double a = f.get(); // retrieve shared value

    std::cout << "After Retrieval" << std::endl;
    std::cout << (f.valid() ? "f is valid" : "f is not valid") << std::endl;
    std::cout << (g.valid() ? "g is valid" : "g is not valid") << std::endl;

    std::cout << "Return Value = " << a << std::endl;
}
```

```text
After Construction
f is not valid
g is valid
After Assignment
f is valid
g is not valid
After Retrieval
f is not valid
g is not valid
Return Value = 12.34
```

### Key learnings

1. **Default construction**: a `std::future` created with the default constructor is **not valid**.
2. **Move semantics**: moving a shared state from one `std::future` to another transfers ownership. The future that gives up ownership becomes **not valid**, and the one that takes ownership becomes **valid**.
3. **`get()`**: calling `get()` on a valid `std::future` retrieves the value, and the future becomes **not valid**.

!!! tip
    A `std::future` can move between valid and not-valid states depending on operations like move-assignment and value retrieval with `get()`.

## Related notes

- [Multithreading](multithreading.md)
- [Thread Class](thread-class.md)

## Practice Questions

??? question "1. What is a shared state, and who are the provider and the consumer?"

    A shared state holds a value (or exception) passed between a **provider** (a thread, `std::promise`, `std::packaged_task`, or `std::async()`) and a **consumer** (`std::future`). It survives as long as either side exists.

??? question "2. How does a promise and future pair work?"

    You get a future from the promise with `get_future()`, pass the promise to a thread, and that thread calls `set_value()`. The consumer calls `fut.get()`, which waits until the value is ready and returns it.

??? question "3. What is the difference between std::ref and std::move when passing a promise to a thread?"

    With `std::ref` the promise stays owned by the main thread and both threads can access it, so you must be careful if several threads use it. With `std::move` ownership transfers to the thread function, so only that thread can use it, which is safer.

??? question "4. When would you choose async over packaged_task or promise?"

    When you want a quick asynchronous task with minimal boilerplate: it launches the task, manages the thread automatically, and returns a `std::future` for the result. `packaged_task` and `promise` give more control but need manual setup.

??? question "5. In the validity example, why is f not valid after get()?"

    Calling `get()` on a valid future retrieves the shared value and consumes it, so the future becomes not valid. Similarly a default-constructed future is not valid, and after `f = std::move(g)` the source `g` becomes not valid.
