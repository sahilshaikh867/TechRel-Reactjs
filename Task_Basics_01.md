# React JS Practical Task
## Create React App → Components → Routing → CSS

**Level:** Beginner  
**Duration:** 2–3 Hours  
**Topic:** React Project Structure, Components, Routing and CSS  
**Prerequisites:** Basic JavaScript, HTML and CSS

---

# 1. Learning Objectives

After completing this practical, students should understand:

- What React is and why we use it
- How to create a React application
- What files and folders are created by default
- Why each important file exists
- How React starts and renders the application
- What components are
- How to create custom components
- How to import and export components
- How to create folders for components
- How to create multiple pages
- How routing works in React
- How to install and use React Router
- How to navigate between pages
- How to add CSS to React components
- Difference between global CSS and component-specific CSS
- How to organize a React project properly

---

# 2. What is React?

React is a JavaScript library used to build user interfaces.

It is mainly used for creating:

- Websites
- Web applications
- Dashboards
- Admin panels
- E-commerce applications
- Social media applications
- Single Page Applications (SPAs)

React was originally developed by Facebook and is now maintained by Meta and the open-source community.

---

# 3. Why Do We Need React?

Imagine creating a large website using only HTML, CSS and JavaScript.

You may have:

```text
Header
Navbar
Sidebar
Cards
Buttons
Forms
Footer
```

If the same UI is required on multiple pages, you may have to write the same code again and again.

React solves this problem using:

```text
Components
```

For example:

```text
Navbar
   ↓
Reusable Component

Button
   ↓
Reusable Component

Card
   ↓
Reusable Component
```

We write the component once and reuse it wherever required.

---

# 4. Practical Task Overview

In this practical, you will create a small React website called:

```text
Student Portal
```

The application will contain:

```text
Home
About
Students
Contact
```

The final project structure will look approximately like:

```text
student-portal/
│
├── public/
│
├── src/
│   │
│   ├── components/
│   │   ├── Navbar.jsx
│   │   ├── Footer.jsx
│   │   └── StudentCard.jsx
│   │
│   ├── pages/
│   │   ├── Home.jsx
│   │   ├── About.jsx
│   │   ├── Students.jsx
│   │   └── Contact.jsx
│   │
│   ├── App.jsx
│   ├── main.jsx
│   ├── App.css
│   └── index.css
│
├── package.json
├── package-lock.json
└── vite.config.js
```

> Note: Modern React projects commonly use **Vite** instead of the older Create React App (`create-react-app`) setup. For this practical, use Vite unless your instructor specifically requires the older CRA workflow.

---

# 5. Task 1 — Create a React Application

## Step 1: Check Node.js

Open Terminal / PowerShell.

Run:

```bash
node -v
```

Then:

```bash
npm -v
```

You should see version numbers.

Example:

```text
Node: v22.x.x
npm: 10.x.x
```

If Node.js is not installed, install the current supported Node.js release first.

---

# 6. Create React App Using Vite

Run:

```bash
npm create vite@latest student-portal
```

You will be asked:

```text
Project name:
student-portal
```

Select:

```text
React
```

Then select:

```text
JavaScript
```

---

# 7. Navigate Into the Project

Run:

```bash
cd student-portal
```

Install dependencies:

```bash
npm install
```

Start the development server:

```bash
npm run dev
```

You will get a local URL similar to:

```text
http://localhost:5173/
```

Open it in your browser.

---

# 8. Understand the Default Project Structure

After creating the application, you will see something similar to:

```text
student-portal/
│
├── node_modules/
├── public/
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

Now let's understand what these files actually do.

---

# 9. `node_modules`

```text
node_modules/
```

This folder contains installed npm packages.

When you run:

```bash
npm install
```

npm downloads the dependencies required by the project.

For example:

```text
React
React DOM
Vite
```

and other packages.

## Important

Do NOT manually edit files inside `node_modules`.

Also do not normally upload it to GitHub.

That's why it is generally included in:

```text
.gitignore
```

---

# 10. `package.json`

This is one of the most important files in a Node/React project.

Example:

```json
{
  "name": "student-portal",
  "version": "0.0.0",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  }
}
```

It contains information about:

- Project name
- Project version
- Dependencies
- Development dependencies
- npm scripts

For example:

```bash
npm run dev
```

comes from the scripts section.

---

# 11. `package-lock.json`

This file records the exact dependency versions installed by npm.

It helps ensure that the project installs consistently on different machines and environments.

Normally:

```text
package.json
        ↓
Defines dependencies

package-lock.json
        ↓
Locks dependency versions
```

Do not manually modify it unless you know exactly why you are doing so.

---

# 12. `vite.config.js`

This file contains Vite configuration.

Example:

```javascript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
})
```

Vite is responsible for:

- Development server
- Fast development experience
- Building the application
- Handling modules
- React integration

---

# 13. `index.html`

This is the main HTML file.

You will usually see:

```html
<div id="root"></div>
```

This is extremely important.

React uses this element as the starting point for rendering the application.

Think of it as:

```text
HTML
 ↓
<div id="root">
 ↓
React Application
```

---

# 14. `src` Folder

The `src` folder contains most of your application source code.

```text
src/
```

This is where you will normally create:

```text
Components
Pages
CSS
JavaScript
Images
Utilities
Hooks
Services
```

For example:

```text
src/
│
├── components/
├── pages/
├── assets/
├── App.jsx
├── main.jsx
├── App.css
└── index.css
```

---

# 15. `main.jsx`

This is the entry point of the React application.

A typical file looks like:

```javascript
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import App from './App.jsx'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>,
)
```

Let's understand it.

---

## `import App`

```javascript
import App from './App.jsx'
```

This imports the main App component.

---

## `document.getElementById('root')`

```javascript
document.getElementById('root')
```

This finds:

```html
<div id="root"></div>
```

inside `index.html`.

---

## `createRoot()`

```javascript
createRoot(...)
```

This creates the React root.

---

## `.render()`

```javascript
.render(<App />)
```

This tells React:

```text
Render the App component inside root.
```

The basic flow is:

```text
index.html
     ↓
<div id="root">
     ↓
main.jsx
     ↓
App.jsx
     ↓
Other Components
     ↓
UI
```

---

# 16. `App.jsx`

`App.jsx` is usually the main application component.

Example:

```jsx
function App() {
  return (
    <h1>Hello React</h1>
  )
}

export default App
```

This component is imported into:

```text
main.jsx
```

and rendered.

---

# 17. What is a Component?

A component is a reusable piece of UI.

For example:

```text
Website
│
├── Navbar
├── Sidebar
├── Hero
├── Cards
├── Form
└── Footer
```

Each can become a React component.

Example:

```jsx
function Welcome() {
  return <h1>Welcome to Student Portal</h1>
}

export default Welcome
```

---

# 18. Why Components Matter

Without components:

```text
Huge App.jsx
1000+ lines
Hard to maintain
Hard to reuse
Hard to debug
```

With components:

```text
App
│
├── Navbar
├── Home
├── StudentCard
├── Footer
└── Contact
```

Benefits:

- Reusability
- Maintainability
- Better organization
- Easier debugging
- Team collaboration
- Cleaner code

---

# 19. Task 2 — Create Components Folder

Inside:

```text
src/
```

create:

```text
components/
```

Your structure becomes:

```text
src/
│
├── components/
│
├── App.jsx
├── App.css
├── index.css
└── main.jsx
```

---

# 20. Task 3 — Create Navbar Component

Inside:

```text
src/components/
```

create:

```text
Navbar.jsx
```

Add:

```jsx
function Navbar() {
  return (
    <nav>
      <h2>Student Portal</h2>

      <ul>
        <li>Home</li>
        <li>About</li>
        <li>Students</li>
        <li>Contact</li>
      </ul>
    </nav>
  )
}

export default Navbar
```

---

# 21. Import the Component

Open:

```text
App.jsx
```

Add:

```jsx
import Navbar from './components/Navbar'
```

Then:

```jsx
function App() {
  return (
    <>
      <Navbar />

      <h1>Welcome to Student Portal</h1>
    </>
  )
}

export default App
```

Now the Navbar component is displayed.

---

# 22. Component Import/Export

There are two important concepts:

## Export

```javascript
export default Navbar
```

## Import

```javascript
import Navbar from './components/Navbar'
```

Think of it as:

```text
Navbar.jsx
     ↓
export
     ↓
App.jsx
     ↓
import
     ↓
<Navbar />
```

---

# 23. Task 4 — Create Footer Component

Create:

```text
src/components/Footer.jsx
```

Code:

```jsx
function Footer() {
  return (
    <footer>
      <p>© 2026 Student Portal</p>
    </footer>
  )
}

export default Footer
```

Import it into:

```text
App.jsx
```

Then render:

```jsx
<Footer />
```

---

# 24. Task 5 — Create StudentCard Component

Create:

```text
src/components/StudentCard.jsx
```

Use:

```jsx
function StudentCard() {
  return (
    <div>
      <h3>Rahul Patil</h3>
      <p>Computer Engineering</p>
      <p>CGPA: 8.4</p>
    </div>
  )
}

