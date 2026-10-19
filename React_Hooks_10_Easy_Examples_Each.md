# React Hooks --- 10 Easy Examples Each

> Beginner-friendly practical guide with 10 simple examples for each
> important React Hook.

------------------------------------------------------------------------

## Table of Contents

1.  [useState](#1-usestate)
2.  [useEffect](#2-useeffect)
3.  [useReducer](#3-usereducer)
4.  [useContext](#4-usecontext)
5.  [useLayoutEffect](#5-uselayouteffect)
6.  [useMemo](#6-usememo)
7.  [useCallback](#7-usecallback)
8.  [Custom Hooks](#8-custom-hooks)
9.  [Quick Hook Comparison](#9-quick-hook-comparison)
10. [Which Hook Should I Use?](#10-which-hook-should-i-use)
11. [Final Practice Project](#11-final-practice-project)

------------------------------------------------------------------------

# 1. `useState`

`useState` is used to store and update data inside a React component.

### Basic Syntax

``` jsx
const [state, setState] = useState(initialValue);
```

------------------------------------------------------------------------

## Example 1 --- Counter

``` jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h2>{count}</h2>

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

**What happens?**

-   `count` stores the current number.
-   `setCount()` updates it.
-   React re-renders the component after the state changes.

------------------------------------------------------------------------

## Example 2 --- Change Name

``` jsx
import { useState } from "react";

function Name() {
  const [name, setName] = useState("Sahil");

  return (
    <div>
      <h2>Hello {name}</h2>

      <button onClick={() => setName("Rahul")}>
        Change Name
      </button>
    </div>
  );
}

export default Name;
```

------------------------------------------------------------------------

## Example 3 --- Show / Hide Text

``` jsx
import { useState } from "react";

function ShowHide() {
  const [show, setShow] = useState(true);

  return (
    <div>
      <button onClick={() => setShow(!show)}>
        Show / Hide
      </button>

      {show && <p>This text is visible.</p>}
    </div>
  );
}

export default ShowHide;
```

------------------------------------------------------------------------

## Example 4 --- Dark Mode Toggle

``` jsx
import { useState } from "react";

function Theme() {
  const [dark, setDark] = useState(false);

  return (
    <div>
      <button onClick={() => setDark(!dark)}>
        Toggle Theme
      </button>

      <h2>{dark ? "Dark Mode" : "Light Mode"}</h2>
    </div>
  );
}

export default Theme;
```

------------------------------------------------------------------------

## Example 5 --- Input Field

``` jsx
import { useState } from "react";

function InputExample() {
  const [name, setName] = useState("");

  return (
    <div>
      <input
        value={name}
        onChange={(e) => setName(e.target.value)}
        placeholder="Enter your name"
      />

      <h2>You entered: {name}</h2>
    </div>
  );
}

export default InputExample;
```

------------------------------------------------------------------------

## Example 6 --- Like Button

``` jsx
import { useState } from "react";

function LikeButton() {
  const [liked, setLiked] = useState(false);

  return (
    <button onClick={() => setLiked(!liked)}>
      {liked ? "❤️ Liked" : "♡ Like"}
    </button>
  );
}

export default LikeButton;
```

------------------------------------------------------------------------

## Example 7 --- Reset Counter

``` jsx
import { useState } from "react";

function ResetCounter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h2>{count}</h2>

      <button onClick={() => setCount(count + 1)}>
        Add
      </button>

      <button onClick={() => setCount(0)}>
        Reset
      </button>
    </div>
  );
}

export default ResetCounter;
```

------------------------------------------------------------------------

## Example 8 --- Object State

``` jsx
import { useState } from "react";

function User() {
  const [user, setUser] = useState({
    name: "Sahil",
    age: 22
  });

  return (
    <div>
      <h2>{user.name}</h2>
      <p>Age: {user.age}</p>

      <button
        onClick={() =>
          setUser({
            ...user,
            age: user.age + 1
          })
        }
      >
        Increase Age
      </button>
    </div>
  );
}

export default User;
```

**Important:** When updating an object, keep the other properties using
the spread operator.

------------------------------------------------------------------------

## Example 9 --- Array State

``` jsx
import { useState } from "react";

function Skills() {
  const [skills, setSkills] = useState(["HTML", "CSS"]);

  const addSkill = () => {
    setSkills([...skills, "React"]);
  };

  return (
    <div>
      {skills.map((skill) => (
        <p key={skill}>{skill}</p>
      ))}

      <button onClick={addSkill}>
        Add React
      </button>
    </div>
  );
}

export default Skills;
```

------------------------------------------------------------------------

## Example 10 --- Functional State Update

Use the previous state when the new state depends on the old state.

``` jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  const increase = () => {
    setCount((previous) => previous + 1);
  };

  return (
    <div>
      <h2>{count}</h2>
      <button onClick={increase}>Add</button>
    </div>
  );
}

export default Counter;
```

------------------------------------------------------------------------

# 2. `useEffect`

`useEffect` is used for **side effects**.

Common examples:

-   API calls
-   Timers
-   Event listeners
-   Updating document title
-   Local storage
-   Subscriptions

### Basic Syntax

``` jsx
useEffect(() => {
  // side effect
}, [dependencies]);
```

------------------------------------------------------------------------

## Example 1 --- Change Document Title

``` jsx
import { useEffect } from "react";

function App() {
  useEffect(() => {
    document.title = "React App";
  }, []);

  return <h2>Hello React</h2>;
}

export default App;
```

------------------------------------------------------------------------

## Example 2 --- Run Only Once

An empty dependency array means the effect runs after the initial mount.

``` jsx
import { useEffect } from "react";

function App() {
  useEffect(() => {
    console.log("Component loaded");
  }, []);

  return <h2>Home Page</h2>;
}

export default App;
```

------------------------------------------------------------------------

## Example 3 --- Run When Name Changes

``` jsx
import { useEffect, useState } from "react";

function App() {
  const [name, setName] = useState("");

  useEffect(() => {
    console.log("Name changed:", name);
  }, [name]);

  return (
    <div>
      <input
        value={name}
        onChange={(e) => setName(e.target.value)}
      />

      <p>{name}</p>
    </div>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 4 --- Timer

``` jsx
import { useEffect, useState } from "react";

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const timer = setInterval(() => {
      setSeconds((previous) => previous + 1);
    }, 1000);

    return () => clearInterval(timer);
  }, []);

  return <h2>{seconds} seconds</h2>;
}

export default Timer;
```

**Why cleanup?**

The interval must be stopped when the component is removed.

------------------------------------------------------------------------

## Example 5 --- Window Resize

``` jsx
import { useEffect, useState } from "react";

function ScreenSize() {
  const [width, setWidth] = useState(window.innerWidth);

  useEffect(() => {
    const handleResize = () => {
      setWidth(window.innerWidth);
    };

    window.addEventListener("resize", handleResize);

    return () => {
      window.removeEventListener("resize", handleResize);
    };
  }, []);

  return <h2>Width: {width}px</h2>;
}

export default ScreenSize;
```

------------------------------------------------------------------------

## Example 6 --- Fetch API Data

``` jsx
import { useEffect, useState } from "react";

function Users() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((response) => response.json())
      .then((data) => setUsers(data));
  }, []);

  return (
    <div>
      {users.map((user) => (
        <p key={user.id}>{user.name}</p>
      ))}
    </div>
  );
}

export default Users;
```

------------------------------------------------------------------------

## Example 7 --- Event Listener Cleanup

``` jsx
import { useEffect } from "react";

function Keyboard() {
  useEffect(() => {
    const handleKey = (event) => {
      console.log("Pressed:", event.key);
    };

    window.addEventListener("keydown", handleKey);

    return () => {
      window.removeEventListener("keydown", handleKey);
    };
  }, []);

  return <h2>Press any key</h2>;
}

export default Keyboard;
```

------------------------------------------------------------------------

## Example 8 --- Local Storage

``` jsx
import { useEffect, useState } from "react";

function App() {
  const [name, setName] = useState("");

  useEffect(() => {
    localStorage.setItem("name", name);
  }, [name]);

  return (
    <input
      value={name}
      onChange={(e) => setName(e.target.value)}
      placeholder="Enter name"
    />
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 9 --- Fetch Data When ID Changes

``` jsx
import { useEffect, useState } from "react";

function User({ id }) {
  const [user, setUser] = useState(null);

  useEffect(() => {
    fetch(`https://jsonplaceholder.typicode.com/users/${id}`)
      .then((response) => response.json())
      .then((data) => setUser(data));
  }, [id]);

  return (
    <div>
      <h2>{user?.name}</h2>
    </div>
  );
}

export default User;
```

------------------------------------------------------------------------

## Example 10 --- Cleanup Timer

``` jsx
import { useEffect } from "react";

function App() {
  useEffect(() => {
    const timer = setTimeout(() => {
      console.log("Hello after 2 seconds");
    }, 2000);

    return () => clearTimeout(timer);
  }, []);

  return <h2>Timer Example</h2>;
}

export default App;
```

------------------------------------------------------------------------

# 3. `useReducer`

`useReducer` is useful when state logic becomes more structured or
complex.

### Basic Syntax

``` jsx
const [state, dispatch] = useReducer(reducer, initialState);
```

A reducer receives:

``` jsx
(state, action)
```

and returns the next state.

------------------------------------------------------------------------

## Example 1 --- Basic Counter

``` jsx
import { useReducer } from "react";

function reducer(state, action) {
  if (action.type === "increment") {
    return state + 1;
  }

  return state;
}

function Counter() {
  const [count, dispatch] = useReducer(reducer, 0);

  return (
    <div>
      <h2>{count}</h2>

      <button onClick={() => dispatch({ type: "increment" })}>
        Add
      </button>
    </div>
  );
}

export default Counter;
```

------------------------------------------------------------------------

## Example 2 --- Increment and Decrement

``` jsx
import { useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return state + 1;

    case "decrement":
      return state - 1;

    default:
      return state;
  }
}

function Counter() {
  const [count, dispatch] = useReducer(reducer, 0);

  return (
    <div>
      <h2>{count}</h2>

      <button onClick={() => dispatch({ type: "increment" })}>
        +
      </button>

      <button onClick={() => dispatch({ type: "decrement" })}>
        -
      </button>
    </div>
  );
}

export default Counter;
```

------------------------------------------------------------------------

## Example 3 --- Reset Counter

``` jsx
import { useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "add":
      return state + 1;

    case "reset":
      return 0;

    default:
      return state;
  }
}

function Counter() {
  const [count, dispatch] = useReducer(reducer, 0);

  return (
    <div>
      <h2>{count}</h2>

      <button onClick={() => dispatch({ type: "add" })}>
        Add
      </button>

      <button onClick={() => dispatch({ type: "reset" })}>
        Reset
      </button>
    </div>
  );
}

export default Counter;
```

------------------------------------------------------------------------

## Example 4 --- Counter With Step

``` jsx
import { useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "add":
      return state + action.amount;

    default:
      return state;
  }
}

function Counter() {
  const [count, dispatch] = useReducer(reducer, 0);

  return (
    <div>
      <h2>{count}</h2>

      <button
        onClick={() =>
          dispatch({
            type: "add",
            amount: 5
          })
        }
      >
        Add 5
      </button>
    </div>
  );
}

export default Counter;
```

------------------------------------------------------------------------

## Example 5 --- Boolean State

``` jsx
import { useReducer } from "react";

function reducer(state, action) {
  if (action.type === "toggle") {
    return !state;
  }

  return state;
}

function Toggle() {
  const [on, dispatch] = useReducer(reducer, false);

  return (
    <button onClick={() => dispatch({ type: "toggle" })}>
      {on ? "ON" : "OFF"}
    </button>
  );
}

export default Toggle;
```

------------------------------------------------------------------------

## Example 6 --- Object State

``` jsx
import { useReducer } from "react";

const initialState = {
  name: "Sahil",
  age: 22
};

function reducer(state, action) {
  switch (action.type) {
    case "changeName":
      return {
        ...state,
        name: action.value
      };

    case "increaseAge":
      return {
        ...state,
        age: state.age + 1
      };

    default:
      return state;
  }
}

function User() {
  const [user, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <h2>{user.name}</h2>
      <p>{user.age}</p>

      <button
        onClick={() =>
          dispatch({
            type: "changeName",
            value: "Rahul"
          })
        }
      >
        Change Name
      </button>

      <button onClick={() => dispatch({ type: "increaseAge" })}>
        Increase Age
      </button>
    </div>
  );
}

export default User;
```

------------------------------------------------------------------------

## Example 7 --- Todo List

``` jsx
import { useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "add":
      return [
        ...state,
        {
          id: Date.now(),
          text: action.text
        }
      ];

    case "remove":
      return state.filter((todo) => todo.id !== action.id);

    default:
      return state;
  }
}

function Todo() {
  const [todos, dispatch] = useReducer(reducer, []);

  return (
    <div>
      <button
        onClick={() =>
          dispatch({
            type: "add",
            text: "Learn React"
          })
        }
      >
        Add Todo
      </button>

      {todos.map((todo) => (
        <p key={todo.id}>
          {todo.text}

          <button
            onClick={() =>
              dispatch({
                type: "remove",
                id: todo.id
              })
            }
          >
            Delete
          </button>
        </p>
      ))}
    </div>
  );
}

export default Todo;
```

------------------------------------------------------------------------

## Example 8 --- Login State

``` jsx
import { useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "login":
      return { loggedIn: true };

    case "logout":
      return { loggedIn: false };

    default:
      return state;
  }
}

function Login() {
  const [state, dispatch] = useReducer(reducer, {
    loggedIn: false
  });

  return (
    <div>
      <h2>
        {state.loggedIn ? "Welcome User" : "Please Login"}
      </h2>

      <button onClick={() => dispatch({ type: "login" })}>
        Login
      </button>

      <button onClick={() => dispatch({ type: "logout" })}>
        Logout
      </button>
    </div>
  );
}

export default Login;
```

------------------------------------------------------------------------

## Example 9 --- Form State

``` jsx
import { useReducer } from "react";

const initialState = {
  name: "",
  email: ""
};

function reducer(state, action) {
  return {
    ...state,
    [action.field]: action.value
  };
}

function Form() {
  const [form, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <input
        value={form.name}
        placeholder="Name"
        onChange={(e) =>
          dispatch({
            field: "name",
            value: e.target.value
          })
        }
      />

      <input
        value={form.email}
        placeholder="Email"
        onChange={(e) =>
          dispatch({
            field: "email",
            value: e.target.value
          })
        }
      />

      <p>{form.name}</p>
      <p>{form.email}</p>
    </div>
  );
}

export default Form;
```

------------------------------------------------------------------------

## Example 10 --- Shopping Cart

``` jsx
import { useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "add":
      return [
        ...state,
        action.product
      ];

    case "remove":
      return state.filter(
        (item) => item.id !== action.id
      );

    default:
      return state;
  }
}

function Cart() {
  const [cart, dispatch] = useReducer(reducer, []);

  const product = {
    id: 1,
    name: "Laptop",
    price: 50000
  };

  return (
    <div>
      <button
        onClick={() =>
          dispatch({
            type: "add",
            product
          })
        }
      >
        Add Laptop
      </button>

      <h3>Cart Items: {cart.length}</h3>

      {cart.map((item) => (
        <p key={item.id}>
          {item.name}
          <button
            onClick={() =>
              dispatch({
                type: "remove",
                id: item.id
              })
            }
          >
            Remove
          </button>
        </p>
      ))}
    </div>
  );
}

export default Cart;
```

------------------------------------------------------------------------

# 4. `useContext`

`useContext` allows components to access shared data without passing
props through every component.

Common uses:

-   Theme
-   User
-   Authentication
-   Language
-   Cart
-   App settings

------------------------------------------------------------------------

## Example 1 --- Simple Theme

``` jsx
import { createContext, useContext } from "react";

const ThemeContext = createContext();

function Child() {
  const theme = useContext(ThemeContext);

  return <h2>Theme: {theme}</h2>;
}

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Child />
    </ThemeContext.Provider>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 2 --- User Name

``` jsx
import { createContext, useContext } from "react";

const UserContext = createContext();

function Profile() {
  const name = useContext(UserContext);

  return <h2>Hello {name}</h2>;
}

function App() {
  return (
    <UserContext.Provider value="Sahil">
      <Profile />
    </UserContext.Provider>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 3 --- Language

``` jsx
import { createContext, useContext } from "react";

const LanguageContext = createContext();

function Message() {
  const language = useContext(LanguageContext);

  return <h2>Language: {language}</h2>;
}

function App() {
  return (
    <LanguageContext.Provider value="English">
      <Message />
    </LanguageContext.Provider>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 4 --- Theme Object

``` jsx
import { createContext, useContext } from "react";

const ThemeContext = createContext();

function Button() {
  const theme = useContext(ThemeContext);

  return (
    <button>
      {theme.buttonText}
    </button>
  );
}

function App() {
  const theme = {
    buttonText: "Click Me",
    mode: "dark"
  };

  return (
    <ThemeContext.Provider value={theme}>
      <Button />
    </ThemeContext.Provider>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 5 --- Authentication

``` jsx
import { createContext, useContext } from "react";

const AuthContext = createContext();

function Dashboard() {
  const user = useContext(AuthContext);

  return <h2>Welcome {user.name}</h2>;
}

function App() {
  const user = {
    name: "Sahil",
    loggedIn: true
  };

  return (
    <AuthContext.Provider value={user}>
      <Dashboard />
    </AuthContext.Provider>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 6 --- Cart Count

``` jsx
import { createContext, useContext } from "react";

const CartContext = createContext();

function CartIcon() {
  const cartCount = useContext(CartContext);

  return <h2>Cart: {cartCount}</h2>;
}

function App() {
  return (
    <CartContext.Provider value={3}>
      <CartIcon />
    </CartContext.Provider>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 7 --- App Settings

``` jsx
import { createContext, useContext } from "react";

const SettingsContext = createContext();

function Settings() {
  const settings = useContext(SettingsContext);

  return (
    <div>
      <p>Language: {settings.language}</p>
      <p>Theme: {settings.theme}</p>
    </div>
  );
}

function App() {
  const settings = {
    language: "English",
    theme: "dark"
  };

  return (
    <SettingsContext.Provider value={settings}>
      <Settings />
    </SettingsContext.Provider>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 8 --- Multiple Context Values

``` jsx
import { createContext, useContext } from "react";

const UserContext = createContext();
const ThemeContext = createContext();

function Profile() {
  const user = useContext(UserContext);
  const theme = useContext(ThemeContext);

  return (
    <div>
      <h2>{user}</h2>
      <p>{theme}</p>
    </div>
  );
}

function App() {
  return (
    <UserContext.Provider value="Sahil">
      <ThemeContext.Provider value="dark">
        <Profile />
      </ThemeContext.Provider>
    </UserContext.Provider>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 9 --- Context + State

``` jsx
import {
  createContext,
  useContext,
  useState
} from "react";

const ThemeContext = createContext();

function Button() {
  const { dark, setDark } = useContext(ThemeContext);

  return (
    <button onClick={() => setDark(!dark)}>
      {dark ? "Dark" : "Light"}
    </button>
  );
}

function App() {
  const [dark, setDark] = useState(false);

  return (
    <ThemeContext.Provider value={{ dark, setDark }}>
      <Button />
    </ThemeContext.Provider>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 10 --- Custom Context Hook

``` jsx
import {
  createContext,
  useContext
} from "react";

const UserContext = createContext();

function useUser() {
  return useContext(UserContext);
}

function Profile() {
  const user = useUser();

  return <h2>{user.name}</h2>;
}

function App() {
  const user = {
    name: "Sahil"
  };

  return (
    <UserContext.Provider value={user}>
      <Profile />
    </UserContext.Provider>
  );
}

export default App;
```

------------------------------------------------------------------------

# 5. `useLayoutEffect`

`useLayoutEffect` is similar to `useEffect`, but it runs **after React
updates the DOM and before the browser paints the screen**.

It is useful when you need to:

-   Measure an element
-   Read layout information
-   Adjust scroll position
-   Make a visual adjustment before the user sees the screen

### Basic Syntax

``` jsx
useLayoutEffect(() => {
  // read or update layout
}, []);
```

> **Important:** Prefer `useEffect` for normal side effects.
> `useLayoutEffect` can block painting and should be used when the
> timing actually matters.

------------------------------------------------------------------------

## Example 1 --- Measure Width

``` jsx
import {
  useLayoutEffect,
  useRef,
  useState
} from "react";

function Box() {
  const boxRef = useRef(null);
  const [width, setWidth] = useState(0);

  useLayoutEffect(() => {
    setWidth(boxRef.current.getBoundingClientRect().width);
  }, []);

  return (
    <div>
      <div ref={boxRef} style={{ width: "300px" }}>
        Box
      </div>

      <p>Width: {width}px</p>
    </div>
  );
}

export default Box;
```

------------------------------------------------------------------------

## Example 2 --- Measure Height

``` jsx
import {
  useLayoutEffect,
  useRef,
  useState
} from "react";

function Box() {
  const ref = useRef(null);
  const [height, setHeight] = useState(0);

  useLayoutEffect(() => {
    setHeight(ref.current.offsetHeight);
  }, []);

  return (
    <div>
      <div ref={ref}>
        This is a box with some content.
      </div>

      <p>Height: {height}px</p>
    </div>
  );
}

export default Box;
```

------------------------------------------------------------------------

## Example 3 --- Set Scroll Position

``` jsx
import {
  useLayoutEffect,
  useRef
} from "react";

function Chat() {
  const chatRef = useRef(null);

  useLayoutEffect(() => {
    chatRef.current.scrollTop =
      chatRef.current.scrollHeight;
  }, []);

  return (
    <div
      ref={chatRef}
      style={{
        height: "100px",
        overflow: "auto"
      }}
    >
      <p>Hello</p>
      <p>How are you?</p>
      <p>I am learning React.</p>
      <p>React Hooks are useful.</p>
    </div>
  );
}

export default Chat;
```

------------------------------------------------------------------------

## Example 4 --- Read Bounding Rectangle

``` jsx
import {
  useLayoutEffect,
  useRef
} from "react";

function Box() {
  const ref = useRef(null);

  useLayoutEffect(() => {
    const rectangle =
      ref.current.getBoundingClientRect();

    console.log("Top:", rectangle.top);
    console.log("Left:", rectangle.left);
  }, []);

  return <div ref={ref}>Hello</div>;
}

export default Box;
```

------------------------------------------------------------------------

## Example 5 --- Focus Input

``` jsx
import {
  useLayoutEffect,
  useRef
} from "react";

function App() {
  const inputRef = useRef(null);

  useLayoutEffect(() => {
    inputRef.current.focus();
  }, []);

  return (
    <input
      ref={inputRef}
      placeholder="Enter your name"
    />
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 6 --- Calculate Position

``` jsx
import {
  useLayoutEffect,
  useRef,
  useState
} from "react";

function Box() {
  const ref = useRef(null);
  const [top, setTop] = useState(0);

  useLayoutEffect(() => {
    setTop(ref.current.offsetTop);
  }, []);

  return (
    <div>
      <div ref={ref}>My Box</div>
      <p>Top position: {top}px</p>
    </div>
  );
}

export default Box;
```

------------------------------------------------------------------------

## Example 7 --- Read Height After Content Changes

``` jsx
import {
  useLayoutEffect,
  useRef,
  useState
} from "react";

function Content() {
  const ref = useRef(null);
  const [showMore, setShowMore] = useState(false);
  const [height, setHeight] = useState(0);

  useLayoutEffect(() => {
    setHeight(ref.current.offsetHeight);
  }, [showMore]);

  return (
    <div>
      <div ref={ref}>
        <p>Basic content</p>

        {showMore && (
          <p>
            Extra content appears here.
          </p>
        )}
      </div>

      <p>Height: {height}px</p>

      <button onClick={() => setShowMore(!showMore)}>
        Show More
      </button>
    </div>
  );
}

export default Content;
```

------------------------------------------------------------------------

## Example 8 --- Scroll Chat Box

``` jsx
import {
  useLayoutEffect,
  useRef
} from "react";

function Chat({ messages }) {
  const ref = useRef(null);

  useLayoutEffect(() => {
    ref.current.scrollTop =
      ref.current.scrollHeight;
  }, [messages]);

  return (
    <div
      ref={ref}
      style={{
        height: "150px",
        overflowY: "auto"
      }}
    >
      {messages.map((message, index) => (
        <p key={index}>{message}</p>
      ))}
    </div>
  );
}

export default Chat;
```

------------------------------------------------------------------------

## Example 9 --- Measure Before Animation

``` jsx
import {
  useLayoutEffect,
  useRef
} from "react";

function Box() {
  const ref = useRef(null);

  useLayoutEffect(() => {
    const width = ref.current.offsetWidth;

    console.log("Starting width:", width);

    ref.current.style.transform =
      "translateX(50px)";
  }, []);

  return (
    <div ref={ref}>
      Animated Box
    </div>
  );
}

export default Box;
```

------------------------------------------------------------------------

## Example 10 --- `useLayoutEffect` vs `useEffect`

``` jsx
import {
  useEffect,
  useLayoutEffect
} from "react";

function App() {
  useLayoutEffect(() => {
    console.log("Layout effect");
  }, []);

  useEffect(() => {
    console.log("Normal effect");
  }, []);

  return <h2>Check the console</h2>;
}

export default App;
```

**Simple idea:**

``` text
React updates DOM
       ↓
useLayoutEffect
       ↓
Browser paints screen
       ↓
useEffect
```

------------------------------------------------------------------------

# 6. `useMemo`

`useMemo` caches a calculated value.

It is mainly useful when a calculation is expensive or when you want to
avoid repeating a calculation unnecessarily.

### Basic Syntax

``` jsx
const result = useMemo(() => {
  return calculation;
}, [dependencies]);
```

> Do not use `useMemo` for every small calculation. It is a performance
> optimization, not a requirement.

------------------------------------------------------------------------

## Example 1 --- Simple Calculation

``` jsx
import { useMemo } from "react";

function App() {
  const result = useMemo(() => {
    return 10 * 20;
  }, []);

  return <h2>{result}</h2>;
}

export default App;
```

------------------------------------------------------------------------

## Example 2 --- Filter Products

``` jsx
import { useMemo, useState } from "react";

function Products() {
  const [search, setSearch] = useState("");

  const products = [
    "Laptop",
    "Mouse",
    "Keyboard",
    "Monitor"
  ];

  const filteredProducts = useMemo(() => {
    return products.filter((product) =>
      product.toLowerCase().includes(search.toLowerCase())
    );
  }, [search]);

  return (
    <div>
      <input
        value={search}
        onChange={(e) => setSearch(e.target.value)}
        placeholder="Search"
      />

      {filteredProducts.map((product) => (
        <p key={product}>{product}</p>
      ))}
    </div>
  );
}

export default Products;
```

------------------------------------------------------------------------

## Example 3 --- Search Filter

``` jsx
import { useMemo, useState } from "react";

function Search() {
  const [query, setQuery] = useState("");

  const users = [
    "Sahil",
    "Rahul",
    "Amit",
    "Priya"
  ];

  const result = useMemo(() => {
    return users.filter((user) =>
      user.toLowerCase().includes(query.toLowerCase())
    );
  }, [query]);

  return (
    <div>
      <input
        value={query}
        onChange={(e) => setQuery(e.target.value)}
      />

      {result.map((user) => (
        <p key={user}>{user}</p>
      ))}
    </div>
  );
}

export default Search;
```

------------------------------------------------------------------------

## Example 4 --- Expensive Calculation

``` jsx
import { useMemo, useState } from "react";

function App() {
  const [number, setNumber] = useState(10);
  const [dark, setDark] = useState(false);

  const result = useMemo(() => {
    console.log("Calculating...");

    let total = 0;

    for (let i = 0; i < 1000000; i++) {
      total += number;
    }

    return total;
  }, [number]);

  return (
    <div>
      <h2>{result}</h2>

      <button onClick={() => setNumber(number + 1)}>
        Change Number
      </button>

      <button onClick={() => setDark(!dark)}>
        Toggle Theme
      </button>
    </div>
  );
}

export default App;
```

Changing `dark` does not recalculate `result` because `dark` is not a
dependency.

------------------------------------------------------------------------

## Example 5 --- Calculate Total Price

``` jsx
import { useMemo } from "react";

function Cart() {
  const products = [
    { name: "Laptop", price: 50000 },
    { name: "Mouse", price: 1000 },
    { name: "Keyboard", price: 2000 }
  ];

  const total = useMemo(() => {
    return products.reduce(
      (sum, product) => sum + product.price,
      0
    );
  }, []);

  return <h2>Total: ₹{total}</h2>;
}

export default Cart;
```

------------------------------------------------------------------------

## Example 6 --- Calculate Average

``` jsx
import { useMemo } from "react";

function Marks() {
  const marks = [80, 75, 90, 85];

  const average = useMemo(() => {
    const total = marks.reduce(
      (sum, mark) => sum + mark,
      0
    );

    return total / marks.length;
  }, []);

  return <h2>Average: {average}</h2>;
}

export default Marks;
```

------------------------------------------------------------------------

## Example 7 --- Sort Data

``` jsx
import { useMemo } from "react";

function Students() {
  const students = [
    "Rahul",
    "Amit",
    "Sahil",
    "Priya"
  ];

  const sortedStudents = useMemo(() => {
    return [...students].sort();
  }, []);

  return (
    <div>
      {sortedStudents.map((student) => (
        <p key={student}>{student}</p>
      ))}
    </div>
  );
}

export default Students;
```

------------------------------------------------------------------------

## Example 8 --- Full Name

``` jsx
import { useMemo } from "react";

function Profile() {
  const firstName = "Sahil";
  const lastName = "Shaikh";

  const fullName = useMemo(() => {
    return `${firstName} ${lastName}`;
  }, [firstName, lastName]);

  return <h2>{fullName}</h2>;
}

export default Profile;
```

------------------------------------------------------------------------

## Example 9 --- Product Category

``` jsx
import { useMemo } from "react";

function Product() {
  const price = 50000;

  const category = useMemo(() => {
    if (price > 40000) {
      return "Premium";
    }

    return "Budget";
  }, [price]);

  return <h2>{category}</h2>;
}

export default Product;
```

------------------------------------------------------------------------

## Example 10 --- Fibonacci

``` jsx
import { useMemo, useState } from "react";

function fibonacci(n) {
  if (n <= 1) {
    return n;
  }

  return fibonacci(n - 1) + fibonacci(n - 2);
}

function App() {
  const [number, setNumber] = useState(10);

  const result = useMemo(() => {
    return fibonacci(number);
  }, [number]);

  return (
    <div>
      <h2>Result: {result}</h2>

      <button onClick={() => setNumber(number + 1)}>
        Next
      </button>
    </div>
  );
}

export default App;
```

------------------------------------------------------------------------

# 7. `useCallback`

`useCallback` caches a **function reference**.

It is especially useful when:

-   Passing a function to a child component
-   The child uses `React.memo`
-   A function is used as a dependency of another Hook

### Basic Syntax

``` jsx
const functionName = useCallback(() => {
  // function
}, [dependencies]);
```

> `useCallback` does not automatically make every application faster.
> Use it when stable function identity is useful.

------------------------------------------------------------------------

## Example 1 --- Basic Callback

``` jsx
import { useCallback } from "react";

function App() {
  const sayHello = useCallback(() => {
    console.log("Hello React");
  }, []);

  return (
    <button onClick={sayHello}>
      Say Hello
    </button>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 2 --- Callback With State

``` jsx
import {
  useCallback,
  useState
} from "react";

function App() {
  const [count, setCount] = useState(0);

  const increase = useCallback(() => {
    setCount((previous) => previous + 1);
  }, []);

  return (
    <div>
      <h2>{count}</h2>
      <button onClick={increase}>
        Add
      </button>
    </div>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 3 --- Pass Function to Child

``` jsx
import {
  useCallback,
  useState
} from "react";

function Child({ onClick }) {
  return (
    <button onClick={onClick}>
      Child Button
    </button>
  );
}

function App() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    console.log("Child clicked");
  }, []);

  return (
    <div>
      <h2>{count}</h2>

      <button onClick={() => setCount(count + 1)}>
        Parent Count
      </button>

      <Child onClick={handleClick} />
    </div>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 4 --- Counter Callback

``` jsx
import {
  useCallback,
  useState
} from "react";

function App() {
  const [count, setCount] = useState(0);

  const add = useCallback(() => {
    setCount((value) => value + 1);
  }, []);

  return (
    <div>
      <h2>{count}</h2>
      <button onClick={add}>Add</button>
    </div>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 5 --- Delete Item

``` jsx
import {
  useCallback,
  useState
} from "react";

function App() {
  const [items, setItems] = useState([
    { id: 1, name: "Laptop" },
    { id: 2, name: "Mouse" }
  ]);

  const deleteItem = useCallback((id) => {
    setItems((previous) =>
      previous.filter((item) => item.id !== id)
    );
  }, []);

  return (
    <div>
      {items.map((item) => (
        <p key={item.id}>
          {item.name}

          <button onClick={() => deleteItem(item.id)}>
            Delete
          </button>
        </p>
      ))}
    </div>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 6 --- Add Item

``` jsx
import {
  useCallback,
  useState
} from "react";

function App() {
  const [items, setItems] = useState([]);

  const addItem = useCallback(() => {
    setItems((previous) => [
      ...previous,
      `Item ${previous.length + 1}`
    ]);
  }, []);

  return (
    <div>
      <button onClick={addItem}>
        Add Item
      </button>

      {items.map((item) => (
        <p key={item}>{item}</p>
      ))}
    </div>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 7 --- Search Callback

``` jsx
import {
  useCallback,
  useState
} from "react";

function App() {
  const [query, setQuery] = useState("");

  const search = useCallback((value) => {
    console.log("Searching for:", value);
  }, []);

  return (
    <input
      value={query}
      onChange={(e) => {
        setQuery(e.target.value);
        search(e.target.value);
      }}
      placeholder="Search"
    />
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 8 --- Form Submit Callback

``` jsx
import {
  useCallback,
  useState
} from "react";

function App() {
  const [name, setName] = useState("");

  const submitForm = useCallback(() => {
    console.log("Submitted:", name);
  }, [name]);

  return (
    <div>
      <input
        value={name}
        onChange={(e) => setName(e.target.value)}
      />

      <button onClick={submitForm}>
        Submit
      </button>
    </div>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 9 --- Callback With Dependency

``` jsx
import {
  useCallback,
  useState
} from "react";

function App() {
  const [count, setCount] = useState(0);

  const showCount = useCallback(() => {
    console.log(count);
  }, [count]);

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>
        Add
      </button>

      <button onClick={showCount}>
        Show Count
      </button>
    </div>
  );
}

export default App;
```

When `count` changes, React creates a new callback because `count` is a
dependency.

------------------------------------------------------------------------

## Example 10 --- `useCallback` With `React.memo`

``` jsx
import {
  memo,
  useCallback,
  useState
} from "react";

const Child = memo(function Child({ onClick }) {
  console.log("Child rendered");

  return (
    <button onClick={onClick}>
      Child Button
    </button>
  );
});

function App() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    console.log("Clicked");
  }, []);

  return (
    <div>
      <h2>{count}</h2>

      <button onClick={() => setCount(count + 1)}>
        Parent Count
      </button>

      <Child onClick={handleClick} />
    </div>
  );
}

export default App;
```

Here `useCallback` keeps the same function reference while its
dependencies remain unchanged.

------------------------------------------------------------------------

# 8. Custom Hooks

A **Custom Hook** is a reusable function that contains React Hook logic.

Rules:

1.  The name should normally start with `use`.
2.  A custom Hook can call other Hooks.
3.  It helps avoid repeating the same logic in multiple components.

------------------------------------------------------------------------

## Example 1 --- `useCounter`

### Custom Hook

``` jsx
import { useState } from "react";

function useCounter(initialValue = 0) {
  const [count, setCount] = useState(initialValue);

  const increment = () => {
    setCount((value) => value + 1);
  };

  const decrement = () => {
    setCount((value) => value - 1);
  };

  const reset = () => {
    setCount(initialValue);
  };

  return {
    count,
    increment,
    decrement,
    reset
  };
}

export default useCounter;
```

### Usage

``` jsx
import useCounter from "./useCounter";

function App() {
  const {
    count,
    increment,
    decrement,
    reset
  } = useCounter(10);

  return (
    <div>
      <h2>{count}</h2>

      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 2 --- `useToggle`

``` jsx
import { useState } from "react";

function useToggle(initialValue = false) {
  const [value, setValue] = useState(initialValue);

  const toggle = () => {
    setValue((previous) => !previous);
  };

  return [value, toggle];
}

export default useToggle;
```

### Usage

``` jsx
import useToggle from "./useToggle";

function App() {
  const [show, toggle] = useToggle(false);

  return (
    <div>
      <button onClick={toggle}>
        Show / Hide
      </button>

      {show && <p>Hello React</p>}
    </div>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 3 --- `useInput`

``` jsx
import { useState } from "react";

function useInput(initialValue = "") {
  const [value, setValue] = useState(initialValue);

  const onChange = (event) => {
    setValue(event.target.value);
  };

  return {
    value,
    onChange
  };
}

export default useInput;
```

### Usage

``` jsx
import useInput from "./useInput";

function App() {
  const name = useInput("");

  return (
    <div>
      <input
        {...name}
        placeholder="Enter your name"
      />

      <p>Hello {name.value}</p>
    </div>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 4 --- `useDocumentTitle`

``` jsx
import { useEffect } from "react";

function useDocumentTitle(title) {
  useEffect(() => {
    document.title = title;
  }, [title]);
}

export default useDocumentTitle;
```

### Usage

``` jsx
import useDocumentTitle from "./useDocumentTitle";

function App() {
  useDocumentTitle("Home Page");

  return <h2>Home</h2>;
}

export default App;
```

------------------------------------------------------------------------

## Example 5 --- `useLocalStorage`

``` jsx
import {
  useEffect,
  useState
} from "react";

function useLocalStorage(key, initialValue) {
  const [value, setValue] = useState(() => {
    const saved = localStorage.getItem(key);

    return saved
      ? JSON.parse(saved)
      : initialValue;
  });

  useEffect(() => {
    localStorage.setItem(
      key,
      JSON.stringify(value)
    );
  }, [key, value]);

  return [value, setValue];
}

export default useLocalStorage;
```

### Usage

``` jsx
import useLocalStorage from "./useLocalStorage";

function App() {
  const [name, setName] =
    useLocalStorage("name", "");

  return (
    <input
      value={name}
      onChange={(e) => setName(e.target.value)}
      placeholder="Enter name"
    />
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 6 --- `useWindowSize`

``` jsx
import {
  useEffect,
  useState
} from "react";

function useWindowSize() {
  const [width, setWidth] =
    useState(window.innerWidth);

  useEffect(() => {
    const updateSize = () => {
      setWidth(window.innerWidth);
    };

    window.addEventListener(
      "resize",
      updateSize
    );

    return () => {
      window.removeEventListener(
        "resize",
        updateSize
      );
    };
  }, []);

  return width;
}

export default useWindowSize;
```

### Usage

``` jsx
import useWindowSize from "./useWindowSize";

function App() {
  const width = useWindowSize();

  return <h2>Width: {width}px</h2>;
}

export default App;
```

------------------------------------------------------------------------

## Example 7 --- `useFetch`

``` jsx
import {
  useEffect,
  useState
} from "react";

function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    setLoading(true);

    fetch(url)
      .then((response) => response.json())
      .then((result) => {
        setData(result);
        setLoading(false);
      });
  }, [url]);

  return {
    data,
    loading
  };
}

export default useFetch;
```

### Usage

``` jsx
import useFetch from "./useFetch";

function App() {
  const { data, loading } = useFetch(
    "https://jsonplaceholder.typicode.com/users"
  );

  if (loading) {
    return <p>Loading...</p>;
  }

  return (
    <div>
      {data.map((user) => (
        <p key={user.id}>{user.name}</p>
      ))}
    </div>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 8 --- `useOnlineStatus`

``` jsx
import {
  useEffect,
  useState
} from "react";

function useOnlineStatus() {
  const [online, setOnline] =
    useState(navigator.onLine);

  useEffect(() => {
    const onlineHandler = () => {
      setOnline(true);
    };

    const offlineHandler = () => {
      setOnline(false);
    };

    window.addEventListener(
      "online",
      onlineHandler
    );

    window.addEventListener(
      "offline",
      offlineHandler
    );

    return () => {
      window.removeEventListener(
        "online",
        onlineHandler
      );

      window.removeEventListener(
        "offline",
        offlineHandler
      );
    };
  }, []);

  return online;
}

export default useOnlineStatus;
```

### Usage

``` jsx
import useOnlineStatus from "./useOnlineStatus";

function App() {
  const online = useOnlineStatus();

  return (
    <h2>
      {online
        ? "You are Online"
        : "You are Offline"}
    </h2>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 9 --- `usePrevious`

``` jsx
import {
  useEffect,
  useRef
} from "react";

function usePrevious(value) {
  const ref = useRef();

  useEffect(() => {
    ref.current = value;
  }, [value]);

  return ref.current;
}

export default usePrevious;
```

### Usage

``` jsx
import {
  useState
} from "react";

import usePrevious from "./usePrevious";

function App() {
  const [count, setCount] = useState(0);

  const previousCount =
    usePrevious(count);

  return (
    <div>
      <h2>Current: {count}</h2>
      <h2>Previous: {previousCount}</h2>

      <button
        onClick={() =>
          setCount(count + 1)
        }
      >
        Add
      </button>
    </div>
  );
}

export default App;
```

------------------------------------------------------------------------

## Example 10 --- `useDebounce`

Debouncing is useful for search boxes and API calls.

``` jsx
import {
  useEffect,
  useState
} from "react";

function useDebounce(value, delay = 500) {
  const [debouncedValue, setDebouncedValue] =
    useState(value);

  useEffect(() => {
    const timer = setTimeout(() => {
      setDebouncedValue(value);
    }, delay);

    return () => {
      clearTimeout(timer);
    };
  }, [value, delay]);

  return debouncedValue;
}

export default useDebounce;
```

### Usage

``` jsx
import {
  useState
} from "react";

import useDebounce from "./useDebounce";

function App() {
  const [search, setSearch] = useState("");

  const debouncedSearch =
    useDebounce(search, 500);

  return (
    <div>
      <input
        value={search}
        onChange={(e) =>
          setSearch(e.target.value)
        }
        placeholder="Search"
      />

      <p>
        Searching for: {debouncedSearch}
      </p>
    </div>
  );
}

export default App;
```

------------------------------------------------------------------------

# 9. Quick Hook Comparison

  -----------------------------------------------------------------------
  Hook                    Main Purpose            Simple Example
  ----------------------- ----------------------- -----------------------
  `useState`              Store changing          Counter
                          component data          

  `useEffect`             Perform side effects    API call

  `useReducer`            Manage                  Todo
                          structured/complex      
                          state                   

  `useContext`            Share data without prop Theme
                          drilling                

  `useLayoutEffect`       Read/change layout      Measure element
                          before paint            

  `useMemo`               Cache calculated values Filter products

  `useCallback`           Cache function          Memoized child callback
                          references              

  Custom Hook             Reuse React logic       `useCounter`
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# 10. Which Hook Should I Use?

## Need to store changing data?

Use:

``` jsx
useState()
```

Example:

``` text
count
name
email
modal open/close
```

------------------------------------------------------------------------

## Need an API call?

Usually:

``` jsx
useEffect()
```

Example:

``` text
Fetch users
Fetch products
Load dashboard data
```

------------------------------------------------------------------------

## State logic is becoming complicated?

Use:

``` jsx
useReducer()
```

Example:

``` text
Todo application
Shopping cart
Complex form
Authentication state
```

------------------------------------------------------------------------

## Need shared application data?

Use:

``` jsx
useContext()
```

Example:

``` text
Theme
User
Language
Authentication
```

------------------------------------------------------------------------

## Need to measure an element before the browser paints?

Use:

``` jsx
useLayoutEffect()
```

Example:

``` text
Element width
Element height
Position
Scroll adjustment
```

------------------------------------------------------------------------

## Need to cache an expensive calculation?

Use:

``` jsx
useMemo()
```

Example:

``` text
Large list filtering
Large calculations
Sorting large datasets
```

------------------------------------------------------------------------

## Need to keep the same function reference?

Use:

``` jsx
useCallback()
```

Example:

``` text
Callback passed to React.memo child
Function used in dependency array
```

------------------------------------------------------------------------

## Repeating the same Hook logic in multiple components?

Create:

``` jsx
Custom Hook
```

Example:

``` text
useCounter()
useFetch()
useLocalStorage()
useDebounce()
```

------------------------------------------------------------------------

# 11. Final Practice Project

## Student Management Dashboard

After learning these examples, build a small **Student Management
Dashboard**.

### Features

``` text
Student Management Dashboard
│
├── Add Student
├── Delete Student
├── Edit Student
├── Search Student
├── Filter Students
├── Student Details
├── Dark Mode
├── Online/Offline Status
├── Local Storage
└── API Data
```

### Suggested Hook Usage

  Feature                      Hook
  ---------------------------- --------------------------
  Student form                 `useState`
  API loading                  `useEffect`
  Student operations           `useReducer`
  Dark mode                    `useContext`
  Measure dashboard element    `useLayoutEffect`
  Search/filter optimization   `useMemo`
  Child callbacks              `useCallback`
  Reusable form logic          Custom Hook
  Local storage                Custom `useLocalStorage`
  Search delay                 Custom `useDebounce`

------------------------------------------------------------------------

# Recommended Learning Order

For beginners, learn the Hooks in this order:

``` text
1. useState
      ↓
2. useEffect
      ↓
3. useContext
      ↓
4. useReducer
      ↓
5. Custom Hooks
      ↓
6. useMemo
      ↓
7. useCallback
      ↓
8. useLayoutEffect
```

------------------------------------------------------------------------

# Beginner Practice Questions

Try building these without looking at the examples:

1.  Counter with `+`, `-`, and Reset.
2.  Name input with live preview.
3.  Like/Unlike button.
4.  Dark mode toggle.
5.  Timer using `useEffect`.
6.  Fetch users from an API.
7.  Todo app using `useReducer`.
8.  Theme switcher using `useContext`.
9.  Search products using `useMemo`.
10. Child component optimization using `useCallback`.
11. Create your own `useCounter`.
12. Create your own `useFetch`.
13. Create your own `useLocalStorage`.
14. Create your own `useDebounce`.
15. Combine multiple Hooks in one mini project.

------------------------------------------------------------------------

# Important Interview Points

### `useState`

**Question:** What is `useState`?

**Answer:** `useState` is a React Hook used to add and manage state in a
functional component.

------------------------------------------------------------------------

### `useEffect`

**Question:** Why do we use `useEffect`?

**Answer:** It is used to synchronize a component with external systems
and perform side effects such as API calls, timers, subscriptions, and
browser APIs.

------------------------------------------------------------------------

### `useReducer`

**Question:** When should we use `useReducer` instead of `useState`?

**Answer:** When state logic is more complex, has multiple related
transitions, or benefits from centralized action-based updates.

------------------------------------------------------------------------

### `useContext`

**Question:** What problem does `useContext` solve?

**Answer:** It helps share data across components without manually
passing props through every intermediate component.

------------------------------------------------------------------------

### `useMemo`

**Question:** What does `useMemo` cache?

**Answer:** It caches the result of a calculation between renders until
its dependencies change.

------------------------------------------------------------------------

### `useCallback`

**Question:** What does `useCallback` cache?

**Answer:** It caches a function reference between renders until its
dependencies change.

------------------------------------------------------------------------

### `useLayoutEffect`

**Question:** What is the difference between `useEffect` and
`useLayoutEffect`?

**Answer:** `useLayoutEffect` runs synchronously after DOM updates and
before the browser paints, while `useEffect` is generally used for
effects that do not need to block painting.

------------------------------------------------------------------------

### Custom Hook

**Question:** What is a Custom Hook?

**Answer:** A Custom Hook is a JavaScript function whose name starts
with `use` and that reuses React Hook-based logic across components.

------------------------------------------------------------------------

# Final Cheat Sheet

``` text
useState
→ Store state

useEffect
→ Side effects

useReducer
→ Complex state logic

useContext
→ Shared data

useLayoutEffect
→ DOM/layout work before paint

useMemo
→ Cache calculated value

useCallback
→ Cache function reference

Custom Hook
→ Reuse Hook logic
```

------------------------------------------------------------------------

## Final Tip

Do not try to memorize all Hooks at once.

First understand:

``` text
State
  ↓
Re-render
  ↓
Side Effect
  ↓
Shared State
  ↓
Complex State
  ↓
Performance Optimization
  ↓
Reusable Logic
```

Once this flow is clear, React Hooks become much easier to understand
and use in real projects.
