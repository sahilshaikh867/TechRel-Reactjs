# React JS Module 6 — useState & useEffect Hooks

> **Level:** Beginner → Intermediate  
> **Goal:** Understand React state, state updates, side effects, dependencies, cleanup, and practical Hook patterns.

---

## 📚 Module Overview

In the previous module, we learned about React Components, Functional Components, Class Components, Props, Pure Components, component patterns, PropTypes, and the component lifecycle.

In this module, we move into one of the most important parts of modern React development:

1. **`useState()` Hook**
2. **State initialization and updates**
3. **Functional state updates**
4. **Objects and arrays in state**
5. **Lazy state initialization**
6. **Forms using state**
7. **`useEffect()` Hook**
8. **Effect dependency arrays**
9. **Cleanup functions**
10. **API calls, timers, browser events, and other side effects**
11. **`useState` + `useEffect` together**
12. **Industry-style practical lab**

---

# 1. What Are React Hooks?

Hooks are functions provided by React that allow functional components to use React features such as:

- State
- Side effects
- Context
- References
- Performance optimizations
- Custom reusable logic

Two of the most commonly used Hooks are:

```jsx
useState()
useEffect()
```

### Simple idea

```text
User Action
    ↓
State Update
    ↓
Component Re-renders
    ↓
UI Updates
    ↓
useEffect runs when its dependencies require it
```

---

# 2. What Is `useState()`?

`useState()` is a React Hook used to add state to a functional component.

State is data that can change during the lifetime of a component.

Examples:

- Counter value
- Username
- Login status
- Theme
- Shopping cart
- Selected product
- Form values
- Modal visibility
- Loading status

### Basic syntax

```jsx
const [state, setState] = useState(initialState);
```

### Parts

| Part | Meaning |
|---|---|
| `state` | Current state value |
| `setState` | Function used to update state |
| `initialState` | Initial value |

Example:

```jsx
const [count, setCount] = useState(0);
```

Initially:

```text
count = 0
```

After:

```jsx
setCount(1);
```

The state becomes:

```text
count = 1
```

React then re-renders the component.

---

# 3. How `useState()` Works

```text
Component renders
       ↓
useState(0)
       ↓
count = 0
       ↓
User clicks button
       ↓
setCount(...)
       ↓
React schedules state update
       ↓
Component renders again
       ↓
New count displayed
```

### Important

State is preserved between renders.

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}
```

React remembers the value of `count` between renders.

---

# 4. Rules of Hooks

Hooks have important rules.

## Rule 1 — Call Hooks at the top level

Correct:

```jsx
function App() {
  const [count, setCount] = useState(0);

  return <h1>{count}</h1>;
}
```

Incorrect:

```jsx
function App() {
  if (true) {
    const [count, setCount] = useState(0);
  }

  return <h1>Hello</h1>;
}
```

## Rule 2 — Do not call Hooks inside loops

Incorrect:

```jsx
for (let i = 0; i < 5; i++) {
  const [value, setValue] = useState(0);
}
```

## Rule 3 — Do not call Hooks inside event handlers

Incorrect:

```jsx
function handleClick() {
  const [count, setCount] = useState(0);
}
```

## Rule 4 — Hooks should normally be called from React components or custom Hooks

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  return <h1>{count}</h1>;
}
```

---

# 5. useState Example 1 — Simple Counter

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  function increment() {
    setCount(count + 1);
  }

  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={increment}>Increment</button>
    </div>
  );
}

export default Counter;
```

### Explanation

```jsx
useState(0)
```

creates:

```text
count    → current value
setCount → update function
0        → initial value
```

---

# 6. useState Example 2 — Increment and Decrement

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h2>Count: {count}</h2>

      <button onClick={() => setCount(count + 1)}>
        +
      </button>

      <button onClick={() => setCount(count - 1)}>
        -
      </button>
    </div>
  );
}

export default Counter;
```

### Real-life use

This pattern can be used for:

- Quantity selectors
- Product quantities
- Voting systems
- Rating counters

---

# 7. useState Example 3 — Functional State Update

When the new state depends on the previous state, prefer a functional update.

```jsx
setCount(prevCount => prevCount + 1);
```

