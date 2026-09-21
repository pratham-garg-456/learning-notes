---
title: NextAuth.js Client API
---

# NextAuth.js Client API

Reference: https://next-auth.js.org/getting-started/client

## Session

Example Session object:

```jsx
{
  user: {
    name: string
    email: string
    image: string
  },
  expires: Date // This is the expiry of the session, not any of the tokens within the session
}
```

!!! tip

    To customize the [session object](https://next-auth.js.org/configuration/callbacks#session-callback) session callback can be used

    Example:

    ```jsx
    ...
    callbacks: {
      async session({ session, token, user }) {
        // Send properties to the client, like an access_token and user id from a provider.
        session.accessToken = token.accessToken
        session.user.id = token.id

        return session
      }
    }
    ...
    ```

## useSession()

The `useSession()` React Hook in the NextAuth.js client is the easiest way to check if someone is signed in.

`useSession()` returns an object containing two values: `data` and `status`:

- **`data`**: This can be three values: [**`Session`**](https://github.com/nextauthjs/next-auth/blob/8ff4b260143458c5d8a16b80b11d1b93baa0690f/types/index.d.ts#L437-L444) / `undefined` / `null`.
    - when the session hasn't been fetched yet, `data` will be `undefined`
    - in case it failed to retrieve the session, `data` will be `null`
    - in case of success, `data` will be [**`Session`**](https://github.com/nextauthjs/next-auth/blob/8ff4b260143458c5d8a16b80b11d1b93baa0690f/types/index.d.ts#L437-L444).
- **`status`**: enum mapping to three possible session states: `"loading" | "authenticated" | "unauthenticated"`

!!! tip

    Make sure that [**`<SessionProvider>`**](https://next-auth.js.org/getting-started/client#sessionprovider) is added to `pages/_app.js`

## Practice Questions

??? question "1. What does a NextAuth session object contain?"

    A `user` (name, email, image) and `expires`, which is the expiry of the session, not of any tokens inside it.

??? question "2. How do you customize the session object?"

    Use the session callback, for example to add an access token or user id to the session.

??? question "3. What does useSession() return?"

    An object with `data` (undefined while loading, null on failure, or the Session on success) and `status` (`loading`, `authenticated`, or `unauthenticated`).

??? question "4. What must be set up for useSession to work?"

    A `SessionProvider` must be added, for example in `pages/_app.js`.
