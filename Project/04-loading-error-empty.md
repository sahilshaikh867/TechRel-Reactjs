# API Integration Lab — 04 Loading, Error and Empty States

A production-quality UI should not only handle success.

## 1. Loading
```jsx
if (loading) return <p>Loading users...</p>;
```

## 2. Error
```jsx
if (error) {
  return (
    <section>
      <h2>Something went wrong</h2>
      <p>{error}</p>
    </section>
  );
}
```

## 3. Empty
```jsx
if (!loading && users.length === 0) {
  return <p>No users found.</p>;
}
```

## 4. Retry
Keep the request function available and connect it to:
```jsx
<button onClick={loadUsers}>Try again</button>
```

## Why?
Networks fail. APIs return 4xx/5xx responses. Users disconnect from Wi-Fi. Rate limits happen. Good UI handles failure deliberately.
