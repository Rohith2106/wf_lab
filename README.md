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

