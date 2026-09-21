---
title: Events
---

# Events

## What is `e.stopPropagation()`?

It is a method used to prevent an event from "bubbling up" from a child element to its parent elements. In React (and the DOM), events normally propagate from the element that was clicked through all ancestor elements' handlers. This is called **event bubbling**.

```javascript
export default function Example() {
  return (
    <div
      onClick={() => alert("Parent clicked!")}
      style={{ padding: 20, background: "#eee" }}
    >
      <button
        onClick={e => {
          e.stopPropagation();
          alert("Button clicked!");
        }}
      >
        Click me!
      </button>
    </div>
  );
}
```

**What happens when you click the button?**

- The button's alert shows ("Button clicked!").
- The parent's alert ("Parent clicked!") does **not** show, because of `e.stopPropagation()`.

**What if you click the gray background (not the button)?**

- Only the parent's alert shows ("Parent clicked!").

## Practice Questions

??? question "1. What is event bubbling?"

    Events normally propagate from the element that was clicked up through all its ancestor elements' handlers.

??? question "2. What does e.stopPropagation() do?"

    It stops the event from bubbling up from a child element to its parent elements.

??? question "3. In the example, which alerts show when you click the button, and which when you click the gray background?"

    Clicking the button shows only "Button clicked!", because `stopPropagation()` prevents the parent's handler from running. Clicking the gray background (not the button) shows only "Parent clicked!".
