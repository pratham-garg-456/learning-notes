---
title: HTTPS Redirect Middleware
---

# HTTPS Redirect Middleware

## The import

```python
from starlette.middleware.httpsredirect import HTTPSRedirectMiddleware
```

This line imports a special middleware called `HTTPSRedirectMiddleware` from Starlette.

## The middleware addition

```python
app.add_middleware(HTTPSRedirectMiddleware)
```

This line tells your app: "Whenever someone visits my website using HTTP, automatically redirect them to the HTTPS version."

## Why is this important?

- **HTTPS** is the secure version of HTTP. It encrypts all data sent between the user and your server, which protects sensitive information like passwords and personal info.
- **Redirecting to HTTPS** ensures all users always use the secure, encrypted connection.

## In simple terms

> This code makes sure that everyone who visits your website is forced to use the secure, encrypted version (HTTPS), even if they try to use the insecure version (HTTP).

## Visual example

- The user goes to `http://yourwebsite.com`.
- The middleware redirects them to `https://yourwebsite.com` (notice the "s").

See also [SSL, TLS, mTLS](../../chapter-4/ssl-tls-mtls.md).

## Practice Questions

??? question "1. What does HTTPSRedirectMiddleware do?"

    It automatically redirects anyone who visits the site over HTTP to the HTTPS version.

??? question "2. How do you add it to a FastAPI app?"

    Import it with `from starlette.middleware.httpsredirect import HTTPSRedirectMiddleware` and call `app.add_middleware(HTTPSRedirectMiddleware)`.

??? question "3. Why is redirecting to HTTPS important?"

    HTTPS encrypts all data between the user and your server, protecting sensitive information like passwords and personal details. Redirecting makes sure every user uses the encrypted connection.
