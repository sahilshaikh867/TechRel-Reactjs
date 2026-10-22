# ReactJS Beginner Practical Task
# Student Management App — Lists, Forms & Keys

> **Level:** Beginner  
> **Topics:** React Lists, React Forms, React Keys  
> **Estimated Time:** 2–3 Hours  
> **Difficulty:** 🟢 Easy

## 1. Project Introduction

Build a small **Student Management App** using ReactJS. The application will allow a user to:

- Enter student information using a form
- Add a student
- Display all students in a list
- Delete a student
- Mark a student as active/inactive
- Display the total number of students

The main purpose is to understand three important React concepts:

```text
React Lists
React Forms
React Keys
```

---

## 2. What Will We Build?

```text
+------------------------------------------------+
|              Student Management                |
+------------------------------------------------+
| Name:    [________________________]            |
| Email:   [________________________]            |
| Course:  [ Select Course _________ ]           |
|                                                |
|              [ Add Student ]                   |
+------------------------------------------------+
| Total Students: 3                              |
+------------------------------------------------+
| Student List                                   |
|                                                |
| Rahul Sharma                                   |
| rahul@gmail.com                                |
| React                                          |
| [Active] [Delete]                              |
+------------------------------------------------+
```

---

## 3. Learning Objectives

After completing this project, you should understand:

### React Lists
- What a list is
- Why React commonly uses `map()` to render lists
- How to render an array of objects
- Why every list item needs a `key`

### React Forms
- What a controlled form is
- `value`
- `onChange`
- `onSubmit`
- `event.preventDefault()`
- Managing multiple inputs with one state object

### React Keys
- What a React key is
- Why React needs keys
- Why stable IDs are preferred
- Why array indexes are not always good keys

---

# PART 1 — PROJECT SETUP

## 4. Create the React Project

Open a terminal:

```bash
npm create vite@latest student-management-app
```

Choose:

```text
Framework: React
Variant: JavaScript
```

Then run:

```bash
cd student-management-app
npm install
npm run dev
```

Open the local URL shown by Vite, usually:

```text
http://localhost:5173
```

---

## 5. Understand the Structure

```text
student-management-app/
├── public/
├── src/
│   ├── App.jsx
│   ├── App.css
│   ├── index.css
│   └── main.jsx
├── index.html
├── package.json
└── vite.config.js
```

For this project, most work happens in:

```text
src/App.jsx
src/App.css
src/index.css
```

---

# PART 2 — REACT FORM

## 6. Start App.jsx

Replace `src/App.jsx` with:

```jsx
import { useState } from "react";
import "./App.css";

function App() {
  return (
    <div>
      <h1>Student Management App</h1>
    </div>
  );
}

export default App;
```

A React component returns JSX. `export default App` makes the component available to the entry file.

---

## 7. Create Form State

Inside `App()` add:

```jsx
const [formData, setFormData] = useState({
  name: "",
  email: "",
  course: "",
});
```

Initially:

```js
{
  name: "",
  email: "",
  course: ""
}
```

After the user enters data it may look like:

```js
{
  name: "Rahul",
  email: "rahul@gmail.com",
  course: "React"
}
```

This is a **controlled form** because React state controls the input values.

---

## 8. Create handleChange

Add inside `App()`:

```jsx
const handleChange = (event) => {
  const { name, value } = event.target;

  setFormData((previousData) => ({
    ...previousData,
    [name]: value,
  }));
};
```

### Line-by-line idea

```js
const { name, value } = event.target;
```

gets the input's `name` and current `value`.

```js
...previousData
```

keeps the other fields.

```js
[name]: value
```

updates the field that changed.

For example, if `name` is `email`, the expression updates `email`.

---

## 9. Add the Form

Add this to the JSX:

