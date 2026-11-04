# SkyCast — Complete React Weather Forecasting Project

A step-by-step beginner-to-advanced project using React, Vite, Open-Meteo, Fetch API, Swagger/OpenAPI, and an optional Express backend.

> Follow the steps in order. Do not skip the API-testing and milestone checks. The free Open-Meteo service is intended for eligible non-commercial use; check its current terms and attribution requirements before commercial use.

---

# 0. What you will build

SkyCast lets a user:

- Search for a city.
- View current temperature, apparent temperature, humidity, wind, precipitation, and conditions.
- View an hourly forecast.
- View a five-day forecast.
- Switch between Celsius and Fahrenheit.
- Load weather for the browser's current location.
- See loading and error states.
- Use a responsive layout on mobile and desktop.

Learning sequence:

1. Install Node.js and VS Code.
2. Create a React project using Vite.
3. Understand the project structure.
4. Learn components, JSX, props, state, events, lists, and effects.
5. Test the third-party API outside React.
6. Build a clean API service.
7. Connect the API to React.
8. Build the dashboard components.
9. Add weather descriptions and icons.
10. Add hourly/daily forecasts, units, location, and recent searches.
11. Debug requests in browser DevTools.
12. Learn Swagger/OpenAPI.
13. Optionally create an Express backend with Swagger UI.
14. Build and deploy.

# 1. Install the tools

## 1.1 Install Node.js

1. Open https://nodejs.org/
2. Download the current **LTS** release.
3. Run the installer.
4. Keep the default options, including npm.
5. Finish installation.
6. Close and reopen PowerShell or the VS Code terminal.

Verify:

```bash
node -v
npm -v
```

Both commands must print version numbers. If Windows says a command is not recognized, restart the terminal. If it still fails, rerun the Node.js installer and ensure Node is added to PATH.

## 1.2 Install VS Code

Download: https://code.visualstudio.com/

Useful extensions (optional):

- ES7+ React/Redux/React-Native snippets
- Prettier
- ESLint
- Error Lens
- Thunder Client

Extensions do not replace understanding the code.

# 2. Create the React project

Open PowerShell or the VS Code terminal. Choose a folder in which you want the project.

Example:

```powershell
cd $HOME\Desktop
npm create vite@latest skycast-weather
```

When prompted, select:

- Framework: `React`
- Variant: `JavaScript`

Then run:

```powershell
cd skycast-weather
npm install
npm run dev
```

Open the local URL printed by Vite, usually:

```text
http://localhost:5173/
```

Keep this terminal running while developing. To stop the server, press `Ctrl + C`.

## 2.1 Open the folder in VS Code

Open a second terminal, navigate to the project folder, and run:

```powershell
code .
```

If the `code` command is unavailable, open VS Code manually and choose **File → Open Folder → skycast-weather**.

## 2.2 Understand the generated files

- `src/main.jsx`: connects React to the HTML page.
- `src/App.jsx`: root application component.
- `src/index.css`: global styles.
- `src/App.css`: application styles.
- `index.html`: browser page entry point.
- `package.json`: project scripts and dependencies.
- `node_modules`: installed packages; do not edit manually.
- `public`: static files served as-is.

# 3. Learn the API before writing React code

We use Open-Meteo because its basic forecast and geocoding services do not require an API key for eligible free use.

Documentation:

- Weather API: https://open-meteo.com/en/docs
- Geocoding API: https://open-meteo.com/en/docs/geocoding-api

## 3.1 Understand the two-step API flow

A forecast endpoint needs latitude and longitude, not a city name. Therefore:

1. Search the city using the Geocoding API.
2. Read the returned latitude and longitude.
3. Send those coordinates to the Forecast API.
4. Read the JSON response.
5. Display selected values in React.

Flow:

```text
User types "Pune"
       |
       v
Geocoding API: search city
       |
       v
City result: latitude + longitude
       |
       v
Forecast API: request weather by coordinates
       |
       v
JSON: current + hourly + daily
       |
       v
React components render the data
```

## 3.2 Test the Geocoding API in a browser

Open this URL:

https://geocoding-api.open-meteo.com/v1/search?name=Pune&count=5&language=en&format=json

Look for `results`. Each result can include `name`, `country`, `latitude`, `longitude`, and other location metadata.

If the city is not found, the response may omit `results`.

## 3.3 Test the Forecast API in a browser

Open:

https://api.open-meteo.com/v1/forecast?latitude=18.5204&longitude=73.8567&current=temperature_2m,relative_humidity_2m,apparent_temperature,is_day,precipitation,weather_code,wind_speed_10m&hourly=temperature_2m,precipitation_probability,weather_code&daily=weather_code,temperature_2m_max,temperature_2m_min,sunrise,sunset&timezone=auto&forecast_days=5

Inspect these objects:

- `current`: current weather measurements.
- `hourly`: arrays of hourly times and values.
- `daily`: arrays of daily dates and values.
- `current_units`, `hourly_units`, `daily_units`: measurement units returned by the API.

Important: array values match by index. For example, `daily.time[0]`, `daily.temperature_2m_max[0]`, and `daily.temperature_2m_min[0]` describe the same date.

The actual values change with time and location. Do not expect example temperatures to match your response.

# 4. Learn the React fundamentals with small exercises

Before integrating the API, understand these concepts.

## 4.1 Component

A component is a reusable UI function. Example:

```jsx
function Welcome() {
  return <h1>Welcome to SkyCast</h1>;
}

export default Welcome;
```

Create `src/Welcome.jsx`, then import it in `App.jsx`:

```jsx
import Welcome from "./Welcome";

function App() {
  return <Welcome />;
}

export default App;
```

## 4.2 JSX and JavaScript expressions

JSX lets you write HTML-like markup inside JavaScript. Use curly braces to display JavaScript values:

```jsx
const city = "Pune";
const temperature = 29;

function Example() {
  return (
    <section>
      <h1>Weather in {city}</h1>
      <p>{temperature}°C</p>
    </section>
  );
}

export default Example;
```

## 4.3 Props

Props pass data from a parent component to a child component.

```jsx
function WeatherCard({ city, temperature }) {
  return (
    <article>
      <h2>{city}</h2>
      <p>{temperature}°C</p>
    </article>
  );
}

export default WeatherCard;
```

Use it:

```jsx
<WeatherCard city="Pune" temperature={29} />
<WeatherCard city="Mumbai" temperature={31} />
```

## 4.4 State with useState

State stores data that can change and cause the UI to render again.

```jsx
import { useState } from "react";

function CityExample() {
  const [city, setCity] = useState("Pune");

  return (
    <div>
      <h2>{city}</h2>
      <button onClick={() => setCity("Mumbai")}>
        Change city
      </button>
    </div>
  );
}

export default CityExample;
```

## 4.5 Controlled input and events

```jsx
import { useState } from "react";

function SearchPractice() {
  const [city, setCity] = useState("");

  function handleSubmit(event) {
    event.preventDefault();

    if (!city.trim()) {
      alert("Enter a city name");
      return;
    }

    alert(`You searched for ${city}`);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input
        value={city}
        onChange={(event) => setCity(event.target.value)}
        placeholder="Enter a city"
      />
      <button type="submit">Search</button>
    </form>
  );
}

export default SearchPractice;
```

