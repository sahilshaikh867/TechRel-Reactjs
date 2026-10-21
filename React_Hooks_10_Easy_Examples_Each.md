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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Counter** is explained below. Read the code
first, then trace these lines in order.

1.  `import { useState } from "react";` --- Imports the React API or
    Hook needed by this example.
2.  `function Counter() {` --- Declares a function or React component.
3.  `const [count, setCount] = useState(0);` --- Creates state: the
    first value is the current state and the second value updates it.
4.  `return (` --- Begins the JSX returned by the component.
5.  `<div>` --- Creates a JSX element that React will render into the
    UI.
6.  `<h2>{count}</h2>` --- Creates a JSX element that React will render
    into the UI.
7.  `<button onClick={() => setCount(count + 1)}>` --- Connects a
    function to the click event of the JSX element.
8.  `+` --- Supports the surrounding React logic, data flow, or rendered
    UI.
9.  `</button>` --- Creates a JSX element that React will render into
    the UI.
10. `<button onClick={() => setCount(count - 1)}>` --- Connects a
    function to the click event of the JSX element.
11. `-` --- Supports the surrounding React logic, data flow, or rendered
    UI.
12. `</button>` --- Creates a JSX element that React will render into
    the UI.
13. `</div>` --- Creates a JSX element that React will render into the
    UI.
14. `);` --- Closes the current function, callback, conditional, or JSX
    block.
15. `}` --- Closes the current function, callback, conditional, or JSX
    block.
16. `export default Counter;` --- Exports this component or Hook so
    another file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Change Name** is explained below. Read the
code first, then trace these lines in order.

1.  `import { useState } from "react";` --- Imports the React API or
    Hook needed by this example.
2.  `function Name() {` --- Declares a function or React component.
3.  `const [name, setName] = useState("Sahil");` --- Creates state: the
    first value is the current state and the second value updates it.
4.  `return (` --- Begins the JSX returned by the component.
5.  `<div>` --- Creates a JSX element that React will render into the
    UI.
6.  `<h2>Hello {name}</h2>` --- Creates a JSX element that React will
    render into the UI.
7.  `<button onClick={() => setName("Rahul")}>` --- Connects a function
    to the click event of the JSX element.
8.  `Change Name` --- Supports the surrounding React logic, data flow,
    or rendered UI.
9.  `</button>` --- Creates a JSX element that React will render into
    the UI.
10. `</div>` --- Creates a JSX element that React will render into the
    UI.
11. `);` --- Closes the current function, callback, conditional, or JSX
    block.
12. `}` --- Closes the current function, callback, conditional, or JSX
    block.
13. `export default Name;` --- Exports this component or Hook so another
    file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Show / Hide Text** is explained below. Read
the code first, then trace these lines in order.

1.  `import { useState } from "react";` --- Imports the React API or
    Hook needed by this example.
2.  `function ShowHide() {` --- Declares a function or React component.
3.  `const [show, setShow] = useState(true);` --- Creates state: the
    first value is the current state and the second value updates it.
4.  `return (` --- Begins the JSX returned by the component.
5.  `<div>` --- Creates a JSX element that React will render into the
    UI.
6.  `<button onClick={() => setShow(!show)}>` --- Connects a function to
    the click event of the JSX element.
7.  `Show / Hide` --- Supports the surrounding React logic, data flow,
    or rendered UI.
8.  `</button>` --- Creates a JSX element that React will render into
    the UI.
9.  `{show && <p>This text is visible.</p>}` --- Conditionally renders
    the expression on the right when the left side is truthy.
10. `</div>` --- Creates a JSX element that React will render into the
    UI.
11. `);` --- Closes the current function, callback, conditional, or JSX
    block.
12. `}` --- Closes the current function, callback, conditional, or JSX
    block.
13. `export default ShowHide;` --- Exports this component or Hook so
    another file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Dark Mode Toggle** is explained below. Read
the code first, then trace these lines in order.

1.  `import { useState } from "react";` --- Imports the React API or
    Hook needed by this example.
2.  `function Theme() {` --- Declares a function or React component.
3.  `const [dark, setDark] = useState(false);` --- Creates state: the
    first value is the current state and the second value updates it.
4.  `return (` --- Begins the JSX returned by the component.
5.  `<div>` --- Creates a JSX element that React will render into the
    UI.
6.  `<button onClick={() => setDark(!dark)}>` --- Connects a function to
    the click event of the JSX element.
7.  `Toggle Theme` --- Supports the surrounding React logic, data flow,
    or rendered UI.
8.  `</button>` --- Creates a JSX element that React will render into
    the UI.
9.  `<h2>{dark ? "Dark Mode" : "Light Mode"}</h2>` --- Uses a
    conditional expression to choose between two possible values/UI
    branches.
10. `</div>` --- Creates a JSX element that React will render into the
    UI.
11. `);` --- Closes the current function, callback, conditional, or JSX
    block.
12. `}` --- Closes the current function, callback, conditional, or JSX
    block.
13. `export default Theme;` --- Exports this component or Hook so
    another file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Input Field** is explained below. Read the
code first, then trace these lines in order.

1.  `import { useState } from "react";` --- Imports the React API or
    Hook needed by this example.
2.  `function InputExample() {` --- Declares a function or React
    component.
3.  `const [name, setName] = useState("");` --- Creates state: the first
    value is the current state and the second value updates it.
4.  `return (` --- Begins the JSX returned by the component.
5.  `<div>` --- Creates a JSX element that React will render into the
    UI.
6.  `<input` --- Creates a JSX element that React will render into the
    UI.
7.  `value={name}` --- Makes an input controlled by React state.
8.  `onChange={(e) => setName(e.target.value)}` --- Runs when an input
    changes, commonly updating React state.
9.  `placeholder="Enter your name"` --- Supports the surrounding React
    logic, data flow, or rendered UI.
10. `/>` --- Supports the surrounding React logic, data flow, or
    rendered UI.
11. `<h2>You entered: {name}</h2>` --- Creates a JSX element that React
    will render into the UI.
12. `</div>` --- Creates a JSX element that React will render into the
    UI.
13. `);` --- Closes the current function, callback, conditional, or JSX
    block.
14. `}` --- Closes the current function, callback, conditional, or JSX
    block.
