## Connection

Server decides the duration

MCP servers can host:
Prompts
Resources
	PDFs
Tools

	1.x - stateful protocol
		1. Server stores state
	2.0 - Stateless protocol
		1. Read about it
		
		Why?
			If an agent needs a tool multiple times
				1. it is difficult to estimate
					1. Stateless - makes it easier
						1. Scalability is easier
						
Different teams can host MCP servers

Internet hosts MCP servers
	Atlassian
	...
	
Standardization
	MCP Gateway - a layer of abstraction
		Authentication
		Security
		...
		(Cross-functional aspects)
		
	Light LLM (proxy)
		MCP Gateway feature
		...
		Same prompt, multiple models
		...
		Read about it
		
		
```
@tool
def simple_search(query: str) -> str:
  """
  Performs a simulated web search for a given query.
  Use this tool to find general information
  ...
  """
  ...
```

Tavily - websearch tool
	Connect your AI agents to the web
		1. Paid
		2. Free usage
		
Anthropic
	Add connections
		Marketplace of MCP servers
			Atlassian
			Tavily
			...
			
Prompt - template
	Call with a prompt name
	
Sampling - Server asks host to call LLM
	Server needs LLM reasoning without holding API keys
	
FastMCP - tool
	Similar to FastAPI
	
Interview
	Description of the tool is very important
		Agents make decisions based on the description
		It should be very well defined
		It should mention arguments clearly
		
Too many descriptions - high cost
	Affects reasoning
		Difficult for agent to choose tools (they may be too close)
			Solution:
				How to solve the problem?
				Approaches
					1. RBAC - This application has access to a subset of tools
						1. 50 instead of 800 tools
					2. Semantic matching
						1. query -> what is the cost spent on operations
							1. See which descriptions are more relevant (similarity score)
								1. Example: AWS Agent Core
									1. Gateway
										1. Exposes symantic matching - it exposes only one tool
											1. Based on semantic match
					3. Hierarchy of tools
						1. Tools are grouped (ordering, maintenance)
							1. Next layer of tools are called internally
					4. Can we use RAG to store the descriptions and do the semantic matching?
						Yes—store MCP tool names/descriptions/metadata in a vector database, retrieve the most semantically relevant tools for the user query, then let the LLM choose from that shortlist.

						Could be an overkill (RAG is good for 10s of thousands of documents)
						
```
mcp.run(
  transport = 'streamable-http',
  host = '0.0.0.0',
  port = 9000
)
```

Streamable http - Responses are streamed (like Chat GPT)

Do we need MCP?
	Agentic systems that may be extended
	3-4 APIs only?
		MCP may not be required
			Overhead
			Authentication
			Maintenance
			
UTCP - read about it
	MCP server is not required
	File will list everything in a commonplace
		Agent will read from the file
	Voice applications - one less hop
	
A2A:
	
Multiagentic system

Orchestrator
|
v
Holiday
	Flight agent
	Hotel agent
	Visa agent
	
Network of agent communication

Sequeantial communication (chain)

Fan out
	Parallel
	Aggregate
	
Agents can be on different platforms, locations, servers, ...
Different frameworks 

Frameworks:
Langgraph - deep agents
Strands
Google ADK
CrewAI
AutoGen

How will A1 talk to A2? (they use different frameworks, platforms, etc.)
	Protocol needs to be defined
		Google standardized it using A2A (agent to agent communication)
	Alternative: We can define our own contracts and communicate
	
AgentCard
	Skills
	
Connections
	Polling
	Long standing connection
		SSE
	Push notification
		Client subscribes to push notification
			Client communicates for result
			
https://github.com/a2aproject/a2a-samples/tree/main/samples/python/agents/travel_planner_agent

A2AStarletteApplication (similar to FastMCP)
DefaultRequestHandler - Handles requests
InMemoryTaskStore
	If agent crashes, tasks are lost
		1. Persistence (SQLite, ...) can be defined to persist task
			1. It is restarted
			
`AgentCard` - used for discovery
	name
	description
	url
	version
	default_input_modes = ['text', 'img', ...]
	default_output_modes = [...]
	capabilities = AgentCapabilities(streaming = true)
		Others
			gRPC
			...
				(needs implementation from us)
	skills = [skills]
		It can have multiple skills
	
`AgentSkill`
	id
	name
	description
	tags = ['travel planner']
		Helps to select agents (filtering)
	examples = ['hello', 'nice to meet you']
		How to use the skill
		
`DefaultRequestHandler`
	agent_executor = TravelPlannerAgentExecutor()
		logic
	task_store = InMemoryTaskStore()
		Can be changed to persistence
		
`A2AStarletteApplication`
	agent_card
	http_handler
	
`unicorn.run(server.build(), host='0.0.0.0', port=10001)`
		
MCP - for calling tools
A2A - Agent to agent communication

A2A protocol inspector
	web-based tool

solo.io	
LLM Gateway
MCP/A2A Gateway
Inference Gateway

Building A2A Agents with LangGraph and WatsonX:
	https://heidloff.net/article/a2a-langgraph-watsonx-ai/
		Wrapping any agent to make it compatible with A2A
		
LangGraph vs Google ADK
	LangGraph: Graph-based flow
	
	Modern agentic systems: Google ADK, Deep Agents, Strands, ...
		Out of the box capabilities
			Multiagent workflows
			Human-in-the-loop
			...
		Google ADK
			Extra capabilities
				Developer Web UI
					ADK Web
						We can debug and trace agents (we have seen it)
						Features:
							We can select application and debug
							New session can be created
								Session specific information
							Traces
								Time taken
							State
								variables
							Artifacts
								If we are generating artifacts (PDF, etc.)
							Evals
								Metrics - how well is the agent performing
									Hallucination score
									Recall
									...
			It has LangGraph features
			
	Strands:
		AWS

Use Google ADK docs - updates are fast
		
Flows
Callbacks/Hooks

Loop agent
	Take inputs and keep logic
		Similar to react agent
		
Sequential agent
Parallel agent

With ADK 2.x
	Graph-based format
		Everything can be represented as graphs
		
		Each node can be
			HITL
			Tool
			Python function
			LLM
			Agent
			...
			
	Dynamic workflows
		Flow is chosen by LLM in a graph
		
		Collaborative agent teams
		
	Runner
		Orchestrates flows
		
Modes: (documentation)
	Chat 
	Task
	Single Turn (no user interaction)
		Returns immediately after task
		Multiple tasks in parallel
		
Callbacks - Hooks
	Agent (using LLM)
		LLM (using tool)
		
	```
	<-- Before
	Agent
	<-- After
	<-- Before
	LLM
	<-- After
	<-- Before
	Tool
	<-- After
	```
	
		1. For guardrails
			1. Prompt injection
			
`CallbackContext`
	Used by the callback