Example:

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  function increaseThreeTimes() {
    setCount(prev => prev + 1);
    setCount(prev => prev + 1);
    setCount(prev => prev + 1);
  }

  return (
    <div>
      <h2>{count}</h2>
      <button onClick={increaseThreeTimes}>
        Increase 3
      </button>
    </div>
  );
}

export default Counter;
```

### Why use it?

It tells React:

> "Calculate the next state from the latest previous state."

This is especially useful when multiple updates depend on the previous value.

---

# 8. useState Example 4 — Toggle

```jsx
import { useState } from "react";

function Toggle() {
  const [isOn, setIsOn] = useState(false);

  return (
    <button onClick={() => setIsOn(prev => !prev)}>
      {isOn ? "ON" : "OFF"}
    </button>
  );
}

export default Toggle;
```

### Real-world examples

- Dark mode
- Menu open/close
- Modal visibility
- Password visibility
- Like/unlike

---

# 9. useState Example 5 — Text Input

```jsx
import { useState } from "react";

function NameInput() {
  const [name, setName] = useState("");

  return (
    <div>
      <input
        value={name}
        onChange={(event) => setName(event.target.value)}
        placeholder="Enter your name"
      />

      <h2>Hello, {name}</h2>
    </div>
  );
}

export default NameInput;
```

### Flow

```text
User types
   ↓
onChange
   ↓
setName()
   ↓
State changes
   ↓
Component re-renders
   ↓
New name appears
```

---

# 10. useState Example 6 — Multiple State Variables

A component can have multiple state variables.

```jsx
import { useState } from "react";

function UserProfile() {
  const [name, setName] = useState("");
  const [age, setAge] = useState(18);
  const [isStudent, setIsStudent] = useState(true);

  return (
    <div>
      <input
        value={name}
        onChange={(e) => setName(e.target.value)}
        placeholder="Name"
      />

      <input
        type="number"
        value={age}
        onChange={(e) => setAge(Number(e.target.value))}
      />

      <button onClick={() => setIsStudent(prev => !prev)}>
        {isStudent ? "Student" : "Not Student"}
      </button>

      <p>Name: {name}</p>
      <p>Age: {age}</p>
      <p>Status: {isStudent ? "Student" : "Not Student"}</p>
    </div>
  );
}

export default UserProfile;
```

---

# 11. useState Example 7 — Object State

`useState()` can store objects.

```jsx
import { useState } from "react";

function Profile() {
  const [user, setUser] = useState({
    name: "Sahil",
    age: 25,
    city: "Pune"
  });

  function updateCity() {
    setUser(prev => ({
      ...prev,
      city: "Mumbai"
    }));
  }

  return (
    <div>
      <h2>{user.name}</h2>
      <p>{user.age}</p>
      <p>{user.city}</p>

      <button onClick={updateCity}>
        Change City
      </button>
    </div>
  );
}

export default Profile;
```

### Important

`useState()` does **not** automatically merge object state.

This is wrong:

```jsx
setUser({
  city: "Mumbai"
});
```

It replaces the complete object.

Use:

```jsx
setUser(prev => ({
  ...prev,
  city: "Mumbai"
}));
```

---

# 12. useState Example 8 — Array State

```jsx
import { useState } from "react";

function TodoList() {
  const [todos, setTodos] = useState([
    "Learn React",
    "Practice Hooks"
  ]);

  function addTodo() {
    setTodos(prev => [
      ...prev,
      "Build a React project"
    ]);
  }

  return (
    <div>
      <ul>
        {todos.map((todo, index) => (
          <li key={index}>{todo}</li>
        ))}
      </ul>

      <button onClick={addTodo}>
        Add Todo
      </button>
    </div>
  );
}

export default TodoList;
```

### Best practice

For dynamic production lists, prefer stable IDs rather than array indexes as keys.

---

# 13. useState Example 9 — Form State

```jsx
import { useState } from "react";

function Form() {
  const [name, setName] = useState("");
  const [age, setAge] = useState("");
  const [submitted, setSubmitted] = useState(false);

  function handleSubmit(event) {
    event.preventDefault();
    setSubmitted(true);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input
        value={name}
        onChange={(e) => setName(e.target.value)}
        placeholder="Name"
      />

      <input
        type="number"
        value={age}
        onChange={(e) => setAge(e.target.value)}
        placeholder="Age"
      />

      <button type="submit">Submit</button>

      {submitted && (
        <p>
          Submitted: {name}, {age}
        </p>
      )}
    </form>
  );
}

