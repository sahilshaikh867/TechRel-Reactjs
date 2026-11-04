# React JS Weather Forecasting App – Complete Beginner-to-Advanced Learning Project

Let's build this like a real-world developer training project, not just copy-paste a ready-made application.

Our goal is to create a beautiful Weather Forecasting Web App using React JS and a free third-party Weather API.

We'll start from zero, understand every concept, write the code step by step, test each feature, and finally deploy the application.

One important thing: I don't want you to directly copy a 500-line React project. You'll build it module by module so you understand what you're writing.

[Buzzy | Governed AI app delivery without technical debt](https://images.openai.com/static-rsc-4/jBo3pa9YIMGZUpB_4sP3MGxsuzJqnCAqU-QR7mLmgq_weQLzTe5ooYTFICYWD56V85c2aOfn15HJTkQlKePRqyBXe97CukOnY5b77GvQpchE9_YydXQESMD0CKrkuo8KmjhnVNrpIbF1ksZh5Q99hi_A4TmCCzFxqE7CV8_0cAY?purpose=inline)

[30-Day Frontend Hackathon | Build a Weather App](https://images.openai.com/static-rsc-4/rzmwWGfX8w9wQL4BrS6-sj0jVGfMar4VKtseDfMIocZOw7dT63BGggQ7ZAcG8P4KpgbmdRBO7sjM-TVsmrmNSMztGqFZfjJgP79XRuUEmABuFC8CIjiPGhiBMrLW-ZSVL6IKAjLYaw8iE5FBff6gw74H2gnnwzC-UGcObvs53d0?purpose=inline)

[Weather App | Frontend, React project | devChallenges](https://images.openai.com/static-rsc-4/In5-QMWwHi0iqBtpO1Gy429QlAaIl65c9UDI_EGn1zBmx0LpK6sJkiOwift1pBR9KjHiO2FmoCPt0MLHfqYMbP4JTe-Zpw5S5LtSav2Onsknj4bitcEeTKw4s2YmCdA7iCppK6F6FEuspNz0AAn81hxHykwwTZkln3qp1iAET8I?purpose=inline)

12

# Project: SkyCast – Weather Forecasting App

Beginner friendly

React JS

Free API

Real-world project

## 1. What are we going to build?

Our application will allow users to search for any city and view its current weather and forecast.

### Final application features

| Feature            | What you will learn        |
| ------------------ | -------------------------- |
| Search city        | React events and state     |
| Current weather    | API integration            |
| Temperature        | Fetch and JSON             |
| Weather conditions | Conditional rendering      |
| Weather icons      | Dynamic images             |
| 5-day forecast     | Arrays and `.map()`        |
| Hourly forecast    | Working with API data      |
| Loading animation  | React state                |
| Error messages     | Error handling             |
| Responsive UI      | CSS and media queries      |
| Weather details    | Component design           |
| API documentation  | Swagger / OpenAPI concepts |

### Technology stack

[File:React.svg - Wikimedia Commons](https://images.openai.com/static-rsc-4/7xLwZ4scX4fnuMMhGGC1cqLT77iXYre5xJdgpd7WX1KQ_p3g1RPDF7yr_WadpTqTOOQqdyWXwfoJZwqVjziB4ZjkWfqXFUA5ZzmEP0gz1yPlo8186Lx7bp_RlOKNJMYunWYIIcau9pEjVKeCiiL7F2AY3pRccI_LGvBv9WXSfHU?purpose=inline)

React JS

Frontend development and components

[Vite Logo PNG,  Vector (AI, EPS, CDR, PDF, SVG) - iconLogoVector](https://images.openai.com/static-rsc-4/3z0Km4avLxM07hDPhEKDfS7e7PZ2lL2d3cwaKeEzgNJv9dyl98qGYk571u4SaDifiikdYK2hz1shWLZ9XF_Yxb2nSviCVF-CT-lxbC7LskalbJ4GtZ76GhzgB_MZk2WTQc3IigAMSX0g3wNU9KhgeUkOGefHiGbg1uJSTHBED1E?purpose=inline)

Vite

React development environment

[Open-Meteo 🌤🌍 (@open_meteo) on X](https://images.openai.com/static-rsc-4/D26_bvoVeej80NOkyVq1CmihEnUmRnOJr4O_i5uNFcHr3Y10EitLf_BcOTGRuZ0XSk-wLXrger_bxuRijX980Bl0xzzqscmzBerHaK_UAZzinVGUcFOLX57Oojv9fVKJhZpGy6-m6qJSpfiqGkv28tiFyTIWBAoosbvGNpJVI7Q?purpose=inline)

Open-Meteo API

Free weather data without an API key for eligible non-commercial use

[JavaScript color icon in PNG, SVG](https://images.openai.com/static-rsc-4/tr6qZTUAn1whOfn0lXCVxhJFmyIYZXNtsFIA9qUaP24t1AZpVWRnxIhyvCLzzinoDuzy5ewSmCe_xtQgWpGRI6qCXGVf3_Qec9yjTvLG3eGny9looSH04-Iqbs7Q73TzXtYEuyNiilBOXZI6rmd7yutxo8_o1Vzgddp9dLfTXk8?purpose=inline)

JavaScript Fetch API

Communicating with third-party APIs

[Swagger Training Course | Master API Design & Documentation](https://images.openai.com/static-rsc-4/CKjKXVG-SXuDuRPtcuSX06H7lQijkpfL9RJOwSI3zRCxXi34H-mfqr3i2e__pBFtDtcKj9FoJUMyBPE5WBE9qWfcgdO_nvWuxYifptYTFVDakpUaRaVQJmMrj2s3nGrfR4tbAOXedAWlZuxn3DUZg_kRL3SxP-xrmefW2vCKrDg?purpose=inline)

Swagger / OpenAPI

Understanding, documenting and testing API endpoints

## 2. Understand the complete application architecture

Before writing code, understand how the application will work.

[Medium](https://images.openai.com/static-rsc-4/thXbLxS58hQNGIrKpNLfmsA25vhce-ofMdhAltqNf0-zl4nCjTEumYz4TrMFBNWDLXL_DKnbOodWAE6UODKrlrwXpT6cN0y650d_B5IFdhozzQTtmeOqhtcEMZn8MGN9F6J0uc-GCwjjXGykwo8JERmgpP5A3G-TbfULxkoy994?purpose=inline)

[medium.com](https://medium.com/%40efeemmanuel2030/what-is-an-api-exploring-rest-apis-and-django-rest-framework-6b73a334b03f?utm_source=chatgpt.com)

The flow is:

1. User opens the React application.
2. User enters a city name, such as Pune.
3. React sends a request to the Geocoding API.
4. API returns the city's latitude and longitude.
5. React uses those coordinates to request weather data.
6. The weather API returns JSON data.
7. React reads the JSON response.
8. React displays temperature, humidity, wind speed and forecast.

Important concept: Most weather APIs do not directly understand every city name in a forecast request. That's why we'll use two API endpoints: one for finding coordinates and another for getting weather data.

## 3. API selection – Which free API will we use?

We'll use Open-Meteo.

Official website: [Open-Meteo API](https://open-meteo.com/?utm_source=chatgpt.com)

Why this API?

- Free access for eligible non-commercial usage.
- No API key required for the basic service.
- Current weather information.
- Hourly forecast.
- Daily forecast.
- Temperature, humidity, wind speed and precipitation.
- Geocoding API for searching cities.

You can read the documentation here:

- [Weather Forecast API Documentation](https://open-meteo.com/en/docs?utm_source=chatgpt.com)
- [Geocoding API Documentation](https://open-meteo.com/en/docs/geocoding-api?utm_source=chatgpt.com)

We'll use these two endpoints:

| API                                              | Purpose                      |
| ------------------------------------------------ | ---------------------------- |
| `https://geocoding-api.open-meteo.com/v1/search` | Find city coordinates        |
| `https://api.open-meteo.com/v1/forecast`         | Retrieve weather information |

For example, searching Pune returns information such as:

```
{
  "name": "Pune",
  "latitude": 18.5204,
  "longitude": 73.8567,
  "country": "India"
}
```

The coordinates are then passed to the forecast API.

## 4. First understand the API request and response

Before React integration, we will test the API independently.

This is an important professional developer habit: never integrate an API into your frontend before understanding its request and response.

### Step 4.1 – Test the Geocoding API

Open your browser and paste:

[Test Pune Geocoding API](https://geocoding-api.open-meteo.com/v1/search?name=Pune\&count=5\&language=en\&format=json\&utm_source=chatgpt.com)

You should receive JSON containing city information, including latitude and longitude.

Understand these parameters:

| Parameter  | Meaning                   |
| ---------- | ------------------------- |
| `name`     | City name                 |
| `count`    | Maximum number of results |
| `language` | Response language         |
| `format`   | Response format           |

### Step 4.2 – Test the Weather API

Now open:

[Test Pune Weather API](https://api.open-meteo.com/v1/forecast?latitude=18.5204\&longitude=73.8567\&current=temperature_2m,relative_humidity_2m,apparent_temperature,is_day,precipitation,weather_code,wind_speed_10m\&hourly=temperature_2m,precipitation_probability\&daily=weather_code,temperature_2m_max,temperature_2m_min,sunrise,sunset\&timezone=auto\&forecast_days=5\&utm_source=chatgpt.com)

You will receive a response containing three important sections:

```
{
  "latitude": 18.52,
  "longitude": 73.85,
  "timezone": "Asia/Kolkata",
  "current": {
    "temperature_2m": 29.5,
    "relative_humidity_2m": 45,
    "apparent_temperature": 30.2,
    "wind_speed_10m": 12.4
  },
  "hourly": {
    "temperature_2m": [],
    "precipitation_probability": []
  },
  "daily": {
    "temperature_2m_max": [],
    "temperature_2m_min": []
  }
}
```

These values are illustrative. Actual API responses depend on the time and weather.

Understand the three sections:

- `current`: current weather information.
- `hourly`: hourly weather forecast.
- `daily`: daily forecast information.

Your first practical task: Open both URLs, inspect the JSON, and identify where temperature, humidity, wind speed and daily maximum temperature are stored.

# 5. Development environment setup – Start from zero

Module 1 – Environment Setup

### Step 5.1 – Install Node.js

React development with Vite requires Node.js and npm.

1. Visit [Node.js official website](https://nodejs.org/?utm_source=chatgpt.com).
2. Download the current LTS version.
3. Install it.
4. Restart your terminal.
5. Verify the installation.

Open VS Code terminal or PowerShell.

```
node -v
npm -v
```

Expected: Both commands should return version numbers.

### Step 5.2 – Install VS Code

Download: [Visual Studio Code](https://code.visualstudio.com/?utm_source=chatgpt.com)

Recommended extensions:

| Extension           | Purpose               |
| ------------------- | --------------------- |
| ES7+ React Snippets | React code snippets   |
| Prettier            | Code formatting       |
| ESLint              | Code quality          |
| Thunder Client      | API testing           |
| Error Lens          | Display errors inline |

### Step 5.3 – Create your first React application

Open your terminal.

First, navigate to the folder where you want to create your project.

```
cd Desktop
```

Create the React application:

```
npm create vite@latest skycast-weather
```

Vite will ask you some questions.

Choose:

```
Project name: skycast-weather
Framework: React
Variant: JavaScript
```

Now enter the project directory:

```
cd skycast-weather
```

Install dependencies:

```
npm install
```

Start the development server:

```
npm run dev
```

You should see something similar to:

```
Local: http://localhost:5173/
```

Open that URL in your browser.



Milestone 1

&#x20;Your first React application is running!



Reference: [Vite official documentation](https://vite.dev/guide/?utm_source=chatgpt.com) and [React learning guide](https://react.dev/learn?utm_source=chatgpt.com).&#x20;

[image](https://www.google.com/s2/favicons?domain=https://react.dev\&sz=32)

React+1



# 6. Understand the React project folder structure

Before coding, open your project in VS Code.

Your folder structure should look similar to this:

```
skycast-weather/
│
├── node_modules/
│
├── public/
│   └── weather-icons/
│
├── src/
│   ├── assets/
│   │
│   ├── components/
│   │   ├── Navbar.jsx
│   │   ├── SearchBar.jsx
│   │   ├── CurrentWeather.jsx
│   │   ├── WeatherDetails.jsx
│   │   ├── HourlyForecast.jsx
│   │   └── DailyForecast.jsx
│   │
│   ├── services/
│   │   └── weatherService.js
│   │
│   ├── App.jsx
│   ├── App.css
│   ├── index.css
│   └── main.jsx
│
├── index.html
├── package.json
└── vite.config.js
```

Let's understand every important folder.

| Folder/file  | Responsibility                |
| ------------ | ----------------------------- |
| `components` | Individual UI components      |
| `services`   | API communication logic       |
| `assets`     | Images and local assets       |
| `App.jsx`    | Main application component    |
| `App.css`    | Application styling           |
| `index.css`  | Global styling                |
| `main.jsx`   | React application entry point |
| `public`     | Static files                  |

Why create a `services` folder?

Imagine that tomorrow you replace Open-Meteo with another weather API.

If your API logic is inside every component, changing the API becomes difficult.

If your API logic is inside `weatherService.js`, you can modify it in one place.

This is a simple introduction to separation of concerns.

# 7. Learn the React concepts before building the app

Module 2 – React Fundamentals

You need to understand these concepts before connecting the API.

We'll learn each one through small exercises.

### Concept 1 – Components

A component is a reusable part of your user interface.

For example:

- Navbar
- Search bar
- Weather card
- Forecast card

Create a file:

`src/components/Navbar.jsx`

```
function Navbar() {
  return (
    <nav>
      <h2>SkyCast Weather</h2>
      <p>Weather Forecasting Application</p>
    </nav>
  );
}

export default Navbar;
```

Now open `App.jsx`:

```
import Navbar from "./components/Navbar";

function App() {
  return (
    <div>
      <Navbar />
      <h1>Welcome to SkyCast</h1>
    </div>
  );
}

export default App;
```

What did you learn?

1. How to create a component.
2. How to export a component.
3. How to import a component.
4. How to reuse components.

### Concept 2 – JSX

JSX allows you to write HTML-like syntax inside JavaScript.

Example:

```
const city = "Pune";
const temperature = 29;

function App() {
  return (
    <div>
      <h1>Weather in {city}</h1>
      <h2>{temperature}°C</h2>
    </div>
  );
}

export default App;
```

Notice `{city}` and `{temperature}`.

Curly braces allow you to display JavaScript values inside JSX.

### Concept 3 – Props

Props allow you to pass data from one component to another.

Create:

`src/components/WeatherCard.jsx`

```
function WeatherCard({ city, temperature }) {
  return (
    <div>
      <h2>{city}</h2>
      <h1>{temperature}°C</h1>
    </div>
  );
}

export default WeatherCard;
```

Now use it inside `App.jsx`:

```
import WeatherCard from "./components/WeatherCard";

function App() {
  return (
    <div>
      <WeatherCard
        city="Pune"
        temperature={29}
      />

      <WeatherCard
        city="Mumbai"
        temperature={31}
      />
    </div>
  );
}

export default App;
```

Practice: Display weather cards for Pune, Mumbai and Delhi using one reusable component.

### Concept 4 – useState

This is one of the most important React concepts for our application.

`useState` allows React components to remember and update information.

Example:

```
import { useState } from "react";

function App() {
  const [city, setCity] = useState("Pune");

  return (
    <div>
      <h1>{city}</h1>

      <button onClick={() => setCity("Mumbai")}>
        Change City
      </button>
    </div>
  );
}

export default App;
```

Understand:

- `city`: current state value.
- `setCity`: function to update the state.
- `"Pune"`: initial state.

When you click the button, the displayed city changes.

### Concept 5 – Events and input handling

We need a search bar where users can enter city names.

```
import { useState } from "react";

function SearchBar() {
  const [city, setCity] = useState("");

  function handleChange(event) {
    setCity(event.target.value);
  }

  function handleSearch() {
    alert("Searching for: " + city);
  }

  return (
    <div>
      <input
        type="text"
        placeholder="Enter city name"
        value={city}
        onChange={handleChange}
      />

      <button onClick={handleSearch}>
        Search
      </button>
    </div>
  );
}

export default SearchBar;
```

Here:

- `onChange` detects changes in the input.
- `event.target.value` reads the entered text.
- `onClick` executes a function when the button is clicked.

### Concept 6 – Conditional rendering

Suppose the weather API is loading.

We should display:

```
Loading weather information...
```

When data arrives, display the weather.

```
function WeatherStatus({ loading }) {
  return (
    <div>
      {loading ? (
        <p>Loading weather information...</p>
      ) : (
        <p>Weather information loaded!</p>
      )}
    </div>
  );
}

export default WeatherStatus;
```

### Concept 7 – Arrays and map()

The API returns multiple forecast entries.

We need to display them as cards.

```
const cities = ["Pune", "Mumbai", "Delhi"];

function CityList() {
  return (
    <div>
      {cities.map((city) => (
        <p key={city}>{city}</p>
      ))}
    </div>
  );
}

export default CityList;
```

`map()` transforms each array item into a React element.

### Concept 8 – useEffect

We use `useEffect` to synchronize a component with external systems, such as APIs.

Example:

```
import { useEffect } from "react";

function App() {
  useEffect(() => {
    console.log("Component mounted");
  }, []);

  return <h1>SkyCast</h1>;
}

export default App;
```

The empty dependency array means this effect runs when the component mounts.

We'll use this concept later to fetch the initial weather.

React fundamentals practice checklist

Your learning progress

0/9

Create a Navbar component

Create a WeatherCard component

Understand JSX expressions

Pass city and temperature through props

Change the city using useState

Build a controlled search input

Display loading using conditional rendering

Render forecast cards using map()

Understand useEffect and its dependency array

Reference: [React official Quick Start](https://react.dev/learn?utm_source=chatgpt.com).&#x20;

[image](https://www.google.com/s2/favicons?domain=https://react.dev\&sz=32)

React



# 8. Learn Fetch API – The most important part of this project

Module 3 – Third-Party API Integration

Now let's understand how React communicates with external APIs.

### What is an API?

API stands for Application Programming Interface.

Imagine:

- Your React application is a customer.
- The weather API is a restaurant.
- The HTTP request is your order.
- The JSON response is your food.

You request something, and the server returns information.

### What is Fetch API?

JavaScript provides a built-in function called `fetch()`.

It allows us to make HTTP requests.

Example:

```
fetch("https://api.example.com/weather")
  .then((response) => response.json())
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.log(error);
  });
```

Understand each line:

| Code       | Meaning                                     |
| ---------- | ------------------------------------------- |
| `fetch()`  | Sends HTTP request                          |
| `response` | Receives server response                    |
| `.json()`  | Converts JSON response into JavaScript data |
| `data`     | Contains the returned information           |
| `.catch()` | Handles network or request errors           |

Important: `fetch()` does not automatically throw an error for HTTP 404 or 500 responses. You should check `response.ok`.

### Learn async and await

Modern JavaScript commonly uses `async` and `await`.

```
async function getWeather() {
  try {
    const response = await fetch(
      "https://api.open-meteo.com/v1/forecast?latitude=18.52&longitude=73.85&current=temperature_2m&timezone=auto"
    );

    if (!response.ok) {
      throw new Error("Weather request failed");
    }

    const data = await response.json();

    console.log(data);

  } catch (error) {
    console.log(error.message);
  }
}

getWeather();
```

Understand:

- `async`: declares an asynchronous function.
- `await`: waits for a Promise to settle.
- `try`: contains code that might fail.
- `catch`: handles errors.
- `response.json()`: parses the response body.

### Practical 1 – Fetch API without React

Create a JavaScript file named `api-practice.js`.

```
async function getPuneWeather() {
  const url =
    "https://api.open-meteo.com/v1/forecast?latitude=18.52&longitude=73.85&current=temperature_2m,relative_humidity_2m,wind_speed_10m&timezone=auto";

  try {
    const response = await fetch(url);

    if (!response.ok) {
      throw new Error("API request failed");
    }

    const data = await response.json();

    console.log("Temperature:", data.current.temperature_2m);
    console.log("Humidity:", data.current.relative_humidity_2m);
    console.log("Wind Speed:", data.current.wind_speed_10m);

  } catch (error) {
    console.error("Error:", error.message);
  }
}

getPuneWeather();
```

Run it in the browser console or a JavaScript environment that supports `fetch`.

Expected output structure:

```
Temperature: 29.5
Humidity: 45
Wind Speed: 12.4
```

Values will vary.



Milestone 2

&#x20;You have successfully understood how to communicate with a third-party API without using React.



# 9. Integrate the Weather API into React

Module 4 – Real API Integration

Now we combine everything you have learned.

We'll implement the integration in four small steps.

## Step 9.1 – Create the API service

Open:

`src/services/weatherService.js`

This file will contain all our API communication logic.

First, create a function to search for a city.

```
const GEO_URL =
  "https://geocoding-api.open-meteo.com/v1/search";

export async function searchCity(city) {
  const params = new URLSearchParams({
    name: city,
    count: "5",
    language: "en",
    format: "json",
  });

  const response = await fetch(`${GEO_URL}?${params}`);

  if (!response.ok) {
    throw new Error("Unable to search city");
  }

  const data = await response.json();

  if (!data.results || data.results.length === 0) {
    throw new Error("City not found");
  }

  return data.results;
}
```

Let's understand:

1. `GEO_URL` stores our Geocoding API endpoint.
2. `URLSearchParams` creates the query parameters.
3. `fetch()` sends the request.
4. `response.json()` reads the JSON.
5. We check whether the city exists.
6. We return the matching results.

Why return `data.results`?

Because our next component needs the city's coordinates.

## Step 9.2 – Create the weather function

Continue in the same file.

```
const WEATHER_URL =
  "https://api.open-meteo.com/v1/forecast";

export async function getWeather(latitude, longitude) {
  const params = new URLSearchParams({
    latitude: String(latitude),
    longitude: String(longitude),

    current: [
      "temperature_2m",
      "relative_humidity_2m",
      "apparent_temperature",
      "is_day",
      "precipitation",
      "weather_code",
      "wind_speed_10m",
    ].join(","),

    hourly: [
      "temperature_2m",
      "precipitation_probability",
    ].join(","),

    daily: [
      "weather_code",
      "temperature_2m_max",
      "temperature_2m_min",
      "sunrise",
      "sunset",
    ].join(","),

    timezone: "auto",
    forecast_days: "5",
  });

  const response = await fetch(`${WEATHER_URL}?${params}`);

  if (!response.ok) {
    throw new Error("Unable to retrieve weather data");
  }

  return await response.json();
}
```

Notice something important:

We are not hardcoding the coordinates of Pune.

Instead, the function accepts:

```
getWeather(latitude, longitude);
```

This means we can search Pune, Mumbai, Delhi or any other supported city.

## Step 9.3 – Create the SearchBar component

Open:

`src/components/SearchBar.jsx`

```
import { useState } from "react";

function SearchBar({ onSearch, loading }) {
  const [city, setCity] = useState("");

  function handleSubmit(event) {
    event.preventDefault();

    if (!city.trim()) {
      return;
    }

    onSearch(city.trim());
  }

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        value={city}
        placeholder="Search city..."
        onChange={(event) => setCity(event.target.value)}
      />

      <button type="submit" disabled={loading}>
        {loading ? "Searching..." : "Search"}
      </button>
    </form>
  );
}

export default SearchBar;
```

New concepts:

- `onSubmit`: handles form submission.
- `event.preventDefault()`: prevents the browser from reloading the page.
- `disabled`: prevents repeated submissions while loading.
- `onSearch`: a function passed from the parent component.

## Step 9.4 – Connect everything inside App.jsx

Open:

`src/App.jsx`

```
import { useState } from "react";

import SearchBar from "./components/SearchBar";

import {
  searchCity,
  getWeather,
} from "./services/weatherService";

function App() {
  const [weather, setWeather] = useState(null);
  const [location, setLocation] = useState(null);

  const [loading, setLoading] = useState(false);
  const [error, setError] = useState("");

  async function handleSearch(city) {
    setLoading(true);
    setError("");

    try {
      // Step 1: Search for the city
      const locations = await searchCity(city);

      // Step 2: Select the first matching location
      const selectedCity = locations[0];

      // Step 3: Get latitude and longitude
      const { latitude, longitude } = selectedCity;

      // Step 4: Fetch weather information
      const weatherData = await getWeather(
        latitude,
        longitude
      );

      // Step 5: Update React state
      setLocation(selectedCity);
      setWeather(weatherData);

    } catch (err) {
      setError(err.message);
      setWeather(null);
      setLocation(null);

    } finally {
      setLoading(false);
    }
  }

  return (
    <div>
      <h1>SkyCast Weather</h1>

      <SearchBar
        onSearch={handleSearch}
        loading={loading}
      />

      {loading && <p>Loading weather...</p>}

      {error && <p>{error}</p>}

      {weather && location && (
        <div>
          <h2>{location.name}</h2>

          <h1>
            {weather.current.temperature_2m}°C
          </h1>

          <p>
            Humidity:
            {weather.current.relative_humidity_2m}%
          </p>

          <p>
            Wind Speed:
            {weather.current.wind_speed_10m} km/h
          </p>

          <p>
            Feels Like:
            {weather.current.apparent_temperature}°C
          </p>
        </div>
      )}
    </div>
  );
}

export default App;
```

### Understand the complete integration

## How your code works

SearchBar.jsx

User enters Pune

App.jsx

handleSearch("Pune")

searchCity()

Geocoding API

Returns latitude and longitude

getWeather()

Forecast API

Returns current, hourly and daily weather

setWeather(weatherData)

React updates the UI



Milestone 3

&#x20;Search for a city and retrieve its real weather data!



# 10. Design the attractive weather application

Module 5 – Frontend Development

Now we improve the appearance.

We'll build the UI in separate components rather than putting everything inside App.jsx.

### Step 10.1 – Create CurrentWeather.jsx

`src/components/CurrentWeather.jsx`

```
function CurrentWeather({ location, weather }) {
  const current = weather.current;

  return (
    <section className="current-weather">
      <div>
        <p>
          {location.name}, {location.country}
        </p>

        <h1>
          {Math.round(current.temperature_2m)}°C
        </h1>

        <p>
          Feels like {current.apparent_temperature}°C
        </p>
      </div>

      <div className="weather-details">
        <p>
          Humidity:
          {current.relative_humidity_2m}%
        </p>

        <p>
          Wind:
          {current.wind_speed_10m} km/h
        </p>

        <p>
          Precipitation:
          {current.precipitation} mm
        </p>
      </div>
    </section>
  );
}

export default CurrentWeather;
```

### Step 10.2 – Create WeatherDetails.jsx

`src/components/WeatherDetails.jsx`

```
function WeatherDetails({ current }) {
  const details = [
    {
      title: "Humidity",
      value: `${current.relative_humidity_2m}%`,
    },
    {
      title: "Wind Speed",
      value: `${current.wind_speed_10m} km/h`,
    },
    {
      title: "Feels Like",
      value: `${current.apparent_temperature}°C`,
    },
    {
      title: "Precipitation",
      value: `${current.precipitation} mm`,
    },
  ];

  return (
    <div className="details-grid">
      {details.map((item) => (
        <div className="detail-card" key={item.title}>
          <p>{item.title}</p>
          <h3>{item.value}</h3>
        </div>
      ))}
    </div>
  );
}

export default WeatherDetails;
```

### Step 10.3 – Create DailyForecast.jsx

`src/components/DailyForecast.jsx`

```
function DailyForecast({ daily }) {
  return (
    <section>
      <h2>5-Day Forecast</h2>

      <div className="forecast-grid">
        {daily.time.map((date, index) => (
          <div className="forecast-card" key={date}>
            <p>{date}</p>

            <h3>
              {Math.round(
                daily.temperature_2m_max[index]
              )}°C
            </h3>

            <p>
              Low: {Math.round(
                daily.temperature_2m_min[index]
              )}°C
            </p>
          </div>
        ))}
      </div>
    </section>
  );
}

export default DailyForecast;
```

Notice how we are accessing the daily API data.

```
daily.time
daily.temperature_2m_max
daily.temperature_2m_min
```

The arrays share the same indexes. For example, index `0` represents the first forecast day.

### Step 10.4 – Add components to App.jsx

Import:

```
import CurrentWeather from "./components/CurrentWeather";
import WeatherDetails from "./components/WeatherDetails";
import DailyForecast from "./components/DailyForecast";
```

Replace your existing weather display section with:

```
{weather && location && (
  <main className="weather-dashboard">

    <CurrentWeather
      location={location}
      weather={weather}
    />

    <WeatherDetails
      current={weather.current}
    />

    <DailyForecast
      daily={weather.daily}
    />

  </main>
)}
```

### Step 10.5 – Create the CSS

Open `src/index.css`:

```
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  background: linear-gradient(135deg, #101d3a, #263e68);
  color: white;
  min-height: 100vh;
}

button,
input {
  font: inherit;
}

button {
  cursor: pointer;
}

#root {
  min-height: 100vh;
}
```

Open `src/App.css`:

```
.app {
  max-width: 1100px;
  margin: auto;
  padding: 40px 20px;
}

h1, h2, p {
  margin-bottom: 15px;
}

form {
  display: flex;
  gap: 10px;
  margin: 25px 0;
}

input {
  flex: 1;
  padding: 14px;
  border: none;
  border-radius: 10px;
  outline: none;
}

button {
  padding: 14px 24px;
  border: none;
  border-radius: 10px;
  background: #63c5da;
  color: #10213b;
  font-weight: bold;
}

.current-weather {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 35px;
  background: rgba(255, 255, 255, 0.12);
  border-radius: 20px;
  margin-bottom: 25px;
}

.current-weather h1 {
  font-size: 64px;
}

.details-grid,
.forecast-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 15px;
  margin: 25px 0;
}

.detail-card,
.forecast-card {
  background: rgba(255, 255, 255, 0.12);
  padding: 20px;
  border-radius: 15px;
}

.forecast-grid {
  grid-template-columns: repeat(5, 1fr);
}

@media (max-width: 700px) {
  .current-weather {
    flex-direction: column;
    align-items: flex-start;
    gap: 20px;
  }

  .details-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .forecast-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}
```

Finally, ensure `App.jsx` imports its stylesheet:

```
import "./App.css";
```

Also, give your main wrapper the `app` class.

```
<div className="app">
  {/* Your application components */}
</div>
```

You now have the initial weather dashboard.

# 11. Advanced Weather Features – Make it a real application

After the basic application works, add these features one by one.

| Feature            | Implementation concept                        |
| ------------------ | --------------------------------------------- |
| Weather icons      | Map weather codes to icons                    |
| Day/night theme    | Use `is_day`                                  |
| Hourly forecast    | Use `hourly.time` and `hourly.temperature_2m` |
| Rain probability   | Use `hourly.precipitation_probability`        |
| Sunrise/sunset     | Use `daily.sunrise` and `daily.sunset`        |
| Current location   | Browser Geolocation API                       |
| Recent searches    | localStorage                                  |
| Search suggestions | Geocoding API results                         |
| Temperature units  | Celsius/Fahrenheit conversion                 |
| Dynamic background | Conditional CSS classes                       |

### Important practical – Weather codes

Open-Meteo returns a `weather_code` value.

You need to translate it into a human-readable condition.

For example:

| Weather code | Condition     |
| ------------ | ------------- |
| 0            | Clear sky     |
| 1            | Mainly clear  |
| 2            | Partly cloudy |
| 3            | Overcast      |
| 45           | Fog           |
| 51           | Light drizzle |
| 61           | Slight rain   |
| 63           | Moderate rain |
| 65           | Heavy rain    |
| 71           | Slight snow   |
| 80           | Rain showers  |
| 95           | Thunderstorm  |

Create:

`src/utils/weatherCodes.js`

```
export function getWeatherCondition(code) {
  const conditions = {
    0: "Clear Sky",
    1: "Mainly Clear",
    2: "Partly Cloudy",
    3: "Overcast",
    45: "Fog",
    51: "Light Drizzle",
    61: "Slight Rain",
    63: "Moderate Rain",
    65: "Heavy Rain",
    71: "Snow",
    80: "Rain Showers",
    95: "Thunderstorm",
  };

  return conditions[code] || "Unknown Weather";
}
```

Use it like this:

```
import { getWeatherCondition } from "../utils/weatherCodes";

<p>
  {getWeatherCondition(weather.current.weather_code)}
</p>
```

This is a simple example of transforming API data into user-friendly information. For a complete application, cover the remaining weather codes too.

# 12. Fetch API vs Axios – Understand the difference

You should learn both because companies commonly use different approaches.

| Fetch API                        | Axios                                 |
| -------------------------------- | ------------------------------------- |
| Built into modern browsers       | Third-party library                   |
| No installation needed           | Requires installation                 |
| JSON parsing is manual           | JSON response is automatically parsed |
| HTTP errors need manual checking | Rejects non-2xx responses by default  |
| Supports AbortController         | Supports AbortController              |

Install Axios:

```
npm install axios
```

Example:

```
import axios from "axios";

async function getWeather() {
  try {
    const response = await axios.get(
      "https://api.open-meteo.com/v1/forecast",
      {
        params: {
          latitude: 18.52,
          longitude: 73.85,
          current: "temperature_2m",
          timezone: "auto",
        },
      }
    );

    console.log(response.data);

  } catch (error) {
    console.log(error.message);
  }
}
```

My recommendation: First complete this project using Fetch API. Then rewrite the API service using Axios. That will give you a much stronger understanding of API integration.

# 13. Swagger and OpenAPI – Separate API learning module

Module 6 – Swagger / OpenAPI

This is an important distinction.

Open-Meteo is the weather API. Swagger is not another weather API.

Swagger is a collection of tools used to describe, document and test APIs. OpenAPI is the specification that describes an API's endpoints, parameters, request bodies and responses.

[How to Read and Understand API Documentation](https://images.openai.com/static-rsc-4/hm2p1pIzlilbjrZlD0N-PpN34gvARQt8SNTqvjKhKn0-wff_q5lrMmkh61Cm7NICn33dKyjirJK0MjFMOmxBGyM_yipvT10lY6b1wNsG4pWKMh2PKk5l5vkBbamn1MOHnVQZFdUuN4heSz7601VPpUNAF4wvKVWWnHKO340ddPQ?purpose=inline)

[archbee.com](https://www.archbee.com/blog/how-to-read-api-documentation?utm_source=chatgpt.com)

### Step 13.1 – Understand Swagger terminology

| Term           | Meaning                                   |
| -------------- | ----------------------------------------- |
| OpenAPI        | Standard format for describing APIs       |
| Swagger UI     | Interactive API documentation             |
| Swagger Editor | Write and validate OpenAPI specifications |
| Endpoint       | API URL                                   |
| GET            | Retrieve information                      |
| POST           | Send information                          |
| Response       | Data returned by server                   |
| Parameters     | Additional request information            |
| Schema         | Structure of request or response data     |

Useful official resources:

- [Swagger UI](https://swagger.io/tools/swagger-ui/?utm_source=chatgpt.com)
- [Swagger Editor](https://editor.swagger.io/?utm_source=chatgpt.com)
- [OpenAPI Specification](https://swagger.io/specification/?utm_source=chatgpt.com)

### Step 13.2 – Understand Swagger using your weather API

We can describe the Geocoding endpoint in OpenAPI format.

Open [Swagger Editor](https://editor.swagger.io/?utm_source=chatgpt.com).

Clear the existing example and paste:

```
openapi: 3.0.3

info:
  title: SkyCast Weather API
  description: API documentation for weather search
  version: 1.0.0

servers:
  - url: https://geocoding-api.open-meteo.com

paths:
  /v1/search:
    get:
      summary: Search for a city
      description: Find city coordinates using its name

      parameters:
        - name: name
          in: query
          required: true
          schema:
            type: string
          example: Pune

        - name: count
          in: query
          required: false
          schema:
            type: integer
            default: 5

        - name: language
          in: query
          required: false
          schema:
            type: string
            default: en

        - name: format
          in: query
          required: false
          schema:
            type: string
            default: json

      responses:
        "200":
          description: City information returned successfully

        "400":
          description: Invalid request
```

What happens?

1. Swagger reads your YAML file.
2. It identifies the API endpoint.
3. It displays the GET method.
4. It displays the parameters.
5. It generates interactive documentation.
6. You can use the Try it out feature to execute requests.



Swagger milestone

&#x20;You have documented your first third-party API endpoint.



### Step 13.3 – Test API endpoints using Swagger

In Swagger Editor:

1. Find `GET /v1/search`.
2. Click Try it out.
3. Enter `Pune` in the name field.
4. Enter `5` in count.
5. Click Execute.
6. Examine the server response.

This helps you understand the relationship between API documentation and actual API requests.

### Step 13.4 – Add your own Swagger backend (advanced)

Here's where the project becomes more professional.

So far, your React app is communicating directly with Open-Meteo.

Now imagine you create your own backend:

```
React Frontend
      |
      v
Express.js Backend
      |
      v
Open-Meteo Weather API
```

Your backend can expose endpoints such as:

```
GET /api/weather?city=Pune

GET /api/forecast?city=Mumbai

GET /api/search?city=Delhi
```

You can document these endpoints with Swagger UI.

First, create a separate backend folder:

```
mkdir skycast-backend
cd skycast-backend

npm init -y
npm install express cors dotenv
npm install swagger-ui-express swagger-jsdoc
npm install --save-dev nodemon
```

Create:

```
skycast-backend/
│
├── server.js
├── swagger.js
├── routes/
│   └── weatherRoutes.js
├── services/
│   └── weatherService.js
├── package.json
└── .env
```

Your backend's `server.js` will eventually:

1. Create an Express server.
2. Configure CORS.
3. Register weather routes.
4. Register Swagger UI.
5. Start listening on a port.

For example, your Swagger UI could be available at:

```
http://localhost:5000/api-docs
```

Important: This is an additional learning stage, not something you need to build before completing the React frontend. Open-Meteo already works directly from the browser for this learning project. You don't need a backend just to use Swagger Editor.

### Step 13.5 – What should you learn in the Swagger backend module?

| Practical                 | Level        |
| ------------------------- | ------------ |
| Understand HTTP methods   | Beginner     |
| Create OpenAPI YAML       | Beginner     |
| Document GET endpoint     | Beginner     |
| Document query parameters | Intermediate |
| Document response schemas | Intermediate |
| Create Express backend    | Intermediate |
| Integrate Swagger UI      | Intermediate |
| Document multiple routes  | Advanced     |
| Add request validation    | Advanced     |
| Add API error responses   | Advanced     |

This separate module will also help you when you start building your own REST APIs.

# 14. API debugging and troubleshooting

Module 7 – Debugging

A developer must know how to debug API integration.

Open your browser:

1. Right-click.
2. Select Inspect.
3. Open Network.
4. Select Fetch/XHR.
5. Search for a city.
6. Inspect the API request.

You should see:

- Request URL
- Request method
- Status code
- Response headers
- Response body
- Timing

### Common errors

| Error                          | Possible reason          | Solution                      |
| ------------------------------ | ------------------------ | ----------------------------- |
| 400                            | Invalid parameters       | Check API query               |
| 404                            | Incorrect endpoint       | Check API URL                 |
| 429                            | Too many requests        | Respect API limits            |
| Failed to fetch                | Network/CORS issue       | Check connection and endpoint |
| City not found                 | Invalid search           | Validate city name            |
| Cannot read properties of null | Data not loaded          | Add conditional rendering     |
| Unexpected token               | Invalid JSON or response | Inspect Network response      |
| Blank page                     | React error              | Check browser console         |

### Professional improvements

When you have the basic app running, also implement:

- AbortController to cancel outdated requests.
- Debouncing for city search suggestions.
- A proper loading skeleton.
- Better API error messages.
- Handling of empty city results.
- Handling of multiple cities with the same name.
- A fallback city when the application first loads.

One more important point: avoid making API requests on every keystroke. Use a Search button initially, then implement debouncing as an advanced exercise.

# 15. Complete learning roadmap

Here is the order I recommend following.

## SkyCast development roadmap

1. Module 1 – Environment Setup

   Node.js, npm, VS Code, Vite, React installation

   Beginner
2. Module 2 – React Fundamentals

   JSX, components, props, state, events, hooks

   Beginner
3. Module 3 – Fetch API

   HTTP requests, JSON, promises, async/await

   Beginner
4. Module 4 – Third-Party API Integration

   Geocoding, weather endpoints, API services, response handling

   Intermediate
5. Module 5 – Frontend Development

   Reusable components, dashboard, CSS, responsive UI

   Intermediate
6. Module 6 – Swagger and OpenAPI

   API documentation, testing, OpenAPI YAML

   Intermediate
7. Module 7 – Backend Integration

   Express.js, API routes, Swagger UI, CORS

   Advanced
8. Module 8 – Advanced Features

   Geolocation, hourly forecast, charts, caching, error handling

   Advanced
9. Module 9 – Deployment

   GitHub, production build, Vercel or Netlify

   Project completion

# 16. Deployment – Publish your React application

Module 8 – Deployment

Once your application works locally, publish it online.

### Step 16.1 – Create production build

Inside your React project:

```
npm run build
```

This creates a `dist` folder.

### Step 16.2 – Upload to GitHub

Create a GitHub repository named:

```
skycast-weather
```

Run:

```
git init
git add .
git commit -m "Initial SkyCast weather application"
git branch -M main
git remote add origin YOUR_GITHUB_REPOSITORY_URL
git push -u origin main
```

### Step 16.3 – Deploy using Vercel

1. Visit [Vercel](https://vercel.com/?utm_source=chatgpt.com).
2. Sign in using GitHub.
3. Import your `skycast-weather` repository.
4. Select Vite as the framework.
5. Set the build command to `npm run build`.
6. Set the output directory to `dist`.
7. Click Deploy.

Your weather application will be accessible through a public URL.

# 17. Practical assignments – Test your knowledge

Don't just complete the code. Try these assignments without looking at the solution.

## Assignment tracker

# 0/12

Tasks completed

AllBeginnerIntermediateAdvanced

Create a static weather card

Beginner

Display city, temperature, humidity and wind speed using hardcoded data.

Create a city search component

Beginner

Build an input and button using useState and onChange.

Fetch API practice

Beginner

Retrieve Pune weather and print temperature in the console.

Integrate Geocoding API

Intermediate

Search a city and retrieve its latitude and longitude.

Display live weather

Intermediate

Use the coordinates to retrieve current weather.

Create a five-day forecast

Intermediate

Render daily temperatures using map().

Create hourly weather cards

Intermediate

Display temperature and precipitation probability.

Current location weather

Advanced

Use browser Geolocation API and fetch weather using coordinates.

Build Swagger documentation

Advanced

Create an OpenAPI document for your weather endpoints.

Create an Express API

Advanced

Build a backend proxy for the weather API and document it using Swagger UI.

Optimize API requests

Advanced

Implement request cancellation, debouncing and caching.

Deploy your application

Advanced

Publish your frontend and, if built, your backend.

Reset progress

# 18. How to learn this project quickly

I recommend a 7-day learning schedule. Spend approximately 2–3 focused hours per day.

| Day   | Learning target                             |
| ----- | ------------------------------------------- |
| Day 1 | React setup, JSX, components, props         |
| Day 2 | useState, events, useEffect, forms          |
| Day 3 | Fetch API, JSON, async/await                |
| Day 4 | Open-Meteo integration and search           |
| Day 5 | Complete dashboard and responsive CSS       |
| Day 6 | Swagger, OpenAPI and Express introduction   |
| Day 7 | Advanced features, debugging and deployment |

## 19. Important interview questions

Once you finish the application, prepare these questions:

1. What is React JS?
2. What is JSX?
3. What are components?
4. What is the difference between props and state?
5. What is useState?
6. What is useEffect?
7. What is the Fetch API?
8. What is the difference between GET and POST?
9. What is JSON?
10. What is a third-party API?
11. What is the difference between Fetch and Axios?
12. What is asynchronous JavaScript?
13. What is CORS?
14. What is an API endpoint?
15. What is OpenAPI?
16. What is Swagger UI?
17. What is the difference between frontend and backend API integration?
18. How do you handle API failures?
19. What is API rate limiting?
20. How would you optimize API calls in React?

# 20. Your first learning session – Start here

Don't start all eight modules today. Let's make sure your fundamentals are strong first.

Day 1 – Beginner React

0/7 completed

Install Node.js and VS Code

Verify node -v and npm -v.

Create Vite React project

Run the project using npm run dev.

Understand project structure

Explore src, public, App.jsx and main.jsx.

Create Navbar component

Create and import Navbar.jsx.

Create WeatherCard component

Display Pune and Mumbai using props.

Build a search input

Use useState and onChange.

Test your first API

Open the Open-Meteo Geocoding URL and inspect JSON.

Start my Day 1 lesson&#x20;

My final recommendation: Learn React fundamentals, then Fetch API, then integrate the weather service, and only after that learn Swagger and backend integration. This order will prevent confusion and make you understand how real applications communicate with external services.

Your most important reference material:

- [React official learning documentation](https://react.dev/learn?utm_source=chatgpt.com)
- [Open-Meteo API documentation](https://open-meteo.com/en/docs?utm_source=chatgpt.com)
- [MDN Fetch API guide](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API?utm_source=chatgpt.com)
- [Swagger documentation](https://swagger.io/docs/?utm_source=chatgpt.com)
- [Vite guide](https://vite.dev/guide/?utm_source=chatgpt.com)

One important API licensing note: Open-Meteo's free API is intended for non-commercial use under its free service terms, with attribution required. Check its current terms before publishing a commercial application.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://github.com\&sz=32)

GitHub+1



Let's build it like a developer, not like someone copying a YouTube tutorial.
