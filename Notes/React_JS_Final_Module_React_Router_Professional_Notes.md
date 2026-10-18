# React JS — Final Module: React Router

> **Module:** React Router  
> **Level:** Beginner → Intermediate → Practical  
> **Status:** Final React Routing Module  
> **Last Updated:** October 2026  
> **Recommended Setup:** React + Vite + React Router DOM

---

## Table of Contents

1. [What is React Router?](#1-what-is-react-router)
2. [Why Do We Need Routing?](#2-why-do-we-need-routing)
3. [Client-Side Routing](#3-client-side-routing)
4. [How React Router Works](#4-how-react-router-works)
5. [Types of Routers](#5-types-of-routers)
6. [BrowserRouter](#6-browserrouter)
7. [HashRouter](#7-hashrouter)
8. [MemoryRouter](#8-memoryrouter)
9. [StaticRouter and NativeRouter](#9-staticrouter-and-nativerouter)
10. [Main React Router Components](#10-main-react-router-components)
11. [Creating a React Router Project](#11-creating-a-react-router-project)
12. [Project Structure](#12-project-structure)
13. [Basic Routing](#13-basic-routing)
14. [Link](#14-link)
15. [NavLink](#15-navlink)
16. [Route Parameters](#16-route-parameters)
17. [useParams](#17-useparams)
18. [Query Parameters](#18-query-parameters)
19. [useSearchParams](#19-usesearchparams)
20. [Programmatic Navigation](#20-programmatic-navigation)
21. [useNavigate](#21-usenavigate)
22. [Nested Routes](#22-nested-routes)
23. [Outlet](#23-outlet)
24. [404 / Not Found Route](#24-404--not-found-route)
25. [Navigation State](#25-navigation-state)
26. [Protected Routes](#26-protected-routes)
27. [BrowserRouter vs HashRouter vs MemoryRouter](#27-browserrouter-vs-hashrouter-vs-memoryrouter)
28. [Real-World Industry Use Cases](#28-real-world-industry-use-cases)
29. [Common Mistakes](#29-common-mistakes)
30. [Final Practical Lab](#30-final-practical-lab)
31. [Student Practice Tasks](#31-student-practice-tasks)
32. [Interview Questions](#32-interview-questions)
33. [Quick Revision](#33-quick-revision)
34. [Final React Learning Roadmap](#34-final-react-learning-roadmap)

---

# 1. What is React Router?

**React Router** is a declarative, component-based routing library used to manage navigation in React applications.

A normal website may have URLs such as:

```text
/
 /about
 /contact
 /products
 /products/101
 /login
 /dashboard
```

React Router connects these URLs to React components.

For example:

```text
URL                         Component

/                           Home
/about                      About
/contact                    Contact
/products                   Products
/products/101               ProductDetails
/login                      Login
/dashboard                  Dashboard
```

### Simple Definition

> React Router allows a React application to display different components based on the current URL without performing a full browser page reload.

---

# 2. Why Do We Need Routing?

Imagine an e-commerce application.

It may contain:

```text
Home
Products
Product Details
Cart
Checkout
Login
Profile
Orders
About
Contact
```

Without routing, managing all these views manually becomes difficult.

Routing gives every important view its own URL.

Example:

```text
myshop.com/
myshop.com/products
myshop.com/products/101
myshop.com/cart
myshop.com/checkout
myshop.com/profile
```

This provides:

- Better navigation
- Bookmarkable URLs
- Browser Back/Forward support
- Deep linking
- Organized application structure
- Dynamic pages
- Nested application sections
- Better user experience

---

# 3. Client-Side Routing

React applications commonly behave as **Single Page Applications (SPAs)**.

In client-side routing:

```text
User clicks link
      ↓
URL changes
      ↓
React Router detects URL
      ↓
Matching Route is found
      ↓
Required component renders
      ↓
Full page reload is avoided
```

### Traditional Website

```text
Click About
    ↓
Browser sends request
    ↓
Server
    ↓
New HTML document
    ↓
Page reload
```

### React SPA

```text
Click About
    ↓
React Router
    ↓
URL changes
    ↓
About component renders
    ↓
No full document reload
```

> Client-side routing does not mean that the server is never involved. Initial application loading and direct URL requests still require appropriate server configuration, especially with `BrowserRouter`.

---

# 4. How React Router Works

A simplified routing architecture:

```text
                 Browser URL
                     │
                     ▼
             React Router
                     │
          ┌──────────┼──────────┐
          ▼          ▼          ▼
        "/"       "/about"   "/contact"
          │          │          │
          ▼          ▼          ▼
        Home       About      Contact
```

React Router matches the current location against your route definitions.

Example:

```jsx
<Routes>
  <Route path="/" element={<Home />} />
  <Route path="/about" element={<About />} />
  <Route path="/contact" element={<Contact />} />
</Routes>
```

---

# 5. Types of Routers

Common React Router types include:

1. `BrowserRouter`
2. `HashRouter`
3. `MemoryRouter`
4. `StaticRouter`
5. `NativeRouter`

For normal React web applications, the most important ones to understand first are:

```text
BrowserRouter
HashRouter
MemoryRouter
```

---

# 6. BrowserRouter

`BrowserRouter` is the most commonly used router for modern React web applications.

It uses the browser's History API to keep the UI synchronized with the URL.

Example:

```text
https://example.com/about
https://example.com/products
https://example.com/contact
```

No `#` is required.

### Basic Syntax

```jsx
import { BrowserRouter } from "react-router-dom";

function App() {
  return (
    <BrowserRouter>
      {/* Application routes */}
    </BrowserRouter>
  );
}

export default App;
```

### History API

BrowserRouter works with browser history mechanisms such as:

```text
pushState
replaceState
popstate
```

This allows applications to provide clean URLs and browser navigation.

### When Should We Use BrowserRouter?

Use it for:

- Business websites
- E-commerce applications
- Admin dashboards
- SaaS applications
- Student management systems
- Job portals
- Social media applications
- Portfolio applications

### Important Deployment Note

With `BrowserRouter`, if a user directly visits:

```text
https://example.com/about
```

the production web server must be configured to serve the React application's entry document for that route.

Otherwise, the browser may receive a server-side `404`.

---

# 7. HashRouter

`HashRouter` uses the hash portion of the URL.

Example:

```text
https://example.com/#/about
https://example.com/#/contact
```

The part after `#` is handled by the client-side application.

### Syntax

```jsx
import { HashRouter } from "react-router-dom";

function App() {
  return (
    <HashRouter>
      {/* Routes */}
    </HashRouter>
  );
}
```

### Why Use HashRouter?

It can be useful when the hosting environment does not provide server-side URL rewriting.

For example:

```text
Static Hosting
      ↓
No server route configuration
      ↓
HashRouter
      ↓
#/about
```

### Example

```jsx
<HashRouter>
  <Routes>
    <Route path="/" element={<Home />} />
    <Route path="/about" element={<About />} />
  </Routes>
</HashRouter>
```

---

# 8. MemoryRouter

`MemoryRouter` stores navigation history in memory.

It does not depend on the browser URL.

```jsx
import { MemoryRouter } from "react-router-dom";

function App() {
  return (
    <MemoryRouter>
      {/* Routes */}
    </MemoryRouter>
  );
}
```

### Common Uses

- Testing routing
- Non-browser environments
- Isolated React applications
- Applications where URL changes are not required

### Concept

```text
Browser URL
     X
     │
     ▼
MemoryRouter
     │
     ▼
Internal navigation history
```

---

# 9. StaticRouter and NativeRouter

## StaticRouter

`StaticRouter` is primarily associated with server-side rendering and static routing scenarios.

It allows a React application to render based on a supplied location without relying on browser navigation APIs.

Conceptually:

```text
Server
  ↓
Requested URL
  ↓
Static Router
  ↓
React Route
  ↓
HTML
```

The exact API can vary with the React Router version and rendering architecture.

---

## NativeRouter

React Native applications use navigation solutions designed for native environments.

If working with React Native, always check the router package/version documentation for the current recommended API.

For normal React web development, focus first on:

```text
BrowserRouter
HashRouter
MemoryRouter
```

---

# 10. Main React Router Components

The core concepts to learn are:

| Component / Hook | Purpose |
|---|---|
| `BrowserRouter` | Enables browser-based routing |
| `HashRouter` | Enables hash-based routing |
| `MemoryRouter` | Keeps routing history in memory |
| `Routes` | Contains route definitions |
| `Route` | Defines a route |
| `Link` | Navigates without full reload |
| `NavLink` | Link with active-state support |
| `Outlet` | Renders child routes |
| `useNavigate()` | Programmatic navigation |
| `useParams()` | Reads route parameters |
| `useSearchParams()` | Reads/updates query parameters |

---

# 11. Creating a React Router Project

## Step 1 — Create React Application

Using Vite:

```bash
npm create vite@latest react-router-example
```

Select:

```text
Framework: React
Variant: JavaScript
```

Then:

```bash
cd react-router-example
npm install
```

---

## Step 2 — Install React Router

```bash
npm install react-router-dom
```

> If your course/project specifically requires React Router v6, a version-pinned installation such as `npm install react-router-dom@6` can be used. For a new project, avoid blindly pinning an old major version unless your project requirements require it.

---

## Step 3 — Start Development Server

```bash
npm run dev
```

Open the URL displayed by Vite, commonly:

```text
http://localhost:5173
```

---

# 12. Project Structure

A clean beginner-friendly structure:

```text
react-router-example/
│
├── public/
│
├── src/
│   ├── components/
│   │   ├── Navbar.jsx
│   │   └── Layout.jsx
│   │
│   ├── pages/
│   │   ├── Home.jsx
│   │   ├── About.jsx
│   │   ├── Contact.jsx
│   │   ├── Products.jsx
│   │   └── NotFound.jsx
│   │
│   ├── App.jsx
│   ├── main.jsx
│   └── index.css
│
├── package.json
└── vite.config.js
```

### Why Separate `pages` and `components`?

```text
pages/
    → Route-level screens

components/
    → Reusable UI
```

For example:

```text
pages/Home.jsx
pages/About.jsx
pages/Products.jsx

components/Navbar.jsx
components/Button.jsx
components/Card.jsx
```

---

# 13. Basic Routing

## Home.jsx

```jsx
function Home() {
  return <h1>Home Page</h1>;
}

export default Home;
```

## About.jsx

```jsx
function About() {
  return <h1>About Page</h1>;
}

export default About;
```

## Contact.jsx

```jsx
function Contact() {
  return <h1>Contact Page</h1>;
}

export default Contact;
```

## App.jsx

```jsx
import {
  BrowserRouter,
  Routes,
  Route,
  Link
} from "react-router-dom";

import Home from "./pages/Home";
import About from "./pages/About";
import Contact from "./pages/Contact";

function App() {
  return (
    <BrowserRouter>

      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
        <Link to="/contact">Contact</Link>
      </nav>

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/contact" element={<Contact />} />
      </Routes>

    </BrowserRouter>
  );
}

export default App;
```

---

# 14. Link

`Link` creates navigation links.

```jsx
import { Link } from "react-router-dom";

function Navbar() {
  return (
    <nav>
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>
      <Link to="/contact">Contact</Link>
    </nav>
  );
}

export default Navbar;
```

### Why not use `<a>`?

You can use normal anchors when you intentionally want a normal browser navigation.

For internal React Router navigation, use:

```jsx
<Link to="/about">About</Link>
```

instead of:

```jsx
<a href="/about">About</a>
```

because React Router's `Link` integrates navigation with the client-side routing system.

---

# 15. NavLink

`NavLink` is similar to `Link`, but it provides information about whether the link is active.

```jsx
import { NavLink } from "react-router-dom";

function Navbar() {
  return (
    <nav>
      <NavLink
        to="/"
        className={({ isActive }) =>
          isActive ? "active" : ""
        }
      >
        Home
      </NavLink>

      <NavLink
        to="/about"
        className={({ isActive }) =>
          isActive ? "active" : ""
        }
      >
        About
      </NavLink>
    </nav>
  );
}

export default Navbar;
```

### CSS

```css
nav {
  display: flex;
  gap: 20px;
}

nav a {
  text-decoration: none;
}

nav a.active {
  font-weight: bold;
  text-decoration: underline;
}
```

### Real-World Example

Active navigation is useful in:

```text
Dashboard
├── Overview
├── Users
├── Orders
├── Reports
└── Settings
```

The currently selected section can be highlighted.

---

# 16. Route Parameters

A route parameter is a dynamic value inside the URL.

Example:

```text
/products/101
/products/102
/products/103
```

Instead of creating:

```jsx
<Route path="/products/101" ... />
<Route path="/products/102" ... />
<Route path="/products/103" ... />
```

we can create:

```jsx
<Route path="/products/:productId" element={<ProductDetails />} />
```

Here:

```text
:productId
```

is a dynamic route parameter.

---

# 17. useParams

`useParams()` reads dynamic route parameters.

## Route

```jsx
<Route
  path="/products/:productId"
  element={<ProductDetails />}
/>
```

## Component

```jsx
import { useParams } from "react-router-dom";

function ProductDetails() {
  const { productId } = useParams();

  return (
    <div>
      <h1>Product Details</h1>
      <p>Product ID: {productId}</p>
    </div>
  );
}

export default ProductDetails;
```

Visiting:

```text
/products/101
```

produces:

```text
Product ID: 101
```

---

## Real-World Example

A job portal may use:

```text
/jobs/501
/jobs/502
/jobs/503
```

Route:

```jsx
<Route
  path="/jobs/:jobId"
  element={<JobDetails />}
/>
```

The same component can display different jobs.

---

# 18. Query Parameters

Query parameters are values after `?`.

Example:

```text
/products?category=laptop
```

Multiple query parameters:

```text
/products?category=laptop&sort=price
```

Another example:

```text
/jobs?location=pune&experience=2
```

### Difference

Route parameter:

```text
/products/101
```

Query parameter:

```text
/products?category=laptop
```

---

# 19. useSearchParams

`useSearchParams()` can read and update query parameters.

```jsx
import { useSearchParams } from "react-router-dom";

function Products() {
  const [searchParams, setSearchParams] = useSearchParams();

  const category = searchParams.get("category");

  return (
    <div>
      <h1>Products</h1>

      <p>Category: {category}</p>

      <button
        onClick={() =>
          setSearchParams({ category: "laptop" })
        }
      >
        Show Laptops
      </button>
    </div>
  );
}

export default Products;
```

### Example URL

```text
/products?category=laptop
```

---

# 20. Programmatic Navigation

Sometimes navigation happens because of an action rather than clicking a link.

Examples:

```text
Login successful
      ↓
Navigate to Dashboard

Form submitted
      ↓
Navigate to Success page

Logout
      ↓
Navigate to Login page
```

For this, use `useNavigate()`.

---

# 21. useNavigate

```jsx
import { useNavigate } from "react-router-dom";

function Login() {
  const navigate = useNavigate();

  function handleLogin() {
    // Login logic

    navigate("/dashboard");
  }

  return (
    <button onClick={handleLogin}>
      Login
    </button>
  );
}

export default Login;
```

### Navigate Back

```jsx
navigate(-1);
```

### Navigate Forward

```jsx
navigate(1);
```

### Replace Current History Entry

```jsx
navigate("/dashboard", {
  replace: true
});
```

`replace: true` is useful in flows such as login where you may not want the user to return to the login page using Back.

---

# 22. Nested Routes

Large applications often contain nested sections.

Example:

```text
/dashboard
/dashboard/profile
/dashboard/settings
/dashboard/orders
```

Instead of defining every page independently, we can create nested routes.

### Route Structure

```text
Dashboard
│
├── Profile
├── Settings
└── Orders
```

---

## Example

```jsx
<Routes>

  <Route path="/dashboard" element={<DashboardLayout />}>

    <Route index element={<DashboardHome />} />

    <Route
      path="profile"
      element={<Profile />}
    />

    <Route
      path="settings"
      element={<Settings />}
    />

    <Route
      path="orders"
      element={<Orders />}
    />

  </Route>

</Routes>
```

Notice:

```jsx
path="profile"
```

not:

```jsx
path="/profile"
```

because it is nested under `/dashboard`.

---

# 23. Outlet

`Outlet` is used inside a parent route component to render the matching child route.

## DashboardLayout.jsx

```jsx
import { Outlet } from "react-router-dom";

function DashboardLayout() {
  return (
    <div>

      <h1>Dashboard</h1>

      <nav>
        {/* Dashboard navigation */}
      </nav>

      <main>
        <Outlet />
      </main>

    </div>
  );
}

export default DashboardLayout;
```

### Routing Flow

```text
/dashboard
     │
     ▼
DashboardLayout
     │
     ▼
   Outlet
     │
     ├── DashboardHome
     ├── Profile
     ├── Settings
     └── Orders
```

---

# 24. 404 / Not Found Route

A professional application should handle unknown URLs.

React Router supports a wildcard route:

```jsx
<Route
  path="*"
  element={<NotFound />}
/>
```

## NotFound.jsx

```jsx
function NotFound() {
  return (
    <div>
      <h1>404</h1>
      <p>Page not found.</p>
    </div>
  );
}

export default NotFound;
```

Example:

```text
https://example.com/this-page-does-not-exist
```

will display the Not Found page.

---

# 25. Navigation State

Sometimes you need to send temporary state while navigating.

Example:

```jsx
navigate("/profile", {
  state: {
    from: "dashboard"
  }
});
```

The destination can read that state using `useLocation()`.

```jsx
import { useLocation } from "react-router-dom";

function Profile() {
  const location = useLocation();

  console.log(location.state);

  return <h1>Profile</h1>;
}

export default Profile;
```

This is useful for temporary navigation context.

Do not use navigation state as a replacement for persistent application state or server data.

---

# 26. Protected Routes

A protected route is a route that should only be accessible when a condition is satisfied.

Typical examples:

```text
Dashboard
Profile
Orders
Admin Panel
Settings
```

may require authentication.

### Concept

```text
User requests /dashboard
          │
          ▼
   Is user logged in?
       /       \
     Yes        No
      │          │
      ▼          ▼
 Dashboard      Login
```

---

## Basic Protected Route Example

```jsx
import { Navigate } from "react-router-dom";

function ProtectedRoute({ children }) {
  const isLoggedIn = Boolean(
    localStorage.getItem("token")
  );

  if (!isLoggedIn) {
    return <Navigate to="/login" replace />;
  }

  return children;
}

export default ProtectedRoute;
```

Usage:

```jsx
<Route
  path="/dashboard"
  element={
    <ProtectedRoute>
      <Dashboard />
    </ProtectedRoute>
  }
/>
```

> This example demonstrates routing logic only. Real production authentication should use secure authentication architecture and server-side authorization; a client-side localStorage check alone is not a security boundary.

---

# 27. BrowserRouter vs HashRouter vs MemoryRouter

| Feature | BrowserRouter | HashRouter | MemoryRouter |
|---|---|---|---|
| Clean URL | Yes | No | Not reflected in browser URL |
| Uses browser history | Yes | Hash-based | Internal memory |
| URL changes | Yes | Yes, with `#` | No browser URL |
| Common web apps | Excellent | Useful in limited hosting cases | Not usually |
| Testing | Possible | Possible | Excellent |
| Static hosting without rewrites | Requires configuration | Convenient | N/A |
| Dynamic routes | Yes | Yes | Yes |
| Nested routes | Yes | Yes | Yes |

### Easy Rule

```text
Normal production web app
        ↓
BrowserRouter

Static hosting without URL rewrite support
        ↓
HashRouter

Testing / in-memory navigation
        ↓
MemoryRouter
```

---

# 28. Real-World Industry Use Cases

## 1. E-Commerce

```text
/
 /products
 /products/:productId
 /cart
 /checkout
 /orders
 /profile
```

---

## 2. Job Portal

```text
/
 /jobs
 /jobs/:jobId
 /companies
 /companies/:companyId
 /login
 /dashboard
```

---

## 3. Admin Dashboard

```text
/dashboard
/dashboard/users
/dashboard/orders
/dashboard/reports
/dashboard/settings
```

Nested routes are especially useful here.

---

## 4. Student Management System

```text
/students
/students/:studentId
/students/add
/students/edit/:studentId
```

---

## 5. Social Media Application

```text
/
/feed
/profile/:username
/messages
/notifications
/settings
```

---

# 29. Common Mistakes

## Mistake 1 — Forgetting to Install Router

Error:

```text
Module not found
```

Solution:

```bash
npm install react-router-dom
```

---

## Mistake 2 — Incorrect Import

Correct:

```jsx
import {
  BrowserRouter,
  Routes,
  Route
} from "react-router-dom";
```

---

## Mistake 3 — Using Wrong Route Syntax

Current element-based routing:

```jsx
<Route
  path="/about"
  element={<About />}
/>
```

Do not copy older examples that use obsolete APIs without checking the version.

---

## Mistake 4 — Using `<a>` for Every Internal Link

Prefer:

```jsx
<Link to="/about">About</Link>
```

for React Router navigation.

---

## Mistake 5 — Forgetting `Outlet`

If child routes are configured but nothing appears, check whether the parent layout contains:

```jsx
<Outlet />
```

---

## Mistake 6 — Wrong Nested Path

Incorrect:

```jsx
<Route path="/profile" element={<Profile />} />
```

inside a `/dashboard` nested route when you intended:

```text
/dashboard/profile
```

Use:

```jsx
<Route path="profile" element={<Profile />} />
```

---

## Mistake 7 — Forgetting Dynamic Parameter

Route:

```jsx
<Route
  path="/users/:userId"
  element={<UserDetails />}
/>
```

Then:

```jsx
const { userId } = useParams();
```

---

## Mistake 8 — BrowserRouter 404 After Deployment

Application works locally but:

```text
example.com/about
```

returns a server 404.

Possible reason:

```text
Server is not configured to serve the SPA entry point
```

Configure the hosting platform's rewrite/fallback rules appropriately.

---

## Mistake 9 — Using `window.location` for Normal Internal Navigation

Instead of:

```jsx
window.location.href = "/about";
```

prefer:

```jsx
navigate("/about");
```

or:

```jsx
<Link to="/about">About</Link>
```

when using React Router.

---

# 30. Final Practical Lab

# Project: StudentHub — Student Management Portal

Build a complete React Router application.

## Objective

Create a multi-page Student Management Portal using:

- React
- Vite
- React Router
- Components
- Props
- State
- Forms
- Lists
- Keys
- Hooks
- Dynamic routes
- Nested routes
- Query parameters
- Programmatic navigation
- 404 handling

---

## Required Pages

```text
Home
About
Students
Student Details
Add Student
Login
Dashboard
Profile
Settings
404
```

---

## Required Routes

```text
/
 /about
 /students
 /students/:studentId
 /add-student
 /login
 /dashboard
 /dashboard/profile
 /dashboard/settings
 *
```

---

## Recommended Project Structure

```text
src/
│
├── components/
│   ├── Navbar.jsx
│   ├── StudentCard.jsx
│   └── ProtectedRoute.jsx
│
├── layouts/
│   └── DashboardLayout.jsx
│
├── pages/
│   ├── Home.jsx
│   ├── About.jsx
│   ├── Students.jsx
│   ├── StudentDetails.jsx
│   ├── AddStudent.jsx
│   ├── Login.jsx
│   ├── Dashboard.jsx
│   ├── Profile.jsx
│   ├── Settings.jsx
│   └── NotFound.jsx
│
├── App.jsx
├── main.jsx
└── index.css
```

---

## Student Data

Use an array such as:

```jsx
const students = [
  {
    id: 101,
    name: "Amit Sharma",
    course: "Computer Engineering",
    city: "Pune"
  },
  {
    id: 102,
    name: "Priya Patil",
    course: "Information Technology",
    city: "Mumbai"
  },
  {
    id: 103,
    name: "Rahul Joshi",
    course: "Computer Engineering",
    city: "Nashik"
  }
];
```

---

## Students Page

Display students using:

```jsx
students.map(...)
```

Use stable keys:

```jsx
key={student.id}
```

Each student should have a button/link:

```text
View Details
```

which navigates to:

```text
/students/101
/students/102
/students/103
```

---

## Student Details Page

Use:

```jsx
useParams()
```

to read:

```text
studentId
```

Example:

```jsx
const { studentId } = useParams();
```

Display:

```text
Student ID
Name
Course
City
```

---

## Search Feature

Create a search box on the Students page.

Store the search value in the URL:

```text
/students?search=amit
```

Use:

```jsx
useSearchParams()
```

to read the value.

---

## Dashboard

Create nested routes:

```text
/dashboard
/dashboard/profile
/dashboard/settings
```

Use:

```jsx
<Outlet />
```

inside:

```text
DashboardLayout.jsx
```

---

## Login

Create a simple login form.

After successful login:

```jsx
navigate("/dashboard");
```

---

## Protected Dashboard

If the user is not authenticated:

```text
/dashboard
      ↓
    Login
```

If authenticated:

```text
/dashboard
      ↓
 Dashboard
```

---

## 404 Page

Any unknown URL should display:

```text
404
Page Not Found
Go Back Home
```

Use:

```jsx
<Route path="*" element={<NotFound />} />
```

---

# 31. Student Practice Tasks

## Task 1 — Basic Routes

Create:

```text
Home
About
Contact
```

---

## Task 2 — Navigation Bar

Create a navbar using:

```jsx
Link
```

---

## Task 3 — Active Navigation

Replace `Link` with:

```jsx
NavLink
```

and highlight the active page.

---

## Task 4 — Product Details

Create:

```text
/products/:productId
```

Use:

```jsx
useParams()
```

---

## Task 5 — Search

Create:

```text
/products?search=laptop
```

Use:

```jsx
useSearchParams()
```

---

## Task 6 — Programmatic Navigation

Create a login page.

After login:

```text
Login → Dashboard
```

Use:

```jsx
useNavigate()
```

---

## Task 7 — Nested Routes

Create:

```text
/dashboard
/dashboard/profile
/dashboard/settings
```

Use:

```jsx
Outlet
```

---

## Task 8 — Protected Route

Prevent unauthenticated users from opening:

```text
/dashboard
```

---

## Task 9 — 404 Page

Create a wildcard route:

```jsx
<Route path="*" element={<NotFound />} />
```

---

## Task 10 — Final Challenge

Build a mini:

> **Job Portal**

Required routes:

```text
/
 /jobs
 /jobs/:jobId
 /companies
 /companies/:companyId
 /login
 /dashboard
 /dashboard/profile
 /dashboard/applications
 /dashboard/settings
 *
```

Features:

- Navbar
- Job listing
- Job details
- Search
- Dynamic job IDs
- Login
- Protected dashboard
- Nested routes
- 404 page
- Back navigation
- Active navigation

---

# 32. Interview Questions

## Beginner

### 1. What is React Router?

A routing library that manages navigation and URL-to-component mapping in React applications.

### 2. Why is React Router used?

To implement client-side routing and navigate between application views without full document reloads.

### 3. What is `BrowserRouter`?

A router that uses browser history APIs to synchronize the application's UI with the URL.

### 4. What is `HashRouter`?

A router that stores route information in the URL hash.

### 5. What is `MemoryRouter`?

A router that stores navigation history in memory instead of the browser URL.

### 6. What is `Route`?

A route definition that maps a path to an element.

### 7. What is `Routes`?

The component that contains route definitions.

### 8. What is `Link`?

A component used for client-side navigation.

### 9. What is `NavLink`?

A navigation link that also exposes active-state information.

### 10. What is `useNavigate()`?

A hook used to navigate programmatically.

---

## Intermediate

### 11. What is dynamic routing?

Creating routes that contain dynamic parameters.

Example:

```text
/users/:userId
```

### 12. What is `useParams()`?

A hook used to read dynamic route parameters.

### 13. What is a nested route?

A route rendered within the layout of another route.

### 14. What is `Outlet`?

A placeholder where the matching child route renders.

### 15. What are query parameters?

Values included in the URL after `?`.

Example:

```text
/products?category=laptop
```

### 16. What is `useSearchParams()`?

A hook for reading and updating URL query parameters.

### 17. How do you create a 404 route?

```jsx
<Route path="*" element={<NotFound />} />
```

### 18. What is a protected route?

A route whose content is conditionally accessible, commonly based on authentication.

### 19. Why can BrowserRouter cause a 404 after deployment?

Because the server must be configured to return the SPA entry document for application routes.

### 20. Difference between `Link` and `NavLink`?

`NavLink` provides active-state information, while `Link` provides basic navigation.

---

# 33. Quick Revision

```text
React Router
│
├── Routing
│   ├── Client-side routing
│   ├── URL mapping
│   └── SPA navigation
│
├── Routers
│   ├── BrowserRouter
│   ├── HashRouter
│   ├── MemoryRouter
│   └── StaticRouter
│
├── Route Configuration
│   ├── Routes
│   └── Route
│
├── Navigation
│   ├── Link
│   ├── NavLink
│   └── useNavigate
│
├── Dynamic Routing
│   ├── :id
│   └── useParams
│
├── Query Parameters
│   └── useSearchParams
│
├── Nested Routing
│   └── Outlet
│
└── Application Patterns
    ├── 404
    └── Protected Routes
```

---

# 34. Final React Learning Roadmap

If you have completed the previous modules and this routing module, your React learning path can now be organized as:

```text
React Introduction
       ↓
Environment Setup
       ↓
JSX
       ↓
Components
       ↓
Props
       ↓
Events
       ↓
Conditional Rendering
       ↓
Lists + Forms + Keys
       ↓
useState
       ↓
useEffect
       ↓
React Router
       ↓
API Integration
       ↓
Authentication
       ↓
Global State Management
       ↓
Redux Toolkit / Context
       ↓
Performance Optimization
       ↓
Testing
       ↓
Deployment
       ↓
Production Projects
```

---

# Final Practical Checklist

Before considering this module complete, make sure you can:

- [ ] Explain client-side routing
- [ ] Explain SPA navigation
- [ ] Create a Vite React project
- [ ] Install React Router
- [ ] Use `BrowserRouter`
- [ ] Explain `HashRouter`
- [ ] Explain `MemoryRouter`
- [ ] Create `Routes`
- [ ] Create `Route`
- [ ] Use `Link`
- [ ] Use `NavLink`
- [ ] Use `useNavigate`
- [ ] Use `useParams`
- [ ] Create dynamic routes
- [ ] Use query parameters
- [ ] Use `useSearchParams`
- [ ] Create nested routes
- [ ] Use `Outlet`
- [ ] Create a 404 page
- [ ] Understand protected routes
- [ ] Understand BrowserRouter deployment requirements
- [ ] Build the StudentHub practical
- [ ] Build a Job Portal routing project

---

# Final Concept

The most important idea to remember is:

```text
URL
 ↓
React Router
 ↓
Match Route
 ↓
Render Component
 ↓
User Interaction
 ↓
Navigate to Another URL
 ↓
React Router
 ↓
Render New Component
```

React Router turns a collection of React components into a structured, navigable application.

For a production-style React application, think of routing as the connection between:

```text
URL
+
Application Structure
+
Navigation
+
Dynamic Data
+
Authentication
+
User Experience
```

---

## End of React Router Module

**Recommended next step:** Build the **StudentHub Final Practical** without copying the solution first. Implement each route one by one, test the URL manually, and then add dynamic routing, query parameters, nested routes, and protected navigation.
