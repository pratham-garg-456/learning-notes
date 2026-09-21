---
title: React
---

# React

## What is React?

- React is an open source JavaScript library for building user interfaces.
- It is not a framework, although it is sometimes referred to as a frontend JavaScript framework. It was created by Facebook.
- It focuses on the UI: it is a tool for building interactive UI components.

### React is declarative

Tell React what you want, and React builds the actual UI.

## How does React work?

- **React creates a virtual DOM in memory.** Instead of manipulating the browser's DOM directly, React creates a virtual DOM in memory, where it does all the necessary manipulating, before making the changes in the browser DOM.
- **React only changes what needs to be changed.** React finds out what changes have been made, and changes only what needs to be changed.

## Rendering user interfaces (UI)

To understand how React works, we first need a basic understanding of how browsers interpret your code to create (render) user interfaces.

When a user visits a web page, the server returns an HTML file to the browser. The browser then reads the HTML and constructs the Document Object Model (DOM).

### What is the DOM?

The DOM is an object representation of the HTML elements. It acts as a bridge between your code and the user interface, and has a tree-like structure with parent and child relationships.

You can use DOM methods and JavaScript to listen to user events and [manipulate the DOM](https://developer.mozilla.org/docs/Learn/JavaScript/Client-side_web_APIs/Manipulating_documents) by selecting, adding, updating, and deleting specific elements in the user interface. DOM manipulation lets you target specific elements and change their style and content.

React is used to build single-page applications. Single page means the website stays on the same page and only the components change as needed. We don't need to reload the page: we just render the component we need and the rest stays the same.

**Component:** a small, reusable piece of code that represents a piece of user interface, for example a navigation bar or a footer.

## Prerequisite: Emmet in VS Code

Go to the VS Code settings, search for `emmet include lang`, and add a mapping so Emmet works in plain `.js` files.

??? note "Why?"

    When you're in a `.js` file, you can then use Emmet abbreviations that support JSX syntax, like `div.container>h1+p`, which expands to:

    ```javascript
    <div className="container">
      <h1></h1>
      <p></p>
    </div>
    ```

    Notice it uses `className` instead of `class` (the React/JSX convention).

    Common mappings:

    ```json
    {
      "vue-html": "html",              // Enable HTML Emmet in Vue templates
      "javascript": "javascriptreact", // Enable JSX Emmet in .js files
      "typescript": "typescriptreact", // Enable JSX Emmet in .ts files
      "django-html": "html"            // Enable HTML Emmet in Django templates
    }
    ```

    **Without this setting**, Emmet shortcuts wouldn't work in plain `.js` files when writing JSX/React code; you'd only get them in `.jsx` files.

## Topics

- [JSX](jsx.md)
- [Components](components.md)
- [Events](events.md)

## Practice Questions

??? question "1. Is React a framework?"

    No. It is an open source JavaScript library for building user interfaces, focused on the UI. It is sometimes called a frontend framework, but it is a library.

??? question "2. What does it mean that React is declarative?"

    You tell React what you want the UI to look like, and React builds the actual UI, instead of you writing step-by-step instructions to change it.

??? question "3. What is the virtual DOM, and why does React use it?"

    An in-memory copy of the DOM. React does its manipulating there, works out what changed, and then updates only what needs to be changed in the browser DOM, instead of manipulating the browser DOM directly.

??? question "4. What is the DOM?"

    An object representation of the HTML elements with a tree-like structure of parent and child relationships. It is the bridge between your code and the user interface.

??? question "5. What does single-page application mean?"

    The website stays on the same page and only the needed components change. There is no page reload: React renders the component that is needed and everything else stays the same.

??? question "6. What is a component?"

    A small, reusable piece of code that represents a piece of the user interface, such as a navigation bar or footer.
