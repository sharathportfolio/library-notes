# Prop-Types

## What is Prop-Types?

`prop-types` is a React package used to validate the data types of props passed from one component to another.

In simple words, it helps ensure that a component receives the correct type of data, such as String, Number, Boolean, Array, or Object.

## 1. Install Prop-Types

```bash
npm install prop-types
```

## 2. Import Prop-Types

```javascript
import PropTypes from 'prop-types';
```

## 3. Basic Example

```javascript
import React from 'react';
import PropTypes from 'prop-types';

function User(props) {
    return (
        <div>
            <h2>{props.name}</h2>
            <p>{props.age}</p>
        </div>
    );
}

User.propTypes = {
    name: PropTypes.string,
    age: PropTypes.number
};

export default User;
```

**Purpose:** Validates that `name` is a string and `age` is a number.

## 4. Pass Props to a Component

```javascript
import User from './User';

function App() {
    return (
        <User name="John" age={25} />
    );
}

export default App;
```

**Purpose:** Passes data from the parent component to the child component.

## 5. Common PropTypes

| PropTypes | Data Type |
|---|---|
| `PropTypes.string` | String |
| `PropTypes.number` | Number |
| `PropTypes.bool` | Boolean |
| `PropTypes.array` | Array |
| `PropTypes.object` | Object |
| `PropTypes.func` | Function |
| `PropTypes.node` | React-renderable content |
| `PropTypes.element` | React element |

## 6. Required Props

We can use `.isRequired` to make a prop mandatory.

```javascript
User.propTypes = {
    name: PropTypes.string.isRequired,
    age: PropTypes.number.isRequired
};
```

**Purpose:** Displays a warning in development if a required prop is missing or has an invalid type.

## 7. Where Do We Use Prop-Types?

- **Component Validation:** Check the data types passed to components.
- **Parent to Child:** Validate props passed between components.
- **Error Prevention:** Identify incorrect prop types during development.
- **Code Maintenance:** Make component requirements easier to understand.
- **Reusable Components:** Ensure components receive expected data.

## Conclusion

Prop-Types is used in React applications to validate props and identify incorrect data types passed between components.

**Important:**
- PropTypes provides runtime warnings in development.
- It does not automatically convert incorrect data types.
- It is not a replacement for TypeScript.
- Modern React projects may use TypeScript for static type checking instead.