15. `export default InputExample;` --- Exports this component or Hook so
    another file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Like Button** is explained below. Read the
code first, then trace these lines in order.

1.  `import { useState } from "react";` --- Imports the React API or
    Hook needed by this example.
2.  `function LikeButton() {` --- Declares a function or React
    component.
3.  `const [liked, setLiked] = useState(false);` --- Creates state: the
    first value is the current state and the second value updates it.
4.  `return (` --- Begins the JSX returned by the component.
5.  `<button onClick={() => setLiked(!liked)}>` --- Connects a function
    to the click event of the JSX element.
6.  `{liked ? "❤️ Liked" : "♡ Like"}` --- Uses a conditional expression
    to choose between two possible values/UI branches.
7.  `</button>` --- Creates a JSX element that React will render into
    the UI.
8.  `);` --- Closes the current function, callback, conditional, or JSX
    block.
9.  `}` --- Closes the current function, callback, conditional, or JSX
    block.
10. `export default LikeButton;` --- Exports this component or Hook so
    another file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Reset Counter** is explained below. Read the
code first, then trace these lines in order.

1.  `import { useState } from "react";` --- Imports the React API or
    Hook needed by this example.
2.  `function ResetCounter() {` --- Declares a function or React
    component.
3.  `const [count, setCount] = useState(0);` --- Creates state: the
    first value is the current state and the second value updates it.
4.  `return (` --- Begins the JSX returned by the component.
5.  `<div>` --- Creates a JSX element that React will render into the
    UI.
6.  `<h2>{count}</h2>` --- Creates a JSX element that React will render
    into the UI.
7.  `<button onClick={() => setCount(count + 1)}>` --- Connects a
    function to the click event of the JSX element.
8.  `Add` --- Supports the surrounding React logic, data flow, or
    rendered UI.
9.  `</button>` --- Creates a JSX element that React will render into
    the UI.
10. `<button onClick={() => setCount(0)}>` --- Connects a function to
    the click event of the JSX element.
11. `Reset` --- Supports the surrounding React logic, data flow, or
    rendered UI.
12. `</button>` --- Creates a JSX element that React will render into
    the UI.
13. `</div>` --- Creates a JSX element that React will render into the
    UI.
14. `);` --- Closes the current function, callback, conditional, or JSX
    block.
15. `}` --- Closes the current function, callback, conditional, or JSX
    block.
16. `export default ResetCounter;` --- Exports this component or Hook so
    another file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Object State** is explained below. Read the
code first, then trace these lines in order.

1.  `import { useState } from "react";` --- Imports the React API or
    Hook needed by this example.
2.  `function User() {` --- Declares a function or React component.
3.  `const [user, setUser] = useState({` --- Creates state: the first
    value is the current state and the second value updates it.
4.  `name: "Sahil",` --- Supports the surrounding React logic, data
    flow, or rendered UI.
5.  `age: 22` --- Supports the surrounding React logic, data flow, or
    rendered UI.
6.  `});` --- Supports the surrounding React logic, data flow, or
    rendered UI.
7.  `return (` --- Begins the JSX returned by the component.
8.  `<div>` --- Creates a JSX element that React will render into the
    UI.
9.  `<h2>{user.name}</h2>` --- Creates a JSX element that React will
    render into the UI.
10. `<p>Age: {user.age}</p>` --- Creates a JSX element that React will
    render into the UI.
11. `<button` --- Creates a JSX element that React will render into the
    UI.
12. `onClick={() =>` --- Connects a function to the click event of the
    JSX element.
13. `setUser({` --- Supports the surrounding React logic, data flow, or
    rendered UI.
14. `...user,` --- Supports the surrounding React logic, data flow, or
    rendered UI.
15. `age: user.age + 1` --- Supports the surrounding React logic, data
    flow, or rendered UI.
16. `})` --- Closes the current function, callback, conditional, or JSX
    block.
17. `}` --- Closes the current function, callback, conditional, or JSX
    block.
18. `>` --- Supports the surrounding React logic, data flow, or rendered
    UI.
19. `Increase Age` --- Supports the surrounding React logic, data flow,
    or rendered UI.
20. `</button>` --- Creates a JSX element that React will render into
    the UI.
21. `</div>` --- Creates a JSX element that React will render into the
    UI.
22. `);` --- Closes the current function, callback, conditional, or JSX
    block.
23. `}` --- Closes the current function, callback, conditional, or JSX
    block.
24. `export default User;` --- Exports this component or Hook so another
    file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Array State** is explained below. Read the
code first, then trace these lines in order.

1.  `import { useState } from "react";` --- Imports the React API or
    Hook needed by this example.
2.  `function Skills() {` --- Declares a function or React component.
3.  `const [skills, setSkills] = useState(["HTML", "CSS"]);` --- Creates
    state: the first value is the current state and the second value
    updates it.
4.  `const addSkill = () => {` --- Declares a local variable whose value
    is used by the component logic.
5.  `setSkills([...skills, "React"]);` --- Supports the surrounding
    React logic, data flow, or rendered UI.
6.  `};` --- Closes the current function, callback, conditional, or JSX
    block.
7.  `return (` --- Begins the JSX returned by the component.
8.  `<div>` --- Creates a JSX element that React will render into the
    UI.
9.  `{skills.map((skill) => (` --- Loops through an array and creates
    one output value/JSX element per item.
10. `<p key={skill}>{skill}</p>` --- Creates a JSX element that React
    will render into the UI.
11. `))}` --- Supports the surrounding React logic, data flow, or
    rendered UI.
12. `<button onClick={addSkill}>` --- Connects a function to the click
    event of the JSX element.
13. `Add React` --- Supports the surrounding React logic, data flow, or
    rendered UI.
14. `</button>` --- Creates a JSX element that React will render into
    the UI.
15. `</div>` --- Creates a JSX element that React will render into the
    UI.
16. `);` --- Closes the current function, callback, conditional, or JSX
    block.
17. `}` --- Closes the current function, callback, conditional, or JSX
    block.
18. `export default Skills;` --- Exports this component or Hook so
    another file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Functional State Update** is explained below.
Read the code first, then trace these lines in order.

1.  `import { useState } from "react";` --- Imports the React API or
    Hook needed by this example.
2.  `function Counter() {` --- Declares a function or React component.
3.  `const [count, setCount] = useState(0);` --- Creates state: the
    first value is the current state and the second value updates it.