```jsx
<form onSubmit={handleSubmit}>
  <input
    type="text"
    name="name"
    placeholder="Enter student name"
    value={formData.name}
    onChange={handleChange}
  />

  <input
    type="email"
    name="email"
    placeholder="Enter student email"
    value={formData.email}
    onChange={handleChange}
  />

  <select
    name="course"
    value={formData.course}
    onChange={handleChange}
  >
    <option value="">Select Course</option>
    <option value="React">React</option>
    <option value="JavaScript">JavaScript</option>
    <option value="Python">Python</option>
    <option value="AWS">AWS</option>
  </select>

  <button type="submit">Add Student</button>
</form>
```

Notice the relationship:

```text
input value
    ↓
formData
    ↓
onChange
    ↓
handleChange
    ↓
setFormData
```

---

# PART 3 — STUDENT STATE AND SUBMIT

## 10. Create Student State

Add:

```jsx
const [students, setStudents] = useState([]);
```

We now have two states:

```text
formData → current form values
students → all submitted students
```

---

## 11. Create handleSubmit

```jsx
const handleSubmit = (event) => {
  event.preventDefault();

  if (
    formData.name.trim() === "" ||
    formData.email.trim() === "" ||
    formData.course === ""
  ) {
    alert("Please fill all fields.");
    return;
  }

  const newStudent = {
    id: crypto.randomUUID(),
    name: formData.name,
    email: formData.email,
    course: formData.course,
    active: true,
  };

  setStudents((previousStudents) => [
    ...previousStudents,
    newStudent,
  ]);

  setFormData({
    name: "",
    email: "",
    course: "",
  });
};
```

### Why `preventDefault()`?

It stops normal browser form submission so React can handle the form without a page reload.

### Why create an ID?

Each student needs a stable identity. We use:

```js
id: crypto.randomUUID()
```

That ID will also become our React `key`.

### Why spread `previousStudents`?

```js
[
  ...previousStudents,
  newStudent,
]
```

creates a new array containing the old students plus the new student. We do not directly mutate React state.

---

# PART 4 — REACT LISTS

## 12. What Is a React List?

Suppose we have:

```js
const students = [
  { id: 1, name: "Rahul" },
  { id: 2, name: "Priya" },
  { id: 3, name: "Amit" },
];
```

We can render them using `map()`:

```jsx
{students.map((student) => (
  <p key={student.id}>
    {student.name}
  </p>
))}
```

React creates one element for every object.

---

## 13. Display the Student List

Add below the form:

```jsx
<div className="student-list">
  <h2>Students</h2>

  {students.length === 0 ? (
    <p>No students added yet.</p>
  ) : (
    students.map((student) => (
      <div key={student.id} className="student-card">
        <h3>{student.name}</h3>
        <p>Email: {student.email}</p>
        <p>Course: {student.course}</p>
      </div>
    ))
  )}
</div>
```

### Important

```js
students.map(...)
```

means:

> Go through every student and create UI for that student.

---

# PART 5 — REACT KEYS

## 14. What Is a Key?

A React key gives a list item a stable identity:

```jsx
<div key={student.id}>
  {student.name}
</div>
```

If the list is:

```text
Rahul → ID 101
Priya → ID 102
Amit  → ID 103
```

and Amit is deleted, React can identify which item was removed.

### Prefer stable IDs

Good:

```jsx
key={student.id}
```

Avoid for dynamic lists:

```jsx
key={index}
```

Also avoid:

```jsx
key={Math.random()}
```

because that generates a new key during rendering instead of giving the item stable identity.

---

# PART 6 — DELETE STUDENT

## 15. Create deleteStudent

```jsx
const deleteStudent = (id) => {
  setStudents((previousStudents) =>
    previousStudents.filter(
      (student) => student.id !== id
    )
  );
};
```

`filter()` creates a new array containing students we want to keep.

If Priya's ID is passed in, every student whose ID is different remains in the list.

---

## 16. Add Delete Button

Inside the student card:

```jsx
<button
  onClick={() => deleteStudent(student.id)}
>
  Delete
</button>
```

