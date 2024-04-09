1. Create a simple to-do list application where users can add tasks, mark them as completed, and delete them.

```ruby
import React, { useState } from 'react';
import './App.css';

function App() {
  const [tasks, setTasks] = useState([]);
  const [taskInput, setTaskInput] = useState('');

  const handleTaskInputChange = (e) => {
    setTaskInput(e.target.value);
  };

  const handleAddTask = (e) => {
    e.preventDefault();
    if (taskInput.trim() !== '') {
      setTasks([...tasks, taskInput.trim()]);
      setTaskInput('');
    }
  };
  
  const handleDeleteTask = (index) => {
    const updatedTasks = [...tasks];
    updatedTasks.splice(index, 1);
    setTasks(updatedTasks);
  };

  return (
    <div class="container">
    <div className="App">
      <h1>To-Do List</h1>
      <form onSubmit={handleAddTask}>
        <input
          type="text"
          value={taskInput}
          onChange={handleTaskInputChange}
          placeholder="Add a new task"
        />
        <button type="submit">Add Task</button>
      </form>
      <ul>
        {tasks.map((task, index) => (
          <li key={index}>
            <input type="checkbox" />
            <span>{task}</span>
            <button onClick={() => handleDeleteTask(index)}>Delete</button>
          </li>
        ))}
      </ul>
    </div>
    </div>
  );
}

export default App;
```

2. Develop a weather application that fetches weather data from an API based on user input (e.g., city name) and displays the weather forecast.

```ruby
//App.js

import { Oval } from "react-loader-spinner";
import React, { useState } from "react";
import axios from "axios";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faFrown } from "@fortawesome/free-solid-svg-icons";
import "./App.css";

function GfGWeatherApp() {
  const [input, setInput] = useState("");
  const [weather, setWeather] = useState({
    loading: false,
    data: {},
    error: false,
  });

  const toDateFunction = () => {
    const months = [
      "January",
      "February",
      "March",
      "April",
      "May",
      "June",
      "July",
      "August",
      "September",
      "October",
      "November",
      "December",
    ];
    const WeekDays = [
      "Sunday",
      "Monday",
      "Tuesday",
      "Wednesday",
      "Thursday",
      "Friday",
      "Saturday",
    ];
    const currentDate = new Date();
    const date = `${WeekDays[currentDate.getDay()]} ${currentDate.getDate()} ${
      months[currentDate.getMonth()]
    }`;
    return date;
  };

  const search = async (event) => {
    if (event.key === "Enter") {
      event.preventDefault();
      setInput("");
      setWeather({ ...weather, loading: true });
      const url = "https://api.openweathermap.org/data/2.5/weather";
      const api_key = "f00c38e0279b7bc85480c3fe775d518c";
      await axios
        .get(url, {
          params: {
            q: input,
            units: "metric",
            appid: api_key,
          },
        })
        .then((res) => {
          console.log("res", res);
          setWeather({ data: res.data, loading: false, error: false });
        })
        .catch((error) => {
          setWeather({ ...weather, data: {}, error: true });
          setInput("");
          console.log("error", error);
        });
    }
  };

  return (
    <div className="App">
      <h1 className="app-name">Weather App</h1>
      <div className="search-bar">
        <input
          type="text"
          className="city-search"
          placeholder="Enter City Name.."
          name="query"
          value={input}
          onChange={(event) => setInput(event.target.value)}
          onKeyPress={search}
        />
      </div>
      {weather.loading && (
        <>
          <br />
          <br />
          <Oval type="Oval" color="black" height={100} width={100} />
        </>
      )}
      {weather.error && (
        <>
          <br />
          <br />
          <span className="error-message">
            <FontAwesomeIcon icon={faFrown} />
            <span style={{ fontSize: "20px" }}>City not found</span>
          </span>
        </>
      )}
      {weather && weather.data && weather.data.main && (
        <div>
          <div className="city-name">
            <h2>
              {weather.data.name}, <span>{weather.data.sys.country}</span>
            </h2>
          </div>
          <div className="date">
            <span>{toDateFunction()}</span>
          </div>
          <div className="icon-temp">
            <img
              className=""
              src={`https://openweathermap.org/img/wn/${weather.data.weather[0].icon}@2x.png`}
              alt={weather.data.weather[0].description}
            />
            {Math.round(weather.data.main.temp)}
            <sup className="deg">°C</sup>
          </div>
          <div className="des-wind">
            <p>{weather.data.weather[0].description.toUpperCase()}</p>
            <p>Wind Speed: {weather.data.wind.speed}m/s</p>
          </div>
        </div>
      )}
    </div>
  );
}

