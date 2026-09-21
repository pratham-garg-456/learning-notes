---
title: JSON
---

# JSON

## Serialization

Converting a JavaScript object into JSON so it can be transferred over the internet.

```javascript
const jsonData = JSON.stringify(data);

const data = JSON.parse(jsonData);
```

`JSON.stringify` turns an object into a JSON string, and `JSON.parse` turns a JSON string back into an object.

## Practice Questions

??? question "1. What is serialization?"

    Converting a JavaScript object into JSON so it can be transferred over the internet.

??? question "2. Which two functions convert between an object and JSON?"

    `JSON.stringify(data)` converts an object into JSON, and `JSON.parse(jsonData)` converts JSON back into an object.