export default Form;
```

---

# 14. useState Example 10 — Lazy Initialization

If the initial state requires expensive computation, pass a function.

```jsx
import { useState } from "react";

function ExpensiveComponent() {
  const [value, setValue] = useState(() => {
    return calculateInitialValue();
  });

  return <h2>{value}</h2>;
}

function calculateInitialValue() {
  console.log("Calculating...");
  return 1000;
}

export default ExpensiveComponent;
```

The initializer function is used to calculate the initial state rather than calculating the value on every render.

---

# 15. More useState Patterns

## Boolean

```jsx
const [isOpen, setIsOpen] = useState(false);
```

## String

```jsx
const [username, setUsername] = useState("");
```

## Number

```jsx
const [price, setPrice] = useState(0);
```

## Array

```jsx
const [items, setItems] = useState([]);
```

## Object

```jsx
const [user, setUser] = useState({
  name: "",
  email: ""
});
```

---

# 16. Important State Rules

### 1. Never mutate state directly

Wrong:

```jsx
user.name = "Rahul";
```

Correct:

```jsx
setUser(prev => ({
  ...prev,
  name: "Rahul"
}));
```

### 2. Use the setter

Wrong:

```jsx
count = count + 1;
```

Correct:

```jsx
setCount(count + 1);
```

### 3. Use functional updates when dependent on previous state

```jsx
setCount(prev => prev + 1);
```

### 4. State updates may be batched

Do not assume the state variable changes immediately after calling its setter in the same execution.

---

# 17. What Is `useEffect()`?

`useEffect()` is a React Hook used to synchronize a component with external systems and handle side effects.

Examples:

- API requests
- Timers
- Browser events
- Subscriptions
- WebSocket connections
- Document title
- External libraries
- Cleanup operations

### Syntax

```jsx
useEffect(() => {
  // Effect logic

  return () => {
    // Cleanup logic
  };
}, [dependencies]);
```

---

# 18. What Is a Side Effect?

A side effect is an operation that interacts with something outside the component's rendering calculation.

Examples:

```text
Component
   │
   ├── Fetch API
   ├── Timer
   ├── Browser event
   ├── WebSocket
   ├── document.title
   └── External library
```

React rendering should primarily calculate what the UI should look like.

Effects handle synchronization with external systems.

---

# 19. How `useEffect()` Works

```text
Component renders
       ↓
React commits UI
       ↓
Effect runs
       ↓
External system is synchronized
       ↓
Dependency changes?
     /      \
   Yes       No
    ↓         ↓
Cleanup     Nothing
    ↓
Effect runs again
```

If the effect returns a cleanup function, React runs that cleanup before the effect runs again with changed dependencies and when the component is removed.

---

# 20. useEffect Example 1 — Run After Every Render

```jsx
import { useEffect, useState } from "react";

function App() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("Effect ran");
  });

  return (
    <div>
      <h1>{count}</h1>

      <button onClick={() => setCount(prev => prev + 1)}>
        Increment
      </button>
    </div>
  );
}

export default App;
```

Because there is no dependency array, the effect runs after every completed render.

---

# 21. useEffect Example 2 — Run Once on Mount

```jsx
import { useEffect } from "react";

function App() {
  useEffect(() => {
    console.log("Component mounted");
  }, []);

  return <h1>Hello React</h1>;
}

export default App;
```

### Common uses

- Initial data loading
- Analytics initialization
- Initial setup

> Note: In development, React Strict Mode can intentionally run setup/cleanup more than once to help detect unsafe effects. Do not use an empty dependency array as a guarantee that an effect will visibly execute only once during development.

---

# 22. useEffect Example 3 — Dependency-Based Effect

```jsx
import { useEffect, useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("Count changed:", count);
  }, [count]);

  return (
    <button onClick={() => setCount(prev => prev + 1)}>
      Count: {count}
    </button>
  );
}

