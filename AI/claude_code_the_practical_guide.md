# Claude Code - The Practical Guide #
## Section 1: Getting Started ##
### Welcome to this course ###
1. Basics and advanced
2. Complete example project
	1. Features in action

### Course Overview ###
1. Claude Code
	1. Generates code with AI
2. Use-cases:
	1. Vibecoding
		1. Go with the flow
		2. No code-specific instructions
		3. No code reviews
	2. Agenting engineering
		1. Developer stays in control
		2. Specific instructions regarding libraries, patterns, etc.
		3. Code reviews
3. To produce high quality code
4. Topics:
	1. Setup 
	2. Configuration
	3. Base usage
	4. Context management
	5. Memory & instructions
	6. MCP
	7. Subagents
	8. Skills & rules
	9. Hooks
	10. Plugins
	11. Patterns & use-cases

### Caude Code Setup ###
1. Setup
	1. Available for all OSs
	2. CLI tools
	3. VS Code
		1. Bare-bones Next.js project
		2. `claude`
			1. It will execute commands
			2. Reads files
			3. ...

### Claude Coe in Different Terminals ###
1. [Supported shortcuts](https://code.claude.com/docs/en/interactive-mode)
2. [Terminal configuration instructions](https://code.claude.com/docs/en/terminal-config)

### Using Bun ###
1. Bun runtime
	1. [Bun installation](https://bun.com/docs/installation)

### Base Usage & IDE Integration ###
1. `PORT=3008 bun run dev`
2. Claude: `Replace the starting page of this Next.js project with a page that says "Hello World", centered in the middle of the screen`
3. Install **Claude Code for VS Code extension** in VS Code.
4. Other option: Command pallette - Claud code
	1. New window - UI
		1. Browse conversations
		2. New conversations

### A Glimpse at the Claude Desktop App ###
1. Desktop app
	1. Modes:
		1. Chat mode
		2. Cowork - general assistant tool
		3. Code
	2. New session
		1. Select folder (project folder)
			1. Put prompts here
2. Mobile app
	1. Chat mode
	2. Code mode
		1. Dispatch and manage cloud tasks
		2. etc...

### Configuring Claude Code ###
1. How to configure?
	1. Global - on system (team members for enterprise)
		1. `.claude/settings.json`
			1. Global settings
		2. Tweaking
			1. `/config` (Claude)
				1. Browse through and change values
					1. Select `Theme` and change
				2. `Thinking mode` - `false` (to save tokens)
2. Documentation - all settings
3. `permissions`
	1. deny: `.env` (not allow Claude code to read sensitive data)
		1. Deny read, write, and execute
4. Project specific claude config
	1. `.claude`
		1. `settings.json` (overrides global settings)
		2. `settings.local.json` (overrides both global and settings.json. It is not checked into source control)

### Choosing AI Models ###
1. Command: `/model` - to choose an AI model we want to use
	1. `Opus` - most capable model offered by Anthropic
	2. `Alt + p` to change the model

### Understanding Sessions & Context ###
1. `/` - shows commands
	1. `/clear` - clears current session and the context window related to the session
		1. Another approach: Open new terminal and run `claude`
	2. `/context` - tells us how the context window for this session is currently being occupied
		1. System prompt - set up by Anthropic engineers
		2. System tools - tool descriptions exposed to claude code - gives hints to claude code on when to use which tool
		3. MCP tools
		4. Free space
		5. Autocompact buffer
			1. If we reach limit of the context window for the session, Claude code compacts it by generating a summary of the work that was done and what needs to be done. It throws away the old context. Claude code continues based on the summary
			2. Reserved. We cannot use those tokens
	3. `/usage`

### When to Start New Sessions & Making Sense of Compaction ###
1. Some details of the conversation can be lost due to compaction.
2. Compaction can be manually triggered using `/compact`
	1. Useful if we know that we might require lots of free space in the context window
3. It is better to keep sessiosn concise and focussed - since compaction will lead to loss of information
	1. Solution: Start new Claude Code instance in new terminal window via `/clear` command
4. If Claude Code can't fix a certain bug or just won't implement a feature the way we want it to, it is better to try again in a new session with cleared context window.

### Core Features You May Not Know Yet ###
1. `claude <prompt>`
	1. `claude "explain this project"`
		1. Generates answer right away
			1. Used to know about the code
	2. `claude -p "explain this project"` - runs in background and outputs response
	3. `/resume` - browse sessions and jump to a session
	4. `claude -c` - starts with last session

### Advanced Permissions Management ###
1. Shift + Tab
	1. Accept edits mode
2. It prompts for other commands (git commit, etc.)
3. To skip prompts for everything:
	1. `claude --dangerously-skip-permissions` **(M)**
		1. It still cannot access directories outside project
			1. It can erase files
			2. Can write script to do something outside the project and run it
				1. It can delete the root folder and destroy the system

### Running Claude Code via Docker Sandboxes ###
1. Two approaches to run in a safe mode
	1. `docker sandbox run claude` **(M)**
		1. Runs a sandbox
		2. Wraps local project in the sandbox
		3. Uses claude code in the sandbox and start it
			1. Starts it in `--dangerously-skip-permissions` mode
				1. Script cannot go out of the sandbox
		4. `sbx run claude` **(M)**

### Using Claude Code's Native Sandboxing ###
1. Claude's built-in sandbox
	1. `/sandbox`
		1. `auto-allow`
			1. Controls exfilteration of data (controls network access)
			2. Scopes to the project alone
			3. `settings.json` is updated
		2. `claude --dangerously-skip-permissions` - runs in sandbox mode

### Undoing Actions & The Importance of Version Control Systems ###
1. We may not be happy with the change
	1. Reverting:
		1. Option 1: Use Git
			1. `git log`
				1. Commit frequently
					1. Have version history
					2. Go back
				2. Use version control diff tools in VS Code
		2. esc + esc
			1. Rewind
				1. Beginning of the conversation
				2. Current snapshot
			2. Alternative:
				1. `/rewind` (it was buggy)

### Commands, Shortcuts & Settings Cheat Sheet ###
1. [claude-code-cli-settings-cheat-sheet](claude-code-cli-settings-cheat-sheet.jpg)

### Course Resources & Community ###
1. [https://github.com/academind/claude-code-course-resources](https://github.com/academind/claude-code-course-resources)
2. [https://academind.com/community/](https://academind.com/community/)

## Key Features & Efficient Usage ##
### Module Introduction ###
1. Web-application with JS + Next.js
2. Topics:
	1. Prompt & Context Engineering
	2. Plan Mode
	3. Memory Management & CLAUDE.MD
	4. Using Custom Subagents
	5. Working with Agent Skills

### Making Sense of Prompt & Context Engineering ###
1. Prompt & Context Engineering
	1. Providing the right information is key!
		1. Good input = good results
	2. Parts:
		1. Specific instruction(s)
			1. Clearly describes the task
		2. Relevant context / extra information (no unnecessary information)

### Prompt Engineering in Action & Working with Specs ###
1. Note-taking app
	1. Rich text editor
	2. View notes
	3. Manage notes
	4. Edit notes
	5. Delete notes
	6. Share notes publicly
2. How to work on it?
	1. Prompt (Chat GPT)
		1. Provide a specification and generate a technical specification document
		
		```
		I'm building a "Note Taking" web app.

		In this app, users will be able to add and manage notes. A "note" is simply a piece of text, created via a rich text editor (TipTap).

		In detail, authenticated (!) users will be able to:
		- add, view, update and delete notes
		- share notes publicly (and also stop sharing)

		I'll build the app using Next.js with Bun & TypeScript. For styling, we'll use TailwindCSS.
		Authentication will be implemented using the better-auth library, the rich text editor will be implemented using the TipTap library.
		I'll provide basic rich text formatting:
		- Bold, italic
		- 3 Heading Levels + Normal Text
		- Inline Code + Code Snippets
		- Bullet point lists
		- Horizontal separator lines

		The data will be stored as JSON in a SQLite database. I'll use Bun's built-in SQLite client with raw SQL statements.

		Do you need more information to construct me a technical specification document which I can use as a foundation to then build this application?
		```

3. Copy paste the technical specification markdown text in SPEC.md file
4. Run the following command in Claud CLI:

```
We're building an app described in @SPEC.md.

  Please format this file as proper markdown.

  Also update the file and update the part about the "users" table and auth-related tables.
  We're using the better-auth library which expects a certain database structure.

  Here's the official better-auth database documentation article:

  <better-auth-database-docs>
  [copy paste md content from https://better-auth.com/docs/adapters/sqlite]
  </better-auth-database-docs>
```

	1. `@SPEC.md` - refers to the file
	2. Copy paste content between xml tags for clarity (optional)

### Prompt & Context Engineering Recommendations ###
1. Writing good prompts and providing helpful context is essential for achieving good results
2. Recommendations/best practices
	1. **Concise & Precise**
		1. Keep prompts concise and focused.
		2. Don't overdo
		3. Accurately and clearly describe the task you want AI to tackle
		4. **Avoid including details that don't matter or unnecessary stuff**
	2. **No Unnecessary Context**
		1. Providing useful (!) context is crucial.
			1. Provicing context that actually doesn't matter can be counterproductive
				1. Avoid referending (`@some-file`) a file we **think** may matter.
					1. Focus on pointing at files we **know** matter.
				2. Avoid documentation atricles or any other kind of information that's not really relevant.
	3. **Think, Plan, Prompt**
		1. Don't just start typing and fix stuff over time.
			1. Think first
			2. Make a plan
			3. Write a good prompt
				1. If many follow-ups or clarifications, then put more effort into upfront planning
					1. Even when using "Plan" mode (use for non-trivial tasks)
	4. **Don't Test the AI**
		1. If we know that AI needs to overcome certain challenge, or if we know challenging part involved, don't hide that information from the AI
			1. Don't let AI struggle and fail
				1. Share all crucial information with the AI agent
		2. If we know of a particular pitfall or common mistake, include it (AND a recommended solution) in the initial prompt.
	5. **Explicitly Tell the AI About the Tools it should Use ##
		1. Claude Code can use many tools
			1. Built-in tools: Bash, web requests, etc.
			2. Some provided by MCP servers
			3. Other features
				1. Subagents
				2. Skills
		2. If we know that certain feature or tools should be used for a (part of a task), explicitly tell the AI to do so.
			1. Don't hope that the AI will automatically use the right tool or feature (even if it theoretically could)
3. **We must be in control. We must steer the AI**

### Initializing Claude Projects ###
1. Installing packages:
	1. `bun add better-auth zod @tiptap/react @tiptap/pm @tiptap/starter-kit`
		1. AI can install but can install older versions
	2. `bun add -D @types/bun` - To avoid typescript errors related to bun APIs
	3. New session: `/clear`
	4. `/init` **(M)**
		1. `CLAUDE.md` - important
			1. At least one in the root
			2. The content will automatically be loaded into every new session we instantiate with Claude code
				1. `/clear` - will load the file first
			3. It has relevant pieces of information that we think Claude code should have
			
			```json
			"scripts": {
				"dev": "bun run --bun next dev",
				"build": "bun run --bun next build",
				"start": "bun run --bun next start",
				...
			```
			
				1. Allows us to use bun APIs
				
			4. It will not be large
			5. Include the following in SPEC.md:
			
			```
			We're building the app described in @SPEC.md. Read the file for general architectural tasks or to double-check the exact database structure, tech stack or application architecture.
			
			Keep your replies extremely concise and focus on conveying the key information. No unnecessary fluff, no long code snippets.
			```
			
			6. We can add multiple CLAUDE.md files in subfolders
				1. Claude will load the files only if it works on the subfolders

### Crafting Great CLAUDE.MD Files ###
### CLAUDE.md vs "Auto Memory" ###
1. Two ways to manage general information:
	1. `CLAUDE.md` files
	2. Auto Memory

#### CLAUDE.md ####
1. They are maintained by us
2. It contians crucial, general information and instructions we want to provide to Claude Code for every (!) session into this file.
3. Keep the file focused and concise to avoid cluttering session context with unnecessary information or instructions (which would consume limited context window space and could lead to worse model performance).

#### Auto Memory ####
1. Additional feature
2. It is also about saving info & instructions and loading them into every new session
3. Claude Code autonomously stores important information or instructions
4. It stores the info in `MEMORY.md` files in a global `~/.claude/projects/<project>/memory/` path
5. Additionally, Claude Code can generate topic-specific memory files in that path (per project).
6. Claude loads first 200 lines of the `MEMORY.md` file for every new conversation.
7. Claude loads the entire `MEMORY.md` file for new session.
8. Claude can be configured (or taught) to keep the memory files concise.
9. Reasons:
	1. We don't have to think about everything that Claude needs to remember
		1. Solution: It tries to learn from our instructions
			1. It could store information/instructions related to an error it made
				1. Example: Code style we corrected Claude Code to use
10. `/memory` - to disable/enable the feature
	1. It also allows us to browse and edit the memory files belonging to our project
11. It is not a replacement for `CLAUDE.md`
	1. It is just an additional help which could lead to better results
12. If we have a certain piece of information or a specific instruction we want Claude Code to follow in our sessions, we don't hope it to memorize it
	1. We put it in `CLAUDE.md` file

### Leveraging Plan Mode ###
1. `/clear`
2. **Smaller and focused tasks leads to better results**
3. Instruction:
	
```
Let's start building the application described in @SPEC.md

Start by setting up the core route structure. Only add a dummy message to each page. No actual page content yet.

Just construct all those different page.tsx files for the different application routes. Don't implement authentication yet.
```

4. Switch to **plan mode** (Shift + tab)
	1. Use this mode for most tasks
	2. How does it work?
		1. Claude code gathers relevant information before starting work
		2. Claude code will ask more clarification questions if required
	3. **Helps turn average prompts into good prompts**
		1. Good prompts can become amazing prompts
	4. Claude code cannot edit files yet
	5. It explores the project and prepares a plan
		1. It saves plans locally, temporarily (it can have access to the plan)
			1. It can refer to them even if context window is cluttered up and needs to be cleared
	6. Displays the plan
		1. Options:
			1. `Yes, and use auto mode`
			2. `Yes, manually approve edits`
			3. `Tell Claude what to change`
				1. `I only want a single "/authenticate" route which supports only email + password auth`
					1. Goes back to planning mode and updates the plan
		2. Select the first option
			1. The code is generated

### Using Claude Code's Built-in Tools ###
1. More complex task:
	1. `/clear`
2. Prompt:

```
Implement authentication and database access as described in @SPEC.md .

Add a "lib" folder with "auth.ts" and "db.ts" files. Export a db handle in the db.ts file and make sure WAL mode is used and all required database tables are created if they don't exist yet.

# One of the following
```

	1. We can include links to official websites and ask Claude to go through (it can do that)
	
	```
	Visit the official docs websites:
	- https://bun.com/docs/runtime/sqlite
	```
	
	2. Web search (Claude can do web search)
	
	```
	Use web search to find the relevant documentation for Bun SQLite and better-auth setup (with next.js and Bun SQLite).
	```

### Using MCP Servers & More on Permissions ###
1. What is the Model Context Protocol (MCP)?
	1. It is a standard for exposing tools and resources to AI tools (Claude Code, etc.)
	2. There are many MCP servers we can add to Claude Code (official documentation has popular options)
		1. It is used to give Claude code more tools and more resources to leverage
			1. Claude code will leverage them when it needs to
	3. Useful MCP server
		1. **context7**
			1. It gives Claude Code easier access to official documentation or libraries (makes browsing them easier)
			2. Installation:
			
			```bash
			claude mcp add context7 -- npx -y @upstash/context7-mcp
			
			# Installing globally - for all projects
			claude mcp add context7 --scope user -- npx -y @upstash/context7-mcp
			
			# Documentation
			claude mcp add --header "CONTEXT7_API_KEY: YOUR_API_KEY" --transport http context7 https://mcp
			```
			
2. Prompt: Run in plan mode

```
Implement authentication and database access as described in @SPEC.md .

Add a "lib" folder with "auth.ts" and "db.ts" files. Export a db handle in the db.ts file and make sure WAL mode is used and all required database tables are created if they don't exist yet.

Use web search or the context7 mcp to find the relevant documentation for Bun SQLite and better-auth setup (with next.js and Bun SQLite).
```

	1. Copying by hand is the safest.
		1. Use the above if you are unsure what documentation to rely on
3. Accept the plan
4. Options: Tab and give other supporting instructions

### Understanding Subagents ###
1. What to do to optimize Claude Code
	1. To check if the current implementation is in-line with our expectations and usage instructions by the libraries we are using
2. Instruction:

```
We're building @SPEC.md

Please evaluate the existing codebase to check whether authentication and database access are implemented correctly (in line with the expectations explaining in SPEC.md and the official documentation for the libraries / technologies used).

Use web search or the context7 mcp to look up docs.
```

	1. Not in edit or plan mode
		1. Just for reply
3. Claude uses subagents
	1. Explore agent
		1. Background
		2. It is optimized for reading and understanding fiels and folders
	2. The subagents can run parallelly with the main agent
4. All bullets (\*) are done by the main agent
5. **The subagents do not pollute the context window of the main agent**
	1. They have their own context windows
		1. Claude code can split up complex work into smaller building blocks and outsource them without putting everything in the main context window
			1. Claude code only gets the results of the subagent and loads that into the main context window

### Constructing & Using a Custom Subagent ###
1. Documentation explorer sub-agent
	1. How to build an agent?
		1. `.claude/agents` (folder)
			1. Paste `DocsExplorer.md` (agent) file
				1. The file name is up to us
				2. Content:
				
				```
				---
				name: DocsExplorer
				description: <important-it-gives-hints-to-claude-code-as-when-to-use-the-agent>
				tools: <list-of-tools-from-documentation>
				model: sonnet
				---
				
				<description-of-how-the-agent-should-work>
				
				<steps>
				<libraries-to-use>
				
				<steps-on-how-to-search>
				```
				
					1. `sonnet` - cheaper
						1. It is fast, too
2. Storing globally:
	1. `<user-home>/.claude/agents/DocsExplorer.md` (available across projects)
3. If the instruction is repeated, it should use the agent

### Encouraging Agent Usage ###
1. CLAUDE.md

```
Whenever working with any third-party library or something similar, you MUST look up the official documentation to ensure that you're working with up-to-date information.
Use the DocsExplorer subagent for efficient documentation lookup.
```

2. Prompt:

```
We're building @SPEC.md

Please evaluate the existing codebase to check whether authentication and database access are implemented correctly (in line with the expectations explaining in SPEC.md and the official documentation for the libraries / technologies used).
```

### Introducing Agent Skills ###
1. Agent Skills
	1. Extra, dynamically loaded, context (helpful for certain tasks)
		1. Example: React Component Best Practices (a document describing the best practices)
		2. Example: Python classes best practices
		3. Example: C++ classes best practices
	2. Open standard (supported by other tools: Cursor, Open code, ...)
	3. Implementation:
		1. `SKILL.md` (+ below optional documents and folders)
			1. `[+ extra.md documents]`
			2. `[+ references/ folder]`
			3. `[+ scripts/ folder]`
				1. Can be executed by AI
					1. Example: Clean-up script that deletes files in a certain way
						1. Python or JS
			4. `[+ assets/ folder]`
				1. Images with diagrams
		2. Most valueable skills
			1. Extra knowledge
				1. Extra information
				2. Extra instructions
				3. Extra best-practices
				4. ...

### Adding Custom Skills ###
1. Local skill
	1. `.claude/skills`
		1. Add one sub-folder per skill
			1. `modern-best-practice-react-components` (folder)
				1. `SKILL.md` (must have this name)
				
				```
				name: <name-of-the-folder>
				description: 
				```
				
					1. Claude discovers and loads the skill when it is needed
					2. All the skills will not be loaded in the context window by default
						1. They are discovered and loaded dynamically
							1. Example: React components
					3. `name`: Should include some keywords that gives Claude code some ideas on when to use that skill
					4. `description`: More important
					
					```
					description: Build clean, modern React components that apply common best practices and avoid common pitfalls like unnecessary state management or useEffect usage
					```
					
						1. Claude code will decide whether to use the skill or not (combined with the name).
							1. All the skill titles will be loaded into the context window but the main content will be loaded only when Claude code thinks it is necessary
						2. We can add more fields to skills metadata
							1. Documentation
								1. `allowed-tools` - Restrict tools
								2. `model`
								3. `context` - new context window
						3. `references`
							1. We want to keep skills fairly concise (they take in context window)
								1. References define aditional rules, which are referenced inside the skill document
								2. The reference is optionally used when the specific condition is met
									1. Example: If using `useEffect`, refer to the additional reference document for the rules.
							2. After the skill has been loaded, more information can be loaded by the AI if it is required
		2. Paste all the other skills
2. Global skills
	1. `<user-home>/.claude/skills`
		1. For all projects
3. Prefer local skills because we don't want to load skills not required accidentally
4. Prompt:

```
Let's add a proper authentication route / page content to this app. We only support email + password auth. Users can switch between modes, implemented via search params.

No password resetting for this demo app.
```

5. When the Claude Code is working, we can send extra messages

```
Make sure you use modern, clean HTML / JSX and Tailwind code.
```

	1. The extra messages will be injected when there is time for it
6. Prompt:

```
Did you implement the component using React best practices and clean, modern HTML / JSX + Tailwind?
```

### Using Agent Skills as Commands ###
1. New `/` commands
	1. Built-in + custom
	2. Quick access to extra features
		1. `/config`
		2. `/init`
		3. `/clear`
	3. Skills
		1. `/modern-accessible-html-jsx` - equally named skill
			1. Use-case: Claude code can use them as needed depending on the task it is working on
			2. We can invoke them
				1. What will happen depends on the skill definition
					1. With current description, nothing will happen (it doesn't know what to do)
						1. It has general knowledge only.
			3. Need to give extra instructions or scripts

### Enhancing Skills & Adding Third-Party Skills ###
1. If custom skill is not being used, do the following:
	1. Add extra instructions:
	
	```
	Use this skill to optimize React components and check for the usage of common best practices
	```
	
	```
	Gets triggered when writing ANY kind of CSS code
	```
	
2. To use skills as custom commands only
	1. Add: `disable-model-invocation: true` to the skills metadata
	
	```
	title: ...
	description: ...
	disable-model-invocation: true
	...
	```
	
		1. `false`: For automatic discoverability and no user invocation
	2. `allowed-tools` metadata
		1. To restrict which tools Claude Code may use
		1. `allowed-tools: Read` - Allows reading of files but prevents editing or creation.
			1. [Available tools](https://code.claude.com/docs/en/settings#tools-available-to-claude)
	3. `$ARGUMENTS` - Placeholder for extra input when using skill as a custom command
		1. Example: `.claude/skills/code-review/SKILL.md`
		
		```
		---
		name: code-review
		description: Review code for bugs, security or performance issues. Use this skill when asked to perform code reviews or after finishing major tasks or after refactoring code.
		allowed-tools: Read
		---
		
		MODE: $ARGUMENTS
		
		If MODE is one of the following, adjust the review as described:
		
		- MODE == BUGS: Focus ONLY on logical or other bugs.
		- MODE == SECURITY: Focus ONLY on security issues.
		- MODE == PERFORMANCE: Focus ONLY on performance issues.
		
		MODE can also be set to a combination like "BUGS,SECURITY" etc => Perform the combined review in that case.
		
		If MODE is set to anything else or nothing at all, perform a thorough, general code review.
		
		Perform an in-depth code review of the entire codebase
		
		Carefully and thoroughtly explore the codebase file-by-file to find potential issues and improvements.
		
		Don't rush it, instead make sure you fully understand the code structure and architecture.
		
		Generate a detailed report of all your findings.
		```
		
3. Adding Third-Party Skills
	1. Public skills repository.
		1. [skills.sh](https://skills.sh/)
			1. To add a skill: `npx skills add <owner/repo>`
				1. We can tweet or remove selected parts of the skills

### Iterating on the Demo App ###
1. Prompt:

```
We added authentication (see @app/authenticate/page.tsw, @lib/auth.ts).

As a next step, add the following features:
- after successfull authentication, redirect the user to "/dashboard"
- protect "/dashboard" and all other note-related routes (except the publicly shared notes route) from unauthenticated access => add protection on a per-route level (NOT via layout)

Use modern Next.js features and focus on writing clean, efficient React / Next.js code.
```

	1. To encourage loading the appropriate skills
2. Testing:
	1. Open Dev Tools
	2. Clear Auth cookie
	3. Reload `/dashboard`
		1. Asks for login
3. `/clear`
4. Complex prompt:

```
Add the following features to our web app:
- header component with title logo ("NextNotes") which links to "/dashboard" (using Next <Link>)
- On @app/dashboard/page.tsx, add "New Note" link that links to the appropriate route
- On the "New Note" route, add a <form> with the title input and rich text content input
- Implement form submission handling + insert data into database

Ensure modern, clean React & Next.js code with accessible JSX and clean, modern Tailwind styling.
```

	1. Run in plan mode
	2. Check and include
	
5. Next prompt:

```
Add a logout button to the header (when the user is authenticated).
```

6. Fixes:

```
The header is white - the rest o the site is dark. Or at least supports dak mode. Adjust the header appropriately. Ensure that overall the entire website with all its pages works well in whatever mode the user is using.

Also: Check the user auth status on the serv and pass that server-side derived user information to the header (instead o using the client-side auth client).
```

	1. Plan mode
	
7. Toolbar

```
On the new note (or edit note) page, add a toolbar that exposes the TipTap tools we want in our app (see @SPEC.md) and makes using them simple.
```

### On Custom Commands ###
1. "Custom Commands" has been merged with "Skills"

### Building & Using Custom Commands (Prompt Templates) ###
1. Code-review:

```
Perform an in-depth code review of our codebase - focus on security and logical bugs.
```
	1. More elaborate one is possible
		1. Problem: Difficult to repeat it.
			1. Solution: Custom commands
				1. `.claude/commands`
					1. `code-reviews.md`
					
```
---
allowed-tools: Read(*)
description: Perform a code-review
---

MODE: $ARGUMENTS

If Mode is one of the following, adjust the review as described:

- MODE == BUGS: Focus ONLY on logical or other bugs.
- MODE == SECURITY: Focus ONLY on security issues.
- MODE = PERFORMANCE: Focus ONLY performance issues.

MODE can also be set to a combination like "BUGS,SECURITY" etc => Perform the combined review in that case.

If MODE is set to anything else or nothing at all, perform a thorough, general code review.

Perform an in-depth code review of the entire codebase.

Carefully and thoroughly explore the codebase file-by-file to find potential issues and improvements.

Don't rush it, instead make sure you fully understand the code structure and architecture.

Create a detailed report of all your findings.
```

	1. Start a new Claude session
		1. `/code-review BUGS,SECURITY` 
			1. Take a look and decide whether to act upon them or not
			2. Fix:
			
			```
			Fix the following issues (IGNORE all others):
			3. Make sure we fully sanitize all user-generated input
			6. I added DB_PATH => make sure it's used
			8. (also for any other related points): Make sure we show user-friendly helpful error messages WITHOUT leading any internal / sensitive information (not even in the response sent back to the client!)
			14. Improve `useState()` using common best practices
			```
			
				1. Run in plan mode
					1. Old tool restriction from the custom command does not apply (it is a new prompt)
						1. It has full access to all tools

### Using Screenshots for Prompting with Feedback ###
1. Dashboard
2. Prompt:

```
I our app, add the following features:
- display all notes that belong to the logged in user on the "/dashboard" route
- upon clicking on a note, link to the "viewing page"
- on that viewing page, render the note (JSON => custom JSX elements, with proper styling)
```

3. Editing:

```
In our app, make the notes editable and deletable.

When viewing a note (as the one who added it), on that viewing page, there should be "Edit" and "Delete" buttons.

"Edit" should be a link to the edit page, where the note gets loaded into the TipTap editor. The title also should be editable.

"Delete" should be a button that opens a confirmation <dialog>. Once confirmed, the note should be removed from the database and the user should be navigated back to the "/dashboard" route.
```

	1. Plan mode: AI can ask clarifying questions and generate a plan
4. Passing screenshots into prompts: (Claude Code can understand images)
	1. Copy and paste
	2. Enter prompt:
	
	```
	When editing, the raw JSON content is loaded into the content field - that's wrong. That JSON content should be loaded into the editor via TipTap to be displayed as (and editable as) rich text. See the attached screenshot.
	```
	
		1. Good for UI problems.

### Understanding & Using Hooks ###
1. Formatting:
	1. Hooks
		1. `bun add -D oxfmt`
		2. `package.json`
		
		```
		"scripts": {
		  ...
		  "format": "oxfmt"
		```
		
		3. `bunx oxfmt --init`
		4. `.oxfmt.json`
		
		```
		{
		  "$schema": "./node_modules/oxfmt/configuration_schema.json",
		  "ignorePatterns:": [],
		  "singleQuote": true,
		  "jsxSingleQuote": true
		}
		```
		
		5. `bun run format`
	2. Hooks: To react to certain events emitted by Claude Code
		1. Example: File edited
			1. We can then run any code as a reaction
	3. Where to add hooks?
		1. settings.local.json (or settings.json)
		
		```
		{
		  "hooks": {
		    "PostToolUse": [
			  {
			    "matcher": "Edit|Write",
				"hooks": [
				  {
				    "type": "command"		# "prompt" - injected automatically
					"command": "cd \"$CLAUDE_PROJECT_DIR\" && bun run format 2>/dev/null || true"			# bash command - new terminal session will be opened and executed
				  }
				]
			  }
			]
		  }
		}
		```
		
			1. [https://code.claude.com/docs/en/hooks](https://code.claude.com/docs/en/hooks)
				1. `PreToolUse`: Runs after Claude constructs tool parameters and before processing the tool call
					1. Tools:
						1. `WebFetch`, `WebSearch`: Web operations
						2. `Edit`: File editing
						3. `Read`: File reading
						4. `Write`: File writing
				2. `PostToolUse`: Runs immediately after a tool completes successfully.
			2. Restart session (hooks will be loaded)
				1. `/hooks`
					1. Shows all hooks - select
						1. Add or see existing hooks
	4. Public sharing feature:
	
	```
	In our web-app, add the "public sharing" feature.
	
	When adding or editing a note the user (owner) should be able to turn on public sharing. This must generate a unique link that leads to the note.
	
	When other users (including guest users who did not sign in) follow that link they can see the note but of course they can't edit or delete it. If sharing is turned off, the link should not lead anywhere anymore.
	```
	
		1. Plan mode			

### Installing & Using Plugins ###
1. `/plugin`
	1. We can build custom plugins, too
	2. Example: We can bundle skills, commands, mcp server, etc. and share them with others in an easy way
	3. The command opens a marketplace
		1. They can be easily installed without visiting other websites or copy files
	4. We can navigate the tabs
		1. Discover
			1. `typescript-lsp` - extra capabilities to Claude Code
				1. Helps detect TypeScript errors in an easier way
				2. Hit space to toggle
				3. Hit enter
					1. Install
				4. `settings.json` gets automatically updated
				
				```
				{
				  ...
				  "enabledPlugins": {
				    "typescript-lsp@claude-plugins-official": true
				  }
				}
				```
				
			2. `playwright`
				1. Giving browser access
		2. Installed
		3. Marketplaces
			1. MCPs are plugins
			2. We can add new marketplace
				1. We can add company's marketplace

### Constructing Feedback Loops by Granting Browser Access ###
1. A way to validate their work
	1. First step: Give access to browser
2. Test:

```
Test the application you built, using the playwright plugin / MCP. Test all main features step by step and ensure they work correctly.

The application dev server is already up and running on port 3000.

Fix all issues you find.
```

	1. Playwright: Built for end-to-end testing of web applications.
	2. Send with "Accept edits on"
		1. Spins up browser window, navigates on its own, and tests the application
	3. Claude Code takes snapshots and examines
	4. This enables feedback loop
		1. Detect issues
		2. Fix issues
		3. Test issues
		4. Repeat
	5. Costs many tokens

### Providing Feedback via Automated Tests ###
1. Another option: Unit tests, integration tests, etc.
2. Testing:
	1. `bun add -D vitest`
3. Adding tests:

```
I've installed the Vitest library to do unit testing.

Set it up appropriately and add unit tests for all the key features of this app. Add mocks as needed and split complex functions up to simplify testing, if needed.
```

	1. Run in plan mode
		1. Maybe it needs more information
	2. Inject the following:
	
	```
	Actually, set up a "bun run test" script that uses Vitest - we don't want to use Bun's built-in test runner
	```
	
	3. It now runs its own tests and fixes any errors it detects
		1. Note: AI might be inclined to match the tests to the implementation.
			1. Solution: Write tests first and then the code
	4. Review the tests
	5. We can ask AI to add more specific tests

### Running Claude Code in a (Ralph) Loop ###
1. Building a loop
	1. We don't interact with Claude Code at all
		1. The pattern is called the Ralph loop (naive persistence)
			1. Write `ralph.sh` under the root
				1. It has a loop that goes up to maximum number of iterations (input)
				2. `--dangerously-skip-permissions` enabled
					1. Run in sandbox mode
				3. `-p` (pass prompt directly. Non-interactive)
					1. Point at some files
						1. It has a list of tasks
							1. It is in the form of JSON (any format is fine)
							2. `passes` is set to `false`
								1. The AI changes it to `true` once the task is done
							3. AI can be used to derive the JSON file from `@SPEC.md`
				4. Run tests
				5. Visit browser using Playwrite
	2. No human intervension
	3. Ensure the following: `settings.json`
	
	```
	{
	  ...
	  "sandbox": {
	    "enabled": true
	  }
	}
	```
	
	4. Invocation: `./ralph.sh 10`
	5. Run another session: `claude -c` (the last session that was started)
		1. See what it is doing
2. The Ralph Loop
	1. Can definitely yield good results, especially for prototyping
		1. For not a super-complex app
		2. For utility software
		3. For internal tools
			1. Caveat: We need to plan ahead (properly)
				1. SPEC document
				2. Look at the tasks in-between and verify
	2. Potentially costs A LOT of tokens
		1. Feedback costs tokens
	3. Trade-off: Less control, more time for other work
		1. Only check-in from time-to-time
			1. No insights
				1. No plan mode
					1. No checking
				2. No live-stream
					1. If it has taken the wrong direction, tokens get wasted
	4. AI code quality will very; it can also get stuck
		1. Working app may not be production-ready
			1. Bugs
				1. Performance
				2. Security
			2. Needs thorough verification
				1. Do not blindly trust it
					1. No vibe-coding trap
		2. If it gets stuck
			1. Needs manual intervention
			2. May need to install dependencies
			3. May need to look for work-arounds to unblock it
				1. It may be fixed in future versions
	5. **Upfront work:**
		1. SPEC.md
		2. prd.json (good tasks)
		3. Solid project setup
		4. Tests enabled
		5. Give AI the right skills

### Using Claude Code Web (Claude) ###
1. We can offload tasks from a local machine to the cloud
2. Example: Changing color
	1. Push the code to Git repository
	2. You need pro/max/enterprise subscription
	3. `code.ai/code`
		1. Prompts:
		
		```
		Give Claude code environments
		
		Let users move sessions from cloud to CLI
		
		Make claw'd dance on hover
		```
		
			1. Connect to the repository
			
		2. Cloud environment
			1. Name: Default
			2. Network access: Full (for flexibility)
				1. Select: Trusted
		3. We can use Claude from cloud interface or locally
			1. Choose repo
				1. main
				2. Default environment
			2. Describe task
			3. Choose model
			4. Add image
			5. Prompt: `Change the main color from blue to an elegant purple`
		4. Locally:
			1. `/remote-env`
				1. Prompt: `& Change the main color from blue to an elegant purple. On all UI elements, across all pages.` (background - in the cloud)
					1. We can run multiple tasks:
					
					```
					& Another task
					```
					
						1. Runs in parallel
			2. Alternative: `claude --remote "Change the main color from blue to an elegant purple. On all UI elements, across all pages."`
				1. Can get notifications (enable)
		5. Claud cloud will pull the code, make changes on a new branch, and raise a PR
		6. Hybrid:
			1. Locally: `Add a confirmation dialog when enabling public sharing in the app.`
				1. Plan mode
			2. Cloud: Continue and interrupt
				1. & Implement the plan
				2. `claude --remote -c "implement the plan"` (continue last session)

## Section 3: Beyond Local CLI Usage ##
### Using the Claude Desktop App ###
1. Other ways:
	1. IDE integration
	2. Claude Desktop app
	3. Mobile app
2. Desktop app
	1. Install
	2. It bundles multiple capabilities
		1. Chat mode (like Chat GPT)
		2. Cowork - general work assistant (slides, etc.)
		3. Claude code
	3. Chats organized by coding projects
	4. Supports cloud session
	5. New session
		1. claude-code (select a project)
		2. local or cloud task
		3. Use git worktree?
			1. Local clone (a copy) into a different path on the same system
				1. We can work on both main codebase and worktree simultaneously
					1. We can spin up different agents to work on different worktrees
			2. Once done, we can merge the worktree back to the main repo
		4. Switch branch?
	6. Task:
		1. Prompt:
		
		```
		The width of the main content container is not consistent across pages. Specifically, the "edit note" page is not as wide as the other screens (which all take up the full width of the main page area).
		
		Carefully analyze the styling and JSX code for these pages and ensure they all have the same width. Avoid unnecessary code duplication, implement a clean solution that's easy to adjust in the future.
		```
		
			1. Extra context:
				1. `@page.tsx`
				2. + (add files or images)
				3. `/` commands
					1. compact
					2. <skills>
					3. `/modern-tailwind`
		2. Voice dictation
		3. Permissions:
			1. Ask permissions
			2. Accept edits
			3. Plan mode
			4. Bypass permissions (Enable in Claude Code settings)
		4. Choose model and effort

### Advanced Claude Code Desktop Features ###
1. We can do things after tasks are completed
	1. Expand sections (file changes).
	2. Modes: Plan, ...
		1. Plan:
			1. It shows the plan
		2. Tasks
			1. Shows what is going on
		3. Preview
			1. Preview of the site
				1. Set up
					1. Stores `/.claude/launch.json`
			2. Automatically starts a preview
				1. We can toggle between desktop and mobile app view
				2. We can toggle between light and dark mode
			3. We can select elements
				1. Injected into the context window
					1. Prompt: `Make this link red`
				2. We can select and add multiple elements
				3. We can remove them by clicking on them in the chat window
	3. Session logs
	4. Integrated terminal
		1. We can run our own commands
	5. Diff
		1. Files that were touched and edited
			1. For reviewing
				1. + - make a comment
					1. Save
						1. Added as context (instead of writing everything)
					2. Can delete the comment

### Don't Forget to Configure! ###
1. Configuration options
	1. Settings
		1. General 
		2. Account
		3. Usage
		4. Claude Code
			1. Allow bypass permission mode
				1. No permissions required
			2. Worktree location
			3. Notifications
			4. Preview feature
		5. Privacy
			1. If you don't want to share some data
	2. Customize
		1. Skills
			1. New skills
			2. Browse skills
				1. Pre-authored skills
		2. Connectors
			1. Can connect to Github (for PRs)
		3. Plugins
			1. Browse
			2. Manage existing plugins

### Dispatching Tasks from the Mobile App ###
1. Dispatch feature
	1. Enable it
2. Dispatch
	1. We can dispatch to locally running instance from a mobile app
		1. Keep awake
		2. Enable computer use (more control)
		3. Code permissions
			1. Bypass permissions (no interaction)
3. Claude code app
	1. Dispatch
		1. Pair phone with machine
		2. Prompt:
		
		```
		In the Claude code project in the development/teaching/courses folder, change the primary color to an elegant pink.
		```
		
			1. Arrives in Desktop app
		3. It starts in a new session
			1. Tasks - can track progress

### Using Claude Code Remote Control ###
1. Remote control
	1. `claude`
		1. `/remote-control`
	2. `claude remote-control`
		1. Enable
		2. Options:
			1. Same directory
			2. Worktree (an isolated worktree)
2. We can initiate session from somewhere else
	1. Difference
		1. Will be attached to a concrete project
		2. Can continue an existing session
3. We can connect from other devices and continue
4. On mobile app, we can select the remote control session
	1. Prompt will be sent to computer and executed

### Using Claude Code Channels (Telegram) ###
1. Claude code channels: A way to connet any communication channel to Claude Code
	1. Example: Push messages
		1. Slack
		2. Whatsapp
		3. Telegram
		4. ...
		5. Own channels
2. Steps:
	1. New `/claude` session
	2. `/plugin install telegram@claude-plugins-official` (by Anthropic)
	3. Globally/this project - globally
	4. `/reload-plugins` (or quit and start a new session)
	5. `/telegram:configure <token>` (token from telegram)
	6. Start telegram
	7. Talk to `BotFather`
	8. Start a new session
	9. `/newbot` - telegram bot (new channel)
		1. Name: AcadCCBot
		2. Internal name: acadcc_bot
		3. Bot token - copy
	10. Paste the token
	11. Allow
	12. `/reload-plugins` - to load updated telegram plugin
	13. New chat with new bot in telegram
		1. `Hello`
			1. You will get a pairing code (need to use in Claude code)
				1. `/telegram:access pair <code>` - authenticating the bot
3. Starting claude code session with the above channel enabled
	1. `claude --channels plugin:telegram@claude-plugins-official`
		1. Listens to that channel
	2. Send: `Generate an HTML file with 'Hello World'`
		1. Give permissions in telegram
		2. Click on file to view it on mobile phone

### Idea: Despite the Name, Claude Code is not (necessarily) Just About Code ###
1. Dispatch - can be used for anything
	1. Prepare excel
	2. Prepare presentation
2. Remote control
	1. Start `/claude` on another machine
	2. Connect and send remote commands to our machine

### Scheduling Tasks with Claude Code ###
1. Routines - feature (desktop app)
	1. Local or remote
	2. Task send to Claude at a certain time
		1. We can tie to a folder/repo
		2. Give permissions
			1. Bypass permissions say
		3. Choose model
		4. Text:
		
		```
		Analyze the recent changes and generate a summary.md file
		```
		
		5. Description: `Summarizes daily changes`
		
2. CLI: `/schedule`
	1. Schedules remote agents (on cloud) (only)
	2. Interactive mode
		1. New trigger
			1. Type: `summarize key changes in a summary.md file`
		2. Give Github URL (if not linked)

### Course Wrap Up ###
1. Done.