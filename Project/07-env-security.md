# API Integration Lab — 07 Environment Variables and Security

## Vite environment variable
Create `.env`:
```env
VITE_PUBLIC_API_URL=https://example.com/api
```

Use:
```js
const url = import.meta.env.VITE_PUBLIC_API_URL;
```

## Important security fact
Vite variables beginning with `VITE_` are available to client-side code. They are configuration, not a secure vault.

Never store these as frontend secrets:
- database passwords
- AWS secret access keys
- payment secret keys
- private signing keys
- private tokens

## Backend pattern
```text
Browser
  ↓
React
  ↓
Your Backend
  ↓  private Authorization header
Third-Party API
```

## `.gitignore`
```gitignore
.env
.env.local
.env.*.local
```

Even with `.gitignore`, never commit a secret that has already been exposed. Rotate/revoke it immediately.