export default Counter;
```

The effect runs after the initial render and after renders where `count` has changed.

---

# 23. useEffect Example 4 — Updating Document Title

```jsx
import { useEffect, useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `Count: ${count}`;
  }, [count]);

  return (
    <button onClick={() => setCount(prev => prev + 1)}>
      Count: {count}
    </button>
  );
}

export default Counter;
```

### Real-world use

Useful for:

- Unread message count
- Shopping cart count
- Dashboard status
- Browser tab titles

---

# 24. useEffect Example 5 — Fetch Data

```jsx
import { useEffect, useState } from "react";

function Users() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    async function loadUsers() {
      try {
        const response = await fetch(
          "https://jsonplaceholder.typicode.com/users"
        );

        const data = await response.json();
        setUsers(data);
      } catch (error) {
        console.error("Failed to load users:", error);
      } finally {
        setLoading(false);
      }
    }

    loadUsers();
  }, []);

  if (loading) {
    return <p>Loading...</p>;
  }

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

export default Users;
```

### Flow

```text
Component mounts
      ↓
useEffect
      ↓
API request
      ↓
Response
      ↓
setUsers(data)
      ↓
Re-render
      ↓
Users displayed
```

---

# 25. useEffect Example 6 — Timer

```jsx
import { useEffect, useState } from "react";

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const intervalId = setInterval(() => {
      setSeconds(prev => prev + 1);
    }, 1000);

    return () => {
      clearInterval(intervalId);
    };
  }, []);

  return <h2>Timer: {seconds}s</h2>;
}

export default Timer;
```

### Why cleanup?

Without cleanup, the interval could continue running after the component is removed.

---

# 26. useEffect Example 7 — Browser Event Listener

```jsx
import { useEffect, useState } from "react";

function WindowWidth() {
  const [width, setWidth] = useState(window.innerWidth);

  useEffect(() => {
    function handleResize() {
      setWidth(window.innerWidth);
    }

    window.addEventListener("resize", handleResize);

    return () => {
      window.removeEventListener("resize", handleResize);
    };
  }, []);

  return <h2>Window width: {width}px</h2>;
}

export default WindowWidth;
```

### Important

The same handler function must be removed during cleanup.

---

# 27. useEffect Example 8 — Search / Filter Based on State

```jsx
import { useEffect, useState } from "react";

function Search() {
  const [query, setQuery] = useState("");

  useEffect(() => {
    if (query.trim() === "") {
      return;
    }

    console.log("Search query changed:", query);
  }, [query]);

  return (
    <input
      value={query}
      onChange={(e) => setQuery(e.target.value)}
      placeholder="Search..."
    />
  );
}

export default Search;
```

In a real application, the effect could synchronize the search query with an API or another external system.

---

# 28. useEffect Example 9 — Cleanup Subscription

A subscription must be removed when the component is no longer using it.

```jsx
import { useEffect } from "react";

function ChatRoom({ roomId }) {
  useEffect(() => {
    const connection = connectToRoom(roomId);

    connection.connect();

    return () => {
      connection.disconnect();
    };
  }, [roomId]);

  return <h2>Room: {roomId}</h2>;
}

function connectToRoom(roomId) {
  return {
    connect() {
      console.log("Connected to", roomId);
    },
    disconnect() {
      console.log("Disconnected from", roomId);
    }
  };
}

export default ChatRoom;
```

### Flow

```text
roomId = 101
   ↓
Connect to room 101
   ↓
roomId changes to 102
   ↓
Disconnect 101
   ↓
Connect 102
```

---

# 29. useEffect Example 10 — Combining State and Effect

```jsx
import { useEffect, useState } from "react";

function ProductCounter() {
  const [quantity, setQuantity] = useState(1);
  const [total, setTotal] = useState(0);

  const price = 499;

  useEffect(() => {
    setTotal(quantity * price);
  }, [quantity]);

  return (
    <div>
      <h2>Price: ₹{price}</h2>
      <h2>Quantity: {quantity}</h2>
      <h2>Total: ₹{total}</h2>

      <button
        onClick={() =>
          setQuantity(prev => Math.max(1, prev - 1))
        }
      >
        -
      </button>

      <button
        onClick={() =>
          setQuantity(prev => prev + 1)
        }
      >
        +
      </button>
    </div>
  );
}

