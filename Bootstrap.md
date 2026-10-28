## 1. Install React-Bootstrap

Inside your React project folder:

```bash
npm install react-bootstrap bootstrap
```

For example:

```bash
cd my-react-project
npm install react-bootstrap bootstrap
```

---

## 2. Import Bootstrap CSS

Open:

```text
src/main.jsx
```

Add:

```jsx
import 'bootstrap/dist/css/bootstrap.min.css';
```

A typical `main.jsx` will look like:

```jsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import 'bootstrap/dist/css/bootstrap.min.css'
import App from './App.jsx'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>,
)
```

**Important:** You need the CSS import for Bootstrap's styling to work.

---

# 3. Import a React-Bootstrap Component

Suppose you want a **Button**.

In `App.jsx`:

```jsx
import Button from 'react-bootstrap/Button'

function App() {
  return (
    <div>
      <h1>Hello React Bootstrap</h1>

      <Button variant="primary">
        Click Me
      </Button>
    </div>
  )
}

export default App
```

Run:

```bash
npm run dev
```

You should see a Bootstrap-styled button.

---

# 4. What Is Happening Here?

This:

```jsx
import Button from 'react-bootstrap/Button'
```

means:

> Bring the `Button` component from React-Bootstrap into this file.

Then:

```jsx
<Button variant="primary">
    Click Me
</Button>
```

is a React component.

The `variant` controls the Bootstrap style.

For example:

```jsx
<Button variant="primary">Primary</Button>
<Button variant="secondary">Secondary</Button>
<Button variant="success">Success</Button>
<Button variant="danger">Delete</Button>
<Button variant="warning">Warning</Button>
<Button variant="info">Info</Button>
<Button variant="dark">Dark</Button>
<Button variant="light">Light</Button>
```

---

# 5. Using Multiple Components

You can import multiple components:

```jsx
import Button from 'react-bootstrap/Button'
import Card from 'react-bootstrap/Card'
import Navbar from 'react-bootstrap/Navbar'
```

Then:

```jsx
function App() {
  return (
    <>
      <Navbar bg="dark" variant="dark">
        <Navbar.Brand>My Website</Navbar.Brand>
      </Navbar>

      <Card style={{ width: '18rem' }} className="m-4">
        <Card.Body>
          <Card.Title>React Bootstrap</Card.Title>

          <Card.Text>
            This is my first React Bootstrap card.
          </Card.Text>

          <Button variant="primary">
            Learn More
          </Button>
        </Card.Body>
      </Card>
    </>
  )
}

export default App
```

---

# 6. Bootstrap Components You Can Use

React-Bootstrap provides components such as:

```text
Button
Navbar
Card
Alert
Modal
Form
Table
Carousel
Accordion
Dropdown
Badge
Spinner
ProgressBar
Pagination
Container
Row
Col
Nav
ListGroup
Breadcrumb
Toast
Offcanvas
```

For example:

### Alert

```jsx
import Alert from 'react-bootstrap/Alert'

function App() {
  return (
    <Alert variant="success">
      Login successful!
    </Alert>
  )
}

export default App
```

---

# 7. Form Example

Import:

```jsx
import Form from 'react-bootstrap/Form'
import Button from 'react-bootstrap/Button'
```

Then:

```jsx
function App() {
  return (
    <Form className="m-4">

      <Form.Group className="mb-3">
        <Form.Label>Email</Form.Label>

        <Form.Control
          type="email"
          placeholder="Enter your email"
        />
      </Form.Group>

      <Form.Group className="mb-3">
        <Form.Label>Password</Form.Label>

        <Form.Control
          type="password"
          placeholder="Enter your password"
        />
      </Form.Group>

      <Button variant="primary">
        Login
      </Button>

    </Form>
  )
}
```

---

# 8. Cards

```jsx
import Card from 'react-bootstrap/Card'
import Button from 'react-bootstrap/Button'

function ProductCard() {
  return (
    <Card style={{ width: '18rem' }}>

      <Card.Img
        variant="top"
        src="https://via.placeholder.com/300"
      />

      <Card.Body>

        <Card.Title>
          Laptop
        </Card.Title>

        <Card.Text>
          Powerful laptop for developers.
        </Card.Text>

        <Button variant="success">
          Buy Now
        </Button>

      </Card.Body>

    </Card>
  )
}

export default ProductCard
```

---

# 9. Navbar

