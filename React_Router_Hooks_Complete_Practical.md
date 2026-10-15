# React Router + Hooks + CSS — Complete Practical Application

## Project: Student Management Portal

This practical builds a complete React application using **React Router, Router Hooks, reusable components, dynamic routes, query parameters, nested routes, forms, and responsive CSS**.

---

## 1. Learning Objectives

By completing this practical, students will learn:

- React Router installation and setup
- `BrowserRouter`, `Routes`, and `Route`
- `Link` and `NavLink`
- `useNavigate()`
- `useParams()`
- `useLocation()`
- `useSearchParams()`
- Dynamic routes
- Nested routes and `Outlet`
- Reusable React components
- Page/component organization
- Global CSS and responsive CSS
- Forms and navigation
- A simple dashboard application structure

---

# 2. Create the React Project

```bash
npm create vite@latest student-management
```

Select:

```text
Framework: React
Variant: JavaScript
```

Then:

```bash
cd student-management
npm install
npm install react-router-dom
npm run dev
```

Open the URL shown by Vite, normally:

```text
http://localhost:5173/
```

> Note: `npm run lint` is not required for this practical. If your `package.json` has no `lint` script, use `npm run dev` to start the application.

---

# 3. Final Project Structure

Create this structure:

```text
student-management/
├── public/
├── src/
│   ├── components/
│   │   ├── Navbar.jsx
│   │   └── StudentCard.jsx
│   ├── data/
│   │   └── students.js
│   ├── layouts/
│   │   └── DashboardLayout.jsx
│   ├── pages/
│   │   ├── Home.jsx
│   │   ├── Students.jsx
│   │   ├── StudentDetails.jsx
│   │   ├── About.jsx
│   │   ├── Login.jsx
│   │   ├── Dashboard.jsx
│   │   ├── Profile.jsx
│   │   └── Settings.jsx
│   ├── App.jsx
│   ├── main.jsx
│   └── index.css
├── package.json
└── vite.config.js
```

---

# 4. Student Data

Create `src/data/students.js`:

```javascript
export const students = [
  {
    id: 101,
    name: "Rahul Sharma",
    course: "Computer Engineering",
    year: "Final Year",
    email: "rahul@example.com",
    city: "Pune",
    skills: ["React", "JavaScript", "CSS"]
  },
  {
    id: 102,
    name: "Priya Patil",
    course: "Information Technology",
    year: "Third Year",
    email: "priya@example.com",
    city: "Mumbai",
    skills: ["Python", "React", "SQL"]
  },
  {
    id: 103,
    name: "Amit Joshi",
    course: "Computer Engineering",
    year: "Final Year",
    email: "amit@example.com",
    city: "Nashik",
    skills: ["Java", "React", "Git"]
  }
];
```

---

# 5. Global CSS

Replace `src/index.css` with:

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

:root {
  font-family: Arial, Helvetica, sans-serif;
  color: #1f2937;
  background: #f5f7fb;
}

body {
  min-width: 320px;
  min-height: 100vh;
  background: #f5f7fb;
}

a {
  text-decoration: none;
  color: inherit;
}

button,
input {
  font: inherit;
}

.container {
  width: min(1100px, 92%);
  margin: 0 auto;
}

.page {
  min-height: calc(100vh - 70px);
  padding: 50px 0;
}

.page-title {
  font-size: 36px;
  margin-bottom: 12px;
}

.page-subtitle {
  color: #6b7280;
  margin-bottom: 30px;
}

.btn {
  display: inline-block;
  padding: 12px 20px;
  border: none;
  border-radius: 8px;
  background: #2563eb;
  color: white;
  cursor: pointer;
  transition: 0.2s;
}

.btn:hover {
  background: #1d4ed8;
}

.btn-secondary {
  background: #111827;
}

.btn-secondary:hover {
  background: #374151;
}

.card {
  background: white;
  border-radius: 14px;
  padding: 24px;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.07);
}

.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}

/* Navbar */

.navbar {
  min-height: 70px;
  background: #111827;
  color: white;
}

.nav-container {
  width: min(1100px, 92%);
  min-height: 70px;
  margin: auto;

  display: flex;
  align-items: center;
  justify-content: space-between;
}

.logo {
  font-size: 22px;
  font-weight: bold;
}

.nav-links {
  display: flex;
  gap: 8px;
}

