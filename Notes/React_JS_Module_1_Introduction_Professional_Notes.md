# React JS — Module 1: React Introduction

> **Professional beginner-friendly lecture notes**
>
> Goal: Understand what React is, why it exists, where it is used, how it works at a high level, and how to start a React project.

---

## 📚 Table of Contents

1. What is React?
2. React as a JavaScript Library
3. Why React Was Needed
4. Problems with Traditional UI Development
5. Where React is Used
6. Key Features of React
7. Component-Based Architecture
8. React and Single Page Applications
9. React and the Virtual DOM
10. How React Works — High Level
11. React Application Flow
12. React vs HTML/CSS/JavaScript
13. React vs Vanilla JavaScript
14. React Advantages
15. React Limitations
16. React Ecosystem
17. React Project Setup
18. Basic React Project Structure
19. First React Application
20. Ten Practical Examples
21. Interview Questions
22. Practice Tasks
23. Quick Revision
24. What's Next?

---

# 1. What is React?

**React** is a JavaScript library for building user interfaces.

It is especially useful for building modern, interactive web applications where the UI changes based on user actions and application data.

React allows developers to divide a large interface into smaller, reusable pieces called **components**.

### Simple definition

> React is a JavaScript library used to create reusable and interactive user interfaces using components.

### Example

A website can be divided into:

```text
Website
│
├── Navbar
├── Sidebar
├── Header
├── Main Content
│   ├── Card
│   ├── Card
│   └── Card
├── Login Form
└── Footer
```

Each part can become a React component.

---

# 2. React as a JavaScript Library

React is a **library**, not a complete programming language.

It focuses mainly on the **UI layer**.

```text
JavaScript
    ↓
React
    ↓
User Interface
```

React can be combined with other libraries and tools for:

- Routing
- API communication
- State management
- Styling
- Testing
- Authentication
- Build tools

For example:

```text
React
 + React Router
 + Axios / Fetch
 + Redux Toolkit
 + CSS / Tailwind
 + Vite
```

Together, these can form a complete modern frontend application.

---

# 3. Why Was React Needed?

Before React, developers commonly used:

- HTML
- CSS
- JavaScript
- DOM APIs
- jQuery

These technologies are still useful.

The problem appears when an application becomes large and highly interactive.

Imagine an e-commerce application containing:

```text
100 Products
Shopping Cart
Login
Search
Filters
Wishlist
Orders
Profile
Notifications
Admin Dashboard
```

There may be many UI elements that change frequently.

Managing all those changes manually can make the code difficult to maintain.

React provides a component-based approach that helps organize this complexity.

---

# 4. Problems with Traditional UI Development

Consider a counter.

Using normal JavaScript, you might manually update the DOM:

```javascript
let count = 0;

function increase() {
  count++;

  document.getElementById("count").innerText = count;
}
```

This works.

But a large application may have hundreds or thousands of UI updates.

You may need to manually manage:

- Which element changed
- What data changed
- Which UI should update
- Event handlers
- DOM references
- Repeated UI structures

React introduces a declarative approach.

Instead of manually saying:

```text
Find this element
Change this text
Hide this button
Show this section
Update this card
```

we describe the UI based on the current data/state.

Example:

```jsx
<h1>{count}</h1>
```

When the state changes, React handles the rendering process.

---

# 5. Where is React Used?

React can be used for many types of applications.

## Common examples

### 1. E-Commerce

```text
Amazon-like application
├── Products
├── Cart
├── Checkout
└── Orders
```

### 2. Admin Dashboard

```text
Dashboard
├── Users
├── Analytics
├── Reports
└── Settings
```

### 3. Job Portal

```text
Job Portal
├── Job Search
├── Job Details
├── Apply
├── Profile
└── Admin Panel
```

### 4. Social Media

```text
Social App
├── Feed
├── Posts
├── Comments
├── Messages
└── Profile
```

### 5. Learning Platform

```text
Learning Platform
├── Courses
├── Lessons
├── Quiz
├── Progress
└── Certificate
```

---

# 6. Key Features of React

Important React features include:

## 1. Components

Build UI using reusable components.

## 2. JSX

Write HTML-like UI syntax inside JavaScript.

## 3. Props

Pass data between components.

## 4. State

Store data that can change.

