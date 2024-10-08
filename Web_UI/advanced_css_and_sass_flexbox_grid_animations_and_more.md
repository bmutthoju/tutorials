# Advanced CSS and Sass: Flexbox, Grid, Animations and More! #
## Section 1: Welcome, Welcome, Welcome! ##
### Welcome to the Most Advanced CSS Course Ever! ###
1. 7 sections - 20+ hours
2. Sections:
	1. Natours Project - Setup and First Steps (Part 1) 
		1. Landing page
		2. New CSS properties and techniques
		3. Animations
		4. Advanced responsive design
		5. CSS architecture
		6. ...
	2. How CSS Works: A Look Behind the Scenes
		1. CSS architecture
	3. Introduction to Sass and NPM
		1. Tools to write and compile Sass
	4. Natours Project - Using Advanced CSS and Sass (Part 2)
		1. CSS properties and features
	5. Natours Project - Advanced Responsive Design (Part 3)
	6. Trillo Project - Master Flexbox!
	7. A Quick Introduction to CSS Grid Layouts
		1. Fundamentals
	8. Nexter Project - Master CSS Grid Layouts!

### READ BEFORE YOU START! ###
1. Download starter files, final project code, and course slides
	1. [Course material and instructions on GitHub](https://github.com/jonasschmedtmann/advanced-css-course)
2. [Discord community](https://discord.gg/uhMkpf4)
3. [Online tools and resources](http://codingheroes.io/resources/)

### Setting up Our Tools ###
1. VS Code
	1. Auto-complete
	2. Built-in git support
	3. Extensions
		1. Very smooth
2. Google Chrome

## Section 2: Natours Project - Setup and First Steps (Part 1) ##
### Section Intro ###
1. HTML and advanced CSS
2. Set up project
3. Exciting CSS features

### Project Overview ###
1. Project
	1. Website - landing page
		1. Tours in the nature
	2. Animations
	3. Features
	4. Animated cards
	5. Popup (pure CSS and not JS)
	6. Background video
	7. Modern look and feel
	8. Placeholder slides down
	9. Custom radio buttons
	10. Navigation
		1. Animation
2. Open Natures project in VS Code: [https://github.com/jonasschmedtmann/advanced-css-course](https://github.com/jonasschmedtmann/advanced-css-course)

### Building the Header - Part 1 ###
1. What you will learn in this lecture
	1. The best way to perform a basic reset using the universal selector
	2. How to set project-wide font definitions
	3. How to clip parts of elements using `clip-path` (modern CSS property)
2. Universal selector:
	1. `*` - selects each and every element in the page
	2. Reset:

			* {
				margin: 0;
				padding: 0;
				box-sizing: border-box;
			}

		1. Browsers, by default, apply some margin and padding on some elements (main heading say)
		2. `border-box` - change box model so that borders and paddings are no longer added to border width or border height specified
	3. Properties related to font are inherited

			body {
				font-family: "Lato", sans-serif; // inherited by all child elements in the body
				font-weight: 400;
				font-size: 16px;
				line-height: 1.7; // 1.7 times bigger than the predefined line-height
				color: #777;
			}

3. [https://bennettfeely.com/clippy/](https://bennettfeely.com/clippy/)
4. Code: style.css

		/*
		COLORS:
		
		Light green: #7ed56f
		Medium green: #55c57a
		Dark green: #28b485
		
		*/
		
		* {
		  margin: 0;
		  padding: 0;
		  box-sizing: border-box;
		}
		
		body {
		  font-family: "Lato", sans-serif;
		  font-weight: 400;
		  font-size: 16px;
		  line-height: 1.7;
		  color: #777;
		  padding: 30px; /* Not inherited */
		}
		
		.header {
		  height: 95vh; /* 95% of viewport height */
		  background-image: linear-gradient(
		      to right bottom,
		      rgba(126, 213, 111, 0.8),
		      rgba(40, 180, 133, 0.8)
		    ),
		    url("../img/hero.jpg");
		  background-size: cover; /* tries to fit image inside the box */
		  background-position: top; /* top of the image stays on top */
		
		  clip-path: polygon(0 0, 100% 0, 100% 75vh, 0 100%);
		  /* clip-path: polygon(50% 0, 100% 100%, 0 100%); */
		}

### Building the Header - Part 2 ###
1. What we will learn:
	1. The easiest way to center anything with the `transform`, `top`, and `left` properties
2. Code: style.css

		.logo-box {
		  position: absolute;
		  top: 40px;
		  left: 40px;
		}
		
		.logo {
		  height: 35px;
		}
		
		.text-box {
		  position: absolute;
		  top: 50%; /* In relation to the parent element */
		  left: 50%;
		  transform: translate(
		    -40%,
		    -50%
		  ); /* Relative to the element and not it's parent */
		}
		
		.heading-primary {
		  color: #fff;
		  text-transform: uppercase;
		}
		
		.heading-primary-main {
		  display: block;
		  font-size: 60px;
		  font-weight: 400;
		  letter-spacing: 35px;
		}
		
		.heading-primary-sub {
		  display: block;
		  font-size: 20px;
		  font-weight: 700;
		  letter-spacing: 17.4px;
		}

3. Code: index.html

		<body>
		    <header class="header">
		        <div class="logo-box">
		            <img src="img/logo-white.png" alt="Logo" class="logo">
		        </div>
		
		        <div class="text-box">
		            <h1 class="heading-primary"> <!-- Important for Google -->
		                <span class="heading-primary-main">Outdoors
		                </span>
		                <span class="heading-primary-sub">is where life happens</span>
		            </h1>
		        </div>
		    </header>
		</body>

### Constructing Cool CSS Animations ###
1. What you will learn in this
	1. How to contstruct CSS animations using `@keyframes` and the `animation` property
2. Browsers are optimized for
	1. Opacity
	2. Transform
3. ctrl+d (select multiple instances)

### Building a Complex Animated Button - Part 1 ###
1. What you will learn in the lecture
	1. What pseudo-elemets and pseudo-classes are;
	2. How and why to use the `::after` pseudo-element
	3. How to construct a creative hover animation effect using the `transition` property
2. Pseudo-class - a special state of an element
3. Code: style.css

		.btn:link,
		.btn:visited {
		  text-transform: uppercase;
		  text-decoration: none;
		  padding: 15px 40px;
		  display: inline-block;
		  border-radius: 100px;
		  transition: all 0.2s;
		}
		
		.btn:hover {
		  transform: translateY(-3px);
		  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2); /* 0px - x axis, 10px down - y axis, 20px - blur  */
		}
		
		.btn:active {
		  transform: translateY(-1px); /* in relation to original state */
		  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
		}
		
		.btn-white {
		  background-color: #fff;
		  color: #777;
		}

3. Code: index.html

		<a href="#" class="btn btn-white">Discover our tours</a>

4. Pseudo elements: Allow us to style certain parts of elements
	1. It is a virtual element after the element under selection which can be styled

### Building a Complex Animated Button - Part 2 ###
1. Code: style.css

		@keyframes moveInBotton {
		  0% {
		    opacity: 0;
		    transform: translateY(30px);
		  }
		
		  100% {
		    opacity: 1;
		    transform: translateY(0);
		  }
		}

		.btn:link,
		.btn:visited {
		  text-transform: uppercase;
		  text-decoration: none;
		  padding: 15px 40px;
		  display: inline-block;
		  border-radius: 100px;
		  transition: all 0.2s;
		  position: relative;
		}
		
		.btn:hover {
		  transform: translateY(-3px);
		  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2); /* 0px - x axis, 10px down - y axis, 20px - blur  */
		}
		
		.btn:active {
		  transform: translateY(-1px); /* in relation to original state */
		  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
		}
		
		.btn-white {
		  background-color: #fff;
		  color: #777;
		}
		
		/* Acts like a child of `btn` */
		.btn::after {
		  content: "";
		  display: inline-block;
		  height: 100%; /* same height as parent: `btn` */
		  width: 100%;
		  border-radius: 100px;
		  position: absolute;
		  top: 0;
		  left: 0;
		  z-index: -1; /* Behind the button */
		  transition: all 0.4s;
		}
		
		.btn-white::after {
		  background-color: #fff;
		}
		
		/* On hover of button apply style to pseudo element ::after */
		.btn:hover::after {
		  transform: scaleX(1.5) scaleY(1.6);
		  opacity: 0;
		}
		
		.btn-animated {
		  animation: moveInBotton 0.5s ease-out 0.75s;
		  animation-fill-mode: backwards; /* It automatically applies the style of 0% before the animation starts */
		}

## Section 3: How CSS Works: A Look Behind the Scenes ##
### Section Intro ###
1. Important and advanced concepts

### Three Pillars of Writing Good HTML and CSS (Never Forget Them!) ###
1. Three pillars to write good HTML and CSS... and build good websites
	1. Responsive design
	2. Maintainable and scalable code
	3. Web performance

#### Responsive Design ####
1. One website that works for all screen sizes on all devices
	1. Concepts:
		1. Fluid layouts
		2. Media queries
		3. Responsive images
		4. Correct units
			1. Font sizes
			2. Element dimensions
		5. Desktop-first vs mobile-first

#### Maintainable and Scalable Code ####
1. Topics - For professional Web development
	1. Clean
	2. Easy-to-understand
	3. Growth
	4. Reusable
	5. How to organize files (part of CSS architecture)
	6. How to name classes (part of CSS architecture)
	7. How to structure HTML (part of CSS architecture)

#### Web Performance ####
1. Performance: Faster and smaller (user needs to download less data)
2. Topics:
	1. Less HTTP requests
	2. Less code
	3. Compress code
	4. Use a CSS preprocessor
	5. Less images
		1. The biggest part of the size
			1. Use only necessary images
	6. Compress images
		1. They use less bandwidth

### How CSS Works Behind the Scenes: An Overview ###
1. To become a better CSS developer

#### What Happens to CSS When We Load Up a Web Page? ####
1. Flow:
	1. Load HTML
	2. Parse HTML (decodes code line by line)
		1. Browser builds Document Object Model (DOM)
			1. Describes web document as a family tree (decoded HTML code)
	3. Browser loads CSS mentioned in the header
	4. Parse CSS (more complex)
		1. **Resolve conflicting CSS declarations (cascade)**
		2. **Process final CSS values**
			1. % to px
	5. CSS Object Model (CSSOM)
		1. Final CSS is stored in a tree-like structure
	6. DOM + CSSOM => Render Tree
	7. Website rendering: the visual formatting model
		1. The visual formatting model: Algorithm calculates and uses many things (box model, floats, positioning)
	8. Final rendered website

### How CSS is Parsed, Part 1: The Cascade and Specificity ###
#### Quick Review: CSS Terminology ####
1. A CSS Rule

			.my-class {
				color: blue;
				text-align: center;
				font-size: 20px;
			}

		1. `.my-class` - selector
			1. To select one or more HTML elements
		2. `{...}` - declaration block
			1. Actual style
		3. `color: blue` - declaration
			1. `color` - property
			2. `blue` - declared value

#### The Cascade (The "C" in CSS) ####
1. Cascade: It is the process of combining different stylesheets and resolving conflicts between different CSS rules and declarations, when more than one rule applies to a certain element.
	1. Sources:
		1. Author declarations
			1. Declarations in stylesheets
		2. User declarations
			1. Users changing style in browser
		3. Browser (user agent)
			1. Default styles applied by browser (if we don't style them)
				1. Set by browser
	2. Strategy to resolve conflict

			importance (weight) > specificity > source order

		1. Cascading gives conflicting declarations different importances based on where they are declared
			1. User `!important` declarations (declarations marked with `!important` keyword)
			2. Author `!important` declarations
			3. Author declarations
			4. User declarations
			5. Default browser declarations (least important)
		2. Example: Author declarations

				.button {
					font-size: 20px;
					color: white;
					background-color: blue !important; /* more important than the next one */
				}

				#nav .pull-right .button {
					background-color: green;
				}

		3. If conflicting rules exist without `!important` then they have the same importance
			1. Next Cascade compares specificities of the declarations
		4. Specificities order:
			1. Inline styles (highest specificity)
			2. IDs
			3. Classes, pseudo-classes, attribute
			4. Elements, pseudo-elements [selectors] (least specificity)
		5. Calculating specificity:

				.button {
					font-size: 20px;
					color: white;
					background-color: blue;
				}

				nav#nav div.pull-right .button {
					background-color: green;
				}

				a {
					background-color: purple;
				}

				#nav a.button:hover {
					background-color: yellow;
				}

			1. Specificity: `(inline, IDs, Classes, Elements)`
				1. For each one, we count the number of occurrences in the selector
				2. Example: (above)

						(0, 0, 1, 0)
						(0, 1, 2, 2) // (-, #nav, .pull-right & .button, nav & div)
						(0, 0, 0, 1)
						(0, 1, 2, 1) // .button & :hover

					1. We look from left to right (most specific to least specific)
						1. If a specificity is the highest, that wins
							1. `(0, 1, 2, 2)` wins
								1. It is the cascaded value
			2. If same specificity?
				1. The last declaration in the code will override all other declarations and will be applied

#### Cascade and Specificity: What you need to know ####
1. CSS declarations marked with `!important` have the highest priority
2. But, only use `!important` as a last resort. It's better to use correct specificities - **more maintainable code!**
	1. Can cause problems in the long run
3. Inline styles will always have priority over styles in external stylesheets
	1. Not a good practice
4. A selector that contains 1 ID is more specific than one with 1000 classes.
5. A selector that contains 1 class is more specific than one with 1000 elements.
6. The universal selector `*` has no specificity value (0, 0, 0, 0)
	1. All other selectors have presedence over it
7. Rely more on **specificity** than on the **order** of selectors
	1. If we re-arrange CSS code, we will not have surprises
		1. Easier to maintain
8. But, rely on order when using 3rd party stylesheets - always put your author stylesheet last
	1. We should be able to override the styles

### Specificity in Practice ###
1. Codepen.io
	1. HTML

			<nav id="nav">
			  <div class="pull-right">
			    <a class="button button-danger" href="link.html">Don't click here!</a>
			  </div>
			</nav>

	2. CSS:

			body {
			  padding: 50px;
			}
			
			.button {
			  font-size: 20px;
			  color: white;
			  background-color: blue;
			}
			
			a {
			  background-color: purple;
			}
			
			#nav div.pull-right a.button {
			  background-color: orangered;
			}
			
			#nav div.pull-right a.button:hover { /* this class should have a higher specificity than the original one without :hover */
			  background-color: green;
			}
			
			#nav a.button:hover {
			  background-color: yellow; /* doesn't work because the specificity is lower */
			}

		1. Helps in debugging if something doesn't work

