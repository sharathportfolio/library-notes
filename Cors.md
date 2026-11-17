# CORS

## What is CORS?

CORS stands for **Cross-Origin Resource Sharing**.

It is a security mechanism that allows or restricts requests from one origin (domain) to another origin.

In simple words, CORS controls which frontend applications can access your backend APIs.

## 1. Install CORS

```bash
npm install cors
```

## 2. Import CORS

```javascript
const express = require('express');
const cors = require('cors');

const app = express();

app.use(cors());
```

## 3. Allow a Specific Origin

```javascript
app.use(cors({
    origin: 'http://localhost:3000'
}));
```

**Purpose:** Allows only the frontend running at `http://localhost:3000` to access the backend.

## 4. Allow Multiple Origins

```javascript
app.use(cors({
    origin: [
        'http://localhost:3000',
        'http://localhost:5173'
    ]
}));
```

**Purpose:** Allows multiple frontend applications to access the backend.

## 5. Where Do We Use CORS?

- **React + Node.js:** Allow React frontend to access backend APIs.
- **Angular + Node.js:** Allow Angular frontend to communicate with backend.
- **Frontend and Backend:** Allow communication between different origins.
- **API Security:** Control which origins are allowed to access APIs.

## 6. Why Do We Use CORS?

For example:

- Frontend: `http://localhost:3000`
- Backend: `http://localhost:5000`

Since both run on different ports, they have different origins.

CORS allows the backend to specify whether the frontend is permitted to access its resources.

## Conclusion

CORS is used in Node.js applications to control cross-origin requests and allow authorized frontend applications to communicate with backend APIs.

**Important:** CORS is not authentication or complete API security. Always use proper authentication and authorization to protect backend APIs.