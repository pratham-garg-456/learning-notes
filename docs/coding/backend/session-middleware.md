---
title: Session Middleware
---

# Session Middleware

### **In Even Simpler Terms**

- **Session middleware** is like giving every visitor a tiny notebook (the session).
- Your app writes things in that notebook for each user (like their name).
- When the user comes back, you can check their notebook and remember who they are.

---

### **Key Points**

- Requires a `secret_key` for security (so no one can fake the session).
- Stores data in the user’s browser (safe, but keep it small).
- Use `request.session` like a Python dictionary to save and read info.

---

### **When Not To Use**

- Don’t store big or sensitive data in sessions.
- For a lot of or sensitive data, use something like a database or Redis.

## Practice Questions

??? question "1. What is session middleware, in simple terms?"

    It gives every visitor a tiny notebook (the session). Your app writes things in it (like their name) and can read it when the user comes back.

??? question "2. What does session middleware require, and how do you use it?"

    A `secret_key` so nobody can fake the session. Use `request.session` like a Python dictionary to save and read information.

??? question "3. When should you not use sessions?"

    Don't store big or sensitive data in them. Use a database or Redis for large or sensitive data.
