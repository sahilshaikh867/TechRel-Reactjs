# React JS — Module 2: React Environment Setup

> **Professional beginner-friendly lecture notes**
>
> Goal: Set up a complete React development environment, create a React project using Vite, understand the project structure, install dependencies, run the development server, and understand alternative setup methods.

---

# 📚 Table of Contents

1. What is a React Development Environment?
2. Prerequisites
3. What is Node.js?
4. What is npm?
5. Checking Node.js and npm
6. Installing Node.js on Windows
7. Installing Node.js on Linux
8. Installing Node.js on macOS
9. Why Use Vite?
10. Creating a React Project with Vite
11. Step-by-Step Vite Setup
12. Understanding the Vite Project Structure
13. What is `package.json`?
14. What is `node_modules`?
15. What is `package-lock.json`?
16. Running the React Application
17. Understanding the Development Server
18. Stopping the Development Server
19. Installing Additional Packages
20. React Environment Setup — 10 Examples
21. Common Errors and Solutions
22. CRA — Create React App
23. Webpack + Babel
24. Vite vs CRA vs Webpack
25. Practical Tasks
26. Interview Questions
27. Quick Revision
28. What's Next?

---

# 1. What is a React Development Environment?

Before creating a React application, we need a development environment.

A React development environment provides the tools required to:

- Create a React project
- Install React and other dependencies
- Write React code
- Run the application locally
- Test changes
- Build the application for production

A simple setup looks like:

```text
Computer
   ↓
Node.js
   ↓
npm
   ↓
Vite
   ↓
React Project
   ↓
Development Server
   ↓
Browser
```

---

# 2. Prerequisites

Before starting React development, we need:

### Required

- Node.js
- npm
- A code editor
- Terminal / Command Prompt / PowerShell
- Web browser

### Recommended Code Editor

You can use:

- Visual Studio Code
- WebStorm
- Sublime Text
- Any editor that supports JavaScript

For this course, we will use **Visual Studio Code**.

---

# 3. What is Node.js?

**Node.js** is a JavaScript runtime that allows JavaScript to run outside the browser.

Normally, JavaScript is associated with browsers.

For example:

```text
Chrome
   ↓
JavaScript
```

Node.js allows JavaScript to run on the operating system:

```text
Computer
   ↓
Node.js
   ↓
JavaScript
```

React development tools use Node.js extensively.

We need Node.js because tools such as npm and Vite run through the Node.js ecosystem.

---

# 4. What is npm?

**npm** stands for **Node Package Manager**.

It is used to:

- Install packages
- Manage dependencies
- Run project scripts
- Manage project versions

Example:

```bash
npm install
```

This installs the dependencies defined by the project.

Another example:

```bash
npm run dev
```

This executes the development script defined in `package.json`.

---

# 5. Check Node.js and npm

Open your terminal.

Run:

```bash
node --version
```

or:

```bash
node -v
```

Then:

```bash
npm --version
```

or:

```bash
npm -v
```

Example:

```text
node -v
v22.x.x

npm -v
10.x.x
```

The exact versions depend on your installed Node.js release.

> **Important:** Do not blindly copy version numbers from someone else's system. Check your own installed versions.

---

# 6. Installing Node.js on Windows

## Step 1 — Download Node.js

Download Node.js from the official Node.js website.

Install the current suitable **LTS** release for a stable development environment.

## Step 2 — Run the Installer

Follow the installation wizard.

Keep the standard options unless you have a specific reason to change them.

## Step 3 — Restart the Terminal

Close and reopen:

- Command Prompt
- PowerShell
- VS Code terminal

## Step 4 — Verify Installation

```bash
node -v
```

```bash
npm -v
```

If both commands return versions, Node.js and npm are available.

---

# 7. Installing Node.js on Linux

On Linux, Node.js can be installed using the package manager or a Node version manager.

After installation, verify:

```bash
node -v
```

```bash
npm -v
```

The exact installation command depends on the Linux distribution and preferred installation method.

---

# 8. Installing Node.js on macOS

On macOS, Node.js can be installed using the official installer or a package/version manager.

After installation:

```bash
node -v
```

```bash
npm -v
```

Again, the important requirement is that both commands work correctly in the terminal.

---

# 9. Why Use Vite?

Vite is a modern frontend build tool.

