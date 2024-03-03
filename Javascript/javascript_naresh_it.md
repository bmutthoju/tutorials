# JavaScript - Naresh IT #
1. Bootstrap:
	1. Dispay Flex
	2. Display Grid
		1. Row & Column
2. SASS
	1. Programming knowledge
		1. JavaScript will give the programming knowledge
3. JavaScript is light weight interpreted and JIT (Just In Time Compiled) programming language
	1. It is more than client-side scripting language
	2. Light weight: Occupy less space in memory
	3. Interpreted: Translation types
		1. Interpreted
			1. Line by line translation of code
		2. Compiled
			1. Everything is translated at a time
				1. JavaScript is both
			2. Just-in-Time compiled
				1. Two types of compiling techniques
					1. Just in Time (JIT)
						1. JS is using JIT
						2. What is it?
							1. On the fly translation
								1. Done in browser
					2. Ahead of Time (AOT)
						1. JS is also using AOT recently
						2. Program is compiled in application
							1. Only output is sent to browser
								1. For high performance
						3. This needs compiler inside application
							1. Babel - JS compiler
								1. Translates JS to keep it ready to use in browser
								2. [babeljs.io](babeljs.io)
						4. Angular/React/Vue
							1. Recently shifted to AOT
	4. JS is a language used in various applications
		1. Client-side (with HTML)
		2. Server-side (with Node.JS)
		3. Database (with MongoDB)
		4. Animations (with Flash, 3DS Max - action-script)
4. JavaScript is a language that supports various programming approaches like
	1. Functional programming
	2. Structural programming
	3. Imperative programming
	4. Object oriented programming

## JavaScript Client-Side ##
1. What is client-side?
	1. Backend has:
		1. Application Center
			1. Communicates with Data Center and gets info
		2. Data Center
			1. Contains info
				1. Example: Product Data
					1. Name
					2. Price
					3. Stock
					4. ...
	2. Front-End:
		1. Client
			1. User
				1. Interacts with application center
					1. Using form say:
						1. Contains:
							1. Name (string)
							2. Price (number)
								1. If we enter wrong type
									1. Database side validation is:
										1. Slow
										2. Burden on Database
											1. **The purpose of language like JavaScript client side is to reduce the burden on servers**
												1. How?
													1. By handling various actions on client side
														1. What client-side actions?
															1. DOM manipulations
																1. Adding elements into DOM
																	1. Example: upload image
																2. Removing elements from DOM
																	1. Example: Remove image
																3. Applying styling to DOM elements
																4. Updating data into elements
																	1. Example: Cut/Crop/Color .. of elements
																5. Configuring events to elements dynamically
																	1. Example: On click it should zoom
																	2. Example: On scroll it should move
															2. Browser interactions
																1. Location
																	1. Example: Knowing your location
																		1. Browser will pop a window and ask our location
																			1. To identify from which city we are accessing
																2. History
																	1. Example: Visiting previous page
																		1. Doesn't require server interaction
																	2. Cookies:
																		1. Example: If we enter userid and password
																			1. For every page, we are supposed to sign in - not good ux
																				1. Solution: client details are stored in cookies
																					1. We cannot login if cookies are not enabled
																		2. allowing or disabling
																		3. Status
																	3. Pages visited
																3. Navigator
																4. Document
																5. Window
															3. Validations
																1. They ensure that contradictory and unauthorized data is not stored into the database
																	1. Contradictory data: Expected and sent data are not matching
																	2. Unauthorized: Passing data not allowed to pass
									2. Solution:
										1. Validation can be performed on the client side (immediately rejects invalid data)
											1. Reduces latency & burden on servers and databases
							3. Stock (boolean)
							4. ...
2. Drawbacks:
	1. Browsers can block JS
		1. React/Angular/... will not work
		2. Chrome://settings
			1. JavaScript
				1. Don't allow sites to use JavaScript
					1. Why?
						1. Virus: Vital Information Under Seizure
							1. Computer program
								1. Delete files
								2. Rename files
								3. Change file extensions
								4. Corrupt files => OS is corrupted
						2. Trojans: Very dangerous
							1. We don't know if it is there
							2. It will send our info to others
								1. They take the help of JS
									1. If JS is disabled, trojans don't work
								2. Client side interactions do not work
						3. Google Family App - control kids' devices
					2. JS is less secure
	2. It is not a strongly typed language
		1. Example: 

				var age = 10;
				age = "John";

			1. How to prevent storing wrong values?
				1. Requires extra logic
	3. It is not implicitly strictly typed language
		1. Rules
			1. JS allows violating rules
				1. We can write in a bad style

						<script>
							x = 10; // using a variable without declaring
							document.write("x=" + x);
						</script>

						<!-- forcing developer to write as per rules -->
						<script>
							"use strict"; // **(M)**
							x = 10; // fails
						</script>

					1. Explicit enforcement of rules
			2. We can skip the programming rules until explicit `strict` is on
	4. It is not an OOP language
		1. It supports only few features of OOP
			1. Extensibility is not good
			2. Code-level security is not good
	5. It can be disabled by browsers
3. No choice
	1. The only language understandable by browser is JS
	2. Alternative:
		1. Some of them are translated to JS ultimately
			1. TypeScript - popular in the market (Angular/React/...)
				1. OOP Language
				2. Strictly typed
				3. Strongly typed
			2. Developers write TypeScript and it is translated to JavaScript
				1. Easier to code
			3. Why not in JS?
				1. Due to the above issues
		2. C# .NET
		3. Python
		4. Go

## JavaScript Integration ##
1. In companies, we use TypeScript, JQuery, Angular/React but not Javascript directly
	1. We need to be good at JavaScript, HTML, CSS, Bootstrap
2. Evolution of JavaScript
	1. History
	2. CERN Labs introducted a programming language for browsers called ECMA (European Computer Manufacturer Association) Script
	3. In early 1995 Netscape started a browser called "Netscape Navigator"
		1. First browser
			1. All browsers in the world follow the architecture of Netscape browser
	4. Netscape appointed "Brendan Eich" to develop a script for browser
		1. Brendan Eich - popular architect of web
			1. Designed a language called "Mocha", which was later renamed as "LiveScript".
				1. For Netscape
			2. Inventor of Mozilla Firefox
			3. He is the head of MDN
				1. Official documentation of HTML, CSS, and JavaScript
	5. Netscape given the responsibility of LiveScript to "Sun Microsystems"
		1. To maintain the infrastructure for the language
	6. Sun Microsystems was popular with Java
		1. Netscape and Sun microsystems renamed LiveScript as JavaScript
			1. To tell community that people maintaining Java is maintaining JavaScript
	7. In 2000 Netscape stopped its services (company closed)
		1. Netscape gave the responsibility of JavaScript to a company ECMA
			1. JavaScript was developed using the standards of ECMA
	8. JavaScript is known as ECMAScript or ES
	9. Its popular versions are:
		1. ECMAScript 2015 - ES5
		2. ECMAScript 2016 - ES6 (many companies are using this version)
		3. ...
		4. ECMAScript 2022 - ES2022