## 5. Hooks

Use React features inside function components.

## 6. Declarative UI

Describe what the UI should look like based on data.

## 7. Component Reusability

Create once and reuse many times.

## 8. Large Ecosystem

React works with many tools and libraries.

---

# 7. Component-Based Architecture

One of the most important React concepts is **components**.

Instead of creating one huge application file, we divide the UI.

Example:

```text
App
│
├── Navbar
├── Hero
├── ProductList
│   ├── ProductCard
│   ├── ProductCard
│   └── ProductCard
├── Contact
└── Footer
```

A component can be:

- Reused
- Tested
- Maintained
- Updated independently

Example:

```jsx
function Button() {
  return <button>Click Me</button>;
}
```

Use it:

```jsx
<Button />
<Button />
<Button />
```

---

# 8. React and Single Page Applications

React is commonly used to create **Single Page Applications (SPAs)**.

In an SPA, the browser can load the main application and then update the displayed content without requiring a complete page reload for every navigation.

Example:

```text
Application
│
├── Home
├── About
├── Products
├── Login
└── Dashboard
```

A routing library such as React Router can manage these views.

### Important

React itself is primarily a UI library.

Routing is commonly added using a routing solution such as **React Router**.

---

# 9. React and the Virtual DOM

The browser has a DOM (Document Object Model).

The DOM represents the HTML document.

React uses a Virtual DOM representation as part of its rendering architecture.

High-level idea:

```text
React UI
   ↓
Virtual DOM representation
   ↓
React determines required changes
   ↓
Browser DOM updates
```

The important beginner idea is:

> React helps efficiently update the UI when application data changes.

Do not think:

> "React updates the entire HTML page every time."

Instead, React determines what needs to change and updates the necessary DOM.

---

# 10. How React Works — High Level

A simplified flow:

```text
User Action
    ↓
Event Handler
    ↓
State/Data Changes
    ↓
React Re-renders
    ↓
React Determines UI Changes
    ↓
DOM Updates
    ↓
User Sees New UI
```

Example:

```text
User clicks +
      ↓
setCount(count + 1)
      ↓
State changes
      ↓
Component renders again
      ↓
UI displays new count
```

---

# 11. React Application Flow

A typical React application has this flow:

```text
Browser
   ↓
index.html
   ↓
main.jsx
   ↓
Root React Component
   ↓
App.jsx
   ↓
Child Components
   ↓
User Interaction
   ↓
State / Props
   ↓
UI Update
```

A simplified project may look like:

```text
my-react-app/
│
├── public/
├── src/
│   ├── App.jsx
│   ├── main.jsx
│   └── index.css
│
├── package.json
└── vite.config.js
```

We will study each file in detail in the next modules.

---

# 12. React vs HTML/CSS/JavaScript

React does not replace HTML, CSS, and JavaScript.

It works **with JavaScript** to build UI.

Think:

```text
HTML
 ↓
Structure

CSS
 ↓
Design

JavaScript
 ↓
Logic

React
 ↓
Component-based UI development
```

A React developer still needs strong JavaScript fundamentals.

---

# 13. React vs Vanilla JavaScript

## Vanilla JavaScript

You directly manipulate the DOM.

```javascript
document.getElementById("message").innerText = "Hello";
```

## React

You describe the UI using components and data.

```jsx
function App() {
  const message = "Hello";

  return <h1>{message}</h1>;
}
```

### Simple comparison

| Vanilla JavaScript | React |
|---|---|
| Direct DOM manipulation is common | React manages rendering |
| UI can become difficult to organize at scale | Components organize UI |
| Reusability must be designed manually | Components encourage reuse |
| State handling is manual | React provides state features |
| No built-in component model | Component-based architecture |

---

# 14. Advantages of React

## 1. Reusable Components

Write a component once and reuse it.

## 2. Easier UI Organization

Large interfaces can be divided into smaller components.

## 3. Declarative UI

Describe what the UI should display.

## 4. Strong Ecosystem

Many tools and libraries are available.

## 5. Large Community

A large developer community means many learning resources and packages.

## 6. Good Developer Tools

React Developer Tools can help inspect components and understand rendering behavior.

## 7. Suitable for Large Applications

With proper architecture, React can be used for complex applications.

---

# 15. Limitations of React