It provides a fast development experience for frontend applications including React.

A React project created with Vite gives us:

- Development server
- Fast development workflow
- Modern JavaScript tooling
- Production build support
- React project template

For this course, **Vite is the recommended project setup method**.

---

# 10. Creating a React Project with Vite

The main command is:

```bash
npm create vite@latest
```

We can also provide the application name directly:

```bash
npm create vite@latest my-react-app
```

Here:

```text
npm
 ↓
create
 ↓
vite@latest
 ↓
my-react-app
```

means:

> Use the Vite project creation tool and create a project named `my-react-app`.

---

# 11. Step-by-Step Vite Setup

## Step 1 — Open the Terminal

Navigate to the folder where you want to create the project.

Example:

```bash
cd Desktop
```

You can choose any suitable development folder.

---

## Step 2 — Create the Project

Run:

```bash
npm create vite@latest my-react-app
```

You will be asked to select a framework.

Choose:

```text
React
```

Then select the variant.

For this beginner course:

```text
JavaScript
```

---

## Step 3 — Navigate Into the Project

```bash
cd my-react-app
```

---

## Step 4 — Install Dependencies

Run:

```bash
npm install
```

Short form:

```bash
npm i
```

This reads the project's dependency information and installs the required packages.

---

## Step 5 — Start the Development Server

Run:

```bash
npm run dev
```

Vite will start the development server.

The terminal will show a local address similar to:

```text
Local: http://localhost:5173/
```

Open that address in your browser.

> The exact port can vary if the default port is already in use.

---

# 12. Understanding the Vite Project Structure

A typical React + Vite project looks similar to:

```text
my-react-app/
│
├── node_modules/
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

The exact files can vary depending on the template and Vite version.

---

# 13. Important Files

## `index.html`

This is the main HTML document.

It contains the root element where the React application is mounted.

Example:

```html
<div id="root"></div>
```

---

## `src/main.jsx`

This is the main JavaScript entry point.

A simplified example:

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

Flow:

```text
index.html
    ↓
<div id="root">
    ↓
main.jsx
    ↓
App.jsx
    ↓
React Components
```

---

## `src/App.jsx`

This is commonly used as the main application component.

Example:

```jsx
function App() {
  return <h1>Hello React</h1>;
}

export default App;
```

---

## `src/index.css`

This file is commonly used for global styles.

Example:

```css
body {
  margin: 0;
  font-family: Arial, sans-serif;
}
```

---

## `src/App.css`

This can contain styles used by the application or App component.

The exact styling architecture can be changed as the project grows.

---

# 14. What is `package.json`?

`package.json` contains important information about a Node-based project.

It can contain:

- Project name
- Version
- Scripts
- Dependencies
- Development dependencies
- Other project metadata

Example:

```json
{
  "name": "my-react-app",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  }
}
```

---

# 15. Understanding npm Scripts

If `package.json` contains:

```json
"scripts": {
  "dev": "vite",
  "build": "vite build",
  "preview": "vite preview"
}
```

we can run:

```bash
npm run dev
```

This executes:

```text
vite
```

We can create a production build:

```bash
npm run build
```

And preview the production build locally:

```bash
npm run preview
```

---

# 16. What is `node_modules`?

After:

```bash
npm install
```

a folder called:

```text
node_modules/
```

is normally created.

It contains installed packages and their dependencies.

Example:

```text
node_modules/
├── react/
├── react-dom/
├── vite/
└── ...
```

### Important

Do not manually edit files inside `node_modules`.

It is generated and managed by the package manager.

---

# 17. What is `package-lock.json`?

When npm installs packages, it creates or updates:

```text
package-lock.json
```

It records the resolved dependency information used for the project.

This helps npm reproduce the dependency installation more consistently.

---

# 18. Running the React Application

After installation:

```bash
npm run dev
```

You will see output similar to:

```text
VITE ready

Local: http://localhost:5173/
```

Open the local URL.

You should see the React application in your browser.

---

# 19. Understanding the Development Server

The development server helps us during development.

```text
You edit code
     ↓
Save file
     ↓
Vite detects change
     ↓
Browser updates
     ↓
