# React.js – Hooks

## What is React.js?

React.js is a JavaScript library used to build interactive user interfaces (UI), especially single-page applications.

React allows developers to create reusable UI components and manage application data efficiently.

## 1. What are React Hooks?

React Hooks are built-in functions that allow functional components to use React features such as state, lifecycle-related effects, context, and references.

**Purpose:** Manage component data, handle side effects, reuse logic, and improve application performance.

## 2. useState()

### What is useState?

`useState()` is a React Hook used to create and manage state inside functional components.

When the state changes, React re-renders the component.

### Example

```jsx
import React, { useState } from 'react';

function Counter() {
    const [count, setCount] = useState(0);

    return (
        <div>
            <h2>Count: {count}</h2>

            <button onClick={() => setCount(count + 1)}>
                Increment
            </button>
        </div>
    );
}

export default Counter;
```

**Purpose:** Store and update component data.

### Where Do We Use useState?

- Login forms
- Registration forms
- Counter applications
- Show / Hide passwords
- Toggle buttons
- Shopping cart quantities
- Dropdown menus

---

## 3. useEffect()

### What is useEffect?

`useEffect()` is a React Hook used to perform side effects in functional components.

Side effects include API calls, event listeners, timers, and subscriptions.

### Example

```jsx
import React, { useEffect, useState } from 'react';

function Users() {
    const [users, setUsers] = useState([]);

    useEffect(() => {
        fetch('https://jsonplaceholder.typicode.com/users')
            .then(response => response.json())
            .then(data => setUsers(data));
    }, []);

    return (
        <div>
            {users.map(user => (
                <p key={user.id}>{user.name}</p>
            ))}
        </div>
    );
}

export default Users;
```

### useEffect Dependency Types

**1. Without dependency array**

```jsx
useEffect(() => {
    console.log('Runs after every render');
});
```

**2. Empty dependency array**

```jsx
useEffect(() => {
    console.log('Runs after initial mount');
}, []);
```

**3. With dependency**

```jsx
useEffect(() => {
    console.log('Count changed');
}, [count]);
```

**Purpose:** Handle side effects and synchronize components with external systems.

### Where Do We Use useEffect?

- API calls
- Event listeners
- Timers and intervals
- Updating document titles
- WebSocket connections
- Subscriptions
- Browser event handling

---

# 4. Other Important React Hooks

## 4.1 useContext()

### What is useContext?

`useContext()` is used to access shared data from React Context without passing props through multiple component levels.

### Example

```jsx
import React, { createContext, useContext } from 'react';

const UserContext = createContext();

function Profile() {
    const user = useContext(UserContext);

    return <h2>Welcome {user}</h2>;
}

function App() {
    return (
        <UserContext.Provider value="John">
            <Profile />
        </UserContext.Provider>
    );
}

export default App;
```

**Purpose:** Share data between components without prop drilling.

**Where do we use it?**
- Authentication
- User information
- Theme management
- Language settings
- Global application data

## 4.2 useRef()

### What is useRef?

`useRef()` is used to store a mutable value that does not cause a component re-render when updated.

It can also be used to access DOM elements directly.

### Example

```jsx
import React, { useRef } from 'react';

function App() {
    const inputRef = useRef(null);

    const handleClick = () => {
        inputRef.current.focus();
    };

    return (
        <div>
            <input ref={inputRef} />

            <button onClick={handleClick}>
                Focus Input
            </button>
        </div>
    );
}

export default App;
```

**Purpose:** Access DOM elements and store values without triggering re-renders.

**Where do we use it?**
- Focus input fields
- Store timer IDs
- Access DOM elements
- Store previous values
- Manage third-party DOM integrations

## 4.3 useMemo()

### What is useMemo?

`useMemo()` is used to cache the result of an expensive calculation between renders.

### Example

```jsx
import React, { useMemo, useState } from 'react';

function App() {
    const [number, setNumber] = useState(1);

    const result = useMemo(() => {
        console.log('Calculating...');

        return number * 10;
    }, [number]);

    return (
        <div>
            <h2>Result: {result}</h2>

            <button onClick={() => setNumber(number + 1)}>
                Increase
            </button>
        </div>
    );
}

export default App;
```