- `value` connects the input to React state.
- `onChange` updates the state.
- `onSubmit` handles form submission.
- `preventDefault()` prevents a browser page reload.

## 4.6 Conditional rendering

```jsx
function Status({ loading, error }) {
  if (loading) return <p>Loading...</p>;
  if (error) return <p role="alert">{error}</p>;
  return <p>Ready</p>;
}

export default Status;
```

## 4.7 Render arrays with map()

```jsx
const cities = ["Pune", "Mumbai", "Delhi"];

function CityList() {
  return (
    <ul>
      {cities.map((city) => (
        <li key={city}>{city}</li>
      ))}
    </ul>
  );
}

export default CityList;
```

React needs a stable `key` for each rendered list item.

## 4.8 useEffect

`useEffect` synchronizes a component with an external system, such as an API or browser feature.

```jsx
import { useEffect } from "react";

function EffectExample() {
  useEffect(() => {
    console.log("Component mounted");
  }, []);

  return <h1>SkyCast</h1>;
}

export default EffectExample;
```

The empty dependency array means this effect runs after the initial mount. Do not use effects for calculations that can be done directly during rendering.

# 5. Create the final folder structure

Stop the Vite server with `Ctrl + C` before reorganizing if you prefer. Inside `src`, create the following folders and files:

```text
skycast-weather/
├── public/
├── src/
│   ├── components/
│   │   ├── CurrentWeather.jsx
│   │   ├── DailyForecast.jsx
│   │   ├── HourlyForecast.jsx
│   │   ├── SearchBar.jsx
│   │   └── WeatherDetails.jsx
│   ├── services/
│   │   └── weatherService.js
│   ├── utils/
│   │   └── weatherCodes.js
│   ├── App.jsx
│   ├── App.css
│   ├── index.css
│   └── main.jsx
├── index.html
├── package.json
└── vite.config.js
```

Create folders by right-clicking `src` in VS Code → **New Folder**. Create files by right-clicking the appropriate folder → **New File**.

You may delete the starter `App.css`, `App.jsx`, and `index.css` contents and replace them with the code below. Do not delete `main.jsx`; replace its contents as shown.

# 6. Write the API service

Create `src/services/weatherService.js`.

This file keeps API requests separate from UI components. It contains two exported functions: one searches for a city, and the other gets its weather.

```javascript
const GEO_URL = "https://geocoding-api.open-meteo.com/v1/search";
const WEATHER_URL = "https://api.open-meteo.com/v1/forecast";

export async function searchCity(city, signal) {
  const params = new URLSearchParams({
    name: city,
    count: "5",
    language: "en",
    format: "json",
  });

  const response = await fetch(`${GEO_URL}?${params}`, { signal });

  if (!response.ok) {
    throw new Error(`City search failed (HTTP ${response.status})`);
  }

  const data = await response.json();

  if (!data.results || data.results.length === 0) {
    throw new Error("City not found. Check the spelling and try again.");
  }

  return data.results;
}

export async function getWeather(latitude, longitude, signal) {
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
      "weather_code",
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

  const response = await fetch(`${WEATHER_URL}?${params}`, { signal });

  if (!response.ok) {
    throw new Error(`Weather request failed (HTTP ${response.status})`);
  }

  return response.json();
}
```

### Understand this file

- `URLSearchParams` safely builds query-string parameters.
- `fetch` sends an HTTP request.
- `response.ok` checks for an HTTP success status.
- `response.json()` parses the response body.
- `signal` lets the caller cancel an outdated request.
- `throw new Error(...)` sends failures to the calling component's `catch` block.

# 7. Convert weather codes into readable conditions

Create `src/utils/weatherCodes.js`.

Open-Meteo uses WMO weather codes. The helper below covers the commonly returned codes:

```javascript
const weatherConditions = {
  0: "Clear sky",
  1: "Mainly clear",
  2: "Partly cloudy",
  3: "Overcast",
  45: "Fog",
  48: "Depositing rime fog",
  51: "Light drizzle",
  53: "Moderate drizzle",
  55: "Dense drizzle",
  56: "Light freezing drizzle",
  57: "Dense freezing drizzle",
  61: "Slight rain",
  63: "Moderate rain",
  65: "Heavy rain",
  66: "Light freezing rain",
  67: "Heavy freezing rain",
  71: "Slight snow",
  73: "Moderate snow",
  75: "Heavy snow",
  77: "Snow grains",
  80: "Slight rain showers",
  81: "Moderate rain showers",
  82: "Violent rain showers",
  85: "Slight snow showers",
  86: "Heavy snow showers",
  95: "Thunderstorm",
  96: "Thunderstorm with slight hail",
  99: "Thunderstorm with heavy hail",
};

export function getWeatherCondition(code) {
  return weatherConditions[code] ?? "Unknown conditions";
}

export function getWeatherEmoji(code, isDay = 1) {
  if (code === 0) return isDay ? "☀️" : "🌙";
  if (code === 1 || code === 2) return isDay ? "🌤️" : "☁️";
  if (code === 3) return "☁️";
  if (code === 45 || code === 48) return "🌫️";
  if (code >= 51 && code <= 67) return "🌧️";
  if (code >= 71 && code <= 77) return "❄️";
  if (code >= 80 && code <= 82) return "🌦️";
  if (code >= 85 && code <= 86) return "🌨️";
  if (code >= 95) return "⛈️";
  return "🌡️";
}
```

# 8. Create the SearchBar component

Create `src/components/SearchBar.jsx`.

```jsx
import { useState } from "react";

function SearchBar({ onSearch, loading, onUseLocation }) {
  const [city, setCity] = useState("");

  function handleSubmit(event) {
    event.preventDefault();

    const trimmedCity = city.trim();

    if (!trimmedCity) {
      return;
    }

    onSearch(trimmedCity);
  }

  return (
    <div className="search-area">
      <form className="search-form" onSubmit={handleSubmit}>
        <input
          type="search"
          value={city}
          onChange={(event) => setCity(event.target.value)}
          placeholder="Search city, e.g. Pune"
          aria-label="City name"
          required
        />

        <button type="submit" disabled={loading}>
          {loading ? "Searching..." : "Search"}
        </button>
      </form>

      <button
        className="location-button"
        type="button"
        onClick={onUseLocation}
        disabled={loading}
      >
        Use my location
      </button>
    </div>
  );
}

export default SearchBar;
```

The parent passes callback functions as props. The child does not need to know how the API works.

# 9. Create the CurrentWeather component

Create `src/components/CurrentWeather.jsx`.

```jsx
import {
  getWeatherCondition,
  getWeatherEmoji,
} from "../utils/weatherCodes";

function CurrentWeather({ location, current, unit }) {
  const temperature =
    unit === "C"
      ? current.temperature_2m
      : (current.temperature_2m * 9) / 5 + 32;

  const feelsLike =
    unit === "C"
      ? current.apparent_temperature
      : (current.apparent_temperature * 9) / 5 + 32;

  return (
    <section className="current-card">
      <div className="current-top">
        <div>
          <p className="eyebrow">CURRENT WEATHER</p>
          <h2>
            {location.name}
            {location.country ? `, ${location.country}` : ""}
          </h2>
          <p className="muted">
            {location.admin1 ? `${location.admin1} · ` : ""}
            {location.timezone || ""}
          </p>
        </div>

        <div className="weather-symbol" aria-hidden="true">
          {getWeatherEmoji(current.weather_code, current.is_day)}
        </div>
      </div>

      <div className="temperature-line">
        <p className="temperature">
          {Math.round(temperature)}°{unit}
        </p>
        <div>
          <p className="condition">
            {getWeatherCondition(current.weather_code)}
          </p>
          <p className="muted">
            Feels like {Math.round(feelsLike)}°{unit}
          </p>
        </div>
      </div>
    </section>
  );
}

export default CurrentWeather;
```