.nav-link {
  padding: 9px 14px;
  border-radius: 7px;
  color: #d1d5db;
}

.nav-link:hover {
  background: #1f2937;
  color: white;
}

.nav-link.active {
  background: #2563eb;
  color: white;
}

/* Hero */

.hero {
  min-height: 500px;
  display: flex;
  align-items: center;

  background: white;
  padding: 60px;
  border-radius: 20px;

  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.06);
}

.hero h1 {
  font-size: 52px;
  line-height: 1.1;
  margin: 12px 0 20px;
}

.hero p {
  max-width: 650px;
  color: #6b7280;
  font-size: 18px;
  line-height: 1.6;
}

.eyebrow {
  color: #2563eb !important;
  font-weight: bold;
}

.hero-actions {
  display: flex;
  gap: 12px;
  margin-top: 25px;
}

/* Student Cards */

.student-card {
  background: white;
  padding: 24px;
  border-radius: 14px;

  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.07);

  transition: transform 0.2s;
}

.student-card:hover {
  transform: translateY(-5px);
}

.student-avatar {
  width: 60px;
  height: 60px;

  display: flex;
  align-items: center;
  justify-content: center;

  margin-bottom: 15px;

  border-radius: 50%;
  background: #2563eb;
  color: white;

  font-size: 24px;
  font-weight: bold;
}

.student-card h2 {
  margin-bottom: 8px;
}

.student-card p {
  margin: 5px 0;
  color: #6b7280;
}

.student-card .btn {
  margin-top: 18px;
}

/* Search */

.search-box {
  margin-bottom: 30px;
}

.search-box input {
  width: 100%;
  max-width: 500px;

  padding: 14px 16px;

  border: 1px solid #d1d5db;
  border-radius: 8px;

  outline: none;
}

.search-box input:focus {
  border-color: #2563eb;
}

.empty-state {
  padding: 40px;
  text-align: center;

  background: white;
  border-radius: 12px;

  color: #6b7280;
}

/* Student Details */

.details-card {
  max-width: 700px;
  margin: auto;

  background: white;
  padding: 40px;

  border-radius: 16px;

  box-shadow: 0 5px 25px rgba(0, 0, 0, 0.08);
}

.large-avatar {
  width: 90px;
  height: 90px;

  display: flex;
  align-items: center;
  justify-content: center;

  border-radius: 50%;

  background: #2563eb;
  color: white;

  font-size: 36px;
  font-weight: bold;

  margin-bottom: 20px;
}

.details-card h1 {
  margin-bottom: 20px;
}

.details-card p {
  margin: 12px 0;
  color: #4b5563;
}

.details-card h3 {
  margin-top: 25px;
  margin-bottom: 12px;
}

.skills {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 25px;
}

.skills span {
  padding: 7px 12px;
  border-radius: 20px;
  background: #dbeafe;
  color: #1d4ed8;
}

/* Login */

.login-card {
  width: min(450px, 100%);
  margin: auto;

  background: white;
  padding: 35px;

  border-radius: 16px;

  box-shadow: 0 5px 25px rgba(0, 0, 0, 0.08);
}

.login-card h1 {
  margin-bottom: 8px;
}

.login-card p {
  color: #6b7280;
  margin-bottom: 25px;
}

.login-card label {
  display: block;
  margin-bottom: 6px;
  margin-top: 15px;
  font-weight: 600;
}

.login-card input {
  width: 100%;
  padding: 12px;
  border: 1px solid #d1d5db;
  border-radius: 8px;
}

.login-card button {
  width: 100%;
  margin-top: 25px;
}

/* Dashboard */

.dashboard-layout {
  min-height: calc(100vh - 70px);

  display: grid;
  grid-template-columns: 240px 1fr;
}

.dashboard-sidebar {
  background: #111827;
  color: white;
  padding: 25px;
}

.dashboard-sidebar h2 {
  margin-bottom: 30px;
}

.dashboard-sidebar nav {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.dashboard-sidebar a {
  padding: 12px;
  border-radius: 8px;
  color: #d1d5db;
}

.dashboard-sidebar a:hover,
.dashboard-sidebar a.active {
  background: #2563eb;
  color: white;
}

.dashboard-content {
  padding: 40px;
}

.dashboard-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  margin-top: 30px;
}

.dashboard-card {
  padding: 25px;

  background: white;
  border-radius: 14px;

  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.07);
}