**Purpose:** Avoid unnecessary recalculation of expensive values.

**Where do we use it?**
- Large data calculations
- Filtering lists
- Sorting data
- Complex calculations
- Performance optimization

## 4.4 useCallback()

### What is useCallback?

`useCallback()` is used to cache a function between renders until its dependencies change.

### Example

```jsx
import React, { useCallback, useState } from 'react';

function App() {
    const [count, setCount] = useState(0);

    const handleClick = useCallback(() => {
        console.log('Button clicked');
    }, []);

    return (
        <div>
            <h2>{count}</h2>

            <button onClick={() => setCount(count + 1)}>
                Increase
            </button>

            <button onClick={handleClick}>
                Click Me
            </button>
        </div>
    );
}

export default App;
```

**Purpose:** Cache functions to avoid unnecessary function recreation, especially when passing callbacks to memoized child components.

**Where do we use it?**
- Passing functions to child components
- Optimizing memoized components
- Avoiding unnecessary effect re-execution
- Expensive callback logic

## 4.5 useReducer()

### What is useReducer?

`useReducer()` is used to manage complex component state using a reducer function.

It is an alternative to `useState()` when state logic becomes complex.

### Example

```jsx
import React, { useReducer } from 'react';

function reducer(state, action) {
    switch (action.type) {
        case 'increment':
            return { count: state.count + 1 };

        case 'decrement':
            return { count: state.count - 1 };

        default:
            return state;
    }
}

function App() {
    const [state, dispatch] = useReducer(reducer, {
        count: 0
    });

    return (
        <div>
            <h2>{state.count}</h2>

            <button onClick={() => dispatch({ type: 'increment' })}>
                Increment
            </button>

            <button onClick={() => dispatch({ type: 'decrement' })}>
                Decrement
            </button>
        </div>
    );
}

export default App;
```

**Purpose:** Manage complex state updates using actions and reducers.

**Where do we use it?**
- Shopping cart
- Multi-step forms
- Complex form state
- Multiple related state values
- Application state management

## 4.6 useLayoutEffect()

### What is useLayoutEffect?

`useLayoutEffect()` works similarly to `useEffect()`, but it runs after DOM updates and before the browser paints the screen.

### Example

```jsx
import React, { useLayoutEffect, useRef } from 'react';

function App() {
    const boxRef = useRef(null);

    useLayoutEffect(() => {
        const height = boxRef.current.offsetHeight;

        console.log('Height:', height);
    }, []);

    return (
        <div ref={boxRef}>
            Hello React
        </div>
    );
}

export default App;
```

**Purpose:** Measure or adjust DOM elements before the browser displays the updated screen.

**Where do we use it?**
- Measuring element dimensions
- Tooltip positioning
- Modal positioning
- Preventing visual layout flickering

## 4.7 useImperativeHandle()

### What is useImperativeHandle?

`useImperativeHandle()` is used to customize the values or methods exposed through a component reference.

### Example

```jsx
import React, {
    useRef,
    useImperativeHandle,
    forwardRef
} from 'react';

const Input = forwardRef((props, ref) => {
    const inputRef = useRef(null);

    useImperativeHandle(ref, () => ({
        focus() {
            inputRef.current.focus();
        }
    }));

    return <input ref={inputRef} />;
});

function App() {
    const inputRef = useRef(null);

    return (
        <>
            <Input ref={inputRef} />

            <button onClick={() => inputRef.current.focus()}>
                Focus
            </button>
        </>
    );
}

export default App;
```

**Purpose:** Expose selected methods from child components to parent components.

**Where do we use it?**
- Custom input components
- Focus management
- Video player controls
- Reusable UI components

## 4.8 useId()

### What is useId?

`useId()` generates unique IDs that can be used to connect HTML elements and accessibility attributes.

### Example

```jsx
import React, { useId } from 'react';

function App() {
    const id = useId();

    return (
        <div>
            <label htmlFor={id}>Email</label>

            <input id={id} type="email" />
        </div>
    );
}

export default App;
```

