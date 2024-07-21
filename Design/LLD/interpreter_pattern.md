# Interpreter Design Pattern #
## Intent ##
1. Consider a language
	1. Define a representation of its grammar
	2. Define an interpreter that uses the representation to interpret sentences in the language
2. Process:
	1. Map a domain to language
	2. Map a language to grammar
	3. Map a grammar to a hierarchical object-oriented design

## Problem ##
1. A class of problems occurs in a well-defined and well-understood domain
	1. If domain is characterized by a "language", then problems can be solved with interpreation "engine"

## Discussion ##
1. Interpreter pattern:
	1. Defining a domain language as a simple language grammar
		1. Problem characterization
	2. Representing domain rules as language sentences
	3. Interpreting sentences to solve the problem
2. Each grammar rule is represented as a class
	1. Since grammars are usually hierarchical in structure, an inheritance hierarchy of rule classes maps nicely
3. Abstract base class specifies the method `interpret()`
	1. Each concrete subclas implements `interpret()`
		1. It accepts the current state of the language stream
		2. It adds its contribution to the problem solving process

## Structure ##
1. The domain is modeled using a recursive grammar
	1. Each rule in the grammar is either 'composite' (a rule that references other rules) or a terminal (a leaf node in a tree structure)
2. Interpreter relies on recursive traversal of Composite pattern to interpret 'sentences' it is asked to process
3. Structure:

		Cliet ---> AbstractExpression <<interface>>
					+ solve(inout Context)
						 ^
						/_\
						 |
					+----+----------------+
					|					  |
					TerminalExpression	CompoundExpression
											+ solve(inout Context)

	1. CompountExpression
		1. Perform "parent" functionality then delegate to each "child" element.
		2. "Context" is data structure for holding input and output

## Example ##
## Check List ##
1. Decide if a "little language" offers a justifiable return on investment
2. Define a grammar for the language
3. Map each production in the grammar to a class
4. Organize the suite of classes into the structure of the Composite pattern
5. Define an `interpet(Context)` method in the Composite hierarchy
6. The `Context` object encapsulates the current state of the input and output as the former is parsed and the latter is accumulated. It is manipulated by each grammar class as the "interpreting" process transforms the input into the output.

## Rules of Thumb ##