export default ProductCounter;
```

> In real applications, values that can be calculated directly from existing state/props often do not need another state variable or an effect. For this teaching example, the effect demonstrates dependency-based synchronization.

---

# 30. Dependency Array — Complete Understanding

The dependency array controls when an effect is synchronized.

## Case 1 — No dependency array

```jsx
useEffect(() => {
  console.log("Runs after every render");
});
```

---

## Case 2 — Empty dependency array

```jsx
useEffect(() => {
  console.log("Runs after initial mount");
}, []);
```

The cleanup, if provided, runs when the component is removed. Development Strict Mode may perform an additional setup/cleanup cycle.

---

## Case 3 — One dependency

```jsx
useEffect(() => {
  console.log("Count changed");
}, [count]);
```

---

## Case 4 — Multiple dependencies

```jsx
useEffect(() => {
  console.log("Count or user changed");
}, [count, userId]);
```

---

# 31. Cleanup Functions

Cleanup is used to stop or undo an effect's external work.

Common cleanup operations:

```text
Timer       → clearInterval()
Timeout     → clearTimeout()
Event       → removeEventListener()
Subscription→ unsubscribe()
WebSocket   → close()
Connection  → disconnect()
Request     → AbortController
```

### Example

```jsx
useEffect(() => {
  const timer = setInterval(() => {
    console.log("Running...");
  }, 1000);

  return () => {
    clearInterval(timer);
  };
}, []);
```

---

# 32. Cleanup Timing

Suppose:

```jsx
useEffect(() => {
  console.log("Effect");

  return () => {
    console.log("Cleanup");
  };
}, [userId]);
```

If `userId` changes:

```text
Old effect
   ↓
Cleanup old effect
   ↓
New render committed
   ↓
New effect
```

When the component is removed:

```text
Component unmounts
       ↓
Cleanup runs
```

---

# 33. useState vs useEffect

| `useState` | `useEffect` |
|---|---|
| Stores component state | Synchronizes with external systems |
| Updates UI state | Performs side effects |
| Returns state + setter | Runs effect logic |
| `useState(value)` | `useEffect(callback, deps)` |
| Used for data changing in UI | Used for API, timers, events, subscriptions, etc. |

### Simple memory trick

```text
useState  → "What data does my UI remember?"
useEffect → "What external system should my component synchronize with?"
```

---

# 34. useState + useEffect Together

This combination appears frequently in real React applications.

```jsx
import { useEffect, useState } from "react";

function UserProfile() {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    async function fetchUser() {
      const response = await fetch(
        "https://jsonplaceholder.typicode.com/users/1"
      );

      const data = await response.json();

      setUser(data);
      setLoading(false);
    }

    fetchUser();
  }, []);

  if (loading) {
    return <p>Loading user...</p>;
  }

  return (
    <div>
      <h2>{user.name}</h2>
      <p>{user.email}</p>
    </div>
  );
}

export default UserProfile;
```

### Architecture

```text
useEffect
   │
   ├── Fetch API
   │
   ↓
setUser()
   │
   ↓
useState
   │
   ↓
Component re-renders
   │
   ↓
Updated UI
```

---

# 35. Practical Example — Loading / Error / Data State

A more realistic API component usually needs multiple states.

```jsx
import { useEffect, useState } from "react";

function Products() {
  const [products, setProducts] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState("");

  useEffect(() => {
    async function fetchProducts() {
      try {
        setLoading(true);
        setError("");

        const response = await fetch(
          "https://fakestoreapi.com/products"
        );

        if (!response.ok) {
          throw new Error("Failed to fetch products");
        }

        const data = await response.json();
        setProducts(data);
      } catch (error) {
        setError(error.message);
      } finally {
        setLoading(false);
      }
    }

    fetchProducts();
  }, []);

  if (loading) {
    return <p>Loading products...</p>;
  }

  if (error) {
    return <p>Error: {error}</p>;
  }

  return (
    <div>
      {products.map(product => (
        <article key={product.id}>
          <h3>{product.title}</h3>
          <p>₹{product.price}</p>
        </article>
      ))}
    </div>
  );
}

