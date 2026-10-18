# ReactJS Mini Projects — Complete Practical Guide

## Beginner to Intermediate React Projects

This practical module contains **6 complete ReactJS mini projects**:

1. ToDo App
2. Quiz App
3. Coin Flipping App
4. Color Box App
5. Dice Rolling App
6. Guess the Number App

The projects are designed for students who already know the basics of:

- React components
- JSX
- `useState`
- Event handling
- Conditional rendering
- Arrays and `map()`
- Forms and input handling
- Basic CSS
- Vite

---

# 1. Common React Project Setup

Before creating the individual projects, understand the standard React setup.

## 1.1 Requirements

Install:

- Node.js
- npm
- VS Code or another code editor
- Modern web browser

Check Node.js:

```bash
node -v
```

Check npm:

```bash
npm -v
```

If both commands return a version number, your environment is ready.

---

# 2. Create a React Project Using Vite

Vite is a fast and modern development tool for React applications.

Create a new project:

```bash
npm create vite@latest react-mini-projects
```

Select:

```text
Framework: React
Variant: JavaScript
```

Move into the project:

```bash
cd react-mini-projects
```

Install dependencies:

```bash
npm install
```

Start the development server:

```bash
npm run dev
```

Open the URL shown by Vite, usually:

```text
http://localhost:5173
```

---

# 3. Standard Project Structure

A newly created Vite React application normally contains:

```text
react-mini-projects/
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

For each mini project, it is recommended to create a separate Vite project.

Example:

```text
react-projects/
│
├── todo-app/
├── quiz-app/
├── coin-flipping-app/
├── color-box-app/
├── dice-rolling-app/
└── guess-number-app/
```

This keeps every project independent and easier to upload to GitHub.

---

# PROJECT 1 — TO-DO APP USING REACTJS

## 1.1 Project Objective

Create a simple To-Do application where the user can:

- Add a task
- View tasks
- Mark a task as completed
- Delete a task
- Clear all tasks
- See the number of remaining tasks

## 1.2 What You Will Learn

This project teaches:

- `useState`
- Arrays in state
- `map()`
- `filter()`
- Input handling
- Form submission
- Conditional rendering
- Dynamic CSS classes
- Unique task IDs

---

## 1.3 Create the Project

```bash
npm create vite@latest todo-app
```

Select:

```text
React
JavaScript
```

Then:

```bash
cd todo-app
npm install
npm run dev
```

---

## 1.4 Project Structure

```text
todo-app/
│
├── src/
│   ├── App.jsx
│   ├── App.css
│   ├── index.css
│   └── main.jsx
│
├── package.json
└── vite.config.js
```

---

## 1.5 Step 1 — Create the Main Component

Open:

```text
src/App.jsx
```

Replace its contents with:

```jsx
import { useState } from "react";
import "./App.css";

function App() {
  const [task, setTask] = useState("");
  const [tasks, setTasks] = useState([]);

  const addTask = (event) => {
    event.preventDefault();

    if (task.trim() === "") {
      return;
    }

    const newTask = {
      id: crypto.randomUUID(),
      text: task,
      completed: false,
    };

    setTasks((previousTasks) => [...previousTasks, newTask]);
    setTask("");
  };

  const toggleTask = (id) => {
    setTasks((previousTasks) =>
      previousTasks.map((item) =>
        item.id === id
          ? { ...item, completed: !item.completed }
          : item
      )
    );
  };

  const deleteTask = (id) => {
    setTasks((previousTasks) =>
      previousTasks.filter((item) => item.id !== id)
    );
  };

  const clearTasks = () => {
    setTasks([]);
  };

  const remainingTasks = tasks.filter(
    (item) => !item.completed
  ).length;

  return (
    <div className="app">
      <div className="todo-container">
        <h1>My To-Do App</h1>

        <form onSubmit={addTask} className="task-form">
          <input
            type="text"
            placeholder="Enter a task..."
            value={task}
            onChange={(event) => setTask(event.target.value)}
          />

          <button type="submit">Add Task</button>
        </form>

        <p>Remaining Tasks: {remainingTasks}</p>

        <div className="task-list">
          {tasks.length === 0 ? (
            <p>No tasks added yet.</p>
          ) : (
            tasks.map((item) => (
              <div
                key={item.id}
                className={`task ${
                  item.completed ? "completed" : ""
                }`}
              >
                <span onClick={() => toggleTask(item.id)}>
                  {item.text}
                </span>

                <button onClick={() => deleteTask(item.id)}>
                  Delete
                </button>
              </div>
            ))
          )}
        </div>

        {tasks.length > 0 && (
          <button onClick={clearTasks}>Clear All</button>
        )}
      </div>
    </div>
  );
}