export default GfGWeatherApp;

```

3. Build a basic calculator that performs arithmetic operations like addition, subtraction, multiplication, and division.


```ruby
import React, { useState } from "react";
import "./App.css";

function App() {
  const [value, setValue] = useState("");

  return (
    <div className="container">
      <div className="calculator">
        <form action="">
          <div className="display">
            <input type="text" value={value} />
          </div>
          <div>
            <input type="button" value="AC" onClick={(e) => setValue("")} />
            <input
              type="button"
              value="DE"
              onClick={(e) => setValue(value.slice(0, -1))}
            />
            <input
              type="button"
              value="."
              onClick={(e) => setValue(value + e.target.value)}
            />
            <input
              type="button"
              value="/"
              onClick={(e) => setValue(value + e.target.value)}
            />
          </div>
          <div>
            <input
              type="button"
              value="7"
              onClick={(e) => setValue(value + e.target.value)}
            />
            <input
              type="button"
              value="8"
              onClick={(e) => setValue(value + e.target.value)}
            />
            <input
              type="button"
              value="9"
              onClick={(e) => setValue(value + e.target.value)}
            />
            <input
              type="button"
              value="*"
              onClick={(e) => setValue(value + e.target.value)}
            />
          </div>
          <div>
            <input
              type="button"
              value="4"
              onClick={(e) => setValue(value + e.target.value)}
            />
            <input
              type="button"
              value="5"
              onClick={(e) => setValue(value + e.target.value)}
            />
            <input
              type="button"
              value="6"
              onClick={(e) => setValue(value + e.target.value)}
            />
            <input
              type="button"
              value="+"
              onClick={(e) => setValue(value + e.target.value)}
            />
          </div>
          <div>
            <input
              type="button"
              value="1"
              onClick={(e) => setValue(value + e.target.value)}
            />
            <input
              type="button"
              value="2"
              onClick={(e) => setValue(value + e.target.value)}
            />
            <input
              type="button"
              value="3"
              onClick={(e) => setValue(value + e.target.value)}
            />
            <input
              type="button"
              value="-"
              onClick={(e) => setValue(value + e.target.value)}
            />
          </div>
          <div>
            <input
              type="button"
              value="00"
              onClick={(e) => setValue(value + e.target.value)}
            />
            <input
              type="button"
              value="0"
              onClick={(e) => setValue(value + e.target.value)}
            />
            <input
              type="button"
              value="="
              className="equal"
              onClick={(e) => setValue(eval(value))}
            />
          </div>
        </form>
      </div>
    </div>
  );
}

export default App;

```

4. Build a Body Mass Index (BMI) calculator where users can input their height and weight to calculate their BMI.

```ruby
//App.js
import React, { useState } from "react";

import "./index.css";

function App() {
  const [weight, setWeight] = useState(0);
  const [height, setHeight] = useState(0);
  const [bmi, setBmi] = useState("");
  const [message, setMessage] = useState("");

  let calcBmi = (event) => {
    event.preventDefault();

    if (weight === 0 || height === 0) {
      alert("Please enter a valid weight and height");
    } else {
      let bmi = weight / (height * height);
      setBmi(bmi.toFixed(1));

      if (bmi < 25) {
        setMessage("You are underweight");
      } else if (bmi >= 25 && bmi < 30) {
        setMessage("You are a healthy weight");
      } else {
        setMessage("You are overweight");
      }
    }
  };

  let reload = () => {
    window.location.reload();
  };

  return (
    <div className="app">
      <div className="container">
        <h2 className="center">BMI Calculator</h2>
        <form onSubmit={calcBmi}>
          <div>
            <label>Weight (Kgs)</label>
            <input value={weight} onChange={(e) => setWeight(e.target.value)} />
          </div>
          <div>
            <label>Height (m)</label>
            <input
              value={height}
              onChange={(event) => setHeight(event.target.value)}
            />
          </div>
          <div>
            <button className="btn" type="submit">
              Submit
            </button>
            <button className="btn btn-outline" onClick={reload} type="submit">
              Reload
            </button>
          </div>
        </form>

        <div className="center">
          <h3>Your BMI is: {bmi}</h3>
          <p>{message}</p>
        </div>
      </div>
    </div>
  );
}