3. Why is it called as a script?
	1. A script is bound to certain functionality
		1. Language that is predictable (what it is going to do, where, and how it is going to do)
		2. It has boundaries
		3. It has limitations
			1. It will not overstep the boundaries

### Official Standard of JavaScript ###
1. ECMA
	1. [www.ecma-international.org](www.ecma-international.org)
		1. Many languages follow this standard
2. Official documentation:
	1. MDN Web Docs
		1. Brendan Eiche is responsible
			1. He developed JavaScript in 10 days
3. Definition of JavaScript
	1. It is lightweight inerpreted (or jit compiled) programming language with first-class functions

### Integrating JavaScript with HTML ###
1. Client Side
2. Server Side
3. Database

#### Client Side ####
1. JavaScript can be integrated into HTML in 3 ways:
	1. Incline JavaScript
		1. Advantage: Fast
		2. Disadvantage: Cannot be reused
	2. Embedded JavaScript
		1. Slow
		2. Can re-use
			1. Only within a page
	3. External File
		1. Increases number of requests
			1. Load time increases
		2. Can be re-used across pages
2. Example: demo.html

		<body>
			<h1>Print Your Ticket</h1>
			<button onclick="window.print()">Print</button>
		</body>

	1. Prints the page
3. Example:
	1. Object: Properties
		1. width = 100
		2. height = 100
		3. radius = 100
		4. border = red
		5. fill = yellow
	2. Object: Methods | Functions (what the actions are)
		1. roll
		2. bounce
		3. explode
	3. Object: Events (when the action happens)
		1. Roll
		2. Throw
		3. Pin
4. Example:
	1. Button: What object - Properties
		1. width = 
		2. height =
		3. color = 
	2. Button: Methods | Functions
		1. Submit
		2. Print
		3. Open
		4. Close
		5. Save
	3. Button: Events
		1. onclick
		2. onmouseover
		3. ondblclick **(M)**
		4. oncontextmenu **(M)**
			1. Right click
	4. Code:

			<button onclick="window.print()" id="btnPrint" class="btn btn-primary">Print</button>

		1. id, class - properties
		2. onclick - event
		3. window.print() - method
5. Inline JavaScript
	1. In this technique the script is defined with in the element by using events and functions
		1. It is faster in responding as it is native
		2. It is not good for reusability
	2. Syntax:

			<button onclick="window.print()">Print</button>

6. Embedded JavaScript
	1. JavaScript code is embedded into page using `<script>` container.
		1. We can embed in body and head
		2. We can put outside - abnormal in behaviour
	2. MIME type of CSS - text/css
	3. MIME type of Javascript - `text/javascript` or `language="javascript"`
	4. Code:

			<script type="text/javascript">
				function PrintPage() {
					window.print();
				}
			</script>
			...
			<button onclick="PrintPage()" ...></button>

		1. `()` - indicates allocation of memory by the name of the function
		2. `;` - optional (recommended)
			1. Even in CSS
		3. Separation of concerns
		4. We can also re-use the function in the page
	5. The actions are defined using a function

			<script>
				function name() {

				}
			</script>

		1. The action is called on specific event of an element

				<button onclick="name()">

			1. `language="javascript"` - old technique (not recommended)
