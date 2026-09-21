---
title: JavaScript
---

# JavaScript

## Topic notes

- [History of Browsing](history-of-the-browser.md)
- [Variables](variables.md)
- [Data Types](data-types.md)
- [Arrays](arrays.md)
- [Sets](sets.md)

## Study plan

## Where you are right now

| # | Topic | Status |
| --- | --- | --- |
| 1 | Scope: `var`, `let`, `const` | Done |
| 2 | Hoisting | Done |
| 3 | Closures | Done |
| 4 | Reference vs value | Done |
| 5 | Callbacks | **Start here** |
| 6 | setTimeout and the event loop | |
| 7 | Promises | |
| 8 | async / await | |
| 9 | Errors in async code | |
| 10 | The keyword `this` | |
| 11 | Array methods | |
| 12 | TypeScript basics | |

---

## Part 1: Foundations (done, but verify)

### 1. Scope

**What it is:** where a variable can be seen from.

**Learn**

- Block scope (`let`, `const`) vs function scope (`var`)
- Why `var` escapes out of `if` blocks and `for` loops
- `const` protects the *label*, not the contents: `const arr = []` still allows `arr.push()`
- Use `const` by default, `let` when the value is reassigned, `var` never

**Prove it**

```javascript
// What prints? Why?
if (true) {
  var a = 1;
  let b = 2;
}
console.log(a);
console.log(b);
```