export default App;
```

5. Develop an application that fetches recipes from an API based on user input (e.g., ingredients) and displays them.

```ruby
// App.js

import React, { useEffect, useState } from "react";
import RecipeCard from "./RecipeCard";

const App = () => {
  const APP_ID = "cd174776";
  const APP_KEY = "d156b26a7d0b33cbf26cce97ce6d8463";
  const [food_recipes, setfood_recipes] = useState([]);
  const [search_recipe, setSearch_recipe] = useState("");
  const [search_query, setSearch_Query] = useState("chicken");

  useEffect(() => {
    getRecipesFunction();
  }, [search_query]);

  const getRecipesFunction = async () => {
    const response = await fetch(
      `https://api.edamam.com/search?q=${search_query}&app_id=${APP_ID}&app_key=${APP_KEY}`
    );
    const data = await response.json();
    setfood_recipes(data.hits);
  };

  const updateSearchFunction = (e) => {
    setSearch_recipe(e.target.value);
  };

  const getSearchFunction = (e) => {
    e.preventDefault();
    setSearch_Query(search_recipe);
    setSearch_recipe("");
  };

  return (
    <div className="bg-blue-50 min-h-screen font-sans">
      <header className="bg-blue-500 py-4 text-white">
        <div className="container mx-auto text-center">
          <h1
            className="text-3xl sm:text-4xl 
								md:text-5xl lg:text-6xl 
								font-extrabold tracking-tight"
          >
            <span className="block">Recipe Finder</span>
          </h1>
        </div>
      </header>
      <div
        className="container mx-auto mt-8 p-4 
							sm:px-6 lg:px-8"
      >
        <form
          onSubmit={getSearchFunction}
          className="bg-white p-4 sm:p-6 
							lg:p-8 rounded-lg shadow-md 
							flex flex-col sm:flex-row items-center 
							justify-center space-y-4 sm:space-y-0 
							sm:space-x-4"
        >
          <div
            className="relative justify-center flex-grow 
									w-full sm:w-1/2"
          >
            <input
              type="text"
              name="search"
              value={search_recipe}
              onChange={updateSearchFunction}
              placeholder="Search for recipes..."
              className="w-full py-3 px-4 bg-gray-100 
									border border-blue-300 focus:ring-blue-500 
									focus:border-blue-500 rounded-full 
									text-gray-700 outline-none transition-colors 
									duration-200 ease-in-out focus:ring-2 
									focus:ring-blue-900 focus:bg-transparent 
									focus:shadow-md"
            />
          </div>
          <button
            type="submit"
            className="bg-blue-500 hover:bg-blue-600 focus:ring-2 
						focus:ring-blue-900 text-white font-semibold py-3 px-6 
						rounded-full transform hover:scale-105 transition-transform 
						focus:outline-none focus:ring-offset-2 
						focus:ring-offset-blue-700"
          >
            Search Recipe
          </button>
        </form>
      </div>

      <div className="container mx-auto mt-8 p-4 sm:px-6 lg:px-8">
        <div
          className="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 
				lg:grid-cols-4 gap-4"
        >
          {food_recipes.map((recipe) => (
            <RecipeCard key={recipe.recipe.label} recipe={recipe.recipe} />
          ))}
        </div>
      </div>
    </div>
  );
};

export default App;

```

6. Develop an expense tracking app where users can input their expenses, categorize them, and view a summary of their spending.

```ruby
// FileName: Tracker.js 

import React, { useEffect, useState } from "react"; 
import styled from "styled-components"; 
import AddTransaction from "./AddTransaction"; 
import OverviewComponent from "./OverviewComponent"; 
import TransactionsContainer from "./TransactionsContainer"; 

const Container = styled.div` 
display: flex; 
flex-direction: column; 
width: 600px; 
max-width: 100%; 
background-color: #fff; 
padding: 30px 20px; 
border: 1px solid #000; 
border-radius: 5px; 
margin: 10px; 
`; 

const Heading = styled.h1` 
font-size: 30px; 
font-weight: bold; 
text-align: center; 
margin-bottom: 20px; 
`; 

const TransactionDetails = styled.div` 
display: flex; 
justify-content: space-between; 
align-items: center; 
gap: 20px; 
margin-bottom: 25px; 
`; 

