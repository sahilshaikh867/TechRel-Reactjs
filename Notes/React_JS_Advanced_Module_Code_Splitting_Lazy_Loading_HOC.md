# React JS — Advanced Module: Code Splitting, Lazy Loading & Higher-Order Components

> **Level:** Advanced React  
> **Audience:** Beginners progressing toward professional React development  
> **Prerequisites:** React fundamentals, JSX, Components, Props, Lists, Forms, `useState`, `useEffect`, and React Router  
> **Recommended setup:** React + Vite + JavaScript  
> **Module focus:** Performance optimization, dynamic imports, lazy loading, Suspense, code splitting, route-based code splitting, error handling, and Higher-Order Components (HOCs)

---

# Table of Contents

1. [Why This Module Matters](#1-why-this-module-matters)
2. [What You Will Learn](#2-what-you-will-learn)
3. [The Big Picture](#3-the-big-picture)
4. [What Is Code Splitting?](#4-what-is-code-splitting)
5. [Bundling Before Code Splitting](#5-bundling-before-code-splitting)
6. [Dynamic Import](#6-dynamic-import)
7. [Lazy Loading in React](#7-lazy-loading-in-react)
8. [React.lazy](#8-reactlazy)
9. [Suspense](#9-suspense)
10. [How React.lazy and Suspense Work Together](#10-how-reactlazy-and-suspense-work-together)
11. [Basic Lazy Loading Example](#11-basic-lazy-loading-example)
12. [Multiple Lazy Components](#12-multiple-lazy-components)
13. [Choosing a Good Suspense Boundary](#13-choosing-a-good-suspense-boundary)
14. [Route-Based Code Splitting](#14-route-based-code-splitting)
15. [React Router + Lazy Loading](#15-react-router--lazy-loading)
16. [Loading UI / Skeletons](#16-loading-ui--skeletons)
17. [Error Handling for Lazy Components](#17-error-handling-for-lazy-components)
18. [Named Exports and React.lazy](#18-named-exports-and-reactlazy)
19. [Lazy Loading Images and Other Assets](#19-lazy-loading-images-and-other-assets)
20. [Performance: What Actually Improves](#20-performance-what-actually-improves)
21. [When NOT to Lazy Load](#21-when-not-to-lazy-load)
22. [Common Lazy Loading Mistakes](#22-common-lazy-loading-mistakes)
23. [Higher-Order Components](#23-higher-order-components)
24. [HOC Mental Model](#24-hoc-mental-model)
25. [Basic HOC Example](#25-basic-hoc-example)
26. [Passing Props Through a HOC](#26-passing-props-through-a-hoc)
27. [HOC for Authentication](#27-hoc-for-authentication)
28. [HOC for Loading States](#28-hoc-for-loading-states)
29. [HOC for Permissions](#29-hoc-for-permissions)
30. [HOC for Logging](#30-hoc-for-logging)
31. [HOC Composition](#31-hoc-composition)
32. [Important HOC Rules](#32-important-hoc-rules)
33. [HOCs vs Hooks vs Components](#33-hocs-vs-hooks-vs-components)
34. [Advanced Industry Architecture](#34-advanced-industry-architecture)
35. [Final Practical Project](#35-final-practical-project)
36. [Practice Tasks](#36-practice-tasks)
37. [Interview Questions](#37-interview-questions)
38. [Quick Revision](#38-quick-revision)
39. [Final Checklist](#39-final-checklist)

---

# 1. Why This Module Matters

So far, you have learned how to build React applications.

You can create:

```text
Components
      ↓
Props
      ↓
State
      ↓
Forms
      ↓
Effects
      ↓
Routing
```

Now we need to answer an important production question:

> What happens when our React application becomes very large?

Imagine an application with:

```text
Home
Dashboard
Admin Panel
Reports
Analytics
Charts
Settings
Profile
Orders
Payments
Large Editor
Maps
Video Player
```

If the browser downloads everything before showing the application, the initial JavaScript bundle can become large.

That can increase:

- Download time
- JavaScript parsing
- JavaScript execution
- Memory usage
- Initial loading time

Code splitting and lazy loading help solve this problem.

---

# 2. What You Will Learn

By the end of this module, you should understand:

### Performance

- Bundling
- Code splitting
- Dynamic imports
- Lazy loading
- Chunk loading

### React APIs

- `lazy()`
- `Suspense`

### Routing

- Route-based code splitting
- Lazy-loaded pages
- Loading UI

### Reliability

- Error boundaries
- Failed chunk loading

### Advanced React

- Higher-Order Components
- HOC patterns
- Authentication HOC
- Permission HOC
- Loading HOC
- Logging HOC

### Architecture

You should understand when to use:

```text
Lazy Loading
Code Splitting
Hooks
HOCs
Reusable Components
```

---

# 3. The Big Picture

The complete concept can be visualized as:

```text
                    React Application
                           │
                           ▼
                       Bundler
                           │
             ┌─────────────┴─────────────┐
             │                           │
       Initial Chunk                Lazy Chunks
             │                           │
             ▼                           ▼
        Home / Core              Dashboard / Reports
        Navigation               Admin / Analytics
             │                           │
             └─────────────┬─────────────┘
                           │
                           ▼
                    Browser requests
                    extra code only
                    when required
```

The main goal is:

> Do not make the browser download every piece of application code before it needs that code.

---

# 4. What Is Code Splitting?

**Code splitting** means dividing a large JavaScript application into smaller chunks that can be loaded independently.

Instead of:

```text
Application
     ↓
One huge JavaScript file
```

we can have:

```text
Application
     │
     ├── main.js
     ├── dashboard.js
     ├── reports.js
     ├── admin.js
     └── settings.js
```

The exact filenames and chunk strategy are determined by the build tool.

## Why?

Suppose:

```text
main.js = 2 MB
```

contains:

```text
Home
Dashboard
Admin
Reports
Charts
Settings
```

A user who only opens Home does not necessarily need all that code immediately.

With code splitting:

```text
Initial:
main.js

Later:
dashboard chunk
reports chunk
admin chunk
```

This can reduce the amount of JavaScript needed during the initial load.

---

# 5. Bundling Before Code Splitting

Modern React applications use build tools such as Vite.

During a production build, the tooling analyzes the application's modules and produces optimized output.

Conceptually:

```text
src/
│
├── App.jsx
├── Home.jsx
├── Dashboard.jsx
├── Reports.jsx
└── Settings.jsx

              ↓

             Build

              ↓

dist/
│
├── index.html
├── assets/
│   ├── main-xxxx.js
│   ├── Dashboard-xxxx.js
│   ├── Reports-xxxx.js
│   └── Settings-xxxx.js
```

The exact output depends on the bundler and build configuration.

---

# 6. Dynamic Import

Before understanding `React.lazy`, understand JavaScript's dynamic `import()`.

## Normal Import

```jsx
import { add } from "./math.js";
```

This is a static module import.

---

## Dynamic Import

```jsx
import("./math.js")
  .then((math) => {
    console.log(math.add(10, 20));
  });
```

The important difference is that:

```jsx
import("./math.js")
```

returns a Promise.

Conceptually:

```text
Application
     │
     ▼
import("./math.js")
     │
     ▼
Promise
     │
     ▼
Module loaded
     │
     ▼
Use module
```

Dynamic imports are one of the foundations of code splitting.

---

# 7. Lazy Loading in React

Lazy loading means:

> Load a component when it is needed instead of loading that component as part of the initial application code.

Example:

```jsx
import { lazy } from "react";

const Dashboard = lazy(() =>
  import("./Dashboard")
);
```

Now React can load the component dynamically.

---

# 8. React.lazy

The basic syntax is:

```jsx
const MyComponent = lazy(() =>
  import("./MyComponent")
);
```

Import:

```jsx
import { lazy } from "react";
```

Complete example:

```jsx
import { lazy } from "react";

const About = lazy(() =>
  import("./pages/About")
);
```

Important:

```jsx
lazy(() => import("./pages/About"))
```

is not the same as:

```jsx
import About from "./pages/About";
```

The first creates a lazy-loaded component.

---

# 9. Suspense

A lazy component may not be available immediately.

React therefore needs a fallback UI while the component is loading.

That is what `Suspense` provides.

```jsx
import { Suspense } from "react";

<Suspense fallback={<p>Loading...</p>}>
  <About />
</Suspense>
```

The user may temporarily see:

```text
Loading...
```

and then:

```text
About Page
```

---

# 10. How React.lazy and Suspense Work Together

The relationship is:

```text
lazy()
  │
  │ component not loaded yet
  ▼
Dynamic import()
  │
  ▼
Browser downloads chunk
  │
  ▼
Suspense shows fallback
  │
  ▼
Chunk finishes loading
  │
  ▼
React renders component
```

Think of them as two separate responsibilities:

```text
React.lazy
    ↓
"Load this component lazily."

Suspense
    ↓
"Show this UI while waiting."
```

---

# 11. Basic Lazy Loading Example

## Project Structure

```text
src/
│
├── components/
│   ├── Home.jsx
│   └── About.jsx
│
├── App.jsx
└── main.jsx
```

## About.jsx

```jsx
function About() {
  return (
    <div>
      <h1>About Page</h1>
      <p>This page was loaded lazily.</p>
    </div>
  );
}

export default About;
```

## App.jsx

```jsx
import { lazy, Suspense } from "react";

const About = lazy(() =>
  import("./components/About")
);

function App() {
  return (
    <div>

      <h1>My Application</h1>

      <Suspense fallback={<p>Loading About...</p>}>
        <About />
      </Suspense>

    </div>
  );
}

export default App;
```

---

# 12. Multiple Lazy Components

You can lazy-load multiple components.

```jsx
import { lazy, Suspense } from "react";

const Profile = lazy(() =>
  import("./Profile")
);

const Reports = lazy(() =>
  import("./Reports")
);

function App() {
  return (
    <Suspense fallback={<p>Loading...</p>}>

      <Profile />

      <Reports />

    </Suspense>
  );
}

export default App;
```

One `Suspense` boundary can cover multiple lazy components.

---

# 13. Choosing a Good Suspense Boundary

You do not always need one giant:

```jsx
<Suspense>
```

around the entire application.

Instead, think about user experience.

For example:

```text
Application
│
├── Header
│
├── Sidebar
│
└── Main Content
       │
       └── Suspense
              │
              └── Reports
```

This can allow the important shell of the application to remain visible while the slower section loads.

Another strategy:

```text
<Suspense fallback="Loading page...">
    Entire Route
</Suspense>
```

Both approaches can be valid.

Choose boundaries based on the UI experience you want.

---

# 14. Route-Based Code Splitting

One of the most useful forms of code splitting is **route-based code splitting**.

Suppose an application has:

```text
/
 /about
 /dashboard
 /reports
 /settings
```

A user visiting Home may not need Dashboard or Reports immediately.

So we can load pages when users navigate to them.

Concept:

```text
Home
 │
 ├── User clicks Dashboard
 │
 ▼
Dashboard chunk loads
 │
 ▼
Dashboard renders
```

---

# 15. React Router + Lazy Loading

This is especially useful because you already learned React Router.

Example:

```jsx
import {
  BrowserRouter,
  Routes,
  Route
} from "react-router-dom";

import {
  lazy,
  Suspense
} from "react";

const Home = lazy(() =>
  import("./pages/Home")
);

const About = lazy(() =>
  import("./pages/About")
);

const Dashboard = lazy(() =>
  import("./pages/Dashboard")
);

function App() {
  return (
    <BrowserRouter>

      <Suspense fallback={<p>Loading page...</p>}>

        <Routes>

          <Route
            path="/"
            element={<Home />}
          />

          <Route
            path="/about"
            element={<About />}
          />

          <Route
            path="/dashboard"
            element={<Dashboard />}
          />

        </Routes>

      </Suspense>

    </BrowserRouter>
  );
}

export default App;
```

Now route-level components can be loaded on demand.

---

# 16. Loading UI / Skeletons

A plain:

```jsx
<p>Loading...</p>
```

works, but production applications often provide better loading states.

Example:

```jsx
function PageLoader() {
  return (
    <div>
      <h2>Loading page...</h2>
      <p>Please wait.</p>
    </div>
  );
}
```

Then:

```jsx
<Suspense fallback={<PageLoader />}>
  <Dashboard />
</Suspense>
```

---

## Skeleton Concept

Instead of:

```text
Loading...
```

you can display:

```text
┌───────────────────────────────┐
│ ███████████████               │
│                               │
│ █████████████████████         │
│ ███████████                   │
│                               │
│ ███████████████████           │
└───────────────────────────────┘
```

This can make the application feel more responsive.

---

# 17. Error Handling for Lazy Components

Lazy loading can fail.

Possible reasons include:

- Network interruption
- Server/CDN issue
- Missing chunk
- Deployment mismatch
- Browser cache issues
- Connection failure

A loading fallback does not replace error handling.

You should consider an **Error Boundary** around important lazy-loaded areas.

Concept:

```text
ErrorBoundary
     │
     ▼
Suspense
     │
     ▼
Lazy Component
     │
     ├── Success → Render
     │
     └── Failure → Error UI
```

---

## Important Difference

`Suspense` handles:

```text
Waiting
```

An Error Boundary handles:

```text
Rendering/loading errors that reach the boundary
```

They solve different problems.

---

# 18. Named Exports and React.lazy

`React.lazy()` expects the dynamically imported module to resolve to a module whose `default` export is the component.

This works directly:

```jsx
// Reports.jsx

export default function Reports() {
  return <h1>Reports</h1>;
}
```

Then:

```jsx
const Reports = lazy(() =>
  import("./Reports")
);
```

---

## What If the Component Is a Named Export?

Suppose:

```jsx
// Components.jsx

export function Reports() {
  return <h1>Reports</h1>;
}

export function Analytics() {
  return <h1>Analytics</h1>;
}
```

The module does not have:

```jsx
export default Reports;
```

One approach is to create an intermediate module:

```jsx
// ReportsLazy.jsx

export {
  Reports as default
} from "./Components";
```

Then:

```jsx
const Reports = lazy(() =>
  import("./ReportsLazy")
);
```

### Why?

Now the lazy import resolves to:

```text
default export
    ↓
Reports component
```

This pattern is useful when you need to adapt a named export to the default-export shape expected by `lazy()`.

---

# 19. Lazy Loading Images and Other Assets

Lazy loading is broader than React components.

For images, modern browsers support:

```jsx
<img
  src="/images/product.jpg"
  alt="Product"
  loading="lazy"
/>
```

This tells the browser that the image can be deferred when appropriate.

This is different from:

```jsx
React.lazy()
```

because `React.lazy()` is specifically for React components.

### Remember

```text
React.lazy()
     ↓
React component code

loading="lazy"
     ↓
Browser image loading
```

---

# 20. Performance: What Actually Improves?

Code splitting can improve performance by reducing the amount of JavaScript needed initially.

Potential benefits:

### 1. Smaller Initial JavaScript

```text
Before:
[Everything]

After:
[Required now]
```

### 2. Faster Initial Loading

Less code may need to be:

```text
Downloaded
Parsed
Compiled
Executed
```

### 3. Better Scalability

Large applications can be divided into logical chunks.

### 4. Better User Experience

Users can access the initial UI before downloading less frequently used features.

---

## Important Warning

Lazy loading does not magically make every application faster.

There is a trade-off:

```text
Less initial code
      +
More requests/chunks later
```

If you split too aggressively, navigation may require additional network requests for many tiny chunks.

Good performance optimization requires measurement.

---

# 21. When NOT to Lazy Load

Do not blindly lazy-load everything.

Avoid unnecessary lazy loading for:

- Tiny components
- Components shown immediately on almost every page
- Critical above-the-fold UI
- Components where extra loading delay hurts UX
- Components whose split provides negligible savings

For example:

```text
Navbar
Logo
Primary layout
Main application shell
```

often belong in the initial application path.

But a rarely visited:

```text
Admin Analytics
Advanced Reports
Large Editor
```

may be a good candidate.

---

# 22. Common Lazy Loading Mistakes

## Mistake 1 — Forgetting Suspense

Incorrect:

```jsx
const Dashboard = lazy(() =>
  import("./Dashboard")
);

<Dashboard />
```

Use:

```jsx
<Suspense fallback={<p>Loading...</p>}>
  <Dashboard />
</Suspense>
```

---

## Mistake 2 — Wrong Import Path

Incorrect:

```jsx
lazy(() => import("./Dashbord"))
```

when the file is:

```text
Dashboard.jsx
```

---

## Mistake 3 — Missing Default Export

If the lazy-loaded module does not resolve to the expected default component export, the lazy component will fail.

---

## Mistake 4 — Lazy Loading Tiny Components

Do not create dozens of tiny chunks without a reason.

---

## Mistake 5 — Assuming Suspense Handles Every Error

Suspense is not an error boundary.

Use an appropriate error boundary for error handling.

---

## Mistake 6 — Ignoring Deployment

Lazy-loaded chunks must be available from the production server/CDN.

A deployment that serves the main application but fails to serve generated chunk files can cause loading failures.

---

# 23. Higher-Order Components

Now we move to another advanced React technique:

> **Higher-Order Components (HOCs)**

A Higher-Order Component is a function that:

```text
takes a component
       ↓
adds reusable behavior
       ↓
returns a new component
```

Syntax:

```jsx
const EnhancedComponent =
  higherOrderComponent(OriginalComponent);
```

---

# 24. HOC Mental Model

Think of a HOC as a wrapper factory.

```text
Original Component
       │
       ▼
   HOC Function
       │
       ▼
Enhanced Component
```

Example:

```text
UserProfile
    │
    ▼
withAuth(UserProfile)
    │
    ▼
ProtectedUserProfile
```

The original component does not need to contain all authentication logic.

---

# 25. Basic HOC Example

Create a HOC:

```jsx
function withName(WrappedComponent) {

  function EnhancedComponent(props) {

    return (
      <WrappedComponent
        {...props}
        name="Sahil"
      />
    );

  }

  return EnhancedComponent;
}

export default withName;
```

Original component:

```jsx
function Welcome({ name }) {
  return <h1>Welcome {name}</h1>;
}
```

Enhance it:

```jsx
const EnhancedWelcome =
  withName(Welcome);
```

Then:

```jsx
<EnhancedWelcome />
```

Result:

```text
Welcome Sahil
```

---

# 26. Passing Props Through a HOC

This is extremely important.

Suppose:

```jsx
function User({ name, age }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>{age}</p>
    </div>
  );
}
```

HOC:

```jsx
function withLogger(WrappedComponent) {

  return function EnhancedComponent(props) {

    console.log("Received props:", props);

    return (
      <WrappedComponent {...props} />
    );
  };
}
```

Then:

```jsx
const EnhancedUser =
  withLogger(User);
```

Use:

```jsx
<EnhancedUser
  name="Amit"
  age={22}
/>
```

The spread:

```jsx
{...props}
```

forwards the props to the wrapped component.

---

# 27. HOC for Authentication

A classic HOC pattern:

```jsx
import { Navigate } from "react-router-dom";

function withAuth(WrappedComponent) {

  return function ProtectedComponent(props) {

    const token =
      localStorage.getItem("token");

    if (!token) {
      return <Navigate to="/login" replace />;
    }

    return (
      <WrappedComponent {...props} />
    );
  };
}

export default withAuth;
```

Usage:

```jsx
function Dashboard() {
  return <h1>Dashboard</h1>;
}

const ProtectedDashboard =
  withAuth(Dashboard);
```

Then:

```jsx
<Route
  path="/dashboard"
  element={<ProtectedDashboard />}
/>
```

> This demonstrates a UI-level authentication gate. A real application must still enforce authorization on the server/API.

---

# 28. HOC for Loading States

Create:

```jsx
function withLoading(WrappedComponent) {

  return function LoadingComponent({
    isLoading,
    ...props
  }) {

    if (isLoading) {
      return <h2>Loading...</h2>;
    }

    return (
      <WrappedComponent {...props} />
    );
  };
}
```

Component:

```jsx
function UserList({ users }) {

  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>
          {user.name}
        </li>
      ))}
    </ul>
  );
}
```

Enhance:

```jsx
const UserListWithLoading =
  withLoading(UserList);
```

Use:

```jsx
<UserListWithLoading
  isLoading={true}
  users={[]}
/>
```

This separates loading behavior from the UI component.

---

# 29. HOC for Permissions

Imagine an admin-only page.

```jsx
function withRole(
  WrappedComponent,
  requiredRole
) {

  return function RoleProtectedComponent(props) {

    const role =
      localStorage.getItem("role");

    if (role !== requiredRole) {
      return (
        <h2>
          Access Denied
        </h2>
      );
    }

    return (
      <WrappedComponent {...props} />
    );
  };
}
```

Usage:

```jsx
const AdminPanel =
  withRole(AdminDashboard, "admin");
```

Concept:

```text
User
 │
 ▼
Role Check
 │
 ├── admin → AdminDashboard
 │
 └── other → Access Denied
```

Again, real authorization must be enforced by the backend.

---

# 30. HOC for Logging

A logging HOC can be useful for learning the pattern or for cross-cutting instrumentation.

```jsx
function withLogger(WrappedComponent) {

  return function LoggedComponent(props) {

    console.log(
      "Rendering:",
      WrappedComponent.name
    );

    return (
      <WrappedComponent {...props} />
    );
  };
}
```

Usage:

```jsx
const LoggedProfile =
  withLogger(Profile);
```

---

# 31. HOC Composition

You can apply multiple HOCs.

Example:

```jsx
const EnhancedDashboard =
  withAuth(
    withLogger(
      Dashboard
    )
  );
```

Conceptually:

```text
Dashboard
   ↓
withLogger
   ↓
withAuth
   ↓
EnhancedDashboard
```

But be careful.

Too many wrappers can make the component tree difficult to understand.

Modern React often prefers hooks and composition for many new use cases.

---

# 32. Important HOC Rules

## Rule 1 — Do Not Modify the Original Component

Bad:

```jsx
function withAuth(Component) {

  Component.isAuthenticated = true;

  return Component;
}
```

Better:

```jsx
function withAuth(Component) {

  return function EnhancedComponent(props) {
    return <Component {...props} />;
  };
}
```

HOCs should generally compose behavior around the original component rather than mutate it.

---

## Rule 2 — Forward Props

Use:

```jsx
<Component {...props} />
```

when appropriate.

---

## Rule 3 — Keep HOCs Composable

A HOC should ideally do one clear job:

```text
withAuth
withLoading
withLogger
withRole
```

---

## Rule 4 — Do Not Create HOCs During Render

Avoid:

```jsx
function App() {

  const Enhanced =
    withAuth(Dashboard);

  return <Enhanced />;
}
```

This creates a new component type during every render.

Instead, define it outside:

```jsx
const EnhancedDashboard =
  withAuth(Dashboard);

function App() {
  return <EnhancedDashboard />;
}
```

---

# 33. HOCs vs Hooks vs Components

Modern React provides multiple ways to reuse logic.

| Technique | Best For |
|---|---|
| Component | Reusable UI |
| Custom Hook | Reusable stateful/behavioral logic |
| HOC | Wrapping/enhancing existing components |
| `React.lazy` | Lazy-loading component code |
| Context | Sharing values across a component tree |

### Example

If you need reusable authentication state:

```jsx
useAuth()
```

may be more natural in modern React.

If you need to enhance many existing components with a wrapper:

```jsx
withAuth(Component)
```

can be useful, especially in older/class-based codebases.

---

# 34. Advanced Industry Architecture

A production React application may combine all these concepts.

Example:

```text
                    React Application
                           │
                           ▼
                     React Router
                           │
          ┌────────────────┼────────────────┐
          ▼                ▼                ▼
        Home           Dashboard          Admin
                           │                │
                           ▼                ▼
                    Lazy-loaded       Lazy-loaded
                       chunk              chunk
                           │                │
                           ▼                ▼
                      Suspense          Suspense
                           │                │
                           ▼                ▼
                      Components       Components
                           │
                           ▼
                    Custom Hooks
```

Authentication may be applied around protected sections:

```text
Request /dashboard
       │
       ▼
Authentication
       │
       ▼
Route
       │
       ▼
Lazy Load Dashboard
       │
       ▼
Suspense
       │
       ▼
Dashboard UI
```

This is a realistic mental model for a larger React application.

---

# 35. Final Practical Project

# Project: SmartPortal — Performance-Optimized React Application

Build a production-style React application demonstrating:

```text
React Router
+
Lazy Loading
+
Code Splitting
+
Suspense
+
Error Boundary
+
HOC
+
Protected Routes
```

---

## Required Pages

```text
/
 /about
 /products
 /products/:productId
 /dashboard
 /dashboard/profile
 /dashboard/reports
 /admin
 /login
 *
```

---

## Required Architecture

```text
src/
│
├── components/
│   ├── Navbar.jsx
│   ├── PageLoader.jsx
│   └── ErrorFallback.jsx
│
├── pages/
│   ├── Home.jsx
│   ├── About.jsx
│   ├── Products.jsx
│   ├── ProductDetails.jsx
│   ├── Dashboard.jsx
│   ├── Profile.jsx
│   ├── Reports.jsx
│   ├── Admin.jsx
│   ├── Login.jsx
│   └── NotFound.jsx
│
├── hoc/
│   ├── withAuth.jsx
│   ├── withLoading.jsx
│   └── withLogger.jsx
│
├── layouts/
│   └── DashboardLayout.jsx
│
├── App.jsx
├── main.jsx
└── index.css
```

---

## Requirement 1 — Lazy Routes

Lazy-load:

```text
About
Products
ProductDetails
Dashboard
Reports
Admin
```

Example:

```jsx
const Dashboard = lazy(() =>
  import("./pages/Dashboard")
);
```

---

## Requirement 2 — Suspense

Create:

```jsx
function PageLoader() {
  return <h2>Loading page...</h2>;
}
```

Use:

```jsx
<Suspense fallback={<PageLoader />}>
  <Routes>
    ...
  </Routes>
</Suspense>
```

---

## Requirement 3 — Dynamic Product Route

Create:

```text
/products/:productId
```

Use:

```jsx
useParams()
```

---

## Requirement 4 — Protected Dashboard

Create:

```jsx
withAuth(Dashboard)
```

or an equivalent protected-route architecture.

---

## Requirement 5 — Nested Routes

Create:

```text
/dashboard
/dashboard/profile
/dashboard/reports
```

Use:

```jsx
<Outlet />
```

---

## Requirement 6 — HOC Logging

Create:

```jsx
withLogger(Component)
```

and log:

```text
Rendering Dashboard
Rendering Reports
```

---

## Requirement 7 — Error Handling

Create an Error Boundary for important lazy-loaded application areas.

Display:

```text
Something went wrong.
Please refresh the page or try again.
```

---

## Requirement 8 — Loading Experience

Use a proper fallback:

```text
Loading Dashboard...
```

or a skeleton UI.

---

# 36. Practice Tasks

## Beginner Advanced Task 1

Create one lazy-loaded component:

```text
Profile
```

---

## Task 2

Create two lazy-loaded components:

```text
Profile
Settings
```

and wrap both in one `Suspense`.

---

## Task 3

Create separate Suspense boundaries for:

```text
Profile
Reports
```

Compare the user experience.

---

## Task 4

Convert all major React Router pages into lazy-loaded routes.

---

## Task 5

Create:

```jsx
PageLoader
```

and reuse it across routes.

---

## Task 6

Create:

```jsx
withLogger()
```

---

## Task 7

Create:

```jsx
withLoading()
```

---

## Task 8

Create:

```jsx
withAuth()
```

---

## Task 9

Create:

```jsx
withRole()
```

for:

```text
admin
teacher
student
```

---

## Task 10 — Final Challenge

Build a:

> **Lazy-Loaded Admin Dashboard**

Requirements:

```text
Login
  ↓
Authentication
  ↓
Dashboard
  ├── Users
  ├── Reports
  ├── Analytics
  ├── Settings
  └── Profile
```

Requirements:

- Lazy-loaded routes
- Suspense
- Loading UI
- Error boundary
- Protected routes
- Dynamic route
- HOC
- Nested routes
- Responsive UI
- Proper folder structure

---

# 37. Interview Questions

## Beginner

### 1. What is lazy loading?

Loading code or assets only when they are needed rather than loading everything initially.

### 2. What is code splitting?

Dividing an application's code into smaller independently loadable chunks.

### 3. What is `React.lazy()`?

An API that allows a React component to be loaded through a dynamic import.

### 4. What is Suspense?

A React mechanism that allows a fallback UI to be shown while supported asynchronous work is not yet ready.

### 5. Why is Suspense used with `React.lazy()`?

Because the lazy component may not be available immediately.

### 6. What is a dynamic import?

An asynchronous JavaScript `import()` expression that loads a module when executed.

### 7. What is a HOC?

A function that accepts a component and returns an enhanced component.

### 8. Does a HOC modify the original component?

A well-designed HOC should normally not mutate the original component.

---

## Intermediate

### 9. Why is route-based code splitting useful?

Because users often need only the code associated with the route they are currently visiting.

### 10. Can multiple lazy components share one Suspense boundary?

Yes.

### 11. Can one application have multiple Suspense boundaries?

Yes.

### 12. What is the difference between lazy loading and code splitting?

Code splitting is the broader technique of dividing code into chunks; lazy loading is the strategy of loading a chunk only when needed.

### 13. What happens if a lazy-loaded chunk fails?

The application should provide appropriate error handling, often using an Error Boundary around the relevant UI.

### 14. What is a named export?

An export that must be imported by its exported name:

```jsx
export function Reports() {}
```

### 15. What does `React.lazy()` expect from the imported module?

It expects the lazy module to resolve to a component through its default export shape.

### 16. Why are HOCs useful?

They can reuse cross-cutting behavior across components.

### 17. What does `{...props}` do in a HOC?

It forwards received props to the wrapped component.

### 18. Why should HOCs not be created during render?

Because creating a new component type during every render can cause unnecessary remounting and performance/reconciliation problems.

### 19. Are HOCs still common in modern React?

They remain supported and useful, especially in existing codebases and certain cross-cutting patterns, but custom Hooks and composition are often preferred for new logic reuse.

### 20. Does lazy loading always improve performance?

No. It can reduce initial JavaScript, but excessive splitting can add network requests and loading delays. Performance should be measured.

---

# 38. Quick Revision

## Code Splitting

```text
Large Application
       ↓
Split into chunks
       ↓
Load chunks when needed
```

## Dynamic Import

```jsx
import("./module")
```

## React.lazy

```jsx
const Component = lazy(() =>
  import("./Component")
);
```

## Suspense

```jsx
<Suspense fallback={<Loader />}>
  <Component />
</Suspense>
```

## Route-Based Splitting

```text
Home
 ↓
Dashboard clicked
 ↓
Dashboard chunk
 ↓
Dashboard rendered
```

## HOC

```text
Component
    ↓
HOC
    ↓
Enhanced Component
```

---

# 39. Final Checklist

Before completing this module, make sure you can:

- [ ] Explain code splitting
- [ ] Explain bundling
- [ ] Explain dynamic imports
- [ ] Use `React.lazy`
- [ ] Use `Suspense`
- [ ] Create loading UI
- [ ] Create route-based code splitting
- [ ] Lazy-load React Router pages
- [ ] Explain chunk loading
- [ ] Understand lazy-loading trade-offs
- [ ] Handle lazy loading errors
- [ ] Understand default vs named exports
- [ ] Create a Higher-Order Component
- [ ] Forward props through an HOC
- [ ] Create an authentication HOC
- [ ] Create a loading HOC
- [ ] Create a permission HOC
- [ ] Create a logging HOC
- [ ] Explain HOCs vs custom Hooks
- [ ] Build the SmartPortal practical

---

# Final Mental Model

Remember these five concepts:

```text
1. CODE SPLITTING
   ↓
   Divide application code into smaller chunks.

2. DYNAMIC IMPORT
   ↓
   Load a module asynchronously when needed.

3. REACT.LAZY
   ↓
   Turn a dynamically imported component into a lazy React component.

4. SUSPENSE
   ↓
   Show fallback UI while supported lazy content is waiting.

5. HOC
   ↓
   Reuse cross-cutting component behavior by wrapping components.
```

The production-oriented flow is:

```text
                    User opens application
                              │
                              ▼
                       Initial JavaScript
                              │
                              ▼
                         React Router
                              │
                    ┌─────────┴─────────┐
                    ▼                   ▼
                 Current             Other
                  route               routes
                    │                   │
                    ▼                   │
              Lazy-loaded               │
                 chunk                  │
                    │                   │
                    ▼                   │
                Suspense                │
                    │                   │
                    ▼                   │
              Page renders              │
                                        │
                         User navigates later
                                        │
                                        ▼
                              Another lazy chunk
                                        │
                                        ▼
                                     Render
```

This is one of the key transitions from **learning React** to **building large React applications**.

---

## End of Advanced React Performance & Reusability Module

### Recommended Next Step

Do not only read this module.

Build the **SmartPortal** project and verify the browser's Network tab while navigating between routes.

Look for:

```text
Initial JavaScript
        ↓
Navigate to Dashboard
        ↓
New JavaScript chunk requested
        ↓
Dashboard renders
```

That observation makes code splitting and lazy loading much easier to understand in practice.
