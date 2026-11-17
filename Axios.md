# Axios

Axios is a promise-based HTTP client for JavaScript. It is used to send HTTP requests from Node.js and browser applications, including React.

## 1. Installation

```bash
npm install axios
```

For Yarn:

```bash
yarn add axios
```

## 2. Import Axios

```javascript
import axios from "axios";
```

Or using CommonJS:

```javascript
const axios = require("axios");
```

## 3. Basic GET Request

Fetch data from an API.

```javascript
import axios from "axios";

axios.get("https://jsonplaceholder.typicode.com/users")
  .then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.error(error);
  });
```

Using async/await:

```javascript
const getUsers = async () => {
  try {
    const response = await axios.get(
      "https://jsonplaceholder.typicode.com/users"
    );

    console.log(response.data);
  } catch (error) {
    console.error(error);
  }
};

getUsers();
```

## 4. HTTP Methods

### GET

Retrieve data from a server.

```javascript
const response = await axios.get("/api/users");
console.log(response.data);
```

### POST

Send data to a server.

```javascript
const response = await axios.post("/api/users", {
  name: "John",
  email: "john@example.com"
});

console.log(response.data);
```

### PUT

Replace or update a resource.

```javascript
const response = await axios.put("/api/users/1", {
  name: "John Updated",
  email: "john@example.com"
});
```

### PATCH

Partially update a resource.

```javascript
const response = await axios.patch("/api/users/1", {
  name: "Updated Name"
});
```

### DELETE

Delete a resource.

```javascript
const response = await axios.delete("/api/users/1");
```

## 5. Query Parameters

Use the `params` option to send query parameters.

```javascript
const response = await axios.get("/api/users", {
  params: {
    page: 1,
    limit: 10,
    search: "john"
  }
});
```

Example URL:

```text
/api/users?page=1&limit=10&search=john
```

## 6. Request Headers

Send custom headers with a request.

```javascript
const response = await axios.get("/api/profile", {
  headers: {
    Authorization: "Bearer YOUR_TOKEN",
    "Content-Type": "application/json"
  }
});
```

## 7. Axios Instance

Create a reusable Axios instance with common configuration.

```javascript
import axios from "axios";

const api = axios.create({
  baseURL: "https://api.example.com",
  timeout: 10000,
  headers: {
    "Content-Type": "application/json"
  }
});

export default api;
```

Use the instance:

```javascript
import api from "./api";

const getUsers = async () => {
  const response = await api.get("/users");
  return response.data;
};
```

## 8. Error Handling

Handle API errors using `try...catch`.

```javascript
try {
  const response = await axios.get("/api/users");
  console.log(response.data);
} catch (error) {
  if (axios.isAxiosError(error)) {
    if (error.response) {
      console.log("Server error:", error.response.status);
      console.log(error.response.data);
    } else if (error.request) {
      console.log("No response received from server");
    } else {
      console.log("Request error:", error.message);
    }
  } else {
    console.log("Unexpected error:", error);
  }
}
```

## 9. Request Interceptors

Interceptors run before a request is sent. They are useful for adding authentication tokens.

```javascript
api.interceptors.request.use(
  (config) => {
    const token = localStorage.getItem("token");

    if (token) {
      config.headers.Authorization = `Bearer ${token}`;
    }

    return config;
  },
  (error) => Promise.reject(error)
);
```

## 10. Response Interceptors

Interceptors can process responses or handle common errors.

```javascript
api.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      console.log("Unauthorized access");
    }

    return Promise.reject(error);
  }
);
```

## 11. Upload Files

Use `FormData` to upload files.

```javascript
const uploadFile = async (file) => {
  const formData = new FormData();
  formData.append("file", file);

  const response = await axios.post("/api/upload", formData);

  return response.data;
};
```

## 12. Download Files

Use `responseType: "blob"` in browser applications.

```javascript
const downloadFile = async () => {
  const response = await axios.get("/api/download", {
    responseType: "blob"
  });

  const url = URL.createObjectURL(response.data);
  const link = document.createElement("a");

  link.href = url;
  link.download = "file.pdf";
  link.click();

  URL.revokeObjectURL(url);
};
```

## 13. Request Timeout

Set a timeout to limit how long Axios waits for a response.

```javascript
const response = await axios.get("/api/users", {
  timeout: 5000
});
```

## 14. Cancel Requests

Use `AbortController` to cancel an ongoing request.

```javascript
const controller = new AbortController();

try {
  const response = await axios.get("/api/users", {
    signal: controller.signal
  });

  console.log(response.data);
} catch (error) {
  if (axios.isCancel(error)) {
    console.log("Request cancelled");
  } else {
    console.error(error);
  }
}

// Cancel the request
controller.abort();
```

## 15. Axios Response Object

Axios responses contain useful properties.

```javascript
const response = await axios.get("/api/users");

console.log(response.data);       // Response body
console.log(response.status);     // HTTP status code
console.log(response.statusText); // HTTP status message
console.log(response.headers);    // Response headers
console.log(response.config);     // Request configuration
```

## 16. Common Axios Methods

| Method | Purpose |
|---|---|
| `axios.get()` | Retrieve data |
| `axios.post()` | Create or submit data |
| `axios.put()` | Replace a resource |
| `axios.patch()` | Partially update a resource |
| `axios.delete()` | Delete a resource |
| `axios.create()` | Create a reusable instance |
| `axios.all()` | Work with multiple promises |
| `axios.isAxiosError()` | Check whether an error is an Axios error |

## 17. Axios with React

Example using `useEffect` and `useState`.

```jsx
import { useEffect, useState } from "react";
import axios from "axios";

function Users() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState("");

  useEffect(() => {
    const controller = new AbortController();

    const fetchUsers = async () => {
      try {
        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/users",
          { signal: controller.signal }
        );

        setUsers(response.data);
      } catch (err) {
        if (!controller.signal.aborted) {
          setError("Failed to fetch users");
        }
      } finally {
        if (!controller.signal.aborted) {
          setLoading(false);
        }
      }
    };

    fetchUsers();

    return () => controller.abort();
  }, []);

  if (loading) return <p>Loading...</p>;
  if (error) return <p>{error}</p>;

  return (
    <div>
      <h2>User List</h2>

      {users.map((user) => (
        <p key={user.id}>{user.name}</p>
      ))}
    </div>
  );
}

export default Users;
```

## 18. Important Notes

- Axios supports promises and async/await.
- Use `response.data` to access the response body.
- Use `axios.create()` for reusable API configurations.
- Use interceptors for common request and response handling.
- Use `AbortController` to cancel requests.
- Never expose private API keys or secrets in frontend code.
- Validate server responses and handle errors properly.

## Official Documentation

https://axios-http.com/