React is powerful, but it is not a solution for everything.

## 1. JavaScript Knowledge is Required

Students should understand JavaScript before React.

## 2. Ecosystem Can Be Confusing

There are many choices for:

```text
Routing
State Management
Styling
API calls
Forms
Testing
```

## 3. React Does Not Provide Everything

React mainly focuses on UI.

Other requirements often need additional tools.

## 4. Poor Architecture Can Still Create Problems

React does not automatically make an application well-designed.

Developers still need to understand:

- Component design
- State management
- Folder structure
- Performance
- Security
- Testing

---

# 16. React Ecosystem

React is often used with other technologies.

```text
                React
                  │
     ┌────────────┼────────────┐
     ↓            ↓            ↓
  Routing      API Calls     Styling
     │            │            │
React Router   Fetch/Axios   CSS/Tailwind
                  │
                  ↓
           Backend / API
                  │
                  ↓
              Database
```

Common technologies students may encounter:

| Requirement | Common Tool |
|---|---|
| UI | React |
| Build Tool | Vite |
| Routing | React Router |
| API | Fetch / Axios |
| Global State | Context / Redux Toolkit |
| Styling | CSS / Tailwind |
| Testing | Vitest / React Testing Library |
| Deployment | Vercel / Netlify / AWS |

---

# 17. React Project Setup

Modern React projects can be created using Vite.

## Step 1 — Check Node.js

```bash
node --version
```

## Step 2 — Check npm

```bash
npm --version
```

## Step 3 — Create React Application

```bash
npm create vite@latest my-react-app
```

Choose:

```text
Framework: React
Variant: JavaScript
```

## Step 4 — Enter Project

```bash
cd my-react-app
```

## Step 5 — Install Dependencies

```bash
npm install
```

## Step 6 — Start Development Server

```bash
npm run dev
```

---

# 18. Basic React Project Structure

A Vite React project commonly contains:

```text
my-react-app/
│
├── node_modules/
│
├── public/
│
├── src/
│   ├── assets/
│   ├── App.css
│   ├── App.jsx
│   ├── index.css
│   └── main.jsx
│
├── .gitignore
├── index.html
├── package.json
├── package-lock.json
└── vite.config.js
```

## Important files

### `index.html`

The HTML entry document.

### `main.jsx`

The JavaScript entry point where React is mounted.

### `App.jsx`

Usually the main application component.

### `index.css`

Global styles.

### `App.css`

Styles associated with the application in a basic Vite setup.

### `package.json`

Contains project metadata, dependencies, and scripts.

---

# 19. First React Application

A simple `App.jsx`:

```jsx
function App() {
  return (
    <div>
      <h1>Hello React!</h1>
      <p>My first React application.</p>
    </div>
  );
}

export default App;
```

A simplified `main.jsx`:

```jsx
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import App from "./App.jsx";

createRoot(document.getElementById("root")).render(
  <StrictMode>
    <App />
  </StrictMode>
);
```

---

# 20. Ten Practical Examples

These examples are intentionally simple. The goal is to understand what React can do before learning advanced concepts.

---

## Example 1 — Hello React

### Code

```jsx
function App() {
  return <h1>Hello React!</h1>;
}

export default App;
```

### What we learn

- React component
- JSX
- `return`
- Export

### Output

```text
Hello React!
```

---

## Example 2 — Personal Introduction

```jsx
function App() {
  return (
    <div>
      <h1>My Name is Sahil</h1>
      <p>I am learning React JS.</p>
    </div>
  );
}

export default App;
```

### What we learn

A component can return multiple elements by wrapping them inside a parent element.

---

## Example 3 — Simple Profile Card

```jsx
function App() {
  return (
    <div>
      <h2>Sahil Shaikh</h2>
      <p>Role: Developer</p>
      <p>Skill: React JS</p>
    </div>
  );
}

export default App;
```

### Real-world use

This is the beginning of reusable:

```text
ProfileCard
StudentCard
EmployeeCard
ProductCard
```

components.

---

## Example 4 — Product Card

```jsx
function App() {
  return (
    <div>
      <h2>Laptop</h2>
      <p>Price: ₹50,000</p>
      <button>Buy Now</button>
    </div>
  );
}

export default App;
```

### Real-world use

E-commerce applications contain many product cards.