The flow is:

```text
Click Delete
    ↓
student.id passed
    ↓
deleteStudent(id)
    ↓
filter()
    ↓
new students array
    ↓
React re-renders
```

---

# PART 7 — ACTIVE / INACTIVE

## 17. Create toggleStudent

```jsx
const toggleStudent = (id) => {
  setStudents((previousStudents) =>
    previousStudents.map((student) =>
      student.id === id
        ? {
            ...student,
            active: !student.active,
          }
        : student
    )
  );
};
```

We use `map()` because we want to create a new array while replacing only the matching student.

If:

```js
active: true
```

then:

```js
!student.active
```

becomes `false`.

---

## 18. Show Status

Inside the card:

```jsx
<p>
  Status: {student.active ? "Active" : "Inactive"}
</p>
```

And add:

```jsx
<button
  onClick={() => toggleStudent(student.id)}
>
  Toggle Status
</button>
```

---

# PART 8 — COMPLETE App.jsx

After understanding every step, use this complete version:

```jsx
import { useState } from "react";
import "./App.css";

function App() {
  const [formData, setFormData] = useState({
    name: "",
    email: "",
    course: "",
  });

  const [students, setStudents] = useState([]);

  const handleChange = (event) => {
    const { name, value } = event.target;

    setFormData((previousData) => ({
      ...previousData,
      [name]: value,
    }));
  };

  const handleSubmit = (event) => {
    event.preventDefault();

    if (
      formData.name.trim() === "" ||
      formData.email.trim() === "" ||
      formData.course === ""
    ) {
      alert("Please fill all fields.");
      return;
    }

    const newStudent = {
      id: crypto.randomUUID(),
      name: formData.name,
      email: formData.email,
      course: formData.course,
      active: true,
    };

    setStudents((previousStudents) => [
      ...previousStudents,
      newStudent,
    ]);

    setFormData({
      name: "",
      email: "",
      course: "",
    });
  };

  const deleteStudent = (id) => {
    setStudents((previousStudents) =>
      previousStudents.filter(
        (student) => student.id !== id
      )
    );
  };

  const toggleStudent = (id) => {
    setStudents((previousStudents) =>
      previousStudents.map((student) =>
        student.id === id
          ? {
              ...student,
              active: !student.active,
            }
          : student
      )
    );
  };

  return (
    <div className="app">
      <div className="container">
        <h1>Student Management App</h1>

        <form
          onSubmit={handleSubmit}
          className="student-form"
        >
          <input
            type="text"
            name="name"
            placeholder="Enter student name"
            value={formData.name}
            onChange={handleChange}
          />

          <input
            type="email"
            name="email"
            placeholder="Enter student email"
            value={formData.email}
            onChange={handleChange}
          />

          <select
            name="course"
            value={formData.course}
            onChange={handleChange}
          >
            <option value="">Select Course</option>
            <option value="React">React</option>
            <option value="JavaScript">JavaScript</option>
            <option value="Python">Python</option>
            <option value="AWS">AWS</option>
          </select>

          <button type="submit">
            Add Student
          </button>
        </form>

        <div className="summary">
          <h2>Total Students: {students.length}</h2>
        </div>

        <div className="student-list">
          <h2>Student List</h2>

          {students.length === 0 ? (
            <p>No students added yet.</p>
          ) : (
            students.map((student) => (
              <div
                key={student.id}
                className="student-card"
              >
                <h3>{student.name}</h3>
                <p>Email: {student.email}</p>
                <p>Course: {student.course}</p>
                <p>
                  Status: {student.active ? "Active" : "Inactive"}
                </p>

                <button
                  onClick={() => toggleStudent(student.id)}
                >
                  Toggle Status
                </button>

                <button
                  onClick={() => deleteStudent(student.id)}
                >
                  Delete
                </button>
              </div>
            ))
          )}
        </div>
      </div>
    </div>
  );
}

export default App;
```

---

