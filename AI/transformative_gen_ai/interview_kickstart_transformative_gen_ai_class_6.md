## Multi-Agent Systems

MA systems coordinate specialized components to tackle complex workflows
	1. Not every complex tasks requires this approach - a single agent with the right tools and prompt can often achieve similar results
	
Parallelisation - scaling up
	1. Example: Multiple bugs, security issues, ...
	
Why multi-agent systems?
	1. Context Management
		1. For instance, team that analyzes has only the context relevant to the analysis
		2. Hospital:
			1. Reception
				1. Data related to customers only required by them
					1. Don't need irrelevant context
			2. Radiology
			3. BIlling
			4. Pharmacy
			5. ...
		3. Context for specialized roles is clearly isolated
			1. Good for isolating context
				1. Context engineering - how well we maintain context
		4. Lost in the middle
			1. If contexts are mixed up, it will forget what it needs to do
	2. Distributed development
		1. Example:
			1. Alert agent
			2. Analysis agent
				1. Example: Log analysis, code analysis, ...
			3. ...
	3. Parallelisation
		1. Example: Travel agent
			1. Hotel search
			2. Flight search
			3. Iterinary
				1. Hotel search and flight search are independent
					1. They can be run in parallel
		2. Example: Independent analysis or different types
	4. Scalable
		1. Adding more agents (horizontal scaling)
	5. Strong and reliable
		1. If an agent stops working, the system keeps going because other agents take over
		2. Example:
			1. Bug Triaging
				1. Intake
				2. Historical search (agent) (if this fails, we can skip it go to the next step)
					1. How to make it optional? LangGraph
				3. Analysis (log + code) (agent)
				4. Synthesis
	6. Faster and more efficient
		1. More agents working on different parts of the problem
		
When to build multi-agent systems?
1. Too many tools
	1. Example: Outlook, confluence, slack, teams, ... N tools
		1. If too many tools are exposed to agent
			1. Prompt: "Draft a slack message" - agent explores too many tools to find slack tool
				1. Solution: Slack agent has only slack tool
					1. Expose the tools requierd by the agent only
2. Specialized knowledge
	1. Only the required tools and context is passed
3. Sequential constraints
	1. Example: A -> B -> C -> D
		1. Only if a criteria is met at B, go to C or go to A
		