# 10. Create the WeatherDetails component

Create `src/components/WeatherDetails.jsx`.

```jsx
function WeatherDetails({ current }) {
  const details = [
    {
      label: "Humidity",
      value: `${current.relative_humidity_2m}%`,
      icon: "💧",
    },
    {
      label: "Wind speed",
      value: `${current.wind_speed_10m} km/h`,
      icon: "💨",
    },
    {
      label: "Precipitation",
      value: `${current.precipitation} mm`,
      icon: "🌧️",
    },
    {
      label: "Feels like",
      value: `${current.apparent_temperature}°C`,
      icon: "🌡️",
    },
  ];

  return (
    <section className="details-grid" aria-label="Weather details">
      {details.map((item) => (
        <article className="detail-card" key={item.label}>
          <span className="detail-icon" aria-hidden="true">
            {item.icon}
          </span>
          <p className="muted">{item.label}</p>
          <h3>{item.value}</h3>
        </article>
      ))}
    </section>
  );
}

export default WeatherDetails;
```

Note: the "Feels like" value in this simple details card is displayed in Celsius. The main current-weather card converts it when Fahrenheit is selected. If you want every card to change units, pass the selected unit into this component and apply the same conversion.

# 11. Create the HourlyForecast component

Create `src/components/HourlyForecast.jsx`.

```jsx
import {
  getWeatherCondition,
  getWeatherEmoji,
} from "../utils/weatherCodes";

function HourlyForecast({ hourly, unit }) {
  const now = new Date();

  const startIndex = hourly.time.findIndex(
    (time) => new Date(time) >= now
  );

  const firstIndex = startIndex === -1 ? 0 : startIndex;
  const indexes = Array.from({ length: 8 }, (_, i) => firstIndex + i)
    .filter((index) => index < hourly.time.length);

  function convertTemperature(value) {
    return unit === "C" ? value : (value * 9) / 5 + 32;
  }

  return (
    <section className="section-card">
      <div className="section-heading">
        <div>
          <p className="eyebrow">NEXT HOURS</p>
          <h2>Hourly forecast</h2>
        </div>
      </div>

      <div className="hourly-list">
        {indexes.map((index) => {
          const date = new Date(hourly.time[index]);

          return (
            <article className="hour-card" key={hourly.time[index]}>
              <p className="muted">
                {date.toLocaleTimeString([], {
                  hour: "numeric",
                  minute: "2-digit",
                })}
              </p>
              <span className="hour-icon" title={getWeatherCondition(hourly.weather_code[index])}>
                {getWeatherEmoji(hourly.weather_code[index])}
              </span>
              <h3>{Math.round(convertTemperature(hourly.temperature_2m[index]))}°</h3>
              <p className="muted">
                {hourly.precipitation_probability[index] ?? 0}% rain
              </p>
            </article>
          );
        })}
      </div>
    </section>
  );
}

export default HourlyForecast;
```

# 12. Create the DailyForecast component

Create `src/components/DailyForecast.jsx`.

```jsx
import {
  getWeatherCondition,
  getWeatherEmoji,
} from "../utils/weatherCodes";

function DailyForecast({ daily, unit }) {
  function convertTemperature(value) {
    return unit === "C" ? value : (value * 9) / 5 + 32;
  }

  return (
    <section className="section-card">
      <div className="section-heading">
        <div>
          <p className="eyebrow">PLAN AHEAD</p>
          <h2>5-day forecast</h2>
        </div>
      </div>

      <div className="daily-list">
        {daily.time.map((date, index) => {
          const day = new Date(`${date}T12:00:00`);

          return (
            <article className="daily-row" key={date}>
              <p className="day-name">
                {index === 0
                  ? "Today"
                  : day.toLocaleDateString([], { weekday: "short" })}
              </p>

              <span
                className="daily-icon"
                title={getWeatherCondition(daily.weather_code[index])}
              >
                {getWeatherEmoji(daily.weather_code[index])}
              </span>

              <p className="daily-condition">
                {getWeatherCondition(daily.weather_code[index])}
              </p>

              <p className="daily-temperatures">
                <strong>
                  {Math.round(convertTemperature(daily.temperature_2m_max[index]))}°
                </strong>
                <span className="muted">
                  {Math.round(convertTemperature(daily.temperature_2m_min[index]))}°
                </span>
              </p>
            </article>
          );
        })}
      </div>
    </section>
  );
}

export default DailyForecast;
```

# 13. Connect everything in App.jsx

Create or replace `src/App.jsx`.

This component owns the main application state and coordinates the API calls.