4.  `const increase = () => {` --- Declares a local variable whose value
    is used by the component logic.
5.  `setCount((previous) => previous + 1);` --- Supports the surrounding
    React logic, data flow, or rendered UI.
6.  `};` --- Closes the current function, callback, conditional, or JSX
    block.
7.  `return (` --- Begins the JSX returned by the component.
8.  `<div>` --- Creates a JSX element that React will render into the
    UI.
9.  `<h2>{count}</h2>` --- Creates a JSX element that React will render
    into the UI.
10. `<button onClick={increase}>Add</button>` --- Connects a function to
    the click event of the JSX element.
11. `</div>` --- Creates a JSX element that React will render into the
    UI.
12. `);` --- Closes the current function, callback, conditional, or JSX
    block.
13. `}` --- Closes the current function, callback, conditional, or JSX
    block.
14. `export default Counter;` --- Exports this component or Hook so
    another file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Change Document Title** is explained below.
Read the code first, then trace these lines in order.

1.  `import { useEffect } from "react";` --- Imports the React API or
    Hook needed by this example.
2.  `function App() {` --- Declares a function or React component.
3.  `useEffect(() => {` --- Starts a side effect that React runs after
    the component commits, according to its dependencies.
4.  `document.title = "React App";` --- Supports the surrounding React
    logic, data flow, or rendered UI.
5.  `}, []);` --- Supports the surrounding React logic, data flow, or
    rendered UI.
6.  `return <h2>Hello React</h2>;` --- Returns a value from the current
    function or component.
7.  `}` --- Closes the current function, callback, conditional, or JSX
    block.
8.  `export default App;` --- Exports this component or Hook so another
    file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Run Only Once** is explained below. Read the
code first, then trace these lines in order.

1.  `import { useEffect } from "react";` --- Imports the React API or
    Hook needed by this example.
2.  `function App() {` --- Declares a function or React component.
3.  `useEffect(() => {` --- Starts a side effect that React runs after
    the component commits, according to its dependencies.
4.  `console.log("Component loaded");` --- Prints information to the
    browser console for learning or debugging.
5.  `}, []);` --- Supports the surrounding React logic, data flow, or
    rendered UI.
6.  `return <h2>Home Page</h2>;` --- Returns a value from the current
    function or component.
7.  `}` --- Closes the current function, callback, conditional, or JSX
    block.
8.  `export default App;` --- Exports this component or Hook so another
    file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Run When Name Changes** is explained below.
Read the code first, then trace these lines in order.

1.  `import { useEffect, useState } from "react";` --- Imports the React
    API or Hook needed by this example.
2.  `function App() {` --- Declares a function or React component.
3.  `const [name, setName] = useState("");` --- Creates state: the first
    value is the current state and the second value updates it.
4.  `useEffect(() => {` --- Starts a side effect that React runs after
    the component commits, according to its dependencies.
5.  `console.log("Name changed:", name);` --- Prints information to the
    browser console for learning or debugging.
6.  `}, [name]);` --- Supports the surrounding React logic, data flow,
    or rendered UI.
7.  `return (` --- Begins the JSX returned by the component.
8.  `<div>` --- Creates a JSX element that React will render into the
    UI.
9.  `<input` --- Creates a JSX element that React will render into the
    UI.
10. `value={name}` --- Makes an input controlled by React state.
11. `onChange={(e) => setName(e.target.value)}` --- Runs when an input
    changes, commonly updating React state.
12. `/>` --- Supports the surrounding React logic, data flow, or
    rendered UI.
13. `<p>{name}</p>` --- Creates a JSX element that React will render
    into the UI.
14. `</div>` --- Creates a JSX element that React will render into the
    UI.
15. `);` --- Closes the current function, callback, conditional, or JSX
    block.
16. `}` --- Closes the current function, callback, conditional, or JSX
    block.
17. `export default App;` --- Exports this component or Hook so another
    file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Timer** is explained below. Read the code
first, then trace these lines in order.

1.  `import { useEffect, useState } from "react";` --- Imports the React
    API or Hook needed by this example.
2.  `function Timer() {` --- Declares a function or React component.
3.  `const [seconds, setSeconds] = useState(0);` --- Creates state: the
    first value is the current state and the second value updates it.
4.  `useEffect(() => {` --- Starts a side effect that React runs after
    the component commits, according to its dependencies.
5.  `const timer = setInterval(() => {` --- Creates a repeating browser
    timer.
6.  `setSeconds((previous) => previous + 1);` --- Supports the
    surrounding React logic, data flow, or rendered UI.
7.  `}, 1000);` --- Supports the surrounding React logic, data flow, or
    rendered UI.
8.  `return () => clearInterval(timer);` --- Stops the interval during
    cleanup.
9.  `}, []);` --- Supports the surrounding React logic, data flow, or
    rendered UI.
10. `return <h2>{seconds} seconds</h2>;` --- Returns a value from the
    current function or component.
11. `}` --- Closes the current function, callback, conditional, or JSX
    block.
12. `export default Timer;` --- Exports this component or Hook so
    another file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Window Resize** is explained below. Read the
code first, then trace these lines in order.

1.  `import { useEffect, useState } from "react";` --- Imports the React
    API or Hook needed by this example.
2.  `function ScreenSize() {` --- Declares a function or React
    component.
3.  `const [width, setWidth] = useState(window.innerWidth);` --- Creates
    state: the first value is the current state and the second value
    updates it.
4.  `useEffect(() => {` --- Starts a side effect that React runs after
    the component commits, according to its dependencies.
5.  `const handleResize = () => {` --- Declares a local variable whose
    value is used by the component logic.
6.  `setWidth(window.innerWidth);` --- Supports the surrounding React
    logic, data flow, or rendered UI.
7.  `};` --- Closes the current function, callback, conditional, or JSX
    block.
8.  `window.addEventListener("resize", handleResize);` --- Registers a
    browser event listener so the component can react to an external
    event.
9.  `return () => {` --- Begins the JSX returned by the component.
10. `window.removeEventListener("resize", handleResize);` --- Removes
    the browser listener during cleanup so stale listeners do not remain
    active.
11. `};` --- Closes the current function, callback, conditional, or JSX
    block.
