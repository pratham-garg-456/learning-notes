---
title: The yield Keyword
---

# The yield Keyword

In Python, the yield keyword is used inside a function to make it a generator. When a function contains yield, it doesn't return a single value and exit—instead, it can produce a series of values, one at a time, pausing after each yield and resuming where it left off when called again.

This is useful for:

- Producing a sequence of values (like a list) without storing them all in memory at once.
- Writing functions that can be paused and resumed, which is helpful for streaming data or handling large datasets.

Example:

```python
def count_up_to(n):
    i = 1
    while i <= n:
        yield i
        i += 1

for number in count_up_to(3):
    print(number)
# Output: 1 2 3
```

## Practice Questions

??? question "1. What does yield do in a Python function?"

    It turns the function into a generator: instead of returning one value and exiting, it produces values one at a time, pausing after each yield and resuming where it left off.

??? question "2. Why is a generator useful?"

    It produces a sequence of values without storing them all in memory, and it can be paused and resumed, which helps with streaming data and large datasets.

??? question "3. What does the count_up_to(3) example print?"

    1, 2, 3, one value per loop iteration.