export default Products;
```

### Industry pattern

```text
             API
              ↓
       ┌───────────────┐
       │ useEffect()   │
       └───────┬───────┘
               ↓
       ┌───────────────┐
       │ Request State │
       └───────────────┘
          /    |    \
       Loading Error Data
          ↓      ↓    ↓
          UI     UI   UI
```

---

# 36. Abort an API Request During Cleanup

For requests that may become irrelevant, `AbortController` can be used.

```jsx
import { useEffect, useState } from "react";

function User({ userId }) {
  const [user, setUser] = useState(null);

  useEffect(() => {
    const controller = new AbortController();

    async function fetchUser() {
      try {
        const response = await fetch(
          `https://jsonplaceholder.typicode.com/users/${userId}`,
          {
            signal: controller.signal
          }
        );

        const data = await response.json();
        setUser(data);
      } catch (error) {
        if (error.name !== "AbortError") {
          console.error(error);
        }
      }
    }

    fetchUser();

    return () => {
      controller.abort();
    };
  }, [userId]);

  return <h2>{user ? user.name : "Loading..."}</h2>;
}

export default User;
```

### Why?

If `userId` changes quickly, the previous request may no longer be relevant.

---

# 37. Common useEffect Mistakes

## Mistake 1 — Forgetting dependencies

```jsx
useEffect(() => {
  console.log(userId);
}, []);
```

If the effect needs to react to changing `userId`, it should generally be included:

```jsx
useEffect(() => {
  console.log(userId);
}, [userId]);
```

---

## Mistake 2 — Missing cleanup

Wrong:

```jsx
useEffect(() => {
  window.addEventListener("resize", handleResize);
}, []);
```

Better:

```jsx
useEffect(() => {
  window.addEventListener("resize", handleResize);

  return () => {
    window.removeEventListener("resize", handleResize);
  };
}, []);
```

---

## Mistake 3 — Infinite effect loop

Avoid patterns such as:

```jsx
useEffect(() => {
  setCount(count + 1);
}, [count]);
```

This changes `count`, which causes the effect to run again.

---

## Mistake 4 — Using an effect for a simple calculation

Instead of:

```jsx
const [total, setTotal] = useState(0);

useEffect(() => {
  setTotal(price * quantity);
}, [price, quantity]);
```

Prefer:

```jsx
const total = price * quantity;
```

If something can be calculated during rendering from existing props/state, an effect is often unnecessary.

---

# 38. useEffect and Event Handlers Are Different

Do not use `useEffect` for every action.

### Event handler

Use for something caused directly by a user action:

```jsx
function handleSubmit() {
  saveForm();
}
```

### Effect

Use for synchronization caused by rendering/dependency changes:

```jsx
useEffect(() => {
  document.title = `Cart (${cartCount})`;
}, [cartCount]);
```

### Easy rule

```text
User clicked "Save"?
        ↓
Event handler

Component state changed and an external system must synchronize?
        ↓
Effect
```

---

# 39. Real-World Applications

## E-commerce

```text
useState
 ├── Cart quantity
 ├── Selected product
 ├── Search text
 └── Login status

useEffect
 ├── Fetch products
 ├── Save preferences
 ├── Update title
 └── Sync external services
```

## Admin Dashboard

```text
useState
 ├── Filters
 ├── Selected user
 ├── Modal state
 └── Form data

useEffect
 ├── Fetch dashboard data
 ├── Fetch users
 └── Subscribe to updates
```

## Chat Application

```text
useState
 ├── Messages
 ├── Message input
 └── Current room

useEffect
 ├── Connect WebSocket
 ├── Listen for messages
 └── Cleanup connection
```

---

# 40. Graphical Summary

```text
                 React Component
                       │
             ┌─────────┴─────────┐
             │                   │
         useState             useEffect
             │                   │
       Stores UI data      Side effects /
             │             external systems
             │                   │
       setState()           API / Timer /
             │               Events /
             ↓             Subscription
        Re-render               │
             │                   │
             └─────────┬─────────┘
                       ↓
                  Updated UI