You see the result
```

This makes development much faster.

---

# 20. Stopping the Development Server

Inside the terminal running the server, press:

```text
Ctrl + C
```

This stops the development server.

To start it again:

```bash
npm run dev
```

---

# 21. Installing Additional Packages

React applications often need additional packages.

For example:

```bash
npm install react-router-dom
```

This installs React Router.

Another example:

```bash
npm install axios
```

This installs Axios.

After installation, the dependency information is updated in `package.json` and the lock file.

---

# 22. Ten Practical Examples

## Example 1 — Check Node.js

Run:

```bash
node -v
```

### Expected

A Node.js version is displayed.

---

## Example 2 — Check npm

Run:

```bash
npm -v
```

### Expected

An npm version is displayed.

---

## Example 3 — Create a React App

```bash
npm create vite@latest student-app
```

Select:

```text
React
JavaScript
```

Then:

```bash
cd student-app
npm install
npm run dev
```

---

## Example 4 — Create Another Project

```bash
npm create vite@latest portfolio-app
```

Then:

```bash
cd portfolio-app
npm install
npm run dev
```

### Purpose

Practice creating projects independently.

---

## Example 5 — Run the Development Server

Inside an existing React project:

```bash
npm run dev
```

### Purpose

Start the local development server.

---

## Example 6 — Install React Router

Inside the project:

```bash
npm install react-router-dom
```

Verify the dependency in:

```text
package.json
```

### Purpose

Prepare the project for routing.

Routing will be taught in a later module.

---

## Example 7 — Install Axios

```bash
npm install axios
```

### Purpose

Prepare the project for HTTP/API requests.

API integration will be taught later.

---

## Example 8 — Build the Application

```bash
npm run build
```

This creates a production build, normally in a folder such as:

```text
dist/
```

### Purpose

Understand the difference between development and production builds.

---

## Example 9 — Preview the Production Build

After:

```bash
npm run build
```

run:

```bash
npm run preview
```

This lets you preview the production build locally.

---

## Example 10 — Inspect Project Scripts

Open:

```text
package.json
```

Find:

```json
"scripts": {
  "dev": "vite",
  "build": "vite build",
  "preview": "vite preview"
}
```

Run each relevant script and observe what it does.

---

# 23. Common Errors and Solutions

## Error 1 — `npm` is not recognized

Example:

```text
'npm' is not recognized as an internal or external command
```

### Possible reason

Node.js is not installed correctly or the terminal has not picked up the updated PATH.

### Check

```bash
node -v
npm -v
```

If unavailable:

1. Install/reinstall Node.js.
2. Close the terminal.
3. Open a new terminal.
4. Check again.

---

# Error 2 — Incorrect Vite Command

Wrong:

```bash
npm create vite@letest my-react-app
```

Correct:

```bash
npm create vite@latest my-react-app
```

### Important

`latest` is the correct keyword.

---

# Error 3 — Running `npm run dev` in the Wrong Folder

If you run:

```bash
npm run dev
```

outside the project directory, npm may not find the correct `package.json`.

Correct:

```bash
cd my-react-app
npm run dev
```

---

# Error 4 — Missing Dependencies

If the project dependencies have not been installed, run:

```bash
npm install
```

Then:

```bash
npm run dev
```

---

# Error 5 — Port Already in Use

If Vite cannot use its default port, it may choose another available port or report an issue depending on the situation.

Check the terminal output carefully and open the URL Vite provides.

---

# Error 6 — Missing Script

If you run:

```bash
npm run lint
```

but `package.json` does not contain a `lint` script, npm will report that the script is missing.

Check:

```text
package.json
```

for:

```json
"scripts": {
  ...
}
```

Only run scripts that actually exist in the project.

---

# Error 7 — Project Created but Browser Does Not Open

First check whether the development server is running:

```bash
npm run dev
```

Then open the local URL shown in the terminal manually.

Example:

```text
http://localhost:5173/
```

---

# 24. Method 2 — Create React App (CRA)

Historically, React projects were commonly created using:

```bash
npx create-react-app my-app
```

Then:

```bash
cd my-app
npm start
```

However:

> **Create React App is deprecated and is not recommended for new projects.**

For new learning projects in this course, use **Vite**.

CRA may still appear in:

- Older tutorials
- Existing legacy projects
- Older company codebases

Therefore, students should understand what it is, but should not choose it for a new project unless a specific legacy requirement calls for it.

---

# 25. Method 3 — Webpack + Babel

A React development environment can also be built manually using tools such as:

- Webpack
- Webpack CLI
- Babel
- Babel presets
- Babel loader
- HTML Webpack Plugin
- Webpack Dev Server

A project may begin with:

```bash
npm init -y
```

React packages can then be installed:

```bash
npm install react react-dom
```

Additional build tooling may include:

```bash
npm install webpack webpack-cli @babel/core @babel/preset-env @babel/preset-react babel-loader html-webpack-plugin webpack-dev-server --save-dev
```

This approach gives more control, but it requires significantly more configuration.

For beginners:

```text
Vite
  ↓