.dashboard-card h2 {
  font-size: 32px;
  color: #2563eb;
}

/* Responsive */

@media (max-width: 800px) {
  .grid {
    grid-template-columns: 1fr 1fr;
  }

  .dashboard-layout {
    grid-template-columns: 1fr;
  }

  .dashboard-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 600px) {
  .nav-container {
    flex-direction: column;
    justify-content: center;
    gap: 5px;
  }

  .nav-links {
    flex-wrap: wrap;
    justify-content: center;
  }

  .hero {
    padding: 30px;
  }

  .hero h1 {
    font-size: 36px;
  }

  .hero-actions {
    flex-direction: column;
  }

  .grid {
    grid-template-columns: 1fr;
  }

  .dashboard-sidebar {
    padding: 15px;
  }

  .dashboard-sidebar nav {
    flex-direction: row;
    flex-wrap: wrap;
  }
}
```

---

# 6. Navbar Component

Create `src/components/Navbar.jsx`:

```jsx
import { NavLink } from "react-router-dom";

function Navbar() {
  return (
    <header className="navbar">
      <div className="nav-container">

        <NavLink to="/" className="logo">
          StudentHub
        </NavLink>

        <nav className="nav-links">

          <NavLink
            to="/"
            className={({ isActive }) =>
              isActive ? "nav-link active" : "nav-link"
            }
          >
            Home
          </NavLink>

          <NavLink
            to="/students"
            className={({ isActive }) =>
              isActive ? "nav-link active" : "nav-link"
            }
          >
            Students
          </NavLink>

          <NavLink
            to="/about"
            className={({ isActive }) =>
              isActive ? "nav-link active" : "nav-link"
            }
          >
            About
          </NavLink>

          <NavLink
            to="/login"
            className={({ isActive }) =>
              isActive ? "nav-link active" : "nav-link"
            }
          >
            Login
          </NavLink>

        </nav>

      </div>
    </header>
  );
}

export default Navbar;
```

---

# 7. Home Page

Create `src/pages/Home.jsx`:

```jsx
import { Link } from "react-router-dom";

function Home() {
  return (
    <main className="page">
      <div className="container">

        <section className="hero">

          <div>
            <p className="eyebrow">
              React Router Practical
            </p>

            <h1>
              Student Management
              <br />
              Portal
            </h1>

            <p>
              A practical React application demonstrating
              routing, hooks, reusable components and CSS.
            </p>

            <div className="hero-actions">

              <Link to="/students" className="btn">
                View Students
              </Link>

              <Link to="/about" className="btn btn-secondary">
                Learn More
              </Link>

            </div>
          </div>

        </section>

      </div>
    </main>
  );
}

export default Home;
```

---

# 8. StudentCard Component

Create `src/components/StudentCard.jsx`:

```jsx
import { Link } from "react-router-dom";

function StudentCard({ student }) {
  return (
    <article className="student-card">

      <div className="student-avatar">
        {student.name.charAt(0)}
      </div>

      <h2>{student.name}</h2>

      <p>{student.course}</p>
      <p>{student.year}</p>
      <p>{student.city}</p>

      <Link
        to={`/students/${student.id}`}
        className="btn"
      >
        View Details
      </Link>

    </article>
  );
}

export default StudentCard;
```

---

# 9. Students Page + Search

Create `src/pages/Students.jsx`:

```jsx
import { useSearchParams } from "react-router-dom";

import { students } from "../data/students";
import StudentCard from "../components/StudentCard";

function Students() {

  const [searchParams, setSearchParams] =
    useSearchParams();

  const search =
    searchParams.get("search") || "";

  const filteredStudents =
    students.filter((student) =>
      student.name
        .toLowerCase()
        .includes(search.toLowerCase())
    );

  const handleSearch = (event) => {

    const value = event.target.value;

    if (value) {
      setSearchParams({
        search: value
      });
    } else {
      setSearchParams({});
    }
  };

  return (
    <main className="page">

      <div className="container">

        <h1 className="page-title">
          Students
        </h1>

        <p className="page-subtitle">
          Search and view student information.
        </p>

        <div className="search-box">

          <input
            type="text"
            placeholder="Search student..."
            value={search}
            onChange={handleSearch}
          />

        </div>

        <div className="grid">

          {filteredStudents.map((student) => (
            <StudentCard
              key={student.id}
              student={student}
            />
          ))}

        </div>

        {filteredStudents.length === 0 && (
          <div className="empty-state">
            No students found.
          </div>
        )}

      </div>

    </main>
  );
}