Relevant data = good context
	1. Only the required data must be fed (don't feed unnecessary data)
		1. Clean context
		
## Common workflows and agent patterns

prompt chaining

```
-> agent -> agent -> ...
```

Workflows are more deterministic
Agents are dynamic

Parallelism

Orchestrator-worker

```
-> orchestrator agent -> worker(s) -> 
```

	1. Orchestrator - only understands the intent of the user and forwards to workers
	2. Router - no intent understanding
		1. If Q is this, route to this worker

Evaluator-optimizer

```
-> agent <-> evaluator - if happy ->
```

Routing

Agent:

```
In -> LLM call - action -> Tool -> Out
        <--------------------
```

Start with one agent, then expand to MAS

## Building a Multi-Agent System

### Popular Frameworks to build MAS
1. JADE
2. AutoGen
3. LangGraph
4. LangChain
5. LlamaIndex 
6. Google ADK
7. CrewAI

Frameworks change
	1. Understanding patterns is important
	
### LangGraph

Graph of nodes

It provides a low-level orchestration framework
	1. Gives flexibility to use it and change it
	
Building blocks:

1. State
2. Node
3. Edge
	
Why LangGraph?
1. Fine-grained control over agent flow
	1. Flow can be to specific agents
2. Built-in persistence & human-in-the-loop
	1. Helps with resuming work (checkpointing)
3. Streaming-first architecture
	1. output is streamed to user (LLM)
		1. Keeping user engaged
4. Debuggability & observability
	1. Agents can crash or not working as expected
		1. We need observability layer
			1. Outputs
			2. Flow
			3. ...
				1. Using LangSmith
5. Flexible agent patterns
	1. Orchestrator 
	2. Router
	3. Evaluator-optimizer
	4. ...
6. State management

### State (schema is defined in langgraph)
	1. Represents the context or memory that is maintained and updated as the computation progresses
	
Context needed by agents (shared): is in the state
	Destination
	Messages
	Dates
	Preferences
	Experience
	flights (populated by flight search agent) (can be used by other agents as input)
	....
	
The information is available to every node

### Node
	1. Building block of you LangGraph. Each node represents a function or a computation step. Each node performs specific tasks, such as processing input, making decisions, or interacting with external APIs
		1. It can be:
			1. Agent
			2. Simple function call
			3. ...
			
### Edge
	1. Connect the nodes in your graph, defining the flow of computation. LangGraph supports conditional edges, allowing you to dynamically determine the next node to execute based on the current state of the graph
		1. Conditional edges are possible
			1. If a condition is met, go to this node, etc.
			
### Program

class State(TypedDict):
  messages: list[AnyMessage]
  extra_field: int
  
def node(state: State):
  messages = state["message"]
  new_message = AIMessage("Hello!")
  return {"messages": messages + [new_message], "extra_field": 10}
  
Reducer: Used control how the state needs to be updated
	1. Overwrite the state or append
	
### Persistence

What are checkpoints?
	LangGraph leverages built-in checkpointers to save the entire state of your agent workflow at specific points, ensuring that no progress is lost and providing a robust foundation for operations
	
Why Persistence Matters
	1. Resuming State
	2. Human-in-the-Loop
	3. Fault Tolerance
	
## Memory Store
	With checkpointers alone, we cannot share information across threads.
	This motivates the need for the Store interface. As an illustration, we can define an `InMemoryStore` to store information about a user across threads
		1. Preferences
		
```
class State(TypedDict):
  foo: str
  bar: Annotated[list[str], add]

workflow = StateGraph(State)
workflow.add_node(node_a)
workflow.add_node(node_b)
workflow.add_edge(START, "node_a")
workflow.add_edge("node_a", "node_b")
workflow.add_edge("node_b", END)

checkpointer = InMemorySaver()
graph = workflow.compile(checkpointer = checkpointer)

config: RunnableConfig = {"configurable": {"thread_id": "1"}}
graph.invoke({"foo": "", "bar": []}, config)
```

## SubAgents
Subagents are useful for context quarantine (keeping the main agent's context clean) and for providing specialized instructions.
	1. Like a thread for a specific task
		1. Example: Web-search sub-agent
			1. For delegating
			2. Sub-set of tools are exposed to it
When to use subagents:
	1. Multi-step tasks that would clutter the main agent's context
	2. Specialized domains that need custom instructions or tools
	3. Tasks requiring different model cpaabilities
	4. When you want to keep the main agent focused on high-level coordination
When NOT to use subagents:
	1. Simple, single-step tasks
	2. When you need to maintain intermediate context
	3. When the overhead outweights benefits
	
## Travel Agent

Step 1: Start with the process to automate

What the agent should do?

1. Search hotels and flights based on user preferences
2. Plan complete travel itineraries
3. Answer travel-related questions with deep research
4. Handle multiple queries in parallel
5. Present unified, well-formatted travel recommendation

Scope:
	1. Search hotel/flights
	2. Planning
	3. Q/A
	4. Parallel
	5. Presentable
	
From Idea to Agents:

Step 2: Map out your workflow as discrete steps:
	1. Search Agent
		1. Hotel search
		2. Flight search
	2. Itererary Planner Agent
		1. utilizes search results and research to construct details travel plans
		
From Idea to Agents:

Step 2: Map out your workflow as discrete steps

Step 3: Identify what each steps need to do

```
Search Agent find flights + hotels --- API call

Itinerary Agent Itinerary research + general Q&A --- deep analysis --> Deep search tool
```

APIs:
	1. Hotel & Flight Search
		1. Serp API
	2. Internet Search
		1. Tavily API
			1. Guide exists
			
## Code

Install langgraph
install langchain - declarative language for chaining

ChatOpenAPI

Install deepagent 
	1. Provided by langchain
		1. Capabilities
			1. A template for agent
Research instructions:

```
SCOPE AND BEHAVIOR RULES

RESEARCH AND REASONING PROCESS (ReAct)

TOOL USAGE

OUTPUT REQUIREMENTS

FORMATTING GUIDELINES

QUALITY BAR
```

SLA can be defined between my company and Open AI
	1. Not using private data for training
	
A subagent can be invoked inside an agent

Deep Agent?

A Deep Agent handles complex, long-running tasks by planning, breaking the problem into smaller steps, using tools or sub-agents, and managing context/state until the task is completed.

Synthesizer:

Give output structure
Give rules

