# JSON Web Token (JWT)

## What is JWT?

JWT stands for **JSON Web Token**.

`jsonwebtoken` is an npm package used to generate, sign, verify, and decode JSON Web Tokens.

In simple words, JWT is used for user authentication. After login, the backend generates a token and sends it to the frontend. The frontend sends this token with future requests to access protected APIs.

## 1. Install JSON Web Token

```bash
npm install jsonwebtoken
```

## 2. Import JSON Web Token

```javascript
const jwt = require('jsonwebtoken');
```

## 3. Generate a JWT Token

```javascript
const jwt = require('jsonwebtoken');

const user = {
    id: 101,
    name: 'John',
    email: 'john@gmail.com'
};

const token = jwt.sign(
    user,
    'my-secret-key',
    { expiresIn: '1h' }
);

console.log(token);
```

**Purpose:** Generates a token containing user information after successful login.

## 4. Verify a JWT Token

```javascript
const jwt = require('jsonwebtoken');

const token = 'your-generated-token';

try {
    const decoded = jwt.verify(token, 'my-secret-key');

    console.log(decoded);
} catch (error) {
    console.log('Invalid or expired token');
}
```

**Purpose:** Checks whether the token is valid and has not expired.

## 5. Decode a JWT Token

```javascript
const jwt = require('jsonwebtoken');

const token = 'your-generated-token';

const decoded = jwt.decode(token);

console.log(decoded);
```

**Purpose:** Reads the token payload without verifying its signature.

**Note:** Decoding does not prove that the token is valid.

## 6. Where Do We Use JWT?

- **Login:** Generate a token after successful authentication.
- **Authentication:** Identify authenticated users.
- **Protected APIs:** Allow authorized users to access specific routes.
- **Authorization:** Check user roles and permissions.
- **Frontend and Backend:** Secure communication between applications.

## 7. How Does JWT Work?

1. User enters email and password.
2. Backend verifies the login credentials.
3. Backend generates a JWT token.
4. Frontend receives and stores the token securely.
5. Frontend sends the token with future API requests.
6. Backend verifies the token before providing protected resources.

## 8. Example: JWT Authentication Middleware

```javascript
const jwt = require('jsonwebtoken');

const verifyToken = (req, res, next) => {
    const token = req.headers.authorization?.split(' ')[1];

    if (!token) {
        return res.status(401).json({
            message: 'Token required'
        });
    }

    try {
        const decoded = jwt.verify(token, process.env.JWT_SECRET);

        req.user = decoded;

        next();
    } catch (error) {
        return res.status(401).json({
            message: 'Invalid or expired token'
        });
    }
};
```

Usage:

```javascript
app.get('/profile', verifyToken, (req, res) => {
    res.json({
        message: 'Welcome to your profile',
        user: req.user
    });
});
```

## Conclusion

JSON Web Token is used to authenticate users and protect backend APIs without maintaining a traditional server-side session for every user.

**Important:**
- Keep the JWT secret key confidential.
- Use environment variables to store secret keys.
- Always verify tokens before accessing protected APIs.
- Set token expiration using `expiresIn`.
- JWT payloads are encoded, not encrypted. Never store passwords or sensitive secrets inside them.
- Use HTTPS in production.