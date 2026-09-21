---
title: JSX
---

# JSX

Take this page:

```html
<html>
  <body>
    <div id="app"></div>
    <script src="https://unpkg.com/react@18/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
    <script>
      const app = document.getElementById('app');
      const root = ReactDOM.createRoot(app);
      root.render(<h1>Develop. Preview. Ship.</h1>);
    </script>
  </body>
</html>
```

If you run this code in the browser, you get a syntax error:

```text
Uncaught SyntaxError: expected expression, got '<'
```

This is because `<h1>...</h1>` is not valid JavaScript. That piece of code is **JSX**.

## What is JSX?

JSX is a syntax extension for JavaScript that lets you describe your UI in a familiar *HTML-like* syntax. The nice thing about JSX is that apart from following [three JSX rules](https://react.dev/learn/writing-markup-with-jsx#the-rules-of-jsx), you don't need to learn any new symbols or syntax outside of HTML and JavaScript.

Browsers don't understand JSX out of the box, so you need a JavaScript compiler, such as [Babel](https://babeljs.io/), to transform your JSX into regular JavaScript.

## Adding Babel to your project

Copy this script into your `index.html`:

```html
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
```

You also need to tell Babel which code to transform by changing the script type to `type="text/jsx"`:

```html
<html>
  <body>
    <div id="app"></div>
    <script src="https://unpkg.com/react@18/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
    <!-- Babel Script -->
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script type="text/jsx">
      const domNode = document.getElementById('app');
      const root = ReactDOM.createRoot(domNode);
      root.render(<h1>Develop. Preview. Ship.</h1>);
    </script>
  </body>
</html>
```

## Practice Questions

??? question "1. Why does passing an h1 tag straight to root.render throw a syntax error in the browser?"

    Because `<h1>...</h1>` written inside JavaScript is not valid JavaScript. It is JSX, and browsers don't understand JSX out of the box.

??? question "2. What is JSX?"

    A syntax extension for JavaScript that lets you describe your UI in an HTML-like syntax. Beyond three JSX rules, you don't need to learn new symbols outside HTML and JavaScript.

??? question "3. What do you need to make JSX run in the browser, and how do you tell it what to transform?"

    A compiler such as Babel to transform JSX into regular JavaScript. Add the Babel script to the page and change the script type of your code to `text/jsx`.
