Naive Baseline
MCP Servers
A2A
Google ADK

real-estate-negotiaion-simulator
	https://github.com/jeev1992/real-estate-negotiaion-simulator
	
git clone https://gith.com/jeev1992/real-estate-negotiaion-simulator/simulator

Two AI agents
	They negotiate a price
		1. Only 5 rounds
			1. End in deal
			2. End in no deal

Buyer wants to buy at lowest price
Sellet wants to sell at highest price

Range: $425,000 vs $477,000

MCP - External data for agents 
Goodle ADK + A2A Protocol

Like USPC

Open standard
	1. Abstract APIs
	
Helps discover tools
	1. We don't have to set up communication
	
Model Context Protocol
	Standard that lets agents call external tools without knowing where the data domes from
		1. It provides context
		2. Abstracts external server
	It takes actions as well (not just get data)
	
It is like REST + TCP + HTTP

	Handshake
	Tools
	Resources
	Prompts
	
API vs CLI vs MCP
	1. Why not API?
		1. M x N integration problem (we have to make sure M agents are compatible with N servers)
			1. M - agents
			2. N - servers
	2. Why not CLI?
		1. No reach to web/mobile/cloud - needs filesystem
	3. MCP
		1. Standard protocol
			1. Discovery
			2. Invocation
			3. Auth
		2. One remote server reaches any compatible client (Claude, ChatGPT, Cursor, VS Code, ADK)
		3. Auth, discovery, and rich semantics are standardized
		4. 300M + SDK downloads / month
		5. Build once, use everywhere
		
	```
	Chat interface <-> MCP <-> Data and file systems (PostgreSQL, SQLite, GDrive)
	IDEs and code editors    Development tools (Git, Sentry, etc.)
	Other AI applications    Productivity tools (Slack, Google Maps, etc.)
	```
	
		1. It is like USB-C prot for AI applications
		
MCP is a think RPC layer over JSON-RPC 2.0
	1. Operations
		1. Initialize
			1. Handshake,
			2. Version
			3. Capability negotiation
		2. Tools/list
			1. The server adevertises typed tools schemas
		3. Tools/call
			1. The host invokes a tolls by name with validated arguments
			
Advantages:
	1. N + M not N x M
	2. Out-of-rocess tools
		1. Tool crash does not crash the agent
			1. The server is isolated compute
			
Structure
	1. MCP Host
		1. AI application that coordinates and manages one or multiple MCP clients
	2. MCP Client
		1. Component that maintains a connection to an MCP server and obtains context from an MCP server for the MCP host to use
			1. Subprocess that maintains connection with MCP server
	3. MCP Server
		1. A program that provides context to MCP clients
		
Connection:
	Shared connection
	Dedicated connection
	
Is there a standard way to handle errors, like we have with HTTP (4xx and 5xx errors)?

Yes, MCP has a standard way to handle errors, but it uses the standard JSON-RPC 2.0 error specifications instead of HTTP status codes.

Standard JSON-RPC Errors (-32700 to -32600): Handles general protocol failures like Parse Error (-32700), Invalid Request (-32600), and Method Not Found (-32601).

MCP Specific Specs (-32020 to -32099): Reserved for protocol-specific issues such as InvalidParams (-32602), HeaderMismatch (-32020), or UnsupportedProtocolVersion (-32022)

Communication:

	session.list_tools() ->
	<- tool schemas
		[{name, description, inputSchema}]
	session.call_tool(...) ->
		name: "get_market_price"
		args: { address: "742 Evergreen..." }
	<- result dict
	
Primitive
	Tool (model invokes with arguments)
	Resource (fetching data)
	Prompt (Host selects template - parameterized, re-usable prompts)
	Sampling (Server asks host to call LLM)
		1. Server doesn't have LLM
			1. Use-case
				1. Cost saving for the service provider

Content types
	TextContent (JSON)
	ImageContent ({ type: image, data: base64(...) }}
	EmbeddedResource : Filename instead of actual file content
	
Three transports:
	stdio - subprocess pipes - lowest latency
		1. Use-case
			1. local dev
			2. integration tests
			3. single-tenant desktop apps
			4. spawn the server
			5. pipe stdin/stdout
			6. Kill on exit
	SSE - Server-sent events over HTTP
		1. Legacy remote deployments
			1. Two endpoints (/sse + /messages)
			2. Use only if you inehrited it
				1. Server can send multiple events on a single connection
	Streamable HTTP - HTTP with chunked SSE response body
		1. Current spec preferred option for remote/multi-tenant
		2. Single endpoint, streaming on the same connection.
			1. Use this for new deployments
	
	Handled by frameworks
	
```
# stdio - subprocess, single tenant
mcp.run()

# Streamable HTTP - multi tenant, new standard
mcp.settings.host = "0.0.0.0"
mcp.settings.port = 8001
mcp.run(transport = "streamable-http")

# SSE - legacy, avoid for new servers
mcp.run(transport = "sse")
```

Streamable HTTP - HTTP/2 or HTTP/3
Websockets - more heavy
	1. maintains continous connection
	
