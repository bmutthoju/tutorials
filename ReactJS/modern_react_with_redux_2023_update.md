# Modern React with Redux [2023 Update] #
## Section 1: Let's Dive In! ##
### How to Get Help ###
1. Udemy QA
	1. Start from here
2. Twitter: @ste_grider
3. Email: ste.grider@gmail.com
4. Monday to Friday around 9 AM PST

### Join Our Community! ###
1. Discord community of fellow students, developers, and engineers
2. Latest news and announcements
3. Start a discussion
3. [Discord link](https://discord.gg/vvcyvjDkdC)

### Course Resources ###
1. Finished Code
	1. Attached to each applicable lecture throughout the course
	2. Use Diffchecker or VSCode's built-in comparison tool to compare codes
2. Diagrams
	1. Diagrams are attached to the lecture note
		1. Download and extract
		2. Visit [diagrams.net (formerly draw.io)](https://www.diagrams.net/)
		3. Select **Open Existing Diagram** and use the file explorer to select the diagram file from computer
		4. OR
		5. Click on **File** from diagrams.net menu
		6. Select **Open From Device** and use file explorer to select diagram file from computer
3. Envronment
	1. VS Code: [https://code.visualstudio.com/](https://code.visualstudio.com/)
	2. Autoformat: [https://prettier.io/](https://prettier.io/)
	3. Terminal:
		1. Iterm2: [https://www.iterm2.com/](https://www.iterm2.com/)
		2. Run the shell: [https://github.com/robbyrussell/oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) with default theme 'Robby Russell'

### Let's Build an App! ###
1. Best way to learn React fast?
	1. Write code!
	2. Work on projects!
2. We are going to build an entire language translation app in the video
	1. Challenging over time
3. Small react app:
	1. It translates some English text into another language
		1. Text input
		2. Select a language
		3. Output
4. [codesandbox.io/s/react-pibc94](codesandbox.io/s/react-pibc94)
	1. Online editor with a few files already created for me
		1. All other projects will be created on my computer from scratch
	2. Copy and paste the URL in browser window
5. Got stuck?
	1. [codesandbox.io/s/react-forked-m5bz37](codesandbox.io/s/react-forked-m5bz37)
6. Code editor:
	1. We can change the text to: Here is a react app!
7. Code:

		import './styles.css';
		...

		export default function App() {
			const [langauge, setLanguage] = useState('es');
			const [text, setText] = useState('');
			
			return (
				<div>
					<Field onChange={setText} />
					<Languages language={language} onLanguageChange={setLanguage} />
					<hr />
					<Translate text={text} language={language} />
				</div>
			);
		}
	
### Critical Questions ###[
1. Critical questions:
	1. So what's React all about?
		1. React (It is like a wrapper around HTML)
			1. Displays HTML
			2. Changes that HTML when user does something (clicking, typing, dragging, ...)
		2. How do we tell React to show HTML?
			1. We define functions that return JSX
				1. Looks like HTML but a little different
			2. JSX tells about individual elements and show to the user
		3. React components
			1. Are functions that return JSX (stuff that looks like HMTL)
				1. Primary way we work with react library
			2. They tell React what to show on the screen
			3. A project can have many components that work together
				1. Components in translate app:
					1. App.js
						1. Used to coordinate between other components
							1. Shares info between them
					2. languages.js
					3. flower.js
					4. translate.js
					5. field.js
				2. Each component is in-charge of displaying content  for a certain portion of the application
				3. All react components are going to return some JSX
					1. JSX tells React to
						1. To construct a normal HTML element
							1. `<div></div>`
							2. `<button>Click</button>`
							3. `<input type="text" />`
						2. To show another component
							1. `<Field />`
							2. `<Languages />`
							3. `<Translate />`
				4. Example:
					1. App Component
					
							function App() {
								return (
									<div>
										<h1>Your Friends</h1>
										<ContactList />
									</div>
								);
							}
							
					2. ContactList Component
					
							function ContactList() {
								return (
									<ul>
										<li>Samantha</li>
										<li>Alex</li>
									</ul>
								);
							}
							
					3. Flow:
						1. 
					
	2. How does a React app start up?
	3. What were the 'useState' functions?
	4. How did the text get translated to another language?

### A Few More Critical Questions ###
### Node Setup ###
### Constructing a React Project ###
### What is Construct React App? ###

## Section 2: Constructing Content with JSX ##
### Showing Basic Content ###
### What is JSX? ###
### Printing JavaScript Variables in JSX ###
### Shorthand JS Expressions ###
### Exercise Overview ###
### Exercise Solution ###
### Typical Component Layouts ###
### Customizing Elements with Props ###
### Converting HTML to JSX ###
### Applying Styling in JSX ###
### Exercise Solution ###
### Extracting Components ###
### Module Systems Overview ###
### Cheatsheet for JSX ###

## Section 3: Building with Reusable Components ##
### Project Overview ###
### Constructing Core Components ###
### Introducing the Props System ###
### Picturing the Movement of Data ###
### Adding Props ###
### Using Argument Destructuring ###
### Exercise Solution ###
### The React Developer Tools ###
### The Most Common Props Mistake ###
### Images for the App ###
### Including Images ###
### Handling Image Accessibility ###
### Review on How CSS Works ###
### Adding CSS Libraries with NPM ###
### A Big Pile of HTML! ###
### Last Bit of Styling ###

## Section 4: State: How to Change Your App ##
### App Overview ###
### Initial App Setup ###
### Introducing the Event System ###
### Events in Detail ###
### Variations on Event Handlers ###
### Exercise Solution ###
### Introducing the State System ###
### More on State ###
### Understanding the Re-Rendering Process ###
### Why Array Destructuring? ###
### Back to the App ###
### Picking a Random Element ###
### List Building in React ###
### Images for the App ###
### Loading and Showing SVGs ###
### Increasing Image Size ###
### Adding Custom CSS ###
### Finaizing Styling ###
### App Wrapup and Review ###

## Section 5: Using an API with React ##
### App Overview ###
### Project Setup ###
### The Path Forward ###
### Overview of HTTP Requests ###
### Understanding the API ###
### Making an HTTP Request ###
### [Optional] Using Async:Await ###
### Data Fetching Cleanup ###
### Thinking About Data Flow ###
### Child to Parent Communication ###
### Implementing Child to Parent Communication ###
### Handling Form Submission ###
### [Optional] OK But Why? ###
### Exercise Solution ###
### Running the Search ###
### Reminder on Async:Await ###
### Communicating the List of Images Down ###
### Building a List of Images ###
### Handling List Updates ###
### Notes on Keys ###
### Displaying Images ###
### A Touch of Styling ###
### App Wrapup ###

## Section 6: How to Handle Forms ##
### App Overview ###
### Initial Setup ###
### State Location ###
### Reminder on Event Handlers ###
### Extra CSS ###
### Receiving New Titles ###
### Adding Styling ###
### Updating State ###
### Don't Mutate That State! ###
### State Updates - Cheat Sheet ###
### [Optional] Adding Elements to the Start or End ###
### Coding Exercise 6: Adding Elements ###
### [Optional] Exercise Solution ###
### [Optional] Inserting Elements ###
### Coding Exercise 7: Inserting Elements ###
### [Optional] Exercise Solution ###
### [Optional] Removing Elements ###
### Coding Exercise 8: Removing Elements ###
### [Optional] Exercise Solution ###
### [Optional] Modifying Elements ###
### [Super Optional] Why the Special Syntax? ###
### Coding Exercise 9: Modifying Elements ###
### [Optional] Exercise Solution ###
### [Optional] Adding, Changing, or Removing Object Properties ###
### Cheatsheet for State Changes ###
### Adding a Book, For Real! ###
### Generating Random ID's ###
### Displaying the List ###
### Deleting Records ###
### Toggling Form Display ###
### Updating the Title ###
### Closing the Form on Submit ###
### A Better Solution! ###
### Collapsing Two Handlers into One ###
### Adding Images ###

## Section 7: Data Persistence with API Requests ##
### Adding Data Persistence ###
### Server Setup ###
### What Just Happened? ###
### How the API Works ###
### Introducing the REST Client ###
### ECONNREFUSED 127.0.0.1:3001 Errors in VSCode ###
### Using the REST Client ###
### Constructing a New Record ###
### Fetching a List of Records ###
### Introducing useEffect ###
### useEffect in Action ###
### More on useEffect ###
### Updating a Record ###
### Thinking About Updates ###
### Deleting a Record ###

## Section 8: Communication Using the Context System ##
### Introducing Context ###
### Context in Action ###
### Changing Context Values ###
### More on Changing Context ###
### Application vs Component State ###
### Refactoring to Use Context ###
### Refactoring the App ###
### Quick Note ###
### Reminder on Sharing with Context ###
### Props and Context Together ###
### Last Bit of Refactoring ###
### A Small Taste of Reusable Hooks ###

## Section 9: Deeper Dive into Hooks! ##
### Return to useEffect ###
### Quick Note ###
### Understanding the Issue ###
### Applying the Fix ###
### ESLint is Good, but be Careful! ###
### Stable References with useCallback ###
### Fixing Bugs with useCallback ###
### useEffect Cleanup Functions ###
### The Purpose of Cleanup Functions ###

## Section 10: Custom Navigation and Routing Systems ##
### Important Info About the Following Sections and Lectures ###
### Project Overview ###
### Project Setup ###
### Some Button Theory ###
### Underlying Elements ###
### The Children Prop ###
### Props Design ###
### Validating Props with PropTypes ###
### PropTypes in Action ###
### Introducing TailwindCSS ###
### Updated Guidance for Installing and Configuring Tailwind ###
### Installing Tailwind ###
### How to use Tailwind ###
### Review on Styling ###
### The ClassNames Library ###
### Building Some Variations ###
### text-white Overriding Other Colors ###
### Finalizing the Variations ###
### Using Icons in React Projects ###
### Issues with Event Handlers ###
### Passing Props Through ###
### Handling the Special ClassName Case ###
### Exclusive Props with TypeScript Instead of PropTypes ###

## Section 11: Mastering the State Design Process ##
### Project Organization ###
### Refactoring with Organization ###
### Component Overview ###
### Component Setup ###
### Reminder on Building Lists ###
### Quick Note ###
### State Diagram Process Overview ###
### Finding the Expanded Item ###
### Conditional Rendering ###
### Inline Event Handlers ###
### Variation on Event Handlers ###
### Conditional Icon Rendering ###
### Displaying Icons ###
### Adding Styling ###
### Toggling Panel Collapse ###
### Quick Note ###
### [Optional] Delayed State Updates ###
### [Optional] Functional State Updates ###
### Coding Exercise 10: Event Handlers with Lists ###
### Exercise Solution ###

## Section 12: Practicing Props and State Design ##
### Component Overview ###
### Designing the Props ###
### Component Creation ###
### [Optional] More State Design ###
### Finally... Implementation! ###
### Reminder on Event Handlers in Maps ###
### Dropdown as a Controlled Component ###
### Controlled Component Implementation ###
### Existence Check Helper ###
### Community Convention with Props Names ###
### Coding Exercise 11: Form Controllers - Prop Naming Convention ###
### Exercise Solution ###
### Adding Styling ###
### The Panel Component ###
### Constructing the Reusable Panel ###
### A Challenging Extra Feature ###
### Document-Wide Click Handlers ###
### Event Capture and Bubbling ###
### Putting it All Together ###
### Why a Capture Phase Handler? ###
### Reminder on the useEffect Function ###
### Reminder on useEffect Cleanup ###
### Issues with Element References ###
### useRef in Action ###
### Checking Click Location ###

## Section 13: Making Navigation Reusable ##
### Traditional Browser Navigation ###
### Theory of Navigation in React ###
### Extracting the DropdownPage ###
### Answering Critical Questions ###
### The PushState Function ###
### Handling Link Clicks ###
### Handling Back:Forward Buttons ###
### Navigation Context ###
### Listening to Forward and Back Clicks ###
### Programmatic Navigation ###
### A Link Component ###
### A Route Component ###
### Handling Control and Command Keys ###
### Link Styling ###
### Custom Navigation Hook ###
### Adding a Slidebar Component ###
### Highlighting the Active Link ###
### Navigation Wrapup ###

## Section 14: Constructing Portals with ReactDOM ##
### Model Component Overview ###
### Toggling Visibility ###
### At First Glance, Easy! ###
### We're Lucky it Works At All! ###
### Fixing the Modal with Portals ###
### Closing the Modal ###
### Customizing the Modal ###
### Additional Styling ###
### One Small Bug ###
### Modal Wrapup ###

## Section 15: Make a Feature-Full Data Table! ##
### Constructing a Reusable Table ###
### Communicating Data to the Table ###
### Reminder on Table HTML Structure ###
### Building the Rows ###
### Better Styling ###
### Done! But It's Not Reusable ###
### Here's the Idea ###
### Dynamic Table Headers ###
### Rendering Individual Cells ###
### Fixed Cell Values ###
### Nested Maps ###
### Fixing the Color ###
### Adding a Key Function ###

## Section 16: Getting Clever with Data Sorting ##
### Adding Sorting to the Table ###
### Reminder on Sorting in JavaScript ###
### Sorting Strings ###
### Sorting Objects ###
### Object Sort Implementation ###
### Reversing Sort Order ###
### Optional Sorting ###
### A Small Extra Feature ###
### Customizing Header Cells ###
### React Fragments ###
### The Big Reveal ###
### Adding SortableTable ###
### Watching for Header Cell Clicks ###
### Quick State Design ###
### Adding Sort State ###
### Yessssss. It Worked! ###
### Determining Icon Set ###
### Styling Header Cells ###
### Resetting Sort Order ###
### Table Wrapup ###

## Section 17: Custom Hooks in Depth ##
### Exploring Code Reuse ###
### Revisiting Custom Hooks ###
### Constructing the Demo Component ###
### Custom Hook Construction ###
### Quick Note ###
### Hook Creation Process in Depth ###
### Making a Reusable Sorting Hook ###

## Section 18: Into the World of Reducers ##
### App Overview ###
### Adding the Form ###
### More on the Form ###
### useReducer in Action ###
### Rules of Reducer Functions ###
### Understanding Action Objects ###
### Constant Action Types ###
### Refactoring to a Switch ###
### Adding a New State Updates ###
### A Few Design Considerations Around Reducers ###
### Introducing Immer ###
### Immer in Action ###

## Section 19: Dive Into Redux Toolkit ##
### Into the World of Redux ###
### Redux vs Redux Toolkit ###
### App Overview ###
### The Path Forward ###
### Implementation Time! ###
### Understanding the Store ###
### The Store's Initial State ###
### Understanding Slices ###
### Understanding Action Creators ###
### Connecting React to Redux ###
### Updating State from a Component ###
### Accessing State in a Component ###
### Removing Content ###
### Practice Updating State! ###
### Practice Accessing State! ###
### Even More State Updating! ###
### Resetting State ###
### Multiple State Updates ###
### Understanding Action Flow ###
### Watching for Other Actions ###
### Getting an Action Creator's Type ###
### Manual Action Creation ###
### File and Folder Structure ###
### Refactoring the Project Structure ###
### Link to Completed Project ###

## Section 20: Managing Multiple Slices with Redux Toolkit ##
### Project Overview ###
### Adding Component Boilerplate ###
### Thinking About Derived State ###
### Thinking About Redux Design ###
### Adding the Form Slice ###
### Maintaining a Collection with a Slice ###
### Creation of the Store ###
### From Values to Update State ###
### Receiving the Cost ###
### Dispatching During the Form Submission ###
### Awkward Double Keys ###
### Listing the Records ###
### Deleting Records ###
### CSS File for Download ###
### Adding Styling ###
### Form Reset on Submission ###
### Reminder on ExtraReducers ###
### Adding a Searching Input ###
### Derived State in useSelector ###
### Total Car Cost ###
### Highlighting Existing Cars ###

## Section 21: Interfacing with API's Using Async Thunks ##
### App Overview ###
### Adding a Few Dependencies ###
### Initial App Boilerplate ###
### API Server Setup ###
### Component Files ###
### Adding a Few Components ###
### Creation of the Redux Store ###
### Thinking About Data Structuring ###
### Reminder on Request Conventions ###
### Data Fetching Techniques ###
### Optional Async Thunks Section ###
### Adding State for Data Loading ###
### Understanding Async Thunks ###
### Steps for Adding a Thunk ###
### More on Adding Thunks ###
### Wrapping up the Thunk ###
### Using Loading State ###
### Adding a Pause for Testing ###
### Adding a Skeleton Loader ###
### Animations with TailwindCSS ###
### Rendering the List of Users ###
### Creation of New Users ###
### Unexpected Loading State ###
### Strategies for Fine-Grained Loading State ###
### Local Fine-Grained Loading State ###
### More on Loading State ###
### Handling Errors with User Creation ###
### Creation of Reusable Thunk Hook ###
### Creation of a Fetch-Aware Button Component ###
### Better Skeleton Display ###
### A Thunk to Delete a User ###
### Updating the Slice ###
### Refactoring the Component ###
### Deleting the User ###
### Fixing a Delete Error ###
### Album Feature Overview ###
### Additional Components ###
### Adding the ExpandablePanel ###
### Wrapping Up the ExpandablePanel ###
### Adding the Albums Listing ###

## Section 22: Modern Async with Redux Toolkit Query ##
### Skipping to this Section? ###
### [Optional] Getting Caught Up ###
### Introducing Redux Toolkit Query ###
### Constructing an RTK Query API ###
### Construcging an Endpoint ###
### Using the Generated Hook ###
### A Few Immediate Notes ###
### Rendering the List ###
### Changing Data with Mutations ###
### Differences Between Queries and Mutations ###
### Options for Refetching Data ###
### Request De-Duplication ###
### Some Internals of Redux Toolkit Query ###
### Refetching with Tags ###
### Fine-Grained Tag Validation ###
### Styling Fixups ###
### Adding a Pause for Testing ###
### Refactoring the List ###
### Remove Implementation ###
### Easy Tag Invalidation ###
### Getting Clever with Cache Tags ###
### More Clever Tag Implementation ###
### Photos Feature Overview ###
### Lots of Photos Setup! ###
### Adding the Endpoints ###
### Creation of the Photo ###
### Showing the List of Photos ###
### Adding Mouse-Over Deletes ###
### Adding Automatic Data Refetching ###

## Section 23: Bonus! ##
### Bonus! ###