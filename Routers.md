# 🚀 React Router – Real-Time Practical Project

> **Level:** Beginner → Intermediate  
> **Technology:** React.js + React Router  
> **Project Type:** Real-World Multi-Page SPA  
> **Recommended For:** React Beginners

---

# 📌 Project: TechStore – React Routing Application

In this practical project, we will build a small **TechStore website**.

The application will have multiple pages:

```text
Home
Products
Product Details
About
Contact
Login
Dashboard
404 Not Found
```

Instead of creating separate HTML files for every page, we will use **React Router**.

---

# 🎯 What You Will Learn

After completing this project, you will understand:

- What routing means
- Why React applications need routing
- What React Router is
- How to install React Router
- How to create routes
- How to create navigation
- How to use `Link`
- How to use `NavLink`
- How to create dynamic routes
- How to read URL parameters
- How to create nested routes
- How to redirect users
- How to create a 404 page
- How to protect routes
- How to create a basic dashboard
- How routing works in a real project

---

# 🧠 1. What Is Routing?

Imagine a normal website:

```text
https://example.com/
https://example.com/products
https://example.com/about
https://example.com/contact
```

Each URL represents a different page.

In a React Single Page Application, we usually don't want the browser to completely reload the application every time the user changes pages.

React Router allows us to display different React components based on the current URL.

For example:

```text
URL                         Component

/                           Home
/products                   Products
/about                      About
/contact                    Contact
/login                      Login
/dashboard                  Dashboard
```

---

# 🌐 2. Real-Life Example

Think about an online shopping website.

A user visits:

```text
/shop
```

They see all products.

Then they click:

```text
Laptop
```

The URL becomes:

```text
/shop/laptop
```

The application displays the laptop details.

Then they click:

```text
Reviews
```

The URL might become:

```text
/shop/laptop/reviews
```

This is routing.

---

# 🏗️ 3. Create the React Project

Create a React application:

```bash
npm create vite@latest techstore
```

Select:

```text
React
JavaScript
```

Go inside the project:

```bash
cd techstore
```

Install dependencies:

```bash
npm install
```

Install React Router:

```bash
npm install react-router-dom
```

Start the application:

```bash
npm run dev
```

---

# 📁 4. Project Structure

We will create the following structure:

```text
techstore/
│
├── src/
│   │
│   ├── components/
│   │   ├── Navbar.jsx
│   │   └── ProductCard.jsx
│   │
│   ├── pages/
│   │   ├── Home.jsx
│   │   ├── Products.jsx
│   │   ├── ProductDetails.jsx
│   │   ├── About.jsx
│   │   ├── Contact.jsx
│   │   ├── Login.jsx
│   │   ├── Dashboard.jsx
│   │   └── NotFound.jsx
│   │
│   ├── App.jsx
│   ├── main.jsx
│   └── index.css
│
├── package.json
└── vite.config.js
```

---

# 🧩 5. Understanding Components

We divide our application into:

```text
Components
    ↓
Reusable UI

Pages
    ↓
Different application screens
```

For example:

```text
Navbar
```

is a component because it can be reused.

But:

```text
Home
Products
About
Contact
```

are pages.

---

# 🏠 6. Create Home Page

Create:

```text
src/pages/Home.jsx
```

Code:

```jsx
function Home() {
  return (
    <div>
      <h1>Welcome to TechStore 🚀</h1>

      <p>
        Your one-stop shop for laptops, mobiles and accessories.
      </p>
    </div>
  );
}

export default Home;
```

---

# 🛍️ 7. Create Products Page

Create:

```text
src/pages/Products.jsx
```

```jsx
function Products() {
  return (
    <div>
      <h1>Products</h1>

      <div>
        <h2>MacBook Pro</h2>
        <p>₹1,50,000</p>
      </div>

      <div>
        <h2>iPhone 17</h2>
        <p>₹80,000</p>
      </div>

      <div>
        <h2>AirPods</h2>
        <p>₹20,000</p>
      </div>
    </div>
  );
}

export default Products;
```

---

# ℹ️ 8. Create About Page

Create:

```text
src/pages/About.jsx
```

```jsx
function About() {
  return (
    <div>
      <h1>About TechStore</h1>

      <p>
        TechStore is a demo e-commerce application
        created for learning React Router.
      </p>
    </div>
  );
}

export default About;
```

---

# 📞 9. Create Contact Page

Create:

```text
src/pages/Contact.jsx
```

```jsx
function Contact() {
  return (
    <div>
      <h1>Contact Us</h1>

      <p>Email: support@techstore.com</p>

      <p>Phone: +91 9876543210</p>
    </div>
  );
}

export default Contact;
```

---

# 🔐 10. Create Login Page

Create:

```text
src/pages/Login.jsx
```

```jsx
function Login() {
  return (
    <div>
      <h1>Login</h1>

      <input
        type="email"
        placeholder="Enter email"
      />

      <br />

      <input
        type="password"
        placeholder="Enter password"
      />

      <br />

      <button>
        Login
      </button>
    </div>
  );
}

export default Login;
```

---

# 📊 11. Create Dashboard Page

Create:

```text
src/pages/Dashboard.jsx
```

```jsx
function Dashboard() {
  return (
    <div>
      <h1>Admin Dashboard</h1>

      <p>Total Products: 150</p>

      <p>Total Orders: 250</p>

      <p>Total Customers: 1200</p>
    </div>
  );
}

export default Dashboard;
```

---

# ❌ 12. Create 404 Page

Create:

```text
src/pages/NotFound.jsx
```

```jsx
function NotFound() {
  return (
    <div>
      <h1>404 😢</h1>

      <p>
        Sorry, the page you are looking for does not exist.
      </p>
    </div>
  );
}

export default NotFound;
```

---

# 🧭 13. Create Navbar

Create:

```text
src/components/Navbar.jsx
```

```jsx
import { Link } from "react-router-dom";

function Navbar() {
  return (
    <nav>
      <Link to="/">Home</Link>{" "}

      <Link to="/products">Products</Link>{" "}

      <Link to="/about">About</Link>{" "}

      <Link to="/contact">Contact</Link>{" "}

      <Link to="/login">Login</Link>{" "}

      <Link to="/dashboard">Dashboard</Link>
    </nav>
  );
}

export default Navbar;
```

---

# 🔥 14. Understanding Link

Instead of:

```html
<a href="/products">
  Products
</a>
```

React Router provides:

```jsx
<Link to="/products">
  Products
</Link>
```

Why?

Because React Router can change the displayed page without performing a traditional full-page navigation.

---

# 🚦 15. Create Routes

Open:

```text
src/App.jsx
```

Add:

```jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";

import Navbar from "./components/Navbar";

import Home from "./pages/Home";
import Products from "./pages/Products";
import About from "./pages/About";
import Contact from "./pages/Contact";
import Login from "./pages/Login";
import Dashboard from "./pages/Dashboard";
import NotFound from "./pages/NotFound";

function App() {
  return (
    <BrowserRouter>

      <Navbar />

      <Routes>

        <Route
          path="/"
          element={<Home />}
        />

        <Route
          path="/products"
          element={<Products />}
        />

        <Route
          path="/about"
          element={<About />}
        />

        <Route
          path="/contact"
          element={<Contact />}
        />

        <Route
          path="/login"
          element={<Login />}
        />

        <Route
          path="/dashboard"
          element={<Dashboard />}
        />

        <Route
          path="*"
          element={<NotFound />}
        />

      </Routes>

    </BrowserRouter>
  );
}

export default App;
```

---

# 🧠 16. Understand Routes

This:

```jsx
<Route
  path="/products"
  element={<Products />}
/>
```

means:

```text
URL
 ↓
/products

React Router
 ↓

Products Component
```

Similarly:

```jsx
<Route
  path="/about"
  element={<About />}
/>
```

means:

```text
/about
   ↓
About.jsx
```

---

# 🗺️ 17. Our Application Routing Map

```text
                    TechStore
                       │
                       ▼
                 React Router
                       │
        ┌──────────────┼───────────────┐
        │              │               │
        ▼              ▼               ▼
      Home          Products          About
        │              │
        │              ▼
        │        Product Details
        │
        ├──────── Contact
        │
        ├──────── Login
        │
        └──────── Dashboard
```

---

# 🔥 18. Dynamic Routing

Now we want to display individual products.

For example:

```text
/products/101
/products/102
/products/103
```

Instead of creating a separate route for every product, we can create a dynamic route.

---

# 🧩 19. Create Product Details Page

Create:

```text
src/pages/ProductDetails.jsx
```

```jsx
import { useParams } from "react-router-dom";

function ProductDetails() {

  const { id } = useParams();

  return (
    <div>

      <h1>Product Details</h1>

      <p>
        Product ID: {id}
      </p>

    </div>
  );
}

export default ProductDetails;
```

---

# 🚦 20. Add Dynamic Route

Inside `App.jsx`:

```jsx
<Route
  path="/products/:id"
  element={<ProductDetails />}
/>
```

Now:

```text
/products/101
```

will produce:

```text
Product ID: 101
```

And:

```text
/products/500
```

will produce:

```text
Product ID: 500
```

---

# 🧠 21. Understanding `:id`

This:

```text
/products/:id
```

means:

```text
/products/
       +
    dynamic value
```

Examples:

```text
/products/101
/products/200
/products/laptop
/products/iphone
```

The value is available through:

```jsx
useParams()
```

---

# 🛒 22. Real E-Commerce Example

Imagine we have:

```text
Product ID = 101
Product Name = MacBook Pro
```

The URL could be:

```text
/products/101
```

React Router gives us:

```jsx
const { id } = useParams();
```

Then we could fetch:

```text
GET /api/products/101
```

from our backend.

This is exactly the kind of pattern used in real-world applications.

---

# 🔗 23. Add Product Links

Update `Products.jsx`:

```jsx
import { Link } from "react-router-dom";

function Products() {

  return (
    <div>

      <h1>Products</h1>

      <div>
        <h2>MacBook Pro</h2>

        <p>₹1,50,000</p>

        <Link to="/products/101">
          View Product
        </Link>
      </div>

      <div>
        <h2>iPhone 17</h2>

        <p>₹80,000</p>

        <Link to="/products/102">
          View Product
        </Link>
      </div>

    </div>
  );
}

export default Products;
```

Now the user can click:

```text
View Product
```

and navigate to:

```text
/products/101
```

---

# ⭐ 24. NavLink

React Router also provides:

```jsx
NavLink
```

It is useful when we want to highlight the active page.

Example:

```jsx
import { NavLink } from "react-router-dom";

function Navbar() {

  return (
    <nav>

      <NavLink to="/">
        Home
      </NavLink>

      <NavLink to="/products">
        Products
      </NavLink>

      <NavLink to="/about">
        About
      </NavLink>

    </nav>
  );
}

export default Navbar;
```

---

# 🎨 25. Active Navigation

We can check whether a link is active:

```jsx
<NavLink
  to="/products"
  className={({ isActive }) =>
    isActive ? "active" : ""
  }
>
  Products
</NavLink>
```

Meaning:

```text
If current URL = /products
        ↓
isActive = true
        ↓
class = active
```

---

# 🪜 26. Nested Routing

Real applications often have sections inside sections.

For example:

```text
/dashboard
/dashboard/profile
/dashboard/orders
/dashboard/settings
```

This is called nested routing.

---

# 📊 27. Dashboard Structure

Our dashboard can become:

```text
Dashboard
│
├── Overview
├── Profile
├── Orders
└── Settings
```

URLs:

```text
/dashboard
/dashboard/profile
/dashboard/orders
/dashboard/settings
```

---

# 🧩 28. Create Dashboard Components

Create:

```text
src/pages/DashboardHome.jsx
```

```jsx
function DashboardHome() {
  return (
    <div>
      <h2>Dashboard Overview</h2>

      <p>Welcome to the admin dashboard.</p>
    </div>
  );
}

export default DashboardHome;
```

Create:

```text
src/pages/Orders.jsx
```

```jsx
function Orders() {
  return (
    <div>
      <h2>Orders</h2>

      <p>Order #1001</p>
      <p>Order #1002</p>
      <p>Order #1003</p>
    </div>
  );
}

export default Orders;
```

Create:

```text
src/pages/Profile.jsx
```

```jsx
function Profile() {
  return (
    <div>
      <h2>Profile</h2>

      <p>Name: Admin User</p>

      <p>Email: admin@techstore.com</p>
    </div>
  );
}

export default Profile;
```

---

# 🏗️ 29. Nested Route Configuration

We can configure routes like this:

```jsx
<Route
  path="/dashboard"
  element={<Dashboard />}
>

  <Route
    index
    element={<DashboardHome />}
  />

  <Route
    path="orders"
    element={<Orders />}
  />

  <Route
    path="profile"
    element={<Profile />}
  />

</Route>
```

Notice:

```jsx
path="orders"
```

not:

```jsx
path="/dashboard/orders"
```

React Router automatically understands that it is inside:

```text
/dashboard
```

So the final URL becomes:

```text
/dashboard/orders
```

---

# 🧠 30. Outlet

Nested routes need:

```jsx
<Outlet />
```

Update `Dashboard.jsx`:

```jsx
import { Outlet, Link } from "react-router-dom";

function Dashboard() {

  return (
    <div>

      <h1>Admin Dashboard</h1>

      <nav>

        <Link to="/dashboard">
          Overview
        </Link>

        {" | "}

        <Link to="/dashboard/orders">
          Orders
        </Link>

        {" | "}

        <Link to="/dashboard/profile">
          Profile
        </Link>

      </nav>

      <hr />

      <Outlet />

    </div>
  );
}

export default Dashboard;
```

---

# 🧠 31. What Does Outlet Do?

Think of:

```jsx
<Outlet />
```

as a placeholder.

For example:

```text
Dashboard
│
├── Navbar
│
└── <Outlet />
```

When user visits:

```text
/dashboard/orders
```

React Router places:

```text
Orders
```

inside:

```jsx
<Outlet />
```

So:

```text
Dashboard
   +
Orders
```

are displayed together.

---

# 🔐 32. Protected Routes

Now comes an important real-world concept.

Imagine:

```text
/dashboard
```

should only be available to logged-in users.

We don't want:

```text
Random user
     ↓
/dashboard
     ↓
❌ Access denied
```

Instead:

```text
Logged in?
   │
   ├── YES → Dashboard
   │
   └── NO → Login
```

---

# 🛡️ 33. Create ProtectedRoute

Create:

```text
src/components/ProtectedRoute.jsx
```

```jsx
import { Navigate } from "react-router-dom";

function ProtectedRoute({ children }) {

  const isLoggedIn = false;

  if (!isLoggedIn) {
    return <Navigate to="/login" />;
  }

  return children;
}

export default ProtectedRoute;
```

---

# 🔒 34. Protect Dashboard

In `App.jsx`:

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

Now:

```text
/dashboard
      ↓
ProtectedRoute
      ↓
Is user logged in?
      ↓
NO
      ↓
/login
```

---

# ⚠️ Important

This:

```jsx
const isLoggedIn = false;
```

is only for learning.

In a real application, authentication would normally come from something like:

```text
Context
Redux
JWT
Session
Cookies
Backend API
Authentication Provider
```

Never trust only frontend routing for actual security.

**The backend must also enforce authorization.**

---

# ↩️ 35. Navigate Programmatically

Sometimes navigation happens after an action.

For example:

```text
Login
 ↓
Login successful
 ↓
Go to Dashboard
```

We can use:

```jsx
useNavigate()
```

Example:

```jsx
import { useNavigate } from "react-router-dom";

function Login() {

  const navigate = useNavigate();

  function handleLogin() {

    // Login logic

    navigate("/dashboard");
  }

  return (
    <div>

      <h1>Login</h1>

      <button onClick={handleLogin}>
        Login
      </button>

    </div>
  );
}

export default Login;
```

---

# 🧠 36. Understanding useNavigate

This:

```jsx
navigate("/dashboard");
```

means:

```text
Change current route
        ↓
/dashboard
```

It is useful after:

```text
Login
Logout
Form submission
Payment
Registration
Creating a product
Deleting an item
```

---

# ❌ 37. 404 Route

At the end of our routes:

```jsx
<Route
  path="*"
  element={<NotFound />}
/>
```

The `*` means:

```text
Any URL that doesn't match
```

For example:

```text
/random
/hello
/abc
/testing
```

will show:

```text
404 Page
```

---

# 🧪 38. Final Route Map

Our application now has:

```text
/
│
├── /products
│       │
│       └── /products/:id
│
├── /about
│
├── /contact
│
├── /login
│
└── /dashboard
        │
        ├── /
        ├── /orders
        └── /profile
```

---

# 🔄 39. Complete Application Flow

```text
                    USER
                      │
                      ▼
                 React App
                      │
                      ▼
                React Router
                      │
          ┌───────────┼───────────┐
          │           │           │
          ▼           ▼           ▼
         Home      Products      Login
                      │
                      ▼
               Product Details
                      │
                      ▼
                /products/:id


Login
  │
  ▼
Authentication
  │
  ▼
Dashboard
  │
  ├── Overview
  ├── Orders
  └── Profile
```

---

# 🏆 40. Real-Time Industry Scenario

Imagine you are working for an e-commerce company.

Your application has:

```text
Customer Website
```

Routes:

```text
/
 /products
 /products/:id
 /cart
 /checkout
 /orders
 /profile
```

And an:

```text
Admin Panel
```

Routes:

```text
/admin
/admin/products
/admin/orders
/admin/customers
/admin/settings
```

Different users have different access.

```text
Customer
   ↓
Customer Routes

Admin
   ↓
Admin Routes
```

This is where React Router becomes extremely useful.

---

# 🧑‍💻 41. Student Practical Task

## Task 1 – Basic Routes

Create these routes:

```text
/
/products
/about
/contact
/login
```

---

## Task 2 – Navigation

Create a navbar containing:

```text
Home
Products
About
Contact
Login
```

Use:

```jsx
Link
```

or:

```jsx
NavLink
```

---

## Task 3 – Dynamic Route

Create:

```text
/products/:id
```

Display:

```text
Product ID
```

using:

```jsx
useParams()
```

Test:

```text
/products/101
/products/202
/products/999
```

---

## Task 4 – Dashboard

Create:

```text
/dashboard
/dashboard/orders
/dashboard/profile
/dashboard/settings
```

Use:

```jsx
Outlet
```

for nested routes.

---

## Task 5 – 404 Page

Create:

```text
404
```

for all invalid URLs.

Example:

```text
/random-page
```

---

## Task 6 – Protected Route

Create a protected dashboard.

If:

```js
isLoggedIn = false
```

redirect to:

```text
/login
```

If:

```js
isLoggedIn = true
```

allow:

```text
/dashboard
```

---

# 🧠 42. Interview Questions

### Beginner

**1. What is routing?**

Routing determines which UI/page should be displayed for a particular URL.

---

**2. What is React Router?**

React Router is a routing library used to handle navigation and URL-based UI rendering in React applications.

---

**3. What is BrowserRouter?**

```jsx
<BrowserRouter>
```

provides routing functionality to the React application.

---

**4. What is Route?**

```jsx
<Route />
```

defines a URL and the component that should render for that URL.

---

**5. What is Link?**

```jsx
<Link />
```

provides navigation between routes without using a normal full-page browser navigation.

---

# 🚀 Intermediate Questions

### 6. What is a dynamic route?

Example:

```text
/products/:id
```

It allows the route to accept dynamic values.

---

### 7. How do you read a URL parameter?

Using:

```jsx
useParams()
```

---

### 8. What is NavLink?

`NavLink` is similar to `Link`, but it can determine whether the current route is active.

---

### 9. What is Outlet?

`Outlet` renders the component associated with a nested child route.

---

### 10. What is useNavigate?

It allows programmatic navigation:

```jsx
const navigate = useNavigate();

navigate("/dashboard");
```

---

# 🔥 43. Mini Challenge

Build this application:

```text
             TechStore
                 │
       ┌─────────┼─────────┐
       │         │         │
      Home    Products    Login
                 │
        ┌────────┼────────┐
        │        │        │
     Laptop    Mobile   Headphones
        │
        ▼
 Product Details
        │
        ▼
     /products/:id
```

Add:

```text
Navbar
Dynamic Products
Product Details
404 Page
Login
Protected Dashboard
Nested Dashboard Routes
```

---

# 🎯 44. Expected Final Application

When the project is complete, your application should support:

```text
✅ Home page

✅ Products page

✅ Product details

✅ Dynamic URL parameters

✅ About page

✅ Contact page

✅ Login page

✅ Dashboard

✅ Nested dashboard routes

✅ Protected routes

✅ Navigation

✅ Active navigation

✅ 404 page
```

---

# 💡 45. Key Concepts to Remember

The most important React Router concepts are:

```text
BrowserRouter
      ↓
Routes
      ↓
Route
      ↓
Link / NavLink
      ↓
Dynamic Routes
      ↓
useParams
      ↓
Nested Routes
      ↓
Outlet
      ↓
useNavigate
      ↓
Navigate
      ↓
Protected Routes
```

---

# 🏁 Final Challenge

Now remove the hardcoded products and create:

```js
const products = [
  {
    id: 101,
    name: "MacBook Pro",
    price: 150000
  },
  {
    id: 102,
    name: "iPhone 17",
    price: 80000
  },
  {
    id: 103,
    name: "AirPods",
    price: 20000
  }
];
```

Render them using:

```jsx
.map()
```

Each product should have:

```text
Product Name
Price
View Details
```

Clicking:

```text
View Details
```

should navigate to:

```text
/products/101
/products/102
/products/103
```

Then use:

```jsx
useParams()
```

to get the ID.

---

# 🧑‍🏫 Trainer Note

This project teaches an important idea:

> **Routing is not just about changing pages. It is about designing how users move through an application.**

In a real production application, routing works together with:

```text
React
   +
React Router
   +
Authentication
   +
Authorization
   +
API
   +
State Management
   +
Backend
```

Once students understand this project, they are ready to move toward **authentication + API integration + protected admin dashboards**, which is where routing starts becoming genuinely useful rather than just a collection of URLs.

---

# 🚀 Project Extension

After completing this project, upgrade TechStore with:

```text
Phase 1
React Router
        ↓
Phase 2
Product API
        ↓
Phase 3
Login Authentication
        ↓
Phase 4
Protected Routes
        ↓
Phase 5
Admin Dashboard
        ↓
Phase 6
CRUD Products
        ↓
Phase 7
Cart
        ↓
Phase 8
Checkout
        ↓
Phase 9
Order Management
```

That turns a simple React Router exercise into a proper **real-world React application project**.