export default StudentCard
```

Render it:

```jsx
<StudentCard />
```

---

# 25. What is JSX?

JSX allows us to write HTML-like syntax inside JavaScript.

Example:

```jsx
const name = "Rahul"

function App() {
  return (
    <h1>Hello {name}</h1>
  )
}
```

The JavaScript variable is inserted using:

```text
{ }
```

---

# 26. Task 6 — Create Pages Folder

Create:

```text
src/pages/
```

Inside it create:

```text
Home.jsx
About.jsx
Students.jsx
Contact.jsx
```

Final structure:

```text
src/
│
├── components/
│   ├── Navbar.jsx
│   ├── Footer.jsx
│   └── StudentCard.jsx
│
├── pages/
│   ├── Home.jsx
│   ├── About.jsx
│   ├── Students.jsx
│   └── Contact.jsx
│
├── App.jsx
├── App.css
├── index.css
└── main.jsx
```

---

# 27. Create Home Page

`Home.jsx`

```jsx
function Home() {
  return (
    <div>
      <h1>Home Page</h1>
      <p>Welcome to the Student Portal.</p>
    </div>
  )
}

export default Home
```

---

# 28. Create About Page

`About.jsx`

```jsx
function About() {
  return (
    <div>
      <h1>About Page</h1>
      <p>This portal is created using React JS.</p>
    </div>
  )
}

export default About
```

---

# 29. Create Students Page

`Students.jsx`

```jsx
import StudentCard from '../components/StudentCard'

function Students() {
  return (
    <div>
      <h1>Students</h1>

      <StudentCard />
      <StudentCard />
      <StudentCard />
    </div>
  )
}

export default Students
```

---

# 30. Create Contact Page

`Contact.jsx`

```jsx
function Contact() {
  return (
    <div>
      <h1>Contact Us</h1>

      <p>Email: support@studentportal.com</p>
      <p>Phone: +91 9876543210</p>
    </div>
  )
}

export default Contact
```

---

# 31. What is Routing?

Routing allows users to move between different pages/views of an application.

For example:

```text
/student
/about
/contact
```

Instead of manually changing HTML files, React can display different components based on the URL.

---

# 32. Why Do We Need React Router?

React applications are commonly Single Page Applications.

That means:

```text
One main HTML document
        ↓
Different UI views
        ↓
Different URLs
```

React Router helps us manage these URLs.

---

# 33. Install React Router

Run:

```bash
npm install react-router-dom
```

---

# 34. Configure BrowserRouter

Open:

```text
main.jsx
```

Import:

```jsx
import { BrowserRouter } from 'react-router-dom'
```

Then wrap your application:

```jsx
createRoot(document.getElementById('root')).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
)
```

Now React Router is available throughout the application.

---

# 35. Create Routes

Open:

```text
App.jsx
```

Import:

```jsx
import { Routes, Route } from 'react-router-dom'
```

Import pages:

```jsx
import Home from './pages/Home'
import About from './pages/About'
import Students from './pages/Students'
import Contact from './pages/Contact'
```

Then:

```jsx
function App() {
  return (
    <>
      <Navbar />

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/students" element={<Students />} />
        <Route path="/contact" element={<Contact />} />
      </Routes>

      <Footer />
    </>
  )
}

export default App
```

---

# 36. Understand Routes

This:

```jsx
<Route path="/" element={<Home />} />
```

means:

```text
URL:
/ 

Display:
Home component
```

This:

```jsx
<Route path="/about" element={<About />} />
```

means:

```text
URL:
/about

Display:
About component
```

Similarly:

```text
/students
/contact
```

---

# 37. Add Navigation

Instead of using normal:

```html
<a href="/about">
```

React Router provides:

```jsx
<Link to="/about">
  About
</Link>
```

Import:

```jsx
import { Link } from 'react-router-dom'
```

Update `Navbar.jsx`:

```jsx
import { Link } from 'react-router-dom'

function Navbar() {
  return (
    <nav>
      <h2>Student Portal</h2>

      <ul>
        <li>
          <Link to="/">Home</Link>
        </li>

        <li>
          <Link to="/about">About</Link>
        </li>

        <li>
          <Link to="/students">Students</Link>
        </li>

        <li>
          <Link to="/contact">Contact</Link>
        </li>
      </ul>
    </nav>
  )
}

