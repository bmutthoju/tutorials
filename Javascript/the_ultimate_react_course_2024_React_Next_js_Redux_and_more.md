# The Ultimate React Course 2024: React, Next.js, Redux & More #
## Section 1: Welcome, Welcome, Welcome! ##
### Course Roadmap and Projects ###
1. We can build any application we can imagine
2. We can become a skilled React developer
3. Overview
	1. Part 01: Fundamentals
		1. Components
		2. JSX
		3. Props
		4. State
		5. Forms
	2. Part 02: Intermediate
		1. Data fetching
		2. useEffect hook
		3. Custom hooks
		4. How React works behind the scenes
	3. Part 03: Advanced
		1. Reducers
		2. Performance optimization
		3. SPA
			1. React router
		4. Redux
		5. Modern Redux toolkit
	4. Part 04: Professional Dev
		1. Two professional applications
			1. Industry standard libraries and tools
				1. Redux
				2. Tailwind
				3. React Query
				4. Supabase
				5. ...

### Building Our First React App! ###
1. Small React App (tiny app)
	1. Fundamental ingredients that all React apps are built upon
2. We don't need a development environment
	1. [codesandbox.io](codesandbox.io)
	2. [react.new](react.new)
		1. A new app is created in [coesandbox.io](coesandbox.io)
3. Code:

		import { useEffect, useState } from "react";

		export default function App() {
		  const [advice, setAdvice] = useState(""); // returns an array
		  const [count, setCount] = useState(0);
		  // [value, setterFunction]
		  // setterFunction - used to update the state
		
		  async function getAdvice() {
		    const res = await fetch("https://api.adviceslip.com/advice");
		    const data = await res.json();
		    console.log(data);
		    setAdvice(data.slip.advice);
		    setCount((c) => c + 1);
		  }
		
		  useEffect(function () {
		    getAdvice();
		  }, []);
		  // Function that we want to get executed at the beginning (when the component is loaded)
		  // [] - dependency array
		
		  return (
		    <div>
		      <h1>Alhamdulillah!</h1>
		      <h2>{advice}</h2>
		      <button onClick={getAdvice}>Get advice</button>
		      <Message count={count} />
		    </div>
		  );
		}
		
		function Message(props) {
		  // Uppercase is convention for component
		  return (
		    <p>
		      You have read <strong>{props.count}</strong> pieces of advice
		    </p>
		  );
		}

### Watch Before You Start! ###
1. Some quick considerations before we start...
	1. This course is for everyone! So please don't write a bad review.
	2. To make the course perfect for YOU: rewatch lectures, jumpt to other sections, watch the source with slower or faster speed, or ask questions
2. Don't have to watch the entire course
3. Don't worry about best-practices
4. Make sure to understand the earlier sections before moving to the subsequent sections
	1. Review the notes
	2. Review the code
	3. Review the project
	4. Write your own code for practice
5. Have fun while coding