**Purpose:** Generate unique IDs for accessibility and form elements.

**Where do we use it?**
- Form labels
- Input fields
- Accessibility attributes
- Reusable components

## 4.9 useTransition()

### What is useTransition?

`useTransition()` is used to mark certain state updates as non-urgent so React can keep the interface responsive.

### Example

```jsx
import React, { useState, useTransition } from 'react';

function App() {
    const [isPending, startTransition] = useTransition();
    const [tab, setTab] = useState('home');

    function changeTab() {
        startTransition(() => {
            setTab('profile');
        });
    }

    return (
        <div>
            <button onClick={changeTab}>
                Change Tab
            </button>

            {isPending && <p>Loading...</p>}

            <h2>{tab}</h2>
        </div>
    );
}

export default App;
```

**Purpose:** Keep the UI responsive during non-urgent state updates.

**Where do we use it?**
- Tab navigation
- Large list rendering
- Search results
- Heavy UI updates

## 4.10 useDeferredValue()

### What is useDeferredValue?

`useDeferredValue()` allows a value to update at a lower priority so that urgent UI updates remain responsive.

### Example

```jsx
import React, { useState, useDeferredValue } from 'react';

function App() {
    const [search, setSearch] = useState('');

    const deferredSearch = useDeferredValue(search);

    return (
        <div>
            <input
                value={search}
                onChange={(e) => setSearch(e.target.value)}
                placeholder="Search..."
            />

            <h2>Search: {deferredSearch}</h2>
        </div>
    );
}

export default App;
```

**Purpose:** Prevent slow UI updates from blocking urgent user interactions.

**Where do we use it?**
- Search applications
- Large filtered lists
- Heavy rendering
- Live search suggestions

## 4.11 useDebugValue()

### What is useDebugValue?

`useDebugValue()` is used to display debugging information for custom Hooks in React Developer Tools.

### Example

```jsx
import { useDebugValue, useState } from 'react';

function useOnlineStatus() {
    const [isOnline] = useState(true);

    useDebugValue(isOnline ? 'Online' : 'Offline');

    return isOnline;
}
```

**Purpose:** Display useful debugging information for custom Hooks.

**Where do we use it?**
- Custom Hooks
- Debugging reusable logic
- React Developer Tools

## 4.12 useSyncExternalStore()

### What is useSyncExternalStore?

`useSyncExternalStore()` is used to subscribe to external stores and read their data consistently in React.

### Example

```jsx
import { useSyncExternalStore } from 'react';

function subscribe(callback) {
    window.addEventListener('online', callback);
    window.addEventListener('offline', callback);

    return () => {
        window.removeEventListener('online', callback);
        window.removeEventListener('offline', callback);
    };
}

function getSnapshot() {
    return navigator.onLine;
}

function App() {
    const isOnline = useSyncExternalStore(
        subscribe,
        getSnapshot
    );

    return (
        <h2>{isOnline ? 'Online' : 'Offline'}</h2>
    );
}

export default App;
```

**Purpose:** Connect React components to external data stores.

**Where do we use it?**
- External state management
- Browser online status
- External subscriptions
- Third-party state stores

## 4.13 useInsertionEffect()

### What is useInsertionEffect?

`useInsertionEffect()` is a specialized Hook used mainly by CSS-in-JS libraries to insert styles before layout effects run.

### Example

```jsx
import { useInsertionEffect } from 'react';

function App() {
    useInsertionEffect(() => {
        const style = document.createElement('style');

        style.textContent = `
            .title {
                color: blue;
            }
        `;

        document.head.appendChild(style);

        return () => {
            style.remove();
        };
    }, []);

    return <h1 className="title">Hello React</h1>;
}
```

**Purpose:** Insert styles before layout effects execute.

**Where do we use it?**
- CSS-in-JS libraries
- Dynamic style insertion
- Styling library integrations

**Note:** Most application developers do not need this Hook directly.

## 4.14 useActionState()

### What is useActionState?

