# The Complete React Native + Hooks Course #
## Section 1: Getting Started ##
1. How to get help
	1. Udemy QA Discussion boards
	2. Message me on Udemy
	3. Twitter - @ste_grider
	4. Google!

### How to Get Help ###
### Course Resources ###
### Join Our Community! ###
1. [https://discord.gg/vvcyvjDkdC](https://discord.gg/vvcyvjDkdC)

### Course Overview ###
1. Overview:
	1. There's a lot of stuff to learn with React Native
	2. Normally, I love showing development of full apps
	3. Instead, we will be building a ton of little mini-apps
		1. Can refer back to
		2. Tells how to do a particular thing
	4. We are still going to make big apps! But later on in the course
2. Local environment setup:
	1. Test on a physical device
		1. By far, easiest to setup
	2. Test on a fake device (simulator, emulator)
		1. Changes to code show up faster
			1. More involved setup though

### Installing Node.js and Prerequisite Info ###
1. [https://nodejs.org/en/download/](https://nodejs.org/en/download/)
2. [https://www.youtube.com/watch?v=S320N3sxinE](https://www.youtube.com/watch?v=S320N3sxinE)
3. [https://www.youtube.com/watch?v=WPqXP_kLzpo](https://www.youtube.com/watch?v=WPqXP_kLzpo)

### Boilerplate Download and Startup ###
1. [Github repository](https://github.com/0x-cygnet/rn-starter.git)
	1. Or: `git clone https://github.com/0x-cygnet/rn-starter.git`
2. Windows users should use PowerShell to run their application
	1. WSL terminal: Advanced users
3. Git Bash does not work with Expo	and will not display the QR code or options

### App Setup ###
1. Physical Device Setup
	1. Download the 'rn-starter.zip' file in the lecture before this one. Extract into a workspace directory
	2. In terminal, change into the 'rn-starter' folder that was just created
	3. In terminal, run `npm install --legacy-peer-deps`
	4. After installing, run `npm start`
		1. Opens the React Native bundler, which gest code ready to be run on a mobile device
	5. Install the `expo` app in mobile device form the App Store or Google Play Store
	6. Scan the QR code from the React Native Bundler on phone
2. Stopping and Restarting:
	1. To stop the RN bundler, press 'control c' in the terminal window running the bundler
	2. To start it back up, run `npm start` in the project directory again, then scan the QR code on your mobile device

### Making Changes ###
1. Open project in VS Code
	1. src/screens/HomeScreen.js
		1. Change text to `Hi There!`
			1. Change appears right away
2. If we see an error message, 

### Expo for Web Browser - Do Not Skip ###
### Using iOS and Android Simulators ###

## Section 2: Working with Content ##
### Overview of React Components ###
### Showing a Custom Component ###
### Common Questions and Answers ###
### Rules of JSX ###
### One Common Error ###
### JSX Exercise Overview ###
### JXS Solution ###

## Section 3: List Building - With Style! ##
### Building Lists ###
### The FlatList Element ###
### Rendering a FlatList ###
### Why a Key Property? ###
### Solving the Key Issue ###
### A Few Props Around FlatList ###
### Exercise Overview ###
### Exercise Solution ###

## Section 4: Navigating Users Between Screens ##
### Button Types ###
### Buttons in Action ###
### Touchable Opacity in Action ###
### Navigating with React Navigation ###
### Destructuring Props ###

## Section 5: Building Reusable Components ##
### Component Reuse with Props ###
### Exercise Solution ###
### Parent-Child Relationships ###
### Communicating from Parent to Child ###
### Images Download ###
### Showing Images ###
### Passing Images as Props ###
### Exercise Outline ###
### Exercise Solution ###

## Section 6: State Management in React Components ##
### State in Components ###
### Screen Boilerplate ###
### State in Action ###
### Notes on State ###
### App Overview ###
### Generating Random Colors ###
### Adding Random Colors ###
### Showing Colors with a FlatList ###
### App Overview ###
### Reusable Color Adjusters ###
### Coordinating State ###
### Passing Callbacks to Children ###
### Tying State Values Together ###
### Validating State Changes ###
### Reusable State Updates ###
### Introduction to Reducers ###
### Constructing a Reducer ###
### Applying State with a Reducer ###
### Restoring Validation ###
### Community Convention in Reducers ###
### Exercise Outline ###
### Exercise Solution ###
### Handling Text Input ###
### Showing a Text Input ###
### Two Important Props ###
### Weird Things with Text and State ###
### Updating State ###
### Exercise Outline ###
### Exercise Solution ###

## Section 7: How to Handle Screen Layout ##
### Layout with React native ###
### Basics of Box Object Model ###
### AlignItems with Flex ###
### Flex Direction ###
### Justify Content ###
### Flex Values ###
### Align Self on Children ###
### The Position Property ###
### Top, Bottom, Left, Right ###
### Absolute Fill Objects ###
### Applying Layout Systems ###
### Exercise Overview ###
### Exercise Solution ###

## Section 8: Putting It All Together - Restaurant Search App ##
### App Overview ###
### Important Note About Project Generation ###
### Project Generation ###
### Yelp API Workarounds ###
### Yelp Signup ###
### React Navigation ###
### Required React Navigation Installation Update ###
### Assembling a Navigator ###
### Architecture Approach ###
### Starting the SearchBar ###
### Displaying Icons ###
### Search Bar Styling ###
### A Touch More Styling ###
### Managing State ###
### Detecting Editing Completion ###

## Section 9: Using Outside API's ##
### Configuring Axios ###
### Making the Request ###
### Error Handling ###
### Running an Initial Search ###

## Section 10: Making Hooks Reusable ##
### Incorrect Hook Name in Slide ###
### The UseEffect Hook ###
### Extracting Hook Logic ###
### Showing Search Results ###
### Grouping Results ###
### FlatList Rendering ###

## Section 11: Navigation with Parameters ##
### Showing a Single Result ###
### Showing Additional Info ###
### A Few More Styling Issues ###
### Hiding Scroll Bars ###
### Constraining View Elements ###
### Empty Elements ###
### Spacing on the Search Bar ###
### Reminder on Navigation ###
### Navigating from a Child Component ###
### The WithNavigation Helper ###
### Communicating Between Screens ###
### Fetching a Single Restaurant ###
### Showing a List of Images ###
### One Last Fix ###
### Upgrading the Restaurant App to Use React Navigation v6 ###

## Section 12: Advanced State Management with Context ##
### Important Note About Project Generation ###
### App Overview ###
### Issues with Data ###
### Required React Navigation Installation Update ###
### Initial Setup ###
### Wrapping the Navigator ###
### Introduction to Context ###
### Adding Context ###
### Moving Data with Context ###
### Rendering a List of Posts ###
### Adding State in Context ###
### It Works! ###
### Opportunity for Improvement ###
### Updating with UseReducer ###
### Automating Context Creation ###
### More Automatic Context Creation ###
### A Bit of Styling ###
### Deleting Posts ###
### Updating the Reducer ###
### Navigation on Tap ###
### Retrieving Single Posts ###
### Adding a Creation Screen ###
### headerRight Deprecation in 'navigationOptions' ###
### Header Navigation ###
### Displaying a Form ###
### Saving a New Post ###
### Navigation on Save ###
### headerRight Deprecation in 'navigationOptions' ###
### The Edit Icon Link ###
### Communicating Info to Edit ###
### Initializing State from Context ###
### Extracting form Logic ###
### Customizing OnSubmit ###
### Initial Form Values ###
### Default Props ###
### Editing Action Function ###
### Editing in a Reducer ###
### Navigating Backwards ###

## Section 13: Data API Sync ##
### Outside Data API ###
### Issues with Servers + React Native ###
### Important - Required Ngrok Setup Steps ###
### JSON Server and Ngrok Setup ###
### JSON Server REST Conventions ###
### Making a Request ###
### Remote Fetch of Posts ###
### Constructing Posts with Post Requests ###
### Refetching on Navigate ###
### Deleting a Post ###
### Editing Posts ###
### App Wrapup ###
### Upgrading the Blog App to Use React Navigation v6 ###

## Section 14: Building a Custom Express API ##
### App Overview ###
### Dependencies Setup ###
### The Basics of Express ###
### MongoDB Setup ###
### Connecting to MongoDB ###
### Nodemon for Automatic Restarts ###
### Understanding the Signup Process ###
### Using Postman ###
### Handling JSON Data ###
### Defining a User Schema ###
### Constructing and Saving a User ###
### Error Handling ###
### JSON Web Tokens ###
### Constructing a JWT ###
### Wiring Up JSON Web Tokens ###
### Understanding Password Hashing ###
### Salting and Hashing ###
### The Signin Route ###
### Testing Signup and Signin ###
### Defining Tracks ###
### Listing Tracks ###
### Constructing Tracks ###

## Section 15: In-App Authentication ##
### Server Code ###
### Server Setup ###
### Important Note About Project Generation ###
### Navigation Design ###
### Required React Navigation Installation Update ###
### A LOT of Boilerplate ###
### Navigator Hookup ###
### Testing the Navigation Flow ###
### React Native Elements ###
### Helper Styling Components ###
### navigationOptions Deprecation Warning ###
### Styling Odds and Ends ###
### Input Props ###
### The Auth Context ###
### What's the Context Doing? ###
### Axios Setup ###
### Making an API Request ###
### Handling Errored Requests ###
### Async Storage ###
### Async Storage Update ###
### Storing the Token ###
### Navigation From Outside of React ###
### Ooops, Typo ###
### Navigation to Signin ###
### Extracting Form Logic ###
### Last Bit of Extracting ###
### Constructing a NavLink ###
### navigationOptions Deprecation ###
### React Component Reuse! ###
### Wiring Up Signin ###
### onWillFocus vs onWillBlur Update ###
### Clearing Error Messages ###
### Automatic Signin ###
### Empty Screens While Resolving Auth ###
### Signing Out a User ###
### Safe Area Views ###
### Working on Track Create ###
### Installing React Native Maps ###
### Showing a Map ###
### Drawing a Series of Points ###
### Notes on Location ###
### Fix for Missing Location Request Error ###
### "requestPermissniosAsync" is Now Deprecated in Expo SDK 41+ ###
### Requesting Location Permissions ###
### Resetting Permissions ###
### How to Test Location? ###
### Faking the Users Location ###
### Reading a Location ###
### Bugginess with Location ###
### Location Architecture ###
### Location Context ###
### Live Location Updates ###
### Fix for Indicator not Tracking Map ###
### Drawing a Position Indicator ###
### Extracting Logic to a Hook ###
### Disabling Location Tracking ###
### Automatic Disables ###
### Building a Track Form ###
### Updates to Location Context ###
### Track Form Wire Up ###
### Buggy UseEffects ###
### Understanding Stale References ###
### Some Errors You May See ###
### Kind of Fixed ###
### The UseCallack Hook ###
### Cleaning Up After Ourselves ###
### Avoiding Stale References ###
### Tracking While Recording ###
### Bring Back the Polyline ###
### What Manages Tracks ###
### Coordination Between Contexts ###
### Async Storage Update ###
### Automatic Authentication ###
### Form Reset and Navigation ###
### Fetching Created Tracks ###
### ListItem Update ###
### Listing All Tracks ###
### Navigating to a Saved Track ###
### Showing Track Details ###
### Fixing Odds and Ends ###

## Section 16: Important - OLD VERSION OF COURSE - Do Not Skip ##
### Note on the Following Section ###

## Section 18: Extras ##
### Bonus! ###