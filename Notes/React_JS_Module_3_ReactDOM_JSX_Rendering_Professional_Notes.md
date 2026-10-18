# React JS — Module 3: ReactDOM, JSX & Rendering Elements

> **Level:** Beginner → Intermediate  
> **Prerequisites:** React Introduction + Environment Setup  
> **Recommended setup:** React + Vite

## Learning Objectives

By the end of this module, students will understand:

- ReactDOM and its purpose
- DOM vs ReactDOM
- `createRoot()` and `root.render()`
- JSX and JSX transformation
- JavaScript expressions inside JSX
- JSX attributes, `className`, `htmlFor`, and inline styles
- `props.children`
- React Elements
- Rendering and re-rendering
- Virtual DOM at a beginner level
- `createPortal()`
- Practical React UI examples

---

# 1. Module Overview

The previous modules covered React fundamentals and environment setup. Now we answer an important question:

> **How does React actually display our UI in the browser?**

The main concepts are:

```text
                    REACT UI
                       │
          ┌────────────┼────────────┐
          ↓            ↓            ↓
         JSX        ReactDOM    React Element
          │            │            │
          ↓            ↓            ↓
     UI Syntax     DOM Bridge    UI Description
                       │
                       ↓
                  Browser DOM
```

---

# 2. What is ReactDOM?

**ReactDOM is the package that connects React with the browser's DOM.**

React describes what the UI should look like, while ReactDOM provides browser-specific rendering APIs.

```text
React
  │
  │ UI description
  ↓
ReactDOM
  │
  │ render/update
  ↓
Browser DOM
  │
  ↓
Web Page
```

### Real-life analogy

```text
Chef          → React
Food order    → React Element
Waiter        → ReactDOM
Dining table  → DOM
Customer      → User
```

React prepares the UI description and ReactDOM helps connect that UI to the browser.

---

# 3. What is DOM?

DOM means:

> **Document Object Model**

When the browser loads HTML, it creates an object-based tree representing the page.

Example:

```html
<div>
  <h1>Hello</h1>
  <p>Welcome</p>
</div>
```

Conceptually:

```text
Document
   │
   └── div
       ├── h1
       │   └── "Hello"
       └── p
           └── "Welcome"
```

This is the **DOM tree**.

---

# 4. ReactDOM vs Browser DOM

| ReactDOM | Browser DOM |
|---|---|
| React package | Browser API |
| Provides React rendering APIs | Represents the webpage |
| Connects React with DOM | Contains actual DOM nodes |
| Works with React elements | Works with HTML elements |
| Modern API uses `createRoot()` | Uses APIs such as `document.getElementById()` |

---

# 5. Installing ReactDOM

In a standard Vite React project, `react-dom` is normally already installed.

Check `package.json`:

```json
{
  "dependencies": {
    "react": "...",
    "react-dom": "..."
  }
}
```

If needed:

```bash
npm install react-dom
```

or:

```bash
npm i react-dom
```

---

# 6. Modern ReactDOM API

For modern React applications:

```jsx
import { createRoot } from "react-dom/client";
```

Then:

```jsx
const root = createRoot(
  document.getElementById("root")
);

root.render(<App />);
```

### Important

Older tutorials may show:

```jsx
import ReactDOM from "react-dom";

ReactDOM.render(
  <App />,
  document.getElementById("root")
);
```

For modern React projects, prefer:

```jsx
import { createRoot } from "react-dom/client";
```

---

# 7. The Root Element

In Vite React applications, `index.html` normally contains:

```html
<div id="root"></div>
```

This is the mounting point of the React application.

```text
index.html
    │
    └── <div id="root">
             │
             ↓
       React Application
```

---

# 8. Understanding `main.jsx`

A typical Vite React entry file:

```jsx
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import "./index.css";
import App from "./App.jsx";

createRoot(document.getElementById("root")).render(
  <StrictMode>
    <App />
  </StrictMode>
);
```