JSON schema for handshake
	Steps:
		"method": "tools/list"
		
		tool list is returned
		
There is a spec for JSON, too
	`"jsonrpc": "2.0"`
		JSON-RPC 2.0 spec (google)
		
Tool loop

FastMcp?

	Uses annotations: `@mcp.tool()`
	`EmbeddedResource`
	
GitHub MCP server
	1. NPM package
		1. Agent spawns Github MCP server
		
	2. Get classic token from Github - easy to work with
	3. We need to define parameter types for `@mcp.tool()`
	4. Docstring is also required
		1. Description, parameters etc. are required to be sent back for LLM calls
		
Sorry, could you please explain why docstring is required again?

In traditional coding it is used for humans to interpret coding, but in MCP a docstring acts as the tool's interface description that a LLM reads to understand when and how to use it

What MCP does not solve for you:
1. Idempotency
	1. Retries after timeuts hit your server twice
	2. Cost accounting
	3. Determinism
		1. Two calls with identical arguments can return different data if the backend system drifts
			1. Caching
			2. Timestamp versioning
			3. ...
	4. Prompt injection defense
		1. "Ignore previous instructions"
	5. Audit
		1. Server log is not enough
			1. Correlate host-side JSON-RPC id with the server-side resurce access log
				1. For end-to-end tracing
				
Google ADK + A2A Protocol
	Goal: Build a complete multi-agent negotiation system using Google ADK
	
ADK:
	Agent Development Kit
		1. Open Source Framework
			1. Provides tools
		2. Alternatives
			1. Autogen
			2. Langchain
			3. ...
	Concepts:
		1. Agent
		2. Tools
		3. Runners/Executors
		4. Memory & Artifacts
		5. Workflows/ Orchestration primitives
		6. Telemetry & evaluation
		
```
root_agent = LlmAgent(
  name="basic_agent",
  model="openai/gpt-40",
  instruction="Use get_quick_estimate when asked about properties.",
  tools: [get_quick_estimate]
)
```

UI - has traces
	state
	artifacts
	...
	
ADK can spawn MCP server, connect to it and get the results

```
MCPToolset
```

Sessions and States:
session table
user_states table
app_states

`tool_context.state["offer_history"] = history`
`tool_context.state["user:total_offers"] = len(history`

How does the server use the state?
state is used as working memory and operational scratchpad for back and forth

We can store info for a session, across sessions, across users, etc.

Loops:
Sequential loop
	Each output is stored in the session
	
	output key scopes what agents can see (across agents)
	
	`SequentialAgent`
	
Parallel Agent - Fan out

```
schools = LlmAgent(output_key = "schools", ...)
comps = LlmAgent(output_key = "comps", ...)
inventory = LlmAgent(output_key = "inventory", ...)

root_agent = ParallelAgent(
  sub_agents = [schools, comps, inventory],
)
```

`LoopAgent`

```
def stop_when_in_range(callback_context: CallbackContext):
  price = int(callback_context.state.get("proposal", "0"))
  if 450_000 <= price <= 470_000:
    callback_context.actions.escalate = True
	
root_agent = LoopAgent(
  sub_agents = [haggler],
  max_iterations = 5,
)
```

Agent-as-Tool

```
valuator = LlmAgent(
  name = "validator",
  description = "Estimates fair market value of Austin properties."
)

root_agent = LlmAgent(
  name = "coordinator"
  tools = [AgentTool(agent = valuator)],
)
```
		
	1. Based on input from user, coordinator can design what other agent to call
	
Mixture of experts pattern
...

Callbacks:

Call a callback before calling the LLM
	1. Example: Guardrail
	
Before tool callback
	1. Example: Restrict tools
	
After tool callback
	1. Example: When tool has returned
		1. Example: handle prompt injection, caching, etc...
		
{before_model]
[before_tool]
[after_tool]
[after_model]

Event Stream:

Tool call writes to state and other tools can use it

What is A2A?
	Agent to Agent Protocol
		1. Problem: What if they're on different machines, different teams, different languages?
		
	A2A solves this. it's an open protocol for agents to discover and communicate over HTTP
		1. Similar to MCP
		
	Operations:
		1. Discovery: GET /.well-known/agent-card.json
			1. Who are you and what can you do?
		2. Schema: Agent Card - name, description, skills, capabiliteis
		3. Invocation: POST /(JSON-RPC message/land)
		
	Without A2A
		1. Buyer and seller are Python objects in the same process
		2. They communicate via shared session state (output_key, {placeholder})
		3. Tightly coupled - you must import both to run either
		
	WITH A2A
		1. Buyer runs on Machine A, seller runs on Machine B
		2. They communicate via HTTP JSON-RPC
		3. neither knows how the other is build - only the Agent Card
		4. Could be different languages, different teams, different companies
		
Agent Card:
	Agent name
	URL
	What it does
	Authentication (how to authenticate)
	Skills
	Capabilities
		Streaming
		
A2A Wire Format:

