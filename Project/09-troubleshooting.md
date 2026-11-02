# API Integration Lab — 09 Troubleshooting

## CORS
CORS is enforced by browsers for cross-origin requests. The API server must permit your origin, or you should use a backend/proxy architecture.

## 401 Unauthorized
Check token/API key and Authorization header.

## 403 Forbidden
The server understood the request but refuses it.

## 404 Not Found
Check URL, endpoint, ID and API version.

## 429 Too Many Requests
You likely exceeded the provider's rate limit. Respect the documented limits.

## 500 Server Error
Usually a server-side problem. Your frontend should still show a useful error.

## React infinite request loop
Avoid:
```jsx
useEffect(() => {
  loadUsers();
}, [users]);
```

Typical initial-load pattern:
```jsx
useEffect(() => {
  loadUsers();
}, []);
```

## Important Fetch behavior
`fetch()` does not automatically reject for HTTP 404/500. Check:
```js
if (!response.ok) {
  throw new Error(`HTTP error: ${response.status}`);
}
```

## Network debugging
F12 → Network → Fetch/XHR → select request → inspect Headers, Payload, Response and Status.