### Read Before You Start! ###
1. [Starter code](https://github.com/jonasschmedtmann/ultimate-react-course)
2. [Join community](https://discord.gg/uhMkpf4)
3. [Resources page](http://codingheroes.io/resources/)

### Downloading Course Material ###
4. [Starter code](https://github.com/jonasschmedtmann/ultimate-react-course)
	1. Code > Download ZIP

## Section 2: Part 1: REACT FUNDAMENTALS [4 PROJECTS] ##
### Introduction to Part 1 ###
1. Skills
	1. Setting up React Apps
	2. React components
	3. Props
	4. JSX
	5. Handling events
	6. State & State management (to make apps dynamic)

### Useful Resources for Part 1 ###
1. [React Documentation](https://react.dev/?ref=jonas.io)
2. [Create React App](https://create-react-app.dev/?ref=jonas.io)
	1. Setup
3. [Vite: Getting Started](https://vitejs.dev/guide/?ref=jonas.io)
	1. Real-World React apps
4. [Adding React URL to an HTML Document](https://gist.githubusercontent.com/gaearon/0275b1e1518599bbeafcde4722e79ed1/raw/db72dcbf3384ee1708c4a07d3be79860db04bff0/example.html)
	1. Pure React lecture

## Section 3: A First Look at React ##
### Section Overview ###
1. Topics:
	1. Why React?
	2. What is React?
	3. React vs. vanilla JS
	4. Setting up new React apps
		1. Options for creation
			1. CreateReactApp

### Why Do Front-End Frameworks Exist? ###
1. Why not use vanilla JS?

#### The Rise of Single-Page Applications ####
1. Before 2010:
	1. Server-side rendering (the old way (but now getting modern again))
		1. View (template) + Data -> Render Webpage
			1. Browser takes the page and paints it on the screen
		2. Example:
			1. Wordpress
				1. JS - only to add simple dynamics to the page (simple animations, hover effects, ...)
					1. jQuery was used for this
						1. Makes JS work the same way across all browsers
	2. Developers started writing more and more JS code, which led to the rise of Single-Page web-applications
		1. Single-Page Web-Applications: Rendered in the browser (not on the server)
			1. Client-Side rendering:
				1. Browser + View -> Render Webpage -> Browser
			2. They are called web-applications
				1. If web-applications need data, it comes from server APIs
					1. Application consumes API data and renders the screen for each view of the application
			3. SPAs makes us feel like we were using a native desktop or phone applications
				1. We can click on links and submit forms without the page reloading
					1. Technically we are on the same page
2. Server-side rendering is making a comeback
	1. Frameworks built on top of modern client-side rendering frameworks
		1. Next.js
		2. Remix
		3. ...

#### Single-Page Applications with Vanilla Javascript? ####
1. There are many problems with using vanilla JS to build large-scale applications
2. Front-end web applications are about:
	1. **Handling** data + **displaying** data in a user interface
		1. Recieves data
		2. Changes data (as user uses the app)
		3. Displays the current data on the screen
	2. User interface needs to **stay in sync** with data

			DATA <-> UI

		1. UI must always display the current state of the data
			1. **Very hard problem** to solve!
				1. Example: Airbnb
					1. Search bar
					2. Filters
					3. Search as we move the map
				2. Example: If we change location or date, list of apartments needs to be updated
					1. Map must also be updated
					2. When map is moved (assuming user has selected this option), the list of apartments needs to be updated
		2. Piece of data = Piec of state
			1. Keeping UI and data in sync would be **virtually impossible with just vanilla JS**
				1. Why?
					1. Problems with JS and jQuery
						1. Requires lots of direct DOM manipulation and traversing (imperative) "Spaghetti code"
							1. We might end up with a huge mess
						2. Data (state) is usually stored in the DOM (in HTML elements), shared across entire app - Hard to reason + bugs
							1. Many parts of the app can access and modify DOM state directly (may introduce many bugs)
					2. If we handle the above problems, we might end up constructing our own framework
						1. It is better to use a well-established, and battle tested framework instead

#### Why do Front-End Frameworks Exist? ####
1. JavaScript front-end frameworks exist because...
	1. Keeping a user interface in sync with data is **really hard** and a **lot of work**
	2. Front-end frameworks **solve this problem** and take hard work away from developers
		1. Users can only focus on data & building UIs
			1. Different frameworks have different approaches
				1. They are similar in keeping the UI and data in sync
2. They enforce a "correct" way of structuring and writing code (therefore contributing to solving the problem of "spaghetti code")
	1. Other developers can follow the conventions
3. They give developers and teams a **consistent** way of building front-end applications
	1. Everyone on the team will build their part of the app in the exact same style as everyone else
		1. Consistent code-base & product
 
### React vs. Vanilla JavaScript ###
1. Comparison of an application
	1. React: (more automatic)
		1. Even HTML is done in JS (inside JS)
		2. No manual selection of elements
		3. We attach event-listeners using attributes
		4. As soon as we update the state, the UI is automatically kept in sync
	2. Vanilla JavaScript: (more manual)
		1. HTML is in charge
			1. JS is inside HTML
		2. We need to manually select elements in JS
			1. No class required
		3. We need to attach event-listeners manually in JS
		4. Updating state will not automatically update UI
			1. UI needs to be updated manually

### What is React? ###
#### What is React? ####
1. It is a JavaScript library for building UIs
2. **Extremely popular**, **declarative**, **component-based**, **state-driven** JavaScript **library for building user interfaces**, constructed by Facebook
	1. Based on components
		1. Buttons, input-fields, search-bars, ...
		2. They are the building-blocks of UIs in React
		3. React takes the components and draws them on a webpage
		4. We build complex UI by building components and combining components like lego pieces
			1. Example:
				1. Navbar
				2. Results pannel
				3. Map
				4. Search bar
		5. We also re-use components
			1. Multiple elements on the page can look similar
				1. Example: Listing component can be defined once and re-used multiple times on the page by adjusting data
	2. Declarative
		1. Each component must have all the information about what it looks like
			1. Solution: We **describe** how components look like and how they work using a **declarative syntax called JSX**
				1. **Declarative**: Telling React what a component should look like, **based on current data/state**
		2. React is **abstraction** away from DOM: we **never touch the DOM** (directly, as with vanilla JS)
			1. We tell react what we want to do when data changes but not how to do it
		3. JSX:
			1. A syntax that **combines** HTML, CSS, JavaScript as well as referencing **other React components**
	3. State-driven
		1. How does React update the UI?
			1. Main goal of React is to keep UI in sync with data
				1. The data is called state in React
		2. Example:
			1. **State**: An array of apartments on Airbnb
		3. Based on the initial state, React will render UI with Components we wrote using JSX
		4. Based on an event (button-click say), the state might change (more data might be loaded from an API)
			1. Whenever state changes, we **manually** update the state in the React app
				1. As a result React will **automatically** re-render the UI to reflect the latest state
					1. **React reacts to state changes by re-rendering the UI** (hence it is called React)
	4. JavaScript library
		1. Is React a library or a framework?
			1. It is just a library
				1. **Because React is only the "view" layer**. We need to pick multiple external libraries to build a complete application
					1. Routing
					2. Data-fetching
				2. Solution: Frameworks built on top of React (includes all functionalities that React is missing out-of-the-box)
					1. Next.js
					2. Remix
	5. Extremely popular
		1. Biggest reason
			1. Most used framework so far
		2. Many large companies have adopted React
			1. Smaller companies are following their footsteps
				1. Huge job market with high demand for React developers
					1. Well paying jobs, too
		3. Large and vibrant React developer community
			1. Tutorials
			2. Stackoverflow Q&A
			3. Lot of support given to React developers
		4. Gigantic third-party library ecosystem
			1. Many useful libraries and tools into our React applications 
	6. Constructed by Facebook
		1. React was built in 2011 by Jordan Walke, an engineer working at Facebook at the time
			1. Was first used for news-feed
			2. Then used for chat-app
			3. Instagram
		2. React was open-sourced in 2013, and has since then completely transformed front-end web development
			1. Many modern frameworks were created on top of React
3. Summary:
	1. Rendering components on a Webpage (UI) based on their current state
	2. Keeping the UI in sync with state, by re-rendering (reacting) when state changes
		1. Implemented using:
			1. Virtual DOM
			2. Fibre-tree
			3. One-way data-flow
			4. ...

### Setting Up Our Development Environment ###
1. Download and install VS Code
2. Download and install Google Chrome
3. Download and install Node.js
	1. The tools run on node.js
		1. >= v18 (LTS)
4. VS Code config:
	1. Extensions
		1. ESLint (code linter)
			1. Finds errors or best practices we are violating
		2. Prettier (code formatter)
		3. Color theme: one monokai
		4. material icon theme
	2. Settings:
		1. Auto Save: onFocusChange
		2. default formatter: Prettier - Code formatter
		3. format on save: Check
		4. ESlint run: onSave
	3. Terminal
		1. `node -v`
	4. Snippets
		1. Starter files: 00-setup
			1. snippets.json - open in VSCode
				1. Copy everything
			2. User snippets:
				1. New Global Snippets file (or open existing one)
					1. Paste

### Pure React ###
1. Inside HTML file (no modern tooling)
2. Folder: 01-pure-react
	1. Open it as project folder in VSCode
		1. index.html
			1. ! (enter)
		2. [react.dev](react.dev)
			1. Learn
				1. Installation
					1. Try React locally
						1. download this HTML page
							1. Copy-paste the `<script>`s
								1. `react.development.js` - core React library
									1. Works with components, state, etc. (how to interact with React)
								2. `react-dom.development.js` - Rendering layer which can render the React components into the DOM
									1. React can be rendered in other environments (As Native applications using ReactNative)
2. Code:

		<!DOCTYPE html>
		<html lang="en">
		
		<head>
		  <meta charset="UTF-8">
		  <meta name="viewport" content="width=device-width, initial-scale=1.0">
		  <title>Hello React!</title>
		</head>
		
		<body>
		  <div id="root"></div>
		
		  <script src="https://unpkg.com/react@18/umd/react.development.js"></script>
		  <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
		  <script>
		    function App() {
		      // We cannot use JSX because we don't have the tooling to convert it into JS
		
		      // const time = new Date().toLocaleTimeString();
		      const [time, setTime] = React.useState(new Date().toLocaleTimeString());
		
		      React.useEffect(function () {
		        setInterval(function () {
		          setTime(new Date().toLocaleTimeString());
		        }, 1000);
		      }, [])
		
		      return React.createElement("header", null, `Hello React! It's ${time}`); // `null` - props, `'Hello React!'` is content
		    } // We need to manually reload the page when we make changes
		
		    const root = ReactDOM.createRoot(document.getElementById('root')); // <div id="root"></div> will become the root of the application. Application will be rendered inside the root
		    root.render(React.createElement(App)); // React renders by adding the App component
		  </script>
		</body>
		
		</html>

### A Quick Look at React's Official Documentation ###
1. [react.dev](react.dev)
	1. Learn
		1. Getting started
		2. Installation
		3. Learning React
			1. Fundamentals
		4. **Escape Hatches**
			1. Useful
				1. After the course
	2. Reference
		1. Every function in React
			1. `useState` - more examples, more information
			2. `useLayoutEffect`

### Setting Up a New React Project: The Options ###
1. Options to setup a react project

#### The Two Options for Setting up a React Project ####
1. Create-React-App
	1. Complete "starter kit" for React applications
		1. To make it easy for developers to scaffold new React apps
	2. Everything is **already configured**: ESLit, Prettier, Jest, etc.
		1. Common dev tools are preconfigured
			1. Development server
			2. Webpack (for module bundling)
			3. Dev tools
				1. ESLint
				2. Prettier
				3. Jest (Testing)
				4. Babel (To enable latest JS features)
	3. Problem:
		1. It was developed many years ago.
			1. Uses **slow and outdated** technologies (i.e. webpack)
		2. They stopped innovating
	4. Usecases:
		1. Use for tutorials or experiments
			1. To get started quickly
				1. Used in the course
		2. Don't use for a real-world app
2. Vite (Build tool)
	1. Usecase: Modern real-world apps
	2. **Modern build tool** that contains a starter **template** for setting up React applications
	3. Need to manually set up **ESLint**, Prettier, Testing library, ...
		1. Most painful - Setting up ESLint to play right with React
	4. Why?
		1. Extremely fast hot module replacement (HMR) (fast to automatically refresh the page) and bundling (extremely fast - good for large-scale applications. Page will update almost instantly)

#### What About React Frameworks? ####
1. The React team now advises to use a "React Framework" for new projects (Built on top of React library)
	1. Next.js
		1. Additional features:
			1. Routing
			2. Data-fetching
			3. Server-side rendering
	2. Remix
2. Many people think that this is not the best idea: **"vanilla" React aps are important too**
3. This only makes sense for building actual products, **not for learning React**
	1. We need to learn React itself

### Setting Up a Project With Create-React-App ###
1. Create-React-App - CLI tool
	1. CMD:

			cd <folder>/ultimate-react-course-main
			npx create-react-app@5 pizza-menu

	2. It is a regular npm project (`npm init` could have been used)
		1. package.json
		2. node_modules
			1. react
			2. react-dom
			3. src
				1. Development happens here
			4. public
				1. All assets that will end up in the final application go
					1. Images
					2. index.html
						1. `<div id="root"></div>`
					3. index.js
		3. Starting:

				npm start

		4. Open terminal in VS Code
			1. Run the command
				1. A web-server is started and App is run in that
				2. It has hot-module replacement

## Section 4: [Optional] Review of Essential JavaScript for React ##
### Section Overview ###
### Destructuring Objects and Arrays ###
### Rest/Spread Operator ###
### Template Literals ###
### Ternaries Instead of if/else Statements ###
### Arrow Functions ###
### Short-Circuiting And Logical Operators: &&, ||, ?? ###
### Optional Chaining ###
### The Array map Method ###
### The Array filter Method ###
### The Array reduce Method ###
### The Array sort Method ###
### Working With Immutable Arrays ###
### Asynchronous JavaScript: Promises ###
### Asynchronous JavaScript: Async/Await ###

## Section 5: Working With Components, Props, and JSX ##
### Section Overview ###
1. Three important concepts
	1. Components
		1. Building blocks of React App
	2. Props
		1. To share data
	3. JSX
2. Constructing and reusing components
3. Rendering lists
4. Conditional rendering
5. Start writing code on your own

### Rendering the Root Component and Strict Mode ###
1. `src/index.js`
	1. Why?
		1. Webpack (module bundler) expects entry point to be called `index.js`
2. `react` and `read-dom` - imported
3. `App` - name is a convention
	1. `React.StrictMode` - Good idea to activate it
		1. It renders component twice (to check for bugs) durnig development
		2. Checks if we are using outdated parts of the React API 

### Before We Start Coding: Debugging ###
1. Techniques to deal with errors and problems
	1. If page doesn't update
		1. Ensure the application is running
			1. Stop the app and restart
			2. Reload on the browser (HOT reload breaks sometimes)
		2. Keep the terminal open
		3. Open Console
			1. React Dev tools (later)
		4. React also displays errors on the screen
			1. If we don't understand the error, copy and paste in Google
				1. Stackoverflow
		5. Work with ESLint
			1. Hover to see the error
			2. They appear in Problems tab in VS Code
		6. If prettier stops working:
			1. Go to output tab
			2. Select Prettier (process running in VS Code)
				1. It shows error sometimes
		7. If ESLint stops working:
			1. Go to output tab
			2. Select ESLint
				1. If you see errors, fix them
		8. Compare with working code (final folder)

### Components as Building Blocks ###
#### Components as Building Blocks ####
1. Components:
	1. React applications are entirely made out of components
		1. There is nothing that is not a component or that is inside a component
		2. Components are building-blocks of any UI
			1. React takes components and draws them onto the page
				1. React renders a view for each component, and all the views make up the UI
	2. Piece of UI that has its own **data**, **logic**, and **appearance** (how it works and looks)
	3. We build complex UIs by **building multiple components** and **combining** them
		1. Example:
			1. VideoPlayer
			2. Menu
			3. RefineQuestions
			4. QuestionList
			5. ...
			6. Filters
				1. It is inside RefineQuestions component
			7. Question
				1. It is inside QuestionList component
				2. We can re-use it for multiple questions by passing different data (Props)
					1. Whenever we want duplication in UI, we define a component and re-use it as many times as necessary
	4. Components can be **reused**, **nested** inside each other, and **pass data** between them
		1. Key advantages:
			1. Nestability
			2. Reusability
	5. A crucial skill:
		1. Breaking a UI into components
			1. One thing that helps with that is: Component Tree
				1. Shows the hierarchy that exists between components that make up the UI
					1. Makes it easy to understand how the components are nested inside each other & how they relate to one-another (relationships - parent-child)
						1. Parent component: RefineQuestions
						2. Child component: Filters

### Constructing And Reusing a Component ###
1. 03-pizza-menu
	1. Copy the everything and paste in `public` folder
		1. Move `index.css` to `src` folder
2. create-react-app adds a git repository automatically
	1. Settings
		1. Search: diff decorations
			1. none
3. Code:

		import React from "react";
		import ReactDOM from "react-dom/client";
		
		const pizzaData = [
		  {
		    name: "Focaccia",
		    ingredients: "Bread with italian olive oil and rosemary",
		    price: 6,
		    photoName: "pizzas/focaccia.jpg",
		    soldOut: false,
		  },
		  {
		    name: "Pizza Margherita",
		    ingredients: "Tomato and mozarella",
		    price: 10,
		    photoName: "pizzas/margherita.jpg",
		    soldOut: false,
		  },
		  {
		    name: "Pizza Spinaci",
		    ingredients: "Tomato, mozarella, spinach, and ricotta cheese",
		    price: 12,
		    photoName: "pizzas/spinaci.jpg",
		    soldOut: false,
		  },
		  {
		    name: "Pizza Funghi",
		    ingredients: "Tomato, mozarella, mushrooms, and onion",
		    price: 12,
		    photoName: "pizzas/funghi.jpg",
		    soldOut: false,
		  },
		  {
		    name: "Pizza Salamino",
		    ingredients: "Tomato, mozarella, and pepperoni",
		    price: 15,
		    photoName: "pizzas/salamino.jpg",
		    soldOut: true,
		  },
		  {
		    name: "Pizza Prosciutto",
		    ingredients: "Tomato, mozarella, ham, aragula, and burrata cheese",
		    price: 18,
		    photoName: "pizzas/prosciutto.jpg",
		    soldOut: false,
		  },
		];
		
		function App() {
		  return (
		    <div>
		      <h1>Alhamdulillah!</h1>
		      <Pizza />
		      <Pizza />
		      <Pizza />
		    </div>
		  );
		}
		
		// Two rules:
		// 1: Starts with capital letter
		// 2: returns a markup (exactly one element)
		// 3: Nesting declaration inside another declaration works but it must not be done
		function Pizza() {
		  return (
		    <div>
		      <h2>Pizza Spinaci</h2>
		      <p>Tomato, mozarella, spinach, and ricotta cheese</p>
		      <img src="pizzas/spinaci.jpg" alt="spinaci" />
		    </div>
		  );
		}
		
		// React v18
		const root = ReactDOM.createRoot(document.getElementById("root"));
		root.render(
		  <React.StrictMode>
		    <App />
		  </React.StrictMode>
		);
		
		// React before 18
		// React.render(<App />, document.getElementById("root")); // What to render, where to render

### What is JSX? ###
1. Component
	1. Contains:
		1. Data
		2. Logic
		3. Appearance
2. JSX:
	1. **Declarative** syntax to **describe** what components **look like** and **how they work** (based on their data and logic)
		1. All about component's appearance
	2. Components must **return** a block of JSX
		1. React will use it to render on the UI
	3. Extension of JavaScript that allows us to **embed JavaScript, CSS and React components into HTML**
		1. Embedding of JS - Example: Referencing JS variables using `{}` syntax
		2. We can embed other React components
	4. There is a simple way of converting JSX into JS:

			<header>
				<h1 style="color: red">
					Hello React!
				</h1>
			</header>
		
				|
				|Babel (automatically included in the application)
				|
				v

			React.createElement(
				'header',
				null,
				React.createElement(
					'h1',
					{ style: { color: 'red' } },
					'Hello React!'
				)
			);

		1. Each JSX element is **converted** to a `React.createElement` function call
			1. The function calls construct the HTML on the screen
		2. Conversion is necessary because Browsers understand only HTML, CSS, and JS
		3. We could use React **without JSX**
			1. Hard to read and understand
			2. Hard to write
#### JSX is Declarative ####
1. Imperative (How to do things)
	1. If we use vanilla JS, we use an imperative approach
		1. Manual DOM element selections and DOM traversing
		2. Step-by-step DOM mutations until we reach the desired UI
	2. Doing the above is infeasible for complex apps
2. Declarative
	1. Describe what UI should look like using JSX, **based on current data** (Props and State)
		1. No DOM manipulation at all
			1. No event-listeners
			2. No query-selectors
			3. No classlist
			4. No `textContent` properties
	2. React is an **abstration** away from DOM: **we never touch the DOM**
	3. Instead, we think of the UI as a **reflection of the current data**
		1. React automatically synchronizes with the data
	4. We just tell React using JSX, what we want to see on the screen, but not achieve it step-by-step

### Constructing More Components ###
1. Code:

		function App() {
		  return (
		    <div>
		      <Header />
		      <Menu />
		      <Footer />
		    </div>
		  );
		}
		
		function Header() {
		  return (
		    <div>
		      <h1>Fast React Pizza Co.</h1>
		      <Pizza />
		      <Pizza />
		      <Pizza />
		    </div>
		  );
		}
		
		function Menu() {
		  return <h2>Our menu</h2>;
		}
		
		function Footer() {
		  // return React.createElement("footer", null, "We're currently open");
		  return <footer>{new Date().toLocaleTimeString()} W're currently open</footer>;
		}

### JavaScript Logic in Components ###
1. Components are just JS functions, so any JS code can be executed in the functions
	1. The code is executed as soon as the function is called
		1. As soon as the component is initialized
2. Code:

		function Footer() {
		  const hour = new Date().getHours();
		  // console.log(hour);
		  const openHour = 7;
		  const closeHour = 22;
		  const isOpen = hour >= openHour && hour <= closeHour;
		  console.log(isOpen);
		
		  // if (hour >= openHour && hour <= closeHour) {
		  //   alert("We're currently open");
		  // } else {
		  //   alert("Sorry we're closed");
		  // }
		
		  // return React.createElement("footer", null, "We're currently open");
		  return <footer>{new Date().toLocaleTimeString()} W're currently open</footer>;
		}

### Separation of Concerns ###
1. JSX combines HTML, CSS, and JS, in a single block of code
	1. Why?

#### Separation of Concerns? ####
1. Rise of interactive SPAs
	1. Before SPAs
		1. One file for HTML, CSS, and JS
			1. Traditional separation of concerns
	2. As pages became more interactive, they became SPAs (JS started to determine UI and content)
		1. JavaScript became more in charge of the HTML
			1. HTML and JS are tightly coupled together (HTML doesn't make sense without the JS)
	3. Logic and UI are tightly coupled:
		1. Why keep them separated?
			1. Solution: React Components + JSX
				1. Hence why a React component contains Data, logic, and appearance of one piece of the UI
					1. Everything is mixed together (content & logic are co-located (things that change together))
						1. We have one component per file instead of one technology per file
2. Separation of Concerns:
	1. It is one concern per component (instead of one concern per file)
		1. Each component is **concerned with one piece of the UI**
			1. New paradigm
				1. Having all info about a certain component in one single place

### Styling React Applications ###
1. We have different ways of styling
	1. React doesn't care
		1. It is just a library (it doesn't have a preferred way of styling components, applications)
			1. We can choose many options
				1. Inline styling
					1. We cannot use `""` as in HTML, but we need to pass a JS object using `{}`
						1. We need to enter JS mode to pass a JS object using `{}`
				2. External CSS & SASS
					1. We can include external CSS (like in any other webpage)
					2. They are global styles
				3. CSS Modules
				4. Styled components
				5. Tailwind CSS
2. External CSS Example:

		import React from "react";
		import ReactDOM from "react-dom/client";
		import "./index.css"; // Webpack automatically included styles in our application
		
		const pizzaData = [
		  {
		    name: "Focaccia",
		    ingredients: "Bread with italian olive oil and rosemary",
		    price: 6,
		    photoName: "pizzas/focaccia.jpg",
		    soldOut: false,
		  },
		  {
		    name: "Pizza Margherita",
		    ingredients: "Tomato and mozarella",
		    price: 10,
		    photoName: "pizzas/margherita.jpg",
		    soldOut: false,
		  },
		  {
		    name: "Pizza Spinaci",
		    ingredients: "Tomato, mozarella, spinach, and ricotta cheese",
		    price: 12,
		    photoName: "pizzas/spinaci.jpg",
		    soldOut: false,
		  },
		  {
		    name: "Pizza Funghi",
		    ingredients: "Tomato, mozarella, mushrooms, and onion",
		    price: 12,
		    photoName: "pizzas/funghi.jpg",
		    soldOut: false,
		  },
		  {
		    name: "Pizza Salamino",
		    ingredients: "Tomato, mozarella, and pepperoni",
		    price: 15,
		    photoName: "pizzas/salamino.jpg",
		    soldOut: true,
		  },
		  {
		    name: "Pizza Prosciutto",
		    ingredients: "Tomato, mozarella, ham, aragula, and burrata cheese",
		    price: 18,
		    photoName: "pizzas/prosciutto.jpg",
		    soldOut: false,
		  },
		];
		
		// `class` is a reserved keyword in JS
		function App() {
		  return (
		    <div className="container">
		      <Header />
		      <Menu />
		      <Footer />
		    </div>
		  );
		}
		
		// `style` - also available in HTML
		// In HTML, we don't use it due to separation of concerns
		// In React, it is fine (because all are mixed per component)
		function Header() {
		  // const style = { color: "red", fontSize: "48px", textTransform: "uppercase" };
		  const style = {};
		
		  return (
		    <header className="header">
		      <h1 style={style}>Fast React Pizza Co.</h1>
		    </header>
		  );
		}
		
		function Menu() {
		  return (
		    <main className="menu">
		      <h2>Our menu</h2>
		      <Pizza />
		      <Pizza />
		      <Pizza />
		    </main>
		  );
		}
		
		function Footer() {
		  const hour = new Date().getHours();
		  // console.log(hour);
		  const openHour = 7;
		  const closeHour = 22;
		  const isOpen = hour >= openHour && hour <= closeHour;
		  console.log(isOpen);
		
		  // if (hour >= openHour && hour <= closeHour) {
		  //   alert("We're currently open");
		  // } else {
		  //   alert("Sorry we're closed");
		  // }
		
		  // return React.createElement("footer", null, "We're currently open");
		  return <footer>{new Date().toLocaleTimeString()} W're currently open</footer>;
		}
		
		// Two rules:
		// 1: Starts with capital letter
		// 2: returns a markup (exactly one element)
		// 3: Nesting declaration inside another declaration works but it must not be done
		function Pizza() {
		  return (
		    <div>
		      <img src="pizzas/spinaci.jpg" alt="spinaci" />
		      <h3>Pizza Spinaci</h3>
		      <p>Tomato, mozarella, spinach, and ricotta cheese</p>
		    </div>
		  );
		}
		
		// React v18
		const root = ReactDOM.createRoot(document.getElementById("root"));
		root.render(
		  <React.StrictMode>
		    <App />
		  </React.StrictMode>
		);
		
		// React before 18
		// React.render(<App />, document.getElementById("root")); // What to render, where to render

### Passing and Receiving Props ###
1. Props:
	1. How we pass data between components
		1. In particular, between parent component and child components
	2. It is a communication channel between parent and child component
2. Code:

		function Header() {
		  // const style = { color: "red", fontSize: "48px", textTransform: "uppercase" };
		  const style = {};
		
		  return (
		    <header className="header">
		      <h1 style={style}>Fast React Pizza Co.</h1>
		    </header>
		  );
		}
		
		// We can pass arrays, objects, react components, etc as props
		function Menu() {
		  return (
		    <main className="menu">
		      <h2>Our menu</h2>
		      <Pizza
		        name="Pizza Spinaci"
		        ingredients="Tomato, mozarella, spinach, and ricotta cheese"
		        photoName="pizzas/spinaci.jpg"
		        price={10}
		      />
		
		      <Pizza
		        name="Pizza Funghi"
		        ingredients="Tomato, mushrooms"
		        price={12}
		        photoName="pizzas/funghi.jpg"
		      />
		    </main>
		  );
		}
		
		// Two rules:
		// 1: Starts with capital letter
		// 2: returns a markup (exactly one element)
		// 3: Nesting declaration inside another declaration works but it must not be done
		function Pizza(props) {
		  console.log(props); // {name: 'Pizza Spinacci', ingredients: 'Tomato, ...'}
		
		  return (
		    <div className="pizza">
		      <img src={props.photoName} alt={props.name} />
		      <div>
		        <h3>{props.name}</h3>
		        <p>{props.ingredients}</p>
		        <span>{props.price + 3}</span>
		      </div>
		    </div>
		  );
		}

### Props, Immutability, and One-Way Data Flow ###
#### Reviewing Props ####
1. Props
	1. Props are used to pass data from **parent components** to **child components (down the component tree)**
	2. Props are essential React tool to **configure** and **customize** components (like function parameters)
	3. With props, parent components **control** how child components look and work
		1. They are just like arguments we pass to JS functions
			1. Since we can pass anything to JS functions, we can pass anything to JSX as props
				1. Single values
				2. Arrays
				3. Objects
				4. Functions
				5. **Other components**
				6. ...
		2. Anything can be passed as props

#### Props are Read-Only ####
1. Component:
	1. Data
		1. What is this?
			1. Props + State
				1. Props
					1. Props is data coming from the **outside**, and can **only** be updated by the **parent component** (owner)
						1. It cannot be modified by he child component
					2. Props are read-only, they are **immutable**! This is one of React's strict rules.
						1. Why?
							1. Mutating props would affect parent, causing **side effects** (not pure) (That is how objects work in JS)
								1. If we copy an object and mutate the copy, the original object is mutated
									1. If we change an object outside the component function, the function has caused a side-effect
										1. Whenever we change data that is outside the current function
										2. React is about pure functions (about component's data)
								2. Components have to be **pure functions** in terms of props and state
									1. Allows React to optimize apps, avoid bugs (when we manipulate external data), make apps predictable
										1. **General rule: A component should never mutate it's data outside its function scope**

												let x = 7;

												function Component() {
													x = 23;
													return <h1>Number {x}</h1>
												}

				2. State
					1. State is internal component data that can be updated by the **component's** logic
					2. This is for data that changes over time (mutable)
	2. Logic
	3. Appearance

#### One-Way Data Flow ####
1. In React applications, data can only be passed from parent to child components. (happens by using props)
	1. Never from children to parent
		1. Angular has **two-way** data flow
2. Why?
	1. Makes applications more predictable and easier to understand
		1. Easier to understand where the data is coming from if it flows only in one direction
	2. Makes applications easier to debug, as we have more control over the data
	3. Is more performant
		1. Two-way data-binding is less efficient to implement
3. What if we wanted to pass data to parent component
	1. Later

### CHALLENGE #1: Profile Card (v1) ###
1. Browser: react.new
	1. Uses `create-react-app` under-the-hood
2. Code:

		import "./App.css";

		function App() {
		  return (
		    <div className="card">
		      <Avatar />
		      <div className="data">
		        <Intro />
		        <SkillList />
		      </div>
		    </div>
		  );
		}
		
		function Avatar() {
		  return (
		    <div className="avatar">
		      <img src="avatar_hero.jpg" alt="Avatar Hero" width="100%" />
		    </div>
		  );
		}
		
		function Intro() {
		  return (
		    <div className="intro">
		      <h2>Abdullah Mutthoju</h2>
		      <p>
		        Java Full-stack web developer and architect. When not doing serious
		        work, I like to play with my daughter, travel, and shop.
		      </p>
		    </div>
		  );
		}
		
		function SkillList() {
		  return (
		    <div className="skill-list">
		      <Skill style={{ backgroundColor: "red" }} emoji="⚡" skill="Java" />
		      <Skill style={{ backgroundColor: "green" }} emoji="💰" skill="Azure" />
		      <Skill
		        style={{ backgroundColor: "yellow" }}
		        emoji="✈️"
		        skill="Kubernetes"
		      />
		      <Skill style={{ backgroundColor: "cyan" }} emoji="📈" skill="React" />
		    </div>
		  );
		}
		
		function Skill(props) {
		  return (
		    <span className="skill" style={props.style}>
		      {props.skill} {props.emoji}
		    </span>
		  );
		}
		
		export default App;

### The Rules of JSX ###
1. Rules:
	1. General JSX Rules
		1. JSX works essentially like HTML, but we can enter "JavaScript mode" by using `{}` (for text or attributes)
			1. Anywhere in the markup
			2. Where text or attribute is expected
		2. We can place **JavaScript expressions** (anything that produces a value) inside `{}`. Examples: 
			1. Reference variables
			2. Construct arrays or objects, 
			3. `[].map()`, 
			4. Ternary operator
		3. Statements are **not allowed** (if/else, for, switch)
		4. JSX produces a **JavaScript expression**

				const el = <h1>Hello React!</h1>;
				// same as
				const el = React.createElement('h1', null, 'Hello React!'); // converted to this expression

			1. We can place **other pieces of JSX** inside `{}`
				1. Since we can put any JS expression inside `{}` (JS mode)
			2. We can write JSX **anywhere** inside a component (in `if/else`, assign to variables, pass it into functions)
		5. A piece of JSX can only have **one root element**. If you need more, use `<React.Fragment>` (or the short `<>`) (later)
	2. Differences between JSX and HTML
		1. `className` instead of HTML's class
		2. `htmlFor` instead of HTML's `for`
		3. Every tag needs to be **closed**. Exmaples: `<img />`, `<br />`
		4. All event handlers and other properties need to be **camelCased**. Examples: `onClick` or `onMouseOver`
		5. **Exception:** `aria-*` and `data-*` are written with dashes like in HTML
		6. CSS inline styles are written like this: `{{<style>}}` (to reference a variable, and then an object)
		7. CSS property names are also **camelCased**
		8. Comments need to be in `{}` (because they are JS)

### Rendering Lists ###
1. One of the most common things we do in almost all React applications
2. How to render list?
3. What is rendering a list?
	1. When we have an array, and we want to construct a component for each element of the array
	2. Each child in a list must have a unique `key` property (prop that is internal to React - for performance optimization (later))
4. Code:

		function Menu() {
		  return (
		    <main className="menu">
		      <h2>Our menu</h2>
		
		      <ul className="pizzas">
		        {/* Array is converted to list of components. forEach will not work (it doesn't return a new array) */}
		        {pizzaData.map((pizza) => (
		          <Pizza pizzaObj={pizza} key={pizza.name} />
		        ))}
		      </ul>
		
		      {/* <Pizza
		        name="Pizza Spinaci"
		        ingredients="Tomato, mozarella, spinach, and ricotta cheese"
		        photoName="pizzas/spinaci.jpg"
		        price={10}
		      />
		      <Pizza
		        name="Pizza Funghi"
		        ingredients="Tomato, mushrooms"
		        price={12}
		        photoName="pizzas/funghi.jpg"
		      /> */}
		    </main>
		  );
		}
		
		// Two rules:
		// 1: Starts with capital letter
		// 2: returns a markup (exactly one element)
		// 3: Nesting declaration inside another declaration works but it must not be done
		function Pizza(props) {
		  console.log(props); // {name: 'Pizza Spinacci', ingredients: 'Tomato, ...'}
		
		  return (
		    <li className="pizza">
		      <img src={props.pizzaObj.photoName} alt={props.pizzaObj.name} />
		      <div>
		        <h3>{props.pizzaObj.name}</h3>
		        <p>{props.pizzaObj.ingredients}</p>
		        <span>{props.pizzaObj.price}</span>
		      </div>
		    </li>
		  );
		}

### Conditional Rendering With && ###
1. Rendering JSX (a piece or entire component) based on a condition
2. Code:

		function Menu() {
		  const pizzas = pizzaData;
		  const numPizzas = pizzas.length;
		
		  return (
		    <main className="menu">
		      <h2>Our menu</h2>
		      {/* It is a truthy value. React renders a 0. Never use number */}
		      {numPizzas > 0 && (
		        <ul className="pizzas">
		          {/* Array is converted to list of components. forEach will not work (it doesn't return a new array) */}
		          {pizzas.map((pizza) => (
		            <Pizza pizzaObj={pizza} key={pizza.name} />
		          ))}
		        </ul>
		      )}
		
		      {/* <Pizza
		        name="Pizza Spinaci"
		        ingredients="Tomato, mozarella, spinach, and ricotta cheese"
		        photoName="pizzas/spinaci.jpg"
		        price={10}
		      />
		      <Pizza
		        name="Pizza Funghi"
		        ingredients="Tomato, mushrooms"
		        price={12}
		        photoName="pizzas/funghi.jpg"
		      /> */}
		    </main>
		  );
		}

### Conditional Rendering With Ternaries ###
1. Code:

		function Menu() {
		  const pizzas = pizzaData;
		  const numPizzas = pizzas.length;
		
		  return (
		    <main className="menu">
		      <h2>Our menu</h2>
		      {/* It is a truthy value. React renders a 0. Never use number.
		      We can only write JS expressions that return values within `{}` */}
		      {numPizzas > 0 ? (
		        <ul className="pizzas">
		          {/* Array is converted to list of components. forEach will not work (it doesn't return a new array) */}
		          {pizzas.map((pizza) => (
		            <Pizza pizzaObj={pizza} key={pizza.name} />
		          ))}
		        </ul>
		      ) : (
		        <p>We're still working on our menu. Please come back later.</p>
		      )}
		    </main>
		  );
		}

		...

		function Footer() {
		  const hour = new Date().getHours();
		  // console.log(hour);
		  const openHour = 9;
		  const closeHour = 22;
		  const isOpen = hour >= openHour && hour <= closeHour;
		  console.log(isOpen);
		
		  // if (hour >= openHour && hour <= closeHour) {
		  //   alert("We're currently open");
		  // } else {
		  //   alert("Sorry we're closed");
		  // }
		
		  // return React.createElement("footer", null, "We're currently open");
		  return (
		    <footer>
		      {isOpen ? (
		        <div className="order">
		          <p>We're open until {closeHour}:00. Come visit us or order online.</p>
		          <button className="btn">Order</button>
		        </div>
		      ) : (
		        <p>
		          We're happy to welcome you between {openHour}:00 and {closeHour}:00
		        </p>
		      )}
		    </footer>
		  ); // short circuiting. React doesn't render `true` or `false` into the DOM
		}

### Extracting JSX Into a New Component ###
1. Multiple returns (based on a condition)
2. Code:

		function Pizza(props) {
		  console.log(props); // {name: 'Pizza Spinacci', ingredients: 'Tomato, ...'}
		
		  if (props.pizzaObj.soldOut) return null; // nothing is rendered
		
		  return (
		    <li className="pizza">
		      <img src={props.pizzaObj.photoName} alt={props.pizzaObj.name} />
		      <div>
		        <h3>{props.pizzaObj.name}</h3>
		        <p>{props.pizzaObj.ingredients}</p>
		        <span>{props.pizzaObj.price}</span>
		      </div>
		    </li>
		  );
		}
		
		function Footer() {
		  const hour = new Date().getHours();
		  // console.log(hour);
		  const openHour = 9;
		  const closeHour = 22;
		  const isOpen = hour >= openHour && hour <= closeHour;
		  console.log(isOpen);
		
		  // if (hour >= openHour && hour <= closeHour) {
		  //   alert("We're currently open");
		  // } else {
		  //   alert("Sorry we're closed");
		  // }
		
		  // return React.createElement("footer", null, "We're currently open");
		  if (!isOpen)
		    return (
		      <footer className="footer">
		        <p>
		          We're happy to welcome you between {openHour}:00 and {closeHour}:00
		        </p>
		      </footer>
		    );
		
		  return (
		    <footer className="footer">
		      {
		        <div className="order">
		          <p>We're open until {closeHour}:00. Come visit us or order online.</p>
		          <button className="btn">Order</button>
		        </div>
		      }
		    </footer>
		  ); // short circuiting. React doesn't render `true` or `false` into the DOM
		}

3. Code:

		function Footer() {
		  const hour = new Date().getHours();
		  // console.log(hour);
		  const openHour = 7;
		  const closeHour = 22;
		  const isOpen = hour >= openHour && hour <= closeHour;
		  console.log(isOpen);
		
		  return (
		    <footer className="footer">
		      {isOpen ? (
		        <Order closeHour={closeHour} />
		      ) : (
		        <p>
		          We're happy to welcome you between {openHour}:00 and {closeHour}:00
		        </p>
		      )}
		    </footer>
		  ); // short circuiting. React doesn't render `true` or `false` into the DOM
		}
		
		function Order(props) {
		  return (
		    <div className="order">
		      <p>
		        We're open until {props.closeHour}:00. Come visit us or order online.
		      </p>
		      <button className="btn">Order</button>
		    </div>
		  );
		}

### Destructuring Props ###
1. Props are always passed into child components (even if it is empty)
2. Code:

		function Pizza({ pizzaObj }) {
		  // Shows what props will be received by the function. We don't have to go to where the component is being used
		  if (pizzaObj.soldOut) return null; // nothing is rendered
		
		  return (
		    <li className="pizza">
		      <img src={pizzaObj.photoName} alt={pizzaObj.name} />
		      <div>
		        <h3>{pizzaObj.name}</h3>
		        <p>{pizzaObj.ingredients}</p>
		        <span>{pizzaObj.price}</span>
		      </div>
		    </li>
		  );
		}
		
		...
		
		function Order({ closeHour, openHour }) {
		  // If we try to destructure a property that doesn't exist, it is `undefined`
		  return (
		    <div className="order">
		      <p>
		        We're open from {openHour}:00 until {closeHour}:00. Come visit us or
		        order online.
		      </p>
		      <button className="btn">Order</button>
		    </div>
		  );
		}

### React Fragments ###
1. It allows us to have more than one element in a piece of JSX
2. Using nothing:

		<>...</>

3. Using `React.Fragment` **(M)**

		<React.Fragment key="abcd">
			...
		</Readt.Fragment>

### Setting Classes and Text Conditionally ###
1. Conditionally set text, and class names
2. Code:

		function Pizza({ pizzaObj }) {
		  // Shows what props will be received by the function. We don't have to go to where the component is being used
		  // if (pizzaObj.soldOut) return null; // nothing is rendered
		
		  // We don't have to use classList and imperative code to set class
		  return (
		    <li className={`pizza ${pizzaObj.soldOut ? "sold-out" : ""}`}>
		      <img src={pizzaObj.photoName} alt={pizzaObj.name} />
		      <div>
		        <h3>{pizzaObj.name}</h3>
		        <p>{pizzaObj.ingredients}</p>
		        <span>{pizzaObj.soldOut ? "SOLD OUT" : pizzaObj.price}</span>
		      </div>
		    </li>
		  );
		}
		
		function Footer() {
		  const hour = new Date().getHours();
		  const openHour = 7;
		  const closeHour = 22;
		  const isOpen = hour >= openHour && hour <= closeHour;
		  console.log(isOpen);
		
		  return (
		    <footer className="footer">
		      {isOpen ? (
		        <Order openHour={openHour} closeHour={closeHour} />
		      ) : (
		        <p>
		          We're happy to welcome you between {openHour}:00 and {closeHour}:00
		        </p>
		      )}
		    </footer>
		  ); // short circuiting. React doesn't render `true` or `false` into the DOM
		}
		
		function Order({ closeHour, openHour }) {
		  // If we try to destructure a property that doesn't exist, it is `undefined`
		  return (
		    <div className="order">
		      <p>
		        We're open from {openHour}:00 until {closeHour}:00. Come visit us or
		        order online.
		      </p>
		      <button className="btn">Order</button>
		    </div>
		  );
		}

### Section Summary ###
1. Components are the building blocks of a UI in React
2. Each component is a self-contained piece of the UI which includes
	1. Data
	2. JS Logic
	3. Appearance: JSX
		1. JSX: A declarative syntax
			1. It is this block of JSX that is returned from a component (This is what we see on the screen)
			2. It can contain markup
				1. HTML
				2. CSS
				3. JS inside `{}` (entering the JS mode)
3. A complete application is composed of multiple components organized in a component tree
	1. Component tree
		1. Components at the top (parent component) use the components below them (child components)
			1. Example:
				1. App
					1. Header
					2. Menu
						1. Pizza
						2. Pizza
						3. Pizza
					3. Footer
						1. Order
	2. To share data between components
		1. Parent components can pass data into child components using **Props**
			1. For each value we pass, we define one prop (property)
			2. Using props, we can configure components as we wish
		2. Props can only be passed down a tree (from parent to child) (never the other way around)
	3. List: Rendering multiple components at once using the JavaScript `.map()` method
		1. There is nothing special in React for loops
			1. We can use JS to construct lists of components of the same type
	4. Components can be conditionally rendered using JS tools: &&, ?, and multipler `return`
4. Theory:
	1. Difference between declarative and imperative programming
	2. Separation of concerns
	3. Why we cannot mutate props
	4. ...

### CHALLENGE #2: Profile Card (v2) ###
1. Code:

		import "./App.css";

		const skills = [
		  {
		    skill: "Java",
		    level: "advanced",
		    color: "#C3DCAF",
		  },
		  {
		    skill: "Spring Boot",
		    level: "advanced",
		    color: "#E84F33",
		  },
		  {
		    skill: "React",
		    level: "beginner",
		    color: "#FF3B00",
		  },
		  {
		    skill: "Azure",
		    level: "intermediate",
		    color: "#2662EA",
		  },
		  {
		    skill: "JavaScript",
		    level: "intermediate",
		    color: "#EFD81D",
		  },
		];
		
		function App() {
		  return (
		    <div className="card">
		      <Avatar />
		      <div className="data">
		        <Intro />
		        <SkillList />
		      </div>
		    </div>
		  );
		}
		
		function Avatar() {
		  return (
		    <div className="avatar">
		      <img src="avatar_hero.jpg" alt="Avatar Hero" width="100%" />
		    </div>
		  );
		}
		
		function Intro() {
		  return (
		    <div className="intro">
		      <h2>Abdullah Mutthoju</h2>
		      <p>
		        Java Full-stack web developer and architect. When not doing serious
		        work, I like to play with my daughter, travel, and shop.
		      </p>
		    </div>
		  );
		}
		
		function SkillList() {
		  return (
		    <div className="skill-list">
		      {skills.map((skill) => {
		        const emoji =
		          skill.level === "advanced"
		            ? "⚡"
		            : skill.level === "intermediate"
		            ? "💰"
		            : "❤️";
		
		        return (
		          <Skill
		            style={{ backgroundColor: skill.color }}
		            emoji={emoji}
		            skill={skill.skill}
		          />
		        );
		      })}
		    </div>
		  );
		}
		
		function Skill(props) {
		  return (
		    <span className="skill" style={props.style}>
		      {props.skill} {props.emoji}
		    </span>
		  );
		}
		
		export default App;


## Section 6: State, Events, and Forms: Interactive Components ##
### Section Overview ###
1. Making components interactive
	1. Handling **events** (in React)
	2. **State** to update the UI
	3. Building **forms** the "React way"
		1. Using state
	4. **Controlled** elements
2. Flashcards application

### Let's Build a Steps Component ###
1. Events & State
2. Static part of the component
	1. New project
3. Code:

		const messages = [
		  "Learn React ⚛️",
		  "Apply for jobs 💼",
		  "Invest your new income 🤑",
		];
		
		export default function App() {
		  const step = 1;
		
		  return (
		    <div className="steps">
		      <div className="numbers">
		        <div className={`${step >= 1 ? "active" : ""}`}>1</div>
		        <div className={`${step >= 2 ? "active" : ""}`}>2</div>
		        <div className={`${step >= 3 ? "active" : ""}`}>3</div>
		      </div>
		
		      <p className="message">
		        Step {step}: {messages.at(step - 1)}
		      </p>
		
		      <div className="buttons">
		        <button style={{ backgroundColor: "#7950f2", color: "#fff" }}>
		          Previous
		        </button>
		        <button style={{ backgroundColor: "#7950f2", color: "#fff" }}>
		          Next
		        </button>
		      </div>
		    </div>
		  );
		}

### Handling Events the React Way ###
1. It is straight-forward
2. Declarative approach
	1. Similar to HTML inline event-listener
		1. We listen for event right on the element where it will happen
3. Code:

		export default function App() {
		  const step = 1;
		
		  function handlePrevious() {
		    // `handle<Name>` is standard
		    alert("Previous");
		  }
		
		  function handleNext() {
		    // `handle<Name>` is standard
		    alert("Next");
		  }
		
		  return (
		    <div className="steps">
		      <div className="numbers">
		        <div className={`${step >= 1 ? "active" : ""}`}>1</div>
		        <div className={`${step >= 2 ? "active" : ""}`}>2</div>
		        <div className={`${step >= 3 ? "active" : ""}`}>3</div>
		      </div>
		
		      <p className="message">
		        Step {step}: {messages.at(step - 1)}
		      </p>
		
		      <div className="buttons">
		        <button
		          style={{ backgroundColor: "#7950f2", color: "#fff" }}
		          onClick={handlePrevious}
		        >
		          Previous
		        </button>
		        <button
		          style={{ backgroundColor: "#7950f2", color: "#fff" }}
		          onClick={handleNext}
		        >
		          Next
		        </button>
		      </div>
		    </div>
		  );
		}

### What is State in React? ###
#### What we need to Learn ####
1. **State** is the most important concept in React
	1. (So we will keep learning about state throughout the entire course...)
		1. Everything in React revolves around state
2. What React developers need to learn about state:
	1. **What is state** and **why** do we need it?
	2. How to use state in **practice**?
		1. `useState`
		2. `useReducer`
		3. Context API
		4. Redux (external tool)
	3. **Thinking** about state (how to)
		1. When to use state
		2. Where to place state
		3. Types of state

#### What is State? ####
1. What if a component needs to hold its own data and need to hold it over time?
	1. Unlike props that are passed from its parent
2. What if we want to make our app interactive, changing UI as a result of an action?
	1. Solution: State
3. **State**:
	1. Data that a component **can hold over time**, necessary for information that it needs to **remember** throughout the app's lifecycle
	2. It is the **component's memory**
	3. Examples:
		1. Notification count
		2. Text content of an input field
		3. Active tab (in a tabbed component)
		4. Contents of a shopping cart (more complext)
	4. The user can change the valus in a state
		1. When a user reads a notification, the count will go down by one
		2. When a user clicks on another tab, that tab will become active
	5. Piece of state: Each of the pieces of information is a piece of state
		1. State - general term
		2. **State variable/ piece of state**: A single variable in a component (component state)
		3. **State**: The entire state a component is in (the entire condition at a certain point in time)
			1. State = all the pieces of state together
	6. Updating **component state** triggers React to **re-render the component** (in the UI)
		1. Whenever we update a piece of state in a component, this will make React re-render the component in the UI
			1. A new update Component View (Component visually rendered on the screen in the UI) is created
				1. **When one single component is rendered, we call that a view**
					1. All views together make up the final UI
		2. State is the mechanism used by React to keep UI in sync with data
			1. If we change the state, we change the UI
			2. State allows developers to:
				1. Update the component's view (by re-rendering it)
	7. State allows developers to:
		1. Update the component's view (by re-rendering it)
		2. Persist local variables between multiple renders (and re-renders)
	8. State is a tool (most powerful in React). **Mastering (the mechanics) state will unlock the power of React development**

### Constructing a State Variable With useState ###
1. `useState(<initial-value>)` - It is a hook in React
	1. All functions that start with `use` are react hooks (`useEffect`, `useReducer`, `useState`, ...)
	2. We can only call hooks on the top level of the function (Component function)
		1. **We cannot call it inside `if` statements, another function, or loop**
2. We must only update state using setter function only (not manually)
3. Code:

		export default function App() {
		  // const step = 1;
		  // 1. Add a new state variables
		  // 2. We use it in code (usually in JSX)
		  // 3. We update the state in an event-handler
		  const [step, setStep] = useState(1); // takes a default value
		
		  function handlePrevious() {
		    // `handle<Name>` is standard
		    if (step > 1) setStep(step - 1);
		  }
		
		  function handleNext() {
		    // `handle<Name>` is standard
		    if (step < 3) setStep(step + 1);
		  }
		
		  return (
		    <div className="steps">
		      <div className="numbers">
		        <div className={step >= 1 ? "active" : ""}>1</div>
		        <div className={step >= 2 ? "active" : ""}>2</div>
		        <div className={step >= 3 ? "active" : ""}>3</div>
		      </div>
		
		      <p className="message">
		        Step {step}: {messages.at(step - 1)}
		      </p>
		
		      <div className="buttons">
		        <button
		          style={{ backgroundColor: "#7950f2", color: "#fff" }}
		          onClick={handlePrevious}
		        >
		          Previous
		        </button>
		        <button
		          style={{ backgroundColor: "#7950f2", color: "#fff" }}
		          onClick={handleNext}
		        >
		          Next
		        </button>
		      </div>
		    </div>
		  );
		}

### Don't Set State Manually! ###
1. Breaking React:

		let [step, setState] = useState(1);
		// ...
		step = step = 1; // React doesn't know that this state variable is updated. Nothing happens after this

	1. `setState` updates the state value without mutating it
		1. The update operation is possible only through this function
	2. Using array or object:

			const [test] = useState({ name: "Jonas" });
			//
			test.name = 'Fred'; // It works

		1. It is a really bad-practice (React doesn't want us to do this)
		2. Better way:

				setTest({ name: 'Fred' });

### The Mechanics of State ###
1. We don't do direct DOM manipulations (because React is **declarative**) (we don't touch the DOM)
	1. How is a component view updated them?
		1. **In React, a view is updated by re-rendering the (entire) component** (important React principle) (whenever the underlying data changes)
			1. How?
				1. **React calls the component function again** (each time the component is rendered)
					1. This is like:
						1. React removes the existing view & re-renders the updated view when re-render needs to happen
			2. **State is preserved throughout re-renders**
				1. Even if component is re-rendered again and again, the state is not reset (unless the component disappears from the UI entirely (unmounting))
				2. **When the state is updated, the component is automatically re-rendered**
2. Flow:
	1. If a user clicks a button
	2. An event handler is triggered
	3. The handler (manually) updates a piece of state (using the `set` function coming from the `useState` hook)
	4. React sees that the state has changed and it will automatically re-render the component
		1. Results in an updated view of the component
3. **Whenever we want to update a view, we update the state**
	1. React will react to the update and do it's thing
		1. React is called React because:
			1. React reacts to state changes by re-rendering the UI

### Adding Another Piece of State ###
1. Code:

		export default function App() {
		  // const step = 1;
		  // 1. Add a new state variables
		  // 2. We use it in code (usually in JSX)
		  // 3. We update the state in an event-handler
		  const [step, setStep] = useState(1); // takes a default value
		  const [isOpen, setIsOpen] = useState(true);
		
		  function handlePrevious() {
		    // `handle<Name>` is standard
		    if (step > 1) setStep(step - 1);
		  }
		
		  function handleNext() {
		    // `handle<Name>` is standard
		    if (step < 3) setStep(step + 1);
		  }
		
		  return (
		    <>
		      <button className="close" onClick={() => setIsOpen(!isOpen)}>
		        &times;
		      </button>
		      {isOpen && (
		        <div className="steps">
		          <div className="numbers">
		            <div className={step >= 1 ? "active" : ""}>1</div>
		            <div className={step >= 2 ? "active" : ""}>2</div>
		            <div className={step >= 3 ? "active" : ""}>3</div>
		          </div>
		
		          <p className="message">
		            Step {step}: {messages.at(step - 1)}
		          </p>
		
		          <div className="buttons">
		            <button
		              style={{ backgroundColor: "#7950f2", color: "#fff" }}
		              onClick={handlePrevious}
		            >
		              Previous
		            </button>
		            <button
		              style={{ backgroundColor: "#7950f2", color: "#fff" }}
		              onClick={handleNext}
		            >
		              Next
		            </button>
		          </div>
		        </div>
		      )}
		    </>
		  );
		}

### React Developer Tools ###
1. Open console:
	1. Click on link to download Dev-Tools
		1. Click: Chrome web-store
		2. Two tabs are added:
			1. Components
			2. Profiler
2. Components:
	1. It is for showing the component tree
	2. We can also see state
		1. props
			1. Props the component currently selected is receiving
		2. hooks
			1. One entry for each state hook
				1. We can manipulate the variables to experiment with state
					1. We can toggle boolean values
					2. We can change values

### Updating State Based on Current State ###
1. We update a state variable based on the current value of the state
	1. How to do that?
		1. We take the state value returned and return modified state
2. We must not directly update state as we have done using `setStep` function. We pass a function that receives the current value of the state:

		setStep(s => s - 1);
		setStep(s => s + 1);

	1. If we use it twice, the state is updated twice

			setStep(s => s + 1); // Preferred approach if we want to set state based on the current state. This is the more safe way
			setStep(s => s + 1);

		1. If we don't want to set state based on the current state, we can directly pass the value

				setStep(25);
 
### More Thoughts About State + State Guidelines ###
#### One Component,One State ####
1. Each component has and manages **its own state**, no matter how many times we render the same component
	1. The multiple component instances will operate independent of one another
		1. Example: Multiple instances of the `counter` component
			1. Counters in each component are independent and will not affect the other components
	2. State is isolated inside each component

#### UI as a Function of State ####
1. UI = f(state)
	1. UI is representation of all the states of all the components
	2. The application is about changing state over time
		1. Correctly displaying state at all times
2. With state, we view UI as a **reflection of data changing over time**
	1. We **describe that reflection** of data using:
		1. State
		2. Event handlers, and 
		3. JSX
3. We describe the UI, and React takes care of the rest

#### In Practical Terms ####
1. Practical guidelines about state
	1. Use a state variable for any data that the component should keep track of ("remember") over time. **This is data that will change at some point**. In Vanilla JS, That's a `let` variable, or an `[]`, or `{}` (that we mutate during the application life-cycle)
	2. Whenever you want something in the component to be **dynamic**, construct a piece of state related to that "thing", and update the state when the "thing" should change (aka "be dynamic")
		1. Example: A modal window can be open or closed. So we define a state variable `isOpen` that tracks whether the modal is open or not. On `isOpen = true` we display the window, on `isOpen = false` we hide it.
	3. If you want to change the way a component looks, or the data it displays, **update its state**. This usually happens in an **event handler** function
	4. When building a component, imagine its view as a **reflection of state changing over time**
	5. For data that should not trigger component re-render, **don't use state**. Use a regular variable instead. This is common **beginner mistake** to use state for any variable

### A Vanilla JavaScript Implementation ###
1. Vanilla JS
	1. JS inside HTML
	2. Manual selection of DOM elements
	3. Variables are updated inside event-handler functions
		1. We need to call the function which does DOM manipulation (to keep it in sync with the state)
			1. Imperative code (step by step)
				1. We need DOM manipulation

### CHALLENGE #1: Date Counter (v1) ###
1. Code:

		import { useState } from "react";
		import "./App.css";
		
		function App() {
		  return <Counter />;
		}
		
		function Counter() {
		  const [step, setStep] = useState(1);
		  const [count, setCount] = useState(1);
		  const [date, setDate] = useState(new Date());
		
		  function handleDecreaseStep() {
		    if (step > 0) setStep((step) => step - 1);
		  }
		
		  function handleIncreaseStep() {
		    setStep((step) => step + 1);
		  }
		
		  function handleDecreaseCount() {
		    setCount((count) => count - step);
		    setDate((date) => {
		      const newDate = new Date(date);
		      newDate.setDate(newDate.getDate() - step);
		      return newDate;
		    });
		  }
		
		  function handleIncreaseCount() {
		    setCount((count) => count + step);
		    setDate((date) => {
		      const newDate = new Date(date);
		      newDate.setDate(newDate.getDate() + step);
		      return newDate;
		    });
		  }
		
		  return (
		    <div>
		      <div>
		        <button onClick={handleDecreaseStep}>-</button>
		        <span>Step: {step}</span>
		        <button onClick={handleIncreaseStep}>+</button>
		      </div>
		      <div>
		        <button onClick={handleDecreaseCount}>-</button>
		        <span>Count: {count}</span>
		        <button onClick={handleIncreaseCount}>+</button>
		      </div>
		      <div>
		        {count} days from today is: {date.toString()}
		      </div>
		    </div>
		  );
		}
		
		export default App;

### Starting a New Project: The "Far Away" Travel List ###
1. Components:
	1. Logo
	2. Form
	3. PackingList
		1. Item
	4. Stats

### Building the Layout ###
1. Starter file: 05-travel-list/index.css
2. Code:

		export default function App() {
		  return (
		    <div className="app">
		      <Logo />
		      <Form />
		      <PackingList />
		      <Stats />
		    </div>
		  );
		}
		
		function Logo() {
		  return <h1>🌴 Far Away 🎒</h1>;
		}
		
		function Form() {
		  return (
		    <div className="add-form">
		      <h3>What do you need for your trip?</h3>
		    </div>
		  );
		}
		
		function PackingList() {
		  return <div className="list"></div>;
		}
		
		function Stats() {
		  return (
		    <footer className="stats">
		      <em>💼 You have X items on your list, and you already packed X (X%)</em>
		    </footer>
		  );
		}

### Rendering the Items List ###
1. Code:

		const initialItems = [
		  { id: 1, description: "Passports", quantity: 2, packed: false },
		  { id: 2, description: "Socks", quantity: 12, packed: true },
		  { id: 2, description: "Charger", quantity: 1, packed: false },
		];
		
		export default function App() {
		  return (
		    <div className="app">
		      <Logo />
		      <Form />
		      <PackingList />
		      <Stats />
		    </div>
		  );
		}
		
		function Logo() {
		  return <h1>🌴 Far Away 🎒</h1>;
		}
		
		function Form() {
		  return (
		    <div className="add-form">
		      <h3>What do you need for your trip?</h3>
		    </div>
		  );
		}
		
		function PackingList() {
		  return (
		    <div className="list">
		      <ul className="list">
		        {initialItems.map((item) => (
		          <Item item={item} />
		        ))}
		      </ul>
		    </div>
		  );
		}
		
		function Item({ item }) {
		  return (
		    <li>
		      <span style={item.packed ? { textDecoration: "line-through" } : {}}>
		        {item.quantity} {item.description}
		      </span>
		      <button>❌</button>
		    </li>
		  );
		}
		
		function Stats() {
		  return (
		    <footer className="stats">
		      <em>💼 You have X items on your list, and you already packed X (X%)</em>
		    </footer>
		  );
		}

### Building a Form and Handling Submissions ###
1. Code:

		function Form() {
		  function handleSubmit(e) {
		    e.preventDefault();
		    console.log(e);
		  }
		
		  return (
		    <form className="add-form" onSubmit={handleSubmit}>
		      <h3>What do you need for your trip?</h3>
		      <select>
		        {Array.from({ length: 20 }, (_, i) => i + 1).map((num) => (
		          <option key={num} value={num}>
		            {num}
		          </option>
		        ))}
		      </select>
		      <input type="text" placeholder="Item..." />
		      {/* <button onClick={handleClick}>Add</button> */}
		    </form>
		  );
		}

### Controlled Elements ###
1. By default, input fields maintain their own state inside the DOM (in the element itself) (it makes it hard to read the values) (values are left in the elements - which is not preferred)
	1. Solution: In React, all state is kept in a central place (inside React app)
		1. Implementation technique: **Controlled elements**
			1. React controls and owns the state of input fields (not the DOM)
				1. Form data needs to be maintained in a state
2. Steps:
	1. Construct a piece of state
	2. Use the state in the JSX as a value: Example: `{description}`
	3. We want to connect the state to the value we type in the form
		1. Since we set the `description` to empty, the input form will stay empty even if we type into it

				<input
			      type="text"
			      placeholder="Item..."
			      value={description}
			      onChange={(e) => setDescription(e.target.value)}
			    />

			1. If we enter anything, it will get synchronized
				1. Whenever we change content in the input fields, `onChange` event is fired-off
3. Code:

		import { useState } from "react";

		const initialItems = [
		  { id: 1, description: "Passports", quantity: 2, packed: false },
		  { id: 2, description: "Socks", quantity: 12, packed: true },
		  { id: 3, description: "Charger", quantity: 1, packed: false },
		];
		
		export default function App() {
		  return (
		    <div className="app">
		      <Logo />
		      <Form />
		      <PackingList />
		      <Stats />
		    </div>
		  );
		}
		
		function Logo() {
		  return <h1>🌴 Far Away 🎒</h1>;
		}
		
		function Form() {
		  const [description, setDescription] = useState("");
		  const [quantity, setQuantity] = useState(1);
		
		  function handleSubmit(e) {
		    e.preventDefault();
		
		    if (!description) return;
		
		    const newItem = { description, quantity, packed: false, id: Date.now() };
		
		    console.log(newItem);
		
		    // Allowing React to keep state in sync with Form elements
		    setDescription("");
		    setQuantity(1);
		  }
		
		  return (
		    <form className="add-form" onSubmit={handleSubmit}>
		      <h3>What do you need for your trip?</h3>
		      <select
		        value={quantity}
		        onChange={(e) => setQuantity(Number(e.target.value))}
		      >
		        {Array.from({ length: 20 }, (_, i) => i + 1).map((num) => (
		          <option key={num} value={num}>
		            {num}
		          </option>
		        ))}
		      </select>
		      <input
		        type="text"
		        placeholder="Item..."
		        value={description}
		        onChange={(e) => setDescription(e.target.value)}
		      />
		      <button>Add</button>
		      {/* <button onClick={handleClick}>Add</button> */}
		    </form>
		  );
		}
		
		function PackingList() {
		  return (
		    <div className="list">
		      <ul className="list">
		        {initialItems.map((item) => (
		          <Item item={item} key={item.id} />
		        ))}
		      </ul>
		    </div>
		  );
		}
		
		function Item({ item }) {
		  return (
		    <li>
		      <span style={item.packed ? { textDecoration: "line-through" } : {}}>
		        {item.quantity} {item.description}
		      </span>
		      <button>❌</button>
		    </li>
		  );
		}
		
		function Stats() {
		  return (
		    <footer className="stats">
		      <em>💼 You have X items on your list, and you already packed X (X%)</em>
		    </footer>
		  );
		}

### State vs. Props ###
1. The difference between State and Props
2. Differences:
	1. State:
		1. **Internal** data, owned by component
			1. Component's memory
				1. It can hold data over time (across multiple re-renders)
		2. Can be updated by the component itself
			1. Causes component to be re-rendered by React
		3. Updating state causes component to re-render
		4. Used to make components interactive
	2. Props:
		1. **External** data, owned by parent component
			1. Similar to function parameters
				1. As a communication channel between parent and child components (parents can pass data into children)
		2. Similar to function parameters
		3. Read-only
			1. They cannot be modified by the components receiving them
		4. **Receiving new props causes component to re-render**.
			1. Usually when the parent's state has been updated

					function Question() {
						const [upvotes, setUpvotes] = useState(0);

						return (
							<div>
								{/* ... */}
								<Button upvotes={upvotes} bgColor="blue" />
							</div>
						);
					}

					function Button(upvotes, bgColor) {
						const [hovered, setHovered] = useState(false);

						return (
							<div>
								{/* ... */}
								<button
									onMouseEnter={() => setHovered(true)}
									onMouseLeave={() => setHovered(false)}
									style={{ background: bgColor }}>
									{hovered} ? "Upvote" : `${upvotes}`}
								</button>
							</div>
						);
					}

				1. `upvotes` is state maintained in parent
				2. If `upvotes` is updated, the parent component is re-rendered
				3. Since `upvotes` is passed as a prop to the child component, the child component is also re-rendered (otherwise, the child component will not be in sync with the state)
			2. Whenever a piece of state is passed as a prop, when the state updates, both the parent and child components are re-rendered
				1. **A connection between state & props**
		5. Used by parent to configure child component (prosp are "settings")

### EXERCISE #1: Flashcards ###
1. How to use state in practice in certain situations can be tricky
2. Code:

		import "./styles.css";
		import { useState } from "react";
		
		export default function App() {
		  return (
		    <div className="App">
		      <FlashCards />
		    </div>
		  );
		}
		
		const questions = [
		  {
		    id: 3457,
		    question: "What language is React based on?",
		    answer: "JavaScript",
		  },
		  {
		    id: 7336,
		    question: "What are the building blocks of React apps?",
		    answer: "Components",
		  },
		  {
		    id: 8832,
		    question: "What's the name of the syntax we use to describe a UI in React?",
		    answer: "JSX",
		  },
		  {
		    id: 1297,
		    question: "How to pass data from parent to child components?",
		    answer: "Props",
		  },
		  {
		    id: 9103,
		    question: "How to give components memory?",
		    answer: "useState hook",
		  },
		  {
		    id: 2002,
		    question:
		      "What do we call an input element that is completely synchronised with state?",
		    answer: "Controlled element",
		  },
		];
		
		function FlashCards() {
		  const [selectedId, setSelectedId] = useState(null);
		
		  function handleClick(id) {
		    setSelectedId(id !== selectedId ? id : null);
		  }
		
		  return (
		    <div className="flashcards">
		      {questions.map((question) => (
		        <div
		          key={question.id}
		          onClick={() => handleClick(question.id)}
		          className={question.id === selectedId ? "selected" : ""}
		        >
		          {question.id === selectedId ? question.answer : question.question}
		        </div>
		      ))}
		    </div>
		  );
		}

### CHALLENGE #2: Date Counter (v2) ###
1. 

## Section 7: Thinking In React: State Management ##
### Section Overview ###
1. Core skills:
	1. **Thinking** in React
	2. **State** management
	3. **When** and **where** to construct state?
	4. **Derived** state (when and where)
	5. **Lifting** up state
		1. How to communicate between parent and child components (by lifting the state up)

### What is "Thinking in React"? ###
#### Thinking in React is a Core Skill ####
1. Building React applications requires completely different mindset
	1. It is different from building applications from vanilla JS
2. React Mindset:
	1. How to work with React API
		1. Functions (`useState`)
	2. Thinking in React
	3. Intersection: This is where professional React apps are built
3. Thinking in React means?
	1. Thinking about a very good mental model of how, and when to use all the React tools like:
		1. Components
		2. State
		3. Props
		4. Data flow
		5. Effects
		6. etc.
	2. Thinking in **state transitions**, not element mutations

#### Thinking in React as a Process ####
1. The "Thinking in React" Process: (helps us build apps in a more structured way)
	1. Break the desired UI into **components** and establish the **component tree** (how the components are related to one-another)
		1. Thinking about re-usability and composability of components
	2. Build a **static** version in React (without state and interactivity)
		1. We do most of the coding up-front, before thinking about state and interactivity
	3. Think about **state**: (state management)
		1. When to use state
		2. Types of state: local vs. global
		3. Where to place each piece of state
	4. Establish **data flow**: Thinking about (state management)
		1. One-way data flow
		2. Child-to-parent communication
		3. Accessing global state
2. There is always back-and-forth among the steps (it is not linear)
3. When you know how to "think in React", you will be able to answer:
	1. How to break up a UI design into components?
	2. How to make some components reusable?
	3. How to assemble UI from reusable components?
	4. What pieces of state do I need for interactivity?
	5. Where to place? (What component should "own" each piece of state?)
	6. What types of state can or should I use?
	7. How to make data flow through app?
4. We will master the skills by practice and writing lots of code

### Fundamentals of State Management ###
1. Managing state is the most important aspect when it comes to thinking in React

#### What is State Management? ####
1. We can use `useState` to construct multiple pieces of state to track data that changes over the life-cycle of an application
	1. Example: Udemy
		1. `searchQuery`
		2. `shoppingCart`
		3. `coupons`
		4. `notifications`
		5. `language`
		6. `isOpen`
		7. `user`
	2. Questions:
		1. How do we know we need these pieces of state?
		2. How do we know where to place them (inside the code)?
	3. Answer: State management
		1. It can be defined in different ways by different people
		2. A definition:
			1. **State management:** (Giving each piece of state a **home** - it becomes important as the application grows)
				1. Deciding **when** to define pieces of state
				2. What **types** of state are necessary
				3. **Where** to place each piece of state
				4. How data **flows** through the app

#### Types of State: Local vs. Global State ####
1. Local State
	1. State needed **only by one or few components** (child or sibling components)
	2. State that is defined in a component and **only that component and child components** have access to it (by passing via props)
		1. Using `useState` inside a component
			1. Example: Input text in the search-bar (only that component needs to know about the state)
2. Global State
	1. State that **many components** (in the app) might need
	2. **Shared** state that is accessible to **every component** in the entire application
		1. Shared between all components
	3. Implementation:
		1. Context API (React's)
		2. Redux
			1. External global state management library
	4. Example:
		1. Udemy: Shopping cart
			1. Almost all components needs access to this state
4. **Important guideline: We should always start with local state**
	1. Move it to Global state if we truly need it

#### State: When and Where? ####
1. If we realize that we: Need to store data
	1. When does this happen?
		1. Ask: Will data change at some point?
			1. If No: Regular `const` variable
			2. If Yes:
				1. Can it be computed from existing state/props?
					1. Yes: **Derive state** (calculate it based on already existing state or prop)
					2. No:
						1. Should it re-render component? (because, updating state always re-renders a component)
							1. No: Ref (`useRef` (it persists data over time, but does not re-render a component, later)
							2. Yes:
								1. **Place a new piece of state in component** (Using `useState`) (in the component we are building)
									1. Always start with local state
	2. Where to place state?
		1. Is state used by only this component?
			1. Yes: Leave it in the component
			2. No:
				1. Also used by a child component?
					1. Yes: Pass the state to child via props
					2. No:
						1. Is the state used by one or a few sibling components (or parent component)?
							1. Yes: **Lift state up to first common parent component**
								1. **Lifting state up**
							2. No (Used by many other components):
								1. Probably **global state**. Global state management later in the course
3. The above becomes intuitive later

### Thinking About State and Lifting State Up ###
1. Flow chart for items:
	1. Will data change at some point?
		1. Yes: Each time we add a new item to the items list
	2. Can the data be computed from existing state/props?
		1. No: We cannot derive the state
	3. Should it re-render component (whenever it is updated)?
		1. Yes
	4. **Place a new piece of state in the component**
	5. Was it only used by this component?
		1. No
	6. Is the state also needed by a child component?
		1. No: It is used by a sibling component
			1. **Lift state up to first common parent**
2. Code:

		import { useState } from "react";

		const initialItems = [
		  { id: 1, description: "Passports", quantity: 2, packed: false },
		  { id: 2, description: "Socks", quantity: 12, packed: true },
		  { id: 3, description: "Charger", quantity: 1, packed: false },
		];
		
		export default function App() {
		  const [items, setItems] = useState([]);
		
		  // The state and logic to update the state are in this component (the home of the state)
		  // The function is passed as a prop
		  // This is lifting-up a state
		  function handleAddItem(item) {
		    setItems((items) => [...items, item]);
		  }
		
		  return (
		    <div className="app">
		      <Logo />
		      <Form onAddItem={handleAddItem} />
		      <PackingList items={items} />
		      <Stats />
		    </div>
		  );
		}
		
		function Logo() {
		  return <h1>🌴 Far Away 🎒</h1>;
		}
		
		function Form({ onAddItem }) {
		  const [description, setDescription] = useState("");
		  const [quantity, setQuantity] = useState(1);
		
		  function handleSubmit(e) {
		    e.preventDefault();
		
		    if (!description) return;
		
		    const newItem = { description, quantity, packed: false, id: Date.now() };
		
		    console.log(newItem);
		
		    onAddItem(newItem);
		
		    // Allowing React to keep state in sync with Form elements
		    setDescription("");
		    setQuantity(1);
		  }
		
		  return (
		    <form className="add-form" onSubmit={handleSubmit}>
		      <h3>What do you need for your trip?</h3>
		      <select
		        value={quantity}
		        onChange={(e) => setQuantity(Number(e.target.value))}
		      >
		        {Array.from({ length: 20 }, (_, i) => i + 1).map((num) => (
		          <option key={num} value={num}>
		            {num}
		          </option>
		        ))}
		      </select>
		      <input
		        type="text"
		        placeholder="Item..."
		        value={description}
		        onChange={(e) => setDescription(e.target.value)}
		      />
		      <button>Add</button>
		      {/* <button onClick={handleClick}>Add</button> */}
		    </form>
		  );
		}
		
		function PackingList({ items }) {
		  return (
		    <div className="list">
		      <ul className="list">
		        {items.map((item) => (
		          <Item item={item} key={item.id} />
		        ))}
		      </ul>
		    </div>
		  );
		}
		
		function Item({ item }) {
		  return (
		    <li>
		      <span style={item.packed ? { textDecoration: "line-through" } : {}}>
		        {item.quantity} {item.description}
		      </span>
		      <button>❌</button>
		    </li>
		  );
		}
		
		function Stats() {
		  return (
		    <footer className="stats">
		      <em>💼 You have X items on your list, and you already packed X (X%)</em>
		    </footer>
		  );
		}

### Reviewing "Lifting Up State" ###
#### Problem: Sharing State with Sibling Component ####
1. Example:
	1. Checkout
		1. Promotions (user can input a coupon codes - they will be added to a list of coupons) (It is local to promotions component along with `setCoupons` function)
			1. coupons
			2. setCoupons
		2. Total
			1. Needs access to `coupons` state
				1. To know what discounts to apply and what price to display
				2. How to give access to `coupons` state?
					1. Solution: Lift it up
2. Lift state up:
	1. To place a state in a component that is a parent of both components that need the state in question
		1. Example: We lift `coupons` and `setState` to `Checkout` component (state was lifted up to the closest common parent)
	2. Giving access to the state to both the components is just passing it using props to them
	3. By lifting state up, we have successfully shared one piece of state with multiple components in different positions in the component tree
	4. **We must really get used to this pattern**
		1. We need this pattern because of `React`'s one-way data flow
3. What will happen if user adds a new coupon?
	1. How to update the `coupons` state?
		1. We cannot mutate props
		2. If data flows from parent to children, how can `Promotions` (child) update state in `Checkout` (parent)?
			1. Solution: Pass `setCoupons` function as a prop to the component that needs to update the state
				2. The child component can call the function to update the state in the parent component
	2. **Child-to-parent communication (inverse data flow):** child updating parent state (data "flowing" **up**)

### Deleting an Item: More Child-to-Parent Communication! ###
1. Code:

		import { useState } from "react";

		const initialItems = [
		  { id: 1, description: "Passports", quantity: 2, packed: false },
		  { id: 2, description: "Socks", quantity: 12, packed: true },
		  { id: 3, description: "Charger", quantity: 1, packed: false },
		];
		
		export default function App() {
		  const [items, setItems] = useState([]);
		
		  // The state and logic to update the state are in this component (the home of the state)
		  // The function is passed as a prop
		  // This is lifting-up a state
		  function handleAddItem(item) {
		    setItems((items) => [...items, item]);
		  }
		
		  function handleDeleteItem(id) {
		    setItems((items) => items.filter((item) => item.id !== id));
		  }
		
		  return (
		    <div className="app">
		      <Logo />
		      <Form onAddItem={handleAddItem} />
		      <PackingList items={items} onDeleteItem={handleDeleteItem} />
		      <Stats />
		    </div>
		  );
		}
		
		function Logo() {
		  return <h1>🌴 Far Away 🎒</h1>;
		}
		
		function Form({ onAddItem }) {
		  const [description, setDescription] = useState("");
		  const [quantity, setQuantity] = useState(1);
		
		  function handleSubmit(e) {
		    e.preventDefault();
		
		    if (!description) return;
		
		    const newItem = { description, quantity, packed: false, id: Date.now() };
		
		    console.log(newItem);
		
		    onAddItem(newItem);
		
		    // Allowing React to keep state in sync with Form elements
		    setDescription("");
		    setQuantity(1);
		  }
		
		  return (
		    <form className="add-form" onSubmit={handleSubmit}>
		      <h3>What do you need for your trip?</h3>
		      <select
		        value={quantity}
		        onChange={(e) => setQuantity(Number(e.target.value))}
		      >
		        {Array.from({ length: 20 }, (_, i) => i + 1).map((num) => (
		          <option key={num} value={num}>
		            {num}
		          </option>
		        ))}
		      </select>
		      <input
		        type="text"
		        placeholder="Item..."
		        value={description}
		        onChange={(e) => setDescription(e.target.value)}
		      />
		      <button>Add</button>
		      {/* <button onClick={handleClick}>Add</button> */}
		    </form>
		  );
		}
		
		function PackingList({ items, onDeleteItem }) {
		  return (
		    <div className="list">
		      <ul className="list">
		        {items.map((item) => (
		          <Item item={item} key={item.id} onDeleteItem={onDeleteItem} />
		        ))}
		      </ul>
		    </div>
		  );
		}
		
		function Item({ item, onDeleteItem }) {
		  return (
		    <li>
		      <span style={item.packed ? { textDecoration: "line-through" } : {}}>
		        {item.quantity} {item.description}
		      </span>
		      <button onClick={() => onDeleteItem(item.id)}>❌</button>
		    </li>
		  );
		}
		
		function Stats() {
		  return (
		    <footer className="stats">
		      <em>💼 You have X items on your list, and you already packed X (X%)</em>
		    </footer>
		  );
		}

### Updating an Item: Complex Immutable Data Operation ###
1. Code:

		import { useState } from "react";

		const initialItems = [
		  { id: 1, description: "Passports", quantity: 2, packed: false },
		  { id: 2, description: "Socks", quantity: 12, packed: true },
		  { id: 3, description: "Charger", quantity: 1, packed: false },
		];
		
		export default function App() {
		  const [items, setItems] = useState([]);
		
		  // The state and logic to update the state are in this component (the home of the state)
		  // The function is passed as a prop
		  // This is lifting-up a state
		  function handleAddItem(item) {
		    setItems((items) => [...items, item]);
		  }
		
		  function handleDeleteItem(id) {
		    setItems((items) => items.filter((item) => item.id !== id));
		  }
		
		  function handleToggleItem(id) {
		    setItems((items) =>
		      items.map((item) =>
		        item.id === id ? { ...item, packed: !item.packed } : item
		      )
		    );
		  }
		
		  return (
		    <div className="app">
		      <Logo />
		      <Form onAddItem={handleAddItem} />
		      <PackingList
		        items={items}
		        onDeleteItem={handleDeleteItem}
		        onToggleItem={handleToggleItem}
		      />
		      <Stats />
		    </div>
		  );
		}
		
		function Logo() {
		  return <h1>🌴 Far Away 🎒</h1>;
		}
		
		function Form({ onAddItem }) {
		  const [description, setDescription] = useState("");
		  const [quantity, setQuantity] = useState(1);
		
		  function handleSubmit(e) {
		    e.preventDefault();
		
		    if (!description) return;
		
		    const newItem = { description, quantity, packed: false, id: Date.now() };
		
		    console.log(newItem);
		
		    onAddItem(newItem);
		
		    // Allowing React to keep state in sync with Form elements
		    setDescription("");
		    setQuantity(1);
		  }
		
		  return (
		    <form className="add-form" onSubmit={handleSubmit}>
		      <h3>What do you need for your trip?</h3>
		      <select
		        value={quantity}
		        onChange={(e) => setQuantity(Number(e.target.value))}
		      >
		        {Array.from({ length: 20 }, (_, i) => i + 1).map((num) => (
		          <option key={num} value={num}>
		            {num}
		          </option>
		        ))}
		      </select>
		      <input
		        type="text"
		        placeholder="Item..."
		        value={description}
		        onChange={(e) => setDescription(e.target.value)}
		      />
		      <button>Add</button>
		      {/* <button onClick={handleClick}>Add</button> */}
		    </form>
		  );
		}
		
		function PackingList({ items, onDeleteItem, onToggleItem }) {
		  return (
		    <div className="list">
		      <ul className="list">
		        {items.map((item) => (
		          <Item
		            item={item}
		            key={item.id}
		            onDeleteItem={onDeleteItem}
		            onToggleItem={onToggleItem}
		          />
		        ))}
		      </ul>
		    </div>
		  );
		}
		
		function Item({ item, onDeleteItem, onToggleItem }) {
		  return (
		    <li>
		      <input
		        type="checkbox"
		        value={item.packed}
		        onChange={() => {
		          onToggleItem(item.id);
		        }}
		      />
		      <span style={item.packed ? { textDecoration: "line-through" } : {}}>
		        {item.quantity} {item.description}
		      </span>
		      <button onClick={() => onDeleteItem(item.id)}>❌</button>
		    </li>
		  );
		}
		
		function Stats() {
		  return (
		    <footer className="stats">
		      <em>💼 You have X items on your list, and you already packed X (X%)</em>
		    </footer>
		  );
		}

### Derived State ###
1. Derived state: state that is computed from an existing piece of state or from props
	1. Example: Three separate pieces of state, even though `numItems`, and `totalPrice` depend on `cart`
	2. Problems:
		1. Need to keep them in sync (update together)
			1. Whenever we update `cart`, we need to update `numItems`, and `totalPrice`
		2. 3 state updates will cause 3 re-renders
	3. Solution:
		1. We can derive `numItems`, and `totalPrice` from `cart` and store them in separate variables

				const numItems = cart.length
				const totalPrice = cart.reduce((acc, cur) => acc + cur.price, 0);

	4. Just regular variables, no `useState`
	5. `cart` state is the **single source of truth** for this related data
		1. Everything will stay in sync
			1. If `cart` is updated, the component is re-rendered, the function is called again as a result, and the other variables are updated
	6. Works because re-rendering component will **automatically re-calculate** derived state
	7. If one state can be computed from another, prefer derived state

### Calculating Statistics as Derived State ###
1. Code:

		function Stats({ items }) {
		  if (!items.length)
		    return (
		      <p className="stats">
		        <em>Start adding some items to your packing list 🚀</em>
		      </p>
		    );
		
		  const numItems = items.length;
		  const numPacked = items.filter((item) => item.packed).length;
		  const percentage = Math.round((numPacked / numItems) * 100);
		
		  return (
		    <footer className="stats">
		      <em>
		        {percentage === 100
		          ? "You got everything! Ready to go ✈️"
		          : `💼 You have ${numItems} items on your list, and you already packed ${numPacked} (${percentage}%)`}
		      </em>
		    </footer>
		  );
		}

### Sorting Items ###
1. Code:

		function PackingList({ items, onDeleteItem, onToggleItem }) {
		  const [sortBy, setSortBy] = useState("input");
		
		  let sortedItems;
		
		  if (sortBy === "input") sortedItems = items;
		  if (sortBy === "description")
		    sortedItems = items
		      .slice()
		      .sort((a, b) => a.description.localeCompare(b.description));
		
		  if (sortBy === "packed")
		    sortedItems = items
		      .slice()
		      .sort((a, b) => Number(a.packed) - Number(b.packed));
		
		  return (
		    <div className="list">
		      <ul className="list">
		        {sortedItems.map((item) => (
		          <Item
		            item={item}
		            key={item.id}
		            onDeleteItem={onDeleteItem}
		            onToggleItem={onToggleItem}
		          />
		        ))}
		      </ul>
		
		      <div className="actions">
		        <select value={sortBy} onChange={(e) => setSortBy(e.target.value)}>
		          <option value="input">Sort by input order</option>
		          <option value="description">Sort by description</option>
		          <option value="packed">Sort by packed status</option>
		        </select>
		      </div>
		    </div>
		  );
		}

### Clearing the List ###
1. Code:

		import { useState } from "react";

		const initialItems = [
		  { id: 1, description: "Passports", quantity: 2, packed: false },
		  { id: 2, description: "Socks", quantity: 12, packed: true },
		  { id: 3, description: "Charger", quantity: 1, packed: false },
		];
		
		export default function App() {
		  const [items, setItems] = useState([]);
		
		  // The state and logic to update the state are in this component (the home of the state)
		  // The function is passed as a prop
		  // This is lifting-up a state
		  function handleAddItem(item) {
		    setItems((items) => [...items, item]);
		  }
		
		  function handleDeleteItem(id) {
		    setItems((items) => items.filter((item) => item.id !== id));
		  }
		
		  function handleToggleItem(id) {
		    setItems((items) =>
		      items.map((item) =>
		        item.id === id ? { ...item, packed: !item.packed } : item
		      )
		    );
		  }
		
		  function handleClearItems() {
		    const confirmed = window.confirm(
		      "Are you sure you want to delete all items?"
		    );
		    if (confirmed) setItems(() => []);
		  }
		
		  return (
		    <div className="app">
		      <Logo />
		      <Form onAddItem={handleAddItem} />
		      <PackingList
		        items={items}
		        onDeleteItem={handleDeleteItem}
		        onToggleItem={handleToggleItem}
		        onClearItems={handleClearItems}
		      />
		      <Stats items={items} />
		    </div>
		  );
		}
		
		function Logo() {
		  return <h1>🌴 Far Away 🎒</h1>;
		}
		
		function Form({ onAddItem }) {
		  const [description, setDescription] = useState("");
		  const [quantity, setQuantity] = useState(1);
		
		  function handleSubmit(e) {
		    e.preventDefault();
		
		    if (!description) return;
		
		    const newItem = { description, quantity, packed: false, id: Date.now() };
		
		    console.log(newItem);
		
		    onAddItem(newItem);
		
		    // Allowing React to keep state in sync with Form elements
		    setDescription("");
		    setQuantity(1);
		  }
		
		  return (
		    <form className="add-form" onSubmit={handleSubmit}>
		      <h3>What do you need for your trip?</h3>
		      <select
		        value={quantity}
		        onChange={(e) => setQuantity(Number(e.target.value))}
		      >
		        {Array.from({ length: 20 }, (_, i) => i + 1).map((num) => (
		          <option key={num} value={num}>
		            {num}
		          </option>
		        ))}
		      </select>
		      <input
		        type="text"
		        placeholder="Item..."
		        value={description}
		        onChange={(e) => setDescription(e.target.value)}
		      />
		      <button>Add</button>
		      {/* <button onClick={handleClick}>Add</button> */}
		    </form>
		  );
		}
		
		function PackingList({ items, onDeleteItem, onToggleItem, onClearItems }) {
		  const [sortBy, setSortBy] = useState("input");
		
		  let sortedItems;
		
		  if (sortBy === "input") sortedItems = items;
		  if (sortBy === "description")
		    sortedItems = items
		      .slice()
		      .sort((a, b) => a.description.localeCompare(b.description));
		
		  if (sortBy === "packed")
		    sortedItems = items
		      .slice()
		      .sort((a, b) => Number(a.packed) - Number(b.packed));
		
		  return (
		    <div className="list">
		      <ul className="list">
		        {sortedItems.map((item) => (
		          <Item
		            item={item}
		            key={item.id}
		            onDeleteItem={onDeleteItem}
		            onToggleItem={onToggleItem}
		          />
		        ))}
		      </ul>
		
		      <div className="actions">
		        <select value={sortBy} onChange={(e) => setSortBy(e.target.value)}>
		          <option value="input">Sort by input order</option>
		          <option value="description">Sort by description</option>
		          <option value="packed">Sort by packed status</option>
		        </select>
		        <button onClick={onClearItems}>Clear List</button>
		      </div>
		    </div>
		  );
		}
		
		function Item({ item, onDeleteItem, onToggleItem }) {
		  return (
		    <li>
		      <input
		        type="checkbox"
		        value={item.packed}
		        onChange={() => {
		          onToggleItem(item.id);
		        }}
		      />
		      <span style={item.packed ? { textDecoration: "line-through" } : {}}>
		        {item.quantity} {item.description}
		      </span>
		      <button onClick={() => onDeleteItem(item.id)}>❌</button>
		    </li>
		  );
		}
		
		function Stats({ items }) {
		  if (!items.length)
		    return (
		      <p className="stats">
		        <em>Start adding some items to your packing list 🚀</em>
		      </p>
		    );
		
		  const numItems = items.length;
		  const numPacked = items.filter((item) => item.packed).length;
		  const percentage = Math.round((numPacked / numItems) * 100);
		
		  return (
		    <footer className="stats">
		      <em>
		        {percentage === 100
		          ? "You got everything! Ready to go ✈️"
		          : `💼 You have ${numItems} items on your list, and you already packed ${numPacked} (${percentage}%)`}
		      </em>
		    </footer>
		  );
		}

### Moving Components Into Separate Files ###
1. Select the component
	1. Right click > Refactor > Move to a new file
2. We use Default exports for components

### EXERCISE #1: Accordion Component (v1) ###
1. Code:

		import "./styles.css";
		import { useState } from "react";
		
		const faqs = [
		  {
		    title: "Where are these chairs assembled?",
		    text: "Lorem ipsum dolor sit amet consectetur, adipisicing elit. Accusantium, quaerat temporibus quas dolore provident nisi ut aliquid ratione beatae sequi aspernatur veniam repellendus.",
		  },
		  {
		    title: "How long do I have to return my chair?",
		    text: "Pariatur recusandae dignissimos fuga voluptas unde optio nesciunt commodi beatae, explicabo natus.",
		  },
		  {
		    title: "Do you ship to countries outside the EU?",
		    text: "Excepturi velit laborum, perspiciatis nemo perferendis reiciendis aliquam possimus dolor sed! Dolore laborum ducimus veritatis facere molestias!",
		  },
		];
		
		export default function App() {
		  return (
		    <div>
		      <Accordion data={faqs} />
		    </div>
		  );
		}
		
		function Accordion({ data }) {
		  return (
		    <div className="accordion">
		      {data.map((el, i) => (
		        <AccordionItem num={i} title={el.title} text={el.text} key={el.title} />
		      ))}
		    </div>
		  );
		}
		
		function AccordionItem({ num, title, text }) {
		  const [isOpen, setIsOpen] = useState(false);
		
		  function handleToggle() {
		    setIsOpen((isOpen) => !isOpen);
		  }
		
		  return (
		    <div className={`item ${isOpen ? "open" : ""}`} onClick={handleToggle}>
		      <p className="number">{num < 9 ? `0${num + 1}` : num + 1}</p>
		      <p className="text">{title}</p>
		      <p className="icon">{isOpen ? "-" : "+"}</p>
		      {isOpen && <div className="content-box">{text}</div>}
		    </div>
		  );
		}

### The "children" Prop: Making a Reusable Button ###
1. `children` prop is a prop that each React component automatically receives.
	1. The value of `children` is the one between opening and closing tag of the component
		1. One of the most useful features
			1. Makes the component truly re-usable
		2. The component will just take the JSX and render it
			1. A hole that can be filled by us passing the content into the component

#### The Children Prop ####
1. Button:
	1. props.children
		1. An empty **"hole"** that can be filled by **any JSX the component receives** as children
	2. How do we pass in the children?
		1. JSX in between opening and closing tags of the component
			1. Example: Children of `Button`, accessible through `props.children`
2. The children prop allow us **to pass JSX into an element** (besides regular props)
3. Essential tools to make **reusable** and **configurable** components (especially component **content**)
	1. Example, we want a button with diferent emojis and text
		1. Pass in a different JSX, and the button will get completely different content
4. Really useful for **generic** components that **don't know their content** before being used (e.g. modal)
	1. Generic Slider
	2. Generic Button
	3. ...

### More Reusable With the "children" Prop ###
1. Code:

		import { useState } from "react";

		const messages = [
		  "Learn React ⚛️",
		  "Apply for jobs 💼",
		  "Invest your new income 🤑",
		];
		
		export default function App() {
		  return (
		    <div>
		      <Steps />
		      <StepMessage step={1}>
		        <p>Pass in content</p>
		        <p>🌴</p>
		      </StepMessage>
		    </div>
		  );
		}
		
		function Steps() {
		  // const step = 1;
		  // 1. Add a new state variables
		  // 2. We use it in code (usually in JSX)
		  // 3. We update the state in an event-handler
		  const [step, setStep] = useState(1); // takes a default value
		  const [isOpen, setIsOpen] = useState(true);
		
		  function handlePrevious() {
		    // `handle<Name>` is standard
		    if (step > 1) setStep((s) => s - 1);
		  }
		
		  function handleNext() {
		    // `handle<Name>` is standard
		    if (step < 3) setStep((s) => s + 1);
		  }
		
		  return (
		    <div>
		      <button className="close" onClick={() => setIsOpen((io) => !io)}>
		        &times;
		      </button>
		      {isOpen && (
		        <div className="steps">
		          <div className="numbers">
		            <div className={step >= 1 ? "active" : ""}>1</div>
		            <div className={step >= 2 ? "active" : ""}>2</div>
		            <div className={step >= 3 ? "active" : ""}>3</div>
		          </div>
		
		          <StepMessage step={step}>
		            {messages[step - 1]}
		            <div className="buttons">
		              <Button
		                bgColor="#e7e7e7"
		                textColor="#333"
		                onClick={() => alert(`Learn how to ${messages[step - 1]}`)}
		              >
		                Learn how
		              </Button>
		            </div>
		          </StepMessage>
		
		          <div className="buttons">
		            <Button bgColor="#7950f2" textColor="#fff" onClick={handlePrevious}>
		              <span>⬅️</span> Previous
		            </Button>
		            <Button bgColor="#7950f2" textColor="#fff" onClick={handleNext}>
		              Next <span>➡️</span>
		            </Button>
		          </div>
		        </div>
		      )}
		    </div>
		  );
		}
		
		function StepMessage({ step, children }) {
		  return (
		    <div className="message">
		      <h3>Step {step}</h3>
		      {children}
		    </div>
		  );
		}
		
		function Button({ textColor, bgColor, onClick, children }) {
		  return (
		    <button
		      style={{ backgroundColor: bgColor, color: textColor }}
		      onClick={onClick}
		    >
		      {children}
		    </button>
		  );
		}

### EXERCISE #2: Accordion Component (v2) ###
1. Code:

		import { useState } from "react";

		const messages = [
		  "Learn React ⚛️",
		  "Apply for jobs 💼",
		  "Invest your new income 🤑",
		];
		
		export default function App() {
		  return (
		    <div>
		      <Steps />
		      <StepMessage step={1}>
		        <p>Pass in content</p>
		        <p>🌴</p>
		      </StepMessage>
		    </div>
		  );
		}
		
		function Steps() {
		  // const step = 1;
		  // 1. Add a new state variables
		  // 2. We use it in code (usually in JSX)
		  // 3. We update the state in an event-handler
		  const [step, setStep] = useState(1); // takes a default value
		  const [isOpen, setIsOpen] = useState(true);
		
		  function handlePrevious() {
		    // `handle<Name>` is standard
		    if (step > 1) setStep((s) => s - 1);
		  }
		
		  function handleNext() {
		    // `handle<Name>` is standard
		    if (step < 3) setStep((s) => s + 1);
		  }
		
		  return (
		    <div>
		      <button className="close" onClick={() => setIsOpen((io) => !io)}>
		        &times;
		      </button>
		      {isOpen && (
		        <div className="steps">
		          <div className="numbers">
		            <div className={step >= 1 ? "active" : ""}>1</div>
		            <div className={step >= 2 ? "active" : ""}>2</div>
		            <div className={step >= 3 ? "active" : ""}>3</div>
		          </div>
		
		          <StepMessage step={step}>
		            {messages[step - 1]}
		            <div className="buttons">
		              <Button
		                bgColor="#e7e7e7"
		                textColor="#333"
		                onClick={() => alert(`Learn how to ${messages[step - 1]}`)}
		              >
		                Learn how
		              </Button>
		            </div>
		          </StepMessage>
		
		          <div className="buttons">
		            <Button bgColor="#7950f2" textColor="#fff" onClick={handlePrevious}>
		              <span>⬅️</span> Previous
		            </Button>
		            <Button bgColor="#7950f2" textColor="#fff" onClick={handleNext}>
		              Next <span>➡️</span>
		            </Button>
		          </div>
		        </div>
		      )}
		    </div>
		  );
		}
		
		function StepMessage({ step, children }) {
		  return (
		    <div className="message">
		      <h3>Step {step}</h3>
		      {children}
		    </div>
		  );
		}
		
		function Button({ textColor, bgColor, onClick, children }) {
		  return (
		    <button
		      style={{ backgroundColor: bgColor, color: textColor }}
		      onClick={onClick}
		    >
		      {children}
		    </button>
		  );
		}

### CHALLENGE #1: Tip Calculator ###
1. Code:

		import { useState } from "react";
		import "./App.css";
		
		function App() {
		  const tipValues = [0, 5, 10, 20];
		  const [bill, setBill] = useState(0);
		  const [firstTip, setFirstTip] = useState(tipValues[0]);
		  const [secondTip, setSecondTip] = useState(tipValues[0]);
		  let tip = (firstTip + secondTip) * bill * 0.005;
		  let total = bill + tip;
		
		  function handleReset() {
		    setBill(0);
		    setFirstTip(tipValues[0]);
		    setSecondTip(tipValues[0]);
		  }
		
		  return (
		    <div>
		      <BillInput bill={bill} onBillChange={setBill} />
		      <SelectPercentage
		        text="How did you like the service?"
		        tipValues={tipValues}
		        tip={firstTip}
		        onTipChange={setFirstTip}
		      />
		      <SelectPercentage
		        text="How did your friend like the service?"
		        tipValues={tipValues}
		        tip={secondTip}
		        onTipChange={setSecondTip}
		      />
		      {total > 0 ? (
		        <Output bill={bill} tip={tip} total={total} />
		      ) : (
		        <h2>&nbsp;</h2>
		      )}
		      <button onClick={handleReset}>Reset</button>
		    </div>
		  );
		}
		
		function BillInput({ bill, onBillChange }) {
		  function handleBillChange(bill) {
		    onBillChange(Number(bill));
		  }
		
		  return (
		    <div>
		      <span>How much was the bill?</span>
		      <input
		        type="text"
		        value={bill}
		        onChange={(e) => handleBillChange(e.target.value)}
		      ></input>
		    </div>
		  );
		}
		
		function SelectPercentage({ text, tipValues, tip, onTipChange }) {
		  function handleTipChange(newTip) {
		    onTipChange(Number(newTip));
		  }
		
		  return (
		    <div>
		      <span>{text}</span>
		      <select value={tip} onChange={(e) => handleTipChange(e.target.value)}>
		        <option value={tipValues[0]}>Dissatisfied (0%)</option>
		        <option value={tipValues[1]}>It was okay (5%)</option>
		        <option value={tipValues[2]}>It was good (10%)</option>
		        <option value={tipValues[3]}>Absolutely Amazing (20%)</option>
		      </select>
		    </div>
		  );
		}
		
		function Output({ bill, tip, total }) {
		  return <h2>{`You pay $${total} ($${bill} + $${tip} tp)`}</h2>;
		}
		
		export default App;

## Section 8: [Optional] Practice Project: Eat-'N-Split ##
### Section Overview ###
1. Topics:
	1. **Review** everything we learned
	2. **No** new concepts!
	3. This practice is **extremely important for your progress**

### Project Setup ###
1. `npx create-reate-app@5 eat-n-split`
2. We can go to dinner or lunch and split the bill
3. Split UI into components
	1. It is subjective
		1. We have some techniques
	2. `FriendList`
		1. `Friend`
	3. `Form`
	4. `BillData`

### Building the Static App: List of Friends ###
1. Code:

		const initialFriends = [
		  {
		    id: 118836,
		    name: "Clark",
		    image: "https://i.pravatar.cc/48?u=118836",
		    balance: -7,
		  },
		  {
		    id: 933372,
		    name: "Sarah",
		    image: "https://i.pravatar.cc/48?u=933372",
		    balance: 20,
		  },
		  {
		    id: 499476,
		    name: "Anthony",
		    image: "https://i.pravatar.cc/48?u=499476",
		    balance: 0,
		  },
		];
		
		export default function App() {
		  return (
		    <div className="app">
		      <div className="sidebar">
		        <FriendsList />
		      </div>
		    </div>
		  );
		}
		
		function FriendsList() {
		  const friends = initialFriends;
		
		  return (
		    <ul>
		      {friends.map((friend) => (
		        <Friend friend={friend} key={friend.id} />
		      ))}
		    </ul>
		  );
		}
		
		function Friend({ friend }) {
		  return (
		    <li key={friend.id}>
		      <img src={friend.image} alt={friend.name} />
		      <h3>{friend.name}</h3>
		      {friend.balance < 0 && (
		        <p className="red">
		          You owe {friend.name} {Math.abs(friend.balance)}💶
		        </p>
		      )}
		      {friend.balance > 0 && (
		        <p className="green">
		          {friend.name} owes you {Math.abs(friend.balance)}💶
		        </p>
		      )}
		      {friend.balance === 0 && <p>You and {friend.name} are even</p>}
		
		      <button className="button">Select</button>
		    </li>
		  );
		}

### Building the Static App: Forms ###
1. Code:

		const initialFriends = [
		  {
		    id: 118836,
		    name: "Clark",
		    image: "https://i.pravatar.cc/48?u=118836",
		    balance: -7,
		  },
		  {
		    id: 933372,
		    name: "Sarah",
		    image: "https://i.pravatar.cc/48?u=933372",
		    balance: 20,
		  },
		  {
		    id: 499476,
		    name: "Anthony",
		    image: "https://i.pravatar.cc/48?u=499476",
		    balance: 0,
		  },
		];
		
		export default function App() {
		  return (
		    <div className="app">
		      <div className="sidebar">
		        <FriendsList />
		        <FormAddFriend />
		        <Button>Add Friend</Button>
		      </div>
		
		      <FormSplitBill />
		    </div>
		  );
		}
		
		function FriendsList() {
		  const friends = initialFriends;
		
		  return (
		    <ul>
		      {friends.map((friend) => (
		        <Friend friend={friend} key={friend.id} />
		      ))}
		    </ul>
		  );
		}
		
		function Friend({ friend }) {
		  return (
		    <li key={friend.id}>
		      <img src={friend.image} alt={friend.name} />
		      <h3>{friend.name}</h3>
		      {friend.balance < 0 && (
		        <p className="red">
		          You owe {friend.name} {Math.abs(friend.balance)}💶
		        </p>
		      )}
		      {friend.balance > 0 && (
		        <p className="green">
		          {friend.name} owes you {Math.abs(friend.balance)}💶
		        </p>
		      )}
		      {friend.balance === 0 && <p>You and {friend.name} are even</p>}
		
		      <Button>Select</Button>
		    </li>
		  );
		}
		
		function Button({ children }) {
		  return <button className="button">{children}</button>;
		}
		
		function FormAddFriend() {
		  return (
		    <form className="form-add-friend">
		      <label>🎳 Friend name</label>
		      <input type="text" />
		
		      <label>🖼️ Image URL</label>
		      <input type="text" />
		
		      <Button>Add</Button>
		    </form>
		  );
		}
		
		function FormSplitBill() {
		  return (
		    <form className="form-split-bill">
		      <h2>Split a bill with X</h2>
		
		      <label>💶 Bill Value</label>
		      <input type="text" />
		
		      <label>💰 Your expense</label>
		      <input type="text" />
		
		      <label>🏸 X's expense</label>
		      <input type="text" disabled />
		
		      <label>🪙 Who is paying the bill</label>
		      <select>
		        <option value="user">You</option>
		        <option value="friend">X</option>
		      </select>
		
		      <Button>Split Bill</Button>
		    </form>
		  );
		}

### Displaying the New Friend Form ###
1. If we want UI to re-render, we might need a state
2. Code:

		function Button({ children, onClick }) {
		  return (
		    <button className="button" onClick={onClick}>
		      {children}
		    </button>
		  );
		}
		
		export default function App() {
		  const [showAddFriend, setShowAddFriend] = useState(false);
		
		  function handleShowAddFriend() {
		    setShowAddFriend((show) => !show);
		  }
		
		  return (
		    <div className="app">
		      <div className="sidebar">
		        <FriendsList />
		        {showAddFriend && <FormAddFriend />}
		        <Button onClick={handleShowAddFriend}>
		          {showAddFriend ? "Close" : "Add Friend"}
		        </Button>
		      </div>
		
		      <FormSplitBill />
		    </div>
		  );
		}

### Adding a New Friend ###
1. Code:

		import { useState } from "react";

		const initialFriends = [
		  {
		    id: 118836,
		    name: "Clark",
		    image: "https://i.pravatar.cc/48?u=118836",
		    balance: -7,
		  },
		  {
		    id: 933372,
		    name: "Sarah",
		    image: "https://i.pravatar.cc/48?u=933372",
		    balance: 20,
		  },
		  {
		    id: 499476,
		    name: "Anthony",
		    image: "https://i.pravatar.cc/48?u=499476",
		    balance: 0,
		  },
		];
		
		function Button({ children, onClick }) {
		  return (
		    <button className="button" onClick={onClick}>
		      {children}
		    </button>
		  );
		}
		
		export default function App() {
		  const [friends, setFriends] = useState(initialFriends);
		  const [showAddFriend, setShowAddFriend] = useState(false);
		
		  function handleShowAddFriend() {
		    setShowAddFriend((show) => !show);
		  }
		
		  function handleAddFriend(friend) {
		    setFriends((friends) => [...friends, friend]);
		    setShowAddFriend(false);
		  }
		
		  return (
		    <div className="app">
		      <div className="sidebar">
		        <FriendsList friends={friends} />
		        {showAddFriend && <FormAddFriend onAddFriend={handleAddFriend} />}
		        <Button onClick={handleShowAddFriend}>
		          {showAddFriend ? "Close" : "Add Friend"}
		        </Button>
		      </div>
		
		      <FormSplitBill />
		    </div>
		  );
		}
		
		function FriendsList({ friends }) {
		  return (
		    <ul>
		      {friends.map((friend) => (
		        <Friend friend={friend} key={friend.id} />
		      ))}
		    </ul>
		  );
		}
		
		function Friend({ friend }) {
		  return (
		    <li key={friend.id}>
		      <img src={friend.image} alt={friend.name} />
		      <h3>{friend.name}</h3>
		      {friend.balance < 0 && (
		        <p className="red">
		          You owe {friend.name} {Math.abs(friend.balance)}💶
		        </p>
		      )}
		      {friend.balance > 0 && (
		        <p className="green">
		          {friend.name} owes you {Math.abs(friend.balance)}💶
		        </p>
		      )}
		      {friend.balance === 0 && <p>You and {friend.name} are even</p>}
		
		      <Button>Select</Button>
		    </li>
		  );
		}
		
		function FormAddFriend({ onAddFriend }) {
		  const [name, setName] = useState("");
		  const [image, setImage] = useState("https://i.pravatar.cc/48");
		
		  function handleSubmit(e) {
		    e.preventDefault();
		
		    if (!name || !image) return;
		
		    const id = crypto.randomUUID();
		    const newFriend = {
		      name,
		      image: `${image}?=${id}`,
		      balance: 0,
		      id,
		    };
		
		    onAddFriend(newFriend);
		
		    setName("");
		    setImage("https://i.pravatar.cc/48");
		  }
		
		  return (
		    <form className="form-add-friend" onSubmit={handleSubmit}>
		      <label>🎳 Friend name</label>
		      <input
		        type="text"
		        value={name}
		        onChange={(e) => setName(e.target.value)}
		      />
		
		      <label>🖼️ Image URL</label>
		      <input
		        type="text"
		        value={image}
		        onChange={(e) => setImage(e.target.value)}
		      />
		
		      <Button>Add</Button>
		    </form>
		  );
		}
		
		function FormSplitBill() {
		  return (
		    <form className="form-split-bill">
		      <h2>Split a bill with X</h2>
		
		      <label>💶 Bill Value</label>
		      <input type="text" />
		
		      <label>💰 Your expense</label>
		      <input type="text" />
		
		      <label>🏸 X's expense</label>
		      <input type="text" disabled />
		
		      <label>🪙 Who is paying the bill</label>
		      <select>
		        <option value="user">You</option>
		        <option value="friend">X</option>
		      </select>
		
		      <Button>Split Bill</Button>
		    </form>
		  );
		}

### Selecting a Friend ###
1. Code:

		import { useState } from "react";

		const initialFriends = [
		  {
		    id: 118836,
		    name: "Clark",
		    image: "https://i.pravatar.cc/48?u=118836",
		    balance: -7,
		  },
		  {
		    id: 933372,
		    name: "Sarah",
		    image: "https://i.pravatar.cc/48?u=933372",
		    balance: 20,
		  },
		  {
		    id: 499476,
		    name: "Anthony",
		    image: "https://i.pravatar.cc/48?u=499476",
		    balance: 0,
		  },
		];
		
		function Button({ children, onClick }) {
		  return (
		    <button className="button" onClick={onClick}>
		      {children}
		    </button>
		  );
		}
		
		export default function App() {
		  const [friends, setFriends] = useState(initialFriends);
		  const [showAddFriend, setShowAddFriend] = useState(false);
		  const [selectedFriend, setSelectedFriend] = useState(null);
		
		  function handleShowAddFriend() {
		    setShowAddFriend((show) => !show);
		  }
		
		  function handleAddFriend(friend) {
		    setFriends((friends) => [...friends, friend]);
		    setShowAddFriend(false);
		  }
		
		  function handleSelection(friend) {
		    // setSelectedFriend(friend);
		    setSelectedFriend((cur) => (cur?.id === friend.id ? null : friend));
		    setShowAddFriend(false);
		  }
		
		  return (
		    <div className="app">
		      <div className="sidebar">
		        <FriendsList
		          friends={friends}
		          onSelection={handleSelection}
		          selectedFriend={selectedFriend}
		        />
		        {showAddFriend && <FormAddFriend onAddFriend={handleAddFriend} />}
		        <Button onClick={handleShowAddFriend}>
		          {showAddFriend ? "Close" : "Add Friend"}
		        </Button>
		      </div>
		
		      {selectedFriend && <FormSplitBill selectedFriend={selectedFriend} />}
		    </div>
		  );
		}
		
		function FriendsList({ friends, onSelection, selectedFriend }) {
		  return (
		    <ul>
		      {friends.map((friend) => (
		        <Friend
		          friend={friend}
		          key={friend.id}
		          onSelection={onSelection}
		          selectedFriend={selectedFriend}
		        />
		      ))}
		    </ul>
		  );
		}
		
		function Friend({ friend, onSelection, selectedFriend }) {
		  const isSelected = selectedFriend?.id === friend.id;
		
		  return (
		    <li key={friend.id} className={isSelected ? "selected" : ""}>
		      <img src={friend.image} alt={friend.name} />
		      <h3>{friend.name}</h3>
		      {friend.balance < 0 && (
		        <p className="red">
		          You owe {friend.name} {Math.abs(friend.balance)}💶
		        </p>
		      )}
		      {friend.balance > 0 && (
		        <p className="green">
		          {friend.name} owes you {Math.abs(friend.balance)}💶
		        </p>
		      )}
		      {friend.balance === 0 && <p>You and {friend.name} are even</p>}
		
		      <Button onClick={() => onSelection(friend)}>
		        {isSelected ? "Close" : "Select"}
		      </Button>
		    </li>
		  );
		}
		
		function FormAddFriend({ onAddFriend }) {
		  const [name, setName] = useState("");
		  const [image, setImage] = useState("https://i.pravatar.cc/48");
		
		  function handleSubmit(e) {
		    e.preventDefault();
		
		    if (!name || !image) return;
		
		    const id = crypto.randomUUID();
		    const newFriend = {
		      name,
		      image: `${image}?=${id}`,
		      balance: 0,
		      id,
		    };
		
		    onAddFriend(newFriend);
		
		    setName("");
		    setImage("https://i.pravatar.cc/48");
		  }
		
		  return (
		    <form className="form-add-friend" onSubmit={handleSubmit}>
		      <label>🎳 Friend name</label>
		      <input
		        type="text"
		        value={name}
		        onChange={(e) => setName(e.target.value)}
		      />
		
		      <label>🖼️ Image URL</label>
		      <input
		        type="text"
		        value={image}
		        onChange={(e) => setImage(e.target.value)}
		      />
		
		      <Button>Add</Button>
		    </form>
		  );
		}
		
		function FormSplitBill({ selectedFriend }) {
		  return (
		    <form className="form-split-bill">
		      <h2>Split a bill with {selectedFriend.name}</h2>
		
		      <label>💶 Bill Value</label>
		      <input type="text" />
		
		      <label>💰 Your expense</label>
		      <input type="text" />
		
		      <label>🏸 {selectedFriend.name}'s expense</label>
		      <input type="text" disabled />
		
		      <label>🪙 Who is paying the bill</label>
		      <select>
		        <option value="user">You</option>
		        <option value="friend">{selectedFriend.name}</option>
		      </select>
		
		      <Button>Split Bill</Button>
		    </form>
		  );
		}

### Constructing Controlled Elements ###
1. Code:

		import { useState } from "react";

		const initialFriends = [
		  {
		    id: 118836,
		    name: "Clark",
		    image: "https://i.pravatar.cc/48?u=118836",
		    balance: -7,
		  },
		  {
		    id: 933372,
		    name: "Sarah",
		    image: "https://i.pravatar.cc/48?u=933372",
		    balance: 20,
		  },
		  {
		    id: 499476,
		    name: "Anthony",
		    image: "https://i.pravatar.cc/48?u=499476",
		    balance: 0,
		  },
		];
		
		function Button({ children, onClick }) {
		  return (
		    <button className="button" onClick={onClick}>
		      {children}
		    </button>
		  );
		}
		
		export default function App() {
		  const [friends, setFriends] = useState(initialFriends);
		  const [showAddFriend, setShowAddFriend] = useState(false);
		  const [selectedFriend, setSelectedFriend] = useState(null);
		
		  function handleShowAddFriend() {
		    setShowAddFriend((show) => !show);
		  }
		
		  function handleAddFriend(friend) {
		    setFriends((friends) => [...friends, friend]);
		    setShowAddFriend(false);
		  }
		
		  function handleSelection(friend) {
		    // setSelectedFriend(friend);
		    setSelectedFriend((cur) => (cur?.id === friend.id ? null : friend));
		    setShowAddFriend(false);
		  }
		
		  return (
		    <div className="app">
		      <div className="sidebar">
		        <FriendsList
		          friends={friends}
		          onSelection={handleSelection}
		          selectedFriend={selectedFriend}
		        />
		        {showAddFriend && <FormAddFriend onAddFriend={handleAddFriend} />}
		        <Button onClick={handleShowAddFriend}>
		          {showAddFriend ? "Close" : "Add Friend"}
		        </Button>
		      </div>
		
		      {selectedFriend && <FormSplitBill selectedFriend={selectedFriend} />}
		    </div>
		  );
		}
		
		function FriendsList({ friends, onSelection, selectedFriend }) {
		  return (
		    <ul>
		      {friends.map((friend) => (
		        <Friend
		          friend={friend}
		          key={friend.id}
		          onSelection={onSelection}
		          selectedFriend={selectedFriend}
		        />
		      ))}
		    </ul>
		  );
		}
		
		function Friend({ friend, onSelection, selectedFriend }) {
		  const isSelected = selectedFriend?.id === friend.id;
		
		  return (
		    <li key={friend.id} className={isSelected ? "selected" : ""}>
		      <img src={friend.image} alt={friend.name} />
		      <h3>{friend.name}</h3>
		      {friend.balance < 0 && (
		        <p className="red">
		          You owe {friend.name} {Math.abs(friend.balance)}💶
		        </p>
		      )}
		      {friend.balance > 0 && (
		        <p className="green">
		          {friend.name} owes you {Math.abs(friend.balance)}💶
		        </p>
		      )}
		      {friend.balance === 0 && <p>You and {friend.name} are even</p>}
		
		      <Button onClick={() => onSelection(friend)}>
		        {isSelected ? "Close" : "Select"}
		      </Button>
		    </li>
		  );
		}
		
		function FormAddFriend({ onAddFriend }) {
		  const [name, setName] = useState("");
		  const [image, setImage] = useState("https://i.pravatar.cc/48");
		
		  function handleSubmit(e) {
		    e.preventDefault();
		
		    if (!name || !image) return;
		
		    const id = crypto.randomUUID();
		    const newFriend = {
		      name,
		      image: `${image}?=${id}`,
		      balance: 0,
		      id,
		    };
		
		    onAddFriend(newFriend);
		
		    setName("");
		    setImage("https://i.pravatar.cc/48");
		  }
		
		  return (
		    <form className="form-add-friend" onSubmit={handleSubmit}>
		      <label>🎳 Friend name</label>
		      <input
		        type="text"
		        value={name}
		        onChange={(e) => setName(e.target.value)}
		      />
		
		      <label>🖼️ Image URL</label>
		      <input
		        type="text"
		        value={image}
		        onChange={(e) => setImage(e.target.value)}
		      />
		
		      <Button>Add</Button>
		    </form>
		  );
		}
		
		function FormSplitBill({ selectedFriend }) {
		  const [bill, setBill] = useState(""); // input text elements have ""
		  const [paidByUser, setPaidByUser] = useState("");
		  const paidByFriend = bill ? bill - paidByUser : ""; // Reset each time state is changed and component is re-rendered and the function is executed
		  const [whoIsPaying, setWhoIsPaying] = useState("user");
		
		  return (
		    <form className="form-split-bill">
		      <h2>Split a bill with {selectedFriend.name}</h2>
		
		      <label>💶 Bill Value</label>
		      <input
		        type="text"
		        value={bill}
		        onChange={(e) => setBill(Number(e.target.value))}
		      />
		
		      <label>💰 Your expense</label>
		      <input
		        type="text"
		        value={paidByUser}
		        onChange={(e) =>
		          setPaidByUser(
		            Number(e.target.value) > bill ? paidByUser : Number(e.target.value)
		          )
		        }
		      />
		
		      <label>🏸 {selectedFriend.name}'s expense</label>
		      <input type="text" disabled value={paidByFriend} />
		
		      <label>🪙 Who is paying the bill</label>
		      <select
		        value={whoIsPaying}
		        onChange={(e) => setWhoIsPaying(e.target.value)}
		      >
		        <option value="user">You</option>
		        <option value="friend">{selectedFriend.name}</option>
		      </select>
		
		      <Button>Split Bill</Button>
		    </form>
		  );
		}

	1. If we click on another user, the component is not re-rendered but a component is rendered at the same place (state will remain the same)

### Splitting a Bill ###
1. Code:

		import { useState } from "react";

		const initialFriends = [
		  {
		    id: 118836,
		    name: "Clark",
		    image: "https://i.pravatar.cc/48?u=118836",
		    balance: -7,
		  },
		  {
		    id: 933372,
		    name: "Sarah",
		    image: "https://i.pravatar.cc/48?u=933372",
		    balance: 20,
		  },
		  {
		    id: 499476,
		    name: "Anthony",
		    image: "https://i.pravatar.cc/48?u=499476",
		    balance: 0,
		  },
		];
		
		function Button({ children, onClick }) {
		  return (
		    <button className="button" onClick={onClick}>
		      {children}
		    </button>
		  );
		}
		
		export default function App() {
		  const [friends, setFriends] = useState(initialFriends);
		  const [showAddFriend, setShowAddFriend] = useState(false);
		  const [selectedFriend, setSelectedFriend] = useState(null);
		
		  function handleShowAddFriend() {
		    setShowAddFriend((show) => !show);
		  }
		
		  function handleAddFriend(friend) {
		    setFriends((friends) => [...friends, friend]);
		    setShowAddFriend(false);
		  }
		
		  function handleSelection(friend) {
		    // setSelectedFriend(friend);
		    setSelectedFriend((cur) => (cur?.id === friend.id ? null : friend));
		    setShowAddFriend(false);
		  }
		
		  function handleSplitBill(value) {
		    setFriends((friends) =>
		      friends.map((friend) =>
		        friend.id === selectedFriend.id
		          ? { ...friend, balance: friend.balance + value }
		          : friend
		      )
		    );
		
		    setSelectedFriend(null);
		  }
		
		  return (
		    <div className="app">
		      <div className="sidebar">
		        <FriendsList
		          friends={friends}
		          onSelection={handleSelection}
		          selectedFriend={selectedFriend}
		        />
		        {showAddFriend && <FormAddFriend onAddFriend={handleAddFriend} />}
		        <Button onClick={handleShowAddFriend}>
		          {showAddFriend ? "Close" : "Add Friend"}
		        </Button>
		      </div>
		
		      {selectedFriend && (
		        <FormSplitBill
		          selectedFriend={selectedFriend}
		          onSplitBill={handleSplitBill}
		        />
		      )}
		    </div>
		  );
		}
		
		function FriendsList({ friends, onSelection, selectedFriend }) {
		  return (
		    <ul>
		      {friends.map((friend) => (
		        <Friend
		          friend={friend}
		          key={friend.id}
		          onSelection={onSelection}
		          selectedFriend={selectedFriend}
		        />
		      ))}
		    </ul>
		  );
		}
		
		function Friend({ friend, onSelection, selectedFriend }) {
		  const isSelected = selectedFriend?.id === friend.id;
		
		  return (
		    <li key={friend.id} className={isSelected ? "selected" : ""}>
		      <img src={friend.image} alt={friend.name} />
		      <h3>{friend.name}</h3>
		      {friend.balance < 0 && (
		        <p className="red">
		          You owe {friend.name} {Math.abs(friend.balance)}💶
		        </p>
		      )}
		      {friend.balance > 0 && (
		        <p className="green">
		          {friend.name} owes you {Math.abs(friend.balance)}💶
		        </p>
		      )}
		      {friend.balance === 0 && <p>You and {friend.name} are even</p>}
		
		      <Button onClick={() => onSelection(friend)}>
		        {isSelected ? "Close" : "Select"}
		      </Button>
		    </li>
		  );
		}
		
		function FormAddFriend({ onAddFriend }) {
		  const [name, setName] = useState("");
		  const [image, setImage] = useState("https://i.pravatar.cc/48");
		
		  function handleSubmit(e) {
		    e.preventDefault();
		
		    if (!name || !image) return;
		
		    const id = crypto.randomUUID();
		    const newFriend = {
		      name,
		      image: `${image}?=${id}`,
		      balance: 0,
		      id,
		    };
		
		    onAddFriend(newFriend);
		
		    setName("");
		    setImage("https://i.pravatar.cc/48");
		  }
		
		  return (
		    <form className="form-add-friend" onSubmit={handleSubmit}>
		      <label>🎳 Friend name</label>
		      <input
		        type="text"
		        value={name}
		        onChange={(e) => setName(e.target.value)}
		      />
		
		      <label>🖼️ Image URL</label>
		      <input
		        type="text"
		        value={image}
		        onChange={(e) => setImage(e.target.value)}
		      />
		
		      <Button>Add</Button>
		    </form>
		  );
		}
		
		function FormSplitBill({ selectedFriend, onSplitBill }) {
		  const [bill, setBill] = useState(""); // input text elements have ""
		  const [paidByUser, setPaidByUser] = useState("");
		  const paidByFriend = bill ? bill - paidByUser : ""; // Reset each time state is changed and component is re-rendered and the function is executed
		  const [whoIsPaying, setWhoIsPaying] = useState("user");
		
		  function handleSubmit(e) {
		    e.preventDefault();
		
		    if (!bill || !paidByUser) return;
		
		    onSplitBill(whoIsPaying === "user" ? paidByFriend : -paidByUser);
		  }
		
		  return (
		    <form className="form-split-bill" onSubmit={handleSubmit}>
		      <h2>Split a bill with {selectedFriend.name}</h2>
		
		      <label>💶 Bill Value</label>
		      <input
		        type="text"
		        value={bill}
		        onChange={(e) => setBill(Number(e.target.value))}
		      />
		
		      <label>💰 Your expense</label>
		      <input
		        type="text"
		        value={paidByUser}
		        onChange={(e) =>
		          setPaidByUser(
		            Number(e.target.value) > bill ? paidByUser : Number(e.target.value)
		          )
		        }
		      />
		
		      <label>🏸 {selectedFriend.name}'s expense</label>
		      <input type="text" disabled value={paidByFriend} />
		
		      <label>🪙 Who is paying the bill</label>
		      <select
		        value={whoIsPaying}
		        onChange={(e) => setWhoIsPaying(e.target.value)}
		      >
		        <option value="user">You</option>
		        <option value="friend">{selectedFriend.name}</option>
		      </select>
		
		      <Button>Split Bill</Button>
		    </form>
		  );
		}

## Section 9: PART 2: INTERMEDIATE REACT [2 PROJECTS] ##
### Introduction to Part 2 ###
1. Build a few small projects
2. Topics:
	1. How react works behind the scenes
	2. Project
		1. UIs and layouts
		2. Setting up effects
		3. Fetching data
		4. custom hooks
		5. ...

### Useful Resources for Part 2 ###
1. Resources:
	1. [Writing Resilient Components](https://overreacted.io/writing-resilient-components/?ref=jonas.io) - Dan Abramov - React Team
	2. [Things I think about when I write React code](https://github.com/mithi/react-philosophies?ref=jonas.io) - GitHub repository
	3. [A (Mostly) Complete Guide to React Rendering Behavior](https://blog.isquaredsoftware.com/2020/05/blogged-answers-a-mostly-complete-guide-to-react-rendering-behavior/?ref=jonas.io) - Mark Erikson (Redux team)
	4. [A Visual Guide to React Rendering](https://alexsidorenko.com/blog/react-render-always-rerenders/?ref=jonas.io) - Multi-part series, check out the other ones
	5. [Inside Fiber: in-depth overview of the new reconcilliation algorithm in React](https://indepth.dev/posts/1008/inside-fiber-in-depth-overview-of-the-new-reconciliation-algorithm-in-react?ref=jonas.io)
	6. [A Cartoon Intro to Fiber](https://www.youtube.com/watch?v=ZCuYPiUIONs?ref=jonas.io) - YouTube video
	7. [What is React Fiber? React.js Deep Dive](https://www.youtube.com/watch?v=0ympFIwQFJw?ref=jonas.io) - YouTube video
	8. [The React and React Native Event System Explained](https://levelup.gitconnected.com/how-exactly-does-react-handles-events-71e8b5e359f2?ref=jonas.io)
	9. [Under the hood of event listeners in React](https://gist.github.com/romain-trotard/76313af8170809970daa7ff9d87b0dd5?ref=jonas.io)
	10. [A DIY guide to build your own React](https://github.com/pomber/didact?ref=jonas.io)
	11. [useSynExternalStore First Look](https://julesblom.com/writing/usesyncexternalstore?ref=jonas.io)
	12. [Under the hood of React's hooks system](https://the-guild.dev/blog/react-hooks-system?ref=jonas.io)
	13. [Why Do React Hooks Rely on Call Order?](https://overreacted.io/why-do-hooks-rely-on-call-order/?ref=jonas.io) - By Dan Abramov
	14. [So you think you know everything about React refs](https://blog.thoughtspile.tech/2021/05/17/everything-about-react-refs/?ref=jonas.io)
	15. [react-use: Reusable React Hook Library](https://github.com/streamich/react-use?ref=jonas.io) - Github repository
	16. [react-hookz: React hooks done right](https://github.com/react-hookz/web?ref=jonas.io) - GitHub repository

## Section 10: Thinking in React: Components, Composition, and Reusability ##
### Section Overview ###
1. Topics:
	1. How to **think** about components
	2. Composition
	3. Reusability
	4. How to **split** a component
	5. Building **layouts**
2. What are we going to study:
	1. How to split a UI into components
	2. What type of components we can use
	3. How to implement in React
	4. Simple app layout using composition

### Setting Up the "usePopcorn" Project ###
1. `npx create-react-app@5 usepopcorn`
	1. [usepopcorn.netlify.app](usepopcorn.netlify.app)
		1. It is all about hooks
2. Topics:
	1. Component reusability

### How to Split a UI into Components ###
1. Important questions:
	1. How do we split UI into components?
	2. When should be build new components?

#### Component Size Matters ####
1. Component size axis
	1. Small to huge (none of them are ideal)
		1. Huge: 
			1. Too many **responsibilities**
				1. If it does too many multiple things, we must break it up into multiple components
			2. Might need too many **props**
				1. 10-15 props
			3. Hard to **reuse**
			4. **Complex** code, hard to understand (and use)
		2. Small:
			1. We end up with 100s of mini-components
			2. Confusing codebase
			3. Too **abstracted**
				1. To define something new to hide the implementation details of the thing
					1. Since, each component is an abstraction
		3. Right balance: Generally, we need to find the right balance between too specific and too broad

#### How to Split a UI into Components ####
1. How?
	1. Logical separation
		1. Each component has a well-defined responsibility
			1. Display price
			2. Display rating
	2. Some are reusable
		1. Heart button
		2. Superhost label
	3. Low complexity
		1. Not overly complex
2. The 4 Criteria for splitting a UI into components:
	1. Logical separation of content/layout
		1. Components define a logical separation
	2. Reusability
		1. We need to make some of the components re-usable
	3. Responsibilities/ Complexity
		1. Each component should have a single, well-defined responsibility
	4. Personal coding style
		1. Some people like smaller components while other prefer larger components
			1. Choose a component size that works best for me (to be as productive as possible)

#### Framework: When to Construct a New Component? ####
1. Criterion 1:
	1. **Suggestion:** When in doubt, start with a relatively big component, then split it into smaller components as it becomes necessary
		1. When does it become necessary?
			1. Use 4 criteria:
				1. Logical separation of content/layout
				2. Reusability
				3. Responsibilities/complexity
				4. Personal coding style
	2. Skip the above step if you're sure you need to reuse.
		1. Otherwise, you don't need to focus on reusability and complexity early on
2. Criterion 2:
	1. Does the component contain pieces of content or layout that **don't belong together**?
		1. You might need a new component
	2. Is it possible to reuse part of the component?
		1. Do you **want** or **need** to reuse it?
			1. You might need a new component
4. Criterion 3:
	1. Is the component doing too **many different things**?
	2. Does the component rely on too **many props**
	3. Does the component have too **many pieces of state** and/or effects?
	4. Is the code, including JSX, too **complex/confusing**?
5. Criterion 4:
	1. Do you prefer **smaller** functions/components?
6. The above are all **guidelines**... it will become intuitive over time!

#### Some More General Guidelines ####
1. Be aware that contructing a new component **defines a new abstraction**. Abstractions have a **cost**, because **more abstractions require more mental energy** to switch back and forth between components. So try not to construct new components too early.
2. Name a component according to **what it does** or **what it displays**. Don't be afraid to using long component names
3. Never declare a new component **inside another component**
	1. Co-locate related components inside the same file. Don't seperate components into different files too early
4. It's completely normal that an app has components of **many different sizes**, including very small and huge ones (See next slide...)

#### Any App Has Components of Different Sizes and Reusability ####
1. Some very small components are necessary
	1. Examples:
		1. Heart button
		2. Superhost
		3. Rarefind
		4. ...
	2. Reasons:
		1. Highly reusable
		2. Very low complexity
2. **Most apps will have a few huge components**
	1. Not meant to be reused (**not a problem!**)
	2. Examples:
		1. Page component
			1. Contains the entire layout of the page
				1. It is not meant to be re-used
					1. Don't worry about reusability or needing to split the component up (?)
3. Reusability range is similar to the size range:
	1. Small - most reusable
	2. Huge - non-reusable
		1. Not all components are meant to be re-usable
	3. Components with all different sizes
		1. Different degrees of:
			1. Size
			2. Reusability
			3. Responsibility
			4. Complexity

### Splitting Components in Practice ###
1. 07-usepopcorn
	1. Mixing JSX and native HTML elements might be ugly
2. Code:

		import { useState } from "react";

		const tempMovieData = [
		  {
		    imdbID: "tt1375666",
		    Title: "Inception",
		    Year: "2010",
		    Poster:
		      "https://m.media-amazon.com/images/M/MV5BMjAxMzY3NjcxNF5BMl5BanBnXkFtZTcwNTI5OTM0Mw@@._V1_SX300.jpg",
		  },
		  {
		    imdbID: "tt0133093",
		    Title: "The Matrix",
		    Year: "1999",
		    Poster:
		      "https://m.media-amazon.com/images/M/MV5BNzQzOTk3OTAtNDQ0Zi00ZTVkLWI0MTEtMDllZjNkYzNjNTc4L2ltYWdlXkEyXkFqcGdeQXVyNjU0OTQ0OTY@._V1_SX300.jpg",
		  },
		  {
		    imdbID: "tt6751668",
		    Title: "Parasite",
		    Year: "2019",
		    Poster:
		      "https://m.media-amazon.com/images/M/MV5BYWZjMjk3ZTItODQ2ZC00NTY5LWE0ZDYtZTI3MjcwN2Q5NTVkXkEyXkFqcGdeQXVyODk4OTc3MTY@._V1_SX300.jpg",
		  },
		];
		
		const tempWatchedData = [
		  {
		    imdbID: "tt1375666",
		    Title: "Inception",
		    Year: "2010",
		    Poster:
		      "https://m.media-amazon.com/images/M/MV5BMjAxMzY3NjcxNF5BMl5BanBnXkFtZTcwNTI5OTM0Mw@@._V1_SX300.jpg",
		    runtime: 148,
		    imdbRating: 8.8,
		    userRating: 10,
		  },
		  {
		    imdbID: "tt0088763",
		    Title: "Back to the Future",
		    Year: "1985",
		    Poster:
		      "https://m.media-amazon.com/images/M/MV5BZmU0M2Y1OGUtZjIxNi00ZjBkLTg1MjgtOWIyNThiZWIwYjRiXkEyXkFqcGdeQXVyMTQxNzMzNDI@._V1_SX300.jpg",
		    runtime: 116,
		    imdbRating: 8.5,
		    userRating: 9,
		  },
		];
		
		function Navbar() {
		  return (
		    <nav className="nav-bar">
		      <Logo />
		      <Search />
		      <NumResults />
		    </nav>
		  );
		}
		
		function Logo() {
		  return (
		    <div className="logo">
		      <span role="img">🍿</span> {/* No need to break */}
		      <h1>usePopcorn</h1>
		    </div>
		  );
		}
		
		function Search() {
		  const [query, setQuery] = useState("");
		  return (
		    <input
		      className="search"
		      type="text"
		      placeholder="Search movies..."
		      value={query}
		      onChange={(e) => setQuery(e.target.value)}
		    />
		  );
		}
		
		function NumResults() {
		  return (
		    <p className="num-results">
		      Found <strong>X</strong> results
		    </p>
		  );
		}
		
		function Main() {
		  return (
		    <main className="main">
		      <ListBox />
		      <WatchedBox />
		    </main>
		  );
		}
		
		function ListBox() {
		  const [isOpen1, setIsOpen1] = useState(true);
		
		  return (
		    <div className="box">
		      <button
		        className="btn-toggle"
		        onClick={() => setIsOpen1((open) => !open)}
		      >
		        {isOpen1 ? "–" : "+"}
		      </button>
		      {isOpen1 && <MovieList />}
		    </div>
		  );
		}
		
		function MovieList() {
		  const [movies, setMovies] = useState(tempMovieData);
		
		  return (
		    <ul className="list">
		      {movies?.map((movie) => (
		        <Movie movie={movie} />
		      ))}
		    </ul>
		  );
		}
		
		function Movie({ movie }) {
		  return (
		    <li key={movie.imdbID}>
		      <img src={movie.Poster} alt={`${movie.Title} poster`} />
		      <h3>{movie.Title}</h3>
		      <div>
		        <p>
		          <span>🗓</span>
		          <span>{movie.Year}</span>
		        </p>
		      </div>
		    </li>
		  );
		}
		
		function WatchedBox() {
		  const [watched, setWatched] = useState(tempWatchedData);
		  const [isOpen2, setIsOpen2] = useState(true);
		
		  return (
		    <div className="box">
		      <button
		        className="btn-toggle"
		        onClick={() => setIsOpen2((open) => !open)}
		      >
		        {isOpen2 ? "–" : "+"}
		      </button>
		      {isOpen2 && (
		        <>
		          <WatchedSummary watched={watched} />
		
		          <WatchedMovieList watched={watched} />
		        </>
		      )}
		    </div>
		  );
		}
		
		function WatchedSummary({ watched }) {
		  const avgImdbRating = average(watched.map((movie) => movie.imdbRating));
		  const avgUserRating = average(watched.map((movie) => movie.userRating));
		  const avgRuntime = average(watched.map((movie) => movie.runtime));
		
		  return (
		    <div className="summary">
		      <h2>Movies you watched</h2>
		      <div>
		        <p>
		          <span>#️⃣</span>
		          <span>{watched.length} movies</span>
		        </p>
		        <p>
		          <span>⭐️</span>
		          <span>{avgImdbRating}</span>
		        </p>
		        <p>
		          <span>🌟</span>
		          <span>{avgUserRating}</span>
		        </p>
		        <p>
		          <span>⏳</span>
		          <span>{avgRuntime} min</span>
		        </p>
		      </div>
		    </div>
		  );
		}
		
		function WatchedMovieList({ watched }) {
		  return (
		    <ul className="list">
		      {watched.map((movie) => (
		        <WatchedMovie movie={movie} key={movie.imdbID} />
		      ))}
		    </ul>
		  );
		}
		
		function WatchedMovie({ movie }) {
		  return (
		    <li key={movie.imdbID}>
		      <img src={movie.Poster} alt={`${movie.Title} poster`} />
		      <h3>{movie.Title}</h3>
		      <div>
		        <p>
		          <span>⭐️</span>
		          <span>{movie.imdbRating}</span>
		        </p>
		        <p>
		          <span>🌟</span>
		          <span>{movie.userRating}</span>
		        </p>
		        <p>
		          <span>⏳</span>
		          <span>{movie.runtime} min</span>
		        </p>
		      </div>
		    </li>
		  );
		}
		
		const average = (arr) =>
		  arr.reduce((acc, cur, i, arr) => acc + cur / arr.length, 0);
		
		export default function App() {
		  return (
		    <>
		      <Navbar />
		      <Main />
		    </>
		  );
		}

### Component Categories ###
1. Most of your components will **naturally** (we shouldn't force our components into one of the categories) all into **one of three categories**:
	1. Stateless/presentational components
		1. **No state**
		2. Can receive props and simply present received data or other content
		3. Usually **small and reusable**
			1. Example:
				1. Logo
				2. NumResults
				3. Movie
	2. Stateful components
		1. **Have state**
		2. Can still be **reusable**
			1. Example: Search
	3. Structural components
		1. **Pages**, **Layouts**, or **Screens** of the app
		2. Result of **composition** (many smaller components together)
		3. Can be **huge and non-reusable** (but don't have to)
		4. **They are responsible for providing some sort of structure to the application**
			1. Pages
			2. Layouts
			3. Screens
			4. ...
		5. Might not be present in small apps
			1. Can be found in bigger apps

### Prop Drilling ###
1. Classification of components:
	1. Structural:
		1. `App`
		2. `NavBar`
		3. `Main`
	2. Presentational:
		1. `Logo` - Stateless
		2. `NumResults`
		3. `Movie`
		4. `WatchedMoviesList`
		5. `WatcheMovie`
	3. Stateful:
		1. `Search`
		2. `ListBox`
		3. `MovieList`
		4. `WatchedBox`
2. Prop drilling:
	1. We need to pass a prop into several nested child components in order to get the data into a deeply nested component
		1. The intermediate nested components do not need the prop
	2. Not good if we need to pass it very deep

### Component Composition ###
1. Principle: Component composition

#### What is Component Composition? ####
1. "Using" A component
	1. Modal component using Success component (using nesting)

			// It can be called a `SuccessModal` because we cannot use it for anything else
			function Modal() {
				return (
					<div>
						<Success />
					</div>
				);
			}

			function Success() {
				return <p>Well done!</p>;
			}

		1. Problem:
			1. `Success` is inside `Modal`: We can NOT reuse Modal (deeply linked together in the JSX)
				1. `Modal` cannot be used to display any other message (`Error` message say)
		2. Solution: Component Composition
			1. Using `children` prop

					function Modal({ children }) {
						return (
							<div className="modal">
								{children}
							</div>
						);
					}

				1. We can pass `Success` or `Error` between opening and closing tags when we use `Modal`

						<Modal>
							<Success />
						</Modal>

					1. We can REUSE `Modal`
				2. **We leave an empty slot ready to be filled by any other component**
				3. `Error` message:

						<Modal>
							<Error />
						</Modal>

2. **Component Composition:** Combining different components using the `children` prop (or explicitly defined props)
3. We use component composition, we can:
	1. Construct highly reusable and flexible components
	2. Fix prop dilling (great for layouts)
		1. Good for layouts
4. It is possible because components don't need to know their children in advance

### Fixing Prop Drilling With Composition (And Building a Layout) ###
1. The entire layout is seen in one place (in the `App` component)

### Using Composition to Make a Reusable Box ###
1. Code:

		import { useState } from "react";

		const tempMovieData = [
		  {
		    imdbID: "tt1375666",
		    Title: "Inception",
		    Year: "2010",
		    Poster:
		      "https://m.media-amazon.com/images/M/MV5BMjAxMzY3NjcxNF5BMl5BanBnXkFtZTcwNTI5OTM0Mw@@._V1_SX300.jpg",
		  },
		  {
		    imdbID: "tt0133093",
		    Title: "The Matrix",
		    Year: "1999",
		    Poster:
		      "https://m.media-amazon.com/images/M/MV5BNzQzOTk3OTAtNDQ0Zi00ZTVkLWI0MTEtMDllZjNkYzNjNTc4L2ltYWdlXkEyXkFqcGdeQXVyNjU0OTQ0OTY@._V1_SX300.jpg",
		  },
		  {
		    imdbID: "tt6751668",
		    Title: "Parasite",
		    Year: "2019",
		    Poster:
		      "https://m.media-amazon.com/images/M/MV5BYWZjMjk3ZTItODQ2ZC00NTY5LWE0ZDYtZTI3MjcwN2Q5NTVkXkEyXkFqcGdeQXVyODk4OTc3MTY@._V1_SX300.jpg",
		  },
		];
		
		const tempWatchedData = [
		  {
		    imdbID: "tt1375666",
		    Title: "Inception",
		    Year: "2010",
		    Poster:
		      "https://m.media-amazon.com/images/M/MV5BMjAxMzY3NjcxNF5BMl5BanBnXkFtZTcwNTI5OTM0Mw@@._V1_SX300.jpg",
		    runtime: 148,
		    imdbRating: 8.8,
		    userRating: 10,
		  },
		  {
		    imdbID: "tt0088763",
		    Title: "Back to the Future",
		    Year: "1985",
		    Poster:
		      "https://m.media-amazon.com/images/M/MV5BZmU0M2Y1OGUtZjIxNi00ZjBkLTg1MjgtOWIyNThiZWIwYjRiXkEyXkFqcGdeQXVyMTQxNzMzNDI@._V1_SX300.jpg",
		    runtime: 116,
		    imdbRating: 8.5,
		    userRating: 9,
		  },
		];
		
		function Navbar({ children }) {
		  return (
		    <nav className="nav-bar">
		      <Logo />
		      {children}
		    </nav>
		  );
		}
		
		function Logo() {
		  return (
		    <div className="logo">
		      <span role="img">🍿</span> {/* No need to break */}
		      <h1>usePopcorn</h1>
		    </div>
		  );
		}
		
		function Search() {
		  const [query, setQuery] = useState("");
		  return (
		    <input
		      className="search"
		      type="text"
		      placeholder="Search movies..."
		      value={query}
		      onChange={(e) => setQuery(e.target.value)}
		    />
		  );
		}
		
		function NumResults({ movies }) {
		  return (
		    <p className="num-results">
		      Found <strong>{movies.length}</strong> results
		    </p>
		  );
		}
		
		function Main({ children }) {
		  return <main className="main">{children}</main>;
		}
		
		function Box({ children }) {
		  const [isOpen, setIsOpen] = useState(true);
		
		  return (
		    <div className="box">
		      <button className="btn-toggle" onClick={() => setIsOpen((open) => !open)}>
		        {isOpen ? "–" : "+"}
		      </button>
		      {isOpen && children}
		    </div>
		  );
		}
		
		function MovieList({ movies }) {
		  return (
		    <ul className="list">
		      {movies?.map((movie) => (
		        <Movie movie={movie} />
		      ))}
		    </ul>
		  );
		}
		
		function Movie({ movie }) {
		  return (
		    <li key={movie.imdbID}>
		      <img src={movie.Poster} alt={`${movie.Title} poster`} />
		      <h3>{movie.Title}</h3>
		      <div>
		        <p>
		          <span>🗓</span>
		          <span>{movie.Year}</span>
		        </p>
		      </div>
		    </li>
		  );
		}
		
		// function WatchedBox() {
		//   const [watched, setWatched] = useState(tempWatchedData);
		//   const [isOpen2, setIsOpen2] = useState(true);
		
		//   return (
		//     <div className="box">
		//       <button
		//         className="btn-toggle"
		//         onClick={() => setIsOpen2((open) => !open)}
		//       >
		//         {isOpen2 ? "–" : "+"}
		//       </button>
		//       {isOpen2 && (
		//         <>
		//           <WatchedSummary watched={watched} />
		
		//           <WatchedMovieList watched={watched} />
		//         </>
		//       )}
		//     </div>
		//   );
		// }
		
		function WatchedSummary({ watched }) {
		  const avgImdbRating = average(watched.map((movie) => movie.imdbRating));
		  const avgUserRating = average(watched.map((movie) => movie.userRating));
		  const avgRuntime = average(watched.map((movie) => movie.runtime));
		
		  return (
		    <div className="summary">
		      <h2>Movies you watched</h2>
		      <div>
		        <p>
		          <span>#️⃣</span>
		          <span>{watched.length} movies</span>
		        </p>
		        <p>
		          <span>⭐️</span>
		          <span>{avgImdbRating}</span>
		        </p>
		        <p>
		          <span>🌟</span>
		          <span>{avgUserRating}</span>
		        </p>
		        <p>
		          <span>⏳</span>
		          <span>{avgRuntime} min</span>
		        </p>
		      </div>
		    </div>
		  );
		}
		
		function WatchedMovieList({ watched }) {
		  return (
		    <ul className="list">
		      {watched.map((movie) => (
		        <WatchedMovie movie={movie} key={movie.imdbID} />
		      ))}
		    </ul>
		  );
		}
		
		function WatchedMovie({ movie }) {
		  return (
		    <li key={movie.imdbID}>
		      <img src={movie.Poster} alt={`${movie.Title} poster`} />
		      <h3>{movie.Title}</h3>
		      <div>
		        <p>
		          <span>⭐️</span>
		          <span>{movie.imdbRating}</span>
		        </p>
		        <p>
		          <span>🌟</span>
		          <span>{movie.userRating}</span>
		        </p>
		        <p>
		          <span>⏳</span>
		          <span>{movie.runtime} min</span>
		        </p>
		      </div>
		    </li>
		  );
		}
		
		const average = (arr) =>
		  arr.reduce((acc, cur, i, arr) => acc + cur / arr.length, 0);
		
		export default function App() {
		  const [movies, setMovies] = useState(tempMovieData);
		  const [watched, setWatched] = useState(tempWatchedData);
		
		  return (
		    <>
		      <Navbar>
		        <Search />
		        <NumResults movies={movies} />
		      </Navbar>
		      <Main>
		        <Box>
		          <MovieList movies={movies} />
		        </Box>
		        <Box>
		          <WatchedSummary watched={watched} />
		          <WatchedMovieList watched={watched} />
		        </Box>
		      </Main>
		    </>
		  );
		}

### Passing Elements as Props (Alternative to children) ###
1. Passed as an element prop:

		<Main>
          <Box element={<MovieList movies={movies} />} />
          <Box
            element={
              <>
                <WatchedSummary watched={watched} />
                <WatchedMovieList watched={watched} />
              </>
            }
          />
	    </Main>

		...

		function Box({ element }) {
		  const [isOpen, setIsOpen] = useState(true);
		
		  return (
		    <div className="box">
		      <button className="btn-toggle" onClick={() => setIsOpen((open) => !open)}>
		        {isOpen ? "–" : "+"}
		      </button>
		      {isOpen && element}
		    </div>
		  );
		}

	1. Similar to passing `children` prop (inside React both must be the same)
	2. Using `children` is the preferred way

### Building a Reusable Star Rating Component ###
1. Isolated component - to be used anywhere
	1. Users can decide the number of stars

### Constructing the Stars ###
### Handling Hover Events ###
1. Code:

		import { useState } from "react";

		const containerStyle = {
		  display: "flex",
		  alignItems: "center",
		  gap: "16px",
		};
		// This doesn't change
		// This object doesn't have to be re-generated by JS each time the component re-rendered (because the function is called again)
		
		const starContainerStyle = {
		  display: "flex",
		};
		
		const textStyle = {
		  lineHeight: "1",
		  margin: "0",
		};
		
		export default function StarRating({ maxRating = 5 }) {
		  const [rating, setRating] = useState(0);
		  const [tempRating, setTempRating] = useState(0);
		
		  function handleRating(rating) {
		    setRating(rating);
		  }
		
		  return (
		    <div style={containerStyle}>
		      <div style={starContainerStyle}>
		        {Array.from({ length: maxRating }, (_, i) => (
		          <Star
		            key={i}
		            onRate={() => handleRating(i + 1)}
		            full={tempRating ? tempRating >= i + 1 : rating >= i + 1}
		            onHoverIn={() => setTempRating(i + 1)}
		            onHoverOut={() => setTempRating(0)}
		          />
		        ))}
		      </div>
		      <p style={textStyle}>{tempRating || rating || ""}</p>
		    </div>
		  );
		}
		
		const starStyle = {
		  width: "48px",
		  height: "48px",
		  display: "block",
		  cursor: "pointer",
		};
		
		function Star({ onRate, full, onHoverIn, onHoverOut }) {
		  return (
		    <span
		      role="button"
		      style={starStyle}
		      onClick={onRate}
		      onMouseEnter={onHoverIn}
		      onMouseLeave={onHoverOut}
		    >
		      {full ? (
		        <svg
		          xmlns="http://www.w3.org/2000/svg"
		          viewBox="0 0 20 20"
		          fill="#000"
		          stroke="#000"
		        >
		          <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
		        </svg>
		      ) : (
		        <svg
		          xmlns="http://www.w3.org/2000/svg"
		          fill="none"
		          viewBox="0 0 24 24"
		          stroke="#000"
		        >
		          <path
		            strokeLinecap="round"
		            strokeLinejoin="round"
		            strokeWidth="{2}"
		            d="M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1 0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1 0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538 1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976 2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0 00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1 1 0 00.951-.69l1.519-4.674z"
		          />
		        </svg>
		      )}
		    </span>
		  );
		}

### Props as a Component API ###
#### Props as an API ####
1. Any component is created by someone and consumed by someone
	1. They might be different developers
	2. We must think about two different entities
		1. Author decides what props the component can accept
		2. Consumer uses the component in an application by specifying values for the props
	3. Why?
		1. Component props = Public API (of the component)
			1. When an author chooses what props to pass to the component, we are choosing the public interface of the component
			2. We are also choosing, how much complexity of the component we want to expose to the consumer of the API
				1. We need to find a good balance on how strict we want to be
					1. How many props we want to enable for configuration
						1. Example: Weather component
							1. Too few props: Extremely simple: Only allowing one prop (location for which consumer wants a weather)
								1. Not **flexible** enough
								2. Might not be **useful**
							2. Too many props: URL, number of days, daily/hourly, how many days, which temperature unit, what data to be displayed, etc...
								1. Too **hard** to use
									1. Exposing too much **complexity**
									2. **Hard-to-write** code
				2. We need to find the right balance between too little and too many props, that works for both the consumer and the author (based on project needs)
					1. We can provide default values for many of them.
	4. A component is just an abstraction that encapsulates UI and logic

### Improving Reusability With Props ###
1. If we want to re-use in many applications (or share it with npm)
2. Consumers want to define:
	1. Colors of the stars
	2. Sizes of the stars
	3. Text
3. Note: Never initialize a state from prop is true if we want state variable to stay in sync with passed in prop
	1. If prop value is updated, state value also gets updated
		1. However, we are using prop as seed data (just as an initial value)
4. Other props that we can allow:
	1. Color to change based on ratings
	2. Different spacing between stars
	3. Which side the text label appears
5. Another most important point:
	1. The consumer might need the `rating` state outside the component

### PropTypes ###
1. Adding type-checking
	1. It is better to use TypeScript, instead of JS
	2. If we don't want to switch to TypeScript, we can use this approach:

#### Code ####
1. Index.js

		import React, { useState } from "react";
		import ReactDOM from "react-dom/client";
		// import "./index.css";
		// import App from "./App";
		
		import StarRating from "./StarRating";
		
		function Test() {
		  const [movieRating, setMovieRating] = useState(0);
		
		  return (
		    <div>
		      <StarRating color="blue" maxRating={10} onSetRating={setMovieRating} />
		      <p>This movie was rated {movieRating} stars</p>
		    </div>
		  );
		}
		
		const root = ReactDOM.createRoot(document.getElementById("root"));
		root.render(
		  <React.StrictMode>
		    {/* <App /> */}
		    <StarRating
		      maxRating={5}
		      messages={["Terrible", "Bad", "Okay", "Good", "Amazing"]}
		    />
		    <StarRating
		      maxRating={10}
		      size={24}
		      color="red"
		      className="text"
		      defaultRating={3}
		    />
		    {/* <StarRating maxRating={10} />
		    <StarRating /> */}
		    <Test />
		  </React.StrictMode>
		);

2. StarRating.js

		import { useState } from "react";
		import PropTypes from "prop-types"; // create-react-app comes with this pre-installed
		
		const containerStyle = {
		  display: "flex",
		  alignItems: "center",
		  gap: "16px",
		};
		// This doesn't change
		// This object doesn't have to be re-generated by JS each time the component re-rendered (because the function is called again)
		
		const starContainerStyle = {
		  display: "flex",
		};
		
		// JS throws warning
		StarRating.propTypes = {
		  maxRating: PropTypes.number,
		  defaultRating: PropTypes.number,
		  color: PropTypes.string,
		  size: PropTypes.number,
		  messages: PropTypes.array,
		  className: PropTypes.string,
		  onSetRating: PropTypes.func,
		};
		
		export default function StarRating({
		  maxRating = 5,
		  color = "#fcc419",
		  size = 48,
		  className = "",
		  messages = [],
		  defaultRating = 0,
		  onSetRating,
		}) {
		  const textStyle = {
		    lineHeight: "1",
		    margin: "0",
		    color,
		    fontSize: `${size / 1.5}px`,
		  };
		
		  const [rating, setRating] = useState(defaultRating);
		  const [tempRating, setTempRating] = useState(0);
		
		  function handleRating(rating) {
		    setRating(rating);
		    onSetRating && onSetRating(rating);
		  }
		
		  return (
		    <div style={containerStyle}>
		      <div style={starContainerStyle} className={className}>
		        {Array.from({ length: maxRating }, (_, i) => (
		          <Star
		            key={i}
		            onRate={() => handleRating(i + 1)}
		            full={tempRating ? tempRating >= i + 1 : rating >= i + 1}
		            onHoverIn={() => setTempRating(i + 1)}
		            onHoverOut={() => setTempRating(0)}
		            color={color}
		            size={size}
		          />
		        ))}
		      </div>
		      <p style={textStyle}>
		        {messages.length === maxRating
		          ? messages[tempRating ? tempRating - 1 : rating - 1]
		          : tempRating || rating || ""}
		      </p>
		    </div>
		  );
		}
		
		function Star({ onRate, full, onHoverIn, onHoverOut, color, size }) {
		  const starStyle = {
		    width: `${size}px`,
		    height: `${size}px`,
		    display: "block",
		    cursor: "pointer",
		  };
		
		  return (
		    <span
		      role="button"
		      style={starStyle}
		      onClick={onRate}
		      onMouseEnter={onHoverIn}
		      onMouseLeave={onHoverOut}
		    >
		      {full ? (
		        <svg
		          xmlns="http://www.w3.org/2000/svg"
		          viewBox="0 0 20 20"
		          fill={color}
		          stroke={color}
		        >
		          <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
		        </svg>
		      ) : (
		        <svg
		          xmlns="http://www.w3.org/2000/svg"
		          fill="none"
		          viewBox="0 0 24 24"
		          stroke={color}
		        >
		          <path
		            strokeLinecap="round"
		            strokeLinejoin="round"
		            strokeWidth="{2}"
		            d="M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1 0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1 0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538 1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976 2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0 00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1 1 0 00.951-.69l1.519-4.674z"
		          />
		        </svg>
		      )}
		    </span>
		  );
		}

### CHALLENGE #1: Text Expander Component ###
1. MUST DO

## How React Works Behind the Scenes ##
### Section Overview ###
1. Topics:
	1. How things work **inside** React
	2. You'll become a **better** and more **confident** React developer
	3. Will be a bit intense...
	4. Watch at least the **final lecture**!
2. Benefit of learning it:
	1. We can become a better and confident React developer
	2. We can ace common React questions
	3. This puts in top 5% of all React developers 

### Project Setup and Walkthrough ###
1. Copy `08-how-react-works/starter` and rename it to `how-react-works`
	1. `npm i`
	2. `npm start`

### Components, Instances, and Elements ###
1. Conceptual differences between React components, component instances, and React elements

#### Component vs. Instance vs. Element ####
1. Component:
	1. **Description** of a piece of UI
	2. A component is a JS function that **returns React elements** (element tree), usually written as JSX (the elements)
	3. It is a "Blueprint" or "Template"
		1. Using the blueprint/template, React instantiates one or more Component Instances
2. Component Instance
	1. Component instances are created when we "use" components
		1. Example:

				function App() {
					return (
						<div className='tabs'>
							<Tab item={content[0]} />
							<Tab item={content[1]} />
							<Tab item={content[2]} />
						</div>
					);
				}

			1. 3 instances of `Tab` components are placed in the component tree (in the actual application)
				1. Since React calls `Tab()` function 3 times
					1. One time for each instance
			2. An instance is the actual "pysical manifestation" of a component living in a component tree
				1. Component is just a function we wrote before it is called
			3. Each instance has its own state and props
			4. **Each instance has a lifecycle** (can "be born", "live", and "die")
				1. We usually use component and component-instance interchangeably
	2. As React executes the code in each of the instances, each of them will return one or more React elements
3. React Element
	1. Behind the scenes, JSX gets converted to multiple `React.createElement` function calls
	2. As React calls `React.createElement` functions, the result will be a React element 
	3. A React element is the **result of the function calls (using components in React code)**
		1. **It is a big, immutable JS object that React keeps in memory**
	4. What is it?
		1. It contains all the information that is necessary to construct DOM elements for the current component instance
	5. The **React Element** is ultimately converted into **DOM Element (HTML)**
		1. Painted onto the screen by the Browser
	6. DOM Element is the actual **visual representation** of the component instance in the browser
		1. It is not React Element that is rendered to the DOM
		2. **React elements just live inside React app** (they have nothing to do the DOM)
			1. React elements are converted into DOM when they are painted onto the screen in the final step

### Instances and Elements in Practice ###
1. Code:

		console.log(<DifferentContent test={23} />); // React uses the object created to convert it into DOM elements
		// Has `Symbol`s: Primitives that cannot be transmitted via JSON. It cannot come from an API call. If a hacker tries to send a fake React element from the API, then React will not see this type as symbol (because symbols cannot be transmitted via JSON). React will not include the fake element into the DOM (protecting us from an attack)
		
		console.log(DifferentContent()); // `type`: `div` instead of `DifferentComponent`. React doesn't see it as a component. It sees raw React element
		// We want React to see the component instance
		
		function Tabbed({ content }) {
		  const [activeTab, setActiveTab] = useState(0);
		
		  return (
		    <div>
		      <div className="tabs">
		        <Tab num={0} activeTab={activeTab} onClick={setActiveTab} />
		        <Tab num={1} activeTab={activeTab} onClick={setActiveTab} />
		        <Tab num={2} activeTab={activeTab} onClick={setActiveTab} />
		        <Tab num={3} activeTab={activeTab} onClick={setActiveTab} />
		      </div>
		
		      {activeTab <= 2 ? (
		        <TabContent item={content.at(activeTab)} />
		      ) : (
		        <DifferentContent />
		      )}
		
		      {TabContent({ item: content.at(0) })}
		      {/* It works. Component tree doesn't show it
		      The state of the component is managed inside the parent component
		      */}
		    </div>
		  );
		}

### How Rendering Works: Overview ###
#### Quick Recap Before We Get Started ####
1. We build components
2. We use the components as many times as we want to construct one or more instances of the components
	1. The component instances are actual physical components which live in our application and hold state and props
3. Each JSX will produce a bunch of `React.createElement` function calls which will produce a React element for each component instance
4. The React elements will be transformed to DOM elements and displayed as UI on the screen
5. **How do the React elements get transformed into DOM elements and displayed on the screen?**

#### Overview: How Components are Displayed on the Screen ####
1. Phases involved in displaying components to the screen
	1. We zoom into each of the phases to learn how the entire process works internally behind the scenes
2. Process:

			Render is Triggered
			The process is started by React each time a new render is triggered (By updating state somewhere)
				|
				v
			Render Phase
			React calls component functions and figures out how DOM should be updated (to reflect the latest state changes)
				DOM is not updated in this phase:
					In React, rendering is NOT updating the DOM or displaying elements on the screen. Rendering only happens internally inside React, it does not produce visual changes
				|
				v
			Commit Phase
				React actually writes to the DOM, updating, inserting, and deleting elements (to reflect the correct state of the application)
					This phase is responsible for actual rendering (traditional definition)
				|
				v
			Browser Paint
				Browser identifies that the DOM is updated, and it repaints the screen (not part of React)

#### How Renders are Triggered ####
1. The two situations that trigger renders:
	1. **Initial render** of the application (first time the application renders)
	2. **State is updated** in one or more component instances (**re-render**) (somewhere in the application)
2. The render process is triggered for the entire application (not for just a single component)
	1. The entire DOM is not updated
		1. Rendering is only calling out component functions and figuring out what needs to change in the DOM
	2. **In practice**, it looks like React only re-renders the component where the state update happens, but that's not how it **works behind the scenes**
		1. **React looks at the entire tree whenever a render happens**
	3. Renders are **not** triggered immediately, but **scheduled** for when the JS engine has some "free time" (the difference is usually a few milliseconds that we won't notice). There is also batching of multiple `setState` calls (in the same function) in event handlers (later)

### How Rendering Works: The Render Phase ###
#### Review: The Mechanics of State in React ####

		Updated State    <--+
			|               |
			v               |
		Render/Re-Render (3)|Update State (2)
			|               |
			v               |
		View                |
			Event handler --+
		      (1)

	1. Not True #1: Rendering is updating the screen/DOM
		1. Rendering in React is just about calling the component functions and figuring out what needs to change in the DOM tree.
	2. Not True #2: React completely discards old view (DOM) on re-render (technically)
		1. DOM will not be updated for the entire component instance

#### The Render Phase ####
1. When render phase begins,
	
		Component instances that triggered re-render
			React will go through the entire component tree and takes all components instances that triggered re-render and renders them (calls corresponding component functions we have written in our code)
			|
			v
		React Elements
			Result of re-render
			|
			v
		New Virtual DOM 
			All React elements together is called a Virtual DOM
			|
			v
		Reconciliation + Diffing <- Current Fiber Tree (before state update)
			The New Virtual DOM gets reconciled with the current Fiber tree (as it exists before the state update)
			The reconciliation is done by the Reconsiler called "Fiber"
			|
			v
		Updated Fiber Tree
			The result of the reconciliation process is an updated Fiber tree
				It is the tree that will eventually be used to write to the DOM
			|
			v
		List of DOM updates
			Result of the render phase ("list of effects")

#### The Virtual DOM (React Element Tree) ####
1. On the initial render:
	1. React takes the component tree and transforms it into a **React Element Tree** (Virtual DOM)
	2. **Virtual DOM**:
		1. Tree of all React elements created from all instances in the component tree
		2. Cheap and fast to construct multiple trees
			1. Even if we need multiple iterations
				1. Why? It is just a JS object
		3. It has nothing to do with "shadow DOM"
			1. Shadow DOM: A browser technology used in things like web-components
3. Suppose there is a state update in a component:
	1. It triggers a re-render
		1. React calls function of the component again
		2. The new react element thus generated is placed in the React Element Tree (Virtual DOM)
		3. **Rendering a component will cause all of its child components to be rendered as well (no matter if props changed or not)**
			1. If updated components return one or more other components, the nested components will be re-rendered as well
				1. If we update the highest component, the entire application will be re-rendered
					1. Necessary because React doesn't know whether children will be affected (React plays it safe)
						1. It does not update the entire DOM
							1. Only Virtual DOM is re-created (not a big problem for small or medium sized applications)

#### What is Reconciliation and Why do we Need it? ####
1. Why not update the entire DOM whenever state changes somewhere in the app?
	1. Creation of Virtual DOM (React Element Tree) is cheap and fast (it is just a JS object)
		1. Writing to DOM is inefficient and wasteful (to always write the entire Virtual DOM to the real DOM, each time a render is triggered):
			1. Writing to the DOM is (relatively) slow
			2. Usually only a **small part of the DOM** needs to be updated
				1. The rest of the DOM can be re-used
	2. For initial render, there is no way of constructing the entire DOM from scratch
		1. It doesn't make any sense doing it again after that
			1. Example: If we click show modal button, `showModal = true`
				1. Only the new DOM related to the modal need to be inserted into the DOM
					1. The rest of the DOM must stay the same
						1. **React reuses as much of the existing DOM as possible** (tries to be as efficient as possible)
							1. How does it do that?
								1. **Reconciliation:** Deciding which DOM elements actually need to be inserted, deleted, or updated, in order to reflect the latest state changes
									1. **The result of the reconciliation process is going to be a list of DOM operations necessary to update the current DOM with the new state**
										1. It is processed by a reconsiler
											1. It is the engine of React (heart) - it allows us to never touch the DOM directly. It tells the React what the next snapshot of UI should look like based on state

#### The Reconciler: Fiber ####
1. Process:
	1. During the initial render of the application, fiber takes the entire element tree (virtual DOM) and builds another tree: Fiber tree
		1. Fiber tree: Special internal tree that has a "fiber" for each component instance and DOM element (in the app)
			1. Unlike React elements in Virtual DOM, **Fibers are NOT re-created on every render**
				1. It is never destroyed (immutable data-structure)
					1. Once it created in the initial render, it is mutated over and over again in future reconciliation steps
			2. Fibers are perfect to keep track of:
				1. Current state
				2. Props
				3. Side effects
				4. List of used hooks
				5. ...
			3. The actual state and props of any component instance are internally stored inside the corresponding fiber in the fiber tree
			4. Each fiber contains a queue of work to do
				1. Updating state
				2. Updating refs
				3. Running registered side-effects
				4. Performing DOM updates
				5. ...
			5. **Fiber is defined as a unit of work**
			6. Fibers are arranged in a different way than the elements in the React Element tree

					App
					 |
					Video---Modal---Btn
							  |
							Overlay
							  |	
							  h3----button

				1. Each first child has a link to the parent
				2. All the other children have a link to the previous sibling
					1. Linked List
						1. Makes it easier for React to process the work associated with each fiber
						2. Both React Element Tree and Fiber tree include DOM elements as well
					2. Both trees are the entire representation of entire DOM structure (not just React components)
			7. Work can be done **asynchronously**
				1. Rendering process (what reconciler does) can be split into chunks, tasks can be prioritized (over others), and work can be **paused**, **reused**, or **thrown away** (if not valid anymore)
					1. Automatic
				2. Practices uses of asynchronous rendering
					1. Enables **concurrent features** like `Suspense` or transitions (React 18)
					2. Long renders **won't block** JS engine
						1. Allows rendering to pause and resume later
							1. Especially good for large application
					3. Possible because render phase does not produce any visible output to the DOM yet

#### Reconciliation in Action ####
1. Steps:
	1. Suppose the state `showModal = true`
	2. If we change `showModal = false`, it triggers a re-render
		1. The `Modal` and all its children are gone 
	3. A new virtual DOM is created
		1. State update in `App`, so **all remaining children** are re-rendered
	4. The New vDOM needs to be reconciled with the fiber tree
		1. Results in `workInProgress` tree
	5. Whenever reconciliation happens, fiber walks through the entire tree (step by step) and analyzes what needs to change in the current fiber tree and the updated fiber tree
		1. Uses Virtual DOM
		2. **Comparing elements based on their position in the tree** - diffing
		3. It has the following marking is done in fiber tree:
			1. DOM Update (change of text in Btn)
			2. DOM Deletions (They are no longer in vDOM but are present in fiber tree)
			3. No updates (didn't change in the vDOM)
	6. After diffing, the DOM manipulations will be placed in a list called "list of effects"
		1. Used in commit phase to mutate the DOM

### How Rendering Works: The Commit Phase ###
1. List of DOM updates (output of render phase)
	1. This list is used in the commit phase
2. **React writes to the DOM**: insertions, deletions, and updates (list of DOM updates are "flushed" to the DOM)
	1. React goes through the effects list and applies them one-by-one to the actual DOM elements (that were already existing in the DOM tree)
3. **Committing is synchronous**: DOM is updated in one go, it can't be interrupted. This is necessary so that the DOM never shows partial results, ensuring a consistent UI (in sync with state at all times).
	1. It cannot be paused or interrupted
4. After the commit phase completes, the `workInProgress` fiber tree becomes the `current` tree **for the next render cycle**
	1. Fiber trees are never discarded and never recreated from scratch
		1. They are reused to save precious rendering time
5. Browser paint:
	1. It re-paints the screen when it has idle time
		1. Updated UI on the screen
			1. We need to understand how browsers work internally
6. **Commit Phase** implementation:
	1. It is done my `ReactDOM` (and not `React`)
		1. `React` does not touch the DOM. React **only renders**. It doesn't know where the render result will go
			1. Why? React can be used on different platforms ("hosts")
				1. React Native - used to build native applications for iOS and Android
				2. Remotion - used to build videos using React
				3. Other renderers (they only commit but not render) - Word documents, PDFs, Figma designs, ...
	2. vDOM is only for web-applications, React Element Tree is preferred because React can be used for other kinds of applications
		1. That is why we import `React` and `ReactDOM`

#### Recap: Putting It All Together ####
1. Trigger <- happens only on inital render and state updates
2. Render Phase <- Does not produce any visual output
	1. Renders all component instances that needs rendering to re-render
	2. Steps:
		1. Updated React Elements will be placed in a new Virtual DOM (tree of React elements)
			1. All child components will be re-rendered (because React doesn't know if child components have been affected or not)
		2. Virtual DOM is reconciled with the Current Fiber Tree (representation of Element Tree before the state update)
			1. Why? It is slow and inefficient to rebuild the DOM tree, each time something on the screen must be updated
			2. Reconciliation finds the smallest number of DOM updates that reflects the latest state updates on the screen
				1. Done by a reconciler called fiber
		3. For each React element and a DOM element, there is a fiber
			1. Fiber - holds actual component state, props, and a queue of work
				1. Queue of work (after reconciliation) contains DOM updates needed for the element
			2. The computation for DOM updates is performed by a diffing algorithm
				1. It compares step-by-step the elements in the new virtual DOM with the elements in the current fiber tree (to know what has changed)
			3. The result of reconciliation and diffing process is a second updated fiber tree & a list of DOM updates
			4. **Asynchronous:** Fiber's work can be split, prioritized, paused, resumed
				1. Necessary for concurrent features
				2. Necessary to prevent JS engine from being blocked by complex render processes
		4. List of DOM updates will be written to the DOM in the commit phase
			1. Renderer (ReactDOM say) will insert, delete, and update DOM elements
				1. We end up with updated DOM that reflects the new state of the application
			2. **Synchronous**: DOM updates are written in one go, to keep UI consistent
		5. Once the browser realizes that the DOM has been updated, it starts a new browser paint to visually update UI on the screen
2. Some of the things discussed have practical implications, and implications on performance

### How Diffing Works ###
1. Diffing uses 2 fundamental assumptions (rules):
	1. Two elements of different types will **produce different trees**
	2. Elements with a stable `key` prop (key that is consistent over time) **stay the same across renders**
		1. The assumptions are obvious, but allows React to go from (1Billion [O(n^3))] to 1000 [O(n)] operations per 1000 processed elements
2. Two situations that need to be considered
	1. Same position, **different** elements (between two renders)
		1. Examples:

				<div>
					<SearchBar />
				</div>
				<main>...</main>

					|
					v

				<header>
					<SearchBar />
				</header>
				<main>...</main>

			1. React assumes **entire sub-tree is no longer valid**
				1. The element and its children will be destroyed and removed from the DOM (**including state**)
					1. The `div` is removed and a new `header` and `SearchBar` component instances are created
						1. If there were components with state, **that state will not be recovered**
							1. State is reset
			2. It works the same for React elements (`SearchBar` changing to `ProfileMenu` component)
				1. State is destroyed

	2. Same position, **same** elements
		1. Example:

				<div>
					<SearchBar wait={1} />
				</div>
				<main>...</main>
					|
					v
				<div>
					<SearchBar wait={5} />
				</div>
				<main>...</main>

			1. Element will be kept (as well as child elements), **including state**
				1. Implications:
					1. Preserves state of both DOM elements and React elements
		2. Changes:
			1. React Elements: **New props** are passed if they changed between renders
			2. DOM Elements: React will just mutate the DOM element **attributes**
				1. React tries to be as efficient as possible, so the DOM elements will stay the same (they will not be removed from the DOM)
					1. State is also not destroyed
			3. Sometimes this is **not** what we want... Then we can use the `key` prop

### Diffing Rules in Practice ###
1. Example:
	1. If we click on different tabs, the state of `TabContent` does not change because it remains in the same position in the Component Tree
	2. If the `TabContent` is replaced with `DifferentContent` component, the state is destroyed. Once we navigate back the `TabContent` the state is reset

### The Key Prop ###
#### What is the Key Prop? ####
1. Key Prop
	1. Special prop that we can use to tell the diffing algorithm that an element is **unique** (by giving a unique id)
		1. Works for both DOM elements and React elements
	2. Allows React to **distinguish** between multiple instances of the same component type
		1. Why do we need to do this?
			1. When a key **stays the same across renders**, the element will be kept in the DOM (even if the position in the tree changes)
				1. This is why we need to **use keys in lists**
	2. When a key **changes between renders**, the element will be destroyed and a new one will be created (even if the position in the tree is the same as before)
		1. **Using keys to reset state** - use-case

#### Keys in Lists [Stable Key] ####
1. Example:

		<ul>
			<Question question={q[1]} />
			<Question question={q[2]} />
		</ul>
			| Adding new list item
			v
		<ul>
			<Question question={q[0]} />
			<Question question={q[1]} />
			<Question question={q[2]} />
		</ul>

	1. The original items appear in different positions in the React element tree (no longer 1st and 2nd children, but 2nd and 3rd children)
	2. Same elements, but **different position in tree**, so they are removed and recreated in the DOM (bad for performance)
		1. Wasted work (React doesn't know that)
	3. Solution: Keys (keys help us uniquely identify elements)

			<ul>
				<Question key='q1' question={q[1]} />
				<Question key='q2' question={q[2]} />
			</ul>
				| Adding new list item
				v
			<ul>
				<Question key='q0' question={q[1]} />
				<Question key='q1' question={q[1]} />
				<Question key='q2' question={q[1]} />
			</ul>

		1. The elements have stabe keys (keys that stay the same across renders)
		2. The elements will be kept in the DOM
		3. **Different position in the tree, but the key stays the same**, so the elements will be kept in the DOM
			1. Always use keys!
				1. If we have multiple child elements of the same type

#### Key Prop to Reset State (Changing Key) ####
1. Example:

		<QuestionBox>
			<Question
				question={{
					title: 'React vs JS',
					body: 'Why should we use React?',
				}}
			/>
		</QuestionBox>
			|
			v
		<QuestionBox>
			<Question
				question={{
					title: 'Best course ever',
					body: 'This is THE React course!',
				}}
			/>
		</QuestionBox>

	1. `Question` state (`answer`):
		1. Set to 'React allows us to build apps faster'
	2. Now `Question` changes to 'This is THE React course!'
		1. Diffing rule: If we have the same element at the same position in the tree, the **DOM element and state** will be kept
			1. State was preserved. NOT what we want
	3. Solution:

			<QuestionBox>
				<Question
					question={{
						title: 'Best course ever',
						body: 'This is THE React course!',
					}}
					key="q23"
				/>
			</QuestionBox>

		1. `key` prop uniquely identifies the question
			1. When a new question appears, we can give it a different key

					<QuestionBox>
						<Question
							question={{
								title: 'Best course ever',
								body: 'This is THE React course!',
							}}
							key="q89"
						/>
					</QuestionBox>

				1. React identifies it to be a different component instance, so React instantiates a new React element
					1. State will be reset (`answer` is set to empty)

### Resetting State With the Key Prop ###
1. Fixing Tabbed component

		<TabContent
          item={content.at(activeTab)}
          key={content.at(activeTab).summary}
        />

### Using the Key Prop to Fix Our Eat-'N-Split App ###
1. Code:

		{selectedFriend && (
	      <FormSplitBill
	        selectedFriend={selectedFriend}
	        onSplitBill={handleSplitBill}
	        key={selectedFriend.id}
	      />
	    )}

### Rules for Render Logic: Pure Components ###
1. Rules
2. What is render logic?

#### The Two Types of Logic in React Components ####
1. Render Logic
	1. Code that lives at the **top level** of the component function
	2. Participates in **describing** how the component view (of an instance) looks like
	3. Example:

			function Question({ question }) {
				const [newAnswer, setNewAnswer] = useState(''); // Participates in describing how component view looks like
				const numAnswers = question.answers.length ?? 0; // Participates in describing how component view looks like

				const handleNewAnswer = function (e) {
					if (question.closed) return;
					setNewAnswer(e.target.value);
				}

				const createList = function () {
					// Participates in describing how component view looks like
					return (
						<ul>
							{question.answers.map((q) => (
								<li>{q}</li>
							))}
						</ul>
					);
				}

				// Participates in describing how component view looks like
				return (
					<div>
						<h3>{question.title}</h3>
						<p>{question.body}</p>
						{question.hasAnswer ? (
							createList()
						) : (
							<input
								value={newAnswer}
								onChange={handleNewAnswer}
							/>
						)
					</div>
				)
			}

		1. Render logic: It is the code that is executed **every time** the component renders (each time the function is called)

2. Event Handler Functions
	1. Executed as a **consequence of the event** that the handler is listening for (`change` event in the example)
		1. `handleNewAnswer` - event handler function
	2. Code that actually **does things**: update state, perform an HTTP request, read an input field, navigate to another page, etc (all things that change and manipulate the application in some way).
		1. Code that makes things happen in the application
3. React requires that all components are pure when it comes to render logic for the app to work as expected

#### Refresher: Functional Programming Principles ####
1. **Side effect:** Dependency on or modification of any data outside the function scope. **"Interaction with the outside world"**. Examples: mutating external variables, HTTP requests, writing to DOM, setting timers

		const areas = {};
		
		function circleArea(r) {
			areas.circle = 3.14 * r * r;
		}

	1. Side effect: Outside variable mutation
2. **Pure function:** A function that has **no** side effects
	1. Does **not** change any variables outside its scope
	2. Give the **same input**, a pure function always returns the **same output**

			function circleArea(r) {
				return 3.14 * r * r;
			}

		1. Makes it predictable
	3. Unpredictable functions:

			function circleArea(r) {
				const date = Date.now();
				const area = 3.14 * r * r;
				return `${date}: ${area}`
			}

		1. The output will always be different
3. **Side effects are not bad!**: A program can only be useful if it has some interaction with the outside world
	1. If an app doesn't fetch any data or never writes to the DOM is useless
		1. Solution: To make useful and bug-free applications, we need to know when and how to cause side-effects

#### Rules for Render Logic ####
1. **Components must be pure when it comes to render logic:** given the same props (input), a component instance should always return the same JSX (output)
	1. **Render logic must produce no side effects**: no interaction with the "outside world" is allowed. So, in render logic:
		1. Do NOT perform **network requests** (API calls)
		2. Do NOT start **timers**
		3. Do NOT directly **use the DOM API**
		4. Do NOT **mutate objects or variables** outside of the function scope
			1. This is why we can't mutate props (hard rule)
				1. Doing so is a side effect
		5. Do NOT **update sate (or refs):** this will cause an infinite loop!
			1. They are not side effects though
		6. Other side effects may be allowed because they are not harmless:
			1. `console.log`
			2. Generating random numbers
	2. Side effects are allowed (and encouraged) in **event handler functions!** There is also a special hook to **register side effects** (`useEffect`)
		1. If we need to cause side effects as soon as a function executes, we can register that side effect using a special hook called `useEffect`

### State Update Batching ###
#### How State Updates are Batched ####
1. Renders are **not** triggered immediately, but **scheduled** for when the JS engine has some "free time". There is also batching of multiple `setState` calls in event handlers
2. Example:

		const [answer, setAnswer] = useState('');
		const [best, setBest] = useState(true);
		const [solved, setSolved] = useState(false);

		const reset = function () {
			setAnswer('');
			console.log(answer);
			setBest(true);
			setSolved(false);
		}

		return (
			<div>
				<button onClick={reset}>Reset</button>
				{/* ... */}
			</div>
		);

	1. Event handler function: `reset`
		1. How are the 3 pieces of state updated behind the scenes
			1. React does not update one state at a time (which are in the same event handler)
				1. The state updates will be batched into one state update for the event-handler
				2. **React triggers one re-render and commit per event handler**
					1. The state changes represent one view, and hence React updates screen only once (we may not be interested in partial render)
						1. Better performance
	2. What is the value of `answer` be at this point?
		1. State is stored in the Fiber tree during **render phase**
		2. At this point, re-render has **not happened yet**
			1. React is reading the function line by line and didn't update the state yet, and not re-rendered yet
				1. The `answer` still contains **current state**, **not** the updated state ('')
				2. The state is stale
	3. Updating state in React is asynchronous
		1. Because updated state variables are **not** immediately available after `setState` call, **but only after the re-render**.
		2. This also applies when **only one** piece of state is updated
		3. If we need to update state **based on pervious update**, we use `setState` with callback (`setAnswer(answer => ...)`) (instead of a single value)

#### Batching Beyond Event Handler Functions ####
1. Before React 18, React only did automatic batching only in event-handlers (not in situations in which a browser event has alreay happened)
	1. There are situations in which we need to update the state long after a browser event has already happened
		1. Examples:
			1. Timeouts (running `reset` function a second after the `click` event)

					setTimeout(reset, 1000);

			2. Promises (running `reset` function only after some data is fetched)

					fetchStuff().then(reset);
		
			3. Native events

					el.addEventListener('click', reset);

		1. Before React 18, state updates inside a function that is called after timeout or primises were not batched.
			1. React would update state variables one by one
		2. With latest React version, we get automatic batching all the time everywhere in the code
		3. In certain situations, in which automatic batching can be problematic
			1. Solution: We can **opt out** of automatic batching by wrapping a state update in `ReactDOM.flushSync()` (but you will never need this)

### State Update Batching in Practice ###
1. If the new state is equal to the current state, the component is not re-rendered (nor the state is updated)
2. If we are updating state based on the previous state, we must always use a callback function
3. Code:

		function handleInc() {
		  // setLikes(likes + 1);
		  setLikes((likes) => likes + 1);
		}
		
		function handleTripleInc() {
		  // Increased only once. `likes` is 0 in all the three cases. The state is stale
	      // setLikes(likes + 1);
	      // setLikes(likes + 1);
	      // setLikes(likes + 1);
	
	      // In each callback, we get access to the latest updated state
	      setLikes((likes) => likes + 1); // 0 + 1
	      setLikes((likes) => likes + 1); // 1 + 1
	      setLikes((likes) => likes + 1); // 2 + 1
	    }

	1. Batching works with other functions as well (not only event-handlers)

			function handleUndoLater() {
    		  setTimeout(handleUndo, 2000); // handleUndo - is just another function that is called at a later time
			}

### How Events Work in React ###
1. How React handles events and how they work behind the scenes

#### DOM Refresher: Event Propagation and Delegation ####
1. Example:

		Document <html> <- DOM tree (not Fiber tree or React element tree)
			|
		<body>
			|
		<div>
		#root
			|
		<header>
		.topbar
			|
		<div>
		.options
			|
		+---+------+---------+
		|          |         |
		<button>   <button>  <button>
		.btn       .btn      .btn

	1. As soon as an event is fired, a new event object will be created
		1. It is not created where the event occurred
			1. The object will be created at the root of the document (top of the tree)
	2. The event object travels down the tree until it reaches the target element in the capturing phase
		1. Target element: Element on which the event was first triggered
		2. At the target, we can place an event handler on the element
	3. After the event object reached the target element, it travels up the tree upto the root of the tree in the bubbling phase
2. During capturing and bubbling phases, an event object goes through every single parent and child element, one by one
	1. It seems the event has originated in each of the DOM elements
	2. By default, event handlers listen to events on the target **and during the bubbling phase**
		1. Every single event-handler in a parent will be executed during the bubbling phase (if they are listening to the same type of event)
			1. We can **prevent bubbling** with `e.stopPropagation()` function (works in vanila JS, and React)
3. Event Delegation:
	1. Handling events for multiple elements centrally in **one single parent element**
		1. If there are 1000 buttons, if each button has an event handler, it would be problematic for the app's performance and memory usage
			1. Example: Add handler to **parent** (`.options`)
				1. When a click happens on one of the buttons, the event will bubble up to the `.options` element.
				2. We can check for **target** element (`e.target`)
				3. If **target** is one of the `<button>`s, handle the event
					1. Very common in vanilla JS apps, but no so much in React apps
						1. Why talk about it?
							1. Sometimes we might find strange behavior related to events in our application (which might have to do with event bubbling)
							2. React does this behind the scenes

#### How React handles Events ####
1. If we want to attach an event handler to one of the buttons or to another DOM element

		<button
			className="btn"
			onClick={() => setLoading(true)}
		/>

	1. What React does is the following:

			document
				.querySelector('#root')
				.addEventListener(
					'click',
					() => setLoading(true)
				);

		1. `#root` container is the DOM element in which the React app is displayed
		2. React registers all event handlers on the **root DOM container**. This is where **all events are handled**
			1. React does it in a more complex way
			2. React registers **one event handler function per event type** at the root node of the fiber tree during the render phase
				1. If we have multiple event-handler functions per event type, React bundles them together into one handler function in the root node of the fiber tree
				2. Behind the scenes, React performs **event delegation** for all events in our applications
					1. To the root DOM container where they are handled
			3. Flow:
				1. When an event occurs (button is clicked), and event is created in the Document root and it descends down until it is captured by the target.
				2. The event object will bubble back up as soon as the event reaches the root container (where React registered all the handlers), the event is handled (if a handler matches the target event type)
					1. Usually `div#root`, but can be **any** DOM element
				3. After the event is handled, it continues to bubble up and disappears

#### Synthetic Events ####
1. How event objects work behind the scenes
	1. Whenever we declare an event handler, React gives us access to the event object that was created (just like JS)
		1. In React the event object is different
			1. In vanilla JS, we get access to the native DOM event object
				1. `PointerEvent`
				2. `MouseEvent`
				3. `KeyboardEvent`
				4. ...
			2. React gives us **SyntheticEvent** (a thin wrapper around DOM's native event object)
				1. They are similar to native event objects but they add or change some functionality on top of them
				2. They have **same interface** as native event objects, like `stopPropagation()`, and `preventDefault()`
				3. Fixes browser inconsistencies, so that events work in the exact **same way in all browsers**
				4. **Most synthetic events bubble** (including focus, blur, and change), except for scroll
2. Event Handlers in React vs JS
	1. Attributes for event handlers are named used `camelCase` (prop-names) (`onClick` instead of `onclick` or `click` (if we use `addEventListener`))
	2. In vanilla JS, to stop the default behavior of the browser in response to an event, we can return `false` from an event handler function
		1. Example: Preventing browser from reloading the page when we click on `submit`
		2. Default behavior can **not** be prevented by returning `false` (only by using `preventDefault()` on synthetic event object)
	3. Attach `Capture` to the event handler name, if you need to handle during **capture phase** (example: `onClickCapture`)

### Libraries vs. Frameworks & The React Ecosystem ###
#### First, an Analogy ####
1. Making a sushi for the first time
	1. All-in-one Kit
		1. Ease of mind: All ingredients are included
		2. No choice
			1. You're stuck with the kit's ingredients (we may not like one or more of them)
	2. Separate Ingredients
		1. Freedom: You can choose the best ingredients
		2. Decision fatigue: You need to research and buy all ingredients separately
2. Front-end technologies
	1. All-in-one kit
		1. Angular
		2. Vue
		3. Swelt
	2. Separate Ingredients
		1. React

#### Framework vs Library ####
1. Framework	
	1. Easy of mind: Everything you need to build a complete application **is included** in the framework ("batteries included")
		1. A complete structure that includes everything we need to build a complete large scale application
	2. Frameworks include everything
		1. Angular:
			1. HTTP Requests
			2. Styling
			3. Routing
			4. Form management
	3. No choice: We're stuck with the framework's tools and conventions (which is not always bad!)
2. Library
	1. Pieces of code that developers share for other developers to use
		1. Example: React
			1. React - View library
				1. It just draws components on a UI (view)
	2. To build a large-scale SPA, we need to include many third-party libraries for
		1. HTTP Requests
		2. Styling
		3. Routing
		4. Form management
		5. ...
	3. We can build React apps with just React (without libraries)
		1. But only for small apps
		2. When learning React
	4. Freedom: You can (or need to) **choose multiple 3rd-party libraries** to build a complete application
		1. We can choose the one we like the most
		2. Every app has different requirements and can have a different combination of libraries
	5. Decision fatigue: You need to **research**, **download**, **learn**, and **stay-up-to-date** with multiple external libraries
		1. We will have a very good understanding of the most important libraries that we usually include in most React projects

#### React 3rd-Party Library Ecosystem ####
1. React's popularity has led to a huge ecosystem of 3rd-party libraries which can be included in our app for different needs
	1. Routing (for SPAs):
		1. **React Router**
		2. React Location
	2. HTTP requests:
		1. **JS** `fetch()`
		2. Axios
	3. Remote state management:
		1. **React Query**
		2. SWR
		3. Apollo
	4. Global state management:
		1. **Context API**
		2. **Redux**
		3. Zustand
	5. Styling
		1. **CSS modules**
		2. **Styled components**
		3. **Tailwindcss**
	6. Form management
		1. **React Hook Form**
		2. Formik
	7. Animations/Transitions
		1. Motion
		2. react-spring
	8. UI components
		1. MJ
		2. Chakra
		3. Mantine
2. Many developers were overwhelmed by the many decisions that need to be made for choosing 3rd-party libraries, which led to the development of opinionated React frameworks such as:
	1. Nextjs
	2. Remix
	3. Gatsby

#### Frameworks Build on Top of React ####
1. Next.js, Remix, and Gatsby are React frameworks because they are built on top of React
	1. They extend React functionality
	2. Opinionated: Other developers have included their own opinions on how to handle stuff like the following into their frameworks
		1. Routing
		2. State-management
		3. Styling
2. In Vanilla React app, we need to make the decisions on what external libraries to use
3. In Next.js, Remix, and Gatsby, some of the decisions have already been taken
	1. Makes project development much easier, faster, and lead to better overall developer experience
4. Different frameworks specialize in different aspects
	1. All of them offload much of the setup work from us
5. **React frameworks offer many other features:** server-side rendering (SSR), static site generation (SSG), better developer experience (DX), etc.
	1. Many can be described as full-stack frameworks
		1. We can build full-stack apps with them (using React as the base layer)
6. **We can learn the frameworks only if we master React, and the third-party frameworks**

### Section Summary: Practical Takeaways ###
#### Practical Summary ####
1. Practical takeaways and conclusions (we need them in the future)
2. A **component** is like a blueprint for a piece of UI that will eventually exist on the screen. When we "use" a component, React constructs a **component instance**, which is like an actual physical manifestation of a component, containing props, state, and more. A component instance, when rendered, will return a **React element**
	1. Similar to a blueprint of a house, and actual houses are built using the blueprint
3. "Rendering" only means **calling component functions** and calculating what DOM elements need to be inserted, deleted, or updated. It has nothing to do with writing to the DOM. Therefore, **each time a component instance is rendered and re-rendered, the function is called again**
	1. Writing to the DOM is "committing" in React language
4. Only the **initial app render** and **state updates** can cause a render, which happens for the **entire application**, not just one single component
	1. The Render process is execute for all components
5. When a component instance gets re-rendered, **all its children will get re-rendered as well**. This doesn't mean that all children will get updated in the DOM, thanks to reconciliation, which checks which elements have actually changed between two renders. But all this re-rendering can still have an impact on performance (more on that later in the course)
6. Diffing is how React decides which DOM elements needs to be added or modified. If, between renders, a certain React element **stays at the same position in the element tree**, the corresponding DOM element and component state will stay the same. If the element **changed to a different position**, or if it's a **different element type**, the DOM element and state will be destroyed.
	1. They will be reset
7. Giving elements a key prop allows React to distinguish between multiple component instances. **When a key stays the same across renders**, the element is kept in the DOM. This is why we need to use keys in lists. **When we change the key between renders**, the DOM element will be destroyed and rebuilt. We use this as a **trick to reset state**
8. **Never declare a new component inside another component!** Doing so will re-construct the nested component every time the parent component re-renders. React will always see the nested component (like a new variable) as **new**, and therefore **reset its state** each time the parent state is updated
	1. Always declare components at the top-level of the file (never inside another component)
9. The logic that produces JSX output for a component instance ("render logic") is **not allowed to produce any side effects**: no API calls, no timers, no object or variable mutations, no state updates. **Side effects are allowed in event handlers** and **useEffect** (next section)
10. The DOM is updated in the commit phase, **but not by React, but by a "renderer" called ReactDOM**. That's why we always need to include both libraries in a React web app project. We can use other renderers to use React on different platforms, for example to build mobile or native apps (with React Native)
11. Multiple state updates inside an event handler function are **batched**, so they happen all at once, **causing only one re-render** (for performance). This means we can **not access a state variable immediately after updating it**: state updates are **asynchronous**. Since React 18, batching also happens in timeouts, promises, and native event handlers.
12. When using events in event handlers, we get access to a **synthetic event object**, not the browser's native object, so that **events work the same way across all browsers**. The difference is that **most synthetic events bubble**, including focus, blur, and change, which do not bubble as native browser events. Only the scroll event does not bubble.
13. **React is a library, not a framework**. This means that you can assemble your application using your favorite third-party libraries (for flexibility and freedom). The downside is that you need to find and learn all these additional libraries. No problem, as you will learn about the most commonly used libraries in this course.

## Section 12: Effects and Data Fetching ##
### Section Overview ###
1. Topics:
	1. Data fetching is essential
	2. Effects with `useEffect` hook
		1. `usePopcorn` project
		2. Side effects
		3. How and when effects are executed
	3. Effect cleanup
	4. Real-world application!

### The Component Lifecycle ###
1. Lifecyle of components

#### Component (Instance) Lifecycle ####
1. Encompasses the different phases, a specific component can go through over time
2. Phases:
	1. Mount/Initial Render
		1. Component instance is rendered for the **first time**
		2. Fresh state and props are **created** (for the component instance)
			1. Component is born in this phase
	2. Re-Render (unlimited number of times) (optional)
		1. Happens when:
			1. **State** changes
				1. This is only for the entire application
			2. **Props** change
			3. **Parent** re-renders
			4. **Context** changes
		2. All components do not go through this phase
			1. Some components are simply mounted and unmounted
	3. Unmount (when no longer needed) (can happen when a user navigates to a new section or page or close the app)
		1. Component instance is **destroyed** and **removed**
		2. State and props are **destroyed**
2. **We can hook into the lifecycle**
	1. We can define code to be executed at these specific points in time
		1. We do so using the `useEffect` hook

### How NOT to Fetch Data in React ###
1. Loading data
	1. Doing it the wrong way
		1. We must never update state in the Render logic
			1. If we break the rule?
2. Movies:
	1. OMDB (Open source version of IMDB)
		1. Generate API Key (for free)
	2. Fetching movies data:

			fetch(`http://www.omdbapi.com/?apikey=${KEY}&s=interstellar`)
    		  .then((res) => res.json())
    		  .then((data) => setMovies(data.Search));

		1. Runs infinite number of requests (never stops)
			1. Why?
				1. Setting state causes component to re-render
				2. Re-render will execute the function again
				3. The function fetches data again and sets the set
				4. Thus the infinite loop
					1. Hence, we must not set state in the render logic

		2. Another example:

				setWatched([]); // Causes too many re-renders

3. How to set state?
	1. In the `useEffect` hook

### useEffect to the Rescue ###
1. It gives us a place where we can safely write side effects
	1. Side effects registered with the `useEffect` hook will only be executed **after certain renders**
		1. Example: **Only after the initial render**
	2. `useEffect` hook is used to register an effect (a side effect). The effect is the function we pass into the hook.
		1. **After it has been painted onto the screen** (after render)
2. Code:

		useEffect(function () {
		  // function contains code that we want to run as a side-effect
		  // It is registered to be run at a certain point in time
		  fetch(`http://www.omdbapi.com/?apikey=${KEY}&s=interstellar`)
		    .then((res) => res.json())
		    .then((data) => setMovies(data.Search));
		}, []); // It doesn't return anything
		// Second argument is dependency array
		// `[]` - means that the hook will run only on mount (inital render)
		// Good if we want to fetch data as soon as the application loads

### A First Look at Effects ###
1. What is an effect, and how is it different from an event-handler function?

#### Where to Define Side Effects ####
1. Review: A **side effect** is basically any "interaction between a React component and the world outside the component". We can also think of a side effect as "code that actually does something" (useful to happen). Examples: Data fetching, setting up subscriptions, setting up timers, manually accessing the DOM, etc.
2. Side Effect:
	1. We need side effects all the time (when we build React apps). They make our applications **do something**. **Not** in render logic (side effects should not occur **during** the execution of the render logic. It can be after)!
	2. We can define side-effects in two different places in React
		1. In Event Handlers
			1. Event handlers are functions triggered by events: `onClick`, `onSubmit`, etc.
			2. Sometimes this is **not enough** for the application's needs
				1. We might need code that executes automatically **as soon as a component renders** (triggered by rendering)
					1. Solution: Effects (`useEffect`)
		2. Using Effects
			1. Effects allow us to write code that will run at **different moments**:
				1. Mount
				2. Re-render
				3. Unmount 

#### Event Handlers vs. Effects ####
1. When? (Both produce the same result, but at different moments)
	1. Event Handlers
		1. Executed when the **corresponding event happens**
		2. Used to **react** to an event
		3. **Preferred way of defining side effects!**
	2. Effects (`useEffect`)
		1. Executed **after the component mounts** (initial render), and **after subsequent re-renders** (according to dependency array)
			1. We can use the dependency array to tell the component to run `useEffect` after a component re-renders
		2. Each effect can returns a `cleanup` function (a function which will be called before the component re-renders or unmounts)

				useEffect(function () {
					fetch(...)
						.then(...)
						.then(...);

					return () => console.log('Cleanup');
				}, []);

			1. We should not think about lifecycle, but about synchronization.
				1. Used to keep a component **synchronized with some external system** (in this example, with the API movie data)
			2. We must not over-use `useEffect` hook
				1. Everything that can handed using event-handlers must be handled in event-handlers

### Using an async Function ###
1. If we use `async` function inside `useEffect`, we get a warning that effect callbacks are synchronous to prevent race-conditions (we cannot return a promise from a `useEffect` callback).
2. In React 18, in strict mode, the effects will run twice
	1. This is only true in development mode.
		1. If we remove from String mode, effect is called only once
	2. This doesn't happen in production

### Adding a Loading State ###
1. If moves are loaded in the background, we want to display a loading indicator
	1. Throttle network using Slow 3G
	2. Solution: More state
		1. A state variable that indictes that the data is still being loaded
			1. When the data is loaded, we can display the data and not the loading indicator
2. Code:

		import { useEffect, useState } from "react";

		const tempMovieData = [
		  {
		    imdbID: "tt1375666",
		    Title: "Inception",
		    Year: "2010",
		    Poster:
		      "https://m.media-amazon.com/images/M/MV5BMjAxMzY3NjcxNF5BMl5BanBnXkFtZTcwNTI5OTM0Mw@@._V1_SX300.jpg",
		  },
		  {
		    imdbID: "tt0133093",
		    Title: "The Matrix",
		    Year: "1999",
		    Poster:
		      "https://m.media-amazon.com/images/M/MV5BNzQzOTk3OTAtNDQ0Zi00ZTVkLWI0MTEtMDllZjNkYzNjNTc4L2ltYWdlXkEyXkFqcGdeQXVyNjU0OTQ0OTY@._V1_SX300.jpg",
		  },
		  {
		    imdbID: "tt6751668",
		    Title: "Parasite",
		    Year: "2019",
		    Poster:
		      "https://m.media-amazon.com/images/M/MV5BYWZjMjk3ZTItODQ2ZC00NTY5LWE0ZDYtZTI3MjcwN2Q5NTVkXkEyXkFqcGdeQXVyODk4OTc3MTY@._V1_SX300.jpg",
		  },
		];
		
		const tempWatchedData = [
		  {
		    imdbID: "tt1375666",
		    Title: "Inception",
		    Year: "2010",
		    Poster:
		      "https://m.media-amazon.com/images/M/MV5BMjAxMzY3NjcxNF5BMl5BanBnXkFtZTcwNTI5OTM0Mw@@._V1_SX300.jpg",
		    runtime: 148,
		    imdbRating: 8.8,
		    userRating: 10,
		  },
		  {
		    imdbID: "tt0088763",
		    Title: "Back to the Future",
		    Year: "1985",
		    Poster:
		      "https://m.media-amazon.com/images/M/MV5BZmU0M2Y1OGUtZjIxNi00ZjBkLTg1MjgtOWIyNThiZWIwYjRiXkEyXkFqcGdeQXVyMTQxNzMzNDI@._V1_SX300.jpg",
		    runtime: 116,
		    imdbRating: 8.5,
		    userRating: 9,
		  },
		];
		
		function Navbar({ children }) {
		  return (
		    <nav className="nav-bar">
		      <Logo />
		      {children}
		    </nav>
		  );
		}
		
		function Logo() {
		  return (
		    <div className="logo">
		      <span role="img">🍿</span> {/* No need to break */}
		      <h1>usePopcorn</h1>
		    </div>
		  );
		}
		
		function Search() {
		  const [query, setQuery] = useState("");
		  return (
		    <input
		      className="search"
		      type="text"
		      placeholder="Search movies..."
		      value={query}
		      onChange={(e) => setQuery(e.target.value)}
		    />
		  );
		}
		
		function NumResults({ movies }) {
		  return (
		    <p className="num-results">
		      Found <strong>{movies.length}</strong> results
		    </p>
		  );
		}
		
		function Main({ children }) {
		  return <main className="main">{children}</main>;
		}
		
		function Box({ element }) {
		  const [isOpen, setIsOpen] = useState(true);
		
		  return (
		    <div className="box">
		      <button className="btn-toggle" onClick={() => setIsOpen((open) => !open)}>
		        {isOpen ? "–" : "+"}
		      </button>
		      {isOpen && element}
		    </div>
		  );
		}
		
		function MovieList({ movies }) {
		  return (
		    <ul className="list">
		      {movies?.map((movie) => (
		        <Movie movie={movie} />
		      ))}
		    </ul>
		  );
		}
		
		function Movie({ movie }) {
		  return (
		    <li key={movie.imdbID}>
		      <img src={movie.Poster} alt={`${movie.Title} poster`} />
		      <h3>{movie.Title}</h3>
		      <div>
		        <p>
		          <span>🗓</span>
		          <span>{movie.Year}</span>
		        </p>
		      </div>
		    </li>
		  );
		}
		
		// function WatchedBox() {
		//   const [watched, setWatched] = useState(tempWatchedData);
		//   const [isOpen2, setIsOpen2] = useState(true);
		
		//   return (
		//     <div className="box">
		//       <button
		//         className="btn-toggle"
		//         onClick={() => setIsOpen2((open) => !open)}
		//       >
		//         {isOpen2 ? "–" : "+"}
		//       </button>
		//       {isOpen2 && (
		//         <>
		//           <WatchedSummary watched={watched} />
		
		//           <WatchedMovieList watched={watched} />
		//         </>
		//       )}
		//     </div>
		//   );
		// }
		
		function WatchedSummary({ watched }) {
		  const avgImdbRating = average(watched.map((movie) => movie.imdbRating));
		  const avgUserRating = average(watched.map((movie) => movie.userRating));
		  const avgRuntime = average(watched.map((movie) => movie.runtime));
		
		  return (
		    <div className="summary">
		      <h2>Movies you watched</h2>
		      <div>
		        <p>
		          <span>#️⃣</span>
		          <span>{watched.length} movies</span>
		        </p>
		        <p>
		          <span>⭐️</span>
		          <span>{avgImdbRating}</span>
		        </p>
		        <p>
		          <span>🌟</span>
		          <span>{avgUserRating}</span>
		        </p>
		        <p>
		          <span>⏳</span>
		          <span>{avgRuntime} min</span>
		        </p>
		      </div>
		    </div>
		  );
		}
		
		function WatchedMovieList({ watched }) {
		  return (
		    <ul className="list">
		      {watched.map((movie) => (
		        <WatchedMovie movie={movie} key={movie.imdbID} />
		      ))}
		    </ul>
		  );
		}
		
		function WatchedMovie({ movie }) {
		  return (
		    <li key={movie.imdbID}>
		      <img src={movie.Poster} alt={`${movie.Title} poster`} />
		      <h3>{movie.Title}</h3>
		      <div>
		        <p>
		          <span>⭐️</span>
		          <span>{movie.imdbRating}</span>
		        </p>
		        <p>
		          <span>🌟</span>
		          <span>{movie.userRating}</span>
		        </p>
		        <p>
		          <span>⏳</span>
		          <span>{movie.runtime} min</span>
		        </p>
		      </div>
		    </li>
		  );
		}
		
		const KEY = "4256c7"; // If it is inside the component, it will get re-created each time the component is re-rendered
		
		const average = (arr) =>
		  arr.reduce((acc, cur, i, arr) => acc + cur / arr.length, 0);
		
		export default function App() {
		  const [movies, setMovies] = useState(tempMovieData);
		  const [watched, setWatched] = useState(tempWatchedData);
		  const [isLoading, setIsLoading] = useState(false);
		  const query = "interstellar";
		
		  useEffect(function () {
		    // function contains code that we want to run as a side-effect
		    // It is registered to be run at a certain point in time
		
		    async function fetchMovies() {
		      setIsLoading(true);
		      const res = await fetch(
		        `http://www.omdbapi.com/?apikey=${KEY}&s=${query}`
		      );
		      const data = await res.json();
		      setMovies(data.Search);
		      console.log(movies); // empty array, because setting state is asynchronous
		      setIsLoading(false);
		    }
		
		    fetchMovies();
		  }, []); // It doesn't return anything
		  // Second argument is dependency array
		  // `[]` - means that the hook will run only on mount (inital render)
		  // Good if we want to fetch data as soon as the application loads
		
		  // setWatched([]); // Causes too many re-renders
		
		  return (
		    <>
		      <Navbar>
		        <Search />
		        <NumResults movies={movies} />
		      </Navbar>
		      <Main>
		        <Box element={isLoading ? <Loader /> : <MovieList movies={movies} />} />
		        <Box
		          element={
		            <>
		              <WatchedSummary watched={watched} />
		              <WatchedMovieList watched={watched} />
		            </>
		          }
		        />
		        {/* <Box>
		          <MovieList movies={movies} />
		        </Box>
		        <Box>
		          <WatchedSummary watched={watched} />
		          <WatchedMovieList watched={watched} />
		        </Box> */}
		      </Main>
		    </>
		  );
		}
		
		function Loader() {
		  return <p className="loader">Loading...</p>;
		}

### Handling Errors ###
1. When we do data fetching in web applications, and dealing with async data, we must assume that something might go wrong.
	1. What can go wrong?
		1. Users losing their internet connections
			1. Slow 3G
			2. Once movies are loading, we select offline
				1. Console log: Failed to fetch
					1. Users lost internet connection
						1. We want to display error message on the screen
							1. Reacting to errors is not built into `fetch`

### The useEffect Dependency Array ###
#### What's the USEEFFECT Dependency Array? ####
1. The dependency array
	1. By default, effects run **after every render**. We can prevent that by passing a **dependency array**
		1. Why does `useEffect` need an array of dependencies?
			1. Without the dependency array, React doesn't know **when** to run the effect.
				1. **Each time one of the dependencies changes, the effect will be executed again**
	2. What are dependencies?
		1. Every **state variable** and **prop** used inside the effect **MUST be included in the dependency array**
2. Example:

		const title = props.move.Title;
		const [userRating, setUserRating] = useState('');

		useEffect(
			function () {
				if (title) return;
				document.title = `${title} ${userRating && (Rated ${userRating} )
				}`;

				return () => (document.title = 'userPopcorn');
			},
			[title, userRating]
		);

	1. Both `title` and `userRating` must be in the dependency array, since we are using both in the `useEffect` hook.
		1. Otherwise, if the `title` or `userRating` changes, React will not know about the change to execute the `useEffect` code
			1. The bug is called: "stale closure" (later)

#### UseEffect is a Synchronization Mechanism ####
1. The machanics of effects:
	1. `useEffect` is like an **event listener** that is listening for one dependency to change. **Whenever a dependency changes, it will execute the effect again**
2. Dependencies:
	1. `[title, userRating]`
		1. `title` changes -> Effect is executed again
		2. `userRating` changes -> Effect is executed again
3. Effects **react** to updates to state and props used inside the effect (the dependencies). So **effects are "reactive"** (like state updates re-render the UI)
	1. Extremely useful and powerful
4. **Effects are used to keep a component synchronized with external system**
	1. Some system that lives outside our React-based code
	
			Component state/props -> synchronize with -> external system (side effect)

		1. Example, if we update the `title`, the `title` of the document will get updated
	2. `useEffect` is a synchronization mechanism
		1. **A mechanism to sync the effect with the state of the application**

#### Synchronization and Lifecycle ####
1. Dependency (State or Prop) Changes 
	1. -> Effect is Executed Again
	2. -> Component is re-rendered
2. Effects and component lifecycle are deeply connected (it is not a lifecycle hook, but a synchronization mechanism) 
3. Whe canuse the dependency array to run effects **when the component renders or re-renders**
4. Types of dependency arrays:
	1. `useEffect(fn, [x, y, z]):
		1. Synchronization:
			1. Effect synchronizes with x, y, and z
		2. Lifecycle
			1. Runs on **mount** and **re-renders** triggered by updating x, y, or z
				1. If any other piece of prop or state is updated, this effect will not be executed 
	2. `useEffect(fn, [])`:
		1. Synchronization:
			1. Effect synchronizes with **no state/props**
				1. It doesn't use any values relevant for rendering the component.
					1. It is safe to be executed only once
		2. Lifecycle:
			1. Runs only on **mount** (initial render)
	3. `useEffect(fn)`:
		1. Synchronization:
			1. Effect synchronizes with **everything**
				1. Every state and every prop will be dependencies in this case
		2. Lifecycle
			1. Runs on **every render** (usually bad)

#### When are Effects Executed? ####
1. Timeline:

		|
		- Mount (Initial Render) `<MovieDetails />`
		|
		- Commit
		|
		- Browser Paint
		|
		- Effect (after browser paint)
			Because effects may contain long running processes (fetching data say)
				Otherwise it would block the component, and will see old version of the component for too long
			If effect sets state, an additional render will be required
				Hence we must not overuse effects
		|
		- `title` changes
		|
		- Re-render
		|
		- Commit
		|
		- Layout Effect (Another type of effect that is **very rarely** necessary (`useLayoutEffect`) - discouraged
		|
		- Browser paint
		|
		- [more effects]
		|
		- Effect (since `title` is part of the effect dependency)
		|
		- ... (this can repeat again until component unmounts
		|
		- Unmount

### Synchronizing Queries With Movie Data ###
1. Code examples:

		useEffect(function () {
		  console.log("After initial render"); // Appears second - because it appears before the other effects.
		}, []);
		
		useEffect(function () {
		  console.log("After every render");
		}); // Appears last
		// If `query` is updated, this effect is executed because it runs after every render.
		
		useEffect(
		  function () {
		    console.log("Synchronized with `query` state variable");
		  },
		  [query]
		);

### Selecting a Movie ###
### Loading Movie Details ###
1. Code: Loading movie details

		useEffect(
		  function () {
		    async function getMovieDetails() {
		      setIsLoading(true);
		      const res = await fetch(
		          `http://www.omdbapi.com/?apikey=${KEY}&i=${selectedId}`
		      );
		      const data = await res.json();
		      console.log(data);
		      setMovie(data);
		      setIsLoading(false);
		    }
		    getMovieDetails();
		  },
		  [selectedId]
		);

### Adding a Watched Movie ###
### Adding a New Effect: Changing Page Title ###
1. Changing the title is a side effect
	1. We want to register a side effect using the `useEffect` hook

### The useEffect Cleanup Function ###
1. We want the title to return to original text if we unmount the movie-details component
	1. We want to execute some code when a component unmounts
		1. Solution: Clean up function

			.
			.
			.
			- BROWSER PAINT (after every re-render)
			|
			- CLEANUP (before the next effect is executed again)
			|
			- EFFECT
			|
			- UNMOUNT
			|
			- CLEANUP
			|
			v

#### The Cleanup Function ####
1. Useeffect Cleanup Function
	1. Function that we can **return from an effect** (optional)
	2. Runs on two different occasions:
		1. Before the effect is **executed again** (to cleanup the results of the previous side-effect)
		2. After a component has **unmounted** (to reset the side-effect created if it is necessary)
2. Flow:

		Component renders
			|
			v
		Execute effect if
		dependency array
		includes updated data

		Component unmounts
			|
			v
		Execute cleanup function

2. When do we need a clean-up function?
	1. Necessary whenever the side effect **keeps happening after the component has been re-rendered or unmounted**
		1. Example: HTTP request in an effect
			1. If component is rerendered while the first request is still running, a new second request would be fired-off
				1. Can result in race-condition
					1. Solution: Cancel request (potential cleanup) whenever the component re-renders or unmounts
		2. Example: API subscription -> Cancel subscription
		3. Example: Start timer -> Stop timer
		4. Example: Add event listener -> Remove listener
3. Each effect should do **only one thing**! Use **one useEffect hook for each side effect.** This makes effects easier to clean up.
	1. If we need to use multiple effects, we need to define multiple `useEffect` hooks
		1. Easier to understand
		2. Easier to define cleanup up function

### Clean Up the Title ###
1. Code:

		useEffect(
		  function () {
		    if (!title) return;
		    document.title = `Movie | ${title}`;
		
		    return function () {
		      // clean-up function - runs after each re-render, and when component unmounts
		      document.title = "usePopcorn";
		      console.log(`Clean up effect for movie ${title}`); // `title` - remembered by the function because of closure concept
		        // closure - a function will always remember the variables that were present at the time and place the function was created
		        // The function closed over the `title` variable, and will remember it in the future
		    };
		  },
		  [title]
		);

### Clean Up Data Fetching ###
1. As we type search keyword, we send a request for each letter
	1. Problems:
		1. Having too many requests will slow them down
		2. We will end up downloading too much data (most of which we may not be using)
		3. If an intermediate request takes longer than the others
			1. It would be the last one to arrive
				1. It would be this result that will be stored in the end in the state and used in the UI
					1. A race condition
2. Code:

		useEffect(
		  function () {
		    // function contains code that we want to run as a side-effect
		    // It is registered to be run at a certain point in time
		
		    const controller = new AbortController(); // Browser API
		
		    async function fetchMovies() {
		      try {
		        setIsLoading(true);
		        setError("");
		        const res = await fetch(
		          `http://www.omdbapi.com/?apikey=${KEY}&s=${query}`,
		          { signal: controller.signal }
		        );
		
		        if (!res.ok)
		          throw new Error("Something went wrong with fetching movies");
		
		        const data = await res.json();
		
		        if (data.Response === "False") throw new Error("Movie not found");
		
		        setMovies(data.Search);
		        console.log(data); // empty array, because setting state is asynchronous
		      } catch (err) {
		        console.error(err.message);
		        if (err.name !== "AbortError") setError(err.message);
		      } finally {
		        setIsLoading(false);
		      }
		    }
		
		    if (query.length < 3) {
		      setMovies([]);
		      setError("");
		      return;
		    }
		
		    fetchMovies();
		
		    return function () {
		      controller.abort();
		    };
		  },
		  [query]
		);

### One More Effect: Listening to a Keypress ###
1. If we want to do DOM manipulation, we can use `useEffect`
2. Code:

		useEffect(
		  function () {
		    function callback(e) {
		      if (e.code === "Escape") {
		        onCloseMovie();
		        console.log("CLOSING");
		      }
		    }
		
		    document.addEventListener("keydown", callback); // DOM manipulation. Stepping outside React. Hence, React team calls the `useEffect` hook an escape hatch (escaping from writing code the React way)
		    // Too many event listeners can cause memory problem
		
		    return function () {
		      document.removeEventListener("keydown", callback);
		    };
		  },
		  [onCloseMovie]
		);

3. Full Code:

		import { useEffect, useState } from "react";
		import StarRating from "./StarRating";
		
		const tempMovieData = [
		  {
		    imdbID: "tt1375666",
		    Title: "Inception",
		    Year: "2010",
		    Poster:
		      "https://m.media-amazon.com/images/M/MV5BMjAxMzY3NjcxNF5BMl5BanBnXkFtZTcwNTI5OTM0Mw@@._V1_SX300.jpg",
		  },
		  {
		    imdbID: "tt0133093",
		    Title: "The Matrix",
		    Year: "1999",
		    Poster:
		      "https://m.media-amazon.com/images/M/MV5BNzQzOTk3OTAtNDQ0Zi00ZTVkLWI0MTEtMDllZjNkYzNjNTc4L2ltYWdlXkEyXkFqcGdeQXVyNjU0OTQ0OTY@._V1_SX300.jpg",
		  },
		  {
		    imdbID: "tt6751668",
		    Title: "Parasite",
		    Year: "2019",
		    Poster:
		      "https://m.media-amazon.com/images/M/MV5BYWZjMjk3ZTItODQ2ZC00NTY5LWE0ZDYtZTI3MjcwN2Q5NTVkXkEyXkFqcGdeQXVyODk4OTc3MTY@._V1_SX300.jpg",
		  },
		];
		
		const tempWatchedData = [
		  {
		    imdbID: "tt1375666",
		    Title: "Inception",
		    Year: "2010",
		    Poster:
		      "https://m.media-amazon.com/images/M/MV5BMjAxMzY3NjcxNF5BMl5BanBnXkFtZTcwNTI5OTM0Mw@@._V1_SX300.jpg",
		    runtime: 148,
		    imdbRating: 8.8,
		    userRating: 10,
		  },
		  {
		    imdbID: "tt0088763",
		    Title: "Back to the Future",
		    Year: "1985",
		    Poster:
		      "https://m.media-amazon.com/images/M/MV5BZmU0M2Y1OGUtZjIxNi00ZjBkLTg1MjgtOWIyNThiZWIwYjRiXkEyXkFqcGdeQXVyMTQxNzMzNDI@._V1_SX300.jpg",
		    runtime: 116,
		    imdbRating: 8.5,
		    userRating: 9,
		  },
		];
		
		function Navbar({ children }) {
		  return (
		    <nav className="nav-bar">
		      <Logo />
		      {children}
		    </nav>
		  );
		}
		
		function Logo() {
		  return (
		    <div className="logo">
		      <span role="img">🍿</span> {/* No need to break */}
		      <h1>usePopcorn</h1>
		    </div>
		  );
		}
		
		function Search({ query, setQuery }) {
		  return (
		    <input
		      className="search"
		      type="text"
		      placeholder="Search movies..."
		      value={query}
		      onChange={(e) => setQuery(e.target.value)}
		    />
		  );
		}
		
		function NumResults({ movies }) {
		  return (
		    <p className="num-results">
		      Found <strong>{movies.length}</strong> results
		    </p>
		  );
		}
		
		function Main({ children }) {
		  return <main className="main">{children}</main>;
		}
		
		function Box({ element }) {
		  const [isOpen, setIsOpen] = useState(true);
		
		  return (
		    <div className="box">
		      <button className="btn-toggle" onClick={() => setIsOpen((open) => !open)}>
		        {isOpen ? "–" : "+"}
		      </button>
		      {isOpen && element}
		    </div>
		  );
		}
		
		function MovieList({ movies, onSelectMovie }) {
		  return (
		    <ul className="list list-movies">
		      {movies?.map((movie) => (
		        <Movie movie={movie} key={movie.imdbID} onSelectMovie={onSelectMovie} />
		      ))}
		    </ul>
		  );
		}
		
		function Movie({ movie, onSelectMovie }) {
		  return (
		    <li key={movie.imdbID} onClick={() => onSelectMovie(movie.imdbID)}>
		      <img src={movie.Poster} alt={`${movie.Title} poster`} />
		      <h3>{movie.Title}</h3>
		      <div>
		        <p>
		          <span>🗓</span>
		          <span>{movie.Year}</span>
		        </p>
		      </div>
		    </li>
		  );
		}
		
		// function WatchedBox() {
		//   const [watched, setWatched] = useState(tempWatchedData);
		//   const [isOpen2, setIsOpen2] = useState(true);
		
		//   return (
		//     <div className="box">
		//       <button
		//         className="btn-toggle"
		//         onClick={() => setIsOpen2((open) => !open)}
		//       >
		//         {isOpen2 ? "–" : "+"}
		//       </button>
		//       {isOpen2 && (
		//         <>
		//           <WatchedSummary watched={watched} />
		
		//           <WatchedMovieList watched={watched} />
		//         </>
		//       )}
		//     </div>
		//   );
		// }
		
		function MovieDetails({ selectedId, onCloseMovie, onAddWatched, watched }) {
		  const [movie, setMovie] = useState({});
		  const [isLoading, setIsLoading] = useState(false);
		  const [userRating, setUserRating] = useState("");
		
		  const isWatched = watched.map((movie) => movie.imdbID).includes(selectedId);
		  const watchedUserRating = watched.find(
		    (movie) => movie.imdbID === selectedId
		  )?.userRating;
		
		  const {
		    Title: title,
		    Year: year,
		    Poster: poster,
		    Runtime: runtime,
		    imdbRating,
		    Plot: plot,
		    Released: released,
		    Actors: actors,
		    Director: director,
		    Genre: genre,
		  } = movie;
		
		  console.log(title, year);
		  function handleAdd() {
		    const newWatchedMovie = {
		      imdbID: selectedId,
		      title,
		      year,
		      poster,
		      imdbRating: Number(imdbRating),
		      runtime: Number(runtime.split(" ").at(0)),
		    };
		
		    onAddWatched(newWatchedMovie);
		    onCloseMovie();
		  }
		
		  useEffect(
		    function () {
		      function callback(e) {
		        if (e.code === "Escape") {
		          onCloseMovie();
		        }
		      }
		
		      document.addEventListener("keydown", callback); // DOM manipulation. Stepping outside React. Hence, React team calls the `useEffect` hook an escape hatch (escaping from writing code the React way)
		      // Too many event listeners can cause memory problem
		
		      return function () {
		        document.removeEventListener("keydown", callback);
		      };
		    },
		    [onCloseMovie]
		  );
		
		  useEffect(
		    function () {
		      async function getMovieDetails() {
		        setIsLoading(true);
		        const res = await fetch(
		          `http://www.omdbapi.com/?apikey=${KEY}&i=${selectedId}`
		        ); // connects controller to `fetch`
		        const data = await res.json();
		        console.log(data);
		        setMovie(data);
		        setIsLoading(false);
		      }
		      getMovieDetails();
		    },
		    [selectedId]
		  );
		
		  useEffect(
		    function () {
		      if (!title) return;
		      document.title = `Movie | ${title}`;
		
		      return function () {
		        // clean-up function - runs after each re-render, and when component unmounts
		        document.title = "usePopcorn";
		        console.log(`Clean up effect for movie ${title}`); // `title` - remembered by the function because of closure concept
		        // closure - a function will always remember the variables that were present at the time and place the function was created
		        // The function closed over the `title` variable, and will remember it in the future
		      };
		    },
		    [title]
		  );
		
		  return (
		    <div className="details">
		      {isLoading ? (
		        <Loader />
		      ) : (
		        <>
		          <header>
		            <button className="btn-back" onClick={onCloseMovie}>
		              &larr;
		            </button>
		            <img src={poster} alt={`Poster of ${movie} movie`} />
		            <div className="details-overview">
		              <h2>{genre}</h2>
		              <p>
		                {released} &bull; {runtime}
		              </p>
		              <p>
		                <span></span>
		                {imdbRating} IMDb rating
		              </p>
		            </div>
		          </header>
		
		          <section>
		            <div className="rating">
		              {!isWatched ? (
		                <>
		                  <StarRating
		                    maxRating={10}
		                    size={24}
		                    onSetRating={setUserRating}
		                  />
		                  {userRating > 0 && (
		                    <button className="btn-add" onClick={handleAdd}>
		                      + Add to list
		                    </button>
		                  )}
		                </>
		              ) : (
		                <p>
		                  You rated the movie {watchedUserRating} <span>⭐</span>
		                </p>
		              )}
		            </div>
		            <p>
		              <em>{plot}</em>
		            </p>
		            <p>Staring {actors}</p>
		            <p>directed by {director}</p>
		          </section>
		        </>
		      )}
		    </div>
		  );
		}
		
		function WatchedSummary({ watched }) {
		  const avgImdbRating = average(watched.map((movie) => movie.imdbRating));
		  const avgUserRating = average(watched.map((movie) => movie.userRating));
		  const avgRuntime = average(watched.map((movie) => movie.runtime));
		
		  return (
		    <div className="summary">
		      <h2>Movies you watched</h2>
		      <div>
		        <p>
		          <span>#️⃣</span>
		          <span>{watched.length} movies</span>
		        </p>
		        <p>
		          <span>⭐️</span>
		          <span>{avgImdbRating.toFixed(2)}</span>
		        </p>
		        <p>
		          <span>🌟</span>
		          <span>{avgUserRating.toFixed(2)}</span>
		        </p>
		        <p>
		          <span>⏳</span>
		          <span>{avgRuntime} min</span>
		        </p>
		      </div>
		    </div>
		  );
		}
		
		function WatchedMovieList({ watched, onDeleteWatched }) {
		  return (
		    <ul className="list">
		      {watched.map((movie) => (
		        <WatchedMovie
		          movie={movie}
		          key={movie.imdbID}
		          onDeleteWatched={onDeleteWatched}
		        />
		      ))}
		    </ul>
		  );
		}
		
		function WatchedMovie({ movie, onDeleteWatched }) {
		  return (
		    <li key={movie.imdbID}>
		      <img src={movie.poster} alt={`${movie.title} poster`} />
		      <h3>{movie.Title}</h3>
		      <div>
		        <p>
		          <span>⭐️</span>
		          <span>{movie.imdbRating}</span>
		        </p>
		        <p>
		          <span>🌟</span>
		          <span>{movie.userRating}</span>
		        </p>
		        <p>
		          <span>⏳</span>
		          <span>{movie.runtime} min</span>
		        </p>
		
		        <button
		          className="btn-delete"
		          onClick={() => onDeleteWatched(movie.imdbID)}
		        >
		          X
		        </button>
		      </div>
		    </li>
		  );
		}
		
		const KEY = "4256c7"; // If it is inside the component, it will get re-created each time the component is re-rendered
		
		const average = (arr) =>
		  arr.reduce((acc, cur, i, arr) => acc + cur / arr.length, 0);
		
		export default function App() {
		  const [query, setQuery] = useState("");
		  const [movies, setMovies] = useState(tempMovieData);
		  const [watched, setWatched] = useState(tempWatchedData);
		  const [isLoading, setIsLoading] = useState(false);
		  const [error, setError] = useState("");
		  const [selectedId, setSelectedId] = useState(null);
		
		  // useEffect(function () {
		  //   console.log("After initial render"); // Appears second - because it appears before the other effects.
		  // }, []);
		
		  // useEffect(function () {
		  //   console.log("After every render");
		  // }); // Appears last
		  // // If `query` is updated, this effect is executed because it runs after every render.
		
		  // useEffect(
		  //   function () {
		  //     console.log("Synchronized with `query` state variable");
		  //   },
		  //   [query]
		  // );
		
		  function handleSelectMovie(id) {
		    setSelectedId((selectedId) => (selectedId === id ? null : id));
		  }
		
		  function handleCloseMovie() {
		    setSelectedId(null);
		  }
		
		  function handleAddWatched(movie) {
		    setWatched((watched) => [...watched, movie]);
		  }
		
		  function handleDeleteWatched(id) {
		    setWatched((watched) => watched.filter((movie) => movie.imdbID !== id));
		  }
		
		  console.log("During render"); // Appears first - effects run after browser paint. This statement is executed during render
		  // If `query` is updated, this line executes during render
		
		  useEffect(
		    // Can be converted to an event-listener in this case
		    function () {
		      // function contains code that we want to run as a side-effect
		      // It is registered to be run at a certain point in time
		
		      const controller = new AbortController(); // Browser API
		
		      async function fetchMovies() {
		        try {
		          setIsLoading(true);
		          setError("");
		          const res = await fetch(
		            `http://www.omdbapi.com/?apikey=${KEY}&s=${query}`,
		            { signal: controller.signal }
		          );
		
		          if (!res.ok)
		            throw new Error("Something went wrong with fetching movies");
		
		          const data = await res.json();
		
		          if (data.Response === "False") throw new Error("Movie not found");
		
		          setMovies(data.Search);
		          console.log(data); // empty array, because setting state is asynchronous
		        } catch (err) {
		          console.log(err.message);
		          if (err.name !== "AbortError") setError(err.message);
		        } finally {
		          setIsLoading(false);
		        }
		      }
		
		      if (query.length < 3) {
		        setMovies([]);
		        setError("");
		        return;
		      }
		
		      handleCloseMovie();
		      fetchMovies();
		
		      return function () {
		        controller.abort();
		      };
		    },
		    [query]
		  ); // It doesn't return anything
		  // Second argument is dependency array
		  // `[]` - means that the hook will run only on mount (inital render)
		  // Good if we want to fetch data as soon as the application loads
		
		  // setWatched([]); // Causes too many re-renders
		
		  return (
		    <>
		      <Navbar>
		        <Search query={query} setQuery={setQuery} />
		        <NumResults movies={movies} />
		      </Navbar>
		      <Main>
		        <Box
		          element={
		            (isLoading && <Loader />) ||
		            (!isLoading && !error && (
		              <MovieList movies={movies} onSelectMovie={handleSelectMovie} />
		            )) ||
		            (error && <ErrorMessage message={error} />)
		          }
		        />
		        <Box
		          element={
		            selectedId ? (
		              <MovieDetails
		                selectedId={selectedId}
		                onCloseMovie={handleCloseMovie}
		                onAddWatched={handleAddWatched}
		                watched={watched}
		              />
		            ) : (
		              <>
		                <WatchedSummary watched={watched} />
		                <WatchedMovieList
		                  watched={watched}
		                  onDeleteWatched={handleDeleteWatched}
		                />
		              </>
		            )
		          }
		        />
		        {/* <Box>
		          <MovieList movies={movies} />
		        </Box>
		        <Box>
		          <WatchedSummary watched={watched} />
		          <WatchedMovieList watched={watched} />
		        </Box> */}
		      </Main>
		    </>
		  );
		}
		
		function Loader() {
		  return <p className="loader">Loading...</p>;
		}
		
		function ErrorMessage({ message }) {
		  return (
		    <p className="error">
		      <span>⛔ {message}</span>
		    </p>
		  );
		}

### CHALLENGE #1: Currency Converter ###
1. Currency conversion using an API that contains real-time currency conversion data
2. 

## Section 13: Custom Hooks, Refs, and More State ##
### Section Overview ###
1. Topics:
	1. Hooks are easy to **learn**, hard to **master**
		1. A solid understanding of hooks is crucial to all React developers
	2. **Rules** of hooks
		1. And why they exist
	3. **Deep** dive into `useState`
	4. `useRef`
	5. **Custom** hooks
		1. Own hooks

### React Hooks and Their Rules ###
#### What are React Hooks? ####
1. React Hooks
	1. Special built-in functions that allow us to **hook into React internals**
		1. They are APIs that expose internal React functionalities such as
			1. Contructing and accessing **state** from Fiber tree
			2. Registering **side effects** in Fiber tree
				1. Fiber tree is deep inside React and is usually not accessible
					1. Using `useState` or `useEffect` hook, we can hook into the internal mechanism 
			3. Manual **DOM selections**
			4. Access context
			5. ...
	2. Always start with "use" (`useState`, `useEffect`, etc.)
		1. To distinguish from other functions
	3. Enable easy **reusing of non-visual logic**: we can compose multiple hooks into our own **custom hooks**
		1. reusing of non-visual logic: logic that is not UI
			1. Class-based components had some problems, hence we have function components with hooks
	4. Give **function components** the ability to own state and run side effects at different lifecycle points (before v16.8 only avaialable in class **components**)

#### Overview of All Built-In Hooks ####
1. Most used:
	1. `useState`
	2. `useEffect`
	3. `useReducer`
	4. `useContext`
2. Less used:
	1. `useRef`
	2. `useCallback`
	3. `useMemo`
	4. `useTransition`
	5. `useDeferredValue`
	6. `useLayoutEffect`
	7. `useDebugValue`
	8. `useImperativeHandle`
	9. `useId`
3. Only for libraries (for library authors)
	1. `useSyncExternalStore`
	2. `useInsertionEffect`

#### The Rules of Hooks ####
1. Rules:
	1. Only call hooks at the top level
		1. Do **NOT** call hooks inside **conditionals, loops, nested functions,** or after an **early return** (similar to a condition)
			1. Why?
				1. This is necessary to ensure that hooks are always called in the **same order** (hooks rely on this)
	2. Only call hooks from React functions
		1. Only call hooks inside a **function components** or a **custom hook**
			1. Not from regular functions
			2. Not from class components
2. The rules are automatically enforced by React's ESLint rules

#### Hooks Rely on Call Order ####
1. Whenever an application is rendered, React constructs a tree of React elements (vDOM)
	1. On initial render, React constructs a fiber tree out of vDOM, where each element is a fiber
		1. Each fiber contains
			1. Received props
			2. List of work
			3. **Linked list of all the hooks that were used in the component instance**
				1. Example: Hypothetical example:

						const [A, setA] = useState(23)

						if (A === 23)
							const [B, setB] = useState('');

						useEffect(fnZ, []);

					1. List built based on hooks call order
						1. `useState(23)` (has reference to second hook)
						2. `useState('')` (has reference to third hook)
						3. `useEffect(...)`
					2. Suppose the component is re-rendered because the state changed from 23 to 7
						1. Problem:
							1. The condition is false
								1. `useState('')` does not exist after the render
								2. The first hook is still pointing to the `useState('')` hook that no longer exists
								3. Nothing is pointing to the third hook (`useEffect(...)`)
							2. A === 23 is now false, so after re-render, this hook would no longer exist, **destroying the linked list**
								1. It works this way because fibers are not re-created on every render
									1. Hence, the list is also not re-created
										1. If a hook disappears from the list, then the list gets completely broken
										2. Condition will completely mess up the list of hooks (React will be confused will not be able to track the list of hooks)
										3. Hence, hooks will be called in the same order after every render (hence the first rule)
2. Why have linked-list in the first place?
	1. Linked list relies on a hook called order is the simplest way to associate a hook with its value
		1. The order in which the hook is called uniquely identifies the hook
			1. Hook 1 has a state of 23, and hook 2 has a state of '', ...
				1. Values are associated with call order
					1. Developers don't have to manually assign names to each hook (there are multiple problems)

### The Rules of Hooks in Practice ###
1. In Dev Tools:
	1. `MovieDetails`
		1. hooks
			1. Hooks are numbered (React identifies by order number (not by name))
2. Code:

		/* eslint-disable */
		if (imdbRating > 8) [isTop, setIsTop] = useState(true);

	1. If the condition is met, React stops working and throws an error
	2. Console:

			Warning: React has detected a change in the order of Hooks called by MovieDetails. This will lead to bugs and errors if not fixed. For more information, read the Rules of Hooks: https://reactjs.org/link/rules-of-hooks
			
			   Previous render            Next render
			   ------------------------------------------------------
			1. useState                   useState
			2. useState                   useState
			3. useState                   useState
			4. useEffect                  useState
			   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

	3. Another example:

			  if (imdbRating > 8) return <p>Greatest ever!</p>; // Same problem occurs. Fewer hooks were rendered (rest of the hooks did not get rendered due to early return)

	4. The initial values we pass to `useState` only matter on the initial render
		1. Example:

				const [isTop, setIsTop] = useState(imdbRating > 8);
				console.log(isTop); // always `false`

			1. What we passed is only initial state, and React will look at the initial state only on the initial render. (when the component first mounts)
				1. `imdbRating` is `undefined` on initial render
				2. The initialization is not executed on re-render
			2. How to overcome this issue?
				1. `useEffect`

						useEffect(function () {
							setIsTop(imdbRating > 8);
						}, [imdbRating]) 

					1. Alternative:

							const isTop = imdbRating > 8; // derived state. It gets updated, each time the component re-renders
							console.log(isTop);

3. State updates are asynchronous

		setAvgRating(Number(imdbRating));
		// alert(avgRating); // We do not get access to the updated state soon after we update the state. We will get access to the updated state after React processes the event-handler. React will then re-render the UI
		
		setAvgRating((avgRating + userRating) / 2); // `avgRating` is still 0. It is asynchronous state setting

### More Details of useState ###
1. Persisting watchlist in local storage
	1. Local storage:
		1. A simple key/value storage available in the browser, where we can store some data for each domain (per URL)
		2. Where to check:
			1. Dev tools
				1. Application tab
					1. Local Storage

### Initializing State With a Callback (Lazy Initial State) ###
1. Code:

		const [watched, setWatched] = useState(function () {
		  const storedValue = localStorage.getItem("watched");
		  return JSON.parse(storedValue);
		}); // React will call the function when the component mounts and uses the value returned by the function as the initial value of the state. The function must be a pure function, and it must not accept arguments. The function is only executed once on initial render, and is ignored on subsequent renders.
		
		...
		
		function handleAddWatched(movie) {
		  setWatched((watched) => [...watched, movie]);
		
		  // localStorage.setItem("watched", JSON.stringify([...watched, movie]));
		}
		
		function handleDeleteWatched(id) {
		  setWatched((watched) => watched.filter((movie) => movie.imdbID !== id));
		}
		
		useEffect(
		  function () {
		    localStorage.setItem("watched", JSON.stringify(watched));
		  },
		  [watched]
		); // When we add or delete a movie in the watched list, the local storage is synchronized.

### useState Summary ###
#### Summary of Defining and Updating State ####
1. Constructing State
	1. Simple way

			const [count, setCount] = useState(23);

	2. Based on a callback function (lazy evaluation)

			const [count, setCount] = useState(
				() => localStorage.getItem('count');
			);

		1. Whenever the initial state requires some computation, for instance to retrieve data from local storage, we can pass in a callback function instead of a single value
			1. Lazy evaluation
			2. The function must be pure and accept no arguments. Called only on initial render
				1. For sebsequent renders, the function will be ignored.

2. Updating State
	1. Simple way
		1. By passing a single value into the setter function as the next state

				setCount(1000);

	2. Based on current state

			setCount((c) => c + 1);	

		1. Function must be pure and return next state (based on the current state)
			1. Preferred way whenever it makes sense
	3. Make sure to **NOT** mutate objects or arrays, but to **replace** them	
		1. A new array or object must be created which incorporates the changes we want to make
			1. Pass the new object into the setter function

### How NOT to Select DOM Elements in React ###
1. Why do we need refs in React
2. Code example:

		function Search({ query, setQuery }) {
		  useEffect(function () {
		    const el = document.querySelector(".search");
		    console.log(el);
		    el.focus();
		  }, []);
		...

	1. React is about declarative.
		1. Manually selecting a DOM element is not React way of doing things
			1. Not inline with the rest of the React code
				1. We must not manually add classes, event-listeners, etc... directly to DOM elements, and not add classes to JSX elements just for selecting them.
				2. If we have a dependency, we will select the element over and over again
	2. Solution: refs

### Introducing Another Hook: useRef ###
1. `useRef` - easiest hook of all

#### What are Refs? ####
1. Ref with `useRef`
	1. "Box" (object) with a **mutable** `.current` property that is **persisted across renders** ("normal" variables are always reset)
		1. We can write to and read from the ref using `.current`

				const myRef = useRef(23);

				myRef.current = 1000; // mutable

		2. Two big use cases:
			1. Creation of variable that stays the same between renders (e.g. previous state, `setTimeout` id, etc)
			2. Selecting and storing DOM elements
				1. We want to store DOM elements and preserve across renders
2. Refs are for **data that is NOT rendered:** usually only appear in event handlers or effects, not in JSX (otherwise use state)
	1. For visual appearance, use state instead
	2. Do **NOT** read write or read `.current` in render logic (like state)
		1. Can cause undesirable side-effects
		2. The mutations are usually done in a `useEffect` hook

#### State vs. Refs ####
1. Refs are like state but with less powers
	1. Both refs and state are persisted across renders
		1. Component remembers values even after re-renders
		2. Updating state causes re-render of component
			1. State is used only if we want a component to re-render on update
		3. Updating refs does not cause re-render of component
			1. Refs are used only if we want the component to remember data over time (never re-render)
				1. Examples: preserving previous state, or storing the id of `setTimeout`
	2. State is immutable but refs are not
	3. State is updated asynchronously but refs are not updated asynchronously

### Refs to Select DOM Elements ###
1. Three steps:
	1. Step 1: 

			const inputEl = useRef(null);

	2. Step 2:

			<input
				...
				ref={inputEl}
			/>

		1. Connects the element to the ref
			1. `inputEl` contains the `input` element

	3. Step 3:
	
			useEffect(function () {
				inputEl.current.focus(); // `inputEl.current` contains the DOM element
			}, []);

		1. Ref gets added to the DOM element after the DOM has already loaded. It can be accessed only in `useEffect` which runs after the DOM is loaded.
2. Code:

		  useEffect(
		    function () {
		      function callback(e) {
		        if (document.activeElement === inputEl.current) return;
		
		        if (e.code === "Enter") {
		          inputEl.current.focus();
		          setQuery("");
		        }
		      }
		
		      document.addEventListener("keydown", callback);
		      return () => document.addEventListener("keydown", callback);
		    },
		    [setQuery]
		  );

### Refs to Persist Data Between Renders ###
1. A variable that is persisted across renders without triggering a re-render
2. Code:

		function MovieDetails({ selectedId, onCloseMovie, onAddWatched, watched }) {
		// ...
		
		  const countRef = useRef(0);
		
		  useEffect(
		    function () {
		      if (userRating) countRef.current++;
		    },
		    [userRating]
		  ); // Because we cannot mutate state in render logic
		
		// ...
		
		  function handleAdd() {
		    const newWatchedMovie = {
		      // ...
		      countRatingDecisions: countRef.current,
		    };

### What are Custom Hooks? When to Construct One? ###
#### Reusing Logic with Custom Hooks ####
1. It is about re-usability
	1.  We can re-use two kinds of things in React
		1.  Piece of UI
			1.  Using a component
		2.  Piece of logic
			1.  Questions to ask:
				1.  Does logic contain any **hooks**?
					1.  No
						1.  Regular function
							1.  Inside or outside a component
					2.  Yes
						1.  We cannot extract logic that contains a hook into a regular function
							1.  Solution: Custom hook
								1.  Allows us to reuse **non-visual logic** in multiple components (stateful logic among multiple components, or any logic )
								2.  One custom hook shoud have **one purpose**, to make it **reusable**, and **portable** (even across multiple projects)
									1. Developers have also started to share their custom hooks
										1. We can download from `npm` and use it
								3. The rules of hooks applies to custom hooks as well.
2. Example of a custom hook:

		function useFetch (url) {
			const [data, setData] = useState([]);
			const [isLoading, setIsLoading] = useState(false);

			useEffect(function () {
				fetch(url)
					.then((res) => res.json())
					.then((res) => setData(res));
			}, []);

			return [data, isLoading]
		}

	1. Unline components, it can receive and return **any relevant data** (usually array [] or object {})
		1. Components can only receive props and must return JSX
		2. A custom hook uses one or more react hooks
			1. `useState`, `useEffect`
	2. Function name must start with `use`

### Constructing our First Custom Hook: useMovies ###
1. Convention:
	1. Use default exports for components
	2. Use named exports for custom hooks
2. `useMovies.js`

		import { useEffect, useState } from "react";

		const KEY = "4256c7"; // If it is inside the component, it will get re-created each time the component is re-rendered
		
		export function useMovies(query, callback) {
		  const [movies, setMovies] = useState([]);
		  const [isLoading, setIsLoading] = useState(false);
		  const [error, setError] = useState("");
		
		  useEffect(
		    // Can be converted to an event-listener in this case
		    function () {
		      callback?.(); // optional chaining
		      // function contains code that we want to run as a side-effect
		      // It is registered to be run at a certain point in time
		
		      const controller = new AbortController(); // Browser API
		
		      async function fetchMovies() {
		        try {
		          setIsLoading(true);
		          setError("");
		          const res = await fetch(
		            `http://www.omdbapi.com/?apikey=${KEY}&s=${query}`,
		            { signal: controller.signal }
		          );
		
		          if (!res.ok)
		            throw new Error("Something went wrong with fetching movies");
		
		          const data = await res.json();
		
		          if (data.Response === "False") throw new Error("Movie not found");
		
		          setMovies(data.Search);
		          console.log(data); // empty array, because setting state is asynchronous
		        } catch (err) {
		          console.log(err.message);
		          if (err.name !== "AbortError") setError(err.message);
		        } finally {
		          setIsLoading(false);
		        }
		      }
		
		      if (query.length < 3) {
		        setMovies([]);
		        setError("");
		        return;
		      }
		
		      // handleCloseMovie();
		      fetchMovies();
		
		      return function () {
		        controller.abort();
		      };
		    },
		    [query]
		  ); // It doesn't return anything
		  // Second argument is dependency array
		  // `[]` - means that the hook will run only on mount (inital render)
		  // Good if we want to fetch data as soon as the application loads
		
		  return { movies, error, isLoading };
		}

2. `App.js`

		  const { movies, error, isLoading } = useMovies(query, handleCloseMovie);

### Constructing useLocalStorageState ###
1. Code:

		import { useState, useEffect } from "react";

		export function useLocalStorageState(initialState, key) {
		  const [value, setValue] = useState(function () {
		    const storedValue = localStorage.getItem(key);
		    return storedValue ? JSON.parse(storedValue) : initialState;
		  });
		
		  useEffect(
		    function () {
		      localStorage.setItem(key, JSON.stringify(value));
		    },
		    [value, key]
		  ); // When we add or delete a movie in the watched list, the local storage is synchronized.
		
		  return [value, setValue];
		}

	1. Custom hook setter function updates both state and local storage

### Construct useKey ###
1. Code:

		import { useEffect } from "react";

		export function useKey(key, action) {
		  useEffect(
		    function () {
		      function callback(e) {
		        if (e.code.toLowerCase() === key.toLowerCase()) {
		          action();
		        }
		      }
		
		      document.addEventListener("keydown", callback); // DOM manipulation. Stepping outside React. Hence, React team calls the `useEffect` hook an escape hatch (escaping from writing code the React way)
		      // Too many event listeners can cause memory problem
		
		      return function () {
		        document.removeEventListener("keydown", callback);
		      };
		    },
		    [key, action]
		  );
		}

	1. App.js

			useKey("Escape", onCloseMovie);

			// ...

			useKey("Enter", function () {
			  if (document.activeElement === inputEl.current) return;
			
			  inputEl.current.focus();
			  setQuery("");
			});

### CHALLENGE #1: useGeolocate ###
1. MUST DO!

## Section 14: [Optional] React Before Hooks: Class-Based React ##
### Section Overview ###
### Our First Class Component ###
### Working With Event Handlers ###
### Class Components vs. Function Components ###
### Starting the "Classy Weather" App ###
### Fetching Weather Data ###
### Displaying the Weather ###
### Removing Boilerplate Code With Class Fields ###
### Child to Parent Communication ###
### Lifecycle Methods ###

## Section: 15: PART 3: ADVANCED REACT + REDUX [4 PROJECTS] ##
### Introduction to Part 3 ###
1. Advanced state management with
	1. `useReducer` hook
	2. Context API
	3. Redux
2. Projects
	1. Using veet
	2. Using React router library
3. Deep into React cosmos for performance optimization
	1. `useMemo` hook
	2. `useCallback` hook

### Useful Resources for Part 3 ###
1. High-quality resources
	1. [Tao of React - Software Design, Architecture & Best Practices](https://alexkondov.com/tao-of-react/?ref=jonas.io)
	2. [The new wave of React state management](https://frontendmastery.com/posts/the-new-wave-of-react-state-management/?ref=jonas.io) - Excellent read!
	3. [A Visual Guide to React Rendering - useMemo](https://alexsidorenko.com/blog/react-render-usememo?ref=jonas.io)
	4. [React as a UI Runtime](https://overreacted.io/react-as-a-ui-runtime/?ref=jonas.io) - By Dan Abramov from the React team
	5. [You Might Not Need an Effect](https://react.dev/learn/you-might-not-need-an-effect?ref=jonas.io) (Official React docs)
	6. [A Complete Guide to useEffect](https://overreacted.io/a-complete-guide-to-useeffect/?ref=jonas.io) (By Dan Abramov)
	7. [useEffect sometimes fires before paint](https://blog.thoughtspile.tech/2021/11/15/unintentional-layout-effect/?ref=jonas.io)
	8. [Making setInterval Declarative with React Hooks](https://overreacted.io/making-setinterval-declarative-with-react-hooks/?ref=jonas.io) (By Dan Abramov)
	9. [Redux - Not Dead Yet!](https://blog.isquaredsoftware.com/2018/03/redux-not-dead-yet/?ref=jonas.io) (By Mark Erikson from the Redux team)
	10. [Why React Context is Not a "State Management" Tool](https://blog.isquaredsoftware.com/2021/01/context-redux-differences/) (By Mark Erikson)
2. Library documentation:
	1. [Vite](https://vitejs.dev/guide/why.html) (Why Vite is so fast)
	2. [CSS Modules](https://github.com/css-modules/css-modules)
	3. [React Router](https://reactrouter.com/en/main?ref=jonas.io)
	4. [React Leaflet: Installation](https://react-leaflet.js.org/docs/start-installation/?ref=jonas.io)
	5. [Redux: Style Guide](https://redux.js.org/style-guide/?ref=jonas.io) (A must-read for Redux users!)
	6. [Redux Toolkit](https://redux-toolkit.js.org/tutorials/overview?ref=jonas.io)
	7. [React Redux](https://react-redux.js.org/api/hooks?ref=jonas.io)

## Section 16: The Advanced useReducer Hook ##
### Section Overview ###
1. Topics:
	1. Another **powerful** way of managing state
	2. Mastering `useReducer` is important to understand **Redux**
	3. Half the section in essentially another **practice project**
		1. `useReducer` re-inforces all that we learn't so far

### Yet Another Hook: useReducer ###
1. High-level overview
	1. Another project:
		1. `npx create-react-app@5 react-quiz`
2. `useReducer` hook:
	1. It is a more complex and more advanced way of managing state than the `useState` hook
	2. It works with a reducer function
		1. Reducer function: It is a pure function that takes previous state, and an action as argument, and returns the next state
3. Code:

		function reducer(state, action) {
		  console.log(state, action);
		  // return state + action;
		  if (action.type === "inc") return state + 1;
		  if (action.type === "dec") return state - 1;
		  if (action.type === "setCount") return action.payload;
		  // What the reducer returns will become the next state
		}

		...
		function DateCounter() {
		  // const [count, setCount] = useState(0);
		
		  const [count, dispatch] = useReducer(reducer, 0); // returns the current state, and dispatch function (which is used to update the state)

		  // ...

		  const dec = function () {
		    // dispatch(-1);
		    dispatch({ type: "dec" }); // standard convention to have `type`, and `payload` properties. Similar in Redux
		    // setCount((count) => count - 1);
		    // setCount((count) => count - step);
		  };
		
		  const inc = function () {
		    // dispatch(1); // 1 - action in the reducer. This is called dispatching an action
		    dispatch({ type: "inc" });
		    // setCount((count) => count + 1);
		    // setCount((count) => count + step);
		  };
		
		  const defineCount = function (e) {
		    // setCount(Number(e.target.value));
		  };
		
		  const defineStep = function (e) {
		    // setStep(Number(e.target.value));
		    dispatch({ type: "setCount", payload: Number(e.target.value) });
		  };

### Managing Related Pieces of State ###
1. We use reducer if we have complex state to manage (not just one single value)
	1. State is usually an object (not just a single value)
2. Advantage of reducer function:
	1. We can have all the possible state updates that can happen in the application in one central place
		1. It makes it easy to understand the application without going into every component, and every function.
3. Code:

		import { useReducer } from "react";

		const initialState = { count: 0, step: 1 };
		
		// The real logic of updating the state is centralized in one location in the reducer
		function reducer(state, action) {
		  console.log(state, action);
		
		  switch (action.type) {
		    case "dec":
		      return { ...state, count: state.count - state.step };
		    case "inc":
		      return { ...state, count: state.count + state.step };
		    case "setCount":
		      return { ...state, count: action.payload };
		    case "setStep":
		      return { ...state, step: action.payload };
		    case "reset":
		      return initialState; // We can update multiple pieces of state at the same time
		    default:
		      throw new Error("Unknown action");
		  }
		}
		
		function DateCounter() {
		  const initialState = { count: 0, step: 1 };
		  const [state, dispatch] = useReducer(reducer, initialState); // returns the current state, and dispatch function (which is used to update the state)
		  const { count, step } = state;
		
		  // This mutates the date object.
		  const date = new Date("june 21 2027");
		  date.setDate(date.getDate() + count);
		
		  const dec = function () {
		    dispatch({ type: "dec" }); // standard convention to have `type`, and `payload` properties. Similar in Redux
		  };
		
		  const inc = function () {
		    dispatch({ type: "inc" });
		  };
		
		  const defineCount = function (e) {
		    dispatch({ type: "setCount", payload: Number(e.target.value) });
		  };
		
		  const defineStep = function (e) {
		    dispatch({ type: "setStep", payload: Number(e.target.value) });
		  };
		
		  const reset = function () {
		    dispatch({ type: "reset" });
		  };
		
		  return (
		    <div className="counter">
		      <div>
		        <input
		          type="range"
		          min="0"
		          max="10"
		          value={step}
		          onChange={defineStep}
		        />
		        <span>{step}</span>
		      </div>
		
		      <div>
		        <button onClick={dec}>-</button>
		        <input value={count} onChange={defineCount} />
		        <button onClick={inc}>+</button>
		      </div>
		
		      <p>{date.toDateString()}</p>
		
		      <div>
		        <button onClick={reset}>Reset</button>
		      </div>
		    </div>
		  );
		}
		export default DateCounter;

### Managing State With useReducer ###
#### Why useReducer? ####
1. State management with `useState` is not enough in certain situations:
	1. As components, and state become more complex, using `useState` is not enough
		1. Example: When components have a **lot of state variables and state updates,** spread across many event handlers **all over the component** (maybe even multiple components)
			1. Can be overwhelming and hard to manage
	2. When **multiple state updates** need to happen **at the same time** (as a reaction to the same event, like "starting a game" (set score to 0, set isPlaying status, start a timer at the same time)
	3. When updating one piece of state that **depends on one or multiple other peices of state**
		1. Becomes challenging when there is a lot of state
2. Solution: In all the above situations, `useReducer` can be of great help

#### Managing State with useReducer ####
1. State with useReducer
	1. An alternative way of setting state, ideal for **complex state** and **related pieces of state**
		1. Example:

				const [state, dispatch] = useReducer(reducer, initialState);
	
	2. Stores related pieces of state in a **state** object (that is returned from the `useReducer` hook
	3. `useReducer` needs a **reducer**: function containing **all logic to update state. Decouples state logic from component** (makes components cleaner and readable) (It is like `setState()` with superpowers)
	4. **reducer:** pure function (**no side effects!**) that takes current `state` and `action`, **and returns the next state**
		1. Reducer is not allowed to mutate the state
	5. **action:** object that describes **how to update state**
		1. It contains an action type, and a payload (input data)
			1. Used by reducer to determine how to define the next state
	6. **dispatch:** function to trigger state updates, by **"sending" actions** from **event handlers** to the **reducer**

#### How Reducers Update State ####
1. Let us say we are in an event-handler of a component

		Updating state in a component
			|
			v
		dispatch -action(type = 'updateDay', payload = 23)-> reducer
																|
															Returns
																|
																v
														Next state
															|
															triggers
															|
															v
														Re-render

	1. Action: Object taht contains information on how the reducer should update the state
		1. Reducer will set the day's value to 23
			1. The shape of action doesn't have to be the one mentioned
	2. Why is it called a reducer?
		1. Just like `array.reduce()` accumulates all array values into a single value, React reducer accumulates ("reduce") **actions over time** into a single state
	3. In the background, the `dispatch` function has access to the reducer, because we passed it to the `useReducer` hook
		1. Dispatcher coordinates the whole thing and gives access to the reducer, the current state
2. `useReducer` vs `useState`
	1. `useState` - we get back a setter function
		1. To update state, we pass updated state value. React will update the state
			1. This triggers a re-render

					setState
						|
						update
						|
						v
					Next (updated) state
						|
						v
					Re-render

3. Analogy
	1. Real-world task: Withdrawing $5000 form your bank account
		1. I go to a bank and approach a teller
		2. We tell the person, the amount, and from which account
		3. Teller will check the account
		4. Teller goes to bank's vault and gets money
		5. Teller hands it over to me
	2. `useReducer`:
		1. State: vault (**what** needs to be updated)
			1. Where money is stored and updated
		2. Reducer: Teller
			1. **Who makes** the update
			2. Teller knows much more.
				1. How to request loan
				2. How to deposit money
				3. ...
		3. Dispatcher: Customer
			1. **Who requests** the update
				1. Doing so by going to a person and withdrawing the money
		4. Action: The amount, and account info
			1. **How** to make the update

					{
						type: 'withdraw',
						payload: {
							amount: 5000,
							account: 453423,
						},
					}

				1. Reducer decouples and abstracts state update logic from the client
					1. Easy to understand components		

### The "React Quiz" App ###
### Loading Questions from a Fake API ###
1. Code:

		import { useEffect, useReducer } from "react";
		import Header from "./Header";
		import Main from "./Main";
		
		const initialState = {
		  questions: [],
		
		  // 'loading', 'error', 'ready', 'active', 'finished'
		  status: "loading",
		};
		
		function reducer(state, action) {
		  switch (action.type) {
		    case "dataReceived":
		      return {
		        ...state,
		        questions: action.payload,
		        status: "ready",
		      };
		    case "dataFailed":
		      return {
		        ...state,
		        status: "error",
		      };
		    default:
		      throw new Error("Action is unknown");
		  }
		}
		
		export default function App() {
		  const [state, dispatch] = useReducer(reducer, initialState);
		
		  useEffect(function () {
		    fetch("http://localhost:8000/questions")
		      .then((res) => res.json())
		      .then((data) => dispatch({ type: "dataReceived", payload: data }))
		      .catch((err) => dispatch({ type: "dataFailed" }));
		  }, []);
		
		  // `dataReceived` can be considered as an event
		
		  return (
		    <div className="app">
		      <Header />
		      <Main>
		        <p>1/15</p>
		        <p>Question?</p>
		      </Main>
		    </div>
		  );
		}

### Handling Loading, Error, and Ready Status ###
1. StartScreen.js

		function StartScreen({ numQuestions }) {
		  return (
		    <div className="start">
		      <h2>Welcome to the React Quiz!</h2>
		      <h3>{numQuestions} questions to test your React mastery</h3>
		      <button className="btn btn-ui">Let's start</button>
		    </div>
		  );
		}
		
		export default StartScreen;

2. App.js

		export default function App() {
		  const [{ questions, status }, dispatch] = useReducer(reducer, initialState);
		
		  const numQuestions = questions.length;
		
		// ...
		
		  return (
		    <div className="app">
		      <Header />
		      <Main>
		        {status === "loading" && <Loader />}
		        {status === "error" && <Error />}
		        {status === "ready" && <StartScreen numQuestions={numQuestions} />}
		      </Main>
		    </div>
		  );
		}

### Starting a New Quiz ###
1. We need to pass `dispatch` functions around (similar to passing an event handler)
	1. We are using a state reducer, so we can just pass `dispatch` function
2. StartScreen.js:

		function StartScreen({ numQuestions, dispatch }) {
		  return (
		    <div className="start">
		      <h2>Welcome to the React Quiz!</h2>
		      <h3>{numQuestions} questions to test your React mastery</h3>
		      <button
		        className="btn btn-ui"
		        onClick={() => dispatch({ type: "start" })}
		      >
		        Let's start
		      </button>
		    </div>
		  );
		}
		
		export default StartScreen;

3. App.js

		import { useEffect, useReducer } from "react";
		import Header from "./Header";
		import Main from "./Main";
		import Loader from "./Loader";
		import Error from "./Error";
		import StartScreen from "./StartScreen";
		import Question from "./Question";
		
		const initialState = {
		  questions: [],
		
		  // 'loading', 'error', 'ready', 'active', 'finished'
		  status: "loading",
		};
		
		function reducer(state, action) {
		  switch (action.type) {
		    case "dataReceived":
		      return {
		        ...state,
		        questions: action.payload,
		        status: "ready",
		      };
		    case "dataFailed":
		      return {
		        ...state,
		        status: "error",
		      };
		    case "start":
		      return {
		        ...state,
		        status: "active",
		      };
		    default:
		      throw new Error("Action is unknown");
		  }
		}
		
		export default function App() {
		  const [{ questions, status }, dispatch] = useReducer(reducer, initialState);
		
		  const numQuestions = questions.length;
		
		  useEffect(function () {
		    fetch("http://localhost:8000/questions")
		      .then((res) => res.json())
		      .then((data) => dispatch({ type: "dataReceived", payload: data }))
		      .catch((err) => dispatch({ type: "dataFailed" }));
		  }, []);
		
		  // `dataReceived` can be considered as an event
		
		  return (
		    <div className="app">
		      <Header />
		      <Main>
		        {status === "loading" && <Loader />}
		        {status === "error" && <Error />}
		        {status === "ready" && (
		          <StartScreen numQuestions={numQuestions} dispatch={dispatch} />
		        )}
		        {status === "active" && <Question />}
		      </Main>
		    </div>
		  );
		}

### Displaying Questions ###
1. Question.js

		import Options from "./Options";

		function Question({ question }) {
		  return (
		    <div>
		      <h4>{question.question}</h4>
		      <Options question={question} />
		    </div>
		  );
		}
		
		export default Question;

2. Options.js

		function Options({ question }) {
		  return (
		    <div className="options">
		      {question.options.map((option) => (
		        <button className="btn btn-option" key={option}>
		          {option}
		        </button>
		      ))}
		    </div>
		  );
		}
		
		export default Options;

3. StartScreen.js

		// ...
		<button
          className="btn btn-ui"
          onClick={() => dispatch({ type: "start" })}
		>
		// ...

### Handling New Answers ###
1. It is better to have as much logic as possible that updates state inside the reducer (than in the place where the event is first handled)

### Moving to the Next Question ###
### Displaying Progress ###
1. Progress.js

		function Progress({ index, numQuestions, points, maxPossiblePoints, answer }) {
		  return (
		    <header className="progress">
		      <progress max={numQuestions} value={index + Number(answer !== null)} />
		
		      <p>
		        Question <strong>{index + 1}</strong> / {numQuestions}
		      </p>
		      <p>
		        <strong>{points}</strong> / {maxPossiblePoints}
		      </p>
		    </header>
		  );
		}
		
		export default Progress;

### Finishing a Quiz ###
### Restarting a Quiz ###
1. By reading the reducer, we will know what the application does

### Setting Up a Timer With useEffect ###
1. We start a timer, and the game will end when the timer stops
2. If state lives in the App component, if it changes, all the components will re-render
	1. A performance issue with very large applications
3. Other features:
	1. Allow user to select a certain number of questions
	2. Allow user to filter for the dificulty of questions
	3. We can store the highscore using the API and fetch when the application is opened again
	4. We could store all answers in an array
		1. User can go back in time, and review the answers

### Section Summary: useState vs. useReducer ###
1. Usestate vs Usereducer
2. `useState`
	1. Ideal for **single**, **independent pieces of state** (numbers, strings, single arrays, etc)
	2. Logic to update state is placed directly in event handlers or effects, **spread all over one or multiple components**
		1. All over a component
		2. Even child components if we use lifted state
	3. State is updated by calling `setState` (setter returned from `useState`)
	4. **Imperative** state updates
	5. **Easy** to understand and to use
3. `useReducer`
	1. Ideal for multiple **related pieces of state** and **complex state** (e.g. object with many values and nested objects or arrays)
	2. Logic to update state lives in **one central place, decoupled from components:** the reducer
		1. The logic is decoupled from components
	3. State is updated by **dispatch an action** to a reducer
		1. Reducer knows how to perform state updates for different actions
		2. Reducers map state transitions to actions with well-defined names
	4. **Declarative** state updates: complex state transitions are **mapped** to actions
		1. Instead of setting the following three states, we can dispatch an action

				setScore(0);
				setPlaying(true);
				setTimeSec(0);

				dispatch({ type: 'startGame' });

			1. Downside: Slightly more difficult to understand and implement
	5. More **difficult** to understand and implement

#### When to Use useReducer? ####
1. Flow:

		Just one piece of state? - yes -> `useState`
				|
				No
				|
				v
		Do states frequently update together? --+ 
				|								yes 
				No								|
				|								v
				v				Are you willing to implement 
		Over 3 or 4 pieces		slightly more complex code?
		of related state,						|		|
		including objects?						yes		No
				|								|		|
				No								v		v
				|							`useReducer`useState
				v
		Too many event
		handlers make
		components large and
		confusing?
				|
				No
				|
				v
			useState
				
	1. `useState` should remain your **default choice** for managing state
		1. If there are problems, consider using `useReducer`

### CHALLENGE #1: Constructing a Bank Account With useReducer ###
1. MUST DO

## Section 17: React Router: Building Single-Page Applications (SPA) ##
### Section Overview ###
1. Topics:
	1. **React Router**: most important 3rd-party library
		1. Used in almost all React projects
		2. Used to build apps with multiple pages, that feel as smooth and as fluid as mobile apps (SPAs)
	2. Building our first single-page application (**SPA**)
		1. Example: WorldWise
	3. Styles with **CSS Modules** (new way)

### Constructing Our First App With Vite: "WorldWise" ###
1. `Vite` - used to instantiate a project
	1. Installation:

			npm create vite@4

			React
			JavaScript

		1. It a build tool
		2. It has templates for the listed frameworks
		3. Unlike `create-react-app`, we need to manually install dependencies
			1. Installation is much faster that `create-react-app`
				1. There are a lot less packages
	2. **index.html** is outside the **public** folder
		1. The developer who maintains the template thinks that this is the best structure
			1. React doesn't care about the file structure
	3. **main.jsx**
		1. Stands for JavaScript JSX
			1. Vite wants the extension to be JSX
			2. Pretty much the same as JS file
		2. Smaller and simpler than **index.js** file of `create-react-app`
	4. Running the app:

			npm run dev

	5. `create-react-app` already comes with important developer tools pre-installed
		1. ESLint (We don't want to build React App without ESLint)
			1. For Vite, we need to install ESLint

					npm i eslint vite-plugin-eslint eslint-config-react-app --save-dev

			2. New file: `.eslintrc.json` (to extend eslint with react rules we installed with `eslint-config-react-app`)

					{
						"extends": "react-app"
					}

			4. `vite.config.js` - used to config Vite project. We can configure things about development and building the project. We need to add eslint plugin

					import eslint from 'vite-plugin-eslint'
					...
					export default defineConfig({
						plugins: [react(), eslint()],
					});

			5. Application reloads
			6. Testing:

					function App() {
						let x = 24;

						return <div>Worldwise</div>;
					}

					export default App;

#### What is Routing? ####
1. Routing
	1. With routing, we match **different URLs** to **different UI views** (React components): **routes**
		1. In case of React, we match each URL to a specific React component
			1. Each match between a URL and a component is called a route
			2. When a specific URL is visited, the corresponding React component will be rendered
				1. Example: www.example.com/
					1. Home component is shown
				2. Example: www.example.com/login
					1. Login component is shown
					2. If login is successful, we redirect to www.example.com/app path
	2. This enables users to **navigate between different application screens**, using the browser URL (using links)
	3. Keeps the UI **in sync** with the current browser URL
	4. Note: **The routing only works on the client side**
		1. There is routing on server side
			1. We are not using this in the Client-side React applications
		2. Most front-end frameworks have the client-side routing capabilities baked into the framework
			1. React depends on third-party packages for many different functionalities (routing is one of them)
				1. In React, it is handled by a third-party package called **React Router** (most important and most used)
					1. Must learn because it allows us to build **single-page applications** (routing is fundamental)

### Routing and Single-Page Applications (SPAs) ###
#### Single-Page Applications (SPA) ####
1. Application that is **executed entirely on the client** (browsers)
2. **Routes:** different URLs correspond to different views (components)
	1. SPA Running on Client
		
			User clicks router link (special link)
					|
					v
			URL is changed (In React, react-router package does this job)
					|
					v
			DOM is updated (as a result of URL change)
				When URL is changed, React component
				corresponding to the new URL is
				rendered

		1. In SPAs, **JavaScript** (React) is used to update the page (DOM)
			1. The page is updated by JS
				1. The page is never reloaded (the entire app exists as one page without hard reloads)
		2. The whole cycle can be repeated
			1. Each time a user clicks on a router link, it will change the URL, and the component on the screen (without reloading the page)
3. Feels like a **native app** (Desktop app, or mobile app)
	1. Fantastic UX
4. Additional data **might be loaded** from a web API
	1. SPA can communicate with a server to fetch data it needs
5. We cannot load a completely new page (Otherwise, it cannot be called as SPA)
	1. All React Apps are SPAs (they are never reloaded)
6. For big applications:
	1. Rely on URLs
	2. Rely on routing capabilities

### Implementing Main Pages and Routes ###
1. Installing React Router:

		npm i react-router-dom@6

	1. There are two big ways to declare routes
		1. Traditional way:
			1. We can define routes in a declarative way
				1. We can use special components that React router gives to define routes in JSX
	2. React matched the URL with the `path` that was provided in the JSX, and selects the one that matches
		1. When we manually change the URL, the page gets reloaded

### Linking Between Routes With <Link /> and <NavLink /> ###
1. Traditional way:

		<a href="/pricing">Pricing</a>

	1. Whole page gets reloaded
		1. Check the Network tab
2. SPA way:

		import { Link } from "react-router-dom";

		function HomePage() {
		  return (
		    <div>
		      <h1>Home Page</h1>
		      <Link to="/pricing">Pricing</Link> {/*  **(M)** Only DOM gets updated */}
		    </div>
		  );
		}
		
		export default HomePage;

3. We can bookpark any page, or share the URL of the page with anybody.
4. If we use `NavLink` instead of `Link`, The element gets a `class="active"` property, which can be used to style the active link differently

		<a aria-current="page" class="active" href="/pricing">Pricing</a>

5. Code: HomePage.jsx

		import { Link } from "react-router-dom";
		import PageNav from "../components/PageNav";
		
		function HomePage() {
		  return (
		    <div>
		      <PageNav />
		      <h1>Home Page</h1>
		      <Link to="/pricing">Pricing</Link> {/*  **(M)** Only DOM gets updated */}
		    </div>
		  );
		}
		
		export default HomePage;

4. Code: PageNav.jsx

		import { NavLink } from "react-router-dom";
		
		function PageNav() {
		  return (
		    <nav>
		      <ul>
		        <li>
		          <NavLink to="/">Home</NavLink>
		        </li>
		        <li>
		          <NavLink to="/pricing">Pricing</NavLink>
		        </li>
		        <li>
		          <NavLink to="/product">Product</NavLink>
		        </li>
		      </ul>
		    </nav>
		  );
		}
		
		export default PageNav;

### Styling Options For React Applications ###
#### Styling Options in React ####
1. Why are there so many different ways of styling a React App?
	1. A philosophy of React App is to be un-opinionated in regards to many common aspects of building web-applications 
		1. One such aspect is styling
			1. Styling option: React doesn't care about styling
				1. We have different styling options
					1. Most of them are provided by third-party libraries
2. Different options:
	1. Styling option:
		1. Inline CSS
			1. Where?
				1. JSX elements
			2. How?
				1. `style` prop
			3. Scope
				1. JSX element
					1. Only to a particular JSX element it is applied to (locally scoped)
			4. Based on
				1. CSS
		2. CSS or Sass file
			1. Where?
				1. External file
			2. How?
				1. `className` prop
			3. Scope
				1. Entire app
					1. Proplems: Global
						1. Any JSX element could use any of the classes in the external CSS file
							1. Example: We don't know which components use which classes, if we update classes, they will be unnecessary repurcussions.
							2. Example: If we add a new class with the name of a class that already exists, there will be clashes between classes 
					2. Solution: CSS must never be global, but must be scoped to individual components
			4. Based on
				1. CSS
		3. CSS Modules
			1. Where?
				1. One external file per component
			2. How?
				1. `className` prop
			3. Scope
				1. Component
					1. No other component can use them
						1. Makes the components modular and re-usable
							1. Better reflects React's separation of concerns
			4. Based on
				1. CSS
		4. CSS-in-JS (library) (Styled components)
			1. Where?
				1. External file or component file
					1. We write CSS inside a JS file. In the same file we define a component
						1. React components are created with styles directly applied to them which can be used just like any other component
							1. Embraces React philosophy - A component must contain all the information related to its appearance
			2. How?
				1. Constructs new component
			3. Scope
				1. Component
			4. Based on
				1. JavaScript
		5. Utility-first CSS (tailwindcss)
			1. Where?
				1. JSX elements
					1. We use pre-defined utility classes to define individual styles to use
						1. Flexbox
						2. To make layouts responsive
						3. To make hover effects
						4. (to design the entire UI without leaving the JSX markup)
			2. How
				1. `className` prop
			3. Scope
				1. JSX element
			4. Based on
				1. CSS
		6. Alterative to styling with CSS: UI libraries like MUI, Chakra UI, Mantine, etc. (We don't have to write any CSS)
			1. Libraries contain pre-built, and pre-styled components that are common in most web-applications (not ideal for beginners)

### Using CSS Modules ###
1. CSS modules comes out of the box with `create-react-app` and `vite` (nothing to install)
2. One external CSS file per component
	1. Convention: `<component-name>.module.css`
	2. Including the the component file:

			import styles from './PageNav.module.css';
			
			// ...

			<nav className={styles.nav}>

		1. Internals: The class is converted to:

				<nav class="_nav_hqhhq_1">

			1. classname + random id (unique to the module)
				1. We can give the same classname in different modules
3. Global CSS: global reset, font, ...
	1. We can include an external CSS file
		1. No classnames exist
	2. Global classnames will not work

			<h1 className="test">Home Page</h1>

		1. Solution:

				:global(.test) {
					// ...
				}

	3. The following doesn't work

			.nav .active {
				// ...
			}

		1. Solution:

				.nav :global(.active) {
					// ...
				}

			1. `:global(...)` is useful when working with classes provided by external sources
				1. Otherwise, css modules will append a random id

						.active_gasdf_1

4. Composing classes
	1. Not covered here

### Building the Pages ###
1. The images in `assets` folder are directly imported into JS code
2. For css modules, we need to write classnames using camelCase and not kabab-case

### Building the App Layout ###
1. We can have a folder for each component
2. Most of the code related to components can be inside the components

### Nested Routes and Index Route ###
1. Nested routes
	1. We need them when we want a part of the UI by a part of the URL

			/cities

		1. Shows list of cities
	2. It is nested route, if the path decides what component is rendered inside another component
	3. Nested routes
		1. App.jsx

				<Route path="app" element={<AppLayout />}>
		          {" "}
		          {/* parent path is not required */}
		          <Route path="cities" element={<p>List of cities</p>} />
		          <Route path="countries" element={<p>Countries</p>} />
		          <Route path="form" element={<p>Form</p>} />
		        </Route>

			2. Sidebar.jsx

					function Sidebar() {
					  return (
					    <div className={styles.sidebar}>
						// ...
					
					      <Outlet /> {/* Similar to children prop */}
							
						// ...

	2. Instead of using `useState` to store the active tab info, we let the React router to store the state and URL path
		1. Overall navigation (including sub-navigations) are managed using React router

### Implementing the Cities List ###
1. Proptypes:

		import PropTypes from "prop-types";

		// ...

		Message.propTypes = {
		  message: PropTypes.string.isRequired,
		};

### Implementing the Countries List ###
1. We can have all imports from third-party libraries on top, and other imports below

### Storing State in the URL ###
#### The URL for State Management ####
1. The URL is an excellent place to store UI state and an alternative to `useState` in some situations!
	1. Example: open/closed panels, currently selected list item, list sorting order, applied list filters
2. Why?
	1. Easy way to store state in a **global place**, accessible to **all components** in the app
		1. We can read the value from the URL, wherever the component is in the component tree
	2. Good way to **"pass" data** from one page into the next page
		1. Without storing the data in some temporary place inside the app
	3. Makes it possible to **bookmark and share** the page with the exact UI state it had at the time
		1. Example: We might filter products by color, price, etc...
			1. We can share the page with someone, and same filters will be applied (great UX)
2. Implementation:

		www.example.com/app/cities/lisbon?lat=38.728&lng=-9.141

	1. path - state that is not useful for state management
	2. params - `/lisbon`
		1. Useful to pass data to next page 
	3. query string - `lat=38.728&lng=-9.141`
		1. Useful to store global state that should be accessible everywhere

#### Example: Params and Query String ####
1. `lisbon` - A link can contain this param and it gets passed to the next page whenever the user clicks on the link
2. `lat=38.728&lng=-9.141` - They correspond to specific positions on the map
3. **City name** and **GPS location** were retrieved from the **URL** instead of application state!

### Dynamic Routes With URL Parameters ###
1. New route:

		<Route path="cities/:id" element={<City />} />

2. Link to the route:

		<Link className={styles.cityItem} to={`${id}`}>
          <span className={styles.emoji}>{emoji}</span>
          <h3 className={styles.name}>{cityName}</h3>
          <time className={styles.date}>({formatDate(date)})</time>
          <button className={styles.deleteBtn}>&times;</button>
		</Link>

3. Retrieve passed data using `useParam` hook

		const { id } = useParams();

### Reading and Setting a Query String ###
### Programmatic Navigation with useNavigate ###
1. To move to a new URL without the user having to click on any link
	1. Use-case: After a user submits a form (programmatic navigation can be used)
2. Code: Form:

		<div className={styles.buttons}>
          <Button type="primary">Add</Button>
          <Button
            type="back"
            onClick={(e) => {
              e.preventDefault();
              navigate(-1);
            }}
          >
            {" "}
            {/**Number of steps back */}
            &larr; Back
          </Button>
        </div>

2. Code: Button

		import styles from "./Button.module.css";
		import PropTypes from "prop-types";
		
		function Button({ children, onClick, type }) {
		  return (
		    <button onClick={onClick} className={`${styles.btn} ${styles[type]}`}>
		      {children}
		    </button>
		  );
		}
		
		Button.propTypes = {
		  children: PropTypes.node.isRequired,
		  onClick: PropTypes.func.isRequired,
		  type: PropTypes.string.isRequired,
		};
		
		export default Button;

### Programmatic Navigation with <Navigate /> ###
1. `<Navigate />` - not so much used.
	1. One important use-case: Inside nested routes
		1. Immediately navigate to a particular URL
	2. **It is a redirect**
	
			<Route index element={<Navigate to="cities" />} />
			<Route
			  path="cities"
			  element={<CityList cities={cities} isLoading={isLoading} />}
			/>

		1. We cannot use `navigate` function coming from `useNavigate` hook
			1. We use declarative JSX `<Navigate ...>` to redirect (`navigate` is imperative)

## Section 18: Advanced State Management: The Context API ##
### Section Overview ###
1. Topics:
	1. Context API **patterns**
		1. Powerful pattern
		2. Apply
	2. State management **deep dive**
		1. New types of state & tools to handle them
	3. Including an interactive **map**

### CHALLENGE #1: Understand "The Atomic Blog" App ###
1. Study code and data flow of `12-atomic-blog`
	1. Open it up in VS Code
		1. How it works
		2. What it does
		3. Open terminal

				npm install

		4. What was used to instantiate the project

				react-scripts 

### What is the Context API? ###
#### A Solution to Prop Drilling ####
1. Task: Passing state into multiple deeply nested child components
	1. Solution 1: Pass props down
		1. Cumbersome and inconvenient
			1. Prop drilling
	2. Solution 2: Component composition using `children` prop
		1. It doesn't always solve the problem
	3. Solution 3: Directly passing a state from parent component to deeply nested child component
		1. **Context API**
			1. Allows a component anywhere in the tree to read state that a context shares

#### What is Context API? ####
1. Context API:
	1. System to pass data throughout the app **without manually passing props** down the component tree
	2. Allows us to **"broadcase" global state** to the entire app (available to all child components of a certain context)
		1. **Provider:** Special React component that gives all child components access to `value`
			1. Can sit anywhere in the component tree
				1. Convention to place it at the top (`App` component)
		2. **value:** data that we want to make available (usually state and function)
			1. It is passed into provider
			2. value contains one or more state variables & some setter functions
		3. **Consumers:** all components that read the provided context `value`
			1. They are components that subscribe to the context
				1. They can read the value from the context
			2. Any number of consumers can be provided with a context
	3. Whenever a context value is updated, all consumers subscribed to the context are re-rendered
		1. Provider will immediately notify consumers about the value change, and will re-render the components
	4. We can have as many contexts as we want and place them in the component tree

### Constructing and Providing a Context ###
1. We usually construct one context per state domain
	1. One context for posts
	2. One context for search query
2. Code:

		// 1) CREATION OF CONTEXT
		const PostContext = createContext(); // we can pass default value, but it cannot change over time. So we pass `null` or not pass anything.
		// It is a component, so upper-case letter

		// ...

		// 2) PROVIDE VALUE TO CHILD COMPONENTS
		<PostContext.Provider
		  value={{
		    posts: searchedPosts,
		    onClearPosts: handleClearPosts,
		    onAddPost: handleAddPost,
		    searchQuery,
		    setSearchQuery,
		  }}
		>
		// ...
		</PostContext.Provider>

### Consuming the Context ###
1. Code:

		const { searchQuery, setSearchQuery } = useContext(PostContext);

3. The context api make the components much more independent and standalone
	1. We can re-use `List` anywhere now

			<footer>
				<List />
				// ...
			</footer>

		1. We didn't have to pass any props first into the `footer` and then to the `List`

### Advanced Pattern: A Custom Provider and Hook ###
1. Implementation of advanced patterns
	1. We can remove all state and state updating logic from a component and place it in a custom provider component.
2. Code: PostProvider.js

		import { createContext, useContext, useState } from "react";
		import { faker } from "@faker-js/faker";
		
		function createRandomPost() {
		  return {
		    title: `${faker.hacker.adjective()} ${faker.hacker.noun()}`,
		    body: faker.hacker.phrase(),
		  };
		}
		
		const PostContext = createContext();
		
		function PostProvider({ children }) {
		  const [posts, setPosts] = useState(() =>
		    Array.from({ length: 30 }, () => createRandomPost())
		  );
		  const [searchQuery, setSearchQuery] = useState("");
		
		  const searchedPosts =
		    searchQuery.length > 0
		      ? posts.filter((post) =>
		          `${post.title} ${post.body}`
		            .toLowerCase()
		            .includes(searchQuery.toLowerCase())
		        )
		      : posts;
		
		  function handleAddPost(post) {
		    setPosts((posts) => [post, ...posts]);
		  }
		
		  function handleClearPosts() {
		    setPosts([]);
		  }
		
		  return (
		    <PostContext.Provider
		      value={{
		        posts: searchedPosts,
		        onClearPosts: handleClearPosts,
		        onAddPost: handleAddPost,
		        searchQuery,
		        setSearchQuery,
		      }}
		    >
		      {children}
		    </PostContext.Provider>
		  );
		}
		
		function usePosts() {
		  const context = useContext(PostContext);
		  if (context === undefined)
		    throw new Error("PostContext was used outside of the PostProvider");
		  return context;
		}
		
		export { PostProvider, usePosts };

3. Code: App.js

		<PostProvider>
		  <Header />
		  <Main />
		  <Archive />
		  <Footer />
		</PostProvider>

### Thinking in React: Advanced State Management ###
#### Review: What is State Management? ####
1. State management: Giving each piece of state the right home
	1. **When** to use state
	2. **Types** of state **(accessibility)**: local vs. global
	3. From lecture "Fundamentals of State Management". You can keep using the flowchart
2. This lecture:
	1. **Types** of state (**domain**): UI vs remote
	2. **Where** to place each piece of state
	3. **Tools** to manage all types of state

#### Types of State ####
1. Classification:
	1. State Accessibility (Check if this component was rendered **twice**, should a state update in one of the components reflect in the other one? No - Local State, Yes - Global State)
		1. Local State
			1. Needed only by **one or few components**
				1. Only accessible inside the component it was defined in + child components
		2. Global State
			1. Might be needed by **many components** (in different parts of the tree)
				1. Can be made accessible in every single component in the tree
	2. State Domain (they are managed in a different way)
		1. Remote State
			1. All application data **loaded from a remote server** (usually using an API)
				1. Usually resides on a server that is loaded into the application
			2. Usually obtained in an **asynchronous** way
				1. Because data might need to be re-fetched an updated frequently
					1. For large-scale applications, data needs to be
						1. Cached
						2. Re-validated
						3. ...
			3. We need some specialized tools for the above
		2. UI State
			1. Everything else
				1. Theme
				2. List filters
				3. Form data
				4. Open panels
				5. ...
			2. Usually **synchronous** and stored in the application
				1. Doesn't interact with any server
			3. Easy to handle with the tools we know of
				1. `useState`
				2. `useReducer`

#### State Placement Options ####
1. Where to physically place state?
	1. Options:
		1. Local component:
			1. Tools
				1. `useState`
				2. `useReducer`
				3. `useRef` (it doesn't re-render a component)
			2. When to use?
				1. Local state
		2. Parent component (of all components that need the state)
			1. Tools
				1. `useState`
				2. `useReducer`
				3. `useRef`
			2. When to use?
				1. Lifting up state
		3. Context (A better solution for the above)
			1. Tools
				1. Context API + `useState` or `useReducer`
					1. Context itself doesn't manage state
						1. It only gives access of state to the tree which is managed using other mechanisms 
			2. When to use?
				1. Global state (preferably UI state)
					1. Not for remote state
		4. 3rd-party library
			1. Tools
				1. Redux
				2. React Query
				3. SWR
				4. Zustand
				5. ...
			2. When to use?
				1. Global state (remote or UI states)
		5. URL
			1. Tools
				1. React Router
			2. When to use?
				1. Global state
					1. Easily sharable or bookmarkable
				2. Passing between pages
		6. Browser (doesn't re-render any components, but it is technically application state)
			1. Tools
				1. Local storage
				2. Session storage
				3. ...
			2. When to use?
				1. Storing data in user's browser
#### State Management Tool Options ####
1. How to manage different types of state in practice?
	1. Local UI State
		1. `useState`
		2. `useReducer`
		3. `useRef`
	2. Global UI State
		1. Context API + `useState`/`useReducer` (good enough)
		2. Redux, Zustand, Recoil, etc. (if we want more performance)
		3. React Router (for more performance)
	3. Local Remote State
		1. `fetch` + `useEffect` + `useState`/`useReducer` (small applications only)
			1. `fetch` inside `useEffect` loads data from a remote location
			2. `useState`, or `useReducer` can be used to store the state fetched
	4. Global Remote State
		1. Context API + `useState`/`useReducer`
		2. Redux, Zustand, Recoil, etc.
		3. Tools highly specialized in handling remote state (**They have caching and automatic re-fetching (to deal with async nature of remote state)**)
			1. React Query
			2. SWR
			3. RTK Query

### Back to "WorldWise": Constructing a CitiesContext ###
1. Context API
	1. For small applications
		1. Where performance is not an issue

### Consuming the CitiesContext ###
### Finishing the City View ###
1. Code: BackButton.jxs

		import { useNavigate } from "react-router-dom";
		import Button from "./Button";
		
		function BackButton() {
		  const navigate = useNavigate();
		
		  return (
		    <div>
		      <Button
		        type="back"
		        onClick={(e) => {
		          e.preventDefault();
		          navigate(-1);
		        }}
		      >
		        {" "}
		        {/**Number of steps back */}
		        &larr; Back
		      </Button>
		    </div>
		  );
		}
		
		export default BackButton;

### Including a Map With the Leaflet Library ###
1. Third-party package

		npm i react-leaflet leaflet

	1. `react-leaflet` is built on `leaflet`
2. React Leaflet: [https://react-leaflet.js.org/docs/start-setup/](https://react-leaflet.js.org/docs/start-setup/)

### Displaying City Markers on Map ###
1. Leaflet adds classes which can be used for styling
	1. Make them global with `.global(...)` since we are using CSS modules.

### Interacting With the Map ###
1. In Leaflet map, we need a custom component to implement centering
2. Capturing position:

		function DetectClick() {
		  const navigate = useNavigate();
		  useMapEvents({
		    click: (e) => {
		      // console.log(e); // Sent by leaflet library
		      navigate(`form?lat=${e.latlng.lat}&lng=${e.latlng.lng}`);
		    },
		  });
		}

### Setting Map Position With Geolocation ###
1. Code: useGeolocation.js

		import { useState } from "react";

		export function useGeolocation(defaultPosition = null) {
		  const [isLoading, setIsLoading] = useState(false);
		  const [position, setPosition] = useState(defaultPosition);
		  const [error, setError] = useState(null);
		
		  function getPosition() {
		    if (!navigator.geolocation)
		      return setError("Your browser does not support geolocation");
		
		    setIsLoading(true);
		    navigator.geolocation.getCurrentPosition(
		      (pos) => {
		        setPosition({
		          lat: pos.coords.latitude,
		          lng: pos.coords.longitude,
		        });
		        setIsLoading(false);
		      },
		      (error) => {
		        setError(error.message);
		        setIsLoading(false);
		      }
		    );
		  }
		
		  return { isLoading, position, error, getPosition };
		}

2. Code: Map.jsx

		import styles from "./Map.module.css";
		import { useNavigate, useSearchParams } from "react-router-dom";
		import {
		  MapContainer,
		  TileLayer,
		  Marker,
		  Popup,
		  useMap,
		  useMapEvents,
		} from "react-leaflet";
		import { useCities } from "../contexts/CitiesContext";
		import PropTypes from "prop-types";
		import { useEffect, useState } from "react";
		import { useGeolocation } from "../hooks/useGeolocation";
		import Button from "./Button";
		
		function Map() {
		  const navigate = useNavigate();
		  const { cities } = useCities();
		  const [mapPosition, setMapPosition] = useState([40, 0]);
		  const [searchParams] = useSearchParams();
		  const {
		    isLoading: isLoadingPosition,
		    position: geolocationPosition,
		    getPosition,
		  } = useGeolocation();
		
		  const mapLat = searchParams.get("lat");
		  const mapLng = searchParams.get("lng");
		
		  useEffect(
		    function () {
		      if (mapLat && mapLng) setMapPosition([mapLat, mapLng]);
		    },
		    [mapLat, mapLng]
		  );
		
		  useEffect(
		    function () {
		      if (geolocationPosition)
		        setMapPosition([geolocationPosition.lat, geolocationPosition.lng]);
		    },
		    [geolocationPosition]
		  );
		
		  return (
		    <div className={styles.mapContainer} onClick={() => navigate("form")}>
		      <Button type="position" onClick={getPosition}>
		        {isLoadingPosition ? "Loading..." : "Use your position"}
		      </Button>
		      <MapContainer
		        center={mapPosition}
		        zoom={6}
		        scrollWheelZoom={true}
		        className={styles.map}
		      >
		        <TileLayer
		          attribution='&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
		          url="https://{s}.tile.openstreetmap.fr/hot/{z}/{x}/{y}.png"
		        />
		        {cities.map((city) => (
		          <Marker
		            position={[city.position.lat, city.position.lng]}
		            key={city.id}
		          >
		            <Popup>
		              <span>{city.emoji}</span> <span>{city.cityName}</span>
		            </Popup>
		          </Marker>
		        ))}
		
		        <ChangeCenter position={mapPosition} />
		        <DetectClick />
		      </MapContainer>
		    </div>
		  );
		}
		
		function ChangeCenter({ position }) {
		  const map = useMap();
		  map.setView(position);
		  return null;
		}
		
		function DetectClick() {
		  const navigate = useNavigate();
		  useMapEvents({
		    click: (e) => {
		      // console.log(e); // Sent by leaflet library
		      navigate(`form?lat=${e.latlng.lat}&lng=${e.latlng.lng}`);
		    },
		  });
		}
		
		ChangeCenter.propTypes = {
		  position: PropTypes.array.isRequired,
		};
		
		export default Map;

### Fetching City Data in the Form ###
### Constructing a New City ###
1. We grab whatever we need from npm

		npm i react-datepicker

2. For small applications, we synchronize application state with the UI using `useEffect` - UI in sync with remote state
	1. For big applications, we use React Query
		1. Whenever we add something new to the remote state, the data will get automatically re-fetched into our application
2. Handler functions can be async functions

### Deleting a City ###
### Advanced State Management System: Context + useReducer ###
1. Converting state management into a reducer
	1. Common with Context API

### Adding Fake Authentication: Setting Up Context ###
### Adding Fake Authentication: Implementing "Login" ###
### Adding Fake Authentication: Protecting a Route ###
### CHALLENGE #2: Refactoring "React Quiz" to Context API ###

## Section 19: Performance Optimization and Advanced useEffect ##
### Section Overview ###
### Performance Optimization and Wasted Renders ###
### The Profiler Developer Tool ###
### A Surprising Optimization Trick With children ###
### Uderstanding memo ###
### memo in Practice ###
### Understanding useMemo and useCallback ###
### useMemo in Practice ###
### useCallback in Practice ###
### Optimizing Context Re-Renders ###
### Back to the "WorldWise" App ###
### Optimizing Bundle Size With Code Splitting ###
### Don't Optimize Prematurely! ###
### useEffect Rules and Best Practices ###
### CHALLENGE #1: Fix Performance Issues in "Workout Timer" ###
### Setting State Based on Other State Updates ###
### Using Helper Functions in Effects ###
### Closures in Effects ###

## Section 20: Redux and Modern Redux Toolkit (With Thunks) ##
### Section Overview ###
### Introduction to Redux ###
### Constructing a Reducer: Bank Account ###
### Constructing a Redux Store ###
### Working with Action Creators ###
### Adding More State: Customer ###
### Professional Redux File Structure: State Slices ###
### Back to React! Connecting our Redux App with React ###
### Dispatching Actions from Our React App ###
### The Legacy Way of Connecting Components to Redux ###
### Redux Middleware and Thunks ###
### Making an API Call with Redux Thunks ###
### The Redux DevTools ###
### What is Redux Toolkit (RTK)? ###
### Constructing the Store with RTK ###
### Constructing the Account Slice ###
### Back to Thunks ###
### Creating the Customer Slice ###
### Redux vs. Context API ###

## Section 21: Part 4: PROFESSIONAL REACT DEVELOPMENT [2 PROJECTS] ##
### Introduction to Part 4 ###
### Useful Resources for Part 4 ###

## Section 22: React Router with Data Loading (v6.4+) ##
### Section Overview ###
### Setting Up a New Project: "Fast React Pizza Co." ###
### Application Planning ###
### Setting Up a Professional File Structure ###
### A New Way of Implementing Routes ###
### Building the App Layout ###
### Fetching Data with React Router "Loaders": Pizza Menu ###
### Displaying a Loading Indicator ###
### Handling Errors with Error Elements ###
### Fetching Orders ###
### Writing Data with React Router "Actions" ###
### Error Handling in Form Actions ###

## Section 23: [Optional] Tailwind CSS Crash Course: Styling the App ##
### Section Overview ###
### What is Tailwind CSS? ###
### Setting Up Tailwind CSS ###
### Working with Color ###
### Styling Text ###
### The Box Model: Spacing, Borders, and Display ###
### Responsive Design ###
### Using Flexbox ###
### Using CSS Grid ###
### Styling Buttons: Element States and Transitions ###
### Styling Form Elements ###
### Reusing Styles with @apply ###
### Reusing Styles with React Components ###
### Absolute Positioning, z-index, and More ###
### Configuring Tailwind: Custom Font Family ###
### Styling the Menu ###
### Styling the Cart ###
### Styling the Order Form ###
### Styling the Order Overview ###

## Section 24: Adding Redux and Advanced React Router ##
### Section Overview ###
### Modeling the "User" State with Redux Toolkit ###
### Reading and Updating the User State ###
### Modeling the "Cart" State ###
### Adding Menu Items to the Cart ###
### Building the Cart Overview with Redux Selectors ###
### Building the Cart Page ###
### Deleting Cart Items ###
### Updating Cart Quantities ###
### Using the Cart for New Orders ###
### Redux Thunks with createAsyncThunk ###
### Integrating Geolocation ###
### Fetching Data Without Navigation: useFetcher ###
### Updating Data Without Navigation ###

## Section 25: Setting Up Our Biggest Project + Styled Components ##
### Section Overview ###
### Application Planning ###
### Setting Up the Project: "The Wild Oasis" ###
### Introduction to Styled Components ###
### Global Styles with Styled Components ###
### Styled Component Props and the "css" Function ###
### Building More Reusable Styled Components ###
### Setting Up Pages and Routes ###
### Building the App Layout ###
### Building the Sidebar and Main Navigation ###

## Section 26: Supabase Crash Course: Building a Back-End! ##
### Section Overview ###
### What is Supabase? ###
### Constructing a New Database ###
### Modeling Application State ###
### Constructing Tables ###
### Relationships Between Tables ###
### Adding Security Policies (RLS) ###
### Connecting Supabase with Our React App ###
### Setting up Storage Buckets ###

## Section 27: React Query: Managing Remote State ##
### Section Overview ###
### What is React Query? ###
### Setting up React Query ###
### Make Sure to Use React Query v4! ###
### Fetching Cabin Data ###
### Mutations: Deleting a Cabin ###
### Displaying Toasts (Notifications) ###
### Introducing Another Library: React Hook Form ###
### Constructing a New Cabin ###
### Handling Form Errors ###
### Uploading Images to Supabase ###
### Editing a Cabin ###
### Abstracting React Query into Custom Hooks ###
### Duplication Cabins ###
### Fetching Applications Settings ###
### Updating Application Settings ###

## Section 28: Advanced React Patterns ##
### Section Overview ###
### An Overview of Reusability in React ###
### Setting Up an Example ###
### The Render Props Pattern ###
### A Look at Higher-Order Components (HOC) ###
### The Compound Component Pattern ###
### Building a Model Window Using a React Portal ###
### Converting the Modal to a Compound Component ###
### Detecting a Click Outside the Modal ###
### Confirming Cabin Deletions ###
### Building a Reusable Table ###
### Applying the Render Props Pattern ###
### Building a Reusable Context Menu ###

## Section 29: [Optional] Implementing More Features: Authentication, Dark Mode, Dashboard, etc ##
### Section Overview ###
### Client-Side Filtering: Filtering Cabins ###
### Client-Side Sorting: Sorting Cabins ###
### Building the Bookings Table ###
### Uploading Sample Data ###
### API-Side Filtering: Filtering Bookings ###
### API-Side Sorting: Sorting Bookings ###
### Building a Reusable Pagination Component ###
### API-Side Pagination: Paginating Bookings ###
### Prefetching with React Query ###
### Building the Single Booking Page ###
### Checking in a Booking ###
### Adding Optional Breakfast ###
### Checking Out a Booking (+ Fixing a Small Bug) ###
### Deleting a Booking ###
### Authentication: User Login with Supabase ###
### Authorization: Protecting Routes ###
### User Logout ###
### Fixing an Important Bug ###
### Building the Sign Up Form ###
### User Sign Up ###
### Authorization on Supabase: Protecting Database (RLS) ###
### Building The App Header ###
### Updating User Data and Password ###
### Implementing Dark Mode with CSS Variables ###
### Building the Dashboard Layout ###
### Computing Recent Bookings and Stays ###
### Displaying Statistics ###
### Displaying a Line Chart with the Recharts Library ###
### Displaying a Pie Chart ###
### Displaying Stays for Current Day ###
### Error Boundaries ###
### Final Touches + Fixing Bugs ###

## Section 30: Deployment with Netlify and Vercel ##
### Section Overview ###
### Deploying to Netlify ###
### Setting Up a Git and GitHub Repository ###
### Deploying to Vercel ###

## Section 31: PART 5: FULL-STACK REACT WITH NEXT.JS [1 PROJECT] ##
### Introduction to Part 5 ###
### Useful Resources for Part 5 ###

## Section 32: Overview of Next.js with the "App" Router ##
### Section Overview ###
### Download Fresh Starter Files + Slides! ###
### An Overview of Server-Side Rendering (SSR) ###
### Experiment: Manual SSR With React DOM + Node.js ###
### The Missing Piece: Hydration ###
### Implementing Hydration ###
### What is Next.js? ###
### Setting up a Next.js Project ###
### Frequent Next.js Updates + Documentation ###
### Defining Routes and Pages ###
### Navigating Between Pages ###
### Constructing a Layout ###
### What are React Server Components? (RSC - Part 1) ###
### Fetching Data in a Page ###
### Adding Interactivity with Client Components ###
### Displaying a Loading Indicator ###
### How RSC Works Behind the Scenes (RSC - Part 2) ###
### RSC vs. SSR: How are They Related? (RSC - Part 3) ###

## Section 33: Starting to Build the "Wild Oasis" Website ##
### Section Overview ###
### Project Planning: "The Wild Oasis" Customer Website ###
### Project Organization ###
### Styling with Tailwind CSS ###
### Adding Page Metadata and Favicon ###
### Loading and Optimization Fonts ###
### Improving the Navigation and Root Layout ###
### Optimizing Images with Next.js <Image /> Component ###
### Building the Home Page ###
### Building the About Page with Responsive Images ###
### Adding Nested Routes and Pages ###
### Adding a Nested Layout ###

## Section 34: Data Fetching, Caching, and Rendering ##
### Section Overview ###
### Setting up Supabase ###
### Fetching and Displaying Cabin List ###
### Streaming Route Segments with loading.js File ###
### What is React Suspense? ###
### Streaming UI with Suspense: Cabin List ###
### Dynamic Route Segments: Building the Cabin Page ###
### Generating Dynamic Metadata ###
### Error Handling: Setting Up Error Boundaries ###
### Error Handling: "Not Found" Errors ###
### Different Types of SSR: Static vs. Dynamic Rendering ###
### Analyzing Rendering in Our App ###
### Making Dynamic Pages Static with generateStaticParams ###
### Static Site Generation (SSG) ###
### Partial Pre-Rendering ###
### How Nest.js Caches Data ###
### Experimenting with Caching and ISR ###
### CHALLENGE #1: Fetching the Number of Cabins ###

## Section 35: Client and Server Interactions ##
### Section Overview ###
### Blurring the Boundary Between Server and Client (RSC - Part 4) ###
### Client Components in Server Components ###
### Highlighting Current Side Navigation Link ###
### Sharing State Between Client and Server: The URL ###
### Advanced: Server Components in Client Components ###
### Data Fetching Strategies for the Reservation Section ###
### Using the Context API for State Management ###
### Constructing an API Endpoint with Route Handlers ###

## Section 36: Authentication with NextAuth (Auth.js) ##
### Section Overview ###
### Setting up NextAuth ###
### Getting the User Session ###
### What is Middleware in Next.js? ###
### Protecting Routes with NextAuth Middleware ###
### Building a Custom Sign in Page ###
### Building a Custom Sign Out Button ###
### Constructing a New Guest on First Sign In ###

## Section 37: Mutations with Server Actions + Modern React Hooks ##
### Section Overview ###
### What are Server Actions? ###
### Updating the Profile Using a Server Action ###
### Manual Cache Revalidation ###
### Displaying a Loading Indicator: The useFormStatus Hook ###
### Building the Guest's Reservations Page ###
### Deleting a Reservation ###
### Another Loading Indicator: The useTransition Hook ###
### CHALLENGE #1: Updating a Reservation ###
### Removing Reservations Immediately: The useOptimistic Hook ###
### Back to the Cabin Page: Finishing the Date Selector ###
### Constructing a New Rerservation ###

## Section 38: Deployment with Vercel ##
### Section Overview ###
### Setting up the GitHub Repository ###
### Deploying to Vercel ###
### Updating Environment Variables and OAuth Credentials ###

## Section 39: [OPTIONAL] Legacy Next.js: The "Pages" Router ##
### Section Overview ###
### Setting up Another Project ###
### Routes, Pages, and Navigation ###
### Dynamic Routes ###
### Constructing a Layout with a Custom _App ###
### Constructing Pages ###
### Defining Page Title and Favicon ###
### Fetching Data with getStaticProps (SSG) ###
### Fetching Data with getServerSideProps (SSR) ###
### API Routes ###
### Handling Form Submissions ###

## Section 40: The End! ##
### Where to Go from Here ###