### Step-by-step

1. Import React features.
2. Import `createRoot`.
3. Import the application component.
4. Find `<div id="root">`.
5. Create the React root.
6. Render `<App />`.

---

# 9. React Rendering Flow

```text
          index.html
              │
              ↓
       <div id="root">
              │
              ↓
          main.jsx
              │
              ↓
        createRoot()
              │
              ↓
         root.render()
              │
              ↓
           <App />
              │
              ↓
             JSX
              │
              ↓
       React Elements
              │
              ↓
      React Rendering
              │
              ↓
         Browser DOM
              │
              ↓
          User sees UI
```

---

# 10. What is JSX?

JSX means:

> **JavaScript XML**

JSX is a syntax extension used with React that allows HTML-like UI syntax inside JavaScript.

Example:

```jsx
const element = <h1>Hello World</h1>;
```

It looks like HTML, but it is JSX syntax.

---

# 11. Why JSX?

Without JSX:

```javascript
const element = React.createElement(
  "h1",
  null,
  "Hello World"
);
```

With JSX:

```jsx
const element = <h1>Hello World</h1>;
```

JSX makes UI code:

- Easier to read
- Easier to write
- Easier to maintain
- Easier to understand inside components

---

# 12. JSX is NOT HTML

JSX looks like HTML, but it is JavaScript syntax.

```text
JSX
 │
 ↓
Build transformation
 │
 ↓
JavaScript representation
 │
 ↓
React Element
 │
 ↓
React rendering
 │
 ↓
Browser DOM
```

---

# 13. How JSX Works

Consider:

```jsx
const element = <h1>Hello World</h1>;
```

Conceptually, a JSX transformation can produce something equivalent to:

```javascript
const element = React.createElement(
  "h1",
  null,
  "Hello World"
);
```

Modern JSX runtimes can generate different internal calls, but the beginner-level idea remains:

> **JSX is transformed into JavaScript that describes React elements.**

---

# 14. JSX Transformation Diagram

```text
┌──────────────────────────────┐
│ Developer writes JSX         │
│                              │
│ <h1>Hello</h1>               │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ Build transformation         │
│ Babel / React tooling        │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ JavaScript representation    │
│ of React UI                  │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ React rendering              │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ Browser DOM                  │
└──────────────────────────────┘
```

---

# 15. JSX Example 1 — Simple Heading

```jsx
function App() {
  return <h1>Hello React</h1>;
}

export default App;
```

---

# 16. JSX Example 2 — Multiple Elements

A component should return one parent structure.

```jsx
function App() {
  return (
    <div>
      <h1>React Course</h1>
      <p>Welcome to the course.</p>
    </div>
  );
}
```

Or use a Fragment:

```jsx
function App() {
  return (
    <>
      <h1>React Course</h1>
      <p>Welcome to the course.</p>
    </>
  );
}
```

---

# 17. JSX Example 3 — JavaScript Expressions

Use `{}` to insert JavaScript expressions.

```jsx
function App() {
  const name = "Sahil";

  return <h1>Hello, {name}</h1>;
}
```

Output:

```text
Hello, Sahil
```

---

# 18. JSX Example 4 — Arithmetic

```jsx
function App() {
  const a = 10;
  const b = 20;

  return <h1>Total: {a + b}</h1>;
}
```

Output:

```text
Total: 30
```

---

# 19. JSX Example 5 — Function Call

```jsx
function App() {
  const getName = () => "React Student";

  return <h1>Hello {getName()}</h1>;
}
```

---

# 20. JSX Example 6 — Object Data

```jsx
function App() {
  const student = {
    name: "Rahul",
    course: "React JS",
    age: 21
  };

  return (
    <div>
      <h2>{student.name}</h2>
      <p>{student.course}</p>
      <p>{student.age}</p>
    </div>
  );
}
```

---

# 21. JSX Example 7 — Conditional Rendering