```

---

# 41. Mini Project — Product Dashboard

Build a small Product Dashboard using:

### Required features

- Fetch products from an API
- Show loading state
- Show error state
- Search products
- Display product cards
- Add product to cart
- Increase/decrease quantity
- Show cart count
- Update document title
- Clean up effects where required

### Suggested structure

```text
src/
├── components/
│   ├── ProductCard.jsx
│   ├── ProductList.jsx
│   ├── SearchBar.jsx
│   └── Cart.jsx
│
├── App.jsx
├── main.jsx
└── index.css
```

### Concepts to use

```text
useState
useEffect
Props
map()
Keys
Events
Conditional Rendering
```

---

# 42. Final Lab Practical — Student Management Dashboard

## Objective

Build a React Student Management Dashboard using `useState()` and `useEffect()`.

## Requirements

### Student fields

```text
ID
Name
Email
Course
City
```

### Features

1. Add student
2. Display students
3. Delete student
4. Search student
5. Filter by course
6. Edit student
7. Show total students
8. Show empty state
9. Form validation
10. Save students to `localStorage`
11. Load students from `localStorage`
12. Update document title

### Required Hooks

```jsx
useState()
useEffect()
```

### Suggested state

```jsx
const [students, setStudents] = useState([]);
const [name, setName] = useState("");
const [email, setEmail] = useState("");
const [course, setCourse] = useState("");
const [search, setSearch] = useState("");
```

### localStorage effect

```jsx
useEffect(() => {
  const savedStudents = localStorage.getItem("students");

  if (savedStudents) {
    setStudents(JSON.parse(savedStudents));
  }
}, []);
```

### Save effect

```jsx
useEffect(() => {
  localStorage.setItem(
    "students",
    JSON.stringify(students)
  );
}, [students]);
```

### Update title

```jsx
useEffect(() => {
  document.title = `Students: ${students.length}`;
}, [students.length]);
```

---

# 43. Lab Architecture

```text
                 Student Dashboard
                        │
        ┌───────────────┼────────────────┐
        │               │                │
     useState        useEffect        Events
        │               │                │
        │          ┌────┴────┐           │
        │          │         │           │
     Form Data   localStorage API     onClick
     Students    document.title      onSubmit
     Search      subscriptions       onChange
        │               │                │
        └───────────────┼────────────────┘
                        ↓
                   Re-render
                        ↓
                  Updated UI
