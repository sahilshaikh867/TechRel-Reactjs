# API Integration Lab — 06 Third-Party API Integration

## What is a third-party API?
A service operated by another organization that your application consumes.

Examples:
- GitHub
- Google Maps
- Stripe
- Razorpay
- OpenWeather
- Firebase
- Cloudinary
- Twilio

## GitHub public API example
```js
export async function getGithubUser(username) {
  const response = await fetch(
    `https://api.github.com/users/${username}`
  );

  if (!response.ok) {
    throw new Error(`GitHub API error: ${response.status}`);
  }

  return response.json();
}
```

## Display the result
```jsx
<img src={user.avatar_url} alt={user.login} width="100" />
<h2>{user.name || user.login}</h2>
<p>Public repositories: {user.public_repos}</p>
<p>Followers: {user.followers}</p>
```

## Integration checklist
Before integrating any third-party API, read its documentation and identify:
1. Base URL
2. Endpoint
3. HTTP method
4. Required parameters
5. Authentication
6. Headers
7. Request body
8. Response schema
9. Error codes
10. Rate limits
11. CORS rules
12. Pricing/terms

## Authentication
A provider may use an API key, Bearer token, Basic auth or OAuth 2.0.

## Critical security rule
If a secret must remain private:

```text
React → Your Backend → Third-Party API
```

Do not expose the private secret in browser JavaScript.