export default Navbar
```

---

# 38. Why Use `<Link>`?

Using:

```html
<a href="/about">
```

can cause a normal browser navigation.

React Router's:

```jsx
<Link to="/about">
```

allows client-side navigation within the React application.

This helps preserve the SPA experience.

---

# 39. CSS in React

There are several ways to add CSS.

Common approaches include:

1. Global CSS
2. Component CSS files
3. CSS Modules
4. Inline styles
5. CSS-in-JS libraries

For beginners, start with:

```text
Global CSS
Component CSS
```

---

# 40. Method 1 — Global CSS

You already have:

```text
src/index.css
```

You can write:

```css
body {
  margin: 0;
  font-family: Arial, sans-serif;
}

h1 {
  color: #333;
}
```

This CSS can affect the entire application.

---

# 41. Method 2 — App.css

Create styles in:

```text
App.css
```

Example:

```css
.app {
  padding: 20px;
}

.title {
  font-size: 32px;
  margin-bottom: 20px;
}
```

Import:

```jsx
import './App.css'
```

Then:

```jsx
<div className="app">
  <h1 className="title">Student Portal</h1>
</div>
```

---

# 42. Important: `className`

In normal HTML:

```html
<div class="container">
```

In React JSX:

```jsx
<div className="container">
```

React uses:

```text
className
```

instead of:

```text
class
```

---

# 43. Method 3 — Component-Specific CSS

Create:

```text
src/components/Navbar.css
```

Add:

```css
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px 30px;
  background: #222;
}

.navbar ul {
  display: flex;
  gap: 20px;
  list-style: none;
}

.navbar a {
  color: white;
  text-decoration: none;
}
```

Then import it inside `Navbar.jsx`:

```jsx
import './Navbar.css'
```

Update:

```jsx
<nav className="navbar">
```

Now the Navbar has its own stylesheet.

---

# 44. Method 4 — Inline CSS

You can also write:

```jsx
<h1 style={{ color: "blue" }}>
  Student Portal
</h1>
```

Notice the double braces:

```text
{{ }}
```

The outer braces indicate JavaScript.

The inner braces represent the JavaScript object.

Example:

```jsx
style={{
  color: "blue",
  fontSize: "30px"
}}
```

---

# 45. Important Difference: CSS Property Names

Normal CSS:

```css
font-size: 30px;
background-color: blue;
```

Inline React style:

```jsx
style={{
  fontSize: "30px",
  backgroundColor: "blue"
}}
```

CSS properties become camelCase.

---

# 46. Recommended CSS Approach for Beginners

For small projects:

```text
index.css
    ↓
Global styles

App.css
    ↓
Application-level styles

Component.css
    ↓
Component-specific styles
```

Example:

```text
src/
│
├── components/
│   ├── Navbar.jsx
│   ├── Navbar.css
│   ├── Footer.jsx
│   └── Footer.css
│
├── pages/
│   ├── Home.jsx
│   ├── About.jsx
│   ├── Students.jsx
│   └── Contact.jsx
│
├── App.jsx
├── App.css
├── index.css
└── main.jsx
```

This is much cleaner than putting all CSS into one giant file.

---

# 47. Final Project Structure

Your completed project should approximately look like:

```text
student-portal/
│
├── node_modules/
│
├── public/
│
├── src/
│   │
│   ├── components/
│   │   ├── Navbar.jsx
│   │   ├── Navbar.css
│   │   ├── Footer.jsx
│   │   ├── Footer.css
│   │   └── StudentCard.jsx
│   │
│   ├── pages/
│   │   ├── Home.jsx
│   │   ├── About.jsx
│   │   ├── Students.jsx
│   │   └── Contact.jsx
│   │
│   ├── assets/
│   │
│   ├── App.jsx
│   ├── App.css
│   ├── index.css
│   └── main.jsx
│
├── .gitignore
├── index.html
├── package.json
├── package-lock.json
└── vite.config.js
```

---

# 48. Final Practical Assignment

## Build a Student Portal

Create a React application with the following requirements.

### Requirement 1 — Navbar

Create:

```text
Navbar.jsx
```

It must contain:

```text
Student Portal
Home
About
Students
Contact
```

---

### Requirement 2 — Routing

Create these routes:

```text
/
 /about
 /students
 /contact
```

Each route must display a different page.

---

### Requirement 3 — Home Page

The Home page should contain:

```text
Welcome to Student Portal

Manage your student information easily.

[View Students]
```

The button should navigate to:

```text
/students
```

---

### Requirement 4 — About Page

Display:

```text
About Student Portal

