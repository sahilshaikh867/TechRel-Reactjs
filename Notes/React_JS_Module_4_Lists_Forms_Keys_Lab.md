# React JS — Module 4: Lists, Forms & Keys

> Beginner → Intermediate | React + Vite | Theory + Examples + Lab

## Module Goals

This module teaches three essential React concepts:

1. **React Lists** — render dynamic arrays with `map()`
2. **React Forms** — collect and manage user input with state
3. **React Keys** — give list items stable identity

---

<p align="center">
  <img src="img/React Lists, Forms, and Keys Infographic.png" alt="React Flow" width="700">
</p>

# Part 1 — React Lists

## 1. What is a List?

A React list displays multiple similar items from an array.

Typical examples:

- users
- products
- students
- courses
- orders
- tasks
- notifications
- navigation items

Instead of:

```jsx
<li>Apple</li>
<li>Banana</li>
<li>Cherry</li>
```

we can use:

```jsx
const fruits = ["Apple", "Banana", "Cherry"];

<ul>
  {fruits.map((fruit) => (
    <li key={fruit}>{fruit}</li>
  ))}
</ul>
```

## 2. Why Lists Matter

Real applications receive dynamic data:

```text
Database / API
      ↓
Array of objects
      ↓
map()
      ↓
Reusable component
      ↓
UI
```

This avoids manually writing hundreds of elements.

## 3. `map()` in React

JavaScript:

```jsx
const numbers = [1, 2, 3];

const result = numbers.map((number) => number * 2);
```

React:

```jsx
const numbers = [1, 2, 3];

function App() {
  return (
    <ul>
      {numbers.map((number) => (
        <li key={number}>{number}</li>
      ))}
    </ul>
  );
}
```

## 4. List with Objects

```jsx
const users = [
  { id: 1, name: "Aden", age: 30 },
  { id: 2, name: "Alex", age: 25 },
  { id: 3, name: "Nicol", age: 20 },
];

function App() {
  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>
          {user.name} is {user.age} years old.
        </li>
      ))}
    </ul>
  );
}
```

## 5. Conditional List Rendering

```jsx
const users = [
  { id: 1, name: "A", age: 30 },
  { id: 2, name: "B", age: 25 },
  { id: 3, name: "C", age: 35 },
];

function App() {
  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>
          {user.age > 30
            ? `${user.name} is over 30`
            : `${user.name} is under 30`}
        </li>
      ))}
    </ul>
  );
}
```

## 6. Clickable Lists

```jsx
function App() {
  const companies = ["Google", "Amazon", "Microsoft"];

  const handleClick = (company) => {
    alert(`You clicked ${company}`);
  };

  return (
    <div>
      {companies.map((company) => (
        <button
          key={company}
          onClick={() => handleClick(company)}
        >
          {company}
        </button>
      ))}
    </div>
  );
}
```

## 7. Nested Lists

```jsx
const departments = [
  {
    id: 1,
    name: "Frontend",
    skills: ["HTML", "CSS", "React"],
  },
  {
    id: 2,
    name: "Cloud",
    skills: ["AWS", "Docker", "Kubernetes"],
  },
];

function App() {
  return (
    <div>
      {departments.map((department) => (
        <section key={department.id}>
          <h2>{department.name}</h2>

          {department.skills.map((skill) => (
            <p key={skill}>{skill}</p>
          ))}
        </section>
      ))}
    </div>
  );
}
```

---

# Part 2 — React Forms

## 8. What is a React Form?

Forms collect information from users.

Examples:

- login
- registration
- contact
- search
- checkout
- profile
- job application
- feedback



## 9. Controlled Components

A controlled input gets its value from React state.

```jsx
import { useState } from "react";

function App() {
  const [name, setName] = useState("");

  return (
    <input
      value={name}
      onChange={(e) => setName(e.target.value)}
    />
  );
}
```

The state is the source of truth.

## 10. `onChange`

```jsx
const handleChange = (event) => {
  console.log(event.target.value);
};
```

Use it:

```jsx
<input onChange={handleChange} />
```

## 11. Form Submission