```

---

# 44. Practice Tasks

## Task 1 — Counter

Create:

- Increment
- Decrement
- Reset

---

## Task 2 — Dark Mode

Use:

```jsx
const [darkMode, setDarkMode] = useState(false);
```

Add a button to switch between light and dark modes.

---

## Task 3 — Character Counter

Create an input and display:

```text
Characters: 15
```

---

## Task 4 — API Users

Fetch users from an API and display:

- Name
- Email
- City

Include:

- Loading
- Error
- Data state

---

## Task 5 — Digital Timer

Create:

```text
00:01
00:02
00:03
```

Use:

```jsx
useEffect()
setInterval()
```

and clean up the interval.

---

## Task 6 — Window Size

Display:

```text
Width: 1366
Height: 768
```

Update when the browser is resized.

---

## Task 7 — Search

Create a search input and use state to filter a list of students.

---

## Task 8 — Shopping Cart

Implement:

- Add item
- Remove item
- Increase quantity
- Decrease quantity
- Total price

---

# 45. Interview Questions

### Beginner

1. What is `useState()`?
2. What does `useState()` return?
3. What is the initial state?
4. What is `useEffect()`?
5. What is a side effect?
6. What is a dependency array?
7. What happens when state changes?
8. Why should state not be mutated directly?
9. Why use functional state updates?
10. Can `useState()` store objects and arrays?

### Intermediate

11. What is lazy state initialization?
12. Why does `useState()` not merge objects automatically?
13. What is the difference between state and props?
14. What happens when an effect has no dependency array?
15. What happens when an effect has `[]`?
16. What happens when an effect has `[count]`?
17. Why do effects need cleanup?
18. What causes an effect to re-run?
19. How can you prevent an infinite effect loop?
20. When should you avoid `useEffect()`?

### Advanced

21. Why should previous state be used for dependent updates?
22. How do you cancel a fetch request?
23. How does `AbortController` work with effects?
24. Why can effects run more than once in development Strict Mode?
25. How do you synchronize a WebSocket connection with a component?
26. What is the difference between an event handler and an effect?
27. How do you avoid unnecessary effects?
28. How do dependency arrays affect effect synchronization?
29. What is stale state/closure behavior in effects?
30. When should complex state logic move from `useState` to `useReducer`?

---

# 46. Quick Revision Cheat Sheet

## useState

```jsx
const [value, setValue] = useState(initialValue);
```

### Update primitive

```jsx
setValue(newValue);
```

### Update using previous state

```jsx
setValue(prev => prev + 1);
```

### Update object

```jsx
setUser(prev => ({
  ...prev,
  name: "Rahul"
}));
```

### Update array

```jsx
setItems(prev => [
  ...prev,
  newItem
]);
```

---

## useEffect

### Every render

```jsx
useEffect(() => {
  // effect
});
```

### After initial mount

```jsx
useEffect(() => {
  // effect
}, []);
```

### When dependency changes

```jsx
useEffect(() => {
  // effect
}, [value]);
```

### Cleanup

```jsx
useEffect(() => {
  // setup

  return () => {
    // cleanup
  };
}, []);
```

---

# 47. Common Beginner Mistakes Checklist

- [ ] Calling Hooks inside conditions
- [ ] Calling Hooks inside loops
- [ ] Calling Hooks inside event handlers
- [ ] Mutating state directly
- [ ] Forgetting the state setter
- [ ] Not using functional updates for dependent state
- [ ] Replacing an object instead of spreading previous state
- [ ] Forgetting effect dependencies
- [ ] Forgetting cleanup for timers/listeners
- [ ] Creating an infinite effect loop
- [ ] Using effects for calculations that can be done during render
- [ ] Fetching data without loading/error handling
- [ ] Ignoring request cancellation where stale requests matter

---

# 48. Key Takeaways

After completing this module, you should understand:

- What React state is
- How `useState()` works
- How to update primitive values
- How to update objects and arrays
- Functional state updates
- Lazy initialization
- Controlled form state
- What side effects are
- How `useEffect()` works
- Dependency arrays
- Cleanup functions
- API calls
- Timers
- Browser event listeners
- Subscriptions
- Request cancellation
- `useState()` + `useEffect()` together
- When an effect is unnecessary
- How Hooks are used in real-world React applications

---

# 49. Module Completion Checklist

### useState

- [ ] Understand `useState`
- [ ] Counter
- [ ] Toggle
- [ ] Input state
- [ ] Multiple states
- [ ] Object state
- [ ] Array state
- [ ] Form state
- [ ] Functional updates
- [ ] Lazy initialization

### useEffect

- [ ] Understand side effects
- [ ] No dependency array
- [ ] Empty dependency array
- [ ] Dependency-based effects
- [ ] API fetching
- [ ] Document title
- [ ] Timer
- [ ] Event listener
- [ ] Subscription
- [ ] Cleanup
- [ ] AbortController
- [ ] Avoid unnecessary effects

### Final Project

- [ ] Student Dashboard
- [ ] CRUD
- [ ] Search
- [ ] Filter
- [ ] localStorage
- [ ] Loading/error handling
- [ ] Document title
- [ ] Proper Hook usage

---

# 50. What Comes Next?

Recommended React learning order after this module:

```text
React Introduction
       ↓
Environment Setup
       ↓
JSX
       ↓
Components
       ↓
Props
       ↓
Lists & Keys
       ↓
Forms
       ↓
State
       ↓
useState()        ← Current Module
       ↓
useEffect()       ← Current Module
       ↓
useContext()
       ↓
useRef()
       ↓
useMemo()
       ↓
useCallback()
       ↓
Custom Hooks
       ↓
React Router
       ↓
API Integration
       ↓
Authentication
       ↓
State Management
       ↓
Redux Toolkit
       ↓
Testing
       ↓
Performance
       ↓
Deployment
```

---

## 🎯 Instructor Note

For teaching beginners, explain the two Hooks with one simple mental model:

> **`useState` remembers data. `useEffect` synchronizes the component with something outside its rendering.**

Start with a counter, then a form, then an API call, and finally combine both Hooks in the Student Management Dashboard.

This progression helps students understand **why Hooks exist**, instead of only memorizing syntax.
