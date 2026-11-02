# API Integration Lab — 03 First GET API

## Goal
Fetch users and display them in React.

## `src/services/api.js`
```js
const BASE_URL = "https://jsonplaceholder.typicode.com";

export async function getUsers() {
  const response = await fetch(`${BASE_URL}/users`);

  if (!response.ok) {
    throw new Error(`HTTP error: ${response.status}`);
  }

  return response.json();
}
```

## `src/components/UserList.jsx`
```jsx
import { useEffect, useState } from "react";
import { getUsers } from "../services/api";

export default function UserList() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState("");

  useEffect(() => {
    async function loadUsers() {
      try {
        const data = await getUsers();
        setUsers(data);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    }

    loadUsers();
  }, []);

  if (loading) return <p>Loading users...</p>;
  if (error) return <p>Error: {error}</p>;

  return (
    <div>
      <h2>Users</h2>
      {users.map((user) => (
        <article key={user.id}>
          <h3>{user.name}</h3>
          <p>{user.email}</p>
        </article>
      ))}
    </div>
  );
}
```

## `App.jsx`
```jsx
import UserList from "./components/UserList";

export default function App() {
  return (
    <main>
      <h1>API Integration App</h1>
      <UserList />
    </main>
  );
}
```

## Browser debugging
Open DevTools → Network → Fetch/XHR and inspect the request, status, headers and response.