```jsx
function App() {
  const handleSubmit = (event) => {
    event.preventDefault();
    console.log("Submitted");
  };

  return (
    <form onSubmit={handleSubmit}>
      <input />
      <button type="submit">Submit</button>
    </form>
  );
}
```

`preventDefault()` prevents the browser's normal form navigation/reload behavior.

## 12. Textarea

```jsx
const [bio, setBio] = useState("");

<textarea
  value={bio}
  onChange={(e) => setBio(e.target.value)}
  placeholder="Write your bio..."
/>
```

## 13. Select

```jsx
const [role, setRole] = useState("developer");

<select
  value={role}
  onChange={(e) => setRole(e.target.value)}
>
  <option value="developer">Developer</option>
  <option value="designer">Designer</option>
  <option value="manager">Manager</option>
</select>
```

## 14. Checkbox

Checkboxes normally use `checked`:

```jsx
const [accepted, setAccepted] = useState(false);

<input
  type="checkbox"
  checked={accepted}
  onChange={(e) => setAccepted(e.target.checked)}
/>
```

## 15. Multiple Inputs

Use one object state:

```jsx
const [formData, setFormData] = useState({
  username: "",
  email: "",
  age: "",
  city: "",
  role: "developer",
});
```

Reusable handler:

```jsx
const handleChange = (e) => {
  const { name, value } = e.target;

  setFormData((prev) => ({
    ...prev,
    [name]: value,
  }));
};
```

Meaning:

```text
name = field being edited
value = new value
...prev = preserve other fields
[name]: value = update only that field
```

## 16. Complete Multi-Input Form

```jsx
import { useState } from "react";

function App() {
  const [formData, setFormData] = useState({
    username: "",
    email: "",
    age: "",
    city: "",
    role: "developer",
  });

  const handleChange = (e) => {
    const { name, value } = e.target;

    setFormData((prev) => ({
      ...prev,
      [name]: value,
    }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(formData);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        name="username"
        value={formData.username}
        onChange={handleChange}
        placeholder="Username"
      />

      <input
        name="email"
        value={formData.email}
        onChange={handleChange}
        placeholder="Email"
      />

      <input
        name="age"
        value={formData.age}
        onChange={handleChange}
        placeholder="Age"
      />

      <input
        name="city"
        value={formData.city}
        onChange={handleChange}
        placeholder="City"
      />

      <select
        name="role"
        value={formData.role}
        onChange={handleChange}
      >
        <option value="developer">Developer</option>
        <option value="designer">Designer</option>
        <option value="manager">Manager</option>
      </select>

      <button type="submit">Submit</button>
    </form>
  );
}

export default App;
```

---

# Part 3 — React Keys

## 17. What is a Key?

A `key` is a special React attribute used to identify list items.

```jsx
users.map((user) => (
  <li key={user.id}>{user.name}</li>
));
```

Keys help React understand which items are:

- added
- removed
- changed
- moved

## 18. Why Keys Matter

Imagine:

```text
Before:
A
B
C

After:
A
X
B
C
```

With stable IDs React can reason about:

```text
A → same
X → new
B → same
C → same
```


## 19. Best Key

Prefer stable IDs:

```jsx
key={user.id}
```

Good key sources:

- database ID
- UUID
- product ID
- order ID
- user ID
- stable slug

## 20. Why Index as Key Is Discouraged

Possible:

```jsx
items.map((item, index) => (
  <li key={index}>{item}</li>
));
```

Problem:

```text
Before:
0 → A
1 → B
2 → C

Insert X:

0 → X
1 → A
2 → B
3 → C
```

The indexes no longer represent the same items. For dynamic lists this can cause incorrect component state and inefficient updates.

Use an index only when the list is genuinely static and does not reorder, insert, or delete items.

## 21. Keys with Components

Incorrect:

```jsx
function MenuItem({ item }) {
  return <li key={item.id}>{item.name}</li>;
}

function Menu({ items }) {
  return (
    <ul>
      {items.map((item) => (
        <MenuItem item={item} />
      ))}
    </ul>
  );
}
```

Correct:

```jsx
function MenuItem({ item }) {
  return <li>{item.name}</li>;
}

function Menu({ items }) {
  return (
    <ul>
      {items.map((item) => (
        <MenuItem
          key={item.id}
          item={item}
        />
      ))}
    </ul>
  );
}
```

