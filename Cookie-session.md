# Cookie-Session

## What is Cookie-Session?

`cookie-session` is Express middleware used to manage user sessions using cookies.

In simple words, it stores session information inside a cookie in the user's browser.

It helps maintain user login information across multiple requests.

## 1. Install Cookie-Session

```bash
npm install cookie-session
```

## 2. Import Cookie-Session

```javascript
const express = require('express');
const cookieSession = require('cookie-session');

const app = express();

app.use(cookieSession({
    name: 'session',
    keys: ['my-secret-key'],
    maxAge: 24 * 60 * 60 * 1000
}));
```

## 3. Create a Session

```javascript
app.post('/login', (req, res) => {
    req.session.user = {
        name: 'John',
        email: 'john@gmail.com'
    };

    res.send('Login successful');
});
```

**Purpose:** Stores user session information in a signed cookie after login.

## 4. Access Session Data

```javascript
app.get('/profile', (req, res) => {
    if (!req.session.user) {
        return res.send('Please login first');
    }

    res.json(req.session.user);
});
```

**Purpose:** Retrieves session information to identify the logged-in user.

## 5. Destroy a Session (Logout)

```javascript
app.post('/logout', (req, res) => {
    req.session = null;

    res.send('Logout successful');
});
```

**Purpose:** Removes the session cookie when the user logs out.

## 6. Where Do We Use Cookie-Session?

- **Login:** Maintain user login information.
- **Logout:** Clear user session information.
- **User Authentication:** Identify logged-in users.
- **Shopping Cart:** Maintain temporary shopping cart information.
- **User Preferences:** Store small amounts of session-related information.

## 7. How Does Cookie-Session Work?

1. User logs into the application.
2. Backend creates session information.
3. Session information is stored in a signed cookie.
4. Browser sends the cookie with subsequent requests.
5. Backend reads the cookie and identifies the session.

## Conclusion

Cookie-Session is used to maintain user sessions using browser cookies without requiring a separate server-side session store.

**Important:**
- Cookie-session signs cookies but does not encrypt their contents.
- Do not store passwords or sensitive information inside session cookies.
- Use HTTPS and secure cookie settings in production.
- Keep the signing keys secret and use strong, randomly generated keys.