`useActionState()` is a React Hook used to manage the state and result of an action, commonly a form submission.

### Example

```jsx
import React, { useActionState } from 'react';

async function submitForm(previousState, formData) {
    const name = formData.get('name');

    return `Welcome ${name}`;
}

function App() {
    const [message, formAction, isPending] = useActionState(
        submitForm,
        ''
    );

    return (
        <form action={formAction}>
            <input name="name" placeholder="Enter name" />

            <button disabled={isPending}>
                Submit
            </button>

            <p>{message}</p>
        </form>
    );
}

export default App;
```

**Purpose:** Manage form action results, pending state, and returned state.

**Where do we use it?**
- Registration forms
- Login forms
- Form submissions
- Server Actions
- Form validation responses

## 4.15 useOptimistic()

### What is useOptimistic?

`useOptimistic()` is used to update the UI immediately while an asynchronous operation is still processing.

### Example

```jsx
import React, { useOptimistic, useState } from 'react';

function App() {
    const [likes, setLikes] = useState(0);

    const [optimisticLikes, addOptimisticLike] =
        useOptimistic(likes, (state, newLike) => state + newLike);

    async function handleLike() {
        addOptimisticLike(1);

        await new Promise(resolve => setTimeout(resolve, 1000));

        setLikes(previous => previous + 1);
    }

    return (
        <div>
            <h2>Likes: {optimisticLikes}</h2>

            <button onClick={handleLike}>
                Like
            </button>
        </div>
    );
}

export default App;
```

**Purpose:** Show immediate UI updates before the server operation finishes.

**Where do we use it?**
- Like buttons
- Comments
- Chat applications
- Shopping carts
- Form submissions

## 4.16 use()

### What is use()?

`use()` is a React API used to read resources such as Promises and Context inside components.

Unlike regular Hooks, `use()` can be called inside conditions and loops, but it must not be called inside a try-catch block.

### Example

```jsx
import React, { use } from 'react';

function User({ userPromise }) {
    const user = use(userPromise);

    return <h2>{user.name}</h2>;
}

export default User;
```

**Purpose:** Read Promise results and Context values in React components.

**Where do we use it?**
- Reading asynchronous data
- Working with Promises
- Accessing Context
- Suspense-based rendering

**Note:** A component using a Promise with `use()` should be rendered within an appropriate Suspense boundary.

## 4.17 useEffectEvent()

### What is useEffectEvent?

`useEffectEvent()` is a React 19.2 Hook used to separate non-reactive event logic from an Effect.

It allows Effect Event functions to read the latest props and state without making those values dependencies of the Effect.

### Example

```jsx
import { useEffect, useEffectEvent } from 'react';

function App({ theme }) {
    const onConnected = useEffectEvent(() => {
        console.log('Current theme:', theme);
    });

    useEffect(() => {
        const connection = connectToServer();

        connection.on('connected', onConnected);

        return () => connection.disconnect();
    }, []);

    return <h2>Chat Application</h2>;
}
```

**Purpose:** Read the latest values inside Effect-related event logic without unnecessarily re-synchronizing the Effect.

**Where do we use it?**
- Event callbacks inside Effects
- WebSocket connections
- Event listeners
- Timer callbacks

**Note:** Available in React 19.2 and later. Effect Events should only be called from Effects or other Effect Events.

---

# 5. React DOM Hooks

React DOM also provides additional Hooks for working with forms.

## 5.1 useFormStatus()

### What is useFormStatus?

`useFormStatus()` is a React DOM Hook used to access the status of the nearest parent form.

### Example

```jsx
import { useFormStatus } from 'react-dom';

function SubmitButton() {
    const { pending } = useFormStatus();

    return (
        <button disabled={pending}>
            {pending ? 'Submitting...' : 'Submit'}
        </button>
    );
}
```

**Purpose:** Track whether a form is currently submitting.

**Where do we use it?**
- Form submission
- Loading buttons
- Disable buttons during submission
- Display pending status

**Note:** It must be used inside a component rendered within the form.

---

# 6. Custom Hooks

### What are Custom Hooks?

