---
title: Sets
---

# Sets

!!! tip
    A Set is a built-in object that lets you store **unique values** of any type, whether primitive or object references.

**How to create a set**

- Passing an array to `new Set()`.
- Creating an empty set and using `add()` to add values.

```javascript
// Creating a new Set
const mySet = new Set();

// Adding values
mySet.add(1);
mySet.add(5);
mySet.add("hello");
mySet.add(1); // Duplicate, will be ignored

console.log(mySet); // Set { 1, 5, 'hello' }
```

## Methods

| Method | Description |
| --- | --- |
| [new Set()](https://www.w3schools.com/jsref/jsref_set_new.asp) | Creates a new Set |
| [add()](https://www.w3schools.com/jsref/jsref_set_add.asp) | Adds a new element to the Set |
| [clear()](https://www.w3schools.com/jsref/jsref_set_clear.asp) | Removes all elements from a Set |
| [delete()](https://www.w3schools.com/jsref/jsref_set_delete.asp) | Removes an element from a Set |
| [entries()](https://www.w3schools.com/jsref/jsref_set_entries.asp) | Returns an Iterator with the [value, value] pairs from a Set |
| [forEach()](https://www.w3schools.com/jsref/jsref_set_foreach.asp) | Invokes a callback for each element |
| [has()](https://www.w3schools.com/jsref/jsref_set_has.asp) | Returns true if a value exists |
| [keys()](https://www.w3schools.com/jsref/jsref_set_keys.asp) | Same as values() |
| [values()](https://www.w3schools.com/jsref/jsref_set_values.asp) | Returns an Iterator with the values in a Set |

```javascript
// 1. new Set() - Creates a new Set
const set = new Set([1, 2, 3]);
console.log(set); // Set { 1, 2, 3 }

// 2. add() - Adds a new element to the Set
set.add(4);
console.log(set); // Set { 1, 2, 3, 4 }

// 3. clear() - Removes all elements from a Set
set.clear();
console.log(set); // Set {}

// 4. delete() - Removes an element from a Set
const set2 = new Set([1, 2, 3]);
set2.delete(2);
console.log(set2); // Set { 1, 3 }

// 5. entries() - Returns an Iterator with the [value, value] pairs
const set3 = new Set(['a', 'b']);
for (const entry of set3.entries()) {
  console.log(entry); // ['a', 'a'] then ['b', 'b']
}

// 6. forEach() - Invokes a callback for each element
set3.forEach((value) => {
  console.log(value); // 'a' then 'b'
});

// 7. has() - Returns true if a value exists
console.log(set3.has('a')); // true
console.log(set3.has('z')); // false

// 8. keys() - Same as values()
for (const key of set3.keys()) {
  console.log(key); // 'a' then 'b'
}

// 9. values() - Returns an Iterator with the values in a Set
for (const value of set3.values()) {
  console.log(value); // 'a' then 'b'
}
```

## Practice Questions

??? question "1. What is a Set, and what happens if you add a duplicate?"

    A built-in object that stores unique values of any type. Adding a duplicate is ignored.

??? question "2. What are two ways to create a set?"

    Pass an array to `new Set()`, or create an empty set and use `add()` to add values.

??? question "3. What is the difference between keys() and values() on a Set?"

    None: `keys()` is the same as `values()`. `entries()` returns `[value, value]` pairs.

??? question "4. How do you check whether a value is in a set?"

    Use `has(value)`, which returns true if the value exists.