---

## Example 5 — Multiple Components

```jsx
function Header() {
  return <h1>My Website</h1>;
}

function Footer() {
  return <p>Copyright 2026</p>;
}

function App() {
  return (
    <div>
      <Header />
      <main>
        <h2>Welcome</h2>
      </main>
      <Footer />
    </div>
  );
}

export default App;
```

### What we learn

One application can contain multiple components.

---

## Example 6 — Reusable Button

```jsx
function Button() {
  return <button>Click Me</button>;
}

function App() {
  return (
    <div>
      <Button />
      <Button />
      <Button />
    </div>
  );
}

export default App;
```

### What we learn

A component can be reused multiple times.

---

## Example 7 — Simple Dashboard

```jsx
function Navbar() {
  return <nav>Dashboard Navbar</nav>;
}

function Sidebar() {
  return <aside>Sidebar</aside>;
}

function Content() {
  return <main>Dashboard Content</main>;
}

function App() {
  return (
    <div>
      <Navbar />
      <Sidebar />
      <Content />
    </div>
  );
}

export default App;
```

### Structure

```text
App
├── Navbar
├── Sidebar
└── Content
```

This is how larger applications can be broken into smaller pieces.

---

## Example 8 — Login UI

```jsx
function Login() {
  return (
    <div>
      <h2>Login</h2>

      <input type="email" placeholder="Enter email" />

      <input
        type="password"
        placeholder="Enter password"
      />

      <button>Login</button>
    </div>
  );
}

function App() {
  return <Login />;
}

export default App;
```

### What we learn

React components can represent complete sections of an application.

---

## Example 9 — Student List

```jsx
function StudentList() {
  return (
    <div>
      <h2>Students</h2>

      <ul>
        <li>Rahul</li>
        <li>Priya</li>
        <li>Amit</li>
        <li>Neha</li>
      </ul>
    </div>
  );
}

function App() {
  return <StudentList />;
}

export default App;
```

### Future concept

Later we will replace the hard-coded list with JavaScript arrays and `.map()`.

---

## Example 10 — Simple Portfolio UI

```jsx
function Navbar() {
  return <nav>Portfolio</nav>;
}

function Hero() {
  return (
    <section>
      <h1>Hello, I'm a Developer</h1>
      <p>I build web applications.</p>
      <button>View Projects</button>
    </section>
  );
}

function Skills() {
  return (
    <section>
      <h2>Skills</h2>
      <p>JavaScript</p>
      <p>React</p>
      <p>Node.js</p>
    </section>
  );
}

function Footer() {
  return <footer>Thank You</footer>;
}

function App() {
  return (
    <>
      <Navbar />
      <Hero />
      <Skills />
      <Footer />
    </>
  );
}

export default App;
```

### Component structure

```text
App
│
├── Navbar
├── Hero
├── Skills
└── Footer
```

This example demonstrates the basic idea behind a real React application's component architecture.

---

# 21. Important Terminology

| Term | Meaning |
|---|---|
| React | JavaScript library for building UI |
| Component | Reusable UI building block |
| JSX | HTML-like syntax used in React |
| Props | Data passed to a component |
| State | Data managed by a component that can change |
| Hook | React function that provides React features |
| Virtual DOM | React's in-memory representation used during rendering |
| SPA | Single Page Application |
| DOM | Browser representation of an HTML document |
| Vite | Modern frontend build tool commonly used to create React projects |

---

# 22. Common Beginner Mistakes

## Mistake 1 — Incorrect Vite command

Wrong:

```bash
npm create vite@letest my-react-app
```

Correct:

```bash
npm create vite@latest my-react-app
```

---

## Mistake 2 — Forgetting to install dependencies

Run:

```bash
npm install
```

before starting a newly created project when needed.

---

## Mistake 3 — Not entering the project directory

Correct:

```bash
cd my-react-app
npm run dev
```

---

## Mistake 4 — Component names starting with lowercase

Avoid:

```jsx
function navbar() {
  return <nav>Navbar</nav>;
}
```

Prefer:

```jsx
function Navbar() {
  return <nav>Navbar</nav>;
}
```

React components should normally use **PascalCase**.

---

## Mistake 5 — Confusing JavaScript variables with React state

A normal variable:

```jsx
let count = 0;
```

is not the same as React state.

Later we will learn:

```jsx
const [count, setCount] = useState(0);
```

---

# 23. Interview Questions

## Beginner Questions

### 1. What is React?

React is a JavaScript library used to build user interfaces using reusable components.

### 2. Who created React?

React was created at Facebook and is maintained by Meta and the open-source community.

### 3. Is React a framework or library?

React is generally described as a JavaScript library focused on UI.

### 4. What is JSX?

JSX is a syntax extension that allows developers to write HTML-like syntax in JavaScript.

### 5. What is a component?

A component is a reusable building block of a React UI.

### 6. What is a SPA?

A Single Page Application is a web application where navigation and content updates can occur without a full browser page reload for every view.

### 7. What is Virtual DOM?

It is a lightweight in-memory representation used by React during its rendering process to determine necessary UI updates.

### 8. Why do we use components?

To divide an application into smaller, reusable, maintainable pieces.

### 9. Does React replace JavaScript?

No. React is built with and used through JavaScript.

### 10. What is Vite?

Vite is a modern frontend build tool that can be used to create and run React projects during development and production builds.

---

# 24. Practical Tasks

## Task 1 — Hello React

Create a React application that displays:

```text
Welcome to React JS
```

---

## Task 2 — Student Profile

Create a profile UI containing:

```text
Name
Age
Course
College
Skills
```

---

## Task 3 — Product Card

Create a product card with:

```text
Product Image
Product Name
Price
Description
Buy Now Button
```

---

## Task 4 — Dashboard

Create:

```text
Navbar
Sidebar
Dashboard Content
Footer
```

---

## Task 5 — Portfolio

Create:

```text
Navbar
Hero
About
Skills
Projects
Contact
Footer
```

Use separate React components for each section.

---

# 25. Mini Project — React Introduction Practice

## Project: Student Portfolio

Build a basic student portfolio using only concepts learned so far.

### Required components

```text
App
│
├── Navbar
├── Hero
├── About
├── Skills
├── Projects
├── Contact
└── Footer
```

### Requirements

- Use separate components.
- Use JSX.
- Use semantic HTML where appropriate.
- Add CSS.
- Keep components organized.
- Use meaningful component names.
- Make the page responsive.

### Suggested folder structure

```text
src/
│
├── components/
│   ├── Navbar.jsx
│   ├── Hero.jsx
│   ├── About.jsx
│   ├── Skills.jsx
│   ├── Projects.jsx
│   ├── Contact.jsx
│   └── Footer.jsx
│
├── App.jsx
├── main.jsx
└── index.css
```

---

# 26. Quick Revision

Remember these points:

```text
React
 ↓
JavaScript UI Library
 ↓
Build interactive interfaces
 ↓
Component-based architecture
 ↓
Reusable components
 ↓
JSX
 ↓
Props
 ↓
State
 ↓
Hooks
```

### Most important definitions

**React**

> A JavaScript library for building user interfaces.

**Component**

> A reusable building block of a React application.

**JSX**

> HTML-like syntax written inside JavaScript.

**Props**

> Data passed from one component to another.

**State**

> Data managed by a component that can change over time.

**Hook**

> A React function that lets function components use React features.

---

# 27. What's Next?

After React Introduction, the recommended sequence is:

```text
✅ React Introduction
        ↓
➡️ JSX
        ↓
Components
        ↓
Props
        ↓
Events
        ↓
Conditional Rendering
        ↓
Lists & Keys
        ↓
State
        ↓
Forms
        ↓
Hooks
        ↓
React Router
        ↓
API Integration
        ↓
Authentication
        ↓
State Management
        ↓
Advanced React
        ↓
Testing
        ↓
Deployment
```

---

# 🎯 Instructor Note

For this first lecture, students do **not** need to memorize advanced React concepts.

The main objective is to make students understand:

```text
Why React?
    ↓
What problem does React solve?
    ↓
What is a component?
    ↓
How does a React application work?
    ↓
Where is React used?
    ↓
How do we create our first React project?
```

Once this foundation is clear, the next lecture can focus on **JSX in detail**.

---

## React Learning Philosophy

> **Understand the problem → Learn the concept → Write code → Practice → Build**

React should be learned by building applications, not by memorizing APIs.
