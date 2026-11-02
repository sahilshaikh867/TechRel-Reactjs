# API Integration Lab — 05 POST, PUT and DELETE

JSONPlaceholder simulates write operations; changes are not permanently stored.

## POST
```js
export async function createUser(user) {
  const response = await fetch(
    "https://jsonplaceholder.typicode.com/users",
    {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(user),
    }
  );

  if (!response.ok) {
    throw new Error(`HTTP error: ${response.status}`);
  }

  return response.json();
}
```

## PUT
```js
export async function updateUser(id, user) {
  const response = await fetch(
    `https://jsonplaceholder.typicode.com/users/${id}`,
    {
      method: "PUT",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(user),
    }
  );

  if (!response.ok) {
    throw new Error(`HTTP error: ${response.status}`);
  }

  return response.json();
}
```

## DELETE
```js
export async function deleteUser(id) {
  const response = await fetch(
    `https://jsonplaceholder.typicode.com/users/${id}`,
    { method: "DELETE" }
  );

  if (!response.ok) {
    throw new Error(`HTTP error: ${response.status}`);
  }
}
```

## Key idea
POST/PUT/PATCH normally send JSON in the request body. The server responds with JSON or a status code.