7. FAQ:
	1. What is JavaScript strict mode? How to turn it ON?
		1. It forces developers to write as per the rules
		2. Example:

				<script type="text/javascript">
					x = 10; // JS allows without declaration
					document.write(x);
				</script>

		3. How to turn on strict mode?

				<script type="text/javascript"> <!-- **(M)** -->
					"use strict";
					x = 10;
					document.write("x = " + x);
				</script>

			1. It sets validation rules for writing code in HTML page
			2. If developer is writing embedded or external code, he can turn strict mode on by using "use strict"
				1. Inline code has not strict mode
		4. Syntax:

				<script type="text/javascript">
					"use strict";
					...your code...
				</script>

	2. How to target JavaScript code for legacy browsers?
		1. HTML parser is also used along with JavaScript interpreter (we don't need this these days)
		2. Code:

				<script type="text/javascript">
					"use strict";
					<!--
						function PrintPage() {
							window.print();
						}
					-->
				</script>

			1. Old browser does not understand
				1. It still works
			2. Why in html comments?
				1. It uses HTML parser to make JS code easier for old browser to understand
		3. By enclosing JavaScript code in HTML comments

				<!--
					javascript functions
				-->

8. JavaScript minification exist

## JavaScript in External File ##
1. We can write JavaScript functions in a separate JavaScript file with extension ".js"
2. We can link script file and access code from any page
3. Advantage: We can reuse the code across pages
4. Disadvantage: It increases page load time.
	1. Since number of requests increase
5. Javascript files:
	1. `src/scripts`
		1. `print.js`

				"use strict";
				<!--
					function PrintPage() {
						window.print();
					}
				-->
	2. `index.js`

				<script type="text/javascript" src="src/scripts/print.js">

6. To reduce the size of script file
	1. Minification
		1. Search: JS Minifier
			1. Copy the minified code
			2. Paste in `print.min.js`
			3. Change `src` in `<script>`

					<script type="text/javascript" src="src/scripts/print.min.js">

		2. It is a coding technique followed by developers to reduce the file size
			1. So we can minify JS code for production
7. When to use what?
	1. If JS is used only in one element, use inline JS
	2. If JS is re-used within a page, use embedded JS
	3. If JS is re-used across pages, use external JS

#### JavaScript Reference Techniques ####
1. To access HTML elements
	1. Why?
		1. JS makes HTML into a dynamic web-page
			1. Example: If we need to change picture as per context
				1. Upload picture and picture changes
2. Folder: `javascript-examples`
	1. `reference.html`

			<div>
				<img width="100" height="100" border="1">
			</div>
			<div>
				<form>
					<h3>Login</h3>
					User Name : <input type="text"> <input type="button">
				</form>
			</div>
			<div>
				<form>
					<h3>Register</h3>
					Your Email : <input type="text"> <input type="button">
				</form>
			</div>

	2. When loading the page:

			<script type="text/javascript">
				"use strict";

				function bodyload() {
					// reference elements
				}
			</script>

			<body onload="bodyload()"> <!-- **(M)** -->

3. Techniques:
	1. JavaScript can refer HTML elements by using DOM hierarchy
		1. DOM hierarchy
			1. Elements in a web-page have a hierarchical order
				1. Hierarchical diagram:

					window
						self, window, parent, top
						document
							all[]
							forms[]
								elements[]
									Button
									Checkbox
									File
									Hiden
									Password
									Radio
									Reset
									Select
										options[]
									Submit
									Text
									TextArea
							applets[]
							images[]
							embeds[]
							links[]
							anchors[]
							layers[]
						frames[]
						location
						history
						navigator
							plugins[]
							mimeTypes[]

			2. Code:

					window.document.images[0].src = "src/images/app.jpeg"

				1. Uses DOM hierarchy
				2. Button:

						window.document.forms[0].elements[1].value = "Login"; // HTML4 button

						window.document.forms[1].elements[1].value = "Register";

				3. Native technique of Javascript
					1. **Fastest**
						1. Since arrays are used
		2. Every page layout is designed using DOM hierarchy
		3. It comprises of parent and child nodes

				window
					document
						forms[]
							elements

				window
					document
						images[]

			1. Developer can use the DOM hierarchy for accessing elements
				1. We can google DOM
		4. It is the native method for browser and hence it is faster
		5. Drawback:
			1. Design is not standard and we may add, remove, or change positions of elements
				1. Example: If we change button's position to above textbox
					1. The index number changes
						1. **We have to change the code**
				2. Changing the position of any element in page requires change in index number in code
		6. When is this technique used?
			1. **To access elements quickly**
	2. JavaScript can refer to HTML elements by using a reference name
		1. For every element, we can give a name:

				<img ... name="poster">
				...
					<input type="button" name="btn-login">
					...
					<input type="button" name="btn-register">

			1. JS:

					function bodyload() {
						poster.src="../public/images/fashion2.jpg"; // **(M)**
					}

		2. Drawbacks:
			1. If an element is a child element, we cannot directly refer it (traditional parents like `ol` and `li` (not `<span>` inside `<div>`))
				1. Example: `li` is a child of `ol` or `ul`
					1. We need to refer to `ol` to refer to `li`
				2. Example: row is in tbody, tbody is in table
					1. All have to be refered
				3. Example: Mandatory to refer parent

						frmLogin.btnLogin.value = "Login";
						frmRegister.btnRegister.value = "Register";

						...

						<form name="frmRegister">
							...
							<input ... name="btnRegister">
							...
						</form>

			2. If same name is given to multiple elements (can cause error)
				1. Example: If all radio buttons have to be given the same name for mutex
				2. Every element in page can be defined with a reference name
					1. A `name` attribute is used to configure reference name

							<img name="poster">
						
							// Reference
							poster.src = "path";

				3. How to debug JS errors
					1. Browser > Inspect > Console
		3. Advantage:
			1. We can move elements but the code doesn't have to be changed
	3. JavaScript can refer elements by using ID
		1. Every element can be defined with a reference ID
		2. ID usually will be a unique reference
			1. Each element will have a unique ID (no two elements can have the same ID)
		3. JavaScript provides the following method to access element with "id".

				document.getElementById()

		4. Advantages:
			1. We can access element directly from any level of hierarchy
				1. No need to refer parent
					1. Even 10th descendant
		5. Drawbacks:
			1. If element doesn't have an id
				1. CSS can refer to multiple elements using a single id (id can be same for multiple elements)

						<input id="btn" ...>

						<input id="btn" ...>

						// CSS - the below code changes color of both buttons

						#btn {
							background-color: 'yellow';
						}

				2. JS cannot have multiple elements with single id
		6. Example:

				<img id="poster">

				document.getElementById("poster").src = "path";

		7. Example: Giving id only to an element

				function bodyload() {
					document.getElementById("poster").src = "../public/images/fashion3.jpg";
					document.getElementById("btnLogin").value = "Login";
					document.getElementById("btnRegister").value = "Login";
				}
	
	4. JavaScript can refer HTML elements by using CSS selectors (all CSS categories can be used)
		1. Example: Button inside nav-bar
		2. How to select?

				document.querySelector("img").src = "../public/images/fashion1.jpg"; // **(M)**
				
				document.querySelector("#btnLogin").src = "../public/images/fashion1.jpg";

				document.querySelector(".btn-register").value = "Register";

		3. Drawbacks:
			1. Multiple images can exist in a document
				1. Good only if there are unique elements
		4. CSS also has an object model
			1. CSSOM
		5. HTML elements are configured with styles by using various CSS selectors
			1. id
			2. class
			3. rational
			4. structural
			5. ...
		6. JavaScript can refer HTML elements with CSS selectors
			1. It uses the method:

					document.querySelector()

		7. Syntax:

				<img>

				// JS
				document.querySelector("img").src = "path";


				<img id="pic">

				// JS
				document.querySelector("#pic").src = "path";

			1. Example:
	5. JavaScript provides various other methods for accessing multiple elements simultaneously at the same time

			getElementsByTagName
			getElementsByClassName
			getElementsByName
			...

		1. Example:

				var result = document.getElementsByTagName("form");
				
				alert("Total number of forms in page are: " + result);

4. Summary:
	1. Integration of JS into HTML
		1. Inline
		2. Embedded
		3. External file
	2. Refering HTML elements
		1. DOM hierarchy
		2. By name
		3. By id
		4. By QuerySelector [CSS selector]

### JavaScript Output Techniques ###
1. A program language can interact with user
	1. If we ask a question
	2. It will process and generate an output and return
	3. Output is rendered on screen
2. A presentation language cannot interace with user 
3. Output:
	1. It is the process of rendering result on screen
4. JavaScript has various output techniques
	1. `alert()`
	2. `confirm()` **(M)**
	3. `document.write()` **(M)**
	4. `console` methods like `log`, `warn`, `debug`, `info` **(M)**
	5. `innerText` **(M)**
	6. `outerHTML` **(M)**
	7. `innerHTML` **(M)**
