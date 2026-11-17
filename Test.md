# Node.js Testing Libraries

## 1. Supertest

### What is Supertest?

`supertest` is a Node.js library used to test HTTP requests and API endpoints.

In simple words, it helps us test backend APIs without manually opening Postman or a browser.

### Installation

```bash
npm install --save-dev supertest
```

### Import Supertest

```javascript
const request = require('supertest');
```

### Example: Test an API

**app.js**

```javascript
const express = require('express');

const app = express();

app.use(express.json());

app.get('/users', (req, res) => {
    res.status(200).json({
        message: 'Users fetched successfully'
    });
});

module.exports = app;
```

**app.test.js**

```javascript
const request = require('supertest');
const app = require('./app');

describe('GET /users', () => {

    it('should return users successfully', async () => {

        const response = await request(app)
            .get('/users');

        expect(response.status).toBe(200);

        expect(response.body.message)
            .toBe('Users fetched successfully');

    });

});
```

**Purpose:** Tests API endpoints by sending HTTP requests and checking their responses.

### Where Do We Use Supertest?

- **API Testing:** Test GET, POST, PUT, PATCH, and DELETE endpoints.
- **Status Code Testing:** Check whether APIs return correct status codes.
- **Response Testing:** Verify API response data.
- **Authentication Testing:** Test login and protected APIs.
- **Integration Testing:** Test how different backend components work together.

---

## 2. Jest

### What is Jest?

`jest` is a JavaScript testing framework used to test application code.

It helps developers write and execute automated tests to check whether their code works correctly.

### Installation

```bash
npm install --save-dev jest
```

### Import Jest

Jest provides testing functions such as:

- `describe()` – Groups related test cases.
- `it()` – Defines an individual test case.
- `test()` – Defines a test case.
- `expect()` – Checks the expected result.
- `beforeEach()` – Runs before every test.
- `afterEach()` – Runs after every test.

### Example: Basic Jest Test

**math.js**

```javascript
function add(a, b) {
    return a + b;
}

module.exports = add;
```

**math.test.js**

```javascript
const add = require('./math');

describe('Addition Test', () => {

    it('should add two numbers', () => {

        const result = add(10, 20);

        expect(result).toBe(30);

    });

});
```

### Run Jest

Add this script inside `package.json`:

```json
{
    "scripts": {
        "test": "jest"
    }
}
```

Run:

```bash
npm test
```

**Purpose:** Automatically tests JavaScript functions and application logic.

### Where Do We Use Jest?

- **Unit Testing:** Test individual functions.
- **Integration Testing:** Test multiple components together.
- **API Testing:** Test backend API functionality.
- **Mocking:** Mock database calls and external services.
- **Regression Testing:** Check whether existing functionality still works after code changes.

---

## 3. Ts-Jest

### What is Ts-Jest?

`ts-jest` is a Jest transformer used to run tests written in TypeScript.

It allows Jest to understand and execute TypeScript test files.

In simple words, Jest is commonly used for JavaScript testing, while ts-jest helps Jest work with TypeScript.

### Installation

```bash
npm install --save-dev jest ts-jest typescript @types/jest
```

### Configure Ts-Jest

Run:

```bash
npx ts-jest config:init
```

This generates a Jest configuration file.

Example configuration:

**jest.config.js**

```javascript
module.exports = {
    preset: 'ts-jest',
    testEnvironment: 'node'
};
```

### Example: TypeScript Test

**math.ts**

```typescript
function add(a: number, b: number): number {
    return a + b;
}

export default add;
```

**math.test.ts**

```typescript
import add from './math';

describe('Addition Test', () => {

    it('should add two numbers', () => {

        const result = add(10, 20);

        expect(result).toBe(30);

    });

});
```

### Run Ts-Jest

```bash
npx jest
```

**Purpose:** Runs Jest test cases written in TypeScript.

### Where Do We Use Ts-Jest?

- **TypeScript Projects:** Test TypeScript applications.
- **Unit Testing:** Test TypeScript functions.
- **API Testing:** Test TypeScript backend APIs.
- **Integration Testing:** Test multiple TypeScript modules.
- **TypeScript + Jest:** Execute TypeScript test files using Jest.

---

## 4. Difference Between These Libraries

| Library | Main Purpose |
|---|---|
| Supertest | Test HTTP requests and API endpoints |
| Jest | Run automated JavaScript tests |
| Ts-Jest | Run Jest tests written in TypeScript |

## 5. How Do They Work Together?

Example: Testing a Node.js + Express + TypeScript application.

1. **Jest:** Runs the test cases.
2. **Supertest:** Sends HTTP requests to the Express application.
3. **Ts-Jest:** Helps Jest execute TypeScript test files.

## Conclusion

These three libraries are commonly used in backend testing.

- **Supertest:** Tests API endpoints.
- **Jest:** Tests application logic.
- **Ts-Jest:** Supports TypeScript testing with Jest.

Together, they help developers build reliable applications through automated testing.

**Important:**
- Supertest does not replace Jest.
- Jest is a testing framework.
- Ts-Jest is a TypeScript transformer for Jest.
- Install testing libraries as development dependencies using `--save-dev`.