export default App;
```

---

## 1.6 Step 2 — Add CSS

Open:

```text
src/App.css
```

Add:

```css
.app {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #f1f5f9;
}

.todo-container {
  width: 500px;
  background: white;
  padding: 30px;
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.todo-container h1 {
  text-align: center;
}

.task-form {
  display: flex;
  gap: 10px;
}

.task-form input {
  flex: 1;
  padding: 12px;
}

button {
  padding: 10px 15px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
}

.task-list {
  margin-top: 20px;
}

.task {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px;
  margin-bottom: 10px;
  background: #f8fafc;
  border-radius: 8px;
}

.task span {
  cursor: pointer;
}

.task.completed span {
  text-decoration: line-through;
  opacity: 0.5;
}
```

---

## 1.7 Step 3 — Test the Application

Try:

1. Enter `Learn React`.
2. Click **Add Task**.
3. Add `Practice useState`.
4. Add `Build a project`.
5. Click a task to mark it completed.
6. Delete a task.
7. Click **Clear All**.

---

## 1.8 How the To-Do App Works

The state contains:

```js
const [task, setTask] = useState("");
```

This stores the current input.

The task list is stored in:

```js
const [tasks, setTasks] = useState([]);
```

A task looks like:

```js
{
  id: "unique-id",
  text: "Learn React",
  completed: false
}
```

When a task is added:

```js
setTasks((previousTasks) => [
  ...previousTasks,
  newTask
]);
```

The spread operator creates a new array.

To delete:

```js
filter()
```

is used.

To update one task:

```js
map()
```

is used.

---

## 1.9 To-Do App Enhancements

After completing the basic version, add:

- Edit task
- Task priority
- Search tasks
- Filter: All / Active / Completed
- Due date
- LocalStorage
- Dark mode
- Task categories
- Drag and drop
- Login and cloud database

---

# PROJECT 2 — QUIZ APP USING REACTJS

## 2.1 Project Objective

Create a quiz application where:

- Questions are displayed one at a time
- User selects an answer
- User moves to the next question
- Score is calculated
- Final result is displayed
- Quiz can be restarted

## 2.2 Concepts Used

- `useState`
- Arrays of objects
- `map()`
- Conditional rendering
- Event handling
- Array indexing
- Button state
- Score calculation

---

## 2.3 Create the Project

```bash
npm create vite@latest quiz-app
```

Select:

```text
React
JavaScript
```

Then:

```bash
cd quiz-app
npm install
npm run dev
```

---

## 2.4 App.jsx

```jsx
import { useState } from "react";
import "./App.css";

const questions = [
  {
    question: "Which language is used with React?",
    options: ["Python", "JavaScript", "Java", "C++"],
    answer: "JavaScript",
  },
  {
    question: "Which hook is used for state?",
    options: ["useData", "useState", "useValue", "useHook"],
    answer: "useState",
  },
  {
    question: "Which company originally created React?",
    options: ["Google", "Microsoft", "Facebook", "Amazon"],
    answer: "Facebook",
  },
  {
    question: "What is JSX?",
    options: [
      "A database",
      "A JavaScript syntax extension",
      "A server",
      "A CSS framework",
    ],
    answer: "A JavaScript syntax extension",
  },
];

function App() {
  const [currentQuestion, setCurrentQuestion] = useState(0);
  const [score, setScore] = useState(0);
  const [selectedAnswer, setSelectedAnswer] = useState("");
  const [finished, setFinished] = useState(false);

  const question = questions[currentQuestion];

  const selectAnswer = (option) => {
    setSelectedAnswer(option);
  };

  const nextQuestion = () => {
    if (!selectedAnswer) {
      alert("Please select an answer.");
      return;
    }

    if (selectedAnswer === question.answer) {
      setScore((previousScore) => previousScore + 1);
    }

    if (currentQuestion === questions.length - 1) {
      setFinished(true);
    } else {
      setCurrentQuestion(
        (previousQuestion) => previousQuestion + 1
      );
      setSelectedAnswer("");
    }
  };

  const restartQuiz = () => {
    setCurrentQuestion(0);
    setScore(0);
    setSelectedAnswer("");
    setFinished(false);
  };

  if (finished) {
    return (
      <div className="quiz">
        <h1>Quiz Completed!</h1>

        <h2>
          Score: {score} / {questions.length}
        </h2>

        <button onClick={restartQuiz}>
          Restart Quiz
        </button>
      </div>
    );
  }

  return (
    <div className="quiz">
      <h1>React Quiz</h1>

      <p>
        Question {currentQuestion + 1} of{" "}
        {questions.length}
      </p>

      <h2>{question.question}</h2>

      <div className="options">
        {question.options.map((option) => (
          <button
            key={option}
            className={
              selectedAnswer === option
                ? "selected"
                : ""
            }
            onClick={() => selectAnswer(option)}
          >
            {option}
          </button>
        ))}
      </div>

      <button onClick={nextQuestion}>
        {currentQuestion === questions.length - 1
          ? "Finish Quiz"
          : "Next Question"}
      </button>
    </div>
  );
}

export default App;
```

---

## 2.5 CSS

```css
.quiz {
  max-width: 600px;
  margin: 80px auto;
  padding: 30px;
  text-align: center;
  background: white;
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.options {
  display: grid;
  gap: 12px;
  margin: 25px 0;
}

.options button {
  padding: 15px;
  cursor: pointer;
}

.options button.selected {
  outline: 3px solid #333;
}
```

---

## 2.6 Quiz Flow

```text
Start
  |
  v
Question 1
  |
  v
Select Answer
  |
  v
Next
  |
  v
Question 2
  |
  v
...
  |
  v
Final Question
  |
  v
Calculate Result
  |
  v
Show Score
```

---

## 2.7 Important Point

The current answer is stored separately:

```js
const [selectedAnswer, setSelectedAnswer] =
  useState("");
```

The score is stored separately:

```js
const [score, setScore] = useState(0);
```

The question index is:

```js
const [currentQuestion, setCurrentQuestion] =
  useState(0);
```

---

## 2.8 Quiz Enhancements

Add:

- Timer
- Difficulty levels
- Categories
- Random questions
- Random options
- Correct/wrong answer explanation
- Progress bar
- High-score system
- LocalStorage
- API-based questions
- Dark mode
- Review answers
- Negative marking

---

# PROJECT 3 — COIN FLIPPING APP USING REACTJS

## 3.1 Project Objective

Create an application that simulates a coin flip.

The user clicks:

```text
Flip Coin
```

The application randomly displays:

```text
Heads
```

or:

```text
Tails
```

The application also keeps track of:

- Total flips
- Heads count
- Tails count

---

## 3.2 Create the Project

```bash
npm create vite@latest coin-flipping-app
```

Then:

```bash
cd coin-flipping-app
npm install
npm run dev
```

---

## 3.3 App.jsx

```jsx
import { useState } from "react";
import "./App.css";

function App() {
  const [result, setResult] = useState("?");
  const [heads, setHeads] = useState(0);
  const [tails, setTails] = useState(0);

  const flipCoin = () => {
    const randomResult =
      Math.random() < 0.5 ? "Heads" : "Tails";

    setResult(randomResult);

    if (randomResult === "Heads") {
      setHeads((previousHeads) => previousHeads + 1);
    } else {
      setTails((previousTails) => previousTails + 1);
    }
  };

  const resetGame = () => {
    setResult("?");
    setHeads(0);
    setTails(0);
  };

  return (
    <div className="coin-app">
      <h1>Coin Flipping App</h1>

      <div className="coin">
        {result}
      </div>

      <button onClick={flipCoin}>
        Flip Coin
      </button>

      <button onClick={resetGame}>
        Reset
      </button>

      <div className="stats">
        <p>Heads: {heads}</p>
        <p>Tails: {tails}</p>
        <p>Total Flips: {heads + tails}</p>
      </div>
    </div>
  );
}

export default App;
```

---

## 3.4 CSS

```css
.coin-app {
  text-align: center;
  margin-top: 80px;
}

.coin {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  margin: 30px auto;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #facc15;
  font-size: 24px;
  font-weight: bold;
}
```

---

## 3.5 Understand Randomness

This:

```js
Math.random()
```

generates a number between `0` and `1`.

Example:

```text
0.12
0.73
0.45
0.91
```

We use:

```js
Math.random() < 0.5
```

If true:

```text
Heads
```

Otherwise:

```text
Tails
```

---

## 3.6 Coin Flip Enhancements

Add:

- Coin animation
- Different coin images
- Heads/Tails sound
- Flip history
- Probability percentage
- 10-flip simulation
- 100-flip simulation
- Custom number of flips
- Statistics chart

---

# PROJECT 4 — COLOR BOX APP USING REACTJS

## 4.1 Project Objective

Create an application containing a box whose color changes when the user selects a color.

Example:

```text
[ Red ]
[ Blue ]
[ Green ]
[ Yellow ]

+----------------+
|                |
|    COLOR BOX   |
|                |
+----------------+
```

---

## 4.2 Concepts Used

- `useState`
- Event handling
- Inline styles
- Buttons
- Dynamic styling

---

## 4.3 Create the Project

```bash
npm create vite@latest color-box-app
```

Then:

```bash
cd color-box-app
npm install
npm run dev
```

---

## 4.4 App.jsx

```jsx
import { useState } from "react";
import "./App.css";

function App() {
  const [color, setColor] = useState("lightgray");

  const colors = [
    "red",
    "blue",
    "green",
    "yellow",
    "purple",
    "orange",
  ];

  return (
    <div className="color-app">
      <h1>Color Box App</h1>

      <div
        className="color-box"
        style={{ backgroundColor: color }}
      >
        {color}
      </div>

      <div className="buttons">
        {colors.map((item) => (
          <button
            key={item}
            onClick={() => setColor(item)}
          >
            {item}
          </button>
        ))}
      </div>

      <button
        onClick={() => setColor("lightgray")}
      >
        Reset
      </button>
    </div>
  );
}

export default App;
```

---

## 4.5 CSS

```css
.color-app {
  text-align: center;
  padding: 50px;
}

.color-box {
  width: 300px;
  height: 200px;
  margin: 30px auto;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 15px;
  font-size: 24px;
  font-weight: bold;
  transition: 0.3s;
}

.buttons {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 10px;
  margin-bottom: 20px;
}
```

---

## 4.6 How It Works

Initial state:

```js
const [color, setColor] = useState("lightgray");
```

When the user clicks:

```js
setColor("red");
```

React updates the component.

The style:

```jsx
style={{ backgroundColor: color }}
```

automatically receives the new value.

---

## 4.7 Color Box Enhancements

Add:

- Color picker
- Random color
- Hex code
- RGB code
- Copy color code
- Color history
- Gradient generator
- Custom color input
- Dark/light theme

---

# PROJECT 5 — DICE ROLLING APP USING REACTJS

## 5.1 Project Objective

Create a dice rolling application.

When the user clicks:

```text
Roll Dice
```

a random number from:

```text
1 to 6
```

is generated.

---

## 5.2 Create the Project

```bash
npm create vite@latest dice-rolling-app
```

Then:

```bash
cd dice-rolling-app
npm install
npm run dev
```

---

## 5.3 App.jsx

```jsx
import { useState } from "react";
import "./App.css";

function App() {
  const [dice, setDice] = useState(1);
  const [rollCount, setRollCount] = useState(0);

  const rollDice = () => {
    const randomNumber =
      Math.floor(Math.random() * 6) + 1;

    setDice(randomNumber);
    setRollCount(
      (previousCount) => previousCount + 1
    );
  };

  const resetGame = () => {
    setDice(1);
    setRollCount(0);
  };

  return (
    <div className="dice-app">
      <h1>Dice Rolling App</h1>

      <div className="dice">
        {dice}
      </div>

      <button onClick={rollDice}>
        Roll Dice
      </button>

      <button onClick={resetGame}>
        Reset
      </button>

      <p>Rolls: {rollCount}</p>
    </div>
  );
}

export default App;
```

---

## 5.4 CSS

```css
.dice-app {
  text-align: center;
  padding-top: 80px;
}

.dice {
  width: 150px;
  height: 150px;
  margin: 30px auto;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 3px solid #222;
  border-radius: 20px;
  font-size: 60px;
  font-weight: bold;
}
```

---

## 5.5 Understand the Random Number Formula

The formula is:

```js
Math.floor(Math.random() * 6) + 1
```

### Step 1

```js
Math.random()
```

generates:

```text
0 <= number < 1
```

### Step 2

```js
Math.random() * 6
```

produces a value from:

```text
0 to less than 6
```

### Step 3

```js
Math.floor()
```

produces:

```text
0, 1, 2, 3, 4, 5
```

### Step 4

Add:

```js
+ 1
```

Result:

```text
1, 2, 3, 4, 5, 6
```

---

## 5.6 Dice Enhancements

Add:

- Two dice
- Three dice
- Dice images
- Dice animation
- Total score
- Roll history
- Multiplayer mode
- Highest roll
- Statistics
- Dice game such as Pig or Yahtzee

---

# PROJECT 6 — GUESS THE NUMBER USING REACTJS

## 6.1 Project Objective

Build a number guessing game.

The application secretly generates a number between:

```text
1 and 100
```

The user enters a guess.

The application tells the user:

```text
Too High
```

or:

```text
Too Low
```

or:

```text
Correct!
```

---

## 6.2 Concepts Used

- `useState`
- `Math.random()`
- `Math.floor()`
- Controlled inputs
- Form submission
- Conditional rendering
- Comparison operators
- Game state

---

## 6.3 Create the Project

```bash
npm create vite@latest guess-number-app
```

Then:

```bash
cd guess-number-app
npm install
npm run dev
```

---

## 6.4 App.jsx

```jsx
import { useState } from "react";
import "./App.css";

function generateNumber() {
  return Math.floor(Math.random() * 100) + 1;
}

function App() {
  const [secretNumber, setSecretNumber] =
    useState(generateNumber);

  const [guess, setGuess] = useState("");
  const [message, setMessage] =
    useState("Guess a number between 1 and 100.");

  const [attempts, setAttempts] = useState(0);
  const [gameOver, setGameOver] = useState(false);

  const checkGuess = (event) => {
    event.preventDefault();

    if (gameOver) {
      return;
    }

    const userGuess = Number(guess);

    if (
      !Number.isInteger(userGuess) ||
      userGuess < 1 ||
      userGuess > 100
    ) {
      setMessage(
        "Please enter a whole number between 1 and 100."
      );
      return;
    }

    setAttempts(
      (previousAttempts) => previousAttempts + 1
    );

    if (userGuess < secretNumber) {
      setMessage("Too Low! Try again.");
    } else if (userGuess > secretNumber) {
      setMessage("Too High! Try again.");
    } else {
      setMessage(
        `Correct! You guessed it in ${
          attempts + 1
        } attempts.`
      );

      setGameOver(true);
    }

    setGuess("");
  };

  const restartGame = () => {
    setSecretNumber(generateNumber());
    setGuess("");
    setMessage(
      "Guess a number between 1 and 100."
    );
    setAttempts(0);
    setGameOver(false);
  };

  return (
    <div className="guess-app">
      <h1>Guess the Number</h1>

      <p>{message}</p>

      <form onSubmit={checkGuess}>
        <input
          type="number"
          min="1"
          max="100"
          value={guess}
          onChange={(event) =>
            setGuess(event.target.value)
          }
          disabled={gameOver}
          placeholder="Enter your guess"
        />

        <button
          type="submit"
          disabled={gameOver}
        >
          Guess
        </button>
      </form>

      <p>Attempts: {attempts}</p>

      {gameOver && (
        <button onClick={restartGame}>
          Play Again
        </button>
      )}
    </div>
  );
}

export default App;
```

---

## 6.5 CSS

```css
.guess-app {
  max-width: 500px;
  margin: 80px auto;
  padding: 35px;
  text-align: center;
  background: white;
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.guess-app form {
  display: flex;
  gap: 10px;
  justify-content: center;
  margin: 25px 0;
}

.guess-app input {
  padding: 12px;
  width: 220px;
}
```

---

# 7. Understand the Guessing Game Logic

The secret number is generated using:

```js
Math.floor(Math.random() * 100) + 1
```

This creates a number between:

```text
1 and 100
```

The user's input is initially a string because HTML form inputs return text.

Therefore:

```js
const userGuess = Number(guess);
```

converts it to a number.

Then:

```js
if (userGuess < secretNumber)
```

means the user's number is smaller.

```js
else if (userGuess > secretNumber)
```

means the user's number is larger.

Otherwise:

```js
else
```

the user has guessed correctly.

---

# 8. Recommended CSS Reset

For every project, you can replace the default `src/index.css` with:

```css
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, sans-serif;
  background: #f1f5f9;
  color: #222;
}

button {
  border: none;
  cursor: pointer;
  font-family: inherit;
}

button:disabled {
  cursor: not-allowed;
  opacity: 0.6;
}
```

---

# 9. Common React Concepts Used in All Six Projects

## 9.1 useState

Used to store data that can change.

Example:

```js
const [count, setCount] = useState(0);
```

---

## 9.2 Event Handling

React handles browser events using props such as:

```jsx
onClick
onChange
onSubmit
```

Example:

```jsx
<button onClick={rollDice}>
  Roll Dice
</button>
```

---

## 9.3 Conditional Rendering

Example:

```jsx
{gameOver && (
  <button>Play Again</button>
)}
```

The button appears only when:

```js
gameOver === true
```

---

## 9.4 Rendering Arrays

Example:

```jsx
colors.map((color) => (
  <button key={color}>
    {color}
  </button>
))
```

React needs a stable `key` when rendering lists.

---

## 9.5 Controlled Input

Example:

```jsx
<input
  value={guess}
  onChange={(event) =>
    setGuess(event.target.value)
  }
/>
```

React controls the input value through state.

---

# 10. Comparison of the Six Projects

| Project | Main React Concept | Main JavaScript Concept |
|---|---|---|
| To-Do App | State + Lists | `map`, `filter` |
| Quiz App | State + Conditional Rendering | Arrays/Objects |
| Coin Flip | State + Events | `Math.random()` |
| Color Box | State + Dynamic Styling | Arrays/Mapping |
| Dice App | State + Events | Random Numbers |
| Guess Number | State + Forms | Conditions/Random Numbers |

---

# 11. Recommended Teaching Order

Teach the projects in this order:

```text
1. Color Box
       ↓
2. Coin Flipping
       ↓
3. Dice Rolling
       ↓
4. Guess the Number
       ↓
5. To-Do App
       ↓
6. Quiz App
```

### Why this order?

The first projects are smaller and introduce:

```text
useState
   ↓
Events
   ↓
Random Numbers
   ↓
Conditional Rendering
   ↓
Forms
   ↓
Arrays
   ↓
Objects
   ↓
Complete Application State
```

---

# 12. Practical Student Tasks

## Task 1 — To-Do App

Add:

- Edit task
- Search task
- Completed filter
- Active filter

---

## Task 2 — Quiz App

Add:

- 10 questions
- Timer
- Progress bar
- Final percentage
- Pass/fail result

---

## Task 3 — Coin Flip

Add:

- Animation
- Flip history
- Heads percentage
- Tails percentage

---

## Task 4 — Color Box

Add:

- HTML color input
- Hex code
- RGB code
- Copy button
- Random color button

---

## Task 5 — Dice

Add:

- Two dice
- Sum of dice
- Roll history
- Highest roll

---

## Task 6 — Guess Number

Add:

- Difficulty levels
- Easy: 1–50
- Medium: 1–100
- Hard: 1–500
- Maximum attempts
- Score system

---

# 13. Industry-Level Improvements

After students complete the basic projects, introduce:

## Componentization

Instead of keeping everything inside `App.jsx`:

```text
src/
├── components/
│   ├── Button.jsx
│   ├── Input.jsx
│   └── Card.jsx
│
├── App.jsx
└── main.jsx
```

---

## Example Component

```jsx
function Button({ children, onClick }) {
  return (
    <button onClick={onClick}>
      {children}
    </button>
  );
}

export default Button;
```

Then:

```jsx
<Button onClick={rollDice}>
  Roll Dice
</Button>
```

---

# 14. LocalStorage Upgrade

The To-Do App is a good project for learning browser storage.

Example:

```js
localStorage.setItem(
  "tasks",
  JSON.stringify(tasks)
);
```

Reading:

```js
const savedTasks =
  JSON.parse(localStorage.getItem("tasks")) || [];
```

For a complete implementation, use `useEffect` to synchronize the React state with LocalStorage.

---

# 15. GitHub Submission Structure

Create one GitHub repository:

```text
react-mini-projects/
│
├── todo-app/
│   ├── src/
│   ├── public/
│   ├── package.json
│   └── README.md
│
├── quiz-app/
│   ├── src/
│   ├── public/
│   ├── package.json
│   └── README.md
│
├── coin-flipping-app/
│   ├── src/
│   ├── public/
│   ├── package.json
│   └── README.md
│
├── color-box-app/
│   ├── src/
│   ├── public/
│   ├── package.json
│   └── README.md
│
├── dice-rolling-app/
│   ├── src/
│   ├── public/
│   ├── package.json
│   └── README.md
│
└── guess-number-app/
    ├── src/
    ├── public/
    ├── package.json
    └── README.md
```

---

# 16. Git Commands

Initialize the repository:

```bash
git init
```

Add files:

```bash
git add .
```

Commit:

```bash
git commit -m "Add React mini projects"
```

Connect your GitHub repository:

```bash
git remote add origin YOUR_GITHUB_REPOSITORY_URL
```

Push:

```bash
git branch -M main
git push -u origin main
```

---

# 17. Common Errors

## Error 1 — npm is not recognized

Check:

```bash
node -v
npm -v
```

If unavailable, install Node.js and restart the terminal.

---

## Error 2 — Wrong Vite command

Correct:

```bash
npm create vite@latest project-name
```

Do not use:

```bash
npm create vite@letest
```

---

## Error 3 — Module not found

Run:

```bash
npm install
```

---

## Error 4 — Port already in use

Vite normally chooses another available port.

You can also stop the previous development server using:

```text
Ctrl + C
```

---

## Error 5 — React page is blank

Check:

- Browser console
- Terminal errors
- `App.jsx`
- `main.jsx`
- Import paths
- JSX syntax
- Missing closing tags

---

## Error 6 — List warning about keys

Incorrect:

```jsx
items.map((item) => (
  <div>{item}</div>
))
```

Correct:

```jsx
items.map((item) => (
  <div key={item.id}>{item}</div>
))
```

Use stable IDs whenever available.

---

# 18. Final Mini Project Challenge

After completing all six projects, build:

# React Game Hub

Create one React application containing:

```text
React Game Hub
│
├── Home
│
├── To-Do
├── Quiz
├── Coin Flip
├── Color Box
├── Dice
└── Guess Number
```

Use:

- React Router
- Components
- `useState`
- `useEffect`
- Forms
- Lists
- Conditional rendering
- Reusable CSS
- LocalStorage

---

# 19. Suggested Final Folder Structure

```text
src/
│
├── components/
│   ├── Navbar.jsx
│   ├── Button.jsx
│   └── GameCard.jsx
│
├── pages/
│   ├── Home.jsx
│   ├── Todo.jsx
│   ├── Quiz.jsx
│   ├── CoinFlip.jsx
│   ├── ColorBox.jsx
│   ├── Dice.jsx
│   └── GuessNumber.jsx
│
├── App.jsx
├── App.css
├── index.css
└── main.jsx
```

---

# 20. Learning Outcomes

After completing these projects, students should be able to:

- Create React applications using Vite
- Create functional components
- Use `useState`
- Handle user events
- Work with forms
- Render arrays using `map()`
- Update arrays using `map()` and `filter()`
- Perform conditional rendering
- Generate random values
- Create controlled inputs
- Apply dynamic styles
- Build small interactive applications
- Organize React projects
- Push projects to GitHub

---

# 21. Interview Questions

## Beginner

### 1. What is `useState`?

`useState` is a React Hook used to store and update state in a functional component.

### 2. Why does React re-render after state changes?

When state changes, React schedules a new render so the UI can reflect the new state.

### 3. What is JSX?

JSX is a JavaScript syntax extension that allows UI markup to be written inside JavaScript.

### 4. Why do lists need keys?

Keys help React identify list items and preserve their identity efficiently between renders.

### 5. What is a controlled input?

An input whose value is controlled by React state.

---

## Intermediate

### 6. Why use functional state updates?

When the new state depends on the previous state, the functional form is safer:

```js
setCount((previousCount) => previousCount + 1);
```

### 7. Why should state not be mutated directly?

React state should be treated as immutable. Create a new array/object when updating it.

### 8. Why use `filter()` in the To-Do app?

It creates a new array without the deleted item.

### 9. Why use `map()`?

`map()` creates a new array by transforming each item.

### 10. Why convert the guessing input using `Number()`?

HTML input values are received as strings, while the guessing logic requires numeric comparison.

---

# 22. Final Revision

Remember this mental model:

```text
USER ACTION
    |
    v
EVENT HANDLER
    |
    v
STATE UPDATE
    |
    v
REACT RE-RENDERS
    |
    v
UPDATED UI
```

Example:

```text
Click "Roll Dice"
        |
        v
rollDice()
        |
        v
Generate random number
        |
        v
setDice(number)
        |
        v
React re-renders
        |
        v
New dice value appears
```

---

# 23. Project Completion Checklist

## To-Do App

- [ ] Create task
- [ ] Display tasks
- [ ] Complete task
- [ ] Delete task
- [ ] Clear tasks
- [ ] Remaining count

## Quiz App

- [ ] Display question
- [ ] Display options
- [ ] Select answer
- [ ] Move to next question
- [ ] Calculate score
- [ ] Restart quiz

## Coin Flip

- [ ] Flip coin
- [ ] Show Heads/Tails
- [ ] Count Heads
- [ ] Count Tails
- [ ] Reset

## Color Box

- [ ] Display box
- [ ] Select color
- [ ] Change color
- [ ] Reset color

## Dice

- [ ] Roll dice
- [ ] Generate 1–6
- [ ] Count rolls
- [ ] Reset

## Guess Number

- [ ] Generate secret number
- [ ] Accept user input
- [ ] Compare values
- [ ] Show Too High
- [ ] Show Too Low
- [ ] Show Correct
- [ ] Count attempts
- [ ] Restart

---

# 24. Final Challenge

Do not stop after copying the code.

For each project:

1. Create the project yourself.
2. Type the code instead of blindly copying it.
3. Run the application.
4. Change the UI.
5. Add one new feature.
6. Break something intentionally.
7. Read the error.
8. Fix the error.
9. Push the project to GitHub.
10. Explain the project without looking at the code.

That process will turn these mini projects from simple practice exercises into real React development experience.

---

# Conclusion

These six projects provide a progression from simple React state management to complete interactive applications.

The overall learning path is:

```text
React Setup
     ↓
Components
     ↓
JSX
     ↓
useState
     ↓
Events
     ↓
Conditional Rendering
     ↓
Forms
     ↓
Arrays + map()
     ↓
Objects
     ↓
Random Number Logic
     ↓
Mini Applications
     ↓
Componentization
     ↓
LocalStorage
     ↓
React Router
     ↓
React Game Hub
```

**Recommended next step:** combine all six applications into one **React Mini Projects / Game Hub** application using React Router and reusable components.