```jsx
function App() {
  const isLoggedIn = true;

  return (
    <h1>
      {isLoggedIn ? "Welcome Back!" : "Please Login"}
    </h1>
  );
}
```

---

# 22. JSX Example 8 — Logical AND

```jsx
function App() {
  const isAdmin = true;

  return (
    <div>
      <h1>Dashboard</h1>

      {isAdmin && <button>Admin Panel</button>}
    </div>
  );
}
```

---

# 23. JSX Example 9 — List Rendering

```jsx
function App() {
  const skills = [
    "React",
    "JavaScript",
    "Node.js",
    "AWS"
  ];

  return (
    <ul>
      {skills.map((skill) => (
        <li key={skill}>{skill}</li>
      ))}
    </ul>
  );
}
```

---

# 24. JSX Example 10 — Reusable Card with Children

```jsx
function Card({ children }) {
  return (
    <div className="card">
      {children}
    </div>
  );
}

function App() {
  return (
    <Card>
      <h2>React Course</h2>
      <p>Learn React step by step.</p>
    </Card>
  );
}
```

---

# 25. JSX Attributes

HTML:

```html
<img src="profile.jpg" alt="Profile">
```

JSX:

```jsx
<img src="profile.jpg" alt="Profile" />
```

Many attributes are similar to HTML, but some names are different.

---

# 26. `className`

HTML:

```html
<div class="card"></div>
```

JSX:

```jsx
<div className="card"></div>
```

---

# 27. `htmlFor`

HTML:

```html
<label for="email">Email</label>
```

JSX:

```jsx
<label htmlFor="email">Email</label>
```

---

# 28. Inline Styling

JSX uses a JavaScript object for the `style` attribute:

```jsx
<div style={{ color: "red" }}>
  Hello
</div>
```

Multiple properties:

```jsx
<div
  style={{
    color: "blue",
    fontSize: "24px",
    backgroundColor: "lightgray"
  }}
>
  React
</div>
```

---

# 29. Dynamic JSX Attributes

```jsx
function App() {
  const imageUrl = "https://example.com/image.jpg";

  return (
    <img
      src={imageUrl}
      alt="Example"
    />
  );
}
```

The `{imageUrl}` tells JSX to use a JavaScript variable.

---

# 30. JSX Boolean Attributes

```jsx
const isDisabled = false;

<button disabled={isDisabled}>
  Submit
</button>
```

---

# 31. JSX Self-Closing Tags

Correct:

```jsx
<img src="photo.jpg" alt="Photo" />
```

```jsx
<input type="text" />
```

```jsx
<br />
```

---

# 32. JSX Comments

```jsx
function App() {
  return (
    <div>
      {/* This is a JSX comment */}
      <h1>Hello React</h1>
    </div>
  );
}
```

---

# 33. JSX Expressions vs Statements

Expressions can be placed inside `{}`:

```jsx
{10 + 20}
```

```jsx
{name}
```

```jsx
{user.name}
```

```jsx
{isLoggedIn ? "Logout" : "Login"}
```

A normal `if` statement cannot be directly written inside JSX:

```jsx
// ❌ Incorrect
{
  if (isLoggedIn) {
    return "Welcome";
  }
}
```

Use a ternary, logical `&&`, or calculate the value before returning JSX.

---

# 34. What are JSX Children?

Content placed between a component's opening and closing tags becomes `children`.

```jsx
function Card(props) {
  return (
    <div className="card">
      {props.children}
    </div>
  );
}
```

Usage:

```jsx
<Card>
  <h2>React Course</h2>
  <p>Welcome to React.</p>
</Card>
```

Diagram:

```text
<Card>
   │
   ├── <h2>React Course</h2>
   └── <p>Welcome to React</p>
   │
   ↓
props.children
   │
   ↓
Card Component
```

---

# 35. What is a React Element?

A React element is a lightweight JavaScript representation describing what should appear in the UI.

Example:

```jsx
const element = <h1>Hello React</h1>;
```

Think:

```text
React Element
      ↓
Description of UI
      ↓
React uses it during rendering
```

A React element is not the same thing as an actual browser DOM node.

---

# 36. React Element vs DOM Element

| React Element | DOM Element |
|---|---|
| JavaScript representation | Browser object |
| Lightweight | Actual browser DOM node |
| Describes UI | Exists in browser document |
| Used by React rendering | Managed by browser |

Example:

```jsx
const element = <h1>Hello</h1>;
```

After rendering, the browser contains an actual `<h1>` DOM node.

---

# 37. Rendering a React Element

```jsx
import { createRoot } from "react-dom/client";

const element = <h1>Hello React</h1>;

const root = createRoot(
  document.getElementById("root")
);

root.render(element);
```

---

# 38. Rendering a Component

```jsx
function App() {
  return <h1>Hello React</h1>;
}

const root = createRoot(
  document.getElementById("root")
);

root.render(<App />);
```

---

# 39. Complete Rendering Architecture

```text
                  Browser
                     │
                 index.html
                     │
              <div id="root">
                     │
                     ↓
                  main.jsx
                     │
                createRoot()
                     │
                     ↓
                  <App />
                     │
                     ↓
                    JSX
                     │
                     ↓
              React Elements
                     │
                     ↓
              React Renderer
                     │
                     ↓
              Virtual UI
                     │
              Compare changes
                     │
                     ↓
                 Real DOM
                     │
                     ↓
                User Interface
```

---

# 40. Virtual DOM — Beginner Explanation

The Virtual DOM is a conceptual representation of the UI that React uses to determine what needs to change.

Suppose the page contains:

```text
Heading
Paragraph
Button
```

When only the paragraph changes, React can determine the necessary update rather than manually rewriting unrelated parts.

Conceptually:

```text
Previous UI
   │
   ↓
Virtual representation
   │
   │ compare
   ↓
New UI
   │
   ↓
Determine changes
   │
   ↓
Update necessary DOM
```

---

# 41. Rendering vs Re-rendering

### Initial rendering

```text
React App
   ↓
Initial render
   ↓
Browser DOM
```

### Re-rendering

```text
State / Props change
       ↓
Component renders again
       ↓
React compares result
       ↓
Required DOM updates
```

---

# 42. Dynamic Counter Example

```jsx
import { useState } from "react";

function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>Counter: {count}</h1>

      <button onClick={() => setCount(count + 1)}>
        Increase
      </button>
    </div>
  );
}

export default App;
```

Flow:

```text
Button Click
    ↓
setCount()
    ↓
State changes
    ↓
App re-renders
    ↓
New JSX result
    ↓
React determines required update
    ↓
Counter text changes
```

---

# 43. Important ReactDOM APIs

## `createRoot()`

Creates a React root for rendering an application.

```jsx
import { createRoot } from "react-dom/client";

const root = createRoot(
  document.getElementById("root")
);

root.render(<App />);
```

## `root.render()`

Renders React content into the root.

```jsx
root.render(<App />);
```

## `createPortal()`

Allows React content to be rendered into another DOM node.

Typical use cases:

- Modal
- Dialog
- Tooltip
- Notification
- Overlay

Example:

```jsx
import { createPortal } from "react-dom";

function Modal() {
  return createPortal(
    <div className="modal">
      <h2>Login</h2>
    </div>,
    document.getElementById("modal-root")
  );
}
```

Diagram:

```text
Main React Tree
       │
       ├── App
       │    ├── Navbar
       │    └── Page
       │
       └── Modal
              │
              ↓
        Different DOM node
```

---

# 44. Older ReactDOM APIs

You may encounter older tutorials mentioning:

```text
ReactDOM.render()
findDOMNode()
unmountComponentAtNode()
hydrate()
```

These are legacy/older patterns or specialized APIs.

For modern React development, focus first on:

```text
createRoot()
root.render()
createPortal()
```

For server rendering and hydration, modern React applications use the appropriate current React DOM client/server APIs.

---

# 45. Ten Practical JSX Examples

## Example 1 — Greeting

```jsx
function App() {
  const name = "Sahil";

  return <h1>Hello, {name}!</h1>;
}
```

## Example 2 — Student Card

```jsx
function App() {
  const student = {
    name: "Rahul",
    course: "React JS",
    age: 21
  };

  return (
    <div>
      <h2>{student.name}</h2>
      <p>Course: {student.course}</p>
      <p>Age: {student.age}</p>
    </div>
  );
}
```

## Example 3 — Product Card

```jsx
function App() {
  const product = {
    name: "Laptop",
    price: 55000
  };

  return (
    <div>
      <h2>{product.name}</h2>
      <p>₹{product.price}</p>
    </div>
  );
}
```

## Example 4 — Conditional Login

```jsx
function App() {
  const isLoggedIn = true;

  return (
    <h1>
      {isLoggedIn ? "Welcome Back" : "Please Login"}
    </h1>
  );
}
```

## Example 5 — Dynamic Class

```jsx
function App() {
  const active = true;

  return (
    <div className={active ? "active" : "inactive"}>
      Account Status
    </div>
  );
}
```

## Example 6 — Dynamic Image

```jsx
function App() {
  const image =
    "https://images.unsplash.com/photo-1497366754035-f200968a6e72";

  return (
    <img
      src={image}
      alt="Workspace"
      width="400"
    />
  );
}
```

## Example 7 — Inline Styling

```jsx
function App() {
  const cardStyle = {
    padding: "20px",
    borderRadius: "10px",
    backgroundColor: "#f4f4f4"
  };

  return (
    <div style={cardStyle}>
      <h2>React Card</h2>
      <p>Styled using JSX.</p>
    </div>
  );
}
```

## Example 8 — List

```jsx
function App() {
  const skills = ["React", "JavaScript", "Node.js", "AWS"];

  return (
    <ul>
      {skills.map((skill) => (
        <li key={skill}>{skill}</li>
      ))}
    </ul>
  );
}
```

## Example 9 — Form

```jsx
function App() {
  return (
    <form>
      <label htmlFor="name">Name</label>

      <input
        id="name"
        type="text"
        placeholder="Enter your name"
      />

      <button type="submit">Submit</button>
    </form>
  );
}
```

## Example 10 — Children

```jsx
function Card({ children }) {
  return <div className="card">{children}</div>;
}

function App() {
  return (
    <Card>
      <h2>React Course</h2>
      <p>Learn React from beginner to advanced.</p>
    </Card>
  );
}
```

---

# 46. Practical Project — Student Profile Card

Build:

```text
┌──────────────────────────────┐
│        Student Profile       │
│                              │
│          [ Photo ]           │
│                              │
│  Name: Sahil                 │
│  Course: React JS            │
│  Level: Beginner             │
│  Skills: React, JS, AWS      │
│                              │
│       [ View Profile ]       │
└──────────────────────────────┘
```

Requirements:

- JSX
- JavaScript expressions
- JSX attributes
- `className`
- CSS
- Array + `.map()`
- `key`
- Button
- Conditional rendering

---

# 47. Practical Project — Product Card

Build:

```text
┌──────────────────────────────┐
│        Product Image         │
│                              │
│       Wireless Mouse         │
│       ₹799                   │
│                              │
│       ⭐ 4.5                 │
│                              │
│      [ Add to Cart ]         │
└──────────────────────────────┘
```

Data:

```javascript
const product = {
  name: "Wireless Mouse",
  price: 799,
  rating: 4.5,
  available: true
};
```

Display:

- Product name
- Price
- Rating
- Availability
- Button

---

# 48. Practical Project — Login Status UI

Use:

```javascript
const isLoggedIn = true;
```

If true:

```text
Welcome Back!
[ Dashboard ]
[ Logout ]
```

If false:

```text
Welcome Guest
[ Login ]
[ Register ]
```

Use:

- JSX
- Ternary operator
- Components
- Buttons
- `className`

---

# 49. Practical Project — Dashboard

Create:

```text
Dashboard
────────────────────────────

Welcome, Student!

┌──────────┐ ┌──────────┐
│ Courses  │ │ Projects │
│    5     │ │    8     │
└──────────┘ └──────────┘

Skills
• React
• JavaScript
• AWS
• Docker
```

Use JSX expressions and arrays.

---

# 50. Common JSX Mistakes

## Mistake 1 — `class`

Wrong:

```jsx
<div class="card">
```

Correct:

```jsx
<div className="card">
```

## Mistake 2 — Multiple Root Elements

Wrong:

```jsx
return (
  <h1>Hello</h1>
  <p>Welcome</p>
);
```

Correct:

```jsx
return (
  <>
    <h1>Hello</h1>
    <p>Welcome</p>
  </>
);
```

## Mistake 3 — Missing Closing Tag

Wrong:

```jsx
<img src="photo.jpg">
```

Correct:

```jsx
<img src="photo.jpg" />
```

## Mistake 4 — Incorrect Style

Wrong:

```jsx
<div style="color:red">
```

Correct:

```jsx
<div style={{ color: "red" }}>
```

## Mistake 5 — `if` directly inside JSX

Wrong:

```jsx
{
  if (isLoggedIn) {
    "Welcome"
  }
}
```

Use:

```jsx
{isLoggedIn ? "Welcome" : "Login"}
```

---

# 51. Debugging Checklist

If JSX is not working:

1. Check browser console.
2. Check terminal errors.
3. Check closing tags.
4. Check `className`.
5. Check `{}` placement.
6. Check component names.
7. Check imports.
8. Check exports.
9. Check `main.jsx`.
10. Check that the root element exists.

---

# 52. Interview Questions

## Beginner

1. What is ReactDOM?
2. What is JSX?
3. Is JSX HTML?
4. Why use `className` instead of `class`?
5. What is `createRoot()`?
6. What does `root.render()` do?
7. What is a React element?
8. What are JSX expressions?
9. What is `props.children`?
10. What is a Portal?

## Intermediate

1. Explain JSX transformation.
2. Explain React element vs DOM element.
3. Explain `createRoot()`.
4. What is the purpose of the root DOM element?
5. What causes a component to re-render?
6. Explain initial rendering vs re-rendering.
7. What is `createPortal()`?
8. Why are JSX attributes different from HTML attributes?
9. Why are old `ReactDOM.render()` tutorials different from modern React?
10. Explain the React rendering flow.

---

# 53. Industry Use Cases

## E-Commerce

```text
Product Data
     ↓
Product Component
     ↓
JSX
     ↓
React Element
     ↓
ReactDOM
     ↓
Browser UI
```

## Admin Dashboard

```text
API Data
   ↓
State
   ↓
Components
   ↓
JSX
   ↓
React Rendering
   ↓
Dashboard
```

## Social Media Feed

```text
Posts
 ↓
Array
 ↓
map()
 ↓
Post Components
 ↓
JSX
 ↓
UI
```

## Banking Application

```text
Account Data
 ↓
Components
 ↓
Conditional JSX
 ↓
React Rendering
 ↓
Customer Dashboard
```

---

# 54. Lecture Diagram

Use this on the board or slide:

```text
                    REACT APPLICATION
                           │
                           ↓
                         JSX
                           │
                           ↓
                    React Elements
                           │
                           ↓
                     React Renderer
                           │
                           ↓
                    Virtual UI
                           │
                     Compare changes
                           │
                           ↓
                      Browser DOM
                           │
                           ↓
                         USER
```

### Teacher explanation