```jsx
import { useEffect, useRef, useState } from "react";
import SearchBar from "./components/SearchBar";
import CurrentWeather from "./components/CurrentWeather";
import WeatherDetails from "./components/WeatherDetails";
import HourlyForecast from "./components/HourlyForecast";
import DailyForecast from "./components/DailyForecast";
import { getWeather, searchCity } from "./services/weatherService";
import "./App.css";

function App() {
  const [location, setLocation] = useState(null);
  const [weather, setWeather] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState("");
  const [unit, setUnit] = useState("C");
  const [recentCities, setRecentCities] = useState(() => {
    try {
      return JSON.parse(localStorage.getItem("skycast-recent-cities")) || [];
    } catch {
      return [];
    }
  });

  const requestController = useRef(null);

  useEffect(() => {
    localStorage.setItem(
      "skycast-recent-cities",
      JSON.stringify(recentCities)
    );
  }, [recentCities]);

  useEffect(() => {
    handleSearch("Pune");
    // Load the default city once when the app first mounts.
    // eslint-disable-next-line react-hooks/exhaustive-deps
  }, []);

  async function loadWeatherForLocation(selectedLocation) {
    requestController.current?.abort();

    const controller = new AbortController();
    requestController.current = controller;

    setLoading(true);
    setError("");

    try {
      const weatherData = await getWeather(
        selectedLocation.latitude,
        selectedLocation.longitude,
        controller.signal
      );

      setLocation(selectedLocation);
      setWeather(weatherData);
    } catch (err) {
      if (err.name !== "AbortError") {
        setError(err.message || "Unable to load weather.");
      }
    } finally {
      if (!controller.signal.aborted) {
        setLoading(false);
      }
    }
  }

  async function handleSearch(city) {
    requestController.current?.abort();

    const controller = new AbortController();
    requestController.current = controller;

    setLoading(true);
    setError("");

    try {
      const results = await searchCity(city, controller.signal);
      const selectedLocation = results[0];

      const weatherData = await getWeather(
        selectedLocation.latitude,
        selectedLocation.longitude,
        controller.signal
      );

      setLocation(selectedLocation);
      setWeather(weatherData);

      setRecentCities((previous) => {
        const withoutDuplicate = previous.filter(
          (item) => item.name.toLowerCase() !== selectedLocation.name.toLowerCase()
        );

        return [selectedLocation, ...withoutDuplicate].slice(0, 5);
      });
    } catch (err) {
      if (err.name !== "AbortError") {
        setError(err.message || "Something went wrong.");
      }
    } finally {
      if (!controller.signal.aborted) {
        setLoading(false);
      }
    }
  }

  function handleUseLocation() {
    if (!navigator.geolocation) {
      setError("Geolocation is not supported by this browser.");
      return;
    }

    setLoading(true);
    setError("");

    navigator.geolocation.getCurrentPosition(
      async (position) => {
        const selectedLocation = {
          name: "Your location",
          country: "",
          latitude: position.coords.latitude,
          longitude: position.coords.longitude,
        };

        await loadWeatherForLocation(selectedLocation);
      },
      (geoError) => {
        setLoading(false);

        if (geoError.code === geoError.PERMISSION_DENIED) {
          setError("Location permission was denied. Allow location access or search for a city.");
        } else if (geoError.code === geoError.TIMEOUT) {
          setError("Location request timed out. Try again.");
        } else {
          setError("Unable to determine your location.");
        }
      },
      {
        enableHighAccuracy: false,
        timeout: 10000,
        maximumAge: 300000,
      }
    );
  }

  return (
    <div className="app-shell">
      <header className="app-header">
        <a className="brand" href="/" aria-label="SkyCast home">
          <span className="brand-icon">☀</span>
          <span>SkyCast</span>
        </a>

        <div className="unit-switch" aria-label="Temperature unit">
          <button
            className={unit === "C" ? "active" : ""}
            onClick={() => setUnit("C")}
            type="button"
          >
            °C
          </button>
          <button
            className={unit === "F" ? "active" : ""}
            onClick={() => setUnit("F")}
            type="button"
          >
            °F
          </button>
        </div>
      </header>

      <main className="main-content">
        <section className="intro">
          <p className="eyebrow">WEATHER, MADE SIMPLE</p>
          <h1>Forecast at a glance.</h1>
          <p className="muted">
            Search a city or use your current location to see the forecast.
          </p>
        </section>

        <SearchBar
          onSearch={handleSearch}
          loading={loading}
          onUseLocation={handleUseLocation}
        />

        {recentCities.length > 0 && (
          <div className="recent-searches">
            <span className="muted">Recent:</span>
            {recentCities.map((city) => (
              <button
                type="button"
                className="recent-chip"
                key={`${city.name}-${city.latitude}`}
                onClick={() => loadWeatherForLocation(city)}
                disabled={loading}
              >
                {city.name}
              </button>
            ))}
          </div>
        )}

        {loading && (
          <p className="status-message" role="status">
            Loading weather data...
          </p>
        )}

        {error && (
          <div className="error-message" role="alert">
            {error}
          </div>
        )}

        {weather && location && !error && (
          <div className="dashboard">
            <CurrentWeather
              location={location}
              current={weather.current}
              unit={unit}
            />

            <WeatherDetails current={weather.current} />

            <HourlyForecast hourly={weather.hourly} unit={unit} />

            <DailyForecast daily={weather.daily} unit={unit} />

            <p className="attribution">
              Weather data provided by{" "}
              <a href="https://open-meteo.com/" target="_blank" rel="noreferrer">
                Open-Meteo
              </a>.
            </p>
          </div>
        )}

        {!weather && !loading && !error && (
          <p className="muted">Search for a city to see its weather.</p>
        )}
      </main>

      <footer className="footer">
        <p>SkyCast · Built with React and Open-Meteo</p>
      </footer>
    </div>
  );
}

export default App;
```

Important implementation note: `useEffect` loads Pune on first render. The app uses `AbortController` to cancel a previous fetch when a new search begins. Browser geolocation generally requires a secure context (HTTPS or localhost) and the user's permission.

# 14. Add the global CSS

Replace `src/index.css` with:

```css
@import url("https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=Space+Grotesk:wght@500;600;700&display=swap");

:root {
  font-family: "DM Sans", sans-serif;
  color: #f5f7ff;
  background: #081426;
  font-synthesis: none;
  text-rendering: optimizeLegibility;
  font-smooth: always;
  font-weight: 400;
}

* {
  box-sizing: border-box;
}

html {
  min-width: 320px;
  min-height: 100%;
}

body {
  margin: 0;
  min-width: 320px;
  min-height: 100vh;
}

button,
input {
  font: inherit;
}

button {
  cursor: pointer;
}

button:disabled {
  cursor: not-allowed;
  opacity: 0.6;
}

a {
  color: inherit;
}

#root {
  min-height: 100vh;
}
```

# 15. Add the application CSS

Replace `src/App.css` with:

```css
.app-shell {
  min-height: 100vh;
  overflow: hidden;
  background:
    radial-gradient(circle at 85% 8%, rgba(39, 130, 189, 0.2), transparent 28rem),
    radial-gradient(circle at 5% 35%, rgba(72, 92, 180, 0.14), transparent 25rem),
    #081426;
}

.app-header {
  width: min(1120px, calc(100% - 40px));
  margin: 0 auto;
  padding: 28px 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.brand {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  text-decoration: none;
  font-family: "Space Grotesk", sans-serif;
  font-size: 1.35rem;
  font-weight: 700;
}

.brand-icon {
  display: grid;
  place-items: center;
  width: 38px;
  height: 38px;
  border-radius: 13px;
  color: #09213b;
  background: #f8c86a;
}

.unit-switch {
  display: flex;
  padding: 4px;
  gap: 3px;
  border: 1px solid rgba(255, 255, 255, 0.12);
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.06);
}

.unit-switch button {
  border: 0;
  border-radius: 999px;
  padding: 8px 13px;
  color: #b7c4d8;
  background: transparent;
}

.unit-switch button.active {
  color: #102039;
  background: #f8c86a;
  font-weight: 700;
}

.main-content {
  width: min(1120px, calc(100% - 40px));
  margin: 35px auto 70px;
}

.intro {
  margin-bottom: 28px;
}

.eyebrow {
  margin: 0 0 9px;
  color: #8eb9df;
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 0.16em;
}

.intro h1 {
  margin: 0;
  font-family: "Space Grotesk", sans-serif;
  font-size: clamp(2.2rem, 5vw, 4rem);
  letter-spacing: -0.055em;
}

.muted {
  color: #9cabc1;
}

.intro > .muted {
  margin-top: 12px;
}

.search-area {
  display: flex;
  gap: 12px;
  align-items: stretch;
}

.search-form {
  display: flex;
  flex: 1;
  gap: 10px;
  padding: 7px;
  border: 1px solid rgba(255, 255, 255, 0.13);
  border-radius: 17px;
  background: rgba(255, 255, 255, 0.07);
}

.search-form input {
  width: 100%;
  min-width: 0;
  padding: 12px 14px;
  border: 0;
  outline: 0;
  color: white;
  background: transparent;
}

.search-form input::placeholder {
  color: #8293ac;
}

.search-form button,
.location-button {
  padding: 12px 19px;
  border: 0;
  border-radius: 12px;
  color: #102039;
  background: #f8c86a;
  font-weight: 700;
  white-space: nowrap;
}

.location-button {
  color: #eaf2ff;
  border: 1px solid rgba(255, 255, 255, 0.15);
  background: rgba(255, 255, 255, 0.08);
}

.recent-searches {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 8px;
  margin: 16px 0 25px;
  font-size: 0.85rem;
}

.recent-chip {
  padding: 7px 12px;
  border: 1px solid rgba(255, 255, 255, 0.13);
  border-radius: 999px;
  color: #dce8fa;
  background: rgba(255, 255, 255, 0.06);
}

.dashboard {
  display: grid;
  gap: 18px;
  margin-top: 28px;
}

.current-card,
.section-card,
.detail-card {
  border: 1px solid rgba(255, 255, 255, 0.11);
  background: linear-gradient(145deg, rgba(255, 255, 255, 0.105), rgba(255, 255, 255, 0.045));
  box-shadow: 0 18px 55px rgba(0, 0, 0, 0.13);
  backdrop-filter: blur(15px);
}

.current-card {
  padding: clamp(22px, 5vw, 42px);
  border-radius: 25px;
}

.current-top,
.temperature-line,
.section-heading {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 18px;
}

.current-top h2 {
  margin: 0 0 7px;
  font-family: "Space Grotesk", sans-serif;
  font-size: clamp(1.5rem, 4vw, 2.2rem);
}

.current-top .muted {
  margin: 0;
}

.weather-symbol {
  font-size: clamp(3rem, 9vw, 5.5rem);
}

.temperature-line {
  justify-content: flex-start;
  margin-top: 24px;
}

.temperature {
  margin: 0;
  font-family: "Space Grotesk", sans-serif;
  font-size: clamp(4rem, 11vw, 6.5rem);
  line-height: 1;
  letter-spacing: -0.08em;
}

.condition {
  margin: 0 0 8px;
  font-size: 1.15rem;
  font-weight: 700;
}

.temperature-line .muted {
  margin: 0;
}

.details-grid {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 14px;
}

.detail-card {
  padding: 20px;
  border-radius: 18px;
}

.detail-icon {
  display: inline-block;
  margin-bottom: 13px;
  font-size: 1.4rem;
}

.detail-card p {
  margin: 0 0 8px;
  font-size: 0.88rem;
}

.detail-card h3 {
  margin: 0;
  font-family: "Space Grotesk", sans-serif;
  font-size: 1.45rem;
}

.section-card {
  padding: 24px;
  border-radius: 20px;
}

.section-heading h2 {
  margin: 0;
  font-family: "Space Grotesk", sans-serif;
  font-size: 1.35rem;
}

.section-heading .eyebrow {
  margin-bottom: 5px;
}

.hourly-list {
  display: grid;
  grid-template-columns: repeat(8, minmax(82px, 1fr));
  gap: 10px;
  margin-top: 20px;
  overflow-x: auto;
  padding-bottom: 5px;
}

.hour-card {
  min-width: 82px;
  padding: 14px 8px;
  border-radius: 14px;
  text-align: center;
  background: rgba(255, 255, 255, 0.055);
}

.hour-card p {
  margin: 0;
  font-size: 0.76rem;
}

.hour-icon,
.daily-icon {
  display: block;
  margin: 13px 0;
  font-size: 1.6rem;
}

.hour-card h3 {
  margin: 0 0 8px;
}

.daily-list {
  margin-top: 15px;
}

.daily-row {
  display: grid;
  grid-template-columns: 75px 45px minmax(100px, 1fr) auto;
  align-items: center;
  gap: 12px;
  padding: 13px 0;
  border-bottom: 1px solid rgba(255, 255, 255, 0.09);
}

.daily-row:last-child {
  border-bottom: 0;
}

.day-name,
.daily-condition,
.daily-temperatures {
  margin: 0;
}

.daily-icon {
  margin: 0;
  text-align: center;
}

.daily-condition {
  color: #aab8cc;
  font-size: 0.9rem;
}

.daily-temperatures {
  display: flex;
  gap: 15px;
}

.attribution {
  margin: 0;
  color: #8798b1;
  font-size: 0.8rem;
  text-align: right;
}

.attribution a {
  color: #c7d9f4;
}

.status-message,
.error-message {
  margin-top: 20px;
  padding: 14px 16px;
  border-radius: 12px;
  background: rgba(255, 255, 255, 0.07);
}

.error-message {
  color: #ffd6d6;
  border: 1px solid rgba(255, 120, 120, 0.3);
  background: rgba(150, 35, 50, 0.18);
}

.footer {
  padding: 25px 20px;
  color: #8292a9;
  text-align: center;
  font-size: 0.82rem;
}

@media (max-width: 760px) {
  .search-area {
    flex-direction: column;
  }

  .location-button {
    width: 100%;
  }

  .details-grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }

  .hourly-list {
    grid-template-columns: repeat(8, 88px);
  }
}

@media (max-width: 480px) {
  .app-header,
  .main-content {
    width: min(100% - 28px, 1120px);
  }

  .app-header {
    padding: 18px 0;
  }

  .main-content {
    margin-top: 25px;
  }

  .search-form {
    gap: 3px;
  }

  .search-form button {
    padding: 11px 13px;
  }

  .current-card,
  .section-card {
    padding: 19px;
  }

  .daily-row {
    grid-template-columns: 55px 35px minmax(70px, 1fr) auto;
    gap: 7px;
  }

  .daily-condition {
    font-size: 0.75rem;
  }

  .daily-temperatures {
    gap: 8px;
    font-size: 0.85rem;
  }
}
```

# 16. Check main.jsx

Replace `src/main.jsx` with:

```jsx
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import App from "./App";
import "./index.css";

createRoot(document.getElementById("root")).render(
  <StrictMode>
    <App />
  </StrictMode>
);
```

React Strict Mode can run certain development checks more than once. You may notice development effects running twice; this is expected and helps reveal unsafe side effects.

# 17. Check index.html

Open the root-level `index.html`. Use:

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta
      name="description"
      content="SkyCast weather forecast application built with React."
    />
    <title>SkyCast — Weather Forecast</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>
```

# 18. Run and test the application

In the project root:

```bash
npm run dev
```

Open the URL Vite prints, normally `http://localhost:5173`.

Test each item:

1. Wait for the default Pune weather to load.
2. Search for `Mumbai`.
3. Search for `Delhi`.
4. Search for a deliberately invalid city name and confirm an error appears.
5. Switch from Celsius to Fahrenheit and confirm the main and forecast temperatures change.
6. Try the **Use my location** button and grant permission.
7. Refresh the page and check recent searches.
8. Resize the browser to mobile width.
9. Check that the hourly cards can scroll horizontally on a narrow screen.

## Important code improvement: convert all detail temperatures

The current `WeatherDetails.jsx` displays the feels-like value in Celsius regardless of the selected unit. To make every temperature consistent, replace its code with this:

```jsx
function WeatherDetails({ current, unit }) {
  const convertTemperature = (value) =>
    unit === "C" ? value : (value * 9) / 5 + 32;

  const details = [
    {
      label: "Humidity",
      value: `${current.relative_humidity_2m}%`,
      icon: "💧",
    },
    {
      label: "Wind speed",
      value: `${current.wind_speed_10m} km/h`,
      icon: "💨",
    },
    {
      label: "Precipitation",
      value: `${current.precipitation} mm`,
      icon: "🌧️",
    },
    {
      label: "Feels like",
      value: `${Math.round(convertTemperature(current.apparent_temperature))}°${unit}`,
      icon: "🌡️",
    },
  ];

  return (
    <section className="details-grid" aria-label="Weather details">
      {details.map((item) => (
        <article className="detail-card" key={item.label}>
          <span className="detail-icon" aria-hidden="true">{item.icon}</span>
          <p className="muted">{item.label}</p>
          <h3>{item.value}</h3>
        </article>
      ))}
    </section>
  );
}

export default WeatherDetails;
```

Then update the component call in `App.jsx`:

```jsx
<WeatherDetails current={weather.current} unit={unit} />
```

# 19. Understand Fetch API in isolation

Before relying on React, practise a standalone request.

Create a file named `api-practice.html` in the project root:

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Fetch API Practice</title>
  </head>
  <body>
    <h1>Open-Meteo API Practice</h1>
    <button id="load">Load Pune Weather</button>
    <pre id="output">Click the button to load data.</pre>

    <script>
      const button = document.querySelector("#load");
      const output = document.querySelector("#output");

      button.addEventListener("click", async () => {
        output.textContent = "Loading...";

        try {
          const url =
            "https://api.open-meteo.com/v1/forecast?latitude=18.5204&longitude=73.8567&current=temperature_2m,relative_humidity_2m,wind_speed_10m&timezone=auto";

          const response = await fetch(url);

          if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`);
          }

          const data = await response.json();

          output.textContent = JSON.stringify(
            {
              temperature: data.current.temperature_2m,
              humidity: data.current.relative_humidity_2m,
              windSpeed: data.current.wind_speed_10m,
            },
            null,
            2
          );
        } catch (error) {
          output.textContent = error.message;
        }
      });
    </script>
  </body>
</html>
```

Open the file in a browser. Click the button. Inspect the output. This exercise separates basic JavaScript API communication from React state management.

# 20. Fetch API vs Axios

Fetch is built into modern browsers. Axios is an additional library.

To practise Axios, install it in the React project:

```bash
npm install axios
```

Example:

```javascript
import axios from "axios";

export async function getPuneWeatherWithAxios() {
  const response = await axios.get(
    "https://api.open-meteo.com/v1/forecast",
    {
      params: {
        latitude: 18.5204,
        longitude: 73.8567,
        current: "temperature_2m,relative_humidity_2m",
        timezone: "auto",
      },
    }
  );

  return response.data;
}
```

Differences:

| Fetch | Axios |
|---|---|
| Built into browsers | Must be installed |
| Parse JSON using `response.json()` | Response data is usually available in `response.data` |
| Check `response.ok` yourself | Non-2xx responses reject by default |
| Supports AbortController | Supports AbortController |

Finish the app with Fetch first. Then rewrite one service function using Axios as an exercise. Do not mix both libraries without a reason.

# 21. Swagger and OpenAPI — understand the difference

- **API:** the service your application calls.
- **Endpoint:** a URL path that performs an operation.
- **HTTP method:** GET, POST, PUT, PATCH, DELETE, etc.
- **OpenAPI:** a standard format for describing an HTTP API.
- **Swagger UI:** a web interface that displays an OpenAPI description and can send test requests.
- **Swagger Editor:** an editor for writing and validating OpenAPI documents.

Official resources:

- Swagger UI: https://swagger.io/tools/swagger-ui/
- Swagger Editor: https://editor.swagger.io/
- OpenAPI specification: https://swagger.io/specification/

## 21.1 Document the third-party Geocoding API

1. Open https://editor.swagger.io/
2. Select the existing example text.
3. Replace it with the YAML below.
4. Wait for the editor to validate the document.
5. Inspect the endpoint, query parameters, and response.

```yaml
openapi: 3.0.3
info:
  title: Open-Meteo Geocoding API - Learning Documentation
  description: Learning example describing the city search endpoint.
  version: 1.0.0

servers:
  - url: https://geocoding-api.open-meteo.com

paths:
  /v1/search:
    get:
      summary: Search for a city
      description: Finds matching locations by city name.
      parameters:
        - name: name
          in: query
          required: true
          description: City or location name.
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
          description: Search completed. Results may be empty.
          content:
            application/json:
              schema:
                type: object
                properties:
                  results:
                    type: array
                    items:
                      type: object
                      properties:
                        name:
                          type: string
                        latitude:
                          type: number
                        longitude:
                          type: number
                        country:
                          type: string
        "400":
          description: Invalid query parameters.
```

This is a learning description of the endpoint, not an official Open-Meteo specification. The response schema is intentionally simplified.

## 21.2 Try the endpoint

In Swagger Editor's rendered documentation:

1. Expand `GET /v1/search`.
2. Select **Try it out** if available.
3. Enter `Pune` for `name`.
4. Keep or enter `5` for `count`.
5. Execute the request.
6. Inspect the response code and response body.

If the editor cannot execute the remote request due to browser CORS restrictions, test the same URL directly in a browser or use Thunder Client. Documentation validity and browser permission to call a server are separate things.

# 22. Optional advanced module: build your own Express API and Swagger UI

This is a separate backend project. It is not required for the React-only app. Build it after the frontend works.

Architecture:

```text
React frontend
     |
     v
Your Express backend
     |
     v
Open-Meteo third-party API
```

Why add a backend?

- Centralize API integration.
- Validate incoming parameters.
- Keep future private API credentials on the server, not in React.
- Add your own routes and error responses.
- Document your own API with Swagger UI.

Open-Meteo's basic public endpoint does not need a secret API key, so a backend is not required just to hide a key for this particular learning project.

## 22.1 Create the backend folder

Open a new terminal outside the frontend project:

```powershell
cd $HOME\Desktop
mkdir skycast-backend
cd skycast-backend
npm init -y
```

Install dependencies:

```bash
npm install express cors dotenv swagger-ui-express swagger-jsdoc
npm install --save-dev nodemon
```

## 22.2 Update backend package.json scripts

Open `skycast-backend/package.json`. Keep the generated name and dependencies, but ensure the scripts and module type look like this:

```json
{
  "name": "skycast-backend",
  "version": "1.0.0",
  "description": "SkyCast weather API backend",
  "main": "server.js",
  "type": "module",
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
  }
}
```

Do not delete the dependency entries that npm added. Add or update only the relevant fields. The complete dependency versions are managed by npm in your local package file.

## 22.3 Create backend folders

```text
skycast-backend/
├── routes/
│   └── weatherRoutes.js
├── services/
│   └── weatherService.js
├── .env
├── .gitignore
├── server.js
└── package.json
```

## 22.4 Create .env

```env
PORT=5000
CLIENT_ORIGIN=http://localhost:5173
```

This file stores local configuration. Do not commit secrets or `.env` files to GitHub.

## 22.5 Create .gitignore

```gitignore
node_modules/
.env
```

## 22.6 Create services/weatherService.js

```javascript
const GEO_URL = "https://geocoding-api.open-meteo.com/v1/search";
const WEATHER_URL = "https://api.open-meteo.com/v1/forecast";

export async function findCity(city) {
  const params = new URLSearchParams({
    name: city,
    count: "5",
    language: "en",
    format: "json",
  });

  const response = await fetch(`${GEO_URL}?${params}`);

  if (!response.ok) {
    throw new Error(`Geocoding provider returned HTTP ${response.status}`);
  }

  const data = await response.json();

  if (!data.results?.length) {
    return null;
  }

  return data.results[0];
}

export async function fetchForecast(latitude, longitude) {
  const params = new URLSearchParams({
    latitude: String(latitude),
    longitude: String(longitude),
    current: "temperature_2m,relative_humidity_2m,apparent_temperature,is_day,precipitation,weather_code,wind_speed_10m",
    hourly: "temperature_2m,precipitation_probability,weather_code",
    daily: "weather_code,temperature_2m_max,temperature_2m_min,sunrise,sunset",
    timezone: "auto",
    forecast_days: "5",
  });

  const response = await fetch(`${WEATHER_URL}?${params}`);

  if (!response.ok) {
    throw new Error(`Weather provider returned HTTP ${response.status}`);
  }

  return response.json();
}
```

## 22.7 Create routes/weatherRoutes.js

```javascript
import { Router } from "express";
import {
  findCity,
  fetchForecast,
} from "../services/weatherService.js";

const router = Router();

router.get("/search", async (req, res) => {
  try {
    const city = String(req.query.city || "").trim();

    if (!city) {
      return res.status(400).json({
        message: "The city query parameter is required.",
      });
    }

    const location = await findCity(city);

    if (!location) {
      return res.status(404).json({
        message: "City not found.",
      });
    }

    return res.json({ location });
  } catch (error) {
    return res.status(502).json({
      message: "Unable to search the weather provider.",
      detail: error.message,
    });
  }
});

router.get("/weather", async (req, res) => {
  try {
    const latitude = Number(req.query.latitude);
    const longitude = Number(req.query.longitude);

    if (
      !Number.isFinite(latitude) ||
      !Number.isFinite(longitude) ||
      latitude < -90 ||
      latitude > 90 ||
      longitude < -180 ||
      longitude > 180
    ) {
      return res.status(400).json({
        message: "Valid latitude and longitude are required.",
      });
    }

    const weather = await fetchForecast(latitude, longitude);

    return res.json({ weather });
  } catch (error) {
    return res.status(502).json({
      message: "Unable to retrieve weather data.",
      detail: error.message,
    });
  }
});

router.get("/forecast", async (req, res) => {
  try {
    const city = String(req.query.city || "").trim();

    if (!city) {
      return res.status(400).json({
        message: "The city query parameter is required.",
      });
    }

    const location = await findCity(city);

    if (!location) {
      return res.status(404).json({
        message: "City not found.",
      });
    }

    const weather = await fetchForecast(
      location.latitude,
      location.longitude
    );

    return res.json({ location, weather });
  } catch (error) {
    return res.status(502).json({
      message: "Unable to retrieve the forecast.",
      detail: error.message,
    });
  }
});

export default router;
```

## 22.8 Create server.js with Swagger UI

```javascript
import express from "express";
import cors from "cors";
import dotenv from "dotenv";
import swaggerUi from "swagger-ui-express";
import swaggerJsdoc from "swagger-jsdoc";
import weatherRoutes from "./routes/weatherRoutes.js";

dotenv.config();

const app = express();
const PORT = process.env.PORT || 5000;

app.use(
  cors({
    origin: process.env.CLIENT_ORIGIN || "http://localhost:5173",
  })
);

app.use(express.json());

const swaggerOptions = {
  definition: {
    openapi: "3.0.3",
    info: {
      title: "SkyCast Backend API",
      version: "1.0.0",
      description: "Weather search and forecast API for the SkyCast learning project.",
    },
    servers: [
      {
        url: `http://localhost:${PORT}`,
      },
    ],
  },
  apis: ["./routes/*.js"],
};

