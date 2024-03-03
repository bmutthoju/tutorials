# The Complete Javascript Course #
## Section 1: Welcome, Welcome, Welcome! ##
### Course Structure and Projects ###
1. Knowing nothing about JS to expert JS developer
2. The best way to learn JS
3. Overview:
	1. 20 sections - 60 hours
	2. 2 - 3: Fundamentals (solid foundations)
	3. 5 - Developer skills
	4. 7 - DOM Manipulation - 3 simple applications
	5. 8 - How JavaScript works
	6. 9 - Modern operators (ES6+)
	7. 10 - Functions (strings, closures, ...)
	8. 11 - Arrays
	9. 12 - Numbers, Dates, Timers
	10. 13 - Advanced DOM
		1. Lazy image loading
		2. Tabed component
		3. Slider
		4. ...
	11. 14 - Object-Oriented JS (ES6 classes, constructors)
	12. 15 - MAPTY Project
		1. Planning & structuring
	13. 16 - Asynchronous JS
		1. AJAX
	14. 17 - Modern JS Applications
	15. 18 - Forkify Project
	16. 19 - Deployment and Git
		1. NPM
		2. Babel
		3. Parcel
		4. ES6 modules
		5. Netlify

### Read Before You Start! ###
1. Download starter files and final code from GitHub repo:
	1. [https://github.com/jonasschmedtmann/complete-javascript-course](https://github.com/jonasschmedtmann/complete-javascript-course)
2. Download course material:
	1. [course-material-v2.zip](https://www.udemy.com/course/the-complete-javascript-course/learn/lecture/22838299#content)
3. Friendly community with students: Updates as well
	1. [https://discord.gg/uhMkpf4](https://discord.gg/uhMkpf4)
4. [Online tools](http://codingheroes.io/resources/)

### Watch Before You Start! ###
1. Code along
	1. Just watching will not help learn
2. Try all coding challenges
	1. Try to understand the lectures and solve if not able to
3. Understand section by section
	1. Practice
	2. Understand
	3. Move on
4. Try to solve questions
5. Ask questions
6. Have fun

### Setting Up Our Code Editor ###
1. Code editor:
	1. VS Code - best code editor that exists
		1. Alternatives:
			1. Atom
			2. Brackets
		2. Open VS Code
			1. Cog
				1. Color Theme
					1. Monokai Pro
						1. Extensions
							1. Search: Monokai Pro
								1. Download - paid theme
					2. Monokai Classic - free (good theme)
				2. Settings
					1. Auto Save: OnFocusChange (when we move away, it will save)
					2. Font Size
					3. Multi Cursor Modifier: ctrl/Cmd
					4. Work Wrap: On
					5. Format On Save: On
						1. We need to install formatter
				3. File Icon Theme
					1. Seti
2. Install latest version of Google chrome

## Section 2: JavaScript Fundaments - Part 1 ##
### Section Intro ###
1. Fundamentals:
	1. Variables
	2. Data types
	3. Operators
	4. If/Else statements
	5. ...

### Hello World! ###
1. Open browser:
	1. Ctrl+Alt+J
		1. Console
	2. Right click > Inspect > Console
	3. View > Developer > Javascript Console
2. Console:

		alert("Hello World!") // opens popup window
		let js = 'amazing'
		if (js === 'amazing') alert('JavaScript is FUN!')
		js = 'boring'
		if (js === 'amazing') alert('JavaScript is FUN!')
		// hit up arrow to go to previous commands
		
		// Math
		40 + 8 + 23 - 10

### A Brief Introduction to JavaScript ###
1. Section: Javascript Fundamentals - Part 1
2. What is Javascript?
	1. Javascript is a high-level, object-oriented, multi-paradigm, programming language
	2. Programming language: It is a tool that allows us to write code that will instruct a computer to do something
	3. High-level language: We don't have to worry about complex stuff like memory management
		1. The language has abstractions over the small details that we don't have to worry about
			1. It makes the language easy to write and learn
	4. Object-Oriented language: It is mostly based on objects, for storing most kinds of data
	5. Multi-Paradigm language: It is very flexible and versatile and we can use different programming styles (imperative, declarative)
		1. Ways of structuring our code
3. The role of Javascript in web development
	1. HTML, CSS, and JS work together for creation of beautiful, interactive, and dynamic websites / web-applications
		1. HTML - responsible for content of the page
			1. Text
			2. Images
			3. Buttons
			4. ...
		2. CSS - responsible for the presentation of the content
			1. Styling
			2. Layout
		3. JS - real programming language: for building web applications - allows developers to:
			1. Add dynamic, interactive effects to web-page
			2. Manipulate content or CSS
			3. Load data from remote servers
				1. Build entire applications
	2. Roles:
		1. HTML - Nouns
			1. p - paragraph (noun)
			
					<p></p>
			
		2. CSS - Adjectives
			1. describes the noun
			2. paragraph is red (adjective)
			
					p {color: red}
			
		3. JS - Verbs
			1. Hide (verb) the paragraph - we are doing something
			
					p.hide();
					
4. Example: Profile page in Twitter
	1. Rotating spinners
		1. JS might be loading some data
		2. JS hides spinners and displays loaded content when data is available
	2. Modal
		1. JS opens a dialog when we hit the tweet button
		2. JS hides the dialog when we click outside
	3. Display user info
		1. JS shows user info if we hover on any user
	4. Anything that is required can be loaded on the fly
5. Recap:
	1. Add dynamic effects to pages & entire web applications in browser
	2. React/Angular/View - tools that make writing modern, large scale web applications easier
		1. They are based on JS
			1. **We need to be really good at JS before jumping into any framework** (not just after writing 10 lines of JS)
	3. JS and Web browser are two different things
		1. JS can be used on web-server - Node.js
			1. Backend applications
				1. Applications that run on web-servers and interact with databases etc.
	4. What we will learn
		1. Ins and outs of JS
		2. How to use JS in web-browser (front-end web applications)
		3. Node.js
	5. We can use JS to build:
		1. Native mobile applications
			1. React Native
			2. Ionic
		2. Native desktop applications
			1. Electron
6. JS releases/versions:
	1. ES5
	2. ES6/ES2015
		1. Biggest update to the language ever
	3. ES7/ES2016
	4. ES8/ES2017
	5. ES9/ES2018
	6. ES10/ES2019
	7. ES11/ES2020
	8. (New update to JS every single year)
		1. The course will cover modern JS

### Linking a JavaScript File ###
1. How to write JS in a file and run the code
	1. Download starter code from repo
		1. Code > Download ZIP
			1. If not visible:
				1. FAQ: this link
			2. Extract:
				1. Starter code
					1. Each folder
						1. final - final version of the code
						2. starter - project folder
			3. Open project folder in VS Code (starter)
				1. index.html
				
						<script>
							let js = 'amazing'; // not mandatory
							if (js === 'amazing') {
								alert('Javascript is FUN!');
							}
						</script>
						
				2. Open the file in Google chrome
					1. Shows an alert
			4. How to see results of our code in browser
			
					<script>
					
						40 + 8 + 23 - 10;
					</script>
					
				1. Open inspector
					1. Console
						1. Result is not in the console
							1. It is a REPL
								1. It doesn't show results of code
						2. Solution:
						
								console.log(40 + 8 + 23 - 10);

### Values and Variables ###
### Practice Assignments ###
### Data Types ###
### let, const, and var ###
### Basic Operators ###
### Operator Precedence ###
### A Note About Challenges ###
### Coding Exercise 1: CHALLENGE #1 ###
### CHALLENGE #1: Video Solution ###
### Strings and Template Literals ###
### Taking Decisions: if/else Statements ###
### Coding Exercise 2: CHALLENGE #2 ###
### CHALLENGE #2: Video Solution ###
### Type Conversion and Coercion ###
### Truthy and Falsy Values ###
### Equality Operators: == vs === ###
### Boolean Logic ###
### Logical Operators ###
### Coding Exercise 3: CHALLENGE #3 ###
### The switch Statement ###
### Statements and Expressions ###
### The Conditional (Ternary) Operator ###
### Coding Exercise 4: CHALLENGE #4 ###
### CHALLENGE #4: Video Solution ###
### JavaScript Releases: ES5, ES6+ and ESNext ###

## Section 4: JavaScript Fundamentals - Part 2 ##
### Section Info ###
### Activating String Mode ###
### Functions ###
### Function Declarations vs. Expressions ###
### Arrow Functions ###
### Functions Calling Other Functions ###
### Reviewing Functions ###
### Coding Exercise 5: CHALLENGE #1 ###
### CHALLENGE #1: Video Solution ###
### Introduction to Arrays ###
### Basic Array Operations (Methods) ###
### Coding Exercise 6: CHALLENGE #2 ###
### CHALLENGE #2: Video Solution ###
### Introduction to Objects ###
### Dot vs. Bracket Notation ###
### Object Methods ###
### Coding Exercise 7: CHALLENGE #3 ###
### CHALLENGE #3: Video Solution ###
### Iteration: The for Loop ###
### Looping Arrays, Breaking and Continuing ###
### Looping Backwards and Loops in Loops ###
### The while Loop ###
### Coding Exercise 8: CHALLENGE #4 ###
### CHALLENGE #4: Video Solution ###

## Section 4: How to Navigate This Course ##
### Pathways and Section Roadmaps ###
### Course Pathways ###

## Section 5: Developer Skills & Editor Setup ##
### Section Intro ###
### Section Roadmap ###
### Setting up Prettier and VS Code ###
### Installing Node.js and Setting Up a Dev Environment ###
### Learning How to Code ###
### How to Think Like a Developer: Become a Problem Solver! ###
### Using Google, StackOverflow and MDN ###
### Debugging (Fixing Errors) ###
### Debugging with the Console and Breakpoints ###
### Coding Challenge #1 ###

## Section 6: [OPTIONAL] HTML & CSS Crash Course ##
### Section Info ###
### Basic HTML Structure and Elements ###
### Attributes, Classes and IDs ###
### Basic Styling with CSS ###
### Introduction to the CSS Box Model ###

## Section 7: JavaScript in the Browser: DOM and Events Fundamentals ##
### Section Intro ###
### Section Roadmap ###
### PROJECT #1: Guess My Number! ###
### What's the DOM and DOM Manipulation ###
### Selecting and Manipulating Elements ###
### Handling Click Events ###
### Implementing the Game Logic ###
### Manipulating CSS Styles ###
### Coding Challenge #1 ###
### Implementing Highscores ###
### Refactoring Our Code: The DRY Principle ###
### PROJECT #2: Modal Window ###
### Working With Classes ###
### Handling an "Esc" Keypress Event ###
### PROJECT #3: Pig Game ###
### Rolling the Dice ###
### Switching the Active Player ###
### Holding Current Score ###
### Resetting the Game ###

## Section 8: How JavaScript Works Behind the Scenes ##
### Section Intro ###
### Section Roadmap ###
### An High-Level Overview of JavaScript ###
### The JavaScript Engine and Runtime ###
### Execution Contexts and The Call Stack ###
### Scope and The Scope Chain ###
### Scoping in Practice ###
### Variable Environment: Hoisting and the TDZ ###
### Hoisting and TDZ in Practice ###
### The this Keyword ###
### The this Keyword in Practice ###
### Regular Functions vs. Arrow Functions ###
### Primitives vs. Objects (Primitive vs. Reference Types) ###
### Primitives vs. Objects in Practice ###

## Section 9: Data Structures, Modern Operators and Strings ##
### Section Info ###
### Section Roadmap ###
### Destructuring Arrays ###
### Destructuring Objects ###
### The Spread Operator (...) ###
### Rest Pattern and Parameters ###
### Short Circuiting (&& and ||) ###
### The Nullish Coalescing Operator (??) ###
### Logical Assignment Operators ###
### Coding Challenge #1 ###
### Looping Arrays: The for-of Loop ###
### Enhanced Object Literals ###
### Optional Chaining (?.) ###
### Looping Objects: Object Keys, Values, and Entries ###
### Coding Challenge #2 ###
### Sets ###
### Maps: Fundaments ###
### Maps: Iteration ###
### Summary: Which Data Structure to Use? ###
### Coding Challenge #3 ###
### Working with Strings - Part 1 ###
### Working with Strings - Part 2 ###
### Working with Strings - Part 3 ###
### Coding Challenge #4 ###
### String Methods Practice ###

## Section 10: A Closer Look at Functions ##
### Section Intro ###
### Section Roadmap ###
### Default Parameters ###
### How Passing Arguments Works: Value vs. Reference ###
### First-Class and Higher-Order Functions ###
### Functions Accepting Callback Functions ###
### Functions Returning Functions ###
### The call and apply Methods ###
### The bind Method ###
### Coding Challenge #1 ###
### Immediately Invoked Function Expression (IIFE) ###
### Closures ###
### More Closure Examples ###
### Coding Challenge #2 ###

## Section 11: Working with Arrays ##
### Section Intro ###
### Section Roadmap ###
### Simple Array Methods ###
### The new at Method ###
### Looping Arrays: forEach ###
### forEach with Maps and Sets ###
### PROJECT: "Bankist" App ###
### Constructing DOM Elements ###
### Coding Challenge #1 ###
### Data Transformations: map, filter, reduce ###
### The map Method ###
### Computing Usernames ###
### The filter Method ###
### The reduce Method ###
### Coding Challenge #2 ###
### The Magic of Chaining Methods ###
### Coding Challenge #3 ###
### The find Method ###
### Implementing Login ###
### Implementing Transfers ###
### The findIndex Method ###
### some and every ###
### flat and flatMap ###
### Sorting Arrays ###
### More Ways of Constructing and Filling Arrays ###
### Summary: Which Array Method to Use? ###
### Array Methods Practice ###
### Coding Challenge #4 ###

## Section 12: Numbers, Dates, Intl and Timers ##
### Section Intro ###
### Section Roadmap ###
### Converting and Checking Numbers ###
### Math and Rounding ###
### The Remainder Operator ###
### Numeric Separators ###
### Working with BigInt ###
### Constructing Dates ###
### Adding Dates to "Bankist" App ###
### Operations With Dates ###
### Internationalizing Dates (Intl) ###
### Internationalizing Numbers (Intl) ###
### Timers: setTimeout and setInterval ###
### Implementing a Countdown Timer ###

## Section 13: Advanced DOM and Events ##
### Section Intro ###
### Section Roadmap ###
### PROJECT: "Bankist" Website ###
### How the DOM Really Works ###
### Selecting, Creating, and Deleting Elements ###
### Styles, Attributes and Classes ###
### Implementing Smooth Scrolling ###
### Types of Events and Event Handlers ###
### Event Propagation: Bubbling and Capturing ###
### Event Propagation in Practice ###
### Event Delegation: Implementing Page Navigation ###
### DOM Traversing ###
### Building a Tabbed Component ###
### Passing Arguments to Event Handlers ###
### Implementing a Sticky Navigation: The Scroll Event ###
### A Better Way: The Intersection Observer API ###
### Revealing Elements on Scroll ###
### Lazy Loading Images ###
### Building a Slider Component: Part 1 ###
### Building a Slider Component: Part 2 ###
### Lifecycle DOM Events ###
### Efficient Script Loading: defer and async ###

## Section 14: Object-Oriented Programming (OOP) with JavaScript ##
### Section Intro ###
### Section Roadmap ###
### What is Object-Oriented Programming? ###
### OOP in JavaScript ###
### Constructor Functions and the new Operator ###
### Prototypes ###
### Prototypal Inheritance and the Protoype Chain ###
### Prototypal Inheritance on Built-in Objects ###
### Coding Challenge #1 ###
### ES6 Classes ###
### Setters and Getters ###
### Static Methods ###
### Object.create ###
### Coding Challenge #2 ###
### Inheritance Between "Classes": Constructor Functions ###
### Coding Challenge #3 ###
### Inheritance Between "Classes": ES6 Classes ###
### Inheritance Between "Classes": Object.create ###
### Another Class Example ###
### Encapsulation: Protected Properties and Methods ###
### Encapsulation: Private Class Fields and Methods ###
### Chaining Methods ###
### ES6 Classes Summary ###
### Coding Challenge #4 ###

## Section 15: Mapty App: OOP, Geolocation, External Libraries, and More! ##
### Section Intro ###
### Section Roadmap ###
### Project Overview ###
### How to Plan a Web Project ###
### Using the Geolocation API ###
### Displaying a Map Using Leaflet Library ###
### Displaying a Map Marker ###
### Rendering Workout Input Form ###
### Project Architecture ###
### Refactoring for Project Architecture ###
### Managing Workout Data: Constructing Classes ###
### Constructing a New Workout ###
### Rendering Workouts ###
### Move to Marker On Click ###
### Working with localStorage ###
### Final Considerations ###

## Section 16: Asynchronous JavaScript: Promises, Async/Await, and AJAX ##
### Section Info ###
### Section Roadmap ###
### Asynchronous JavaScript, AJAX and APIs ###
### IMPORTANT: API URL Change ###
### Our First AJAX Call: XMLHttpRequest ###
### [OPTIONAL] How the Web Works: Requests and Responses ###
### Welcome to Callback Hell ###
### Promises and the Fetch API ###
### Consuming Promises ###
### Chaining Promises ###
### Handling Rejected Promises ###
### Throwing Errors Manually ###
### Coding Challenge #1 ###
### Asynchronous Behind the Scenes: The Event Loop ###
### The Event Loop in Practice ###
### Building a Simple Promise ###
### Promisifying the Geolocation API ###
### Coding Challenge #2 ###
### Consuming Promises with Async/Await ###
### Error Handling With try...catch ###
### Returning Values from Async Functions ###
### Running Promises in Prallel ###
### Other Promise Combinators: race, allSettled and any ###
### Coding Challenge #3 ###

## Section 17: Modern JavaScript Development: Modules, Tooling, and Functional ##
### Section Intro ###
### Section Roadmap ###
### An Overview of Modern JavaScript Development ###
### An Overview of Modules in JavaScript ###
### Exporting and Importing in ES6 Modules ###
### Top-Level await (ES2022) ###
### The Module Pattern ###
### CommonJS Modules ###
### A Brief Introduction to the Command Line ###
### Introduction to NPM ###
### Bundling with Parcel and NPM Scripts ###
### Configuring Babel and Polyfilling ###
### Review: Writing Clean and Modern JavaScript ###
### Let's Fix Some Bad Code: Part 1 ###
### Declarative and Functional JavaScript Principles ###
### Let's Fix Some Bad Code: Part 2 ###

## Section 18: Forkify App: Building a Modern Application ##
### Section Into ###
### Section Roadmap ###
### Project Overview and Planning (I) ###
### Latest Code Updates (Parcel v2 and more) ###
### Loading a Recipe from API ###
### Rendering the Recipe ###
### Listening for load and hashchange Events ###
### The MVC Architecture ###
### Refactoring for MVC ###
### Helpers and Configuration Files ###
### Event Handlers in MVC: Publisher-Subscriber Pattern ###
### Implementing Error and Success Messages ###
### Implementing Search Results - Part 1 ###
### Implementing Search Results - Part 2 ###
### Implementing Pagination - Part 1 ###
### Implementing Pagination - Part 2 ###
### Project Planning II ###
### Updating Recipe Servings ###
### Developing a DOM Updating Algorithm ###
### Implementing Bookmarks - Part 1 ###
### Implementing Bookmarks - Part 2 ###
### Storing Bookmarks with localStorage ###
### Project Planning III ###
### Uploading a New Recipe - Part 1 ###
### Uploading a New Recipe - Part 2 ###
### Uploading a New Recipe - Part 3 ###
### Wrapping Up: Final Considerations ###

## Section 19: Setting Up Git and Deployment ##
### Section Intro ###
### Section Roadmap ###
### Simple Deployment with Netlify ###
### Setting up Git and GitHub ###
### Git Fundamentals ###
### Pushing to GitHub ###
### Setting up Continuous Integration with Netlify ###

## Section 20: The End! ##
### Where to Go from Here ###
### My Other Courses + Updates ###

## Section 21: [LEGACY] Access the Old Course ##
### Access the Old Course ###