The key belongs on the element returned directly by `map()`.

## 22. Key vs Props

```jsx
<UserCard key={user.id} id={user.id} />
```

Here:

```text
key → React's internal identity
id  → normal prop
```

You cannot read:

```jsx
props.key
```

If the component needs the ID, pass it:

```jsx
<UserCard key={user.id} id={user.id} />
```

```...
flowchart LR
A[Parent map()] --> B[key]
A --> C[Normal props]
B --> D[React identity]
C --> E[Component]
```

---

# Part 4 — 15 React List Examples

## List Example 1 — Fruits

```jsx
const fruits = ["Apple", "Banana", "Mango"];

function App() {
  return (
    <ul>
      {fruits.map((fruit) => (
        <li key={fruit}>{fruit}</li>
      ))}
    </ul>
  );
}
```

## List Example 2 — Students

```jsx
const students = ["Amit", "Rahul", "Sneha"];

function App() {
  return (
    <ul>
      {students.map((student) => (
        <li key={student}>{student}</li>
      ))}
    </ul>
  );
}
```

## List Example 3 — Users

```jsx
const users = [
  { id: 1, name: "Amit" },
  { id: 2, name: "Priya" },
];

function App() {
  return (
    <div>
      {users.map((user) => (
        <p key={user.id}>{user.name}</p>
      ))}
    </div>
  );
}
```

## List Example 4 — Products

```jsx
const products = [
  { id: 1, name: "Laptop", price: 55000 },
  { id: 2, name: "Mouse", price: 799 },
];

function App() {
  return (
    <div>
      {products.map((product) => (
        <article key={product.id}>
          <h3>{product.name}</h3>
          <p>₹{product.price}</p>
        </article>
      ))}
    </div>
  );
}
```

## List Example 5 — Courses

```jsx
const courses = [
  { id: 1, name: "React JS" },
  { id: 2, name: "Node.js" },
  { id: 3, name: "AWS" },
];

function App() {
  return (
    <ul>
      {courses.map((course) => (
        <li key={course.id}>{course.name}</li>
      ))}
    </ul>
  );
}
```

## List Example 6 — Tasks

```jsx
const tasks = [
  { id: 1, title: "Learn JSX", completed: true },
  { id: 2, title: "Learn Lists", completed: false },
];

function App() {
  return (
    <ul>
      {tasks.map((task) => (
        <li key={task.id}>
          {task.title} - {task.completed ? "Done" : "Pending"}
        </li>
      ))}
    </ul>
  );
}
```

## List Example 7 — Active Users

```jsx
const users = [
  { id: 1, name: "A", active: true },
  { id: 2, name: "B", active: false },
];

function App() {
  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>
          {user.name} - {user.active ? "Active" : "Inactive"}
        </li>
      ))}
    </ul>
  );
}
```

## List Example 8 — Click Event

```jsx
const companies = ["Google", "Amazon", "Microsoft"];

function App() {
  const handleClick = (company) => alert(company);

  return (
    <div>
      {companies.map((company) => (
        <button
          key={company}
          onClick={() => handleClick(company)}
        >
          {company}
        </button>
      ))}
    </div>
  );
}
```

## List Example 9 — Skills

```jsx
const skills = ["React", "JavaScript", "Docker", "AWS"];

function App() {
  return (
    <div>
      {skills.map((skill) => (
        <span key={skill}>{skill} </span>
      ))}
    </div>
  );
}
```

## List Example 10 — Navigation

```jsx
const menu = [
  { id: 1, title: "Home" },
  { id: 2, title: "About" },
  { id: 3, title: "Contact" },
];

function App() {
  return (
    <nav>
      {menu.map((item) => (
        <a href="#" key={item.id}>
          {item.title}
        </a>
      ))}
    </nav>
  );
}
```

## List Example 11 — Employees

```jsx
const employees = [
  { id: 1, name: "John", role: "Developer" },
  { id: 2, name: "Sara", role: "Designer" },
];

function App() {
  return (
    <div>
      {employees.map((employee) => (
        <article key={employee.id}>
          <h3>{employee.name}</h3>
          <p>{employee.role}</p>
        </article>
      ))}
    </div>
  );
}
```

## List Example 12 — Orders

```jsx
const orders = [
  { id: "ORD101", amount: 1200, status: "Delivered" },
  { id: "ORD102", amount: 2500, status: "Pending" },
];

function App() {
  return (
    <ul>
      {orders.map((order) => (
        <li key={order.id}>
          {order.id} - ₹{order.amount} - {order.status}
        </li>
      ))}
    </ul>
  );
}
```

## List Example 13 — Filter + Map

```jsx
const numbers = [1, 2, 3, 4, 5, 6];

function App() {
  const even = numbers.filter(
    (number) => number % 2 === 0
  );

  return (
    <ul>
      {even.map((number) => (
        <li key={number}>{number}</li>
      ))}
    </ul>
  );
}
```

## List Example 14 — Nested List

```jsx
const departments = [
  {
    id: 1,
    name: "Frontend",
    skills: ["HTML", "CSS", "React"],
  },
  {
    id: 2,
    name: "Backend",
    skills: ["Node.js", "Python", "SQL"],
  },
];

function App() {
  return (
    <div>
      {departments.map((department) => (
        <section key={department.id}>
          <h2>{department.name}</h2>

          {department.skills.map((skill) => (
            <p key={skill}>{skill}</p>
          ))}
        </section>
      ))}
    </div>
  );
}
```

## List Example 15 — Reusable Component

```jsx
function Product({ product }) {
  return (
    <article>
      <h3>{product.name}</h3>
      <p>₹{product.price}</p>
    </article>
  );
}

function App() {
  const products = [
    { id: 1, name: "Laptop", price: 55000 },
    { id: 2, name: "Keyboard", price: 1500 },
  ];

  return (
    <div>
      {products.map((product) => (
        <Product
          key={product.id}
          product={product}
        />
      ))}
    </div>
  );
}
```

---

# Part 5 — 15 React Form Examples

## Form Example 1 — Basic Input

```jsx
const [name, setName] = useState("");

<input
  value={name}
  onChange={(e) => setName(e.target.value)}
/>
```

## Form Example 2 — Live Output

```jsx
const [name, setName] = useState("");

<>
  <input
    value={name}
    onChange={(e) => setName(e.target.value)}
  />
  <p>Hello, {name}</p>
</>
```

## Form Example 3 — Submit

```jsx
const handleSubmit = (e) => {
  e.preventDefault();
  alert("Submitted");
};

<form onSubmit={handleSubmit}>
  <input />
  <button type="submit">Submit</button>
</form>
```

## Form Example 4 — Email

```jsx
const [email, setEmail] = useState("");

<input
  type="email"
  value={email}
  onChange={(e) => setEmail(e.target.value)}
/>
```

## Form Example 5 — Password

```jsx
const [password, setPassword] = useState("");

<input
  type="password"
  value={password}
  onChange={(e) => setPassword(e.target.value)}
/>
```

## Form Example 6 — Number

```jsx
const [age, setAge] = useState("");

<input
  type="number"
  value={age}
  onChange={(e) => setAge(e.target.value)}
/>
```

## Form Example 7 — Textarea

```jsx
const [message, setMessage] = useState("");

<textarea
  value={message}
  onChange={(e) => setMessage(e.target.value)}
/>
```

## Form Example 8 — Select

```jsx
const [role, setRole] = useState("");

<select
  value={role}
  onChange={(e) => setRole(e.target.value)}
>
  <option value="">Select role</option>
  <option value="developer">Developer</option>
  <option value="designer">Designer</option>
</select>
```

## Form Example 9 — Checkbox

```jsx
const [accepted, setAccepted] = useState(false);

<input
  type="checkbox"
  checked={accepted}
  onChange={(e) => setAccepted(e.target.checked)}
/>
```

## Form Example 10 — Radio Buttons

```jsx
const [gender, setGender] = useState("");

<label>
  <input
    type="radio"
    value="male"
    checked={gender === "male"}
    onChange={(e) => setGender(e.target.value)}
  />
  Male
</label>

<label>
  <input
    type="radio"
    value="female"
    checked={gender === "female"}
    onChange={(e) => setGender(e.target.value)}
  />
  Female
</label>
```