**Where:** [javascript.info: Variable scope](https://javascript.info/closure)

### 2. Hoisting

**What it is:** JavaScript reads your whole file before running it, so some things exist before their line.

**Learn**

- `var` is hoisted and set to `undefined`: usable before its line, holding nothing
- `let` and `const` are hoisted too, but *unusable* until their line runs (this gap is called the Temporal Dead Zone)
- Function declarations are fully hoisted; function expressions aren't

**Prove it**

```javascript
console.log(a);   // ?
console.log(b);   // ?
var a = 1;
let b = 2;
```

**Where:** [javascript.info: Variable scope](https://javascript.info/closure)

### 3. Closures

**What it is:** a function that keeps access to the variables it was created next to, even after the outer function has finished. The backpack.

**Learn**

- Functions can be returned from other functions
- A returned function carries its variables with it
- Each call to the outer function makes a *fresh* set of variables: separate backpacks
- The backpack holds a **live link**, not a frozen copy
- This is how you make private state in JavaScript

**Prove it:** write all four from a blank file.

```javascript
// 1. makeCounter: increment, decrement, get, reset
// 2. makeGreeter(name): returns a function that greets
// 3. multiplier(n): returns a function that multiplies by n
// 4. once(fn): runs fn the first time, returns the cached result forever after
```

`once` is the real test. It needs two things in the backpack: whether it has run, and what it returned.

**Where:** [javascript.info: Closure](https://javascript.info/closure)

### 4. Reference vs value

**What it is:** numbers and strings get copied. Objects and arrays get *shared*.

**Learn**

- `const a = {…}; const b = a;` is one object with two labels. Changing `b` changes `a`.
- `[1,2] === [1,2]` is `false`: comparison is by identity, not contents
- Shallow copy (`{...obj}`, `[...arr]`) vs deep copy (`structuredClone`)
- **Why it matters in React:** this is why `useEffect` with an object in the dependency array re-fires every render

**Prove it**

```javascript
const a = { count: 1 };
const b = a;
b.count = 2;
console.log(a.count);          // ?
console.log([1,2] === [1,2]);  // ?
```

`===` on objects and arrays doesn't look inside them at all. It only checks: **is this literally the same object in memory, or two different ones?** It never compares contents.

**Where:** [javascript.info: Object references and copying](https://javascript.info/object-copy)

---

## Part 2: Async (the big one)

This is where most self-taught developers stall, and it's where your remaining wrong answers live. Take it slowly. Topics 5 to 9 are really **one topic** told in five steps.

### 5. Callbacks

**What it is:** handing a function to another function so it can run it later.

You've been doing this all along: `onClick={handleClick}` is a callback. You just didn't have the word.

**Learn**

- Functions are values. You can store them in variables, pass them as arguments, return them.
- The difference between `sayHi` (the function itself) and `sayHi()` (the result of running it). Passing the second by mistake is a classic bug.
- Writing a function that *takes* a function as an argument
- Callback hell: what nested callbacks look like, and why promises were invented to fix it

**Prove it**

```javascript
// 1. Write repeat(n, fn) that calls fn n times, passing the index each time
//    repeat(3, i => console.log(i));   // 0 1 2

// 2. Write your own version of forEach:
//    myForEach([10,20,30], (item, i) => console.log(i, item));

// 3. Explain out loud: what's the difference between these two lines?
setTimeout(sayHi, 1000);
setTimeout(sayHi(), 1000);
```

**Where:** [javascript.info: Callbacks](https://javascript.info/callbacks) (just the first section)

### 6. setTimeout and the event loop

**What it is:** how JavaScript handles things that happen *later*.

**Learn**

- JavaScript has **one worker**. It does one thing at a time.
- `setTimeout(fn, 0)` doesn't mean "run now." It means "put this on a list, run it when you're free."
- All normal code finishes completely before anything on the list runs
- There are **two lists**: promises (microtasks) and timers (macrotasks)
- **The order is always: normal code, then promises, then timers**
- `clearTimeout`, `setInterval`, `clearInterval`

**Prove it**

```javascript
// Predict the output before running:
console.log('A');
setTimeout(() => console.log('B'), 0);
Promise.resolve().then(() => console.log('C'));
console.log('D');
```

```javascript
// Why does this print 3 3 3 and not 0 1 2?
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 0);
}
// Now fix it three ways: with let, with an IIFE, and with setTimeout's third argument
```

**Where:** [javascript.info: Event loop](https://javascript.info/event-loop) · [Loupe visualizer](http://latentflip.com/loupe/) (watch the event loop run, genuinely worth 10 minutes)

### 7. Promises

**What it is:** an object standing in for a value that isn't ready yet. A receipt.

You order food, you get a buzzer. The buzzer isn't the food, but it tells you when the food is ready.

**Learn**

- The three states: pending, fulfilled, rejected
- `.then()`: "when it's ready, do this"
- `.catch()`: "if it fails, do this"
- `.finally()`: "either way, do this"
- Chaining: each `.then()` returns a new promise, so they stack
- `Promise.resolve()` and `Promise.reject()` for making them by hand
- The four combinators:
    - `Promise.all`: all must succeed; **rejects immediately if any one fails, and you lose the successful results**
    - `Promise.allSettled`: waits for everything, reports each one individually
    - `Promise.race`: first to finish, success or failure
    - `Promise.any`: first to *succeed*

**Prove it**

```javascript
// 1. Write sleep(ms): a promise that resolves after ms milliseconds
//    sleep(1000).then(() => console.log("done"));

// 2. Predict this. What exactly prints?
const p1 = Promise.resolve(1);
const p2 = Promise.reject('nope');
const p3 = Promise.resolve(3);

Promise.all([p1, p2, p3])
  .then(r => console.log('ok', r))
  .catch(e => console.log('err', e));

// 3. Rewrite it so you get results for the ones that worked AND the one that failed
```

**Where:** [javascript.info: Promises](https://javascript.info/promise-basics)

### 8. async / await

**What it is:** nicer syntax on top of promises. Nothing new underneath.

**Learn**

- `async` on a function means it **always returns a promise**, no matter what you write inside
- `await` pauses inside that function until a promise settles
- `await` only works inside an `async` function (or at the top level of a module)
- Sequential vs parallel. Doing these in the wrong order is one of the most common real-world performance bugs.

    ```javascript
    const a = await slow();   // waits 2s
    const b = await slow();   // then another 2s = 4s total

    const [a, b] = await Promise.all([slow(), slow()]);  // 2s total
    ```

- Converting a `.then()` chain into `async/await` and back

**Prove it**

```javascript
// 1. Write fetchUser(id) using async/await, wrapped in try/catch

// 2. Take this and rewrite it with async/await:
getUser(1)
  .then(user => getPosts(user.id))
  .then(posts => console.log(posts))
  .catch(err => console.error(err));

// 3. Given three slow API calls that don't depend on each other,
//    write the version that finishes in 2s, not 6s
```

**Where:** [javascript.info: async/await](https://javascript.info/async-await)

### 9. Errors in async code

**What it is:** why your `try/catch` sometimes catches nothing.

This one causes silent production bugs. Worth real attention.

**Learn**

- An `async` function that throws does **not** throw right away. It returns a **rejected promise**.
- So a plain `try/catch` around an un-awaited async call catches nothing:

    ```javascript
    try {
      getData();          // no await: the error escapes
    } catch (e) {
      console.log('never runs');
    }
    ```

- Two correct fixes: `await` it inside the `try`, or attach `.catch()` to it
- Unhandled promise rejections: what the warning means and why it matters
- `try/catch/finally` inside `async` functions
- Error handling in `.then()` chains: where `.catch()` should sit

**Prove it**

```javascript
// Why does this print only "done"? Fix it two different ways.
async function getData() {
  throw new Error('boom');
}

try {
  getData();
} catch (e) {
  console.log('caught');
}

console.log('done');
```

**Where:** [javascript.info: Error handling with promises](https://javascript.info/promise-error-handling)

---

## Part 3: Everything else

### 10. The keyword `this`

**What it is:** what `this` points at, decided by **how a function is called**, not where it was written.

**Learn**

- `user.greet()`: `this` is `user`, because of the dot
- `const fn = user.greet; fn();`: `this` is lost. Detaching a method breaks it.
- Arrow functions don't get their own `this`; they use the surrounding one. This is why arrows are safer in callbacks.
- `bind`, `call`, `apply`
- Strict mode (which all your Next.js code runs in) makes `this` `undefined` instead of the global object

**Prove it**

```javascript
const user = {
  name: 'Pratham',
  greet() { return `Hi ${this.name}`; }
};

const fn = user.greet;

console.log(user.greet());   // ?
console.log(fn());           // ? and why
// Now fix fn so it works
```

**Where:** [javascript.info: Object methods, "this"](https://javascript.info/object-methods)

### 11. Array methods

**What it is:** the tools you'll use every single day in React.

**Learn**, and know which ones change the original array and which return a new one:

- `map`, `filter`, `find`, `findIndex`, `some`, `every`, `includes`
- `reduce`: the hard one. Worth an hour on its own.
- `sort` (**mutates!**), `reverse` (**mutates!**), `slice` vs `splice`
- `flat`, `flatMap`, `Object.keys` / `values` / `entries`
- Chaining them: `.filter().map().reduce()`

**Prove it**

```javascript
const transactions = [
  { category: 'food',      amount: 20 },
  { category: 'transport', amount: 5  },
  { category: 'food',      amount: 35 },
];

// 1. Total of all amounts                          → 60
// 2. Only food transactions                        → 2 items
// 3. Total per category, as an object              → { food: 55, transport: 5 }
// 4. Sorted by amount, highest first, without changing the original array
```

That's real Finance Tracker work. Do it by hand.

**Where:** [javascript.info: Array methods](https://javascript.info/array-methods)

### 12. TypeScript basics

**What it is:** JavaScript with labels saying what kind of thing each variable holds.

Only start this once topics 1 to 11 are solid. TypeScript on shaky JavaScript is twice as confusing.

**Learn**

- Basic types: `string`, `number`, `boolean`, `string[]`, `null`, `undefined`
- `type` vs `interface`: either is fine, pick one and be consistent
- Union types: `"loading" | "success" | "error"`
- Optional properties: `age?: number`
- Typing function parameters and return values
- Typing React props
- `any` (avoid) vs `unknown` (safer)
- Utility types: `Partial`, `Pick`, `Omit`, `Record`

**Prove it**

```typescript
// Type a Transaction object, then write a function that takes
// Transaction[] and returns a number, with everything typed
```

**Where:** [Total TypeScript: Beginner's Tutorial](https://www.totaltypescript.com/tutorials) (free, interactive)

---

## Habits that make this work

**Type every example.** Reading code creates the feeling of understanding without the substance. Typing it, and getting the error, creates the real thing.

**Predict before you run.** Every single time. Write down what you think prints, *then* run it. When you're wrong, you've found something real. When you skip this step, you learn almost nothing.

**Twenty minutes daily on your own code.** Open the Finance Tracker, pick a file, read it out loud and explain each line. Stop when you can't. That's the day's topic. Keep a file called `things-i-now-know.md` and add two sentences each time.

**No AI-written code while you're learning these.** AI can explain a concept or check your answer. It can't produce code you paste. The struggle is the mechanism, not an obstacle to it.

**Small and daily beats big and occasional.** One hour a day for three weeks moves you further than seven hours every Saturday.

## Practice Questions

This is the checkpoint quiz. Take it when you finish topic 11: no running the code, no AI. Write your answer *and* your reasoning before opening each answer.

Scoring: 8/8 means the async and closure material is genuinely yours and you can move to React with confidence. 6 to 7 means review the ones you missed. Below 6 means go back to the topic, not the quiz.

??? question "1. Hoisting: what does this print?"

    ```javascript
    console.log(a);
    console.log(b);
    var a = 1;
    let b = 2;
    ```

    **Answer:** `undefined`, then a `ReferenceError`, and the script dies there. `var a` is hoisted and set to `undefined`. `let b` is hoisted but unusable until its line runs (the Temporal Dead Zone).

??? question "2. Scope and timers: what does this print?"

    ```javascript
    for (var i = 0; i < 3; i++) setTimeout(() => console.log(i), 0);
    for (let j = 0; j < 3; j++) setTimeout(() => console.log(j), 0);
    ```

    **Answer:** `3 3 3`, then `0 1 2`. `var` is function scoped, so all three callbacks share one `i`, which is 3 by the time they run. `let` creates a fresh `j` for each iteration.

??? question "3. Event loop: what is the output order?"

    ```javascript
    console.log('A');
    setTimeout(() => console.log('B'), 0);
    Promise.resolve().then(() => console.log('C'));
    console.log('D');
    ```

    **Answer:** `A D C B`. Normal code runs first, then promises (microtasks), then timers (macrotasks).

??? question "4. Reference vs value: what does this print?"

    ```javascript
    const a2 = { count: 1 };
    const b2 = a2;
    b2.count = 2;
    console.log(a2.count);
    console.log([1,2] === [1,2]);
    ```

    **Answer:** `2`, then `false`. `a2` and `b2` are two labels on one object. `===` on objects checks whether they are literally the same object in memory, not whether the contents match.

??? question "5. this: what does this print?"

    ```javascript
    const user = { name: 'P', greet() { return `Hi ${this.name}`; } };
    const fn = user.greet;
    console.log(user.greet());
    console.log(fn());
    ```

    **Answer:** `Hi P`, then a `TypeError` in strict mode or modules. `this` is decided by how the function is called: with the dot it is `user`, but the detached `fn()` has lost it (it is `undefined` in strict mode).

??? question "6. Errors in async code: why does this print only done?"

    ```javascript
    async function getData() { throw new Error('boom'); }
    try { getData(); } catch (e) { console.log('caught'); }
    console.log('done');
    ```

    **Answer:** `done` only, plus an unhandled rejection warning. An `async` function that throws returns a rejected promise instead of throwing right away, so the `try/catch` catches nothing. Fix it by `await`ing inside the `try`, or by attaching `.catch()`.

??? question "7. Promise.all: what prints?"

    ```javascript
    Promise.all([Promise.resolve(1), Promise.reject('nope'), Promise.resolve(3)])
      .then(r => console.log('ok', r))
      .catch(e => console.log('err', e));
    ```

    **Answer:** `err nope`, and that's all. `Promise.all` rejects immediately if any one promise fails, and you lose the successful results. Use `Promise.allSettled` to get each result.

??? question "8. Closures: what does this print?"

    ```javascript
    function makeCounter() {
      let count = 0;
      return { increment: () => ++count, get: () => count };
    }
    const c1 = makeCounter(), c2 = makeCounter();
    c1.increment(); c1.increment(); c2.increment();
    console.log(c1.get(), c2.get());
    ```

    **Answer:** `2 1`. Each call to `makeCounter` makes a fresh `count`, so `c1` and `c2` have separate backpacks.