const swaggerSpec = swaggerJsdoc(swaggerOptions);

app.get("/", (req, res) => {
  res.json({
    message: "SkyCast API is running",
    documentation: "/api-docs",
  });
});

app.use("/api", weatherRoutes);
app.use("/api-docs", swaggerUi.serve, swaggerUi.setup(swaggerSpec));

app.use((req, res) => {
  res.status(404).json({ message: "Route not found." });
});

app.listen(PORT, () => {
  console.log(`SkyCast backend running at http://localhost:${PORT}`);
  console.log(`Swagger UI at http://localhost:${PORT}/api-docs`);
});
```

## 22.9 Add OpenAPI route documentation

To make `swagger-jsdoc` discover endpoint documentation, add JSDoc blocks immediately above each route in `routes/weatherRoutes.js`. For example, add this immediately above `router.get("/search", ...)`:

```javascript
/**
 * @openapi
 * /api/search:
 *   get:
 *     summary: Search for a city
 *     tags:
 *       - Weather
 *     parameters:
 *       - in: query
 *         name: city
 *         required: true
 *         schema:
 *           type: string
 *         example: Pune
 *     responses:
 *       "200":
 *         description: Matching city returned.
 *       "400":
 *         description: City parameter is missing.
 *       "404":
 *         description: City not found.
 *       "502":
 *         description: Weather provider request failed.
 */