```jsx
import Navbar from 'react-bootstrap/Navbar'
import Nav from 'react-bootstrap/Nav'
import Container from 'react-bootstrap/Container'

function MyNavbar() {
  return (
    <Navbar bg="dark" variant="dark">
      <Container>

        <Navbar.Brand href="/">
          My Website
        </Navbar.Brand>

        <Nav>
          <Nav.Link href="/">Home</Nav.Link>
          <Nav.Link href="/about">About</Nav.Link>
          <Nav.Link href="/contact">Contact</Nav.Link>
        </Nav>

      </Container>
    </Navbar>
  )
}

export default MyNavbar
```

---

# 10. Bootstrap Grid

This is extremely important for responsive design.

Import:

```jsx
import Container from 'react-bootstrap/Container'
import Row from 'react-bootstrap/Row'
import Col from 'react-bootstrap/Col'
```

Example:

```jsx
function App() {
  return (
    <Container>

      <Row>

        <Col>
          <h2>Column 1</h2>
        </Col>

        <Col>
          <h2>Column 2</h2>
        </Col>

        <Col>
          <h2>Column 3</h2>
        </Col>

      </Row>

    </Container>
  )
}
```

Bootstrap automatically creates a responsive grid.

---

# 11. Control Column Size

For example:

```jsx
<Row>

  <Col md={8}>
    Main Content
  </Col>

  <Col md={4}>
    Sidebar
  </Col>

</Row>
```

This gives:

```text
Desktop

┌────────────────────────┬────────────┐
│                        │            │
│      Main Content      │  Sidebar   │
│         8/12           │    4/12    │
│                        │            │
└────────────────────────┴────────────┘
```

On smaller screens, Bootstrap can stack them.

---

# 12. You Can Also Use Bootstrap Classes

React-Bootstrap components and normal Bootstrap classes can be used together.

For example:

```jsx
<div className="container mt-5">

  <h1 className="text-center">
    My React Website
  </h1>

  <p className="text-muted text-center">
    Built with React Bootstrap
  </p>

</div>
```

Some useful classes:

```text
container
container-fluid

mt-1
mt-2
mt-3
mt-4
mt-5

mb-1
mb-2
mb-3
mb-4
mb-5

p-1
p-2
p-3
p-4
p-5

text-center
text-start
text-end

text-primary
text-success
text-danger

bg-primary
bg-dark
bg-light
```

---

# 13. Recommended Project Structure

For your React projects, I recommend:

```text
src/
│
├── components/
│   ├── Navbar.jsx
│   ├── Footer.jsx
│   ├── ProductCard.jsx
│   └── LoginForm.jsx
│
├── pages/
│   ├── Home.jsx
│   ├── About.jsx
│   └── Contact.jsx
│
├── App.jsx
├── main.jsx
└── index.css
```

For example:

### `components/Navbar.jsx`

```jsx
import Navbar from 'react-bootstrap/Navbar'
import Container from 'react-bootstrap/Container'

function MyNavbar() {
  return (
    <Navbar bg="dark" variant="dark">
      <Container>
        <Navbar.Brand>
          My Website
        </Navbar.Brand>
      </Container>
    </Navbar>
  )
}

export default MyNavbar
```

Then in `App.jsx`:

```jsx
import MyNavbar from './components/Navbar'

function App() {
  return (
    <>
      <MyNavbar />

      <h1>Welcome to my website</h1>
    </>
  )
}

export default App
```

---

# 14. The Important Concept

Don't think:

> "I have to create Bootstrap components myself."

React-Bootstrap already gives you the components.

Think:

```text
React Project
     ↓
Install React-Bootstrap
     ↓
Import Component
     ↓
Use Component
     ↓
Customize with props/classes
```

For example:

```jsx
import Button from 'react-bootstrap/Button'
```

then:

```jsx
<Button variant="success" size="lg">
  Save
</Button>
```

Here:

```text
Button       → Component
variant      → Prop
success      → Prop value
size         → Prop
lg           → Prop value
```

---

## One complete beginner example

```jsx
import Button from 'react-bootstrap/Button'
import Card from 'react-bootstrap/Card'
import Container from 'react-bootstrap/Container'

function App() {

  return (

    <Container className="mt-5">

      <Card style={{ width: '20rem' }}>

        <Card.Body>

          <Card.Title>
            My First React Website
          </Card.Title>

          <Card.Text>
            I am learning React Bootstrap.
          </Card.Text>

          <Button variant="primary">
            Get Started
          </Button>

        </Card.Body>

      </Card>

    </Container>

  )
}

export default App
```

### In short, remember these 3 steps:

```bash
npm install react-bootstrap bootstrap
```

```jsx
import 'bootstrap/dist/css/bootstrap.min.css'
```

```jsx
import Button from 'react-bootstrap/Button'
```

Then:

```jsx
<Button variant="primary">
  Hello Bootstrap
</Button>
```