const THeading = styled.div` 
font-size: 30px; 
font-weight: bold; 
text-align: center; 
margin-bottom: 20px; 
color: #44E610; 
`; 

const ExpenseBox = styled.div` 
flex: 1; 
border: 1px solid #000; 
border-radius: 5px; 
padding: 10px 20px; 
background-color: #fff; 
& span { 
	font-weight: bold; 
	font-size: 25px; 
	display: block; 
	color: ${(props) => (props.isExpense ? "red" : "green")}; 
} 
`; 

const IncomeBox = styled(ExpenseBox)``; 

const Tracker = () => { 
const [toggle, setToggle] = useState(false); 
const [transactions, setTransactions] = useState([]); 
const [expense, setExpense] = useState(0); 
const [income, setIncome] = useState(0); 

const AddTransactions = (payload) => { 
	const transactionArray = [...transactions]; 
	transactionArray.push(payload); 
	setTransactions(transactionArray); 
}; 

const removeTransaction = (id) => { 
	const updatedTransactions = transactions 
								.filter((transaction) => transaction.id !== id); 
	setTransactions(updatedTransactions); 
}; 

const calculateTransactions = () => { 
	let exp = 0; 
	let inc = 0; 

	transactions.map((item) => { 
	item.transType === "expense"
		? (exp = exp + item.amount) 
		: (inc = inc + item.amount); 
	}); 

	setExpense(exp); 
	setIncome(inc); 
}; 

useEffect(() => { 
	calculateTransactions(); 
}, [transactions]); 

return ( 
	<Container> 
		<THeading>GeeksforGeeks</THeading> 
	<Heading>Expense Tracker</Heading> 
	<OverviewComponent 
		toggle={toggle} 
		setToggle={setToggle} 
		expense={expense} 
		income={income} 
	/> 

	{toggle && ( 
		<AddTransaction 
		setToggle={setToggle} 
		AddTransactions={AddTransactions} 
		/> 
	)} 

	<TransactionDetails> 
		<ExpenseBox isExpense> 
		Expense <span>₹{expense}</span> 
		</ExpenseBox> 

		<IncomeBox> 
		Budget <span>₹{income}</span> 
		</IncomeBox> 
	</TransactionDetails> 

	<TransactionsContainer 
		transactions={transactions} 
		removeTransaction={removeTransaction} 
	/> 
	</Container> 
); 
}; 

export default Tracker; 
```
7. Develop a quiz application with multiple-choice questions on various topics, with a score tracker at the end.

```ruby
// Quiz.js
import React, { useState } from 'react';
import quizData from './quizData';

const Quiz = () => {
  const [currentQuestion, setCurrentQuestion] = useState(0);
  const [score, setScore] = useState(0);
  const [showScore, setShowScore] = useState(false);

  const handleAnswerOptionClick = (selectedOption) => {
    if (selectedOption === quizData[currentQuestion].correctAnswer) {
      setScore(score + 1);
    }

    const nextQuestion = currentQuestion + 1;
    if (nextQuestion < quizData.length) {
      setCurrentQuestion(nextQuestion);
    } else {
      setShowScore(true);
    }
  };

  return (
    <div className="quiz">
      {showScore ? (
        <div className="score-section">
          <p>You scored {score} out of {quizData.length}.</p>
        </div>
      ) : (
        <>
          <div className="question-section">
            <div className="question-count">
              <span>Question {currentQuestion + 1}</span>/{quizData.length}
            </div>
            <div className="question-text">
              {quizData[currentQuestion].question}
            </div>
          </div>
          <div className="answer-section">
            {quizData[currentQuestion].options.map((option) => (
              <button key={option} onClick={() => handleAnswerOptionClick(option)}>
                {option}
              </button>
            ))}
          </div>
        </>
      )}
    </div>
  );
};

export default Quiz;

```

8. Develop an app that generates random numbers within a specified range and displays them to the user.

```ruby
import React, { useState } from "react";
import "./App.css";
const App = () => {
	const [num, setNum] = useState(0);

	const randomNumberInRange = (min, max) => {
		return Math.floor(Math.random()
			* (max - min + 1)) + min;
	};

	const handleClick = () => {
		setNum(randomNumberInRange(1, 20));
	};

	return (
		<div className="wrapper">
			<h2>Number is: {num}</h2>
			<button onClick={handleClick}>
				Click Me Generate
			</button>
		</div>
	);
};

