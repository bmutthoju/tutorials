# Sass #
## Topics ##
1. Install Sass first
	1. [Go here](https://sass-lang.com/install/)
		1. Node.js:

				npm i -g sass

			1. Only pure JS implementation of Sass (slower than other options)
				1. But it has same interface as other implementations
					1. Hence can be switched later

### Preprocessing ###
1. CSS can be fun, but stylesheets get large, complex, and hard to maintain
	1. Solution: Preprocessor (example: Sass)
		1. Sass has features that don't exist in CSS
			1. Nesting
			2. Mixins
			3. Inheritance
			4. ...
		2. Sass features help us write robust, maintainable CSS
2. Sass takes preprocessed Sass file and saves it as a normal CSS file that can be used in a website
	1. How?
		1. Terminal:
			1. We can compile sass file into css using `sass` command
				1. Inputs: which sass file to build from (input.scss)
				2. Outputs: CSS (output.css)
			2. Watching files or directories using `--watch` flag
				1. It watches source files for changes, re-compile CSS each time we save the sass file
				2. Example:

						sass --watch input.scss output.css

			3. We can watch and output to directories by using folder paths as input and output. Separate them with `:`

					sass --watch app/sass:public/stylesheets

				1. Gives the same names as the input files
				2. Watches all files in the `app/sass` folder for changes and compiles the changed files into CSS files in the `public/stylesheets` folder
3. Sass has two syntaxes:
	1. `SCSS` (`.scss`) - most commonly used
		1. It is a superset of CSS
			1. All valid CSS is also SCSS
	2. `SASS` - indented syntax (more unusual)
		1. Uses indentation instead of curly braces to nest statements
		2. Uses newlines instead of `;` to separate the statements

### Variables ###
1. We can store:
	1. Colors
	2. Font stacks
	3. CSS value (to re-use)
2. `$` - used to make something a variable
3. Example:

		$font-stack: Helvetica, sans-serif;
		$primary-color: #333;

		body {
			font: 100% $font-stack;
			color: $primary-color;
		}

	1. Sass takes variables and outputs normal CSS with variable values replaced in CSS
		1. Why? Keeps brand colors consistent throughout the site

### Nesting ###
1. HTML has nested and visual hierarchy, but CSS doesn't
	1. Solution: Sass allows us to nest CSS selectors
		1. It follows the same visual hierarchy of HTML
			1. Challenge: Overly nested rules will result in over-qualified CSS
				1. Hard to maintain and is a bad practice
2. Example:

		nav {
			ul {
				margin: 0;
				padding: 0;
				list-style: none;
			}

			li { display: inline-block; }

			a {
				display: block;
				padding: 6px 12px;
				text-decoration: none;
			}
		}

	1. Helps organize CSS and make it more readable

### Partials ###
1. Partial Sass files contain little snippets of CSS that we can include in other Sass files
	1. Why? To modularize CSS
		1. Helps things easier to maintain
2. Naming:
	1. Partial is a file named with a leading underscore (`_`)
		1. Example: `_partial.scss`
			1. `_` tells Sass that it is a partial file
				1. It will not be generated into a CSS file
3. Usage:
	1. Done using `@use` **(M)** rule

### Modules ###
1. Sass can be split into multiple files and combined using `@use` **(M)** rule
	1. `@use` loads another Sass file as a module
		1. Module: We can refer to the following with a **namespace based on the filename**
			1. Variables
			2. Mixins
			3. Functions
2. Example:

		// _base.scss
		$font-stack: Helvetica, sans-serif;
		$primary-color: #333;

		body {
			font: 100% $font-stack;
			color: $primary-color;
		}

		// styles.scss
		@use 'base';

		.inverse {
			background-color: base.$primary-color;
			color: white;
		}

	1. `@use 'base';` - Extension is not required
		1. `_` is not required

### Mixins ###
1. Problem:
	1. CSS3 is tedious sometimes
		1. It also has many vendor prefixes
	2. Solution:
		1. Mixins:
			1. A group of CSS declarations that we can re-use throughout our site
				1. Helps keep Sass DRY
			2. We can pass values to make mixin flexible
	3. Example:

			$mixin theme($theme: DarkGray) {
				background: $theme;
				box-shadow: 0 0 1px rgba($theme, .25);
				color: #fff;
			}

			.info {
				@include theme;
			}

			.alert {
				@include theme($theme: DarkRed);
			}

			.success {
				@include theme($theme: DarkGreen);
			}

		1. `@mixin` - directive to construct a mixin
			1. `theme` - name of the mixin
		2. `$theme` - variable to pass a value
		3. `@include` - To use the mixin
			1. `theme` - name of the mixin to include

### Extend/Inheritance ###
1. `@extend` - helps us share a set of CSS properties from one selector to another
	1. Placeholder class: A special class that only prints when it is extended (keeps compiled CSS neat and clean)
2. Example:
	1. Messaging for errors, warnings, successes extend placeholder class
3. Code: extend.scss

		/* This CSS will print because %message-shared is extended. */
		%message-shared {
			border: 1px solid #ccc;
			padding: 10px;
			color: #333;
		}

		// This CSS won't print because %equal-heights is never extended.
		%equal-heights {
			display: flex;
			flex-wrap: wrap;
		}

		.message {
			@extend %message-shared;
		}

		.success {
			@extend %message-shared;
			border-color: green;
		}

		.error {
			@extend %message-shared;
			border-color: red;
		}

		.warning {
			@extend %message-shared;
			border-color: yellow;
		}

	1. The above code tells that `.message`, `.success`, `.error`, and `.warning` must behave just like `%message-shared`
	2. In the generated CSS, each of the classes will get the CSS properties of `%message-shared`
	3. Helps avoid writing multiple class names
	4. Placeholder ensures that the class that's nested elsewhere in styles are not extended

### Operators ###
1. Sass has standard math operators (+, -, *, `math.div()`, and %)
2. Example: Simple math to calculate widths of `article` and `aside`

		@use "sass:math";

		.container {
			display: flex;
		}

		article[role="main"] {
			width: math.div(600px, 960px) * 100%;
		}

		aside[role="complementary"] {
			width: math.div(300px, 960px) * 100%;
			margin-left: auto;
		}

	1. A fluid grid based on 960px.
	2. Use-cases: Take pixel values and convert them to %.

## Documentation ##
### Syntax ###
1. Sass supports two different syntaxes
	1. Each one can load the other

#### Overview ####
1. SCSS:
	1. Uses the file extension: `.scss`
		1. It is a superset of CSS (all valid CSS is valid SCSS)
			1. It is the easiest syntax to get used to and most popular
	2. Example:

			@mixin button-base() {
				@include typography(button);
				@include ripple-surface;
				@include ripple-radius-bounded;

				display: inline-flex;
				position: relative;
				height: $button-height;
				border: none;
				vertical-align: middle;

				&:hover {
					cursor: pointer;
				}

				&:disabled {
					color: $mdc-button-disabled-ink-color;
					cursor: default;
					pointer-events: none;
				}
			}

##### The Indented Syntax #####
1. Sass's original syntax
2. File extension: `.sass`
3. It supports all the same features as SCSS
	1. Uses indentation instead of curly braces
		1. There are some additional differences in the indented syntax
		2. It does not support expressions that wrap across multiple lines
	2. Uses newline instead of semicolons
4. Example:

		@mixin button-base()
			@include typography(button)
			@include ripple-surface
			@include ripple-radius-bounded

			display: inline-flex
			position: relative
			height: $button-height
			border: none
			vertical-align: middle

			&:hover
				cursor: pointer

			&:disabled
				color: $mdc-button-disabled-ink-color
				cursor: default
				pointer-events: none

#### Parsing a Stylesheet ####
1. A sequence of Unicode code points are parsed
	1. Parsed directly without converting to a token stream

##### Input Encoding #####
1. A sequence of bytes are decoded into Unicode
	1. Sass performs it as follows:
		1. If sequence of bytes begins with UTF-8 or UTF-16 encoding of U+FEFF BYTE ORDER MARK, the corresponding encoding is used
		2. If sequence of bytes begins with plain ASCII string `@charset`, Sass determines the encoding using Step 2 of CSS algorithm for determining the fallback encoding
		3. Otherwise, UTF-8 is used

##### Parse Errors #####
1. If Sass encounters invalid syntax in a stylesheet, parsing will fail and an error will be presented to user with information about the location of the invalid syntax and the reason it was invalid.
	1. Different than CSS
		1. CSS specifies how to recover from most errors without failing immediately
			1. In this case, SCSS is not strictly the superset of CSS
			2. Benefit:
				1. Allows Sass users to see errors immediately instead of having them passed through to CSS output
	2. Location of parse errors can be accessed through implementation specific APIs
		1. Example: Dart Sass: `SassException.span`
			1. Node Sass, Dart Sass JS API: `file`, `line`, and `column` properties

#### Structure of a Stylesheet ####
1. Most Sass stylesheets (like CSS) made of up style rules that contain property declarations
	1. Sass stylesheets has many more features

##### Statements #####
1. Sass stylesheet is made up of a series of statements
	1. The statements are evaluated in order to build the CSS
2. Statements may have:
	1. blocks: Defined using `{` and `}`
		1. Blocks contain other statements
		2. Example: Style rule is a statement with a block
			1. Block contains other statements such as property declarations
		3. In SCSS, statements are separated by semicolons (optioanl if statement uses a block)
			1. In indented syntax, statements are separated using newline

###### Universal Statements ######
1. The following types of statements can be used anywhere in the stylesheet.
	1. Variable declarations: `$var: value`
	2. Flow control at-rules: `@if` and `@each`
	3. `@error`, `@warn`, and `@debug` rules

###### CSS Statements ######
1. The following statements produce CSS, and they can be used anywhere except withing `@function`
	1. Style rules, like `h1 { /* ... */ }`
	2. CSS at-rules, like `@media` and `@font-face`
	3. Mixin uses `@include`
	4. The `@at-root` rule

###### Top-Level Statements ######
1. The following statements can only be used at the top level of a stylesheet, or nested within a CSS statement at the top level
	1. Module loads: `@use`
	2. Imports: `@import`
	3. Mixin definitions: `@mixin`
	4. Function definition: `@function`

###### Other Statements ######
1. Property declarations may only be used within style rules and some CSS at-rules
	1. `width: 100px`
2. `@extend` may only be used within style rules

##### Expressions #####
1. Expression: Anything that goes on the right-hand side of a property or variable declaration
	1. Each expression produces a value
	2. Any valid CSS property value is a Sass expression
		1. Sass expressions are more powerful than plain CSS values
		2. They can be passed as arguments to `mixin`s and `function`s.
			1. They can be used to control flow with `@if` rule
			2. They can be manipulated using arithmetic
	3. Sass expression syntax is called `SassScript`

###### Literals ######
1. Simplest expressions represent static values
	1. Numbers: may or may not have units
		1. Example: 12, 100px
	2. Strings: may or may not have quotes
		1. Example: "Helvetica Neue" or `bold`
	3. Colors: may be hex representation or name
		1. Example: `#c6538c` or `blue`
	4. The `boolean` literals `true` or `false`
	5. The singleton `null`
	6. List of values (separated by spaces or commas). May be enclosed in square brackets or no brackets
		1. Example:

				1.5em 1em 0 2em, Helvetica, Arial, sans-serif, or [col1-start]
	
	7. Maps: Associate values with keys
		1. `'background': red`
		2. `'foreground': pink`

###### Operations ######
1. Sass defines syntax for many operations
	1. `==` and `!=`: used to check if two values are the same
	2. `+`, `-`, `*`, `/`, and `%`: Mathematical operators (for numbers)
		1. They have special behavior for units in scientific math
	3. `<`, `<=`, `>`, and `>=`: comparison operators
	4. `and`, `or`, and `not`: Boolean operators
		1. Every value is true except `false` and `null`
	5. `+`, `-`, and `/`: for concatenation of strings.
	6. `(` and `)`: used to control presedence order of operations.

###### Other Expressions ######
1. Variables, like `$var`
2. Function calls: `nth($list, 1)` or `var(--main-bg-color)`
	1. They may call **Sass core library functions** or **user-defined functions**, or may be **compiled directly to CSS**
3. Special functions
	1. `calc(1px + 100%)`
	2. `url(http://myapp.com/assets/logo.png)`
4. The parent selector, `&`
5. The value `!important`
	1. Parsed as an unquoted string

#### Comments ####
1. SCSS and SASS support two types of comments
	1. `/* */` - (usually) compiled to CSS
	2. `//` - not compiled to CSS

##### In SCSS #####
1. Similar to the ones in other languages (like JS)
	1. Single-line comments: `//` - go until the end of the line
		1. Nothing in a single line comment is emtted as CSS
		2. They are called silent comments (no CSS is produced)
2. Multi-line comments: `/* ... */`
	1. Written wherever statement is allowed. It is compiled to a CSS comment
	2. They are called loud comment
	3. **It may contain interpolation, evaluated before comment is compiled**
	4. **By default multi-line comments are stripped from compiled CSS in compressed mode**
	5. `/*!` - always included in the CSS output
3. Example:

		// This comment won't be included in the CSS.

		/* But this comment will, except in compressed mode. */

		/* It can also contain interpolation:
		 * 1 + 1 = #{1 + 1} */

		/*! This comment will be included even in compressed mode. */

		p /* Multi-line comments can be written anywhere
		   * whitespace is allowed. */ .sans {
		  font: Helvetica, // So can single-line comments.
		        sans-serif;
		}

##### In Sass #####
1. Indented syntax: Comments work differently
	1. `//` - silent comments are never emitted as CSS
		1. Unline SCSS, everything indented beneath opening `//` is also commented out.
	2. `/*` - They work as above but are compiled into CSS
		1. `*/` - optional (because indentation is used)
	3. `/*` - Can contain interpolation
	4. `/*!` - not stripped in compressed mode
	5. Comments can be used in expressions (same as SCSS)
2. Example:

		// This comment won't be included in the CSS.
		   This is also commented out

		/* But this comment will, except in compressed mode.

		/* It can also contain interpolation:
		   1 + 1 = #{1 + 1}

		/*! This comment will be included even in compressed mode.

		p .sans
			font: Helvetica, /* Inline comments must be closed. */ sans-serif

##### Documentation Comments #####
1. If writing style libraries using Sass: We can use comments to document `mixins`, `functions`, `variables`, and `placeholder selectors` provided by the library
	1. The comments are read by `SassDoc` tool
		1. To generate beautiful documentation
			1. Example: [Susy grid engine's documentation](http://oddbird.net/susy/docs/index.html)
2. Documentation comments are silent comments with three slashes (`///`) directly above thing we're documentating
	1. SassDoc parses text in the comments as Markdown
		1. Supports useful annotations to describe it in detail
3. Example:

		/// Computes an exponent
		///
		/// @param {number} $base
		///   The number to multiply by itself.
		/// @param {integer (unitless)} $exponent
		///   The number of `$base`s to multiply together.
		/// @return {number} `$base` to the power of `$exponent`.
		@function pow($base, $exponent) {
			$result: 1;
			@for $_ from 1 through $exponent {
				$result: $result * $base;
			}
			@return $result;
		}

	1. SassDoc installation:

			npm i sassdoc -g

	2. Running SassDoc

			sassdoc source/

#### Special Functions ####
1. CSS defines many functions
	1. Most CSS functions work fine with Sass's normal function syntax
		1. The Sass's functions are parsed and resolved to plain CSS functions ([plain CSS functions](https://sass-lang.com/documentation/at-rules/function/#plain-css-functions))
	2. Exceptions:
		1. A few Sass functions have syntax tat cannot be parsed as SassScript expression.
			1. Special function calls return unquoted strings
				1. Unquoted strings?
					1. Written just like CSS identifiers
						1. `bold`
						2. `-webkit-flex`
						3. `--123`

#### Page Sections ####
#### url() ####
1. `url()` function
	1. Commonly used in CSS
		1. It can take a quoted or unquoted URL
			1. Since unquoted URL is not a valid SassScript expression, Sass needs special logic to parse it
2. If `url()`'s argument is a valid unquoted URL, Sass parses it as-is
	1. Interpolation may be used to inject SassScript values
3. If `url()`'s argument is not a valid unquoted URL (say if it contains variables or function calls), it is parsed as a plain CSS function call
4. Example:

		$rototo-font-path: "../fonts/roboto";

		$font-face {
			// This is parsed as a normal function call that takes a quoted string.
			src: url("#{$roboto-font-path}/Roboto-Thin.woff2") format("woff2");

			font-family: "Roboto";
			font-weight: 100;
		}

		@font-face {
			// This is parsed as a normal function call that takes an arithmetic
			// expression
			src: url($roboto-font-path + "/Roboto-Light.woff2" format("woff2");

			font-family: "Roboto";
			font-weight: 300;
		}

		$font-face {
			// This is parsed as an interpolated special function.
			src: url(#{$roboto-font-path}/Roboto-Regular.woff2) format("woff2");

			font-family: "Roboto";
			font-weight: 400;
		}

	1. Output:

			@font-face {
			  src: url("../fonts/roboto/Roboto-Thin.woff2") format("woff2");
			  font-family: "Roboto";
			  font-weight: 100;
			}
			@font-face {
			  src: url("../fonts/roboto/Roboto-Light.woff2") format("woff2");
			  font-family: "Roboto";
			  font-weight: 300;
			}
			@font-face {
			  src: url(../fonts/roboto/Roboto-Regular.woff2) format("woff2");
			  font-family: "Roboto";
			  font-weight: 400;
			}

#### element(), progid:...(), and expression() ####
1. `element()` - It is a function
	1. It is defined in CSS spec
	2. IDs can be parsed as colors
		1. In Sass, it needs special parsing (?)
2. `expression()` & functions beginning with `progid`:
	1. They are legacy IE features (non-standard syntax)
		1. Sass supports them for backwards compatibility
3. **Sass allows any text in the function calls, including nested parantheses**
	1. Nothing is interpreted as SassScript expression (exception: Interpolation can be used to inject dynamic values)
4. Example:

		$logo-element: logo-bg;

		.logo {
			background: element(##{$logo-element});
		}

	1. Output: CSS

			.logo {
			  background: element(#logo-bg);
			}

### Style Rules ###
#### Overview ####
1. Style rules are just like they are for CSS (they work the same way)
	1. Example:

			.button {
				padding: 3px 10px;
				font-size: 12px;
				border-radius: 3px;
				border: 1px solid #e1e4e8;
			}

##### Nesting #####
1. Problem: Repetition of selectors over and over again
	1. Solution: Nesting (writing one style rule inside another)
		1. Sass automatically combines outer rule's selector with inner rule's selector
		2. Example:

				nav {
					ul {
						margin: 0;
						padding: 0;
						list-style: none;
					}

					li { display: inline-block; }

					a {
						display: block;
						padding: 6px 12px;
						text-decoration: none;
					}
				}

			1. Heads up!
				1. Nesting makes it hard to visualize how much CSS we are generating
					1. The deeper we nest, the more bandwidth it takes to serve CSS and more work it takes the browser to render it
						1. Solution: **Keep the selectors shallow**

###### Selector Lists ######
1. Selector lists: command separated selectors.
	1. Each complex selector (selectors between commas) is nested separately, and then combined back into a selector list.
2. Example:

		.alert, .warning {
			ul, p {
				margin-right: 0;
				margin-left: 0;
				padding-bottom: 0;
			}
		}

	1. CSS:

			.alert ul, .alert p, .warning ul, .warning p {
				margin-right: 0;
				margin-left: 0;
				padding-bottom: 0;
			}

###### Selector Combinators ######
1. We can nest combinators
	1. We can put combinator at the end of outer selector, at the beginning of inner selector, or all on its own in between the two
2. Example:

		ul > {
			li {
				list-style-type: none;
			}
		}

		h2 {
			+ p {
				border-top: 1px solid gray;
			}
		}

		p {
			~ {
				span {
					opacity: 0.8;
				}
			}
		}

	1. CSS:

			ul > li {
				list-style-type: none;
			}

			h2 + p {
				border-top: 1px solid gray;
			}

			p ~ span {
				opacity: 0.8;
			}

		1. Combinators:
			1. `+` - next-sibling combinator
			2. `>` - child combinator
			3. `||` - column combinator
			4. `~` - subsequent sibling combinator
			5. `" "` - descendant combinator
			6. `|` - namespace combinator

###### Advanced Nesting ######
1. [Parent selector combination](https://sass-lang.com/documentation/style-rules/parent-selector/)

##### Interpolation #####
1. Interpolation can be used to inject values from expressions like variables and function calls into selectors. (mixins - allows us to construct selectors from parameters users pass in)
2. Example:

		@mixin define-emoji($name, $glyph) {
			span.emoji-#{$name} {
				font-family: IconFont;
				font-variant: normal;
				font-weight: normal;
				content: $glyph;
			}
		}

		@include define-emoji("women-holding-hands", "🧑‍🤝‍🧑");

	1. CSS:

			@charset "UTF-8";
			span.emoji-women-holding-hands {
				font-family: IconFont;
				font-variant: normal;
				font-weight: normal;
				content: "🧑‍🤝‍🧑";
			}

		1. Note: Sass only parses selectors **after interpolation is resolved**
			1. We can use interpolation to generate any part of the selector
3. Interpolation can be combined with: ([Parent selector combination](https://sass-lang.com/documentation/style-rules/parent-selector/))
	1. Parent selector `&`
	2. `@at-root` rule
	3. Selector functions

#### Property Declarations ####
1. Property declaration: Defines how elements that match a selector a styled (similar to CSS)
	1. Sass adds extra features to make them easier to write and automate
		1. Declaration can be any SassScript expression
			1. The expression is evaluated and included in the result
2. Example:

		.circle {
			$size: 100px;
			width: $size;
			height: $size;
			border-radius: $size * 0.5;
		}

		/* CSS */
		.circle {
			width: 100px;
			height: 100px;
			border-radius: 50px;
		}

##### Interpolation #####
1. Property's name can include interpolation
	1. Helps generate properties dynamically as needed. (We can interpolate entire property names)
2. Example:

		@mixin prefix($property, $value, $prefixes) {
			@each $prefix in $prefixes {
				-#{$prefix}-#{$property}: $value;
			}
			#{$property}: $value;
		}

		.gray {
			@include prefix(filter, grayscale(50%), moz webkit);
		}

		/* CSS */
		.gray {
			-moz-filter: grayscale(50%);
			-webkit-filter: grayscale(50%);
			filter: grayscale(50%);
		}

##### Nesting #####
1. In CSS, many properties start with same prefix
	1. The prefix acts as a namespace
		1. Examples:
			1. `font-family`
			2. `font-size`
			3. `font-weight`
2. Sass allows property declarations to be nested.
	1. The outer property is added to the inner separated by `-`
3. Example:

		.enlarge {
			font-size: 14px;
			transition: {
				property: font-size;
				duration: 4s;
				delay: 2s;
			}

			&:hover { font-size: 36px; }
		}

		// CSS
		.enlarge {
			font-size: 14px;
			transition-property: font-size;
			transition-duration: 4s;
			transition-delay: 2s;
		}
		.enlarge:hover {
			font-size: 36px;
		}

4. Some CSS properties have shorthand versions that use namespace as property name
	1. We can write shorthand version and explicit versions
	2. Example:

			.info-page {
				margin: auto {
					bottom: 10px;
					top: 2px;
				}
			}

			// CSS
			.info-page {
				margin: auto;
				margin-bottom: 10px;
				margin-top: 2px;
			}

##### Hidden Declarations #####
1. Sometimes, we want to show property declaration only some of the time
	1. If value is null
	2. If empty, unquoted string
2. Sass doesn't compile the declaration to CSS

		$rounded-corners: false

		.button {
			border: 1px solid black;
			border-radius: if($rounded-corners, 5px, null);
		}

		// CSS
		.button {
			border: 1px solid black;
		}

##### Custom Properties #####
1. CSS custom properties (AKA CSS variables)
	1. They allow any text in declaration values
	2. The values are accessible to JS
		1. Any value can potentially be relevant to the user
			1. The values could be parsed as SassScript
2. Sass parses custom property declarations differently than other property declarations
	1. All tokens (including those that look like SassScript) are passed through to CSS as-is.
		1. Exception: Interpolation (the only way to inject dynamic values into custom property)
3. Example:

		$primary: #81899b;
		$accent: #302e24;
		$warn: #dfa612;

		:root {
			--primary: #{$primary};
			--accent: #{$accent};
			--warn: #{$warn};

			// Even though this looks like a Sass variable, it's valid CSS so it's not
			// evaluated.
			--consumed-by-js: $primary;
		}

		// CSS
		:root {
			--primary: #81899b;
			--accent: #302e24;
			--warn: #dfa612;
			--consumed-by-js: $primary;
		}

4. Heads up!
	1. Interpolation removes quotes from strings
		1. Makes it difficult to use quoted strings as values for custom properties when they come from Sass variables
			1. Workaround: Use `meta.inspect()` **(M)** function to preserve quotes

					@use "sass:meta";

					$font-family-sans-serif: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto;
					$font-family-monospace: SFMono-Regular, Menlo, Monaco, Consolas;

					:root {
						--font-family-sans-serif: #{meta.inspect($font-family-sans-serif)};
						--font-family-monospace: #{meta.inspect($font-family-monospace)};
					}

					// CSS
					:root {
						--font-family-sans-serif: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto;
						--font-family-monospace: SFMono-Regular, Menlo, Monaco, Consolas;
					}

#### Parent Selector ####
1. `&` - Special selector invented by Sass
	1. Used in nested selectors
	2. **It refers to outer selector** (like `this`)
	3. Purpose:
		1. To use outer selector in complex ways
			1. Examples:
				1. pseduo-class
				2. Adding selector before the parent
2. Example:

		.alert {
			// The parent selector can be used to add pseudo-classes to the outer
			// selector.
			&:hover {
				font-weight: bold;
			}

			// It can also be used to style the outer selector in a certain context, such
			// as a body set to use a right-to-left language.
			[dir=rtl] & {
				margin-left: 0;
				margin-right: 10px;
			}

			// You can even use it as an argument to pseudo-class selectors.
			:not(&) {
				opacity: 0.8;
			}
		}

		// CSS
		.alert:hover {
			font-weight: bold;
		}
		[dir=rtl] .alert {
			margin-left: 0;
			margin-right: 10px;
		}
		:not(.alert) {
			opacity: 0.8;
		}

3. Heads up!
	1. Parent selector is only allowed at the beginning of compound selectors where a type selector would also be allowed
		1. Example: `span&` is not allowed (?)

##### Adding Suffixes #####
1. We can use parent selector to add extra suffixes to outer selector
	1. Use-cases: [BEM](http://getbem.com/) - highly structured class names.
2. Requirement:
	1. Outer selector should end with an alphanumeric name (class selector, ID selector, element selector)
3. Example:

		.accordion {
			max-width: 600px;
			margin: 4rem auto;
			width: 90%;
			font-family: "Raleway", sans-serif;
			background: #f4f4f4;

			&__copy {
				display: none;
				padding: 1rem 1.5rem 2rem 1.5rem;
				color: gray;
				line-height: 1.6;
				font-size: 14px;
				font-weight: 500;

				&--open {
					display: block;
				}
			}
		}

		// CSS
		.accordion {
			max-width: 600px;
			margin: 4rem auto;
			width: 90%;
			font-family: "Raleway", sans-serif;
			background: #f4f4f4;
		}
		.accordion__copy {
			display: none;
			padding: 1rem 1.5rem 2rem 1.5rem;
			color: gray;
			line-height: 
		}
		.accordion__copy--open {
			display: block;
		}

##### In SassScript #####
1. Parent selector can be used in SassScript.
	1. A special expression that returns current parent selector in the same format used by selector functions (comma-separated list (selector list) that contains space-separated list (complex selectors)) that contain unquoted strings (compound selectors))
2. Example:

		.main aside:hover,
		.sidebar p {
			parent-selector: &;
			// => ((unquote(".main") unquote("aside:hover")),
			//     (unquote(".sidebar") unquote("p")))
		}

		// CSS
		.main aside:hover,
		.sidebar p {
			parent-selector: .main aside:hover, .sidebar p;
		}

	1. If `&` expression is used outside style rules, it returns `null`
		1. `null` is falsey
			1. Use-case: It can be used to determine whether a mixin is used in a style rule or not.
				1. Example:

						@mixin app-background($color) {
							#{if(&, '&.app-background', '.app-background')} {
								background-color: $color;
								color: rgba(#fff, 0.75);
							}
						}

						@include app-background(#036);

						.sidebar {
							@include app-background(#c6538c);
						}

						// CSS
						.app-background {
							background-color: #036;
							color: rgba(255, 255, 255, 0.75);
						}
						.sidebar.app-background {
							background-color: #c6538c;
							color: rgba(255, 255, 255, 0.75);
						}

###### Advanced Nesting ######
1. `&` can be used as a normal SassScript expression
	1. It can be passed to functions or included in interpolation (even in other selectors)
	2. Combining `&` with selector functions & `@at-root` rule allows us to nest selectors in powerful ways
		1. Example: Suppose we want to write a selector that matches outer selector and an element selector
			1. We can write a mixin that uses `selector.unify()` function to combine `&` with user's selector

					@use "sass:selector";

					@mixin unify-parent($child) {
						@at-root #{selector.unify(&, $child)} {
							@content;
						}
					}

					.wrapper .field {
						@include unify-parent("input") {
							/* ... */
						}
						@include unify-parent("select") {
							/* ... */
						}
					}

					// CSS
					.wrapper input.field {
						/* ... */
					}
					.wrapper select.field {
						/* ... */
					}

2. Heads up!
	1. Sass doesn't know what interpolation was used to generate the selectors
		1. It adds outer selector to the inner selector even if you used `&` as a SassScript expression (?)
			1. Solution: `@at-root` to tell Sass not to include outer selector
				1. `@at-root <selector> { ... }` - causes everyting within in to be emitted at the root of the document instead of using normal nesting.

#### Placeholder Selectors ####
1. Placeholder - a special kind of selector
	1. It looks and acts like a class selector but starts with `%`
		1. **It is not icluded in the CSS output**
		2. **Any complex selector (ones between commas) that contain placeholder is not included in CSS**
2. Example:

		.alert:hover, %strong-alert {
			font-weight: bold;
		}

		%strong-alert:hover {
			color: red;
		}

		// CSS
		.alert:hover {
			font-weight: bold;
		}

2. What is the use of a selector that isn't emitted?
	1. It can be extended
3. Advantages:
	1. Placeholders don't clutter the CSS if they are not extended
	2. Placeholders don't mandate that users of a library use specific class names for HTML
4. Example:

		%toolbelt {
			box-sizing: border-box;
			border-top: 1px rgba(#000, .12) solid;
			padding: 16px 0;
			width: 100%;

			&:hover {
				border: 2px rgba(#000, .5) solid;
			}
		}

		.action-buttons {
			@extend %toolbelt;
			color: #4285f4;
		}

		.reset-buttons {
			@extend %toolbelt;
			color: #cddc39;
		}

		// CSS
		.rest-buttons, .action-buttons {
			box-sizing: border-box;
			border-top: 1px rgba(0, 0, 0, .12) solid;
			padding: 16px 0;
			width: 100%;
		}
		.reset-buttons:hover, .action-buttons:hover {
			border: 2px rgba(0, 0, 0, 0.5) solid;
		}
		.action-buttons {
			color: #4285f4;
		}
		.reset-buttons {
			color: #cddc39;
		}

	1. Use-cases:
		1. Placeholder selectors are useful when writing Sass library where each style rule may or may not be used
		2. Rule of thumb:
			1. If writing stylesheet ust for our own app, it is better to extend a class selector if one is available

### Variables ###
1. Sass variables are simple:
	1. Assign a value to a name that begins with `$`
	2. Refer to the name instead of value
2. Advantages:
	1. Reduces repitition
	2. Does complex math
	3. Configure libraries
	4. ...
3. Variable declaration is similar to property declaration
	1. Syntax:

			<variable>: <expression>

		1. Variables can be declared anywhere we want
			1. Unline properties, which can be declared in a style rule or at-rule
		2. Usage: Include it in a value
	2. Example:

			$base-color: #c6538c;
			$border-dark: rgba($base-color, 0.88);

			.alert {
				border: 1px solid $border-dark;
			}

			// CSS
			.alert {
				border: 1px solid rgba(198, 83, 140, 0.88)
			}

4. Heads Up!
	1. CSS has variables of its own
		1. They are totally different from Sass variables
	2. Sass variables are compiled by Sass
		1. CSS variables are included in the CSS output
	3. CSS variables can have different values for different elements
		1. Sass variables only have one value at a time
	4. Sass variables are imperative
		1. If you use a variable and change its value, earlier use will be the same
		2. CSS variables are declarative
			1. If you change the value, it'll affect both earlier uses and later uses.
	5. Example:

			$variable: value 1;
			.rule-1 {
				value: $variable;
			}

			$variable: value 2;
			.rule-2 {
				value: $variable;
			}

			// CSS
			.rule-1 {
				value: value 1;
			}
			.rule-2 {
				value: value 2;
			}

		1. Fun fact:
			1. Sass treat hyphens and underscores as identical
				1. `$font-size` and `$font_size` both refer to the same variable
					1. Because earlier Sass allowed only `_` in ids
						1. Sass added support for `-` to match CSS
							1. The two were made equivalent

#### Default Values ####
1. When we assign a value to a variable, if the variable had a value, its old value is overwritten
	1. Requirement: If writing a Sass library, we might want to allow users to configure library's variables before we use them to generate CSS.
		1. Solution: `!default` flag
			1. **It assigns a value to a variable only if that variable isn't defined or its value is null. Otherwise, the existing value will be used**

##### Configuring Modules #####
1. Variable defined with `!default` can be configured when loading a module with the `@use` rule
	1. Sass libraries use `!default` variables to allow users o configure the library's CSS
2. To load a module with configuration:
	1. Write `@use <url> with (<variable>: <value>, <variable>: <value>)`
		1. Configured values will override variable's default values
		2. Only variables written at the top level of stylesheet with `!default` flag can be configured
3. Example:

		// _library.scss
		$black: #000 !default;
		$border-radius: 0.25rem !default;
		$box-shadow: 0 0.5rem 1rem rgba($black, 0.15) !default;

		code {
			border-radius: $border-radius;
			box-shadow: $box-shadow;
		}

		// style.scss
		@use 'library' with (
			$black: #222,
			$border-radius: 0.1rem
		);

		// CSS
		code {
			border-radius: 0.1rem;
			box-shadow: 0 0.5rem 1rem rgba(34, 34, 34, 0.15);
		}

#### Built-in Variables ####
1. Variables defined by built-in modules cannot be modified.
2. Example:

		@use "sass:math" as math;

		// This assignment will fail.
		math.$pi: 0;

		// CSS

#### Scope ####
1. Variables declared at the top level of a stylesheet are global
	1. They can be accessed anywhere in their module after they've been declared
		1. Not true for all variables
2. Variables declared in blocks (curly braces in SCSS or indented code in Sass) are usually local.
	1. They can be accessed only within the block they are declared
3. Example:

		$global-variable: global value;

		.content {
			$local-variable: local value;
			global: $global-variable;
			local: $local-variable;
		}

		.sidebar {
			global: $global-variable;

			// This would fail, because $local-variable isn't in scope:
			// local: $local-variable;
		}

		// CSS
		.content {
			global: global value;
			local: local value;
		}
		.sidebar {
			global: global value;
		}

##### Shadowing #####
1. Local variables can be declared with the same name as global variable
	1. If so, There are two variables with the same name
		1. Local
		2. Global
	2. Helps ensure that an author writing a local variable doesn't accidentally change the value of a global variable
2. Example:

		$variable: global value;

		.content {
			$variable: local value;
			value: $variable;
		}

		.sidebar {
			value: $variable;
		}

		// CSS
		.content {
			value: local value;
		}
		.sidebar {
			value: global value;
		}

3. If we need to set a global variable's value from within a local scope (example in a mixin), use `!global` **(M)** flag 
	1. It will always assign to the global scope
	2. Example:

			$variable: first global value;

			.content {
				$variable: second global value !global;
				value: $variable;
			}

			.sidebar {
				value: $variable;
			}

			// CSS
			.content {
				value: second global value;
			}
			.sidebar {
				value: second global value;
			}

		1. `!global` - only used to set variable already declared in the top level of a file
			1. It may not be used to declare a new variable

##### Flow Control Scope #####
1. Variables declared in flow control rules have special scoping rules
	1. They don't shadow variables at the same level as the flow control rule
		1. They just assign to those variables
			1. Why? To conditionally assign a value to a variable, or build u a value as part of a loop

#### Advanced Variable Functions ####
1. Sass core provides advanced functions for working with variables
	1. `meta.variable-exists()` **(M)** - returns whether a variable with the given name exists in the current scope
	2. `meta.global-variable-exists()` **(M)** - returns whether a variable with the given name exists in the global scope
2. Heads up!
	1. Sass doesn't allow using interpolation to define a variable based on another variable
		1. Reasons: Much harder to tell at a glance which variables are defined where
			1. Workaround: Define a `map` from names to values that we can access using variables
3. Example:

		@use "sass:map";

		$theme-colors: {
			"success": #28a745,
			"info": #17a2b8,
			"warning": #ffc107,
		};

		.alert {
			// Instead of $theme-color-#{warning}
			background-color: map.get($theme-colors, "warning");
		}

		// CSS
		.alert {
			background-color: #ffc107;
		}

### Interpolation ###
1. Use-case: Used anywhere in Sass stylesheet to embed the result of a SassScript expression into a chunk of CSS
	1. Syntax: Wrap expression in `#{}` in any of the following places:
		1. Selectors in style rules
		2. Property names in declarations
		3. Custom property values
		4. CSS at-rules
		5. @extends
		6. Plain CSS @imports
		7. Quoted or unquoted strings
		8. Special functions
		9. Plain CSS function names
		10. Loud comments
2. Example:

		@mixin corner-icon($name, $top-or-bottom, $left-or-right) {
			.icon-#{$name} {
				background-image: url("/icons/#{$name}.svg");
				position: absolute;
				#{$top-or-bottom}: 0;
				#{$left-or-right}: 0;
			}
		}

		@include corder-icon("main", top, left);

		// CSS
		.icon-main {
			background-image: url("/icons/main.svg");
			position: absolute;
			top: 0;
			left: 0;
		}

#### In SassScript ####
1. Interpolation can be used in SassScript to inject SassScript into unquoted strings
	1. Useful when dynamically generating names (example for animations)
	2. Useful when using slash-separated values
2. **Interpolation in SassScript always returs an unquoted string**
3. Example:

		@mixin inline-animation($duration) {
			$name: inline-#{unique-id()};

			@keyframes #{$name} {
				@content;
			}

			animation-name: $name;
			animation-duration: $duration;
			animation-iteration-count: infinite;
		}

		.pulse {
			@include inline-animation(2s) {
				from { background-color: yellow }
				to { background-color: red }
			}
		}

		// CSS
		.pulse {
			animation-name: inline-sdgs9s7d;
			animation-duration: 2s;
			animation-iteration-count: infinite;
		}
		@keyframes inline-sdgs9s7d {
			from { 
				background-color: yellow;
			}
			to { 
				bacground-color: red; 
			}
		} 

4. Fun fact:
	1. Interpolation is useful for injecting values into strings
		1. It is rarely used in SassScript expressions
			1. It doesn't have to be used as variable in a property value

					color: #{$accent}; // This is not required
					color: $accent;

5. Heads up!
	1. Interpolation must not be used with numbers
		1. Why? Interpolation returns unquoted strings that can't be used for any further math.
			1. Avoids Sass's built-in safeguards to ensure that units are used correctly.
				1. Solution: Sass unit arithmetic
					1. Instead of writing `#{$width}px`, we can write `${width} * 1px`
						1. Another solution: Declare `$width` variable in `px`
							1. We get nice error messages if `$width` already has units

#### Quoted Strings ####
1. Quotation marks around quoted strings are removed (even if the quoted strings are in lists)
	1. Advantage: Allows writing quoted strings with syntax not allowed in SassScript (like selectors) which can be interpolated into style rules.
2. Example:

		.example {
			unquoted: #{"string"};
		}

		// CSS
		.example {
			unquoted: string;
		}

	1. Tip: Don't use interpolation to convert quoted strings to unquoted strings (it is not clear)
		1. Use `string.unquote()` function
			1. `string.unquote($string)`

### At-Rules ###
#### Overview ####
1. Sass's extra functionality comes in the form of `at-rules` it adds on top of CSS:
	1. `@use` - loads mixins, functions, variables from other Sass stylesheets
		1. Combines CSS from multiple stylesheets together
	2. `@forward` - Loads a Sass stylesheet and makes its mixins, functions, and variables avaialable when your stylesheet is loaded with `@use` rule (?)
	3. `@import` - extends the CSS at-rule to load styles, mixins, functions, and variables from other stylesheets
	4. `@mixin` and `@include` - Makes it easy to use chunks of styles
	5. `@function` - defines custom functions that can be used in SassScript expressions.
	6. `@extend` - allows selectors to inherit styles from one another.
	7. `@at-root` - Puts styles within it at the root of the CSS document
	8. `@error` - causes compilation to fail with an error message.
	9. `@warn` - prints a warning without stopping compilation entirely.
	10. `@debug` - prints a message for debugging purposes
	11. Flow control rules like `@if`, `@each`, `@for`, and `@while` controls whether or how many times styles are emitted.
2. Sass lso has special behavior for plain CSS at-rules
	1. They can contain interpolation
	2. They can be nested in style rules
	3. `@media`, and `@supports` allow SassScript to be used directly in the rule itself without interpolation

#### @use ####
1. `@use` - rule loads mixins, functions, and variables from other Sass stylesheets

#### @forward ####
#### @import ####
#### @mixin and @include ####
#### @function ####
#### @extend ####
#### @error ####
#### @warn ####
#### @debug ####
#### @at-root ####

#### Flow Control ####
##### Overview #####
##### @if and @else #####
##### @each #####
##### @for #####
##### @while #####

#### From CSS ####

### Values ###
#### Overview ####
#### Numbers ####
#### Strings ####
#### Colors ####
#### Lists ####
#### Maps ####
#### true and false ####
#### Calculations ####
#### Functions ####
#### Mixins ####

### Operators ###
#### Overview ####
#### Equality ####
#### Relational ####
#### Numeric ####
#### String ####
#### Boolean ####

### Built-In Modules ###
#### Overview ####
#### sass:color ####
#### sass:list ####
#### sass:map ####
#### sass:math ####
#### sass:meta ####
#### sass:selector ####
#### sass:string ####

### Breaking Changes ###
#### Overview ####
#### Strict Unary Operators ####
#### Invalid Combinations ####
#### Media Queries Level 4 ####
#### / as Division ####
#### Function Units ####
#### -moz-document ####
#### Extending Compound Selectors ####
#### CSS Variable Syntax ####
#### Duplicate Variable Flags ####
#### Default Exports ####
#### Null Alpha Channel ####
#### abs() Percentage ####
#### Functions and Mixins Beginning with -- ####
#### Mixed Declearations ####
#### meta.feature-exists ####
#### Color Functions ####
#### Color JS API ####
#### Legacy JS API ####

### Command Line ###
#### Overview ####
#### Dart Sass ####
#### Ruby Sass ####
#### Migrator ####

### JavaScript API ###