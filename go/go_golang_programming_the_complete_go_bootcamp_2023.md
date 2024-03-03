# Go (Golang) Programming: The Complete Go Bootcamp 2023 #
## Section 1: Course Introduction ##
1. It is used to solve Google size problems
2. What is Go good for?
	1. Web-services at scale
	2. Networking
	3. Massively concurrent applications
	4. OSes
	5. Automation
	6. CLI tools
	7. Cryptography
3. Go is expressive, comprehensible, sophisticated, clean and clear, and easy to read
4. It is the next enterprise programming language
	1. It provides high performance like C and C++
	2. It provides super-efficient concurrency handling like Java
	3. It is fun to code like Python
5. Software written in Go
	1. Docker
	2. K8S
	3. Etherium
6. Other companies using Go
	1. Uber
	2. Netflix
	3. Pintarest
	4. Soundcloud
	5. ...
7. It is for large scaled engineering
8. Go is second top paying in the US

### Why Go Programming? Why now? ###
### IMPORTANT: Please read! ###
1. It is one of the most valuable technical skills to have right now

### Join Our Online Community! ###
1. [Online Discord Community](https://discord.com/invite/TeFg9HrZ46)
	1. Support
	2. To interact with course colleagues
	3. Help others
2. Companies use discord to communicate across teams
3. [Channel](https://www.youtube.com/c/andreidumitrescu)
	1. Programming
	2. Networking
	3. Information Security
	4. Blockchain
	5. Cutting-Edge Technologies

## Section 2: Getting Started ##
### The Go Playground. Your First Go Program ###
1. [go.dev/play](go.dev/play)
2. Playground infrastructure overview:

		Client
		  ^
		  |
		  HTTP
		  |
		  v
		App Engine
		Front End (many instances)
		  ^
		  |
		  RPC
		  |
		  v
		Playground Service
		Back End (many instances)

	1. For testing Go programming concepts
	2. We don't have to install anything on our machine
	3. Playground has some limitations
3. We are going to use playground & VS Code
4. Open [https://go.dev/play/](https://go.dev/play/)
	1. Run
		1. Sends code to Google servers
			1. The code will be executed in a protected environment and result is returned to the client
		2. Client prints the program output (browser)
	2. Format
		1. Idiomatic formatting
		2. It uses `gofmt` **(M)** utility (built into the language runtime)
5. Each go function is included in a package that must be imported

		import "fmt"

	1. It is an import path that uniquely identifies a package and imports it into the current program
		1. It corresponds to its location inside the workspace or remote repository
	2. `math` package

			import {
				"fmt"
				"math"
			}

			result := math.Pow(x, 8)
			fmt.Println("x to the power of 8 is ", result)

		1. Playground automatically imports the package
		2. Share: unique URL where code is saved
			1. We can use the URL to share the code
6. Google: search - golang standard library
	1. Search for: `time`
		1. Examples
			1. We can run directly
7. Alternatives:
	1. [goplay.space](goplay.space)
		1. It is a playground with many features such as syntax highlighting, live syntax error checking, auto-closing braces and quotes, auto-indentation, ...

### Setup the Programming Environment on Windows (Go, Git, and VSCode) ###
1. Installing Go on Windows, Git, VS Code
2. Open Browser:
	1. Open [golang.org/dl/](golang.org/dl/)
		1. Download the latest version for Windows
	2. Install
3. Open cmd
	1. `go` **(M)**
	2. `go version` **(M)**
4. Git:
	1. Most widely used, modern version control system in the world
	2. It keeps track of every change we make to a file
	3. It contains the minimum version of bash shell for windows
	4. It integrates will with VS Code
	5. [gitforwindows.org](gitforwindows.org)
		1. Install
			1. Select All components except the last one
			2. Default editor:
				1. Switch to VS Code after installing VS Code
			3. Checkout as-is
			4. Install
5. VS Code
	1. [code.visualstudio.com](code.visualstudio.com)s
	2. Download
	3. Install
		1. Check all the boxes
		2. Install
	4. Launch
	5. Configuration
		1. Extension
			1. Search: go
				1. Go Team at Google
		2. Restart VS Code
	6. Go to View > Command Palette
		1. gotools
			1. Install/Update tools
			2. Check all the boxes (to install all necessary go tools)
			3. Ok
		2. Ctrl+Shift+P or F1
			1. Command Palette: Select default profile
				1. Git Bash
		3. Changing theme
			1. File > Preferences > Settings
				1. theme
					1. Workbench Color Theme
						1. Light

### Setup the Programming Environment on Linux (Go and VSCode) ###
### Setup the Programming Environment on MacOS (Go, Git, and VSCode) ###
### Code Organization ###
1. Older versions of go wanted us to organize code in a specific way
	1. With go 1.13 - it supports modules
		1. Organizing code is not important
			1. We can construct directory structure anywhere on the drive and put our go source-code files there
			2. We will put code in single workspace
				1. It is just a directory where our code resides
				2. The workspace path is stored in an environment variable called `GOPATH`
					1. `C:\Users\ad\go` - Windows
					2. `~/go` - Linux and MacOS
2. We can print the environment variables:

		go env #**(M)**

	1. Workspace directory
		1. `bin`
			1. Contains compiled and executable go programs
				1. When we run `go install` on a program directory, go will put exe files under this folder
		2. `src`
			1. Contains the source files for own and other downloaded packages
			2. Sub-directory can be instantiated anywhere we want
				1. File explorer:
					1. `master_go_programming` (no whitespaces)
						1. Whitespaces are special chars
						2. Use: `_`, `-`
						3. Each program is created inside a sub-directory inside this directory
		3. `pkg`
			1. Contains package objects aka package archives
				1. They are non-executable files
					1. Shared libraries ending in `.a`
			2. It contains the compiled and packaged binary code which is customized for:
				1. Machine architecture
				2. Go version
			3. We cannot run the the packages directly
				1. They are not binary files
			4. They are imported and used inside other executable packages

### The Struture of a Go Application ###
1. VS Code: `master_go_prgramming`
	1. `application_structure`
		1. `main.go` - begins with a package declaration (indicates what the file is part of)
			1. Every go program must be included in a package

					package main

			2. It is an executable package
				1. Generates standard executable file that can be run
				2. Name of an executable package is pre-defined and it is always called `main`
				3. The package must also have a function called `main`
			3. Package declaration is followed by import statements
			4. Then sequence of package level declarations
				1. Variables
				2. Constants
				3. Functions
				4. Types
					1. (any order)
			5. Example:

					package main

					import "fmt"

					const secondsInHour = 3600

					func main() {
						fmt.Println("Hello Go World")
						distance := 60.8s
						fmt.Printf("The distance in miles is %f", distance * 0.621)
					}

				1. `fmt` - a standard library package included in Go
					1. It is used to format strings printed to the output
				2. Running:
					1. Open terminal:
						1. Go to directory that contains `main.go`
						2. Run the command:

								go run main.go # **(M)**

						3. If module error:
						
								go mod init # **(M)**
								go run main.go

					2. Ctrl + F5
						1. Allow access

### Coding - Go Application Structure ###
1. Example:

		/////////////////////////////
		// The Typical structure of a Go Application
		// Go Playground: https://play.golang.org/p/VY_IeYBb1GN
		/////////////////////////////

		// a package clause starts every source file

		// main is a special name declaring an executable rather than
		// a library (package)

		package main

		// import declaration declares packages used in thsi file
		import "fmt"

		// package scoped variables and constants
		var x int = 100

		const y = 0

		// a function declaration. main is a special function name
		// it is the entry point for the executable program
		// Go uses braces brackets to delimit code blocks
		func main() {
			// local Scoped Variables and Constants Declarations, calling functions etc
			var a int = 7
			var b float64 = 3.5
			const c int = 10

			// Println() function prints out a line to stdout
			// It belongs to package fmt
			fmt.Println("Hello Go world!") // => Hello Go world!
			fmt.Println(a, b, c)           // => 7 3.5 10
		}

### Quiz 1: Test Your Knowledge: Getting Started with Go ###
### Compiling (go build) and Running Go Applications (go run) ###
1. More ways to compile and run go program
	1. Even on different OSs
	2. Ways:
		1. Ctrl + F5 (VS Code)
			1. Go command:
				1. go is a tool for managing Go source code
					1. `go run`: it compiles and runs the application
						1. It doesn't produce an executable
							1. `go run file.go` **(M)** - compiles and immediately runs the Go program
								1. We can move the the program directory (directory that contains main.go) and execute `go run main.go`
								2. `go run -x main.go` **(M)** - to see details of the compilation process
					2. `go build`: it just compiles the application.
						1. It produces an executable
							1. `go build file.go` **(M)** - Compiles a bunch of Go source files
								1. It compiles packages and dependencies
								2. If you ru `go build`, it will compile the files in the current directory and will produce **an executable file with the name of the current working directory**
								3. `go build -o app` will produce an executable file call `app`

### Go Packages and Modules ###
### Formatting Go Source Code (gofmt) ###
### Quiz 2: Test Your Knowledge: Formatting Code, Compiling, and Running Go Applications ###

## Section 3: Challenge Hands-On Exercises - Getting Started ##
### Hands-On Exercises ###

## Section 4: Go Basics ##
### Variables in Go ###
### Multiple Declarations ###
### Coding - Variables and Declarations ###
### Quiz 3: Test Your Knowledge: Variables and Declarations ###
### Types and Zero Values ###
### Coding - Types and Zero Values ###
### Comments ###
### Naming Conventions in Go ###
### Coding - Comments and Naming Convention ###
### Quiz 4: Test Your Knowledge: Types, Zero Values, Comments and Conventions ###
### Package fmt ###
### Coding - Package fmt ###
### Quiz 5: Test Your Knowledge: Package fmt ###
### Constants in Go ###
### Constant Rules ###
### Constant Expressions. Typed vs. Untyped Constants ###
### IOTA ###
### Coding - Constants and IOTA ###
### Quiz 6: Test Your Knowledge: Constants ###
### Go Data Types - Part 1 ###
### Go Data Types - Part 2 ###
### Coding - Go Data Types ###
### Quiz 7: Test Your Knowledge: Go Data Types ###
### Operations on Types: Arithmetic and Assignment Operators ###
### Comparison and Logical Operations ###
### Coding - Go Operators ###
### Overflows ###
### Converting Numeric Types ###
### Converting Numbers to Strings and Strings to Numbers ###
### Coding - Converting Types ###
### Quiz 8: Test Your Knowledge: Operators and Conversions ###
### Defined (Named) Types - Part 1 ###
### Defined (Named) Types - Part 2 ###
### Coding - Defined Types ###
### Alias Declarations ###
### Coding - Aliases ###
### Quiz 9: Test Your Knowledge: Defined Types and Aliases ###

## Section 5: Coding Challenges - Go Basics ##
### Declare Variables ###
### Constant ###
### Package fmt ###
### Operators and Conversions ###
### Named Types and Aliases ###

## Section 6: Program Flow Control in Go ##
### If, Else If and Else Statements ###
### Coding - If, Else If, and Else ###
### Command Line Arguments: os.Args ###
### Coding - Command Line Arguments ###
### Simple If Statement ###
### Coding - Simple If ###
### Quiz 10: Test Your Knowledge: If, Else If, and Else Statements ###
### For Loops ###
### Where is the While Loop in Go? ###
### Coding - For Loops ###
### For and Continue Statements ###
### For and Break Statements ###
### Coding - For, Break, and Continue ###
### Quiz 11: Test Your Knowledge: For Loops ###
### Label Statement ###
### Goto ###
### Coding - Labels and Goto Statements ###
### Switch Statement ###
### Quiz 12: Test Your Knowledge: Label, Goto, and Switch Statements ###
### Coding - Switch Statement ###
### Scopes in Go ###
### Coding - Scopes ###
### Quiz 13: Test Your Knowledge: Scopes ###

## Section 7: Coding Challenges - Flow Control ##
### Coding Challenge Exercises - Flow Control ###

## Section 8: Arrays in Go ##
### Intro to Arrays ###
### Delaring Arrays ###
### Array Operations ###
### Coding - Declaring Arrays and Operations ###
### Arrays with Keyed Elements ###
### Coding - Arrays with Keyed Elements ###
### Quiz 14: Test Your Knowledge: Arrays ###

## Section 9: Coding Challenges - Arrays ##
### Array Coding Exercises ###

## Section 10: Slices in Go ##
### Intro to Slices ###
### Declaring Slices and Basic Slice Operations ###
### Comparing Slices ###
### Coding - Slice Basics ###
### Appending to a Slice. Copying Slices ###
### Quiz 15: Test Your Knowledge: Slice Basics ###
### Slice Expressions ###
### Coding - Slice Expressions ###
### Slice Internals: Backing Array and Slice Header - Part 1 ###
### Slice Internals: Backing Array and Slice Header - Part 2 ###
### Coding - Slice's Backing Array ###
### Append, Length and Capacity In-Depth ###
### Coding - Appending to Slices ###
### Quiz 16: Test Your Knowledge: Slice Expressions and Slice Header ###

## Section 11: Coding Challenges - Slices ##
### Coding Challenge Exercices - Slices ###

## Section 12: Strings, Runes, Bytes and UTF-8 in Go ##
### Intro to Strings ###
### Coding - String Basics ###
### Quiz 17: Test Your Knowledge: Strings Basics ###
### Intro to Rules, Bytes and Unicode Code Points ###
### Coding Rules and Strings. Decoding Strings Byte by Byte and Rune by Rune ###
### String Length in Bytes and Runes ###
### Coding - Strings, Runes and Decoding ###
### Slicing Strings ###
### Coding - Slicing Strings ###
### Quiz 18: Test Your Knowledge: Strings, Runes, Decoding ###
### String Package Part1: Contains, ContainsAny, Count, ToLower, ToUpper, EqualFold ###
### Strings Package Part2. Manipulating Strings: Repeat, Replace, Split, Join, Field ###
### Coding - Strings Package ###
### Quiz 19: Test Your Knowledge: Strings Package ###

## Section 13: Coding Challenges - Strings ##
### Coding Challenge Exercises - Strings ###

## Section 14: Maps in Go ##
### Intro to Maps ###
### Declaring Maps, Working with Maps ###
### Comparing Maps ###
### Map Header, Cloning Maps ###
### Coding - Maps in Go ###
### Quiz 20: Test Your Knowledge: Maps ###

## Section 15: Coding Challenges - Maps ##
### Coding Challenge Exercises - Maps ###

## Section 16: Working with Files in Go ##
### Open, Close, Rename, Move, Remove Files ###
### Coding - Operations on Files ###
### Writing Bytes to File: os.Write and ioutil.WriteFile ###
### Coding - Writing to Files Using os and ioutil ###
### Writing to Files using a Buffered Writer (bufio Package) ###
### Coding - Writing to Files Using a Buffer in Memory ###
### Reading n Bytes from a File. Reading a File using a Buffered Reader ###
### Coding - Reading Bytes from Files ###
### Reading a File Line by Line Using a Scanner ###
### Coding - Reading Files Using a Delimiter ###
### Scanning for User Input. Reading From Stdin ###
### Coding - Reading from Console ###
### Quiz 21: Test Your Knowledge: Working with Files ###

## Section 17: Coding Challenges - Working with Files ##
### Coding Exercises - Working with Files ###

## Section 18: Structs in Go ##
### Organizing Data with Structs ###
### Constructing Structs ###
### Retrieving and Updating Struct Fields ###
### Coding - Working with Structs ###
### Anonymous Structs and Anonymous Struct Fields ###
### Embedded Structs ###
### Coding - Anonymous and Embedded Structs ###
### Quiz 22: Test Your Knowledge: Structs ###

## Section 19: Coding Challenges - Structs ##
### Coding Challenge Exercises - Structs ###

## Section 20: Functions in Go ##
### Intro to Functions ###
### Function Parameters, Arguments and Return Values ###
### Coding - Function Basics ###
### Quiz 23: Test Your Knowledge: Function Basics ###
### Variadic Functions - Part 1 ###
### Variadic Functions - Part 2 ###
### Coding - Variadic Functions ###
### Defer Statement ###
### Coding - Defer Statement ###
### Anonymous Functions ###
### Coding - Anonymous Functions ###
### Quiz 24: Test Your Knowledge: Functions in Depth ###

## Section 21: Coding Challenges - Functions ##
### Coding Challenge Exercises - Functions ###

## Section 22: Pointers in Go ##
### Computer Memory and Pointers ###
### Declaring Pointers, Address of and Dereferencing Operators ###
### Pointer to Pointer. Comparing Pointers ###
### Coding - Pointer Basics ###
### Passing and Returning Pointers From Functions - Part 1 ###
### Passing Pointers to Functions. Passing by Value vs. Passing by Pointer - Part 2 ###
### Coding - Passing Values and Pointers to Functions ###
### Quiz 25: Test Your Knowledge: Pointers ###

## Section 23: Coding Challenges - Pointers ##
### Coding Challenge Exercises - Pointers ###

## Section 24: Methods and Interaces in Go (OOP) ##
### Receiver Functions (Methods) ###
### Coding - Intro to Methods ###
### Methods with a Pointer Receiver ###
### Coding - Methods with a Pointer Receiver ####
### Quiz 26: Test Your Knowledge: Methods ###
### Intro to Interfaces ###
### Implementing Interfaces ###
### Coding - Implementing Interfaces ###
### Interface Dynamic Type and Polymorphism ###
### Type Assertions and Type Switches ###
### Coding - Type Assertions ###
### Embedded Interfaces ###
### Empty Interface ###
### Coding - Empty Interface ###
### Quiz 27: Test Your Knowledge: Interfaces ###

## Section 25: Coding Challenges - Methods and Interfaces ##
### Coding Challenge Exercises - Methods ###
### Coding Challenge Exercises - Interfaces ###

## Section 26: Concurrency in Go ##
### Concurrency vs. Parallelism ###
### Intro to Goroutines ###
### Spawning Goroutines. The go Keyword ###
### Coding - Getting Information ###
### WiatGroups ###
### Coding - Goroutines and WaitGroups ###
### Project: URL Checker and Page Downloader ###
### Project Refactoring Using WaitGroups: URL Checker and Page Downloader ###
### Data Race ###
### Go Race Detector ###
### Coding - Data Race ###
### Mutexes ###
### Coding - Mutexes ###
### Intro to Channels ###
### Coding - Intro to Channels ###
### Goroutines and Channels ###
### Goroutines, Channels and Anonymous Function ###
### Coding - Goroutines and Channels ###
### Project Refactoring Using Channels: URL Checker and Page Downloader ###
### Project Refactoring Using Channels and Anonymous Function ###
### Unbuffered Channels ###
### Coding - Unbuffered Channels ###
### Buffered Channels ###
### Coding - Buffered Channels ###
### Select Statement ###
### Coding - Select Statement ###
### Quiz 28: Test Your Knowledge: Concurrency in Go ###

## Section 27: Coding Challenges - Concurrency ##
### Coding Challenge Exercises - Goroutines, WaitGroups and Mutexes ###
### Coding Challenge Exercises - Goroutines and Channels ###

## Section 28: Go Packages and Modules ##
### Go Packages Overview ###
### Constructing a Package ###
### GOPATH and Packages in Depth ###
### Exporting Names. Private vs. Private Access ###
### Import Statement and Scopes ###
### The Init Function ###
### Quiz 29: Test Your Knowledge: Go Packages ###
### Importing and Using Go Modules ###
### Constructing Your Own Go Module ###
### Publish the Module on GitHub. Semantic Versioning ###
### Commands - Construct and Publish a Module on GitHub ###
### Releasing a Bug Fix and a Minor Update ###
### Releasing a Major Update ###
### Using Multi-Version Dependency ###
### Quiz 30: Test Your Knowledge: Go Modules ####

## Section 29: Challenge Hands-On Exercises - Packages and Modules ##
### Hands-On Exercises ###

## Section 30: [APPENDIX] Linux Administration ##
### Installing Ubuntu in a VM ###
### Things to Do After Installing Ubuntu ###
### Terminals, Consoles, Shells and Command ###
### Linux Command Structure ###
### Getting Help, Map Pages (man, type, help, apropos) ###
### Mastering the Terminal: The TAB Key ###
### Mastering the Terminal: Keyboard Shortcuts ###
### Mastering the Terminal: The Bash History ###
### root vs. Non-privileged Users. Getting root Access (sudo, su, passwd) ###
### Intro to The Linux Files System ###
### The Filesystem Hierarchy Standard (FHS) ###
### Absolute vs. Relative Paths. Walking through the File System (pwd, cd, tree) ###
### The LS Command In Depth (ls) ###
### Understanding File Timestamps: atime, mtime, ctime (stat, touch, date) ###
### Sorting Files by Timestamp ###
### File Types in Linux (ls -F, file) ###
### Viewing Files - Part 1 (cat) ###
### Viewing Files - Part 2 (less, more) ###
### Viewing Files - Part 3 (tail, head, watch) ###
### Constructing Files and Directories (touch, mkdir) ###
### Copying Files and Directories (cp) ###
### Moving and Renaming Files and Directories (mv) ###
### Removing Files and Directories (rm, shred) ###
### Working With Pipes in Linux (|, wc) ###
### Command Redirection (>, >>, 2> &>, cut, tee) ###
### Finding Files and Directories - Part 1 (locate, which) ###
### Finding Files and Directories - Part 2 (find) ###
### Find and Exec ###
### Searching for String Patterns in Text Files (grep) ###
### Searching for Strings in Binary Files (strings) ###
### Comparing Files (cmp, diff, sha256) ###
### Compressing and Archiving Files and Directories (tar, gzip) ###
### Hard Links and the lnode Structure ###
### Working With Symlinks. Symlinks vs. Hard Links ###

## Section 31: BONUS SECTION ##
### Congratulations ###
### BONUS: THANK YOU GET ###