```

Add these blocks above the other two routes as well.

For `GET /api/weather`, document required query parameters `latitude` and `longitude`, both numbers, and responses 200, 400, and 502.

For `GET /api/forecast`, document required query parameter `city` (string), and responses 200, 400, 404, and 502.

The route documentation must be inside the same file path matched by `apis: ["./routes/*.js"]`.

## 22.10 Start and test the backend

From `skycast-backend`:

```bash
npm run dev
```

Open:

```text
http://localhost:5000/
http://localhost:5000/api-docs
```

Test these URLs in a browser:

```text
http://localhost:5000/api/search?city=Pune
http://localhost:5000/api/forecast?city=Pune
http://localhost:5000/api/weather?latitude=18.5204&longitude=73.8567
```

Expected behavior:

- `/api/search` returns the matching location.
- `/api/forecast` returns the location and forecast.
- `/api/weather` returns the forecast for supplied coordinates.
- Missing or invalid parameters return HTTP 400.
- Unknown city returns HTTP 404.
- Provider failures return HTTP 502.

# 23. Connect React to your own backend (optional exercise)

Once the backend works, you can replace the frontend's direct Open-Meteo calls with your backend.

For a simple city forecast, the frontend can call:

```javascript
export async function getBackendForecast(city) {
  const params = new URLSearchParams({ city });

  const response = await fetch(
    `http://localhost:5000/api/forecast?${params}`
  );

  if (!response.ok) {
    const errorData = await response.json().catch(() => ({}));
    throw new Error(errorData.message || `Backend error: ${response.status}`);
  }

  return response.json();
}
```

This returns `{ location, weather }`. Adapt the React search handler to use those properties instead of separately calling `searchCity()` and `getWeather()`.

Do not switch to this version until the direct Open-Meteo frontend is working. Keep one integration approach at a time while learning.

# 24. Debugging: use browser DevTools

1. Open the app in Chrome.
2. Press `F12` or right-click → Inspect.
3. Open the **Network** tab.
4. Select **Fetch/XHR**.
5. Search for a city.
6. Select the request.
7. Inspect:
   - Request URL
   - Request method
   - Status code
   - Response headers
   - Response JSON
   - Timing

Also inspect the **Console** tab for JavaScript errors.

Common issues:

| Symptom | Likely cause | What to do |
|---|---|---|
| `node` not recognized | Node PATH/terminal issue | Reopen terminal or repair Node installation |
| `npm` not recognized | npm not installed or PATH issue | Reinstall Node LTS |
| Vite page does not open | Server not running | Run `npm run dev` |
| `Failed to fetch` | Network, CORS, DNS, or endpoint issue | Inspect Network tab and test URL directly |
| HTTP 400 | Invalid query parameters | Check spelling and query values |
| HTTP 404 | Wrong endpoint or city not found | Check URL and response |
| HTTP 429 | Request limit reached | Reduce repeated requests and respect provider terms |
| Blank React page | Runtime or import error | Read browser Console |
| `Cannot read properties of undefined` | Accessing data before it exists or wrong JSON path | Check response JSON and conditional rendering |
| Location permission denied | Browser permission blocked | Allow location or search manually |
| Swagger Try it out fails | Browser CORS or server limitation | Test with browser/Thunder Client and inspect response |

# 25. Production build

When the app works:

```bash
npm run build
```

Vite creates a `dist` folder. Test the production build locally:

```bash
npm run preview
```

Open the local preview URL printed by Vite.

If the build fails, fix all errors before deployment.

# 26. Upload the frontend to GitHub

Create a new empty repository on https://github.com/ named `skycast-weather`.

In the frontend project root:

```bash
git init
git add .
git commit -m "Build SkyCast weather application"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/skycast-weather.git
git push -u origin main
```

Replace `YOUR_USERNAME` with your GitHub username and use the repository URL GitHub gives you.

If Git says `remote origin already exists`, inspect it:

```bash
git remote -v
```

Then update it if necessary:

```bash
git remote set-url origin https://github.com/YOUR_USERNAME/skycast-weather.git
```

Do not commit `node_modules`. Vite's standard `.gitignore` should exclude it. Add `.env` to `.gitignore` if you later introduce environment variables.

# 27. Deploy the frontend

You can use Vercel:

1. Open https://vercel.com/
2. Sign in using GitHub.
3. Import the `skycast-weather` repository.
4. Confirm the framework is Vite.
5. Build command: `npm run build`.
6. Output directory: `dist`.
7. Deploy.
8. Open the deployed URL and test city search, forecast, responsive layout, and geolocation.

For the frontend-only version, no backend environment variable is required because it calls Open-Meteo directly.

If you deploy the optional Express backend, deploy it separately and configure its production `CLIENT_ORIGIN` to your deployed frontend origin. Update the frontend backend URL to the deployed backend URL. Do not leave `localhost` URLs in a deployed frontend.

# 28. Final practical checklist

## Beginner

- [ ] Install Node.js and VS Code.
- [ ] Verify `node -v` and `npm -v`.
- [ ] Create the Vite React project.
- [ ] Run the Vite server.
- [ ] Understand `main.jsx` and `App.jsx`.
- [ ] Create a reusable component.
- [ ] Pass props.
- [ ] Use `useState`.
- [ ] Build a controlled input.
- [ ] Render an array with `map()`.

## API integration

- [ ] Test the Geocoding endpoint.
- [ ] Test the Forecast endpoint.
- [ ] Read a JSON response.
- [ ] Understand `fetch()`.
- [ ] Understand `async` and `await`.
- [ ] Check `response.ok`.
- [ ] Handle errors with `try/catch`.
- [ ] Create `weatherService.js`.
- [ ] Search a city and get coordinates.
- [ ] Request weather using coordinates.

## React application

- [ ] Create the SearchBar.
- [ ] Create the CurrentWeather card.
- [ ] Create the WeatherDetails cards.
- [ ] Create the HourlyForecast.
- [ ] Create the DailyForecast.
- [ ] Add loading and error states.
- [ ] Add Celsius/Fahrenheit.
- [ ] Add current location.
- [ ] Add recent searches.
- [ ] Add responsive CSS.
- [ ] Add weather condition descriptions.
- [ ] Add API attribution.

## Swagger and backend

- [ ] Understand OpenAPI and Swagger UI.
- [ ] Write an OpenAPI YAML document.
- [ ] Validate it in Swagger Editor.
- [ ] Use Try it out or another API client.
- [ ] Create an Express server.
- [ ] Create API routes.
- [ ] Validate query parameters.
- [ ] Add Swagger UI.
- [ ] Test 200, 400, 404, and 502 responses.
- [ ] Optionally connect React to your backend.

## Deployment

- [ ] Run `npm run build`.
- [ ] Run `npm run preview`.
- [ ] Create a GitHub repository.
- [ ] Push the code.
- [ ] Deploy on Vercel.
- [ ] Test the public URL.

# 29. Seven-day learning schedule

| Day | Learn and build |
|---|---|
| 1 | Node, npm, Vite, React setup, JSX, components, props |
| 2 | State, events, forms, conditional rendering, `useEffect` |
| 3 | HTTP, JSON, Fetch, promises, async/await, error handling |
| 4 | Geocoding and forecast API integration |
| 5 | Dashboard components, CSS, hourly and daily forecast |
| 6 | Swagger/OpenAPI and optional Express backend |
| 7 | Debugging, GitHub, production build, deployment |

Spend 2–3 focused hours per day. Type the code yourself rather than pasting everything at once. After each section, explain in your own words what the code does.

# 30. Interview questions

1. What is React?
2. What is JSX?
3. What is a React component?
4. What are props?
5. What is state?
6. What is the difference between props and state?
7. What does `useState` do?
8. What does `useEffect` do?
9. What is a controlled input?
10. What is conditional rendering?
11. What does `map()` do in React?
12. What is an API?
13. What is a third-party API?
14. What is an endpoint?
15. What is JSON?
16. What is HTTP GET?
17. What does `fetch()` do?
18. What is a Promise?
19. What are `async` and `await`?
20. Why should you check `response.ok`?
21. What is the difference between Fetch and Axios?
22. What is CORS?
23. What is geocoding?
24. Why does a weather forecast API need latitude and longitude?
25. What is OpenAPI?
26. What is Swagger UI?
27. What is the difference between Swagger and OpenAPI?
28. What is Express.js?
29. Why might a frontend call its own backend instead of a third-party API directly?
30. What is `AbortController` and why is it useful?

# 31. Official learning references

- React: https://react.dev/learn
- Vite: https://vite.dev/guide/
- Open-Meteo Forecast API: https://open-meteo.com/en/docs
- Open-Meteo Geocoding API: https://open-meteo.com/en/docs/geocoding-api
- MDN Fetch API: https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API
- MDN Geolocation API: https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API
- Swagger: https://swagger.io/docs/
- OpenAPI: https://swagger.io/specification/
- Express: https://expressjs.com/
- Git: https://git-scm.com/doc
- Vercel: https://vercel.com/docs

---

## How to work through this guide

Do not jump directly to the backend. First finish Sections 1–18 and verify the React frontend. Then study Fetch/Axios and Swagger. Build the Express backend only after you understand the frontend API flow. Finally, deploy and test the public application.