Custom Hooks are JavaScript functions that allow developers to reuse stateful React logic between multiple components.

A custom Hook name must start with `use`.

### Example

```jsx
import { useState } from 'react';

function useCounter() {
    const [count, setCount] = useState(0);

    const increment = () => {
        setCount(previous => previous + 1);
    };

    return {
        count,
        increment
    };
}

function App() {
    const { count, increment } = useCounter();

    return (
        <div>
            <h2>{count}</h2>

            <button onClick={increment}>
                Increment
            </button>
        </div>
    );
}

export default App;
```

**Purpose:** Reuse component logic without duplicating code.

**Where do we use it?**
- API calls
- Authentication logic
- Form handling
- Window resize handling
- Online/offline status
- Reusable state logic

---

# 7. React Hooks Summary

| Hook | Main Purpose |
|---|---|
| `useState()` | Manage component state |
| `useEffect()` | Handle side effects |
| `useContext()` | Access shared context |
| `useRef()` | Store mutable values and access DOM |
| `useMemo()` | Cache calculated values |
| `useCallback()` | Cache functions |
| `useReducer()` | Manage complex state |
| `useLayoutEffect()` | Run effects before browser paint |
| `useImperativeHandle()` | Customize exposed ref methods |
| `useId()` | Generate unique IDs |
| `useTransition()` | Manage non-urgent updates |
| `useDeferredValue()` | Defer less urgent values |
| `useDebugValue()` | Debug custom Hooks |
| `useSyncExternalStore()` | Subscribe to external stores |
| `useInsertionEffect()` | Insert styles before layout effects |
| `useActionState()` | Manage action and form state |
| `useOptimistic()` | Show optimistic UI updates |
| `use()` | Read Promises and Context |
| `useEffectEvent()` | Separate non-reactive Effect logic |
| `useFormStatus()` | Track parent form submission status |
| Custom Hooks | Reuse stateful logic |

---

# 8. When Should We Use Which Hook?

| Requirement | Hook |
|---|---|
| Store user input | `useState` |
| Fetch API data | `useEffect` |
| Share user information | `useContext` |
| Focus an input | `useRef` |
| Optimize calculations | `useMemo` |
| Optimize callback functions | `useCallback` |
| Manage complex state | `useReducer` |
| Measure DOM elements | `useLayoutEffect` |
| Control child component methods | `useImperativeHandle` |
| Generate unique IDs | `useId` |
| Handle non-urgent updates | `useTransition` |
| Improve search responsiveness | `useDeferredValue` |
| Debug custom Hooks | `useDebugValue` |
| Subscribe to external stores | `useSyncExternalStore` |
| Insert dynamic styles | `useInsertionEffect` |
| Handle form actions | `useActionState` |
| Update UI immediately | `useOptimistic` |
| Read Promises or Context | `use` |
| Handle Effect event logic | `useEffectEvent` |
| Track form submission | `useFormStatus` |
| Reuse component logic | Custom Hooks |

---

# 9. Rules of React Hooks

1. Call Hooks only at the top level of React function components or custom Hooks.
2. Do not call regular Hooks inside loops, conditions, or nested functions.
3. Always use the `use` prefix when creating custom Hooks.
4. Do not call Hooks inside regular JavaScript functions.
5. Follow the dependency rules for `useEffect`, `useMemo`, and `useCallback`.
6. Do not directly modify state. Use the state setter function.
7. Do not use `useEffect` for every operation; use it only when synchronizing with external systems.

**Special Note:** React's `use()` API has different calling rules and can be used inside conditions and loops.

---

# 10. Conclusion

React Hooks help developers build interactive and reusable components without using class components.

The most commonly used Hooks in real-world React applications are:

1. `useState` – State management.
2. `useEffect` – API calls and side effects.
3. `useContext` – Global data sharing.
4. `useRef` – DOM access.
5. `useMemo` – Performance optimization.
6. `useCallback` – Function optimization.
7. `useReducer` – Complex state management.
8. Custom Hooks – Reusable logic.

**Important:** Not every Hook is required in every application. Choose Hooks based on the actual requirement.