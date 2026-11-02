# API Integration Lab — 01 Project Setup

## Goal
Build a beginner-friendly React application from scratch and progressively connect it to APIs.

We will use:
- React + Vite
- JavaScript
- Browser Fetch API
- JSONPlaceholder REST API
- GitHub REST API as a third-party example
- Environment variables
- Loading, error and empty states
- GET, POST, PUT and DELETE

## 1. Install Node.js
Install the current LTS version.

Check:
```bash
node -v
npm -v
```

## 2. Create the React application
```bash
npm create vite@latest api-integration-app
cd api-integration-app
npm install
npm run dev
```

Choose React and JavaScript when Vite asks.

## 3. Recommended structure
```text
api-integration-app/
├── src/
│   ├── components/
│   │   ├── UserList.jsx
│   │   ├── UserCard.jsx
│   │   ├── CreateUserForm.jsx
│   │   └── GithubProfile.jsx
│   ├── services/
│   │   └── api.js
│   ├── App.jsx
│   ├── main.jsx
│   └── index.css
├── .env
├── .gitignore
└── package.json
```

## Important
Never put a private API secret in React source code. Browser code is delivered to the user.
