# Advanced React Testing: Redux Saga and React Router #
## Section 1: Introduction ##
### Welcome and Introduction ###
1. Testing:
	1. Redux Saga
	2. Ract Router
	3. Auth-Protected Routes
2. Introduction
	1. For people who know the basics of testing
		1. Want to see more complicated cases
	2. Course covers
		1. Redux Saga
		2. React Router
			1. Push history routes testing
			2. URL parameters
			3. Query parameters
		3. Auth-Protected Routes
	3. Uses Redux Tookit
		1. Applicable to Redux
		2. No testing of action creators or reducers
			1. Not directly tested
3. Course Roadmap
	1. Introduction
	2. Redux Saga
	3. React Router
	4. Auth-Protected Routes
4. Prerequisites
	1. Jest basics (how to write tests)
	2. Testing Library basics (`render` and `screen`)
	3. React Hooks (built-in and custom)
	4. Redux and Redux Saga usage (Saga section only)
	5. React Router usage (React Router and Auth sections only)
5. Course will not cover...
	1. Basic testing
		1. Skip lots of tests not relevant to the course
		2. App will not be completely tested by the end of the course!
	3. TDD (Test-Driven Development)
		1. All code to be tested is already written
		2. Focus course time on testing, not writing code

### Popular Music Venue app ###
1. App for a music venue ("Popular Music Venue")
2. See info about shows, bands
3. Purchase tickets
	1. But only if logged in!