export default Students;
```

### What is happening?

If the user searches `Rahul`, the URL becomes:

```text
/students?search=Rahul
```

Read it:

```jsx
searchParams.get("search")
```

Update it:

```jsx
setSearchParams({
  search: value
});
```

This is a practical example of `useSearchParams()`.

---

# 10. Student Details + Dynamic Route

Create `src/pages/StudentDetails.jsx`:

```jsx
import {
  Link,
  useParams
} from "react-router-dom";

import { students } from "../data/students";

function StudentDetails() {

  const { id } = useParams();

  const student = students.find(
    (student) => student.id === Number(id)
  );

  if (!student) {
    return (
      <main className="page">

        <div className="container">

          <h1>Student Not Found</h1>

          <Link
            to="/students"
            className="btn"
          >
            Back to Students
          </Link>

        </div>

      </main>
    );
  }

  return (
    <main className="page">

      <div className="container">

        <div className="details-card">

          <div className="large-avatar">
            {student.name.charAt(0)}
          </div>

          <h1>{student.name}</h1>

          <p>
            <strong>Student ID:</strong>{" "}
            {student.id}
          </p>

          <p>
            <strong>Course:</strong>{" "}
            {student.course}
          </p>

          <p>
            <strong>Year:</strong>{" "}
            {student.year}
          </p>

          <p>
            <strong>Email:</strong>{" "}
            {student.email}
          </p>

          <p>
            <strong>City:</strong>{" "}
            {student.city}
          </p>

          <h3>Skills</h3>

          <div className="skills">

            {student.skills.map((skill) => (
              <span key={skill}>
                {skill}
              </span>
            ))}

          </div>

          <Link
            to="/students"
            className="btn"
          >
            Back to Students
          </Link>

        </div>

      </div>

    </main>
  );
}

export default StudentDetails;
```

### Dynamic Route

The route will be:

```text
/students/:id
```

For:

```text
/students/101
```

this hook:

```jsx
const { id } = useParams();
```

returns:

```text
101
```

For:

```text
/students/102
```

it returns:

```text
102
```

---

# 11. About Page

Create `src/pages/About.jsx`:

```jsx
function About() {
  return (
    <main className="page">

      <div className="container">

        <div className="card">

          <h1 className="page-title">
            About StudentHub
          </h1>

          <p>
            StudentHub is a demonstration application
            created for learning React Router and
            React Router Hooks.
          </p>

          <br />

          <p>
            It demonstrates routing, dynamic URLs,
            query parameters, navigation, components,
            forms and responsive CSS.
          </p>

        </div>

      </div>

    </main>
  );
}

export default About;
```

---

# 12. Login Page + useNavigate()

Create `src/pages/Login.jsx`:

```jsx
import { useNavigate } from "react-router-dom";

function Login() {

  const navigate = useNavigate();

  const handleLogin = (event) => {

    event.preventDefault();

    // Real authentication would happen here.

    navigate("/dashboard");
  };

  return (
    <main className="page">

      <div className="container">

        <form
          className="login-card"
          onSubmit={handleLogin}
        >

          <h1>Login</h1>

          <p>
            Login to access the dashboard.
          </p>

          <label>Email</label>

          <input
            type="email"
            placeholder="Enter email"
            required
          />

          <label>Password</label>

          <input
            type="password"
            placeholder="Enter password"
            required
          />

          <button
            type="submit"
            className="btn"
          >
            Login
          </button>

        </form>

      </div>

    </main>
  );
}

export default Login;
```

### Why useNavigate?

After successful login:

```jsx
navigate("/dashboard");
```

changes the route programmatically.

Use it when navigation happens because of an action or result.

Examples:

```text
Login successful → Dashboard
Form submitted → Details
Logout → Login
Cancel → Previous page
Payment successful → Success page
```

---

# 13. Dashboard

Create `src/pages/Dashboard.jsx`:

```jsx
function Dashboard() {
  return (
    <div>

      <h1>Dashboard</h1>

      <p>
        Welcome to the StudentHub dashboard.
      </p>

      <div className="dashboard-grid">

        <div className="dashboard-card">
          <h2>103</h2>
          <p>Total Students</p>
        </div>

        <div className="dashboard-card">
          <h2>8</h2>
          <p>Courses</p>
        </div>

        <div className="dashboard-card">
          <h2>95%</h2>
          <p>Attendance</p>
        </div>

      </div>

    </div>
  );
}

