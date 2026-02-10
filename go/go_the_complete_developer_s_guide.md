# Go: The Complete Developer's Guide (Golang) #
## Section 1: Getting Started ##
### How to Get Help ###
### Course Resources ###
1. [diagrams](https://www.udemy.com/course/go-the-complete-developers-guide/learn/lecture/7830456#overview)
	1. [diagrams.net](https://www.diagrams.net/)

### Join Our Community! ###
1. [https://discord.gg/h2G3CbxPZA](https://discord.gg/h2G3CbxPZA)

### Environment Setup ###
1. Steps:
	1. Install Go - https://golang.org/dl/
		1. Runtime to build and execute Go programs
	2. Install VS Code - https://code.visualstudio.com/
		1. Code editor with awesome Go integration
	3. Configure VSCode
		1. Install Golang extension
			1. Easier to debug, write, format, etc.
	4. Write code!
		1. The fun part!
2. [https://golang.org/dl/](https://golang.org/dl/)

### VSCode Installation ###
1. Go installation:

```golang
go # prime tool - build, compile, test, ...
```

2. VSCode Installer

### Go Support in VSCode ###
1. Extensions
	1. go
		1. Rich Go language support for Visual Studio
		2. It needs extra tools to function properly
			1. Close editor
			2. Start again
				1. Open code editor window open (new file)
					1. Bottom right: Click on Plain Text
						1. Go
							1. Analysis tools missing.

### Gopls, undeclared name, and module errors in VSCode ###
1. Each directory should have only a single project

## Section 2: A Simple Start ##
### Boring OI' Hello World ###
1. New project folder: helloworld
2. main.go

```go
package main

import "fmt"

func main() {
  fmt.Println("Hi there!")
}
```

### Five Important Questions ###
1. Questions:
	1. How do we run the code in our project?
		1. Terminal:
			1. `go run main.go` **(M)**
		2. Go CLI:
			1. `go build` - compiles a bunch of go source code files
				1. Compiles only and doesn't execute
					1. Generates `main.exe` (Windows)
			2. `go run` - compiles and executes one or more files
				1. list of files are provided
			3. `go fmt` - formats all the code in each file in the current directory
			4. `go install` - compiles and "installs' a package
			5. `go get` - Downloads the raw source code of someone else's package
			6. `go test` - runs any tests associated with the current project
	2. What does 'package main' mean?
	3. What does 'import "fmt"' mean?
	4. What's that 'func' thing?
	5. How is the main.go file organized?

### Go Packages ###
1. `package`
	1. A project or workspace
		1. A collection of common source-code files
	2. `package main`
		1. `main.go` - each file must declare the package it belongs to
		2. `support.go`
		3. `helper.go`
	3. Why `main`?
		1. Types of packages
			1. Executable
				1. Generates a file we can run (after compile)
				2. For doing something
			2. Reusable
				1. Code used as 'helpers'. Good place to put reusable logic.
				2. Code dependencies or libraries
					1. Helper functions
					2. ...
		2. `package main`
			1. Name determines the type of package
				1. `main` - Is used for executable type of package
			2. Any other name, it will not spit out an executable
			3. Defines a package that can be compiled and then *executed*. Must have a func called 'main'
		3. `package calculator`
			1. Defines a package that can be used as a dependency (helper code)
			2. Reusable package

### Import Statements ###
1. `import` - to give our package access to code written in another package
	1. Give `main` package access to all the code in `fmt` package
		1. `fmt` - Standard library package (format)
			1. Used to print out information - especially to terminal
			2. Other packages:
				1. `debug`
				2. `math`
				3. `encoding`
				4. `crypto`
				5. `io`
		2. We can import packages of other engineers as well
		3. Standard library packages: [golang.org/pkg](golang.org/pkg)

### File Organization ###
### How to Access Course Diagrams ###

## Section 3: Deeper Into Go ##
### Project Overview ###
### New Project Folder ###
### Variable Declarations ###
### Functions and Return Types ###
### Slices and For Loops ###
### OO Approach vs Go Approach ###
### Custom Type Declarations ###
### Receiver Functions ###
### Constructing a New Deck ###
### Slice Range Syntax ###
### Multiple Return Values ###
### Byte Slices ###
### Deck to String ###
### Joining a Slice of Strings ###
### Saving Data to the Hard Drive ###
### Reading From the Hard Drive ###
### Error Handling ###
### Shuffling a Deck ###
### Random Number Generation ###
### Constructing a go.mod File ###
### Testing With Go ###
### Errorf call has arguments but no formatting directives ###
### Writing Useful Tests ###
### Asserting Elements in a Slice ###
### Testing File IO ###
### Project Review ###
### Assignment: Even or Odd? ###
### Even or Odd Solution ###

## Section 4: Organizing Data With Structs ##
### Structs in Go ###
### Defining Structs ###
### Declaring Structs ###
### Updating Struct Values ###
### Embedding Structs ###
### Structs with Receiver Functions ###
### Pass By Value ###
### Structs with Pointers ###
### Pointer Shortcut ###
### Gotchas With Pointers ###
### Reference vs Value Types ###

## Section 5: Maps ##
### What's a Map? ###
### Manipulating Maps ###
### Interating Over Maps ###
### Differences Between Maps and Structs ###

## Section 6: Interfaces ##
### Purpose of Interfaces ###
### Problems Without Interfaces ###
### Interfaces in Practice ###
### Rules of Interfaces ###
### Extra Interface Notes ###
### The HTTP Package ###
### Reading the Docs ###
### More Interface Syntax ###
### Interface Review ###
### The Reader Interface ###
### More on the Reader Interface ###
### Working with the Read Function ###
### The Writer Interface ###
### The io.Copy Function ###
### The Implementation of io.Copy ###
### A Customer Writer ###
### Assignment: Interfaces ###
### Interfaces Solution ###
### Assignment: Hard Mode Interfaces ###
### Hard Mode Interfaces Solution ###

## Section 7: Channels and Go Routines ##
### Website Status Checker ###
### Printing Site Status ###
### Serial Link Checking ###
### Go Routines ###
### Theory of Go Routines ###
### Channels ###
### Channel Implementation ###
### Blocking Channels ###
### Receiving Messages ###
### Repeating Routines ###
### Alternative Loop Syntax ###
### Sleeping a Routine ###
### Function Literals ###
### Channels Gotcha! ###

## Section 8: Extras ##
### Bonus! ###