## Form Example 11 — Search

```jsx
const [search, setSearch] = useState("");

<form
  onSubmit={(e) => {
    e.preventDefault();
    console.log(search);
  }}
>
  <input
    value={search}
    onChange={(e) => setSearch(e.target.value)}
  />
  <button>Search</button>
</form>
```

## Form Example 12 — Login

```jsx
const [form, setForm] = useState({
  email: "",
  password: "",
});

const handleChange = (e) => {
  const { name, value } = e.target;

  setForm((prev) => ({
    ...prev,
    [name]: value,
  }));
};
```

## Form Example 13 — Registration

```jsx
const [form, setForm] = useState({
  name: "",
  email: "",
  password: "",
});

const handleChange = (e) => {
  const { name, value } = e.target;

  setForm((prev) => ({
    ...prev,
    [name]: value,
  }));
};
```

## Form Example 14 — Validation

```jsx
const [email, setEmail] = useState("");
const [error, setError] = useState("");

const handleSubmit = (e) => {
  e.preventDefault();

  if (!email.includes("@")) {
    setError("Please enter a valid email");
    return;
  }

  setError("");
};
```

## Form Example 15 — Profile Form

```jsx
const [formData, setFormData] = useState({
  name: "",
  email: "",
  city: "",
  role: "developer",
  bio: "",
});

const handleChange = (e) => {
  const { name, value } = e.target;

  setFormData((prev) => ({
    ...prev,
    [name]: value,
  }));
};

const handleSubmit = (e) => {
  e.preventDefault();
  console.log(formData);
};
```

---

# Part 6 — 15 React Keys Examples

## Key Example 1 — User ID

```jsx
users.map((user) => (
  <li key={user.id}>{user.name}</li>
));
```

## Key Example 2 — Product ID

```jsx
products.map((product) => (
  <Product key={product.id} product={product} />
));
```

## Key Example 3 — Order ID

```jsx
orders.map((order) => (
  <li key={order.id}>{order.id}</li>
));
```

## Key Example 4 — Stable String

```jsx
const skills = ["React", "AWS", "Docker"];

skills.map((skill) => (
  <li key={skill}>{skill}</li>
));
```

## Key Example 5 — UUID

```jsx
tasks.map((task) => (
  <Task key={task.uuid} task={task} />
));
```

## Key Example 6 — Slug

```jsx
posts.map((post) => (
  <article key={post.slug}>{post.title}</article>
));
```

## Key Example 7 — Static Index

```jsx
const months = ["Jan", "Feb", "Mar"];

months.map((month, index) => (
  <li key={index}>{month}</li>
));
```

Use this only when the list is stable.

## Key Example 8 — Component Key

```jsx
users.map((user) => (
  <UserCard key={user.id} user={user} />
));
```

## Key Example 9 — Nested Keys

```jsx
departments.map((department) => (
  <section key={department.id}>
    {department.skills.map((skill) => (
      <p key={skill}>{skill}</p>
    ))}
  </section>
));
```

## Key Example 10 — Conditional List

```jsx
products.map((product) => (
  <div key={product.id}>
    {product.available ? "Available" : "Out of stock"}
  </div>
));
```

## Key Example 11 — Key Is Not a Prop

```jsx
<UserCard
  key={user.id}
  id={user.id}
/>
```

Use `props.id`, not `props.key`.

## Key Example 12 — Extracted Component

```jsx
function MenuItem({ item }) {
  return <li>{item.name}</li>;
}

function Menu({ items }) {
  return (
    <ul>
      {items.map((item) => (
        <MenuItem key={item.id} item={item} />
      ))}
    </ul>
  );
}
```

## Key Example 13 — Duplicate Keys

Bad:

```jsx
const users = [
  { id: 1, name: "A" },
  { id: 1, name: "B" },
];
```

Both siblings have the same key.

## Key Example 14 — Sorting

```jsx
products
  .sort((a, b) => a.price - b.price)
  .map((product) => (
    <Product
      key={product.id}
      product={product}
    />
  ));
```

Stable IDs remain the same even when order changes.