Recommended

Webpack + Babel
  ↓
Advanced / custom setup
```

---

# 26. Vite vs Create React App vs Webpack

| Method | Main Use | Recommended for New Projects? |
|---|---|---|
| Vite | Modern React development | Yes |
| Create React App | Older/legacy React projects | No |
| Webpack + Babel | Custom/advanced build configuration | Depends on requirements |

### Simple decision

```text
Starting a new React project?
          ↓
        Vite
          ↓
      npm create
       vite@latest
```

For a legacy project:

```text
Existing CRA project
       ↓
Understand and maintain it
```

For advanced custom tooling:

```text
Need custom build pipeline?
       ↓
Webpack + Babel
```

---

# 27. Recommended React Setup for This Course

We will use:

```text
Operating System
       ↓
Node.js
       ↓
npm
       ↓
Vite
       ↓
React
       ↓
VS Code
       ↓
Browser
```

Recommended commands:

```bash
npm create vite@latest my-react-app
cd my-react-app
npm install
npm run dev
```

---

# 28. Professional Project Setup

For a new project:

```bash
npm create vite@latest student-management
cd student-management
npm install
npm run dev
```

Later, when additional functionality is required:

```bash
npm install react-router-dom
```

```bash
npm install axios
```

Then the project can evolve into:

```text
student-management/
│
├── public/
├── src/
│   ├── components/
│   ├── pages/
│   ├── services/
│   ├── hooks/
│   ├── assets/
│   ├── App.jsx
│   ├── main.jsx
│   └── index.css
│
├── package.json
└── vite.config.js
```

We will introduce this professional structure gradually as the course progresses.

---

# 29. Practical Tasks

## Task 1 — Environment Check

Run:

```bash
node -v
npm -v
```

Record the versions.

---

## Task 2 — Create First React Project

Create:

```text
react-first-app
```

using Vite.

Requirements:

```bash
npm create vite@latest react-first-app
cd react-first-app
npm install
npm run dev
```

---

## Task 3 — Modify App.jsx

Replace the default content with:

```jsx
function App() {
  return (
    <div>
      <h1>My First React Application</h1>
      <p>I successfully created my React environment.</p>
    </div>
  );
}

export default App;
```

---

## Task 4 — Change CSS

Modify `index.css` and create a basic professional-looking page.

---

## Task 5 — Create Components Folder

Create:

```text
src/components/
```

Then create:

```text
Navbar.jsx
Footer.jsx
```

---

## Task 6 — Install React Router

Run:

```bash
npm install react-router-dom
```

Do not implement routing yet. The goal is only to understand package installation.

---

## Task 7 — Install Axios

Run:

```bash
npm install axios
```

Check `package.json`.

---

## Task 8 — Create Production Build

Run:

```bash
npm run build
```

Find the generated production output.

---

## Task 9 — Preview Production Build

Run:

```bash
npm run preview
```

Open the provided local URL.

---

## Task 10 — Create a Student Portfolio Project

Create:

```text
student-portfolio
```

with:

```text
Navbar
Hero
About
Skills
Projects
Contact
Footer
```

At this stage, use only concepts learned so far.

---

# 30. Mini Project

## Project: React Environment Setup Verification

### Objective

Create a React + Vite project and prove that your development environment is working.

### Requirements

Project name:

```text
react-environment-demo
```

### Required steps

```bash
npm create vite@latest react-environment-demo
cd react-environment-demo
npm install
npm run dev
```

### Application requirements

Display:

```text
React Environment Setup Complete