export default Dashboard;
```

---

# 14. Dashboard Layout + Outlet

Create `src/layouts/DashboardLayout.jsx`:

```jsx
import {
  NavLink,
  Outlet
} from "react-router-dom";

function DashboardLayout() {
  return (
    <div className="dashboard-layout">

      <aside className="dashboard-sidebar">

        <h2>StudentHub</h2>

        <nav>

          <NavLink to="/dashboard">
            Overview
          </NavLink>

          <NavLink to="/dashboard/profile">
            Profile
          </NavLink>

          <NavLink to="/dashboard/settings">
            Settings
          </NavLink>

        </nav>

      </aside>

      <main className="dashboard-content">

        <Outlet />

      </main>

    </div>
  );
}

export default DashboardLayout;
```

### What is Outlet?

`Outlet` is the location where a child route renders.

Conceptually:

```text
DashboardLayout
       |
       +---- Sidebar
       |
       +---- Outlet
               |
               +---- Dashboard
               +---- Profile
               +---- Settings
```

---

# 15. Profile Page

Create `src/pages/Profile.jsx`:

```jsx
function Profile() {
  return (
    <div className="card">

      <h1>Profile</h1>

      <p>
        StudentHub user profile.
      </p>

    </div>
  );
}

export default Profile;
```

---

# 16. Settings Page

Create `src/pages/Settings.jsx`:

```jsx
function Settings() {
  return (
    <div className="card">

      <h1>Settings</h1>

      <p>
        Application settings.
      </p>

    </div>
  );
}

export default Settings;
```

---

# 17. App.jsx — Configure All Routes

Replace `src/App.jsx` with:

```jsx
import {
  Routes,
  Route,
  Navigate
} from "react-router-dom";

import Navbar from "./components/Navbar";

import Home from "./pages/Home";
import Students from "./pages/Students";
import StudentDetails from "./pages/StudentDetails";
import About from "./pages/About";
import Login from "./pages/Login";
import Dashboard from "./pages/Dashboard";
import Profile from "./pages/Profile";
import Settings from "./pages/Settings";

import DashboardLayout from "./layouts/DashboardLayout";

function App() {
  return (
    <>
      <Navbar />

      <Routes>

        {/* Public Routes */}

        <Route
          path="/"
          element={<Home />}
        />

        <Route
          path="/students"
          element={<Students />}
        />

        <Route
          path="/students/:id"
          element={<StudentDetails />}
        />

        <Route
          path="/about"
          element={<About />}
        />

        <Route
          path="/login"
          element={<Login />}
        />

        {/* Nested Dashboard Routes */}

        <Route
          path="/dashboard"
          element={<DashboardLayout />}
        >

          <Route
            index
            element={<Dashboard />}
          />

          <Route
            path="profile"
            element={<Profile />}
          />

          <Route
            path="settings"
            element={<Settings />}
          />

        </Route>

        {/* Unknown URL */}

        <Route
          path="*"
          element={
            <Navigate
              to="/"
              replace
            />
          }
        />

      </Routes>
    </>
  );
}

export default App;
```

---

# 18. main.jsx — BrowserRouter

Replace `src/main.jsx` with:

```jsx
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";

import {
  BrowserRouter
} from "react-router-dom";

import App from "./App.jsx";

import "./index.css";

createRoot(
  document.getElementById("root")
).render(
  <StrictMode>

    <BrowserRouter>
      <App />
    </BrowserRouter>

  </StrictMode>
);
```

---

# 19. How the Application Works

The complete flow is:

```text
Browser
   |
   v
BrowserRouter
   |
   v
App.jsx
   |
   v
Routes
   |
   +---- "/" --------------------> Home
   |
   +---- "/students" ------------> Students
   |
   +---- "/students/:id" --------> StudentDetails
   |
   +---- "/about" ---------------> About
   |
   +---- "/login" ---------------> Login
   |
   +---- "/dashboard" -----------> DashboardLayout
                                      |
                                      +--> Outlet
                                             |
                                             +--> Dashboard
                                             +--> Profile
                                             +--> Settings
```

---

# 20. Router Hooks Cheat Sheet

| Requirement | API |
|---|---|
| Enable routing | `BrowserRouter` |
| Define routes | `Routes` |
| Create a route | `Route` |
| Internal navigation | `Link` |
| Active navigation | `NavLink` |
| Navigate from code | `useNavigate()` |
| Read `/students/:id` | `useParams()` |
| Read current URL | `useLocation()` |
| Read/update `?search=react` | `useSearchParams()` |
| Render child route | `Outlet` |
| Parent route context | `useOutletContext()` |

---

# 21. Route Parameters vs Query Parameters

### Route parameter

URL:

```text
/students/101
```

Route:

```jsx
<Route
  path="/students/:id"
  element={<StudentDetails />}
/>
```

Read:

```jsx
const { id } = useParams();
```

Use route parameters when identifying a resource.

Examples:

```text
/products/25
/students/101
/orders/ORD1001
```

### Query parameter

URL:

```text
/students?search=Rahul
```

Read:

```jsx
const [searchParams] =
  useSearchParams();

const search =
  searchParams.get("search");
```

Use query parameters for:

```text
Search
Filtering
Sorting
Pagination
Optional settings
```

---

# 22. Link vs NavLink vs useNavigate

## Link

Use when the user should click a normal navigation link:

```jsx
<Link to="/students">
  Students
</Link>
```

## NavLink

Use for navigation menus where active styling matters:

```jsx
<NavLink to="/students">
  Students
</NavLink>
```

## useNavigate

Use when navigation happens inside JavaScript:

```jsx
const navigate = useNavigate();

navigate("/dashboard");
```

Simple rule:

```text
User clicks navigation
        ↓
Link / NavLink

Application logic causes navigation
        ↓
useNavigate()
```

---

# 23. Nested Routes

Our dashboard contains:

```text
/dashboard
/dashboard/profile
/dashboard/settings
```

Parent route:

```jsx
<Route
  path="/dashboard"
  element={<DashboardLayout />}
>
```

Child route:

```jsx
<Route
  path="profile"
  element={<Profile />}
/>
```

The child appears here:

```jsx
<Outlet />
```

This makes layouts reusable.

---

# 24. Protected Route Concept

Our current Login page is a demonstration only. It does **not** implement real authentication.

In a production application, you can create a protected route:

```jsx
import {
  Navigate
} from "react-router-dom";

function ProtectedRoute({ children }) {

  const isLoggedIn = true;

  if (!isLoggedIn) {
    return (
      <Navigate
        to="/login"
        replace
      />
    );
  }

  return children;
}
```

Concept:

```text
User requests Dashboard
        |
        v
Is user authenticated?
        |
     +--+--+
     |     |
    YES    NO
     |     |
 Dashboard Login
```

For a real project, `isLoggedIn` should come from actual authentication state.

---

# 25. Test the Application

Start:

```bash
npm run dev
```

Test every route.

### Home

```text
http://localhost:5173/
```

### Students

```text
http://localhost:5173/students
```

### Student 101

```text
http://localhost:5173/students/101
```

### Student 102

```text
http://localhost:5173/students/102
```

### Search

```text
http://localhost:5173/students?search=Rahul
```

### About

```text
http://localhost:5173/about
```

### Login

```text
http://localhost:5173/login
```

### Dashboard

```text
http://localhost:5173/dashboard
```

### Profile

```text
http://localhost:5173/dashboard/profile
```

### Settings

```text
http://localhost:5173/dashboard/settings
```

### Invalid route

```text
http://localhost:5173/anything
```

It should redirect to Home.

---

# 26. Common Errors

## Error: react-router-dom not found

Run:

```bash
npm install react-router-dom
```

---

## Error: Router hook used outside Router

Make sure `main.jsx` contains:

```jsx
<BrowserRouter>
  <App />
</BrowserRouter>
```

---

## Error: Dynamic route not working

Correct:

```jsx
<Route
  path="/students/:id"
  element={<StudentDetails />}
/>
```

Then visit:

```text
/students/101
```

Do not visit:

```text
/students/:id
```

---

## Error: CSS not working

Check:

```jsx
import "./index.css";
```

inside `main.jsx`.

---

## Error: Blank page

Check the browser console and terminal.

Common causes:

- Incorrect import path
- Incorrect component name
- Missing closing tag
- Missing export
- Wrong route
- Missing package installation

---

# 27. Practical Student Tasks

## Task 1 — Add Contact Page

Create:

```text
src/pages/Contact.jsx
```

Add:

```jsx
function Contact() {
  return (
    <main className="page">
      <div className="container">
        <div className="card">
          <h1>Contact Us</h1>
          <p>Email: support@example.com</p>
          <p>Phone: +91 9876543210</p>
          <p>Location: Pune</p>
        </div>
      </div>
    </main>
  );
}

export default Contact;
```

Add its route and Navbar link.

---

## Task 2 — Add a Student

Add another object to:

```text
src/data/students.js
```

---

## Task 3 — Student Search

Make the search work with:

```text
/students?search=studentName
```

Use:

```jsx
useSearchParams()
```

---

## Task 4 — Dynamic Student Details

Create:

```text
/students/:id
```

Use:

```jsx
useParams()
```

---

## Task 5 — Login Redirect

After form submission:

```text
/login
   ↓
useNavigate()
   ↓
/dashboard
```

---

## Task 6 — Dashboard

Add another dashboard page:

```text
/dashboard/attendance
```

Use nested routing and `Outlet`.

---

# 28. Final Student Challenge

Build your own application using the same architecture.

Choose one:

```text
College Management System
Job Portal
E-Commerce Store
Hospital Management System
Employee Management System
Course Management Portal
Photography Portfolio
Book Store
```

Minimum requirements:

- 5 pages
- Navbar
- Active navigation
- Responsive CSS
- 3 reusable components
- 2 dynamic routes
- Search/filter using query parameters
- Login page
- Dashboard
- Nested routes
- Proper folder structure
- Responsive mobile layout

---

# 29. Interview Questions

1. What is React Router?
2. Why do React applications need routing?
3. What is an SPA?
4. What is BrowserRouter?
5. What is Routes?
6. What is Route?
7. Difference between Link and NavLink?
8. Difference between Link and `<a>`?
9. What is useNavigate()?
10. What is useParams()?
11. What is a dynamic route?
12. What is useSearchParams()?
13. What is useLocation()?
14. What are nested routes?
15. What is Outlet?
16. What is a protected route?
17. Difference between route parameters and query parameters?
18. Why should reusable components be separated from pages?
19. Why should CSS be organized?
20. How would you protect a dashboard in a real application?

---

# 30. Trainer Explanation — Learn by Problem

Do not teach router hooks only as definitions.

Teach them through problems:

```text
"I need to create /about"
        ↓
Route

"I need a menu link"
        ↓
Link / NavLink

"I need the student ID from /students/101"
        ↓
useParams()

"I need to redirect after login"
        ↓
useNavigate()

"I need search/filter in the URL"
        ↓
useSearchParams()

"I need to know the current URL"
        ↓
useLocation()

"I need a common dashboard layout"
        ↓
Nested Routes + Outlet
```

This makes the API easier to understand and remember.

---

# 31. Final Architecture

```text
                         React Application
                                |
                         BrowserRouter
                                |
                              Routes
                                |
        +-----------------------+-----------------------+
        |                       |                       |
       Pages              Dynamic Routes          Dashboard
        |                       |                       |
   Components              useParams()            Nested Routes
        |                       |                       |
       CSS                useSearchParams()        Outlet
        |                       |
 Responsive UI              URL Search

                  Router Hooks
                       |
       +---------------+----------------+
       |               |                |
 useNavigate      useParams      useSearchParams
       |               |                |
 Navigation       Dynamic URL      Query String
```

---

# 32. Final Commands

From the project directory:

```bash
npm install
```

Install Router:

```bash
npm install react-router-dom
```

Start development server:

```bash
npm run dev
```

Build for production:

```bash
npm run build
```

Preview the production build:

```bash
npm run preview
```

---

# 33. What Students Should Know After This Practical

Students should now be able to explain and implement:

```text
React Router
    ↓
BrowserRouter
    ↓
Routes + Route
    ↓
Link + NavLink
    ↓
Dynamic Routing
    ↓
useParams()
    ↓
useNavigate()
    ↓
useSearchParams()
    ↓
useLocation()
    ↓
Nested Routes
    ↓
Outlet
    ↓
Reusable Components
    ↓
CSS
    ↓
Responsive UI
    ↓
Complete React Application
```

**End of Practical — React Router + Hooks + CSS**