4. Repository
	1. [https://github.com/bonnie/udemy-ADVANCED-REACT-TESTING](https://github.com/bonnie/udemy-ADVANCED-REACT-TESTING)
		1. `base-app` - no tests
		2. `lecture-files` - code from optional lectures
		3. `saga-flow-charts` - flow charts
		4. `tested-app` - with tests
	2. Start server
	
	```bash
	cd base-app/server
	npm i
	mv .env_tempalte .env
	# enter a secret
	npm start
	```
	
	3. Start client
	
	```bash
	npm install --save-dev react-scripts@latest webpack@latest
	npm start
	```

5. Server Technology
	1. Express server
	2. Auth done via JWT
	3. Provides dat afor shows and bands
		1. Records ticket purchases
	4. Not testing server at all!
		1. Mock Service Worker for server responses in tests
6. Client technology
	1. Create React App
	2. TypeScript
	3. Redux Toolkit
	4. Redux Saga (complicated actions, sign-in)
	5. React Router
	6. Chakra UI (Styling)
	7. Jest
	8. Testing Library

### Notes on ESLint and Prettier Formatting ###
1. [ESLint configuration](https://github.com/bonnie/udemy-REACT-QUERY/blob/dffb7dc8108c2c28e3064781955f8ed2f37682f6/base-lazy-days/client/.eslintrc.json)
2. [Prettier configuration](https://github.com/bonnie/udemy-REACT-QUERY/blob/dffb7dc8108c2c28e3064781955f8ed2f37682f6/base-lazy-days/client/.prettierrc.json)
3. [VS Code settings to auto-format on save](https://github.com/bonnie/udemy-REACT-QUERY/blob/dffb7dc8108c2c28e3064781955f8ed2f37682f6/base-lazy-days/client/.vscode/settings.json)
4. Install ESLint and Prettier extensions
	1. Must not generate any errors in the output window
	2. To auto-fix
	
	```bash
	eslint --fix src/ --ext ".jsx,.js,.ts,.tsx"
	```
	
	3. To fix line-ending errors
	
	```bash
	./node_modules/.bin/prettier --write "src/**/*.{js,jsx,tx,txs,json,css,scss,md}"
	```
	
	4. Run Global git settings:
	
	```bash
	git config --global core.autocrlf true
	```
	
		1. Pull the code from Github again
		
	5. Update prettier/prettier rule in .eslintrc.json
	
	```json
	"prettier/prettier": [
	  "error",
	  {
		"endOfLine": "auto"
	  }
	],
	```
	
	6. Set line endings in .vscode/settings.json
	
	```json
	{
		"files.eol": "\n",
	}
	```

### How to Get Help ###
### Choice Point! Redux Saga or React Router? ###
1. Course Roadmap:
	1. Introduction
	2. Redux Saga
	3. Reac tRouter (Custom Render)
	4. Auth-Protected Routes

## Section 2: Using redux-saga-test-plan ##
### Introduction to Testing Redux Sagas ###
1. Testing Redux Saga
	1. Intro and `TakeEvery`
2. Testing Implementation Details
	1. Testing Sagas is testing implementation details
		1. Not testing app the way a user would
		2. Testing code, not app behavior
	2. Good idea for complicated sagas
		1. redux-saga is known from testability
		2. Testing implementation tradeoffs:
			1. Diagnosis is easier; test maintenance is harder
				1. Needs updating tests if implementation changes, but not the behavior.
		3. Help diagnose behavior-based ("functional") tests
			1. If tests fail, we can tell if it was because of the sagas
	3. The tests are not for behavioral testing purists
3. Three Saga Sections:
	1. This section: Intro to redux-saga-test-plan syntax
	2. Next section: complex `ticketFlow` saga
		1. Holding tickets
		2. Canceling or expiring
		3. Controlled by `takeEvery`
	3. Last section: `signInFlow` saga with fork
		1. Controlled by infinite `while` loop

### Introduction to redux-saga-test-plan ###
1. 

### Introduction to logErrorToast Saga ###
### First Saga Test ###
### Code Quiz! Non-Error Toast ###
### Partial Assertions ###
### Review: redux-saga-test-plan Introduction ###
sdxxfx
## Section 3: Testing Complex Saga that Uses `takeEvery` ##
### Introduction to ticketFlow Saga ###
### Set up ticketFlow Saga Test File ###
### Error from not Returning `expectSaga` ###
### Mocking with `.provide()` method ###
### Dispatching Actions with `.dispatch()` method ###
### `throwError()` Method to Test Error Paths ###
### Code Quiz! Assertions ###
### Abstracting cancelTransaction Saga Tests and Network Providers ###
### Code Quiz! Purchase Error ###
### Asserting on Axios Cancel Call ###
### Testing Race Effect ###
### OPTIONAL Code Quiz! Successful Purchase ###
### OPTIONAL Code Quiz! Hold Cancel ###
### Parameterization with `test.each()` ###
### Review: Complex takeEvery Saga Tests ###

## Section 4: Testing Saga with Fork and Cancel Effects in Infinite while Loop ##
### Introduction to Sign in Sagas ###
### Set Up signInSaga Test File ###
### Testing Successful Sign-in: .silentRun and Timeout ###
### Return Value from Network Provider ###
### Code Quiz! Sign Up Flow ###
### Integration Test for Canceled Fork ###
### Code Quiz! Error Path ###
### Introduction to redux-saga-test-plan Unit Tests ###
### Cancel Flow Unit Test ###
### Code Quiz! Unit Tests ###
### Review: Fork, Cancel, Infinite while Loop ###
### Getting Help with Saga Tests ###

## Section 5: Testing Library Custom render: Redux and React Router ##
### -----> Start here for React Router! ###
### Why is Custom render Necessary? ###
### Custom render Concepts ###
### Planning Custom render with Test Store ###
### Writing Custom render with Test Store ###
### Using Custom render in Tests ###
### Adding React Router to Custom render ###
### Asserting on history Object ###
### OPTIONAL Behavior Testing for Redirect ###
### Code Quiz! history.push() ###
### OPTIONAL: Redux State Code Quiz ###
### Custom router Summary ###

## Section 6: Testing Routes with URL and Query Params ##
### Introduction to Testing Routes with URL and Query Params ###
### OPTIONAL Introduction to Mock Service Worker ###
### OPTIONAL Setting up Mock Service Worker ###
### OPTIONAL Testing "Shows" Component with Mock Service Worker ###
### OPTIONAL Code Quiz! Mock Service Worker for Sold-Out Show ###
### Testing a Route with URL Params ###
### Writing Handler for Route with URL Params ###
### Testing Page Contents for Route with URL Params ###
### Code Quiz! Page Contents of Route with URL Params ###
### Redirecting to Route with URL Params ###
### Redirecting to Route with URL and Query Params ###
### Code Quiz! Bad Query Params ###
### Review: Routes with URL and Query Params ###

## Section 7: Testing Auth-Protected Routes ##
### Into to Testing Auth-Protected Routes ###
### Test for Non-Protected Route ###
### OPTIONAL: Introduction to Parameterization with test.each() ###
### Parameterizing Non-Protected Page Tests with test.each() ###
### Planning Protected Route Tests ###
### Code Quiz! Redirect to Sign-In for Protected ###
### Parameterizing Sign-In Redirect ###
### SignIn/SignUp Handlers for Mock Service Worker ###
### Planning Tests for Protected Route Redirect after Sign-In ###
### Starting Test for Protected Route Redirect after Sign In ###
### Getting error when you run `waitFor`? ###
### Completing Test for Protected Route Redirect after Sign In ###
### Code Quiz! Successful Sign-Up ###
### Testing Failed SignIn Followed by Successful SignIn ###
### Code Quiz! Server Error on Sign In ###
### Code Quiz! Parameterizing Unsuccessful Sign In/ Sign Up ###
### Review: Auth-Protected Routes ###
### Congratulations and Thank You! ###

## Section 8: Further Learning ##
### Bonus Lecture ###