> Developer writes JSX. React tooling transforms JSX into JavaScript. React uses the resulting element descriptions to determine the UI. ReactDOM provides the browser-specific APIs needed to render the React application into the DOM.

---

# 55. Complete Example

### `index.html`

```html
<div id="root"></div>
```

### `main.jsx`

```jsx
import { createRoot } from "react-dom/client";
import App from "./App.jsx";

createRoot(document.getElementById("root")).render(
  <App />
);
```

### `App.jsx`

```jsx
function App() {
  const name = "React Student";

  return (
    <div>
      <h1>Hello, {name}</h1>
      <p>Welcome to React JS.</p>
    </div>
  );
}

export default App;
```

### Complete Flow

```text
index.html
    │
    │ <div id="root">
    ↓
main.jsx
    │
    │ createRoot()
    ↓
<App />
    │
    ↓
JSX
    │
    ↓
React Elements
    │
    ↓
React Rendering
    │
    ↓
ReactDOM
    │
    ↓
Browser DOM
    │
    ↓
Screen
```

---

# 56. Assignment

## Task 1 — Personal Profile

Create a profile containing:

- Name
- Photo
- Education
- Skills
- Location
- About
- Button

## Task 2 — Product Cards

Create 3 product cards using an array and `.map()`.

Each card should contain:

- Image
- Product name
- Price
- Rating
- Availability
- Add to Cart button

## Task 3 — Student Dashboard

Create:

- Student name
- Total courses
- Completed courses
- Pending courses
- Skills
- Profile button

## Task 4 — Login UI

Use conditional rendering for:

- Logged-in user
- Logged-out user

## Task 5 — Reusable Card

Create:

```jsx
<Card>
  ...
</Card>
```

using:

```jsx
props.children
```

---

# 57. Challenge Task — Student Management UI

Build:

```text
Student Management
─────────────────────────────

Search Student

┌─────────────────────────────┐
│ Student Name                │
│ Course                      │
│ Skills                      │
│ Status                      │
│ [View Profile]              │
└─────────────────────────────┘
```

Use:

- JSX
- Components
- Props
- Children
- Arrays
- `.map()`
- Conditional rendering
- `className`
- JSX expressions

---

# 58. Quick Revision

```text
React
 ↓
UI Library

ReactDOM
 ↓
React ↔ Browser DOM bridge

JSX
 ↓
HTML-like syntax inside JavaScript

React Element
 ↓
Description of UI

createRoot()
 ↓
Creates React rendering root

root.render()
 ↓
Renders React UI

createPortal()
 ↓
Renders content into another DOM node

Re-render
 ↓
Updated UI description
 ↓
Necessary DOM updates
```

---

# 59. Command Cheat Sheet

Create project:

```bash
npm create vite@latest react-dom-demo
```

Install:

```bash
cd react-dom-demo
npm install
```

Run:

```bash
npm run dev
```

Install ReactDOM if needed:

```bash
npm install react-dom
```

---

# 60. What Students Should Remember

1. **ReactDOM connects React with the browser DOM.**
2. **JSX lets us write HTML-like UI syntax inside JavaScript.**
3. **JSX is transformed before browser execution.**
4. **A React element describes UI.**
5. **`createRoot()` creates a React rendering root.**
6. **`root.render()` renders React UI.**
7. **Use `className` instead of `class`.**
8. **Use `{}` for JavaScript expressions in JSX.**
9. **`props.children` represents nested component content.**
10. **React updates the DOM based on UI changes.**
11. **`createPortal()` is useful for modals and overlays.**
12. **Prefer current ReactDOM APIs over legacy tutorials.**

---

# 61. Next Module

## React Components

Recommended sequence:

```text
Components
   ↓
Functional Components
   ↓
Component Structure
   ↓
Reusable Components
   ↓
Component Composition
   ↓
Props
   ↓
Events
   ↓
Conditional Rendering
   ↓
Lists & Keys
```

This moves students from understanding React's rendering foundation to building reusable real-world React applications.