## Key Example 15 — API Data

```jsx
function Users({ users }) {
  return (
    <div>
      {users.map((user) => (
        <div key={user.id}>
          <h3>{user.name}</h3>
          <p>{user.email}</p>
        </div>
      ))}
    </div>
  );
}
```

---

# Part 7 — Visual / Graphical Understanding

## Lists

```text
             DATA
              │
              ▼
        ┌────────────┐
        │ users[]    │
        └─────┬──────┘
              │
              ▼
           map()
              │
       ┌──────┼──────┐
       ▼      ▼      ▼
      User   User   User
       │      │      │
       └──────┼──────┘
              ▼
          React UI
```

## Forms

```text
┌───────────────┐
│     USER      │
└───────┬───────┘
        │ types
        ▼
┌───────────────┐
│    INPUT      │
└───────┬───────┘
        │ onChange
        ▼
┌───────────────┐
│ REACT STATE   │
└───────┬───────┘
        │
        ▼
┌───────────────┐
│  VALIDATION   │
└───────┬───────┘
        │ onSubmit
        ▼
┌───────────────┐
│ API / SERVER  │
└───────────────┘
```

## Keys

```text
Previous                New
─────────                ─────
ID 101  A                ID 101  A
ID 102  B       →        ID 105  X
ID 103  C                ID 102  B
                         ID 103  C

              ↓

        React compares IDs

              ↓

101 → same
105 → new
102 → same
103 → same
```

---

# Part 8 — Industry Use Cases

## E-Commerce

```text
Product API
    ↓
products[]
    ↓
map()
    ↓
ProductCard
    ↓
key={product.id}
    ↓
Product UI
```

## Login

```text
Email + Password
       ↓
     State
       ↓
 Validation
       ↓
   onSubmit
       ↓
  Login API
```

## Admin Dashboard

```text
API
 ↓
Users / Orders / Products
 ↓
Lists
 ↓
Keys
 ↓
Reusable Components
 ↓
Dashboard
```

---

# Part 9 — Common Mistakes

### Missing key

Bad:

```jsx
items.map((item) => <li>{item.name}</li>)
```

Good:

```jsx
items.map((item) => (
  <li key={item.id}>{item.name}</li>
))
```

### Random keys

Avoid:

```jsx
key={Math.random()}
```

### Dynamic lists using indexes

Avoid:

```jsx
key={index}
```

when items can be reordered, inserted, or deleted.

### Controlled input without `onChange`

Bad:

```jsx
<input value={name} />
```

Good:

```jsx
<input
  value={name}
  onChange={(e) => setName(e.target.value)}
/>
```

### Forgetting `preventDefault`

```jsx
const handleSubmit = (e) => {
  e.preventDefault();
};
```

### Losing other form fields

Bad:

```jsx
setFormData({ email: value });
```

Good:

```jsx
setFormData((prev) => ({
  ...prev,
  email: value,
}));
```

---

# Part 10 — Mini Projects

## Project 1 — Todo List

Build:

```text
Todo Application

[ Enter task ] [Add]

☐ Learn React
☑ Learn JSX
☐ Learn Forms

Total: 3
Completed: 1
Pending: 2
```

Use:

- `useState`
- forms
- `map()`
- keys
- events
- conditional rendering

## Project 2 — Student Management

Fields:

```text
Name
Email
Course
City
[Add Student]
```

Display student cards with Delete.

## Project 3 — Product Management

Fields:

```text
Product Name
Price
Category
[Add Product]
```

Render products dynamically with stable IDs.

---

# Part 11 — LAB PRACTICAL

## Student Management System

### Objective

Build a React application that allows an instructor to add, search, display and delete students.

### Student Object

```javascript
{
  id: crypto.randomUUID(),
  name: "Amit",
  email: "amit@example.com",
  course: "React JS",
  city: "Pune"
}
```

### Requirements

1. Add student
2. Display students
3. Delete student
4. Search students
5. Validate required fields
6. Use controlled inputs
7. Use `map()`
8. Use `key={student.id}`
9. Use `onSubmit`
10. Prevent page reload

### Suggested UI

