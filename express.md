# Node.js Express Libraries

## 1. Express

### What is Express?

Express.js is a Node.js web framework used to build web applications and REST APIs.

It simplifies handling HTTP requests, responses, routing, and middleware.

### Installation

```bash
npm install express
```

### Import Express

```javascript
const express = require('express');

const app = express();
```

### Basic Example

```javascript
const express = require('express');

const app = express();

app.use(express.json());

app.get('/users', (req, res) => {
    res.json({
        message: 'Users fetched successfully'
    });
});

app.post('/users', (req, res) => {
    const user = req.body;

    res.json({
        message: 'User created successfully',
        data: user
    });
});

app.listen(5000, () => {
    console.log('Server running on port 5000');
});
```

**Purpose:** Creates a backend server and handles client requests.

### Where Do We Use Express?

- **API Development:** Create REST APIs.
- **Routing:** Handle GET, POST, PUT, PATCH, and DELETE requests.
- **Middleware:** Process requests before sending responses.
- **Authentication:** Handle login and registration APIs.
- **Database Integration:** Connect backend APIs with MongoDB or SQL databases.

---

## 2. Express-Async-Errors

### What is Express-Async-Errors?

`express-async-errors` is a package used to handle errors automatically in asynchronous Express route handlers.

Normally, in Express 4, asynchronous errors need to be passed to `next()` manually.

This package helps forward rejected promises to Express error-handling middleware.

### Installation

```bash
npm install express-async-errors
```

### Import Express-Async-Errors

```javascript
require('express-async-errors');
```

**Note:** Import it before registering your routes.

### Example

```javascript
require('express-async-errors');

const express = require('express');

const app = express();

app.get('/users', async (req, res) => {

    const users = await getUsersFromDatabase();

    res.json(users);

});

app.use((err, req, res, next) => {

    console.log(err.message);

    res.status(500).json({
        message: 'Internal Server Error'
    });

});

app.listen(5000);
```

**Purpose:** Automatically forwards rejected promises from async route handlers to error-handling middleware in Express 4.

### Where Do We Use Express-Async-Errors?

- **Database Operations:** Handle database query errors.
- **API Requests:** Handle errors in asynchronous API operations.
- **Authentication:** Handle errors during login and registration.
- **File Operations:** Handle asynchronous file processing errors.
- **Error Handling:** Avoid writing `try-catch` blocks in every route handler.

**Important:**
- This package is mainly used with Express 4.
- Express 5 automatically forwards rejected promises from async route handlers, so this package is generally unnecessary with Express 5.

---

## 3. Express-Validator

### What is Express-Validator?

`express-validator` is an Express middleware library used to validate and sanitize incoming request data.

In simple words, it checks whether the data sent by the frontend is valid before processing it in the backend.

### Installation

```bash
npm install express-validator
```

### Import Express-Validator

```javascript
const {
    body,
    validationResult
} = require('express-validator');
```

### Example: Validate User Registration

```javascript
const express = require('express');

const {
    body,
    validationResult
} = require('express-validator');

const app = express();

app.use(express.json());

app.post(
    '/register',

    [
        body('name')
            .notEmpty()
            .withMessage('Name is required'),

        body('email')
            .isEmail()
            .withMessage('Enter a valid email'),

        body('password')
            .isLength({ min: 6 })
            .withMessage('Password must contain at least 6 characters')
    ],

    (req, res) => {

        const errors = validationResult(req);

        if (!errors.isEmpty()) {
            return res.status(400).json({
                errors: errors.array()
            });
        }

        res.json({
            message: 'Registration successful',
            data: req.body
        });

    }
);

app.listen(5000);
```

**Purpose:** Validates user input before saving or processing data.

### Common Validation Methods

| Method | Purpose |
|---|---|
| `notEmpty()` | Checks whether a field is empty |
| `isEmail()` | Checks email format |
| `isLength()` | Checks string length |
| `isNumeric()` | Checks numeric values |
| `isInt()` | Checks integer values |
| `isString()` | Checks string values |
| `isBoolean()` | Checks boolean values |
| `isStrongPassword()` | Checks password strength |
| `isMobilePhone()` | Checks phone number format |
| `trim()` | Removes leading and trailing spaces |
| `normalizeEmail()` | Normalizes email addresses |

### Where Do We Use Express-Validator?

- **Registration:** Validate name, email, and password.
- **Login:** Validate email and password fields.
- **Forms:** Validate submitted form data.
- **API Requests:** Check incoming request parameters.
- **Data Sanitization:** Clean and normalize user input.

---

## 4. Difference Between These Libraries

| Library | Main Purpose |
|---|---|
| Express | Build backend servers and APIs |
| Express-Async-Errors | Handle asynchronous errors |
| Express-Validator | Validate and sanitize incoming data |

## Conclusion

These three libraries are commonly used in Node.js backend development.

1. **Express:** Handles requests, responses, routing, and middleware.
2. **Express-Async-Errors:** Handles rejected promises in Express 4 async routes.
3. **Express-Validator:** Validates and sanitizes incoming user data.

Together, they help build structured, reliable, and maintainable backend applications.