12. `}, []);` --- Supports the surrounding React logic, data flow, or
    rendered UI.
13. `return <h2>Width: {width}px</h2>;` --- Returns a value from the
    current function or component.
14. `}` --- Closes the current function, callback, conditional, or JSX
    block.
15. `export default ScreenSize;` --- Exports this component or Hook so
    another file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Fetch API Data** is explained below. Read the
code first, then trace these lines in order.

1.  `import { useEffect, useState } from "react";` --- Imports the React
    API or Hook needed by this example.
2.  `function Users() {` --- Declares a function or React component.
3.  `const [users, setUsers] = useState([]);` --- Creates state: the
    first value is the current state and the second value updates it.
4.  `useEffect(() => {` --- Starts a side effect that React runs after
    the component commits, according to its dependencies.
5.  `fetch("https://jsonplaceholder.typicode.com/users")` --- Starts an
    HTTP request to retrieve data.
6.  `.then((response) => response.json())` --- Supports the surrounding
    React logic, data flow, or rendered UI.
7.  `.then((data) => setUsers(data));` --- Supports the surrounding
    React logic, data flow, or rendered UI.
8.  `}, []);` --- Supports the surrounding React logic, data flow, or
    rendered UI.
9.  `return (` --- Begins the JSX returned by the component.
10. `<div>` --- Creates a JSX element that React will render into the
    UI.
11. `{users.map((user) => (` --- Loops through an array and creates one
    output value/JSX element per item.
12. `<p key={user.id}>{user.name}</p>` --- Creates a JSX element that
    React will render into the UI.
13. `))}` --- Supports the surrounding React logic, data flow, or
    rendered UI.
14. `</div>` --- Creates a JSX element that React will render into the
    UI.
15. `);` --- Closes the current function, callback, conditional, or JSX
    block.
16. `}` --- Closes the current function, callback, conditional, or JSX
    block.
17. `export default Users;` --- Exports this component or Hook so
    another file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Event Listener Cleanup** is explained below.
Read the code first, then trace these lines in order.

1.  `import { useEffect } from "react";` --- Imports the React API or
    Hook needed by this example.
2.  `function Keyboard() {` --- Declares a function or React component.
3.  `useEffect(() => {` --- Starts a side effect that React runs after
    the component commits, according to its dependencies.
4.  `const handleKey = (event) => {` --- Declares a local variable whose
    value is used by the component logic.
5.  `console.log("Pressed:", event.key);` --- Prints information to the
    browser console for learning or debugging.
6.  `};` --- Closes the current function, callback, conditional, or JSX
    block.
7.  `window.addEventListener("keydown", handleKey);` --- Registers a
    browser event listener so the component can react to an external
    event.
8.  `return () => {` --- Begins the JSX returned by the component.
9.  `window.removeEventListener("keydown", handleKey);` --- Removes the
    browser listener during cleanup so stale listeners do not remain
    active.
10. `};` --- Closes the current function, callback, conditional, or JSX
    block.
11. `}, []);` --- Supports the surrounding React logic, data flow, or
    rendered UI.
12. `return <h2>Press any key</h2>;` --- Returns a value from the
    current function or component.
13. `}` --- Closes the current function, callback, conditional, or JSX
    block.
14. `export default Keyboard;` --- Exports this component or Hook so
    another file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Local Storage** is explained below. Read the
code first, then trace these lines in order.

1.  `import { useEffect, useState } from "react";` --- Imports the React
    API or Hook needed by this example.
2.  `function App() {` --- Declares a function or React component.
3.  `const [name, setName] = useState("");` --- Creates state: the first
    value is the current state and the second value updates it.
4.  `useEffect(() => {` --- Starts a side effect that React runs after
    the component commits, according to its dependencies.
5.  `localStorage.setItem("name", name);` --- Reads or writes browser
    storage so data can survive a refresh.
6.  `}, [name]);` --- Supports the surrounding React logic, data flow,
    or rendered UI.
7.  `return (` --- Begins the JSX returned by the component.
8.  `<input` --- Creates a JSX element that React will render into the
    UI.
9.  `value={name}` --- Makes an input controlled by React state.
10. `onChange={(e) => setName(e.target.value)}` --- Runs when an input
    changes, commonly updating React state.
11. `placeholder="Enter name"` --- Supports the surrounding React logic,
    data flow, or rendered UI.
12. `/>` --- Supports the surrounding React logic, data flow, or
    rendered UI.
13. `);` --- Closes the current function, callback, conditional, or JSX
    block.
14. `}` --- Closes the current function, callback, conditional, or JSX
    block.
15. `export default App;` --- Exports this component or Hook so another
    file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Fetch Data When ID Changes** is explained
below. Read the code first, then trace these lines in order.

1.  `import { useEffect, useState } from "react";` --- Imports the React
    API or Hook needed by this example.
2.  `function User({ id }) {` --- Declares a function or React
    component.
3.  `const [user, setUser] = useState(null);` --- Creates state: the
    first value is the current state and the second value updates it.
4.  `useEffect(() => {` --- Starts a side effect that React runs after
    the component commits, according to its dependencies.