5. Example: Confirmation to user if we click a button

		<head>
			<script type="text/javascript">
				function DeleteClick() {
					alert("...");
				}
			</script>
		</head>
		<body>
			<button onclick="DeleteClick()">Delete</button>
		</body>

	1. `alert` - It pops up a message box in browser window
		1. It can show any message or result of any expression

				alert("your message" | expression);

			1. expression - calculation (10 + 20) say
		2. Drawbacks:
			1. It will not have any option to cancel.
				2. Example:

						alert("Record deleted..");

					1. We cannot customize the style of `alert`
						1. Alternatives: modals in bootstrap
						2. `alert` is `window` related and cannot be changed
							1. A lot of programming is required to change this
			2. It is RC data type.
				1. We cannot have styling for text (plain text)
					1. Bold, size change, etc... cannot be changed
						1. Change can be made in browser settings
				2. It will not allow formats for text
	2. `confirm()` - It is similar to `alert` but it has an option to cancel
		1. It is a boolean method
			1. It returns `true` or `false`
				1. On Ok it returns `true`
				2. On Cancel it returns `false`
		2. Example:

				result = confirm("Are you sure you want to delete?);
				if (result == true) {
					alert("Record deleted...");
				} else {
					alert("You cancelled...");
				}

6. `document.write()`: 
	1. It is an output method that renders result on new screen
	2. **It allows formatted text along with markup**
	3. It can also use expression
		1. It results some result
	4. Example:

			if (result == true) {
				document.write("<b><i><font color='red'>Record Deleted..</font></i></b><a href='output.html'>Back</a>");
			}

		1. It writes the formatted output on screen directly **in a new screen**
		2. Alert doesn't recognize formatting (it is RC datatype)
	5. Syntax:

			document.write("text | markup | expression");

7. `innerText`: **(M)**
	1. If we want to display output **on the same page** somewhere (no new screen), we can use a container (div, main, aside, article, span, p, ...)
		1. Example:

				if (result == true) {
					document.querySelector("p").innerText = "Record Deleted Successfully.";
				}

				<p></p>

	2. Drawbacks: It does not support formats
		1. It is RC datatype
	4. Use-case: Only for text
	5. It is used to render output in any container of HTML that can display text
8. `innerHTML`: **(M)**
	1. It is similar to `innerText` but supports formats and markup
	2. it will render the result into existing element
	3. Example:

			docuement.querySelector("p").innerHTML = "<b>Record Deleted Successfully.</b>";

	4. Syntax:

			document.querySelector("<element>").innerHTML = "<markup> | text | Expression";

	5. Example:

			if (result == true) {
				document.querySelector("p").innerHTML = "<b>Record Deleted Successfully.</b>";
			} else {
				
			}

	6. Problem:

			document.querySelector("p").innerHTML = "<h2></h2>";

		1. Puts <h2> inside <p> (adds two line breaks)
	7. Replacing existing element
9. `outerHTML`: **(M)**
	1. It is used to replace the existing element with the new element while rendering output
	2. Syntax:

			document.querySelector("p").outerHTML = "<h2>Text</h2>";

		1. Paragraph is replaced with heading
10. `console` methods:
	1. They are not for users but for developer
	2. Console is a developer tool available in every browser used to test developer function
		1. It allows testing logic directly
	3. We can display different styles
		1. Contextual styles: Primary, Success, Danger, Warning, ...
		2. If we want to show in error style
		3. If we want to show in warning style
		4. If we want to show in info style
		5. Some Browsers have good icons
	4. Example: `console.warn(...)`

			function DeleteClick() {
				console.warn("Delete Button Clicked");
				// ...
				if (result == true) {
					console.error("OK Clicked - Delete Processed.");
					// ...
				} else {
					console.log("Cancel button Clicked");
				}
			}

		1. We can also print how long it took to delete
	5. A developer can test JS commands in console
	6. A developer can log various contextual message in browser

			console.log(text | expression) => markup not allowed **(M)**
			console.warn() **(M)**
			console.info() **(M)**
			console.error() **(M)**
			console.debug() **(M)**
			...

### JavaScript Input ###
1. Input is the process of accepting value from user
2. User can input any value into HTML page using following techqniques
	1. **Query String**
	2. **Prompt()**
	3. **Form Input Elements**

#### Query String ####
1. Example:

		<p>Hello ! <span id="uname"></span></p>

	1. Whatever we type in address bar, it is query-string
	2. We can read the query-string and display on page
	3. Example: https://www.amazon.com/watches
		1. Opens: httsp://www.amazon.com/watches/?key=value&key=value
2. Process to configure query string:
	1. A query string is configured in the address bar of browser as part of URL
		1. Query string is appended to URL using ?
	2. Query string comprises of a key and value

			?key=value

	3. We can access the querystring from address bar using JavaScript `location.search` **(M)**
	4. Example:

			<script>
				function bodyload() {
					document.getElementById("search").innerHTML = location.search;
				}
			</script>
			...
			<body onload="bodyload()">
				<p>Searching for <span id="search"></span></p>
			</body>

		1. Address-bar: <url>/?username=John
		2. Methods:
			1. `slice()` **(M)**
				1. It can get only a part of string from specific index to specific index
			2. `indexOf()` **(M)**
		3. Example:

				document.getElementById("search").innerHTML = location.search.slice(location.search.indexOf("=") + 1);

				// in parts
				queryString = location.search;
				equalPosition = queryString.indexOf("=");
				value = queryString.slice(equalPosition + 1);
				document.getElementById("search").innerHTML = value;

		4. We need JavaScript string methods to extract values from querystring
			1. `indexOf()` - index number of a character in string
			2. `slice()` - It returns the characters between specified indices

#### Prompt ####
1. `prompt()` **(M)** - similar to alert but we can type
	1. It pops up an input box from where a user can input a value
	2. Drawback: Only one text box to input
		1. We cannot have multiple
		2. We cannot have other elements
2. Syntax: `prompt("message", "default_value");` **(M)**
	1. `Cancel` - null
	2. `OK`
		1. Without value - it will return empty string "" (it is still a value)
		2. With value - it will return the value
	3. We need to return condition for all three
	4. If we provide a default value, it will be shown in the textbox
	5. When we get a value, it will be stored in reference

			function bodyload() {
				if (category == null) {
					document.write(You cancelled...");
				} else if (category == "") {
					document.write("Please Provide a Category Name");
				} else {
					document.getElementById("search").innerHTML = category;
				}
			}

	6. `prompt()` returns the following:
		1. null : If it is cancelled
		2. "" : If value is not provided and clicked OK
		3. someValue : If clicked OK with value
	7. Use-Case: If input is not frequent, we don't need a dedicated input (text-box, search-button, ...)
		1. Standard screen occupies space
		2. If we need to input occasionally
		3. Example:

				<link rel="stylesheet" href="../node_modules/bootstrap-icons/font/bootstrap-icons.css">
				...
				<script>
					function AddClick() {
						folder = prompt("Enter folder name");
						if (folder == null) {
							alert("You cancelled...");
						} else if (folder == "") {
							alert("Please provide folder name");
						} else {
							document.querySelector("p").innerHTML += "Folder Created : " + folder + " <button class='bi bi-pen-fill'>Edit</button> <button class='bi bi-trash-fill'>Delete</button>" + "<br>"; // append
						}
					}
				</script>
				...
				<button onclick="AddClick()">
					<span class="bi bi-plus"></span> New Folder
				</button>

### Form Input Elements ###
1. We can use any form input element like textbox, checkbox, radio, listbox, dropdown, password, url, email, date, etc.
2. To access the value entered into an element, we can use "value" property
3. Syntax:
	1. `document.getElementById("txtEmail").value;`
	2. `document.querySelector("select").value;`
	3. Example:

			<link rel="stylesheet" href="../node_modules/bootstrap-icons/font/bootstrap-icons.css">
			<link rel="stylesheet" href="../node_modules/bootstrap/dist/css/bootstrap.css">
			...
			<script>
				function searchClick() {
					str = document.getElementById("search").value; // returns value in text-box
					document.querySelector("p").innerHTML = "Searching for: " + str;
				}
			</script>
			<body class="container-fluid">
				<header class="mt-4 p-2 input-group text-center w-10">
					<input type="text" placeholder="Search Amazon.in" class="form-control">
					<button onclick="searchClick()" class="btn btn-warning"><span class="bi bi-search"></span></button>
				</header>
				<p class="h3 text-center text-primary"></p>
			</body>


## Example Page ##
1. Quick Booking Toolbar
	1. Movies info
		1. Info
	2. New project:

				<link rel="stylesheet" href="../node_modules/bootstrap-icons/font/bootstrap-icons.css">
				<link rel="stylesheet" href="../node_modules/bootstrap/css/bootstrap.css">
				...
				<script type="text/javascript">
					"use strict";
					function getSummary() {

						document.getElementById("summaryContainer").style.display = "block";
						document.getElementById("btnContainer").style.display = "none";

						document.getElementById("lblMovie").innerText = document.getElementById("lstMovies").value;
						document.getElementById("lblCinema").innerText = document.getElementById("lstCinema").value;
						document.getElementById("lblDate").innerText = document.getElementById("lstDate").value;
						document.getElementById("lblTime").innerText = document.getElementById("lstTime").value;
						document.getElementById("lblSeats").innerText = document.getElementById("lstSeats").value;

						var movieName = document.getElementById("lstMovies").value;
						var imgPoster = document.getElementById("imgPoster"); // refers to the image pl	`aceholder

						if (movieName == "Kushi") {
							imgPoster.src = "../public/images/kushi.jpg";
						} else {
							imgPoster.src = "../public/images/jawan.jpg";
						}
					}
				</script>
			</head>
			<body class="container-fluid">
				<div id="btnContainer"> <!-- to toggle showing or hiding -->
					<button class="btn btn-danger target="#movies" mt-2">Quick Booking</button>
				</div>
				<div class="modal fade" id="movies">
					<div class="modal-dialogue modal-fullscreen">
						<div class="modal-content">
							<div class="modal-header">
								<h3>Quick Booking</h3>
								<button class="btn-close" data-bs-dismiss="modal"></button>
							</div>
							<div class="modal-body">
								<nav class="d-flex text-white p-3 justify-content-between">
									<div>
										<select id="lstMovies" class="form-select">
											<option>Select Movie</option>
											<option>Kushi</option>
											<option>Jawan</option>
										</select>
									</div>
									<div>
										<select id="lstCinema" class="form-select">
											<option>Select Cinema</option>
											<option>INOX - B'hills</option>
											<option>INOX - KPHB</option>
										</select>
									</div>
									<div>
										<select id="lstDate" class="form-select">
											<option>Select Date</option>
											<option>TODAY 9 SEP</option>
											<option>TOMORROW 10 SEP</option>
										</select>
									</div>
									<div>
										<select id="lstTime" class="form-select">
											<option>Select Time</option>
											<option>10:30 AM</option>
											<option>04:30 PM</option>
										</select>
									</div>
									<div>
										<select id="lstSeats" class="form-select">
											<option>Select Seats</option>
											<option>1</option>
											<option>2</option>
											<option>3</option>
											<option>4</option>
										</select>
									</div>
									<div>
										<button onclick="getSummary()" data-bs-dismiss="modal" class="btn btn-danger">BOOK</button>
									</div>
								</nav>
							</div>
						</div>
					</div>
				</div>

				<div id="summaryContainer" style="display: none;"> <!-- for toggling -->
					<dl class="w-25">
					<!--
					<dl class="w-50">
						<h4 class="bg-dark text-white p-2">Booking Summary</h4>
						<div class="row">
							<div class="col">
								<img width="100%" height="250" border="1" id="imgPoster">
							</div>
							<div class="col">
								<h4 class="bg-dark text-white p-2">Booking Summary</h4>
								<img width="100%" height="300" border="1" id="imgPoster">
								<dt>Movie</dt>
								<dd id="lblMovie"></dd>
								<dt>Cinema</dt>
								<dd id="lblCinema"></dd>
								<dt>Date</dt>
								<dd id="lblDate"></dd>
								<dt>Time</dt>
								<dd id="lblTime"></dd>
								<dt>Seats</dt>
								<dd id="lblSeats"></dd>
							</div>
						</div>
					-->
						<h4 class="bg-dark text-white p-2">Booking Summary</h4>
						<img width="100%" height="300" border="1" id="imgPoster">
						<dt>Movie</dt>
						<dd id="lblMovie"></dd>
						<dt>Cinema</dt>
						<dd id="lblCinema"></dd>
						<dt>Date</dt>
						<dd id="lblDate"></dd>
						<dt>Time</dt>
						<dd id="lblTime"></dd>
						<dt>Seats</dt>
						<dd id="lblSeats"></dd>
					</dl>
					<button class="btn btn-link" data-bs-toggle="modal" data-bs-target="#movies">Modify Booking</button>
				</div>

				<script src="../node_modules/jquery/disk/jquery.js"></script>
				<script src="../node_modules/bootstrap/disk/js/bootstrap.bundle.js"></script>
			</body>

		1. Option has:
			1. text
				1. What we see
				2. What we submit	
					1. If there is no value
			2. value
				1. If we want something different from text
		2. Every element in a form submit `value`
			1. We need to collect `value` of the element
			2. How?
				1. Each dropdown needs a separate id
					1. Rules of IDs:
						1. We use camel-case
						2. Convention for prefixes:
							1. `btn`
							2. `txt`
							3. `chk`
							4. `opt`
						3. Suffix - tells the purpose
							1. `close`
								1. Example: `btnClose`
							2. `open`
							3. `price`
								1. Example: `txtPrice`
						4. Element with multiple items
							1. We use plural form
								1. Example: `lst` - list
									1. `lstMovies` (plural)

## Example ##
1. Example form:

		<!DOCTYPE html>
		<html lang="en">
		
		<head>
		  <meta charset="UTF-8">
		  <meta name="viewport" content="width=device-width, initial-scale=1.0">
		  <title>Document</title>
		  <link rel="stylesheet" href="./node_modules/bootstrap-icons/font/bootstrap-icons.css">
		  <link rel="stylesheet" href="./node_modules/bootstrap/dist/css/bootstrap.css">
		  <script type="text/javascript">
		    function RegisterClick() {
		      document.getElementById("detailsContainer").style.display = "block";
		      document.getElementById("btnContainer").style.display = "none";
		
		      document.getElementById("lblName").innerText = document.getElementById("txtName").value;
		      document.getElementById("lblPrice").innerText = document.getElementById("txtPrice").value;
		      document.getElementById("lblCity").innerText = document.getElementById("lstCities").value;
		      stockCheckBox = document.getElementById("chkStock");
		      status = "";
		
		      if (stockCheckBox.checked) {
		        status = "Available";
		      } else {
		        status = "Out of Stock";
		      }
		
		      document.getElementById("lblStock").innerText = status;
		    }
		
		    function EditClick() {
		      document.getElementById("btnRegister").innerHTML = "Save";
		      document.getElementById("btnRegister").className = "btn btn-success";
		      document.getElementById("frmTitle").innerHTML = "Update Product";
		    }
		  </script>
		</head>
		
		<body>
		  <div id="btnContainer" class="mt-3">
		    <button data-bs-target="#register" data-bs-toggle="modal" class="btn btn-primary">Register Product</button>
		  </div>
		  <div class="modal fade" id="register">
		    <div class="modal-dialog modal-dialog-centered">
		      <div class="modal-content">
		        <div class="modal-header">
		          <h3 id="frmTitle">Register Product</h3>
		          <button class="btn-close" data-bs-dismiss="modal"></button>
		        </div>
		        <div class="modal-body">
		          <dl>
		            <dt>Name</dt>
		            <dd><input type="text" class="form-control" id="txtName"></dd>
		            <dt>Price</dt>
		            <dd><input type="number" class="form-control" id="txtPrice"></dd>
		            <dt>City</dt>
		            <dd>
		              <select id="lstCities" class="form-select">
		                <option>Select City</option>
		                <option>Delhi</option>
		                <option>Hyd</option>
		              </select>
		            </dd>
		            <dt>Stock</dt>
		            <dd class="form-switch">
		              <input type="checkbox" class="form-check-input" id="chkStock"> <label
		                class="form-check-label">Available</label>
		            </dd>
		          </dl>
		        </div>
		        <div class="modal-footer">
		          <button onclick="RegisterClick()" data-bs-dismiss="modal" id="btnRegister"
		            class="btn btn-primary">Register</button>
		          <button data-bs-dismiss="modal" id="btnCancel" class="btn btn-danger">Cancel</button>
		        </div>
		      </div>
		    </div>
		  </div>
		
		  <div id="detailsContainer" class="w-25" style="display: none;">
		    <dl>
		      <h3 class="bg-dark text-white p-2">Product Details</h3>
		      <dt>Name</dt>
		      <dd id="lblName"></dd>
		      <dt>Price</dt>
		      <dd id="lblPrice"></dd>
		      <dt>City</dt>
		      <dd id="lblCity"></dd>
		      <dt>Stock</dt>
		      <dd id="lblStock"></dd>
		    </dl>
		    <button onclick="EditClick()" data-bs-target="#register" data-bs-toggle="modal" class="btn btn-warning"><span
		        class="bi bi-pen-fill"></span>Edit</button>
		  </div>
		  <script src="../node_modules/jquery/dist/jquery.js"></script>
		  <script src="../node_modules/bootstrap/dist/js/bootstrap.bundle.js"></script>
		</body>
		
		</html>

## JavaScript Language ##
1. Topics
	1. Variables
	2. Data types
	3. Operators
	4. Statements
	5. Functions
	6. Object Oriented Programming

### Variables ###
1. Variables are storage locations in memory where we can store a value and use it in an expression
2. What is the problem if there are no variables?
	1. Example:

			<script>
			  document.write("Hello ! " + prompt("Enter Your Name") + "<br/>"); // user name needs to be appended, name fetched from prompt is 
			  // We need to address him again
			  document.write("Hey " + prompt("Enter Your Name") + " Welcome to JavaScript <br/>"); // He entered already and we didn't store it anywhere
			</script>

3. We can store value in memory
	1. A reference can be given to access the value stored in memory
		1. This is called a variable
4. With varible:
	1. Example:

			<script>
			  username = prompt("Enter Your Name");
			  document.write("Hello ! " + username + "<br/>"); // user name needs to be appended, name fetched from prompt is 
			  // We need to address him again
			  document.write("Hey " + username + " Welcome to JavaScript <br/>"); // He entered already and we didn't store it anywhere
			</script>

5. **Variable configuration contains 3 phases:**
	1. **Declaration**
	2. **Assignment**
	3. **Initialization**
6. Example: 

		var x; // no value inside - this is called declaration
		x = 10; // after declaration - this is called assignment
		var x = 10; // if we send a value when we delare - this is called initialization
		x = 30; // this is called assignment

7. Declaration comprises of keyword and variable name

		var x;
		var price;

8. Assignment is the phase where value is passed into variable
	1. It usually occurs after declaration

			x = 10; // assignment

9. Initialization is the process of passing a value at the time of declaration

		var x = 10; // initialization
		x = 20; // assignment
		var x = ""; // initialization

10. JavaScript allows directly assigning of value without declaring if it is not in strict mode
	1. Declaring a variable is not compulsory in non-strict mode
		1. Turing on strict mode:

				<script>
					"use strict";
					var x = 10;
					document.write(x);
				</script>

11. Declaring or initializing is mandatory for variable if it is in strict mode

		<script>
			"use strict";
			x = 10;	// invalid - x is not defined
			document.write(x);
		</script>

12. JavaScript variables can be declared by using 3 keywords
	1. `var`
	2. `let`
	3. `const`
13. Diferences:
	1. `var` - It defines function scope variable
		1. You can declare in any block of a function and access from any other block
		2. Example:

				<script>
					function f1() {
						var x;	// declaring variables
						x = 10; // assigning
						if (x == 10) {
							var y = 20; // initialization
						}
						document.write("x = " + x = "<br/>" + "y = " + y);
					}
					f1();
				</script>

			1. `function` block
			2. `if` block
				1. We have declared `y` inside
				2. It is possible to access it outside the `if` block
			3. `var` makes the variable a `function` scope variable (we can access it anywhere inside the function)
			4. The members of outer scope are accessible in inner scope
			5. The members of inner scope are accessible in outer scope
		3. It allows declaration, assignment, and initialization
		4. It allows shadowing
			1. Example:

					if (x == 10) {
						var y = 20;
						y = 30; // assigning
						y = 40;
					}
					document.write("x = " + x = "<br/>" + "y = " + y); // prints the latest value 40

				1. The latest value (assigned) will be printed
				2. Arranges values in a stack:

						40
						30
						20

			2. Shadowing example:

					if (x == 10) {
						var y = 20;
						var y = 30; // shadowing
					}
					document.write("x = " + x = "<br/>" + "y = " + y);

				1. Re-initializing the same name variable again
					1. Not possible in other programming languages like C, C++, Java, C#, ...
				2. Why do we need this?
			3. Shadowing is the process of re-initializing the same name identifier within the scope
				1. **The previously declared or initialized variable with the same is replaced completely**
			4. This is only possible with `var`
		5. `var` **allows hoisting** (it is used to tell "I am here")
			1. Example:

					<script>
						"use strict";
						function f1() {
							x = 10;
							document.write("x = " + x);
							var x; // this is error in other programming languages, in JS, it is valid
						}
					</script>

				1. JS is using interpreter
					1. `var x` - it will get hoisted (like a flag)
						1. The program is tranformed to:

								"use strict";
								function f1() {
									var x; // compiler does this, interpreter sees this and doesn't complain
									x = 10;
									document.write("x = " + x);
								}
				
			2. Hoisting is the process of configuring a variable and allowing to access without any order dependency
				1. You can use a variable first and later declare or initialize
				2. Example:

						<script>
							"use strict";
							x = 10;
							document.write("x = " + x);
							var x; // hoisted to the top
						</script>

	2. `let` - It configures a block-scope variable
		1. **A block scope variable is accessible only within the defined block and its inner block**
		2. It supports
			1. Declaring
			2. Assigning
			3. Initialization
		3. **It will not support shadowing and hoisting**
		4. It is fewer features than `var`
			1. We sometimes don't want a variable to be re-declared
				1. Example: Somebody can re-declare outside
		5. Example:

				<script>
					"use strict";
					function f1() {
						let x;
						x = 10;
						if (x == 10) {
							let y = 20;
							y = 30; // supported
							// var y = 30; // invalid - interpreter checks if name is taken or not (both var is allowed - shadowing)
							document.write("x = " + x + "<br/>y = " + y); // allowed
						}
						document.write("x = " + x + "<br/>y = " + y); // not allowed
					}
					f1();
				</script>

			1. A name must not be taken before except in the case of shadowing
		6. Example:

				"use strict";
				function f1() {
					x = 10;
					document.write("x = " + x);
					let x = 20; // hoisting is not supported
				}
				f1();

		7. Syntax:

				<script>
					let x = 10;
					let x = 20; // invalid - shadowing is not allowed
				</script>

				<!-- Hoisting is not allowed -->
				<script>
					"use strict";
					x = 10;
					document.write("x = " + x);
					let x; // invalid
				</script>

	3. `const`
		1. It defines a block scope variable (like `let`)
		2. It allows only:
			1. Initalization
				1. No Assignment
				2. No Declaration
		3. Example:

				<script>
					const x; // invalid - missing initializer
				</script>

				<script>
					const x = 10; // valid
					x = 20; // invalid
				</script>

		4. **Doesn't support shadowing and hoisting**

				const x = 10;
				const x = 20; // invalid

				
				x = 10;
				const x = 10; // invalid

		5. Constants can change during initialization

				const x = prompt("Enter number");

			1. We can change the value at the time of initialization of memory

## JavaScript - 7 ##
1. Summary:
	1. Variables
	2. Declaration
	3. Assignment
	4. Initialization
	5. Keywords
		1. var
			1. Allows
				1. Shadowing
				2. Hoisting
		2. let
			1. Block scope
			2. Supports
				1. Declaring
				2. Assignment
				3. Initialization
		3. const
			1. Block scope
			2. Supports
				1. Initialization
2. Local and Global Scope for Variable:
	1. If a variable is declared inside function or block, then it is local to function & block
	2. A local variable is not accessible outside function
	3. If a variable is declared outside function within script or module scope, then it is known as global variable
	4. A global variable is accessible to all functions in script or module
		1. Embedded - script
		2. Separate JS file - module
			1. If you are writing an external file, it is module
	5. Scope depends where we declare but not on which keyword is used
	6. Example:

			<script>
				function f1() {
					var x = 10;
				}
				function f2() {
					document.write("x in f2 is " + x); // not accessible
				}
				f1();
				f2();
			</script>

			<script>
				var x = 10; // becomes global
				// let x = 10; // still a global variable
				function f1() {
				}
				function f2() {
					document.write("x in f2 is " + x); // not accessible
				}
				f1();
				f2();
			</script>

3. Syntax:

		<script>
			var x = 10; // Global
			function f1() {
				var y = 20;  // local
			}
			function f2() {
				var z = 30;  // local
			}
		</script>

	1. If we declare/initialize a variable, it is a global variable
4. FAQ: Can we declare a variable in a function and make it global?
	1. Answer: Yes, it is possible using JavaScript `window` object
		1. It is not possible with `var`, `let`, or `const`
		2. Syntax:

				window.variableName = value; // **(M)** global even if we declare in a function - works on in browser (Client side)

		3. Example:

				function f1() {
					window.x = 50;
					document.write("x in f1 is: " + window.x);
				}

				function f2() {
					document.write("x is f2 is: " + window.x);
				}

		4. Example: Non-strict mode

				function f1() {
					x = 40;
					document.write("x in f1 is: " + x);
				}

				function f2() {
					document.write("x in f2 is: " + x); // works
				}

			1. Module variables
5. Variable Naming:
	1. A variable name must start with an alphabet or "_"
		1. Cannot start with number or special characters
	2. It can be alpha numberic
	3. Special characters are not recommended
		1. `_` is also not recommended
	4. Example:

			var _id = 1;
			var product_id = 2;
			var sales2023 = 454;
			var sales_2023 = 3434;

			var 2023sales = 353434; // invalid
			var $sales = 353434; // not recommended

	5. Always use camel case for naming variables

			var userName = "dgsdfsdf";

	6. A variable name must speak what it is:

			var c = 0; // not good
			var count = 0; // good
			var product;
			var products;

		1. Coding rules:
			1. [https://pmd.github.io](https://pmd.github.io) - static code analyzer
			2. [https://eslint.org](https://eslint.org) - Language initializer
				1. Officially built by JS developers
				2. Rules for writing JS
	7. Variable name can't exceed more than 255 characters
	8. If a variable requires further implementation (it is not final but it might change in the future):

			var _userName;

		1. Note: Variable names starting with `_` is a tradition for developer to define that it requires further implementation
6. FAQ's:
	1. What is the output for following code?

			var x;
			document.write("x = " + x);

		1. `x = undefined`
	2. What is the output for following code?

			var x,y = 10;
			document.write("x=" + x + "<br>" + "y = " + y);

			// Output
			x = undefined
			y = 10

	3. What is the output for following code?

			var x = y = 10;
			document.write("x=" + x + "<br>" + "y = " + y);

			// Output
			x = 10
			y = 10		
			
7. Destructuring technique for variables

		<script>
			var x, y = [10, 20];
			document.write("x=" + x + "<br>" + "y = " + y);
		</script>

		<script>
			var [x, y] = [10, 20]; // **(M)**
			document.write("x=" + x + "<br>" + "y = " + y);
		</script>

7. What is the output for?

		var [x, y, z] = [10,,20];

	1. x = 10
	2. y = undefined
	3. z = 20

### Data Types ###
1. Data Structure: It is not just what type but how it behaves
	1. Data type refers to Data Structure which specifies the type and behaviour of data in memory
2. JavaScript is not a strongly typed language (no restriction of data types - we can change the type of data)
3. JavaScript variables are implicitly typed
	1. Data type is determined according to value initialized or assigned

			var x = 10; // x is number type
			x = "John"; // x changes to string type

		1. This requires a lot of validation
	2. Variables in JavaScript can handle data types which are categorized into 2 types
		1. **Primitive data types**
			1. These are immutable types - we cannot changed the structure (not value)
			2. They have a fixed structure
			3. They cannot change the structure dynamically
			4. They have a fixed range of values
				1. Value range cannot be changed
					1. Developer knows what is inside
			5. They are stored in memory as stack [ Last-in-First-out ]
			6. JavaScript primitive types are **(M)**
				1. Number
				2. String
				3. Boolean
				4. Null
				5. Undefined
				6. Symbol (New)
				7. BigInt (New)
		2. **Non-primitive data types**

4. Primitive data types:

		<script>
			var x = 10;
			document.write(`MIN=${Number.MIN_SAFE_INTEGER}<br/>MAX=${Number.MAX_SAFE_INTEGER}`);
		</script>

	1. We cannot change the range
	2. In any device the range is same
	3. Number Type:
		1. JavaScript considers the following as number type
			1. Signed Integer - negative sign is allowed
			2. Unsigned Integer - all numbers are positive
			3. Floating Point - Upto 2 places integer and 2 places fraction
			4. Double - 3 places integer and 2 places fraction
			5. Decimal - More than 3 places integer and 29 fraction
				1. 3434534.4546435234
			6. Exponent - 2e3 => 2 x 10^3 = 2000 **(M)**
			7. Hexa - 0ffffff **(M)**
			8. Octa - 0o323 **(M)**
			9. Binary - 0b1010 **(M)**
			10. BigInt - 398739847398479837498374983749837498738947398n **(M)** (large integer)
				1. To safely use large number:
					1. Large value will not get rounded by compiler
		2. Examples:

				<script>
					var x = 0o343;
					document.write("x = " + x);
				</script>

	4. Every input from a form or HTML element is a string, which we have to convert into number (even numbers)
		1. How to convert:

				parseInt() **(M)**
				parseFloat() **(M)**

		2. Example:

				<script>
					var userName = prompt("Enter User Name");
					var age = parseInt(prompt("Enter Your Age"));
					document.write("Hello ! " + userName + "You will be " + (age + 1) + " next year");
				</script>

				<script>
					var cost = parseFloat(prompt("Enter cost of the item");
					document.write("Hello ! " + cost);
				</script>

	5. You can convert a number into a string by using

			toString() // **(M)** - It converts into plain string
			toLocaleString() **(M)** - It converts into a string with local and global formats

		1. Example:

				<script>
					var price = 56000.44;
					document.write(price.toLocaleString("en-in", {
						style: 'currency',
						currency: 'INR'
					}));
				</script>

			1. Syntax:

					number.toLocaleString('lang', { options })

## JavaScript - Class 7 ##
1. Immutable
	1. Number - signed, unsigned, floating, double, decimal, binary, octa, hexa, BigInt
2. String to number:
	1. parseInt()
	2. parseFloat()
3. Number to string:
	1. toString()
	2. toLocaleString()
		1. Currency format
		2. Currency
4. EMI Calculator: Shows number as formatted string with currency and , separators
5. We can verify the format of number by using `isNaN()` **(M)**
	1. Required because JS is not strongly typed

			<script>
				var age = prompt("Enter Age");
				if (isNaN(age)) {
					document.write("Age must be a number");
				} else {
					document.write("Age = " + age);
				}
			</script>

	2. It is a boolean function that returns `true` if value is not a number
6. Syntax:

		if (isNaN(value)) {

		} else {

		}

7. What is the output of the code?

		var a = parseInt("20A");
		var b = 10;
		var c = a + b;

	1. `c = 30`

8. What is the output of the code?

		var a = parseInt("A20"); // if it doesn't start with number, it will not be parsed
		var b = 10;
		var c = a + b;

	1. `c = NaN` - tells that we are not using a number
	
9. What is the output of the code?

		var a = parseInt("20A30"); // if it doesn't start with number, it will not be parsed
		var b = 10;
		var c = a + b;

	1. `c = 30` - takes only first number

10. To manipulate numbers in JavaScript, we have to use various arithmetic operators and "Math" functions
11. Arithmetic Operators:
	1. + : Addition - 10 + 20 = 30
	2. - : Subtraction - 20 - 10 = 10
	3. / : Division - 10 / 2 = 5
		1. For quotient (generally)
	4. * : Multiplication - 5 * 3 = 15
	5. % : Modulus - 10 % 2 = 0
		1. Remainder
	6. **: Power [number raised to its power] - 2\*\*3 = 8
	7. ++: Increment - x++, ++x
	8. --: Decrement - x--, --x
12. We need to understand how to convert a mathematical formula into a JS formula
13. Math Functions:
	1. Math library
		1. `Math.sqrt()` **(M)**
		2. `Math.PI` **(M)**
		3. `Math.cos()` **(M)**
		4. `Math.sin()` **(M)**
		5. `Math.tan()` **(M)**
		6. `Math.random()` **(M)**
		7. `Math.round()` **(M)**
		8. `Math.pow()` **(M)**
		9. `Math.floor()` **(M)**
		10. `Math.ceil()` **(M)**
		11. ...
	2. Syntax:

			Math.pow(2, 3) => 8
			Math.round(45.67) => 46
			Math.PI => 3.414...

	3. Formula:

			EMI = (P * R * Math.pow((1 + R),N)) / (Math.pow((1 + R), N) - 1)

		1. P - principal amount
		2. R - rate of interest (%)
			1. Convert: 8 / 12 / 100
		3. N - years
			1. N x 12 = months
14. emi-calculator.html

		<!DOCTYPE html>
		<html lang="en">
		
		<head>
		  <meta charset="UTF-8">
		  <meta name="viewport" content="width=device-width, initial-scale=1.0">
		  <title>Document</title>
		  <link rel="stylesheet" href="../node_modules/bootstrap/dist/css/bootstrap.css">
		  <style>
		    input[type="range"] {
		      width: 100%;
		    }
		  </style>
		  <script type="text/javascript">
		    function AmountChange() {
		      document.getElementById("txtAmount").value = document.getElementById("amountRange").value;
		    }
		
		    function YearChange() {
		      document.getElementById("txtYears").value = document.getElementById("yearRange").value;
		    }
		
		    function RateChange() {
		      document.getElementById("txtRate").value = document.getElementById("rateRange").value;
		    }
		
		    function CalculateClick() {
		      var P = parseInt(document.getElementById("txtAmount").value);
		      var N = parseInt(document.getElementById("txtYears").value) * 12;
		      var R = parseFloat(document.getElementById("txtRate").value) / 12 / 100;
		      var EMI = (P * R * Math.pow(1 + R, N)) / (Math.pow(1 + R, N) - 1);
		      document.getElementById("result").innerHTML = "Your monthly installment amount is &#8377;" + Math.round(EMI);
		    }
		  </script>
		</head>
		
		<body class="container-fluid bg-dark text-white">
		  <div class="bg-white text-dark p-3 m-3">
		    <h1 class="text-primary text-center">Personal Loan Calculator</h1>
		    <div class="row mt-4">
		      <div class="col">
		        Amount you need &#8377; <input type="text" id="txtAmount">
		      </div>
		      <div class="col">
		        for <input type="text" size="4" id="txtYears"> years
		      </div>
		      <div class="col">
		        Interest rate <input type="text" size="4" id="txtRate"> %
		      </div>
		    </div>
		    <div class="row mt-4">
		      <div class="col text-center">
		        <input type="range" onchange="AmountChange()" class="form-range" id="amountRange" min="50000" max="500000"
		          value="50000">
		      </div>
		      <div class="col text-center">
		        <input type="range" onchange="YearChange()" class="form-range" id="yearRange" min="1" max="5" value="1">
		      </div>
		      <div class="col text-center">
		        <input type="range" onchange="RateChange()" class="form-range" id="rateRange" min="8.45" max="12.45"
		          value="8.45" step="0.01">
		      </div>
		    </div>
		    <div class="row mt-4">
		      <div class="col d-flex justify-content-between">
		        <span>&#8377; 50,000</span>
		        <span>&#8377; 5,00,000</span>
		      </div>
		      <div class="col d-flex justify-content-between">
		        <span>1</span>
		        <span>5</span>
		      </div>
		      <div class="col d-flex justify-content-between">
		        <span>8.45%</span>
		        <span>12.45%</span>
		      </div>
		    </div>
		    <div class="row mt-4">
		      <div class="col text-end">
		        <button class="btn btn-primary" onclick="CalculateClick()">Calculate</button>
		      </div>
		    </div>
		    <div class="mt-4">
		      <p id="result" class="text-center h2 text-success"></p>
		    </div>
		  </div>
		</body>
		
		</html>

15. BMI Calculator
	1. https://www.calculator.net/bmi-calculator.html