### How CSS is Parsed, Part 2: Value Processing ###
1. How values are processed in parsing phase

#### How CSS Values are Processed ####
1. Each time we use a unit other than px (%, rem, ...), it will ultimately be converted to px.
	1. Helps us predict and control which property takes with value
2. Example:

		<div class="section">
			<p class="amazing">CSS is absolutely amazing</p>
		</div>

		.section {
			font-size: 1.5rem;
			width: 280px;
			background-color: orangered;
		}

		p {
			width: 140px;
			background-color: green;
		}

		.amazing {
			width: 66%;
		}

	1. 6 steps:
		1. Declared value (author declaration)
			1. width (paragraph):
				1. 140px
				2. 66% - more specific
			2. padding (paragraph):
			3. font-size (root):
			4. font-size (section):
			5. font-size (paragraph):
		2. Cascaded value (after the cascade)
			1. width (paragraph):
				2. 66% - more specific
			2. padding (paragraph):
			3. font-size (root):
			4. font-size (section):
			5. font-size (paragraph):
		3. Specified value (defaulting, if there is no cascaded value)
		4. Computed value (converting relative values to absolute - they can be inherited) - keywords such as `auto`, `orange`, `bolder`, ... are computed and replaced
			1. width (paragraph):
				2. 66% (nothing happens in this step because it is not a unit)
			2. padding (paragraph):
			3. font-size (root):
			4. font-size (section):
			5. font-size (paragraph):
		5. Used value (final calculations, based on layout)
			1. width (paragraph):
				2. 66% of 280px = 184.8px
			2. padding (paragraph):
			3. font-size (root):
			4. font-size (section):
			5. font-size (paragraph):
		6. Actual value (considered using browser and device restrictions)
			1. width (paragraph):
				2. 184.8px => 185px
			2. padding (paragraph):
			3. font-size (root):
			4. font-size (section):
			5. font-size (paragraph):
3. For each and every element in the page, each and every CSS property needs to have a value (even if not declared)
	1. padding (paragraph)
		1. Declared value (author declarations) -
		2. Cascaded value (after the cascade) -
		3. Specified value (defaulting if there is no cascaded value)
			1. 0px (initial value) - already in absolute unit (if no padding is declared, we don't want any)
				1. Used if there is no cascaded value
					1. Inheritance also plays a role here
		4. Computed value (converting relative vals to absolute)
		5. Used value (final calculations, based on layout)
		6. Actual value (browser and device restrictions)
4. Root: font-size:
	1. Declared value -
	2. Cascaded value (after the cascade) - 16px (Browser default - user agent declaration)
		1. No more calculation needed
5. Section: font-size:
	1. Declared value
		1. 1.5rem
	2. Cascaded value
		1. 1.5rem
	3. Specified value
		1. 1.5rem
	4. Computed value
		1. 24px (1.5rem x 16px)
	5. Used value
		1. 24px
	6. Actual value
		1. 24px
6. Paragraph: font-size
	1. Declared value
		1. -
	2. Cascaded value
		1. -
	3. Specified value
		1. 24px (inheritance)
			1. Some elements inherit the computed value of their parent
	4. Computed value
		1. 24px (1.5rem x 16px)
	5. Used value
		1. 24px
	6. Actual value
		1. 24px

#### How Units are Converted from Relative to Absolute (PX) ####
1. Example:

		html, body {
			font-size: 16px;
			width: 80vw;
		}

		header {
			font-size: 150%;
			padding: 2em;
			margin-bottom: 10rem;
			height: 90vh;
			width: 1000px;
		}

		.header-child {
			font-size: 3em;
			padding: 10%;
		}

	1. Example (x);
		1. % (fonts)
			1. 150%
		2. % (lengths) (reference is always parent element's width)
			1. 10%
		3. em (font) (font-based) (uses parent's font-size as reference)
			1. 3em
		4. em (lengths) (font-based) (uses parent's font-size as reference)
			1. 2em
		5. rem (font-based) (uses root's font-size as reference)
			1. 10rem
	2. How to convert to pixels
		1. % (fonts)
			1. x% * parent's computed font-size
				1. html/body
		2. % (lengths)
			1. x% * parent's computed width
				1. 10% * 1000px
		3. em (font)
			1. x * parent computed font-size
				1. 3 * 24px
		4. em (lengths)
			1. x * current element computed font-size
				1. 2 * 24px
		5. rem
			1. x * root computed font-size
				1. 10 * 16px
	3. Result in pixels
		1. % (fonts)
			1. 24px
		2. % (lengths)
			1. 100px
		3. em (font)
			1. 72px
		4. em (lengths)
			1. 48px
		5. rem
			1. 160px
2. Why using font-size and ems and rems
	1. Enables building more responsive layouts
		1. Lengths can be changed by just changing font-size
			1. For flexibility
4. `vh`
	1. Example (x)
		1. 90vh
	2. How to convert to pixels
		1. x * 1% of viewport height
	3. Result in pixels
		1. 90% of the current viewport height (browser knows what the viewport height is)
5. `vw`
	1. Example (x)
		1. 80vw
	2. How to convert to pixels
		1. x * 1% of viewport width
	3. Result in pixels
		1. 80% of the current viewport width

#### CSS Value Processing: What you need to know ####
1. Each property has an initial value, used if nothing is declared (and if there is no inheritance - see next lecture)
2. Browsers specify a **root font-size** for each page (usually 16px)
3. Percentages and relative values are always converted to pixels
	1. For CSS engine to render the page in the screen
4. Percentages are measured relative to their parent's font-size, if used to specify font-size
5. Percentages are measured relative to their parent's width, if used to specify lengths
6. em are measured relative to their parent font-size, if used to specify font-size
7. em are measured relative to the current font-size, if used to specify lengths
8. rem are always measured relative to the document's root font-size
9. vh and vw are simply percentage measurements of the viewport's height and width

### How CSS is Parsed, Part 3: Inheritance ###
#### Inheritance in CSS ####
1. Example: Let's analyse line-height on .child

		.parent {
			font-size: 20px;
			line-height: 150%;
		}

		.child {
			font-size: 25px;
		}

	1. Every CSS property must have a value
		1. Even if the author nor the browser specifies it
			1. (no cascaded value)
	2. Is there a cascaded value?
		1. If yes:
			1. Specified value = cascaded values
		2. If no:
			1. Is the property inherited? (specified to each property)
				1. Yes:
					1. Some are inherited, and others are not
					2. `line-height` property specification
						1. It is inherited
					3. Specified value = Computed value of parent element
						1. It is not the % that is inherited, but the computed value 
				2. No:
					1. Secified value = Initial value (specific to each property)

#### Inheritance in CSS ####
1. Example:

		.parent {
			font-size: 20px;
			line-height: 150%;
		}

		.child {
			font-size: 25px;
		}

	1. Let's analyse `line-height` on `.child`
2. Steps:
	1. Every CSS property must have a value
	2. Is there a cascaded value?
		1. Yes
			1. Specified value = Cascaded value
		2. No
			1. Is the property inherited? (specific to each property)
				1. Yes
					1. Specified value = Computed value of parent element
						1. 30px (computed value)
				2. No
					1. Specified value = Initial value (specific to each property)
						1. Padding: 0px (intuitive)

#### Inheritance: What You Need to Know ####
1. Inheritance passes the value for some specific properties from parents to children - **more maintainable code**
	1. Advantage:
		1. Allows developer to write less code and code that is more maintainable
2. Poperties related to text are inherited:
	1. `font-family`
	2. `font-size`
	3. `color`
	4. etc.
3. Properties like margins and paddings are not inherited
	1. Impractical
		1. All children inheriting margin doesn't make sense
4. The computed value of a property is what gets inherited, not the declared value
5. Inheritance of a property only works if no one declares a value for that property
6. The `inherit` keyword forces inheritance on a certain property
7. The `initial` keyword resets a property to its initial value

### Converting px to rem: An Effective Workflow ###

#### What You Will Learn in this Lecture ####
1. How and why to use `rem` units in our project
2. A great workflow for converting px to rem

#### Why? ####
1. We want an easy way to change measurements in a page with one simple setting
	1. Example: When we hit a breakpoint to display on a mobile device
		1. We want to decrease all measurements at the same time
			1. Instead of writing a lot of code to do that in media queries. One global setting can be changed. `font-size` say
2. Change font-size and px to rem

		html {
			font-size: 10px;
		}

		/* ... */
		border-radius: 10rem; /* 10 * 10px = 100px */

	1. Using `px` is also a bad practice
		1. Users cannot change the font-size in the browser (it is hardcoded)
			1. Solution: Change to `%`
				1. Example:

						html {
						  /* font-size: 10px; */ /* 1rem = 10px */
						  font-size: 62.5%;
						}

			2. `rem` not supported below IE 9 - irrelevant
3. Inheritance must be used instead of universal selector
4. Code: style.css

		* *::after *::before {
		  /* after and before don't get the style by default */
		  margin: 0;
		  padding: 0;
		  /* box-sizing: border-box; */
		  box-sizing: inherit; /* Inherits whatever we put inside `body` which is `box-sizing: border-box` */
		}
		
		body {
		  font-family: "Lato", sans-serif;
		  font-weight: 400;
		  /* font-size: 16px; */
		  line-height: 1.7;
		  color: #777;
		  /* padding: 30px; /* Not inherited */
		  padding: 4rem;
		
		  box-sizing: border-box; /* makes it easier to change in plugins. Better practicing */
		}

### How CSS Renders a Website: The Visual Formatting Model ###
#### The Visual Formatting Model ####
1. **Definition**: It is an algorithm that calculates boxes and determines the layout of these boxes, for each element in the render tree, in order to determin the final layout of the page.
	1. Factors considered
		1. **Dimensions of boxes**: the box model
		2. **Box type**: inline, block, inline-block
		3. **Positioning scheme**: floats and positioning
		4. **Stacking contexts**
		5. Other elemnts in the render tree
			1. Siblings
			2. Parents
		6. Viewport size, dimensions of images, etc.

#### The Box Model ####
			
								-
							margin
								-
							padding
								-
								^
								|
		margin | padding | <--- width ---> | padding | margin
							height
								|
								v
								-
							padding
								-
							margin
								-

	1. Each and every element in a web-page can be seen as a box
	2. Each box can have
		1. Width
		2. Height
		3. Padding (optional)
		4. Margin (optional)
		5. Border (optional)
	3. **Content**
		1. text, images, etc. (we specify)
		2. We can define its `height` and `width` using the CSS properties.
	4. **Padding**
		1. **Transparent area** around the content, inside of the box
		2. It is used to define whitespace inside of the box
		3. `padding` property can be used in CSS
	5. **Border**
		1. Goes around the padding and the content
	6. **Margin**
		1. Space between boxes (outside the box)
		2. Used to define space between two elements
	7. **Fill area**
		1. Area that gets filled with background color or background image
			1. Includes **content area + padding area + border area**

#### The Box Model: Heights and Widths ####
1. **total width** = right border + right padding + specified width + left-padding + left border
2. **total height** = top border + top padding + specified height + bottom padding + bottom border
	1. Example: height = 0 + 20px + 100px + 20px + 0 = 140px
3. If we don't specify height and width, the visual formatting model will use content of the box to determine its size

#### The Box Model with Box-Sizing: Border-Box ####
1. width = left border + left padding + content width + right padding + right border
2. height = top border + top padding + content height + bottom padding + bottom border
3. **total width** = specified width
4. **total height** = specified height

#### Box Types: Inline, Block-Level, and Inline-Block ####
1. Block-Level boxes
	1. Elements formatted visually as blocks
	2. 100% of parent's width (as much space as possible)
	3. Vertically, one after another
		1. Line breaks are created at the end
	4. Box-model applies as shown
	5. `display: block` (The below also produce block-level boxes)
		1. `display: flex`
		2. `display: list-item`
		3. `display: table`
	6. Some elements' display property is set to `block` by default
2. Inline boxes
	1. Content is distributed in lines
		1. Only occupies the space its content needs
	2. Occupies only **content's space**
	3. No line-breaks
		1. They sit inside block level parent element
	4. No heights and widths
		1. They do not apply
	5. Paddings and margins only horizontal (left and right)
	6. `display: inline`
3. Inline-block boxes
	1. A mix of block and inline
	2. Occupies only content's space
	3. No line-breaks
	4. Box-model applies as shown
	5. `display: inline-block`

#### Positioning Schemes: Normal Flow, Absolute Positioning, And Floats ####
1. Normal flow
	1. Default position scheme
		1. Elements are layed out in the natural order of the code
	2. If **NOT** floated
	3. If **NOT** absolutely positioned
	4. Elements laid out according to their source order
	5. **Default**
		1. `position: relative` - it will still be normal flow
2. Floats
	1. **Element is removed from the normal flow**
		1. Shifted to left or right as far as possible until it touches the edge of its containing box or another float element
	2. Text and inline elements will wrap around the floated element
	3. The container will not adjust its height to the element
		1. Solution: Using clear fixes
	4. Types:
		1. `float: left`
		2. `float: right`
3. Absolute positioning
	1. **Element is removed from the normal flow**
	2. No impact on surrounding content or elements
		1. It can overlap other elements
	3. We use `top`, `bottom`, `left`, and `right` to offset the element from its relatively positioned container
		1. Stacking contexts
	4. Types:
		1. `position: absolute`
		2. `position: fixed`

#### Stacking Contexts ####
1. Determine in which order elements are rendered on the page
	1. A new stacking context can be constructed using different CSS properties
		1. Example: z-index
	2. Layers on the bottom of the stack are painted first and then subsequent layers on the top
	3. Example:

			z-index: 3
			position: relative

			z-index: 2
			position: absolute

			z-index: 1
			position: relative

		1. Stacking context with higher z-index appears on top
	4. Other properties that construct stacking contexts
		1. Opacity different from 1
		2. Transform
		3. Filter
	5. Sometimes the stacking order doesn't work as expected even after setting the z-index

### CSS Architecture, Components and BEM ###
#### The Think - Build - Architect Mindset ####
1. We want code that is:
	1. Clean
	2. Modular
	3. Reusable
	4. Ready for growth (to add more features)
2. Architecture
	1. We need to take important decisions concerning HTML and CSS code right from the beginning
		1. We need good strategy
3. Strategy:

		Think ----------------------------> Build ----------------------------> Architect
		Think about the layout of your		Build your layout in HTML and		Construct a logical **architecture** for
		webpage or web app before			CSS with a consistent structure		your CSS with files and folders
		writing code						for naming classes

#### Thinking About the Layout ####
1. Component-driven design
	1. **Modular building blocks** that make up interfaces
		1. Interface - collection of components held together by overall layout of the page
		2. Components should be **Re-usable** across a project, and between different projects
			1. We can build a library of components and re-use them across the project which will speed up development
		3. **Components** should be independent, allowing us to use them anywhere on the page
			1. Components should not depend on parent elements
		4. Similar to **Atomic design** philosopht
			1. Atoms -> Molecules -> Organisms -> Templates -> Pages
				1. Atoms - smallest units of the page
					1. They combine to form molecules
					2. Molecules compile to form organisms
						1. Organisms - components

#### Building with Meaningful Class Names ####
1. Consistent strategy, structure for naming classes
	1. Strategies
		1. Object Oriented CSS
		2. SMAX?
		3. BEM (more popular)
			1. Clean system
2. BEM - Block Element Modifier

		.block {}
		.block__element {}
		.block__element--modifier {}

	1. Low specificity BEM selectors
		1. We always use classe, and they are not nested - always low specificity
			1. Hence easy to maintain and re-usable code
	2. Block: Standalone component that is meaningful on its own
		1. Components are the blocks (standalone components that we can use anywhere in the project)
			1. Example:
				1. `recipe`
				2. `btn` (inside `recipe` block)
	3. Element: Part of a block that has no standalone meaning (if we take them out, they will not have any meaning)
		1. `__info`
		2. `__stats-box` (`recipe__stats--box`)
	4. Modifier: A different version of a block or an element
		1. To make it different from regular blocks or elements
			1. Example: To make a button round

					btn--round

				1. Modifier is used to make a different button
				2. `btn` applies to all buttons
3. Example:

		<figure class="recipe">
			<div class="recipe__hero">
				<img class="recipe__img" src="" />
			</div>
			<div class="recipe__info">
				<div class="recipe__category">
					Veggie
				</div>
				<figoption class="recipe__details">
					<h2 class="recipe__title">Pizza Vegetole</h2>
					<p class="recipe__description">
						Yummy veggie pizza with tasty olives
					</p>
				</figoption>
				<div class="recipe__stats-box">
					<div class="recipe__stat">
						<span class="recipe__stat-value">4.9</span>
						<span class="recipe__stat-name recipe__state-name--1">Stats</span>
					</div>
					<div class="recipe__stat">
						<span class="recipe__stat-value">45</span>
						<span class="recipe__stat-name recipe__state-name--1">Minutes</span>
					</div>
					<div class="recipe__stat">
						<span class="recipe__stat-value">2</span>
						<span class="recipe__stat-name recipe__state-name--1">Persons</span>
					</div>
				</div>
			</div>
			<a class="recipe__btn btn btn--round" href="#">Try</a>
		</figure>

	1. BEM might look ugly and hard to write (opinion) - more code
		1. It is worth it

#### Architecting with Files and Folders ####
1. Strategies
	1. ITCSS
	2. SMAXS
	7. 7-1 pattern
2. 7-1 pattern
	1. 7 different folders for partial Sass files (or any other CSS preprocessor), and
		1. `base/`
			1. Basic project definitions
		2. `components/`
			1. One file for each component
		3. `layout/`
			1. Definition of the overall layout of the project
		4. `pages/`
			1. Styles for specific pages of the project
		5. `themes/`
			1. To implement different visual themes
		6. `abstracts/`
			1. Code that does not output any CSS
				1. Variables
				2. Mixins
				3. ...
		7. `vendors/`
			1. All third party CSS goes
	2. 1 main Sass file to import all other files into a compiled CSS stylesheet
3. We don't have to use all the folders
	1. Depends on size and scope of project

### Implementing BEM in the Natours Project ###
1. What you will learn in this lecture
	1. How to use the BEM method in practice
2. Code: style.css

		/*
		COLORS:
		
		Light green: #7ed56f
		Medium green: #55c57a
		Dark green: #28b485
		
		*/
		
		html {
		  /* font-size: 10px; */ /* 1rem = 10px */
		  font-size: 62.5%;
		}
		
		* *::after *::before {
		  /* after and before don't get the style by default */
		  margin: 0;
		  padding: 0;
		  /* box-sizing: border-box; */
		  box-sizing: inherit; /* Inherits whatever we put inside `body` which is `box-sizing: border-box` */
		}
		
		body {
		  font-family: "Lato", sans-serif;
		  font-weight: 400;
		  /* font-size: 16px; */
		  line-height: 1.7;
		  color: #777;
		  /* padding: 30px; /* Not inherited */
		  padding: 4rem;
		
		  box-sizing: border-box; /* makes it easier to change in plugins. Better practicing */
		}
		
		.header {
		  height: 95vh; /* 95% of viewport height */
		  background-image: linear-gradient(
		      to right bottom,
		      rgba(126, 213, 111, 0.8),
		      rgba(40, 180, 133, 0.8)
		    ),
		    url("../img/hero.jpg");
		  background-size: cover; /* tries to fit image inside the box */
		  background-position: top; /* top of the image stays on top */
		  position: relative;
		
		  clip-path: polygon(0 0, 100% 0, 100% 75vh, 0 100%);
		  /* clip-path: polygon(50% 0, 100% 100%, 0 100%); */
		}
		
		.header__logo-box {
		  position: absolute;
		  top: 4rem;
		  left: 4rem;
		}
		
		.header__logo {
		  height: 3.5rem;
		}
		
		.header__text-box {
		  position: absolute;
		  top: 50%; /* In relation to the parent element */
		  left: 50%;
		  transform: translate(
		    -50%,
		    -40%
		  ); /* Relative to the element and not it's parent */
		  text-align: center;
		}
		
		.heading-primary {
		  color: #fff;
		  text-transform: uppercase;
		
		  backface-visibility: hidden; /* back part of the element will not be visible. Fixes shaking problem. Hack */
		
		  margin-bottom: 6rem;
		}
		
		.heading-primary--main {
		  display: block;
		  font-size: 6rem;
		  font-weight: 400;
		  letter-spacing: 3.5rem;
		
		  animation-name: moveInLeft;
		  animation-duration: 1s;
		  animation-timing-function: ease-out;
		
		  /* animation-iteration-count: 3; */ /* Happens 3 times */
		  /* animation-delay: 3s; */
		}
		
		.heading-primary--sub {
		  display: block;
		  font-size: 2rem;
		  font-weight: 700;
		  letter-spacing: 1.75rem;
		
		  animation: moveInRight 1s ease-out;
		}
		
		@keyframes moveInLeft {
		  0% {
		    opacity: 0;
		    transform: translateX(-10rem);
		  }
		
		  80% {
		    transform: translateX(1rem);
		  }
		
		  100% {
		    opacity: 1;
		    transform: translateX(0);
		  }
		}
		
		@keyframes moveInRight {
		  0% {
		    opacity: 0;
		    transform: translateX(10rem);
		  }
		
		  80% {
		    transform: translateX(-1rem);
		  }
		
		  100% {
		    opacity: 1;
		    transform: translateX(0);
		  }
		}
		
		@keyframes moveInBotton {
		  0% {
		    opacity: 0;
		    transform: translateY(3rem);
		  }
		
		  100% {
		    opacity: 1;
		    transform: translateY(0);
		  }
		}
		
		.btn:link,
		.btn:visited {
		  text-transform: uppercase;
		  text-decoration: none;
		  padding: 1.5rem 4rem;
		  display: inline-block;
		  border-radius: 10rem;
		  transition: all 0.2s;
		  position: relative;
		  font-size: 1.6rem;
		}
		
		.btn:hover {
		  transform: translateY(-0.3rem);
		  box-shadow: 0 1rem 2rem rgba(0, 0, 0, 0.2); /* 0px - x axis, 10px down - y axis, 20px - blur  */
		}
		
		.btn:active {
		  transform: translateY(-0.1rem); /* in relation to original state */
		  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
		}
		
		.btn--white {
		  background-color: #fff;
		  color: #777;
		}
		
		/* Acts like a child of `btn` */
		.btn::after {
		  content: "";
		  display: inline-block;
		  height: 100%; /* same height as parent: `btn` */
		  width: 100%;
		  border-radius: 10rem;
		  position: absolute;
		  top: 0;
		  left: 0;
		  z-index: -1; /* Behind the button */
		  transition: all 0.4s;
		}
		
		.btn--white::after {
		  background-color: #fff;
		}
		
		/* On hover of button apply style to pseudo element ::after */
		.btn:hover::after {
		  transform: scaleX(1.5) scaleY(1.6);
		  opacity: 0;
		}
		
		.btn--animated {
		  animation: moveInBotton 0.5s ease-out 0.75s;
		  animation-fill-mode: backwards; /* It automatically applies the style of 0% before the animation starts */
		}

## Section 4: Introduction to Sass and NPM ##
### Section Intro ###
1. Sass
	1. Basics
	2. Not hard to learn
		1. Extension of CSS
	3. Sass compiler
		1. NPM ecosystem
			1. How to compile using NPM packages & NPM scripts

### What is Sass? ###
### First Steps with Sass: Variables and Nesting ###
### First Steps with Sass: Mixins, Extends, and Functions ###
### A Brief Introduction to the Command Line ###
### NPM Packages: Let's Install Sass Locally ###
### NPM Scripts: Let's Write and Compile Sass Locally ###
### The Easiest Way of Automatically Reloading a Page on File Changes ###

## Section 5: Natours Project - Using Advanced CSS and Sass (Part 2) ##
### Section Intro ###
### Converting Our CSS Code to Sass: Variables and Nesting ###
### Implementing the 7-1 CSS Architecture with Sass ###
### Review: Responsive Design Principles and Layout Types ###
### Building a Custom Grid with Floats ###
### Building the About Section - Part 1 ###
### Building the About Section - Part 2 ###
### Building the About Section - Part 3 ###
### Building the Features Section ###
### Building the Tours Section - Part 1 ###
### Building the Tours Section - Part 2 ###
### Building the Tours Section - Part 3 ###
### Building the Stories Section - Part 1 ###
### Building the Stories Section - Part 2 ###
### Building the Stories Section - Part 3 ###
### Building the Booking Section - Part 1 ###
### Building the Booking Section - Part 2 ###
### Building the Booking Section - Part 3 ###
### Building the Footer ###
### Building the Navigation - Part 1 ###
### Building the Navigation - Part 2 ###
### Building the Navigation - Part 3 ###
### Building a Pure CSS Popup - Part 1 ###
### Building a Pure CSS Popup - Part 2 ###

## Section 6: Natours Project - Advanced Responsive Design (Part 3) ##
### Section Intro ###
### Mobile-First vs Desktop-First and Breakpoints ###
### Let's Use the Power of Sass Mixins to Write Media Queries ###
### Writing Media Queries - Base, Typography and Layout ###
### Writing Media Queries - Layout, About and Features Sections ###
### Writing Media Queries - Tours, Stories and Booking Sections ###
### An Overview of Responsive Images ###
### Responsive Images in HTML - Art Direction and Density Switching ###
### Responsive Images in HTML - Density and Resolution Switching ###
### Responsive Images in CSS ###
### Testing for Browser Support with @supports ###
### Setting up a Simple Build Process with NPM Scripts ###
### Wrapping up the Natours Project: Final Considerations ###

## Section 7: Trillo Project - Master Flexbox! ##
### Section Intro ###
### Why Flexbox: An Overview of the Philosophy Behind Flexbox ###
### A Basic Intro to Flexbox: The Flex Container ###
### A Basic Intro to Flexbox: Flex Items ###
### A Basic Intro to Flexbox: Adding More Flex Items ###
### Project Overview ###
### Defining Project Settings and Custom Properties ###
### Building the Overall Layout ###
### Building the Header - Part 1 ###
### Building the Header - Part 2 ###
### Building the Header - Part 3 ###
### Building the Navigation - Part 1 ###
### Building the Navigation - Part 2 ###
### Building the Hotel Overview - Part 1 ###
### Building the Hotel Overview - Part 2 ###
### Building the Description Section - Part 1 ###
### Building the Description Section - Part 2 ###
### Building the User Reviews Section ###
### Building the CTA Section ###
### Writing Media Queries - Part 1 ###
### Writing Media Queries - Part 2 ###
### Wrapping up the Trillo Project: Final Considerations ###

## Section 8: A Quick Introduction to CSS Grid Layouts ##
### Section Intro ###
### Why CSS Grid: A Whole New Mindset ###
### Quick Setup for This Section ###
### Constructing Our First Grid ###
### Getting Familiar with the fr Unit ###
### Positioning Grid Items ###
### Spanning Grid Items ###
### Grid Challenge ###
### Grid Challenge: A Basic Solution ###
### Naming Grid Lines ###
### Naming Grid Areas ###
### Implicit Grids vs. Explicit Grids ###
### Aligning Grid Items ###
### Aligning Tracks ###
### Using min-content, max-content, and the minmax() function ###
### Responsive Layouts with auto-fit and auto-fill ###

## Section 9: Nexter Project - Master CSS Grid Layouts! ##
### Project Overview and Setup ###
### Building the Overall Layout - Part 1 ###
### Building the Overall Layout - Part 2 ###
### Building the Features Section - Part 1 ###
### Building the Features Section - Part 2 ###
### Building the Story Section - Part 1 ###
### Building the Story Section - Part 2 ###
### Building the Homes Section - Part 1 ###
### Building the Homes Section - Part 2 ###
### Building the Gallery - Part 1 ###
### Building the Gallery - Part 2 ###
### Building the Footer ###
### Building the Sidebar ###
### Building the Header - Part 1 ###
### Building the Header - Part 2 ###
### Building the Realtors Section ###
### Witing Media Queries - Part 1 ###
### Writing Media Queries - Part 2 ###
### Browser Support to CSS Grid ###
### Wrapping up the Nexter Project: Final Considerations ###

## Section 10: That's it, Everyone! ##
### See You Next Time, CSS Master! ###
### My Other Courses + Updates ###