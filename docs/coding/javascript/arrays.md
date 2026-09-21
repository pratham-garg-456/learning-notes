---
title: Arrays
---

# Arrays

## Methods

### `map()`

- Transforms each element in an array using a provided function.
- Returns a new array of the same length with the transformed elements.

```javascript
[1, 2, 3].map(x => [x, x * 2]);
// Output: [[1, 2], [2, 4], [3, 6]]
```

### `flat()`

- Flattens nested arrays into a single array up to a specified depth.
- Does not apply any transformation, just removes nesting.

```javascript
[[1, 2], [3, 4]].flat();
// Output: [1, 2, 3, 4]
```

### `flatMap()`

- Combines the functionality of `map` followed by `flat` (with a depth of 1).
- Transforms each element, then flattens the result by one level.
- Often used to avoid creating extra levels of nesting.

```javascript
[1, 2, 3].flatMap(x => [x, x * 2]);
// Output: [1, 2, 2, 4, 3, 6]
```

### `from()`

A JavaScript method that creates a new, shallow-copied array instance from an array-like or iterable object. It can also apply a mapping function to each element.

```javascript
Array.from('hello');
// Output: ['h', 'e', 'l', 'l', 'o']

Array.from([1, 2, 3], x => x * 2);
// Output: [2, 4, 6]

Array.from({ length: 5 }, (_, i) => i);
// Output: [0, 1, 2, 3, 4]
```

See also topic 11 (Array methods) in the [JavaScript study plan](index.md).

## Practice Questions

??? question "1. What is the difference between map() and flatMap()?"

    `map()` transforms each element and returns a new array of the same length (which may contain nested arrays). `flatMap()` does a `map` and then flattens the result by one level, avoiding extra nesting.

??? question "2. What does flat() do?"

    Flattens nested arrays into a single array up to a specified depth, without transforming any elements.

??? question "3. What does Array.from() do? Give an example."

    Creates a new, shallow-copied array from an array-like or iterable object, optionally applying a mapping function. `Array.from('hello')` gives `['h', 'e', 'l', 'l', 'o']`, and `Array.from({ length: 5 }, (_, i) => i)` gives `[0, 1, 2, 3, 4]`.