export default App;
```

9. Create a tool that counts the number of characters in a given text input by the user.

```ruby
import React, { useState } from "react";
import "./App.css";

function CharacterCounter() {
  const [text, setText] = useState("");
  const [characterCount, setCharacterCount] = useState(0);

  const handleInputChange = (event) => {
    setText(event.target.value);
    setCharacterCount(event.target.value.length);
  };

  return (
    <div className="App">
      <input type="text" value={text} onChange={handleInputChange} />
      <p>Character count: {characterCount}</p>
    </div>
  );
}

export default CharacterCounter;
```


10. Develop a simple password generator that creates random passwords.

```ruby
// App.js
import React, { useState } from "react";

const containerStyle = {
  maxWidth: "400px",
  margin: "1rem",
  padding: "20px",
  border: "1px solid #ccc",
  borderRadius: "8px",
  boxShadow: "0px 0px 10px 0px grey",
};

const inputContainerStyle = {
  display: "flex",
  alignItems: "center",
  marginBottom: "10px",
};

const labelStyle = {
  flex: "1",
};

const inputStyle = {
  padding: "5px",
  border: "1px solid #ccc",
  borderRadius: "3px",
};

const checkboxContainerStyle = {
  display: "flex",
  alignItems: "center",
  marginBottom: "5px",
};

const buttonStyle = {
  padding: "10px 15px",
  backgroundColor: "#007bff",
  color: "#fff",
  border: "none",
  borderRadius: "5px",
  cursor: "pointer",
  transition: "background-color 0.2s ease-in-out",
};

const copyButtonStyle = {
  marginLeft: "10px",
};

const App = () => {
  const [password, setPassword] = useState("");
  const [passwordLength, setPasswordLength] = useState(12);
  const [useSymbols, setUseSymbols] = useState(true);
  const [useNumbers, setUseNumbers] = useState(true);
  const [useLowerCase, setUseLowerCase] = useState(true);
  const [useUpperCase, setUseUpperCase] = useState(true);
  const [successMessage, setSuccessMessage] = useState("");

  const generatePassword = () => {
    let charset = "";
    let newPassword = "";

    if (useSymbols) charset += "!@#$%^&*()";
    if (useNumbers) charset += "0123456789";
    if (useLowerCase) charset += "abcdefghijklmnopqrstuvwxyz";
    if (useUpperCase) charset += "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

    for (let i = 0; i < passwordLength; i++) {
      newPassword += charset.charAt(Math.floor(Math.random() * charset.length));
    }

    setPassword(newPassword);
  };

  const copyToClipboard = () => {
    const el = document.createElement("textarea");
    el.value = password;
    document.body.appendChild(el);
    el.select();
    document.execCommand("copy");
    document.body.removeChild(el);
    setSuccessMessage("Password copied to clipboard!");
    setTimeout(() => setSuccessMessage(""), 2000);
    // Hide message after 2 seconds
  };

  return (
    <div style={containerStyle}>
      <h1
        style={{
          color: "green",
          textAlign: "center",
        }}
      >
        Geeksforgeeks
      </h1>
      <h3 style={{ textAlign: "center" }}>Random Password Generator</h3>
      <div style={inputContainerStyle}>
        <label style={labelStyle}>Password Length:</label>
        <input
          type="number"
          min="8"
          max="32"
          value={passwordLength}
          onChange={(e) => setPasswordLength(e.target.value)}
          style={inputStyle}
        />
      </div>
      <div style={checkboxContainerStyle}>
        <label>
          <input
            type="checkbox"
            checked={useSymbols}
            onChange={() => setUseSymbols(!useSymbols)}
          />
          Symbols
        </label>
        <label>
          <input
            type="checkbox"
            checked={useNumbers}
            onChange={() => setUseNumbers(!useNumbers)}
          />
          Numbers
        </label>
        <label>
          <input
            type="checkbox"
            checked={useLowerCase}
            onChange={() => setUseLowerCase(!useLowerCase)}
          />
          LowerCase
        </label>
        <label>
          <input
            type="checkbox"
            checked={useUpperCase}
            onChange={() => setUseUpperCase(!useUpperCase)}
          />
          UpperCase
        </label>
      </div>
      <button style={buttonStyle} onClick={generatePassword}>
        Generate Password
      </button>
      {password && (
        <div style={inputContainerStyle}>
          <label style={labelStyle}>Generated Password:</label>
          <input type="text" value={password} readOnly style={inputStyle} />
          <button
            style={{
              ...buttonStyle,
              ...copyButtonStyle,
            }}
            onClick={copyToClipboard}
          >
            Copy
          </button>
        </div>
      )}
      {successMessage && (
        <p
          style={{
            color: "green",
            textAlign: "center",
          }}
        >
          {successMessage}
        </p>
      )}
    </div>
  );
};

