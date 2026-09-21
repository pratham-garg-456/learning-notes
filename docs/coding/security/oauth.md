---
title: OAuth
---

# OAuth

See also [OAuth 2.0 and OpenID Connect (OIDC)](../../chapter-4/oauth-2-0-and-openid-connect-oidc.md) in the System Design notes.

## How social login works

1. **User initiates login.** The user tries to access an application that requires authentication.
2. **Authorization request.** The application redirects the user to an authorization server, asking for permission to access their data.
3. **User grants permission.** The user logs in and approves the requested permissions.
4. **Authorization code issued.** The authorization server redirects the user back to the application with an authorization code.
5. **Token exchange.** The application sends the authorization code to the authorization server to request an access token.
6. **Access token received.** The authorization server validates the code and returns an access token.
7. **Access token used.** The application uses the token to access protected resources on behalf of the user.
8. **Token expiry and refresh.** When the token expires, the application can request a new one using a refresh token.

## Steps to set up

- Go to the [Google developer console](https://console.cloud.google.com/).
- Create a new project.
- Go to APIs and Services.
- Open the OAuth consent screen.
- Then follow the steps.
- For GitHub: go to GitHub, Settings, Developer settings, and follow the steps.

Local development values used:

- `http://127.0.0.1:8000` is the URL origin.
- `http://127.0.0.1:8000/auth/callback` is the redirect (callback) URL.
- `http://127.0.0.1:8000/login` is the application homepage URL (for GitHub).

## Practice Questions

??? question "1. Walk through the steps of social login with OAuth."

    The user tries to log in, the app redirects them to the authorization server, the user logs in and grants permission, the server redirects back with an authorization code, the app exchanges the code for an access token, and the app uses the token to access protected resources on the user's behalf.

??? question "2. What is the authorization code used for?"

    The application sends it to the authorization server to request an access token. The server validates the code and returns the token.

??? question "3. What happens when an access token expires?"

    The application can request a new one using a refresh token.

??? question "4. What three URLs do you configure for local development?"

    The URL origin (`http://127.0.0.1:8000`), the redirect or callback URL (`http://127.0.0.1:8000/auth/callback`), and, for GitHub, the application homepage URL (`http://127.0.0.1:8000/login`).