5.  `fetch(\`https://jsonplaceholder.typicode.com/users/\${id}\`)\` ---
    Starts an HTTP request to retrieve data.
6.  `.then((response) => response.json())` --- Supports the surrounding
    React logic, data flow, or rendered UI.
7.  `.then((data) => setUser(data));` --- Supports the surrounding React
    logic, data flow, or rendered UI.
8.  `}, [id]);` --- Supports the surrounding React logic, data flow, or
    rendered UI.
9.  `return (` --- Begins the JSX returned by the component.
10. `<div>` --- Creates a JSX element that React will render into the
    UI.
11. `<h2>{user?.name}</h2>` --- Uses a conditional expression to choose
    between two possible values/UI branches.
12. `</div>` --- Creates a JSX element that React will render into the
    UI.
13. `);` --- Closes the current function, callback, conditional, or JSX
    block.
14. `}` --- Closes the current function, callback, conditional, or JSX
    block.
15. `export default User;` --- Exports this component or Hook so another
    file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Cleanup Timer** is explained below. Read the
code first, then trace these lines in order.

1.  `import { useEffect } from "react";` --- Imports the React API or
    Hook needed by this example.
2.  `function App() {` --- Declares a function or React component.
3.  `useEffect(() => {` --- Starts a side effect that React runs after
    the component commits, according to its dependencies.
4.  `const timer = setTimeout(() => {` --- Creates a browser timer that
    runs once after the delay.
5.  `console.log("Hello after 2 seconds");` --- Prints information to
    the browser console for learning or debugging.
6.  `}, 2000);` --- Supports the surrounding React logic, data flow, or
    rendered UI.
7.  `return () => clearTimeout(timer);` --- Stops the timeout during
    cleanup.
8.  `}, []);` --- Supports the surrounding React logic, data flow, or
    rendered UI.
9.  `return <h2>Timer Example</h2>;` --- Returns a value from the
    current function or component.
10. `}` --- Closes the current function, callback, conditional, or JSX
    block.
11. `export default App;` --- Exports this component or Hook so another
    file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Basic Counter** is explained below. Read the
code first, then trace these lines in order.

1.  `import { useReducer } from "react";` --- Imports the React API or
    Hook needed by this example.
2.  `function reducer(state, action) {` --- Declares a function or React
    component.
3.  `if (action.type === "increment") {` --- Checks a condition and runs
    the block only when the condition is true.
4.  `return state + 1;` --- Returns a value from the current function or
    component.
5.  `}` --- Closes the current function, callback, conditional, or JSX
    block.
6.  `return state;` --- Returns a value from the current function or
    component.
7.  `}` --- Closes the current function, callback, conditional, or JSX
    block.
8.  `function Counter() {` --- Declares a function or React component.
9.  `const [count, dispatch] = useReducer(reducer, 0);` --- Connects the
    component to a reducer and provides the current state plus dispatch.
10. `return (` --- Begins the JSX returned by the component.
11. `<div>` --- Creates a JSX element that React will render into the
    UI.
12. `<h2>{count}</h2>` --- Creates a JSX element that React will render
    into the UI.
13. `<button onClick={() => dispatch({ type: "increment" })}>` --- Sends
    an action to the reducer, which decides the next state.
14. `Add` --- Supports the surrounding React logic, data flow, or
    rendered UI.
15. `</button>` --- Creates a JSX element that React will render into
    the UI.
16. `</div>` --- Creates a JSX element that React will render into the
    UI.
17. `);` --- Closes the current function, callback, conditional, or JSX
    block.
18. `}` --- Closes the current function, callback, conditional, or JSX
    block.
19. `export default Counter;` --- Exports this component or Hook so
    another file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Increment and Decrement** is explained below.
Read the code first, then trace these lines in order.

1.  `import { useReducer } from "react";` --- Imports the React API or
    Hook needed by this example.
2.  `function reducer(state, action) {` --- Declares a function or React
    component.
3.  `switch (action.type) {` --- Starts action-based branching so
    different actions can produce different state transitions.
4.  `case "increment":` --- Handles one specific action type in the
    reducer.
5.  `return state + 1;` --- Returns a value from the current function or
    component.
6.  `case "decrement":` --- Handles one specific action type in the
    reducer.
7.  `return state - 1;` --- Returns a value from the current function or
    component.
8.  `default:` --- Defines the fallback behavior when no other case
    matches.
9.  `return state;` --- Returns a value from the current function or
    component.
10. `}` --- Closes the current function, callback, conditional, or JSX
    block.
11. `}` --- Closes the current function, callback, conditional, or JSX
    block.
12. `function Counter() {` --- Declares a function or React component.
13. `const [count, dispatch] = useReducer(reducer, 0);` --- Connects the
    component to a reducer and provides the current state plus dispatch.
14. `return (` --- Begins the JSX returned by the component.
15. `<div>` --- Creates a JSX element that React will render into the
    UI.
16. `<h2>{count}</h2>` --- Creates a JSX element that React will render
    into the UI.
17. `<button onClick={() => dispatch({ type: "increment" })}>` --- Sends
    an action to the reducer, which decides the next state.
18. `+` --- Supports the surrounding React logic, data flow, or rendered
    UI.
19. `</button>` --- Creates a JSX element that React will render into
    the UI.
20. `<button onClick={() => dispatch({ type: "decrement" })}>` --- Sends
    an action to the reducer, which decides the next state.
21. `-` --- Supports the surrounding React logic, data flow, or rendered
    UI.
22. `</button>` --- Creates a JSX element that React will render into
    the UI.
23. `</div>` --- Creates a JSX element that React will render into the
    UI.
24. `);` --- Closes the current function, callback, conditional, or JSX
    block.
25. `}` --- Closes the current function, callback, conditional, or JSX
    block.
26. `export default Counter;` --- Exports this component or Hook so
    another file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Reset Counter** is explained below. Read the
code first, then trace these lines in order.

1.  `import { useReducer } from "react";` --- Imports the React API or
    Hook needed by this example.
2.  `function reducer(state, action) {` --- Declares a function or React
    component.
3.  `switch (action.type) {` --- Starts action-based branching so
    different actions can produce different state transitions.
4.  `case "add":` --- Handles one specific action type in the reducer.
5.  `return state + 1;` --- Returns a value from the current function or
    component.
6.  `case "reset":` --- Handles one specific action type in the reducer.
7.  `return 0;` --- Returns a value from the current function or
    component.
8.  `default:` --- Defines the fallback behavior when no other case
    matches.
9.  `return state;` --- Returns a value from the current function or
    component.
10. `}` --- Closes the current function, callback, conditional, or JSX
    block.
11. `}` --- Closes the current function, callback, conditional, or JSX
    block.
12. `function Counter() {` --- Declares a function or React component.
13. `const [count, dispatch] = useReducer(reducer, 0);` --- Connects the
    component to a reducer and provides the current state plus dispatch.
14. `return (` --- Begins the JSX returned by the component.
15. `<div>` --- Creates a JSX element that React will render into the
    UI.
16. `<h2>{count}</h2>` --- Creates a JSX element that React will render
    into the UI.
17. `<button onClick={() => dispatch({ type: "add" })}>` --- Sends an
    action to the reducer, which decides the next state.
18. `Add` --- Supports the surrounding React logic, data flow, or
    rendered UI.
19. `</button>` --- Creates a JSX element that React will render into
    the UI.
20. `<button onClick={() => dispatch({ type: "reset" })}>` --- Sends an
    action to the reducer, which decides the next state.
21. `Reset` --- Supports the surrounding React logic, data flow, or
    rendered UI.
22. `</button>` --- Creates a JSX element that React will render into
    the UI.
23. `</div>` --- Creates a JSX element that React will render into the
    UI.
24. `);` --- Closes the current function, callback, conditional, or JSX
    block.
25. `}` --- Closes the current function, callback, conditional, or JSX
    block.
26. `export default Counter;` --- Exports this component or Hook so
    another file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Counter With Step** is explained below. Read
the code first, then trace these lines in order.

1.  `import { useReducer } from "react";` --- Imports the React API or
    Hook needed by this example.
2.  `function reducer(state, action) {` --- Declares a function or React
    component.
3.  `switch (action.type) {` --- Starts action-based branching so
    different actions can produce different state transitions.
4.  `case "add":` --- Handles one specific action type in the reducer.
5.  `return state + action.amount;` --- Returns a value from the current
    function or component.
6.  `default:` --- Defines the fallback behavior when no other case
    matches.
7.  `return state;` --- Returns a value from the current function or
    component.
8.  `}` --- Closes the current function, callback, conditional, or JSX
    block.
9.  `}` --- Closes the current function, callback, conditional, or JSX
    block.
10. `function Counter() {` --- Declares a function or React component.
11. `const [count, dispatch] = useReducer(reducer, 0);` --- Connects the
    component to a reducer and provides the current state plus dispatch.
12. `return (` --- Begins the JSX returned by the component.
13. `<div>` --- Creates a JSX element that React will render into the
    UI.
14. `<h2>{count}</h2>` --- Creates a JSX element that React will render
    into the UI.
15. `<button` --- Creates a JSX element that React will render into the
    UI.
16. `onClick={() =>` --- Connects a function to the click event of the
    JSX element.
17. `dispatch({` --- Sends an action to the reducer, which decides the
    next state.
18. `type: "add",` --- Supports the surrounding React logic, data flow,
    or rendered UI.
19. `amount: 5` --- Supports the surrounding React logic, data flow, or
    rendered UI.
20. `})` --- Closes the current function, callback, conditional, or JSX
    block.
21. `}` --- Closes the current function, callback, conditional, or JSX
    block.
22. `>` --- Supports the surrounding React logic, data flow, or rendered
    UI.
23. `Add 5` --- Supports the surrounding React logic, data flow, or
    rendered UI.
24. `</button>` --- Creates a JSX element that React will render into
    the UI.
25. `</div>` --- Creates a JSX element that React will render into the
    UI.
26. `);` --- Closes the current function, callback, conditional, or JSX
    block.
27. `}` --- Closes the current function, callback, conditional, or JSX
    block.
28. `export default Counter;` --- Exports this component or Hook so
    another file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Boolean State** is explained below. Read the
code first, then trace these lines in order.

1.  `import { useReducer } from "react";` --- Imports the React API or
    Hook needed by this example.
2.  `function reducer(state, action) {` --- Declares a function or React
    component.
3.  `if (action.type === "toggle") {` --- Checks a condition and runs
    the block only when the condition is true.
4.  `return !state;` --- Returns a value from the current function or
    component.
5.  `}` --- Closes the current function, callback, conditional, or JSX
    block.
6.  `return state;` --- Returns a value from the current function or
    component.
7.  `}` --- Closes the current function, callback, conditional, or JSX
    block.
8.  `function Toggle() {` --- Declares a function or React component.
9.  `const [on, dispatch] = useReducer(reducer, false);` --- Connects
    the component to a reducer and provides the current state plus
    dispatch.
10. `return (` --- Begins the JSX returned by the component.
11. `<button onClick={() => dispatch({ type: "toggle" })}>` --- Sends an
    action to the reducer, which decides the next state.
12. `{on ? "ON" : "OFF"}` --- Uses a conditional expression to choose
    between two possible values/UI branches.
13. `</button>` --- Creates a JSX element that React will render into
    the UI.
14. `);` --- Closes the current function, callback, conditional, or JSX
    block.
15. `}` --- Closes the current function, callback, conditional, or JSX
    block.
16. `export default Toggle;` --- Exports this component or Hook so
    another file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Object State** is explained below. Read the
code first, then trace these lines in order.

1.  `import { useReducer } from "react";` --- Imports the React API or
    Hook needed by this example.
2.  `const initialState = {` --- Declares a local variable whose value
    is used by the component logic.
3.  `name: "Sahil",` --- Supports the surrounding React logic, data
    flow, or rendered UI.
4.  `age: 22` --- Supports the surrounding React logic, data flow, or
    rendered UI.
5.  `};` --- Closes the current function, callback, conditional, or JSX
    block.
6.  `function reducer(state, action) {` --- Declares a function or React
    component.
7.  `switch (action.type) {` --- Starts action-based branching so
    different actions can produce different state transitions.
8.  `case "changeName":` --- Handles one specific action type in the
    reducer.
9.  `return {` --- Returns a value from the current function or
    component.
10. `...state,` --- Supports the surrounding React logic, data flow, or
    rendered UI.
11. `name: action.value` --- Supports the surrounding React logic, data
    flow, or rendered UI.
12. `};` --- Closes the current function, callback, conditional, or JSX
    block.
13. `case "increaseAge":` --- Handles one specific action type in the
    reducer.
14. `return {` --- Returns a value from the current function or
    component.
15. `...state,` --- Supports the surrounding React logic, data flow, or
    rendered UI.
16. `age: state.age + 1` --- Supports the surrounding React logic, data
    flow, or rendered UI.
17. `};` --- Closes the current function, callback, conditional, or JSX
    block.
18. `default:` --- Defines the fallback behavior when no other case
    matches.
19. `return state;` --- Returns a value from the current function or
    component.
20. `}` --- Closes the current function, callback, conditional, or JSX
    block.
21. `}` --- Closes the current function, callback, conditional, or JSX
    block.
22. `function User() {` --- Declares a function or React component.
23. `const [user, dispatch] = useReducer(reducer, initialState);` ---
    Connects the component to a reducer and provides the current state
    plus dispatch.
24. `return (` --- Begins the JSX returned by the component.
25. `<div>` --- Creates a JSX element that React will render into the
    UI.
26. `<h2>{user.name}</h2>` --- Creates a JSX element that React will
    render into the UI.
27. `<p>{user.age}</p>` --- Creates a JSX element that React will render
    into the UI.
28. `<button` --- Creates a JSX element that React will render into the
    UI.
29. `onClick={() =>` --- Connects a function to the click event of the
    JSX element.
30. `dispatch({` --- Sends an action to the reducer, which decides the
    next state.
31. `type: "changeName",` --- Supports the surrounding React logic, data
    flow, or rendered UI.
32. `value: "Rahul"` --- Supports the surrounding React logic, data
    flow, or rendered UI.
33. `})` --- Closes the current function, callback, conditional, or JSX
    block.
34. `}` --- Closes the current function, callback, conditional, or JSX
    block.
35. `>` --- Supports the surrounding React logic, data flow, or rendered
    UI.
36. `Change Name` --- Supports the surrounding React logic, data flow,
    or rendered UI.
37. `</button>` --- Creates a JSX element that React will render into
    the UI.
38. `<button onClick={() => dispatch({ type: "increaseAge" })}>` ---
    Sends an action to the reducer, which decides the next state.
39. `Increase Age` --- Supports the surrounding React logic, data flow,
    or rendered UI.
40. `</button>` --- Creates a JSX element that React will render into
    the UI.
41. `</div>` --- Creates a JSX element that React will render into the
    UI.
42. `);` --- Closes the current function, callback, conditional, or JSX
    block.
43. `}` --- Closes the current function, callback, conditional, or JSX
    block.
44. `export default User;` --- Exports this component or Hook so another
    file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Todo List** is explained below. Read the code
first, then trace these lines in order.

1.  `import { useReducer } from "react";` --- Imports the React API or
    Hook needed by this example.
2.  `function reducer(state, action) {` --- Declares a function or React
    component.
3.  `switch (action.type) {` --- Starts action-based branching so
    different actions can produce different state transitions.
4.  `case "add":` --- Handles one specific action type in the reducer.
5.  `return [` --- Returns a value from the current function or
    component.
6.  `...state,` --- Supports the surrounding React logic, data flow, or
    rendered UI.
7.  `{` --- Supports the surrounding React logic, data flow, or rendered
    UI.
8.  `id: Date.now(),` --- Supports the surrounding React logic, data
    flow, or rendered UI.
9.  `text: action.text` --- Supports the surrounding React logic, data
    flow, or rendered UI.
10. `}` --- Closes the current function, callback, conditional, or JSX
    block.
11. `];` --- Supports the surrounding React logic, data flow, or
    rendered UI.
12. `case "remove":` --- Handles one specific action type in the
    reducer.
13. `return state.filter((todo) => todo.id !== action.id);` --- Creates
    a new array containing only items that pass the condition.
14. `default:` --- Defines the fallback behavior when no other case
    matches.
15. `return state;` --- Returns a value from the current function or
    component.
16. `}` --- Closes the current function, callback, conditional, or JSX
    block.
17. `}` --- Closes the current function, callback, conditional, or JSX
    block.
18. `function Todo() {` --- Declares a function or React component.
19. `const [todos, dispatch] = useReducer(reducer, []);` --- Connects
    the component to a reducer and provides the current state plus
    dispatch.
20. `return (` --- Begins the JSX returned by the component.
21. `<div>` --- Creates a JSX element that React will render into the
    UI.
22. `<button` --- Creates a JSX element that React will render into the
    UI.
23. `onClick={() =>` --- Connects a function to the click event of the
    JSX element.
24. `dispatch({` --- Sends an action to the reducer, which decides the
    next state.
25. `type: "add",` --- Supports the surrounding React logic, data flow,
    or rendered UI.
26. `text: "Learn React"` --- Supports the surrounding React logic, data
    flow, or rendered UI.
27. `})` --- Closes the current function, callback, conditional, or JSX
    block.
28. `}` --- Closes the current function, callback, conditional, or JSX
    block.
29. `>` --- Supports the surrounding React logic, data flow, or rendered
    UI.
30. `Add Todo` --- Supports the surrounding React logic, data flow, or
    rendered UI.
31. `</button>` --- Creates a JSX element that React will render into
    the UI.
32. `{todos.map((todo) => (` --- Loops through an array and creates one
    output value/JSX element per item.
33. `<p key={todo.id}>` --- Creates a JSX element that React will render
    into the UI.
34. `{todo.text}` --- Supports the surrounding React logic, data flow,
    or rendered UI.
35. `<button` --- Creates a JSX element that React will render into the
    UI.
36. `onClick={() =>` --- Connects a function to the click event of the
    JSX element.
37. `dispatch({` --- Sends an action to the reducer, which decides the
    next state.
38. `type: "remove",` --- Supports the surrounding React logic, data
    flow, or rendered UI.
39. `id: todo.id` --- Supports the surrounding React logic, data flow,
    or rendered UI.
40. `})` --- Closes the current function, callback, conditional, or JSX
    block.
41. `}` --- Closes the current function, callback, conditional, or JSX
    block.
42. `>` --- Supports the surrounding React logic, data flow, or rendered
    UI.
43. `Delete` --- Supports the surrounding React logic, data flow, or
    rendered UI.
44. `</button>` --- Creates a JSX element that React will render into
    the UI.
45. `</p>` --- Creates a JSX element that React will render into the UI.
46. `))}` --- Supports the surrounding React logic, data flow, or
    rendered UI.
47. `</div>` --- Creates a JSX element that React will render into the
    UI.
48. `);` --- Closes the current function, callback, conditional, or JSX
    block.
49. `}` --- Closes the current function, callback, conditional, or JSX
    block.
50. `export default Todo;` --- Exports this component or Hook so another
    file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

### 🔎 Deep Line-by-Line Explanation

Every meaningful line in **Login State** is explained below. Read the
code first, then trace these lines in order.

1.  `import { useReducer } from "react";` --- Imports the React API or
    Hook needed by this example.
2.  `function reducer(state, action) {` --- Declares a function or React
    component.
3.  `switch (action.type) {` --- Starts action-based branching so
    different actions can produce different state transitions.
4.  `case "login":` --- Handles one specific action type in the reducer.
5.  `return { loggedIn: true };` --- Returns a value from the current
    function or component.
6.  `case "logout":` --- Handles one specific action type in the
    reducer.
7.  `return { loggedIn: false };` --- Returns a value from the current
    function or component.
8.  `default:` --- Defines the fallback behavior when no other case
    matches.
9.  `return state;` --- Returns a value from the current function or
    component.
10. `}` --- Closes the current function, callback, conditional, or JSX
    block.
11. `}` --- Closes the current function, callback, conditional, or JSX
    block.
12. `function Login() {` --- Declares a function or React component.
13. `const [state, dispatch] = useReducer(reducer, {` --- Connects the
    component to a reducer and provides the current state plus dispatch.
14. `loggedIn: false` --- Supports the surrounding React logic, data
    flow, or rendered UI.
15. `});` --- Supports the surrounding React logic, data flow, or
    rendered UI.
16. `return (` --- Begins the JSX returned by the component.
17. `<div>` --- Creates a JSX element that React will render into the
    UI.
18. `<h2>` --- Creates a JSX element that React will render into the UI.
19. `{state.loggedIn ? "Welcome User" : "Please Login"}` --- Uses a
    conditional expression to choose between two possible values/UI
    branches.
20. `</h2>` --- Creates a JSX element that React will render into the
    UI.
21. `<button onClick={() => dispatch({ type: "login" })}>` --- Sends an
    action to the reducer, which decides the next state.
22. `Login` --- Supports the surrounding React logic, data flow, or
    rendered UI.
23. `</button>` --- Creates a JSX element that React will render into
    the UI.
24. `<button onClick={() => dispatch({ type: "logout" })}>` --- Sends an
    action to the reducer, which decides the next state.
25. `Logout` --- Supports the surrounding React logic, data flow, or
    rendered UI.
26. `</button>` --- Creates a JSX element that React will render into
    the UI.
27. `</div>` --- Creates a JSX element that React will render into the
    UI.
28. `);` --- Closes the current function, callback, conditional, or JSX
    block.
29. `}` --- Closes the current function, callback, conditional, or JSX
    block.
30. `export default Login;` --- Exports this component or Hook so
    another file can import it.

### 🔄 Execution Flow

1.  React executes the component function.
2.  Hooks read/create the required state, context, ref, memoized value,
    or effect.
3.  JSX describes the UI.
4.  A user action or external event may trigger an update.
5.  React renders again when relevant state/context changes; dependency
    arrays control when effects and memoized work run again.

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

---

# 12. Common Mistakes Students Make

## Mistake 1 — Mutating state directly

Wrong:
```jsx
user.name = "Rahul";
```

Better:

``` jsx
setUser({ ...user, name: "Rahul" });
```

React state should be treated as immutable data.

## Mistake 2 --- Wrong effect dependencies

If an effect uses a reactive value such as `name`, think carefully about
whether `name` belongs in the dependency list.

## Mistake 3 --- Forgetting cleanup

Timers, subscriptions, and browser event listeners can continue after a
component disappears. Return a cleanup function when the external system
requires it.

## Mistake 4 --- Using `useMemo` for every calculation

`useMemo` is a performance optimization. A tiny calculation is often
clearer as normal JavaScript.

## Mistake 5 --- Using `useCallback` everywhere

Use it when stable function identity is useful, especially with memoized
child components or Hook dependencies.

## Mistake 6 --- Confusing `useMemo` and `useCallback`

``` text
useMemo     → remembers a calculated VALUE
useCallback → remembers a FUNCTION reference
```

## Mistake 7 --- Using `useLayoutEffect` for normal side effects

Use `useLayoutEffect` when layout timing matters. For normal API calls,
timers, subscriptions, and similar effects, `useEffect` is generally the
better choice.

## Mistake 8 --- Treating Context as a complete state-management solution

Context provides values to a component subtree. It can be combined with
state, reducers, or other architecture depending on application size and
needs.

------------------------------------------------------------------------

# 13. Hook Mental Model

``` text
useState
  ↓