Name: Your Name
Course: React JS
Environment: Vite
Status: Ready to Learn React
```

### Expected component structure

```text
App
│
├── Header
├── EnvironmentInfo
└── Footer
```

---

# 31. Interview Questions

## 1. Why do we need Node.js for React development?

React itself runs in the browser, but modern React development uses Node-based tooling such as npm and Vite for project creation, dependency management, development servers, and builds.

---

## 2. What is npm?

npm is the Node Package Manager and is used to install and manage JavaScript packages and execute project scripts.

---

## 3. What is Vite?

Vite is a modern frontend build tool that provides a development server and production build tooling for frontend applications.

---

## 4. How do you create a React project with Vite?

```bash
npm create vite@latest my-react-app
```

Then select React and the desired variant.

---

## 5. Why do we run `npm install`?

To install the dependencies specified by the project.

---

## 6. What does `npm run dev` do?

It executes the `dev` script from `package.json`, which normally starts the Vite development server in a Vite React project.

---

## 7. What is `node_modules`?

It is the directory where npm installs project dependencies and their required packages.

---

## 8. What is `package.json`?

It contains project metadata, scripts, dependencies, and other configuration information.

---

## 9. What is `package-lock.json`?

It records resolved dependency information used by npm to install packages consistently.

---

## 10. Is Create React App recommended for new projects?

No. Create React App is deprecated and is not recommended for new projects. Vite is the setup method used in this course.

---

# 32. Quick Revision

Remember this flow:

```text
Install Node.js
      ↓
Check node and npm
      ↓
Create Vite project
      ↓
Select React
      ↓
Select JavaScript
      ↓
cd project
      ↓
npm install
      ↓
npm run dev
      ↓
Open localhost
      ↓
Start coding
```

### Essential commands

```bash
node -v
```

```bash
npm -v
```

```bash
npm create vite@latest my-react-app
```

```bash
cd my-react-app
```

```bash
npm install
```

```bash
npm run dev
```

```bash
npm run build
```

```bash
npm run preview
```

---

# 33. Command Cheat Sheet

| Command | Purpose |
|---|---|
| `node -v` | Check Node.js version |
| `npm -v` | Check npm version |
| `npm create vite@latest` | Create a Vite project |
| `cd project-name` | Enter project directory |
| `npm install` | Install dependencies |
| `npm i` | Short form of `npm install` |
| `npm run dev` | Start development server |
| `npm run build` | Create production build |
| `npm run preview` | Preview production build |
| `npm install package-name` | Install a package |
| `Ctrl + C` | Stop running terminal process |

---

# 34. Important Rules for Students

### Rule 1

Always check your Node.js and npm installation.

```bash
node -v
npm -v
```

### Rule 2

For new projects in this course, use Vite.

```bash
npm create vite@latest
```

### Rule 3

Do not manually modify `node_modules`.

### Rule 4

Run npm commands from the correct project directory.

### Rule 5

Read the terminal output when an error occurs.

### Rule 6

Do not blindly copy commands from old tutorials.

### Rule 7

Understand what each command does.

---

# 35. What's Next?

After successfully setting up the React environment, the next topic is:

# ➡️ JSX — JavaScript XML

We will learn:

```text
What is JSX?
     ↓
Why JSX?
     ↓
JSX Syntax
     ↓
HTML vs JSX
     ↓
JavaScript Expressions
     ↓
JSX Attributes
     ↓
className
     ↓
Fragments
     ↓
JSX Rules
     ↓
Practical Examples
```

---

# 🎯 Instructor Note

The goal of this lecture is **not** to teach React programming yet.

The goal is to make every student capable of independently doing:

```text
Open Terminal
     ↓
Check Node.js
     ↓
Create React Project
     ↓
Understand Project Files
     ↓
Install Dependencies
     ↓
Start Development Server
     ↓
Open React App
     ↓
Modify App.jsx
     ↓
Build the Application
```

Once every student can perform these steps without assistance, the class is ready to move to **JSX**.

---

# 🚀 Final Takeaway

A modern React setup can be summarized as:

```text
Node.js
   ↓
npm
   ↓
Vite
   ↓
React
   ↓
Components
   ↓
Application
   ↓
Development Server
   ↓
Browser
```

The most important commands to remember are:

```bash
npm create vite@latest my-react-app
cd my-react-app
npm install
npm run dev
```

> **Environment setup is the foundation. If students can create, run, modify, and build a React project independently, they are ready to start learning React itself.**