Student Portal is a React-based application
created for managing student information.
```

---

### Requirement 5 — Students Page

Create at least **3 Student Cards**.

Each card should contain:

```text
Student Name
Course
Year
CGPA
```

Example:

```text
Rahul Patil
Computer Engineering
Third Year
CGPA: 8.4
```

---

### Requirement 6 — Contact Page

Create a simple contact section:

```text
Email
Phone
Address
```

---

### Requirement 7 — CSS

The application must be styled.

Students should add:

- Navbar styling
- Page spacing
- Student cards
- Buttons
- Typography
- Hover effects
- Responsive layout

---

# 49. Bonus Challenge 🔥

Add a `StudentCard.css` file.

Create a card:

```css
.student-card {
  padding: 20px;
  border-radius: 10px;
  margin: 10px;
}
```

Add a hover effect:

```css
.student-card:hover {
  transform: translateY(-5px);
}
```

---

# 50. Bonus Challenge — Reusable Student Data

Instead of writing:

```jsx
<StudentCard />
<StudentCard />
<StudentCard />
```

create an array:

```javascript
const students = [
  {
    name: "Rahul",
    course: "Computer Engineering",
    cgpa: 8.4
  },
  {
    name: "Priya",
    course: "IT Engineering",
    cgpa: 9.1
  },
  {
    name: "Amit",
    course: "Computer Engineering",
    cgpa: 7.8
  }
]
```

Then use:

```jsx
students.map(...)
```

to generate the cards.

> This introduces students to the idea of reusable components and dynamic rendering.

---

# 51. Challenge — Active Navigation

Try to highlight the current page in the Navbar.

For example:

```text
Home
About
Students
Contact
```

When the user is on:

```text
/students
```

the Students link should visually appear active.

Hint:

Look into:

```javascript
NavLink
```

from:

```javascript
react-router-dom
```

---

# 52. Questions Students Must Answer

Before submitting the practical, answer these questions.

### Q1. What is React?

### Q2. Why do we use components?

### Q3. What is JSX?

### Q4. What is the purpose of `main.jsx`?

### Q5. What is the purpose of `App.jsx`?

### Q6. What is the purpose of `package.json`?

### Q7. Why should we not edit `node_modules` manually?

### Q8. What is React Router?

### Q9. Why do we use `<Link>` instead of normal `<a>` for internal React navigation?

### Q10. What is the difference between:

```html
class
```

and:

```jsx
className
```

### Q11. What is the purpose of CSS?

### Q12. What is the difference between global CSS and component-specific CSS?

### Q13. Why are reusable components useful?

### Q14. What does this code do?

```jsx
<Route path="/about" element={<About />} />
```

### Q15. Explain the React application flow:

```text
index.html
     ↓
main.jsx
     ↓
App.jsx
     ↓
Components / Pages
     ↓
Browser UI
```

---

# 53. Submission Checklist

Before submitting, verify:

- [ ] React application created successfully
- [ ] Project runs with `npm run dev`
- [ ] Navbar created
- [ ] Footer created
- [ ] StudentCard created
- [ ] Home page created
- [ ] About page created
- [ ] Students page created
- [ ] Contact page created
- [ ] React Router installed
- [ ] Routes working
- [ ] Navigation working
- [ ] CSS added
- [ ] Components have proper files
- [ ] No unnecessary code inside `App.jsx`
- [ ] No manual changes inside `node_modules`
- [ ] Project runs without console errors

---

# 54. Expected Final Architecture

The goal is to move from:

```text
Beginner React App

App.jsx
   ↓
Everything inside one file
```

to:

```text
Organized React Application

App
│
├── Navbar
│
├── Routes
│   ├── Home
│   ├── About
│   ├── Students
│   │    └── StudentCard
│   └── Contact
│
└── Footer
```

This is the beginning of proper React application architecture.

---

# 55. Key Takeaways

Remember these concepts:

```text
React
  ↓
Component-based UI

Component
  ↓
Reusable UI building block

App.jsx
  ↓
Main application component

main.jsx
  ↓
Application entry point

React Router
  ↓
URL-based navigation

Route
  ↓
URL → Component

Link
  ↓
Navigation between routes

CSS
  ↓
Styling the UI
```

The most important idea is:

> **Don't build the whole application in one giant component. Break the UI into small, reusable and maintainable components.**

---

# Practical Goal

By the end of this task, you should be able to independently create a React project, understand its default files, create reusable components, organize pages, configure routing, navigate between pages, and style your components using CSS.

**Next Recommended Topic:**  
`React Props → Passing Data Between Components → Dynamic Components → Rendering Lists with map()`