# PART 9 — CSS

## 19. App.css

Replace `src/App.css` with:

```css
.app {
  min-height: 100vh;
  background: #f1f5f9;
  padding: 40px 20px;
}

.container {
  max-width: 800px;
  margin: auto;
  background: white;
  padding: 30px;
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.08);
}

h1 {
  text-align: center;
  margin-bottom: 30px;
}

.student-form {
  display: grid;
  gap: 12px;
}

.student-form input,
.student-form select {
  padding: 12px;
  border: 1px solid #cbd5e1;
  border-radius: 8px;
  font-size: 16px;
}

button {
  padding: 10px 15px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  background: #2563eb;
  color: white;
  margin-right: 8px;
  margin-top: 8px;
}

.summary {
  margin: 30px 0;
  padding: 15px;
  background: #eff6ff;
  border-radius: 10px;
}

.student-card {
  padding: 20px;
  margin-top: 15px;
  border: 1px solid #e2e8f0;
  border-radius: 10px;
  background: #f8fafc;
}

.student-card h3 {
  margin-top: 0;
}

.student-card p {
  margin: 8px 0;
}
```

## 20. index.css

Replace `src/index.css` with:

```css
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
  color: #1e293b;
}

button {
  font-family: inherit;
}
```

---

# PART 10 — TESTING

## 21. Test the Form

Try submitting an empty form.

Expected:

```text
Please fill all fields.
```

Then add:

```text
Name: Rahul Sharma
Email: rahul@gmail.com
Course: React
```

Click **Add Student**.

Expected result:

```text
Rahul Sharma
rahul@gmail.com
React
Active
```

Add two more students to verify the list.

---

## 22. Test the List

Add:

```text
Rahul
Priya
Amit
```

All three should appear.

This proves that `map()` is rendering an array into UI.

---

## 23. Test the Key

Check:

```jsx
key={student.id}
```

Every student gets a stable ID from:

```js
crypto.randomUUID()
```

---

## 24. Test Delete

Delete Priya.

Expected:

```text
Rahul
Amit
```

---

## 25. Test Toggle

Click **Toggle Status**.

Expected:

```text
Active → Inactive
Inactive → Active
```

---

# PART 11 — COMPLETE DATA FLOW

```text
User enters data
       ↓
React Form
       ↓
handleChange()
       ↓
formData state
       ↓
Submit
       ↓
handleSubmit()
       ↓
Create Student Object
       ↓
setStudents()
       ↓
students array
       ↓
map()
       ↓
Student Cards
       ↓
key={student.id}
```

---

# 26. Important Concepts to Remember

### Controlled input

```jsx
value={formData.name}
onChange={handleChange}
```

### Form submission

```jsx
<form onSubmit={handleSubmit}>
```

### Prevent browser submission

```js
event.preventDefault();
```

### Render a list

```jsx
students.map((student) => (
  <div key={student.id}>
    {student.name}
  </div>
))
```

### Delete from an array

```js
filter()
```

### Update an item in an array

```js
map()
```

### Stable React key

```jsx
key={student.id}
```

---

# 27. Beginner Challenges

## Challenge 1 — Phone Number

Add a phone input and store:

```js
phone: ""
```

Display it in the student card.

## Challenge 2 — Age

Add an age field and display:

```text
Age: 21
```

## Challenge 3 — Search

Add:

```text
Search students...
```

Use `filter()` before `map()` so only matching students are displayed.

Concept:

```text
students
   ↓
filter()
   ↓
matching students
   ↓
map()
   ↓
UI
```

## Challenge 4 — Filters

Add:

```text
All | Active | Inactive
```

## Challenge 5 — Counts

Display:

```text
Total Students: 10
Active Students: 7
Inactive Students: 3
```

## Challenge 6 — Edit

Add an **Edit** button. Clicking it should load the student's data into the form so it can be changed and saved.

---

# 28. Common Beginner Mistakes