Changing local data

useEffect
  ↓
Synchronize with external systems

useReducer
  ↓
Structured state transitions

useContext
  ↓
Share values across a component tree

useMemo / useCallback
  ↓
Performance and referential stability

useLayoutEffect
  ↓
DOM/layout work before paint

Custom Hooks
  ↓
Reuse Hook-based logic
```

------------------------------------------------------------------------

# 14. One-Sentence Memory Tricks

``` text
useState       → I need to remember changing data.
useEffect      → I need to synchronize with something outside rendering.
useReducer     → My state transitions need structured actions.
useContext     → Many components need the same value.
useLayoutEffect→ I need DOM/layout work before paint.
useMemo        → I want to reuse a calculated value.
useCallback    → I want to reuse a function reference.
Custom Hook    → I want to reuse React logic.
```

------------------------------------------------------------------------

# 15. Final Student Challenge --- React Student Management System

Build a complete Student Management System in stages.

### Level 1 --- Basic

-   Add student
-   Delete student
-   Display student list
-   Count students

Use `useState`.

### Level 2 --- Side Effects

-   Save students to localStorage
-   Change document title
-   Load data from an API

Use `useEffect`.

### Level 3 --- Complex State

Move add/delete/edit logic into a reducer.

Use `useReducer`.

### Level 4 --- Shared Data

Create theme and user contexts.

Use `useContext`.

### Level 5 --- Reusable Logic

Create `useLocalStorage`, `useDebounce`, `useFetch`, and `useCounter`.

Use Custom Hooks.

### Level 6 --- Performance

Optimize filtering, sorting, and child callbacks.

Use `useMemo` and `useCallback`.

### Level 7 --- DOM/Layout

Create a dashboard card that measures its own width and adjusts its UI
before paint.

Use `useLayoutEffect`.

------------------------------------------------------------------------

# Final Goal

When you see React code, ask:

``` text
What data is changing?
        ↓
Where is it stored?
        ↓
What causes a re-render?
        ↓
Is there an external side effect?
        ↓
Is state logic complex enough for a reducer?
        ↓
Does another component need the same value?
        ↓
Is an expensive calculation being repeated?
        ↓
Does function identity matter?
        ↓
Is DOM measurement required?
        ↓
Can the logic become a reusable Custom Hook?
```

That is the real objective of learning Hooks: **understand the data
flow, timing, and reason for each Hook instead of memorizing syntax.**