```text
┌──────────────────────────────────────┐
│       STUDENT MANAGEMENT SYSTEM      │
├──────────────────────────────────────┤
│ Name                                 │
│ [____________________________]       │
│ Email                                │
│ [____________________________]       │
│ Course                               │
│ [ React JS ▼ ]                      │
│ City                                 │
│ [____________________________]       │
│                                      │
│          [ Add Student ]             │
│                                      │
│ Search                               │
│ [ Search student... ]               │
├──────────────────────────────────────┤
│ STUDENTS                             │
│                                      │
│ Amit                                 │
│ amit@example.com                     │
│ React JS • Pune                      │
│                       [ Delete ]     │
└──────────────────────────────────────┘
```

### Search

```javascript
const filteredStudents = students.filter((student) =>
  student.name
    .toLowerCase()
    .includes(search.toLowerCase())
);
```

### Delete

```javascript
setStudents((prev) =>
  prev.filter((student) => student.id !== id)
);
```

### Add

```javascript
setStudents((prev) => [
  ...prev,
  {
    id: crypto.randomUUID(),
    ...formData,
  },
]);
```

### Validation

Required:

- Name
- Email
- Course
- City

Example:

```javascript
if (!formData.name.trim()) {
  setError("Name is required");
  return;
}
```

---

# Lab Bonus Challenges

### Challenge 1 — Edit Student

Add an Edit button and load the selected student into the form.

### Challenge 2 — Course Filter

Add:

```text
All
React JS
AWS
Python
JavaScript
```

### Challenge 3 — Student Count

Show:

```text
Total Students: 10
```

### Challenge 4 — Empty State

Show:

```text
No students found.
```

### Challenge 5 — Local Storage

Persist the student array using:

```javascript
localStorage
```

---

# Interview Questions

## Lists

1. How do you render a list in React?
2. Why is `map()` commonly used?
3. What is a key?
4. Why must keys be unique among siblings?
5. Why is index as key discouraged?
6. How do you render objects?
7. How do you render nested lists?
8. How do you add events to list items?
9. How do you render API data?
10. What is list reconciliation?

## Forms

11. What is a controlled component?
12. What does `onChange` do?
13. Why use `preventDefault()`?
14. How do you manage multiple inputs?
15. Why use the `name` attribute?
16. How do you handle a checkbox?
17. How do you handle a select?
18. How do you validate a form?
19. Controlled vs uncontrolled components?
20. How would you submit form data to an API?

## Keys

21. What is the purpose of a key?
22. Why should keys be stable?
23. Why is `Math.random()` a bad key?
24. Why can index keys cause bugs?
25. Where should the key be placed with extracted components?
26. Can `props.key` be accessed?
27. What is the difference between key and prop?
28. Do keys need to be globally unique?
29. What happens with duplicate keys?
30. What is reconciliation?

---

# Quick Revision

```text
LISTS
Array
  ↓
map()
  ↓
JSX
  ↓
key
  ↓
React UI
```

```text
FORMS
Input
  ↓
onChange
  ↓
State
  ↓
Validation
  ↓
onSubmit
  ↓
API
```

```text
KEYS
Stable ID
  ↓
Unique sibling identity
  ↓
React tracks items
  ↓
Efficient updates
```

---

# Module Completion Checklist

- [ ] Understand React Lists
- [ ] Understand `map()`
- [ ] Render arrays
- [ ] Render objects
- [ ] Render nested lists
- [ ] Handle list events
- [ ] Understand controlled components
- [ ] Handle text input
- [ ] Handle textarea
- [ ] Handle select
- [ ] Handle checkbox
- [ ] Handle radio buttons
- [ ] Handle multiple inputs
- [ ] Submit forms
- [ ] Validate forms
- [ ] Understand keys
- [ ] Use stable IDs
- [ ] Understand index-key limitations
- [ ] Understand key vs props
- [ ] Complete Student Management Lab

---

# Next Module

## React Components & Props

Recommended sequence:

```text
Functional Components
        ↓
Reusable Components
        ↓
Component Composition
        ↓
Props
        ↓
Props Destructuring
        ↓
Children
        ↓
Parent → Child
        ↓
Child → Parent
```

> **Goal:** Move from rendering dynamic data to building reusable React application architecture.