### Mistake 1 — Forgetting the key

Bad:

```jsx
students.map((student) => (
  <div>{student.name}</div>
))
```

Good:

```jsx
students.map((student) => (
  <div key={student.id}>{student.name}</div>
))
```

### Mistake 2 — Random key

Avoid:

```jsx
key={Math.random()}
```

Use a stable ID.

### Mistake 3 — Direct state mutation

Avoid:

```js
students.push(newStudent);
```

Use:

```js
setStudents((previousStudents) => [
  ...previousStudents,
  newStudent,
]);
```

### Mistake 4 — Controlled input without onChange

Avoid:

```jsx
<input value={formData.name} />
```

Use:

```jsx
<input
  value={formData.name}
  onChange={handleChange}
/>
```

### Mistake 5 — Forgetting preventDefault

Use:

```js
event.preventDefault();
```

when handling a normal HTML form submission in React.

---

# 29. Mini Interview Questions

### 1. What is a React list?

A UI collection generated from an array of data.

### 2. Which JavaScript method is commonly used to render lists?

```js
map()
```

### 3. Why does React need keys?

Keys help React identify list items and track their identity between renders.

### 4. What should be used as a key?

Prefer a stable unique ID from the data.

### 5. What is a controlled input?

An input whose value is controlled by React state.

### 6. Why use `preventDefault()`?

To prevent the browser's default form submission behavior.

### 7. Why use `filter()` for deletion?

It creates a new array containing the items we want to keep.

### 8. Why use `map()` when changing one student?

It creates a new array while allowing us to replace the matching student.

### 9. Should React state be mutated directly?

No. Create a new array or object and update state through the setter.

### 10. Is an array index always a bad key?

No. It can be acceptable for static lists that never reorder, insert, or delete items. Stable IDs are preferable for dynamic lists.

---

# 30. Final Checklist

## Form

- [ ] Name input
- [ ] Email input
- [ ] Course select
- [ ] Controlled inputs
- [ ] `onChange`
- [ ] `onSubmit`
- [ ] Validation
- [ ] Form reset

## List

- [ ] Student array
- [ ] `map()`
- [ ] Student card
- [ ] Empty-list message

## Keys

- [ ] Unique student ID
- [ ] `key={student.id}`
- [ ] No random key during render
- [ ] Understand why keys matter

## Actions

- [ ] Add student
- [ ] Delete student
- [ ] Toggle status
- [ ] Student count

## Bonus

- [ ] Search
- [ ] Filter
- [ ] Phone
- [ ] Age
- [ ] Edit student

---

# 31. Final Mental Model

Remember the project like this:

```text
FORM
  |
  | collects data
  v
STATE
  |
  | stores students
  v
LIST
  |
  | map()
  v
UI
  |
  | key={student.id}
  v
React identifies each item
```

The overall flow is:

```text
React Form
    ↓
User Input
    ↓
useState
    ↓
Submit
    ↓
Array of Objects
    ↓
map()
    ↓
List of UI Items
    ↓
key={uniqueId}
```

The goal is not simply to copy the final code. Rebuild the project yourself and be able to explain:

```text
Why are we using useState?
Why is formData an object?
Why do inputs use value?
Why do inputs use onChange?
Why do we use preventDefault()?
Why do we use map()?
Why do we use filter()?
Why does every list item need a key?
Why is student.id better than index for a dynamic list?
Why should we not mutate students directly?
```

If you can answer those questions and rebuild the application yourself, you have successfully understood **React Lists + React Forms + React Keys**.

---

# 32. Next Step

After this project, continue with:

```text
Lists + Forms + Keys
        ↓
useState
        ↓
useEffect
        ↓
API Integration
        ↓
React Router
        ↓
Context API
        ↓
Authentication
        ↓
Real-world React Project
```

**Recommended next project:** convert this Student Management App into a Student Dashboard with search, filters, edit functionality, LocalStorage, React Router, and reusable components.