export default App;
```

11. Build a simple location tracker application that utilizes the browser's geolocation API to display the user's current location on a map.

```ruby
import React, { useState, useEffect } from 'react';
import { MapContainer, TileLayer, Marker, Popup } from 'react-leaflet';
import L from 'leaflet'; // Import Leaflet library
import 'leaflet/dist/leaflet.css';

// Import custom pointer image
import pointerImg from './pointer.png';

function App() {
  const [location, setLocation] = useState({ lat: 0, lng: 0 });

  useEffect(() => {
    navigator.geolocation.getCurrentPosition(
      (position) => {
        setLocation({
          lat: position.coords.latitude,
          lng: position.coords.longitude,
        });
      },
      (error) => alert(`Error accessing your location: ${error.message}`)
    );
  }, []);

  // Create a custom pointer icon using the custom image
  const pointerIcon = new L.Icon({
    iconUrl: pointerImg,
    iconSize: [32, 32],
    iconAnchor: [16, 32],
  });

  return (
    <div className="App">
      <h1>Location Tracker</h1>
      <MapContainer
        center={[location.lat, location.lng]}
        zoom={13}
        style={{ height: '800px', width: '100%' }}
      >
        <TileLayer url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png" />
        <Marker position={[location.lat, location.lng]} icon={pointerIcon}>
          <Popup>Your Location</Popup>
        </Marker>
      </MapContainer>
    </div>
  );
}

export default App;

```

12. Build a currency converter application that fetches exchange rates from an API and allows users to convert between different currencies

```ruby
// App.js
import { useEffect, useState } from 'react';
import Axios from 'axios';
import Dropdown from 'react-dropdown';
import { HiSwitchHorizontal } from 'react-icons/hi';
import 'react-dropdown/style.css';
import './App.css';

function App() {

	// Initializing all the state variables 
	const [info, setInfo] = useState([]);
	const [input, setInput] = useState(0);
	const [from, setFrom] = useState("usd");
	const [to, setTo] = useState("inr");
	const [options, setOptions] = useState([]);
	const [output, setOutput] = useState(0);

	// Calling the api whenever the dependency changes
	useEffect(() => {
		Axios.get(
`https://cdn.jsdelivr.net/gh/fawazahmed0/currency-api@1/latest/currencies/${from}.json`)
			.then((res) => {
				setInfo(res.data[from]);
			})
	}, [from]);

	// Calling the convert function whenever
	// a user switches the currency
	useEffect(() => {
		setOptions(Object.keys(info));
		convert();
	}, [info])

	// Function to convert the currency
	function convert() {
		var rate = info[to];
		setOutput(input * rate);
	}

	// Function to switch between two currency
	function flip() {
		var temp = from;
		setFrom(to);
		setTo(temp);
	}

	return (
		<div className="App">
			<div className="heading">
				<h1>Currency converter</h1>
			</div>
			<div className="container">
				<div className="left">
					<h3>Amount</h3>
					<input type="text"
						placeholder="Enter the amount"
						onChange={(e) => setInput(e.target.value)} />
				</div>
				<div className="middle">
					<h3>From</h3>
					<Dropdown options={options}
						onChange={(e) => { setFrom(e.value) }}
						value={from} placeholder="From" />
				</div>
				<div className="switch">
					<HiSwitchHorizontal size="30px"
						onClick={() => { flip() }} />
				</div>
				<div className="right">
					<h3>To</h3>
					<Dropdown options={options}
						onChange={(e) => { setTo(e.value) }}
						value={to} placeholder="To" />
				</div>
			</div>
			<div className="result">
				<button onClick={() => { convert() }}>Convert</button>
				<h2>Converted Amount:</h2>
				<p>{input + " " + from + " = " + output.toFixed(2) + " " + to}</p>

			</div>
		</div>
	);
}

export default App;

```
