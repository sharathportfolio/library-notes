# React and React Packages

React is a JavaScript library for building user interfaces. It allows developers to create reusable UI components and build interactive web applications.

## 1. `react`

`react` is the core React library. It provides components, hooks, context, and other tools for building user interfaces.

### Installation

```bash
npm install react
```

### Import

```javascript
import React from "react";
```

Import individual hooks:

```javascript
import { useState, useEffect, useRef } from "react";
```

### Example: Component

```jsx
function App() {
  return <h1>Hello React!</h1>;
}

export default App;
```

### Common React Features

| Feature | Purpose |
|---|---|
| Components | Build reusable UI elements |
| JSX | Write HTML-like syntax in JavaScript |
| Props | Pass data between components |
| State | Manage component data |
| Hooks | Use React features in function components |
| Context | Share data across components |
| Custom Hooks | Reuse stateful logic |

### Common Hooks

```javascript
useState()
useEffect()
useContext()
useRef()
useMemo()
useCallback()
useReducer()
useId()
```

---

## 2. `react-dom`

`react-dom` provides methods for rendering React components into the browser DOM.

### Installation

```bash
npm install react-dom
```

### Common Import

```javascript
import { createPortal } from "react-dom";
```

### Example: Portal

Render a component outside its normal DOM parent.

```jsx
import { createPortal } from "react-dom";

function Modal() {
  return createPortal(
    <div className="modal">
      <h2>Hello Modal!</h2>
    </div>,
    document.body
  );
}

export default Modal;
```

### Common Methods

| Method | Purpose |
|---|---|
| `createPortal()` | Render children into another DOM node |
| `flushSync()` | Force React to flush updates synchronously |

**Note:** `react-dom` also contains legacy APIs such as `render()` and `hydrate()`. Modern applications should use the APIs from `react-dom/client`.

---

## 3. `react-dom/client`

`react-dom/client` provides APIs to create and manage the root of a React application.

It is commonly used in React 18 and later.

### Import

```javascript
import { createRoot } from "react-dom/client";
```

### Example: Render React Application

```jsx
import React from "react";
import { createRoot } from "react-dom/client";
import App from "./App";

const rootElement = document.getElementById("root");

const root = createRoot(rootElement);

root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

### Common Methods

| Method | Purpose |
|---|---|
| `createRoot()` | Create a React root for client rendering |
| `hydrateRoot()` | Attach React to existing server-rendered HTML |

### Example: Hydration

```jsx
import { hydrateRoot } from "react-dom/client";
import App from "./App";

hydrateRoot(
  document.getElementById("root"),
  <App />
);
```

**Note:** Use `hydrateRoot()` when the HTML was already rendered on the server. Use `createRoot()` for normal client-side rendering.

---

## 4. `react-scripts`

`react-scripts` is the package used by Create React App (CRA) to run development, build, test, and eject commands.

### Installation

```bash
npm install react-scripts
```

### Common Commands

Start the development server:

```bash
npm start
```

Create a production build:

```bash
npm run build
```

Run tests:

```bash
npm test
```

Eject configuration:

```bash
npm run eject
```

### Example: package.json

```json
{
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  }
}
```

### Commands Explained

| Command | Purpose |
|---|---|
| `start` | Run the development server |
| `build` | Generate production files |
| `test` | Run tests |
| `eject` | Expose the underlying build configuration |

**Note:** Create React App is deprecated for new projects. Existing CRA applications can still use `react-scripts`, but consider Vite or a React framework for new applications.

---

## 5. `react-stripe-checkout`

`react-stripe-checkout` is a React component library that provides a Stripe Checkout button for older Stripe token-based integrations.

### Installation

```bash
npm install react-stripe-checkout
```

### Import

```javascript
import StripeCheckout from "react-stripe-checkout";
```

### Example: Stripe Payment Button

```jsx
import StripeCheckout from "react-stripe-checkout";

function Payment() {
  const handleToken = async (token) => {
    console.log("Stripe token:", token);

    // Send the token to your backend.
    // Your backend should process the payment securely.
  };

  return (
    <StripeCheckout
      name="My Store"
      description="Product Payment"
      amount={1000}
      currency="USD"
      stripeKey="YOUR_PUBLISHABLE_KEY"
      token={handleToken}
    >
      <button>Pay Now</button>
    </StripeCheckout>
  );
}

export default Payment;
```

### Common Props

| Prop | Purpose |
|---|---|
| `stripeKey` | Stripe publishable key |
| `token` | Callback receiving the Stripe token |
| `amount` | Payment amount in the smallest currency unit |
| `currency` | Payment currency |
| `name` | Store or business name |
| `description` | Payment description |
| `email` | Customer email |
| `children` | Custom payment button |

### Important Security Notes

- Never expose Stripe secret keys in frontend code.
- Process payments on your backend.
- Validate payment amounts on the server.
- Use Stripe's current recommended Checkout or Payment Intents integration for new projects.

**Note:** `react-stripe-checkout` is an older integration and is not the recommended approach for new Stripe applications. Consider Stripe Checkout Sessions or Payment Intents with Stripe's maintained libraries.

---

## 6. Quick Comparison

| Package | Main Purpose |
|---|---|
| `react` | Build UI components |
| `react-dom` | Browser DOM integration |
| `react-dom/client` | Create and hydrate React roots |
| `react-scripts` | CRA development and build tools |
| `react-stripe-checkout` | Legacy Stripe payment button |

## 7. Typical React Project Structure

```text
my-react-app/
│
├── public/
│   └── index.html
│
├── src/
│   ├── components/
│   │   └── Header.jsx
│   │
│   ├── App.jsx
│   └── index.js
│
├── package.json
└── README.md
```

## 8. Important Notes

- `react` contains the core React functionality.
- `react-dom` connects React to the browser DOM.
- `react-dom/client` provides modern rendering and hydration APIs.
- `react-scripts` is associated with Create React App.
- `react-stripe-checkout` is an older Stripe integration.
- Keep `react` and `react-dom` on compatible versions.

## Official Documentation

- React: https://react.dev/
- React DOM: https://react.dev/reference/react-dom
- React DOM Client: https://react.dev/reference/react-dom/client
- Create React App: https://create-react-app.dev/
- Stripe: https://docs.stripe.com/