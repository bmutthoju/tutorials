# LLMOps Part 1: Operating AI Systems in Production
Wednesday - Technical Coaching Session
	Q&A
The Ops Mindset
MLOps
LLMOps
Integrated Demo

Software Ops to AI Ops
	Traditional software follows deterministic logic. AI ssytems behave probabilistically - this shif changes everything about how we operate them.
		Software: Testing for pass or fail
			Monitoring - Latency, CPU, Memory, ... (Metrics, Traces, Logs)
				Binary monitoring
				
		LLMs: 
			Temperature - varies determinism
				There is still a chance that response will be different if we set temperature = 0
			How to write tests?
				Is the answer factually correct?
				Is there any hallucination?
				Is the answer relevant?
				
			Monitoring
				Answer relevance: w1 - 91%, w2 - 84%, w3 - 76%
					Statistical signals monitoring
					
			Failure detection: Gradual (not immediate)
				We see degradation over time
			Observability:
				Trace inputs
				Trace prompts
				Trace outputs
		
		SoftwareOps:
			Is my service running?
			What is the health of the service?
		
		MLOps - Is my model performing with atmost accuracy?
			Data
			Training
			Model deployment
			Model versioning
			Monitoring
			Fraud detection
			
		LLMOps: Is my LLM producing good, safe, grounded responses?
			Prompts
			Token economics
			RAG
			Evals
			Guardrails
			
		AgentOps: Is the AI agent reasoning using tools and taking actions correctly?
			LLMOps + the others below:
				Tools
				Memory (for the agent)
				Agent state
				Orchestration
				...
				
Deterministic software vs probablistic AI
	Deterministic: binary
		No variance
	AI systems: failures are gradual and dependent on the data (contextual, data-dependent)
		Variance - The responses may be correct but the language or style may vary
		Non repeatability - you cannot replay a request and get the exact same result
		Drift - model behavior degrades over time without any code change
			Application code is the same but responses degrade over time
				Why?
					RAG - Vector store - it might have become stale - possible drift
						Maintaining quality - keeping them fresh
		Emergent behavior - unexpected outputs from context, data, or prompt interactions
			Small change in prompt can trigger it
				- version controlling prompts is important
					- benchmarking them with evals
					
MLOps:
	Is the transaction froudulant?
	Forecast ice cream sales in Jan
	Is X is a good customer?
	
	Data pipelines & feature stores
	Model training & hyperparameters
	Model registry & versioning
	Deployment & rollback automation
	
	---
	Model v1 - 94%
	Model v2 - 89% (precision)
		Roll back to Model V1
		
	How good are
		Data
		Features
		Hyperparameters
	
LLMOps
	Prompt management & versioning 
	Context window optimization
		Length of tokens sent to LLM
	Token cost monitoring & budgets
	Guardrails & safety layers
		PII
	Evaluation pipelines
		LLM as a judge
		
	Multi-step workflow orchestration
	Tool calling reliability & retries
	Memory & state management
	Multi-agent coordination
	
	---
	We are not concerned about the model
		It is already good
			MLOps is taken care of
		Model is fixed
	We are concerned about things we build around it
		Prompt
		Context
		RAG
		Guardrails
	
	
AgentOps
	LLM is fixed
	Is it following the steps correctly?
		With a graph of agents
			Supervisor (coordinator)
			Fraud agent
			Account agent
			Support agent
	
	
System prompt: Role (travel assistant, say)
	Fixing it for each user prompt
	
How to test?
	Factual relevancy
	
	Evaluation frameworks
		Ragas
			Factual correctness
			Scores
			
		Against golden dataset
		
		We can also evaluate ssytem prompts (P1 and P2)
		
		if context is too big?
			Cost is high
			Latency is high
			Accuracy is low
			
			We should retrieve only fewer relevant chunks in a RAG system
				Ranking must also be good
					We need to ground the LLM using good quality context
					
	Skills
		Path to follow for the skill is given (workflow based)
		Instead of system prompt
		
Failure modes
	Data drift: Input distribution shifts; model silently degrades
		Software system: service is down
		LLM: GenAI system is degrading in quality (not down)
			non-relevant responses
		
		LLM - training on simple prompts but user input is complex
	Concept drift: Target variable changes meaning over time
		LLM - best flight means cheapest flight (as per user's preference)
			Best flight is now good food, ancilliary, baggage mamangement, luxury, zero layover, etc.
				The concept has changed over time
				
	Prompt Drift: Small propmt edits cause quality regressions
	Tool failures: Agent tool calls timeout or return bad data
		Function fails to return
		
	Hallucination: Confident but factually incorrect output
	Cost explosion: Token runaway loops in agent chains
	Latency amplification: Chained LLM calls multiply end-to-end latency
		LLM1 -> LLm2 -> LLM3 -> ...
		
AI System Lifecycle

Data -> Model -> Prompt -> Agent -> User -> Feedback

Phase:
	Data collection
	Data processing - clean, dedup, chunk, embedding
	Model training - pretrain, finetune, posttune, ...
	Model deployment
	Prompt engineering - tweaking input so that it behaves the way we want it to behave
	Agent orchestration - tool calling to take actions (reasoning, actions)
	User interaction - HITL
	Feedback loop - HITL
	
Observability
	Software
		Logs
		Metrics
			up and running
		Distributed traces
		
	LLM
		prompt version tracking
		Model response scoring
		Human feedback capture
		Cost tracking per request
		Latency per tool call
		Drift monitoring over time
		
Langfuse
	tokens consumed
	latency (trace)
	Version control prompts
		If we are happy with one, we can promote it to production
	Eval pipelines
		(alternative: Raga)
	
7 core principles
	Expect uncertainty
	Instrument everything
	Version Prompts like code
	...
	
Demo: Why LLMOps is needed

Deterministic vs Probabilistic behavior: You need behavior tests (distribution/score), not exact-match assertions
Prompt drift regression test: Prompts must be verisnoned + evaluted by code
Hallucination vs grounded answers (RAG): Guardrails + grounding reduce plausible wrong outputs
Agent tool failur + retries
Cost & latency explosion in multi-tep chains:

`!pip install -qU langchain-openai tiktoken numpy pandas`

temperature - 0, 0.7, 1, 2
	0 - precise responses and deterministic
	2 - randomized or imaginative
	0.7 - balanced
	
Measuring variances
	Generate hashes of each response
	Find unique hashes
	If hashes are different, there is variance
	
Prompt drift regression test
	What if someone changes prompt
	
LLM As a judge
	Scores answers based on change in the prompt
	
	Unit-test equivalents
		Score per prompt based on golden dataset
		
Deterministic tests
	Regex matching
	Schema validation
	Number of words matching
	...
	
	Cosine similarity
	
Tools are in most cases deterministic functions
	Simulate a tool that fails 40% of the time
	
Cost & Latency
	input cost per 1k tokens
	output cost per 2k tokens
	
SLO - Cost & Latency are first-class SLO (predetermined)
	There must be a cutoff for each
	
MLOps
	Train -> Version -> Deploy -> Monitor -> Rollback
	(Data + hyperparams)
			(Registry + lineage)
						(Canary / Shadow)
								(Quality, Drift, Cost)
											(Auto or Manual revert)
		
DVC - Data version control
	
	Data -> Feature stores -> Model training -> Tune hyperparameters -> Eval -> Deployment -> Continuous monitoring
	
MLFlow model version control

Airflow
	DAG: Machine learning workflow can be defined
		The lifecycle can be automated, monitored, and versioned
		
Evaluation
	Two ways
		Offline
			With hold out data
				Split golden dataset
					Training data
					Testing data (offline evaluation)
						F1 scores
						Blue scores
						LLM as a judge
						...
			Precision
			Recall
			F1
			BlEU
			ROUGE
			Safe
			Repeatable
			Cheap
			Regrssion gate
		Online
			A/B tests
			Shadow tests
			Interleaving
			Business KPIs
				Clicks
				Views
				Screen-time
				...
			Engagement
			Revenue
			Real user behavior
			Validated in the wild
			
Code change -> Offline Eval -> Deploy (Canary / Shadow) -> Online Eval -> Full Rollout

Business KPIs - Product leadership decide them (PM, TPM, EM)
	Revenue impact
	Conversion rate
	User satisfaction - NPS, CSAT
	Retention and engagement
	Task completion rate
	
Canary - reduce deployment risk
Poor canary sampling (selection bias) can skew the performance of the model wrt online evaluation metrics

Data Drift vs Concept Drift
	Data drift - Input feature distribution changes over time
		Old data vs new data
			Distributions changed
			
			Example: 5000 pm to 2L pm with 50k as average
			Example: 20000 pm to 4L pm with 1L as average
	Concept drift - Relationship between input and target changes
		y = f(x)
			it changes over time
			
	Mitigation:
		Scheduled retraining
		
		Drift alerts
		KSI index drift
		CSI
		PSI 
		
		Software: evidently - run tests automatically
			Trigger mitigation strategy on dection (threshold is defined)
			
		Human-in-the-loop review
		
		Canary evaluation
		
Dashboards
	Model Health Score
	SLA Compliance
		Latency & uptime vs agreeed targets
			Told to customers (legal consequences)
			
Shadow
	New model gets the same traffic as the current model
		The results are not shown to the customer
			Offline and online evaluation is done
	Costly
	for: high-risk changes, new architectures
	
Canary
	Small real exposure
	for: iterative quality improvements
	
Blue/Green
	Instant traffic switch + instant rollback
	Two full environments
	
LLMOps topics:

Prompt Lifecycle and Prompt Versioning: Langfuse
Model Selection and Routing Strategies
	1. Simple question -> Small model
	2. Complex question -> Large Model
	3. Sensitive question -> Self-Hosted
Latency / Cost / Quality Trade-offs
Caching Strategies: Exact and Semantic
	Questions and answer are stored in a cache
		Word-by-word matching
			If it was answered before, we don't need LLM
	{Q: A, Embedding(Q)}
		Retrieve the answer without LLM and send back
		
Langfuse
	Observability and Evaluation Platform
	Organization, public key, secret key
	Fetching metrics
	Traces
	
faiss - vector store
pydantic - schema enforcement model

PII detectors - Presidio

Prompt injection detection at scale

---

AgentOps
Evals & quality
Reliability & Cost
Integrated Demo

Caching - to reduce LLM cost
	Exact-match cache
	Semantic cache (FAISS): Similar inputs -> return cached output via FAISS vector simiolarity search
		What is FAISS? - vector store
		
AgentOps Fundamentals
	The four-phase agent lifeecycle and why each phase matters
	Single-agent vs multi-agent systems and when to use each
	Tool reliability engineering: retries, timeouts, circuit breakers
	Memory architecture: working, short-term, and long-term layers
	Agent-level metrics and how to define SLAs before launch
	
Four-phase agent lifecycle
	Build
	Run
	Monitor
	Improve
	
Multiple agents
	Scalability
	Parallelism
	Complexity management
	
	User query -> Supervisor / orchestrator -> Agent A
	                                        -> Agent B
											
				  It decides how to distribute the work
				  
	Peer-to-peer
		Agents check and criticize each other
		
	Agent swarm
		Agents talk to each other
		Starting point - sends to a single agent
		Each agent supervisor and a worker
	
	Workflow
		Human defines the sequence of agent calls
		
LangChain ecosystem
	Deep Agents
		Harness building
			Context management is taken care of
			
			Example: Claude
	LangGraph
		Building graphs
		
		State control system
		
	LangChain - linear chains
		For simple chains
			
		Task 1 -> Task 2 -> Task 3 -> ...
			
	LangSmith
		Default tracing framework for the above
	
LangFuse - different from the ecosystem

http://anthropic.com/engineering/building-effective-agents

LangSmith - no much configuration and good integration with LangChain but expensive
LangFuse - Cheaper, some configuration code

Tool Reliability and Agent Failure Modes
	Infinite loops
		Agent retries failing tool or ocillates between two states
			Solution: Loop rate metric, max iteration alert
	Tool misuse - Wrong tool called, wrong arguments, or hallucinated tool name
		Solution: Define a schema of the tool
			Schema validation errors
			Argument type errors
	Compound errors - Wrong tool called, wrong arguments, or a
		Bad tool result -> worse LLM decision -> cascading failures
			Cascade of errors due to wrong tool or wrong arguments passed
		Solution: End-to-end trace - each step looks 'reasonable' individually
	Context overflow - Agent accumulates too much state, exceeds context window
		Solution: Token count metrics
			Truncation warnings
	
Router agent - just routes requests

state - passed among the agents

How to choose between LangSmith and LangFuse?
$ Value. Large companies have adopted LangSmith to begin with but in parallel are devising a wrapper on top of Langfuse for long term cost optimization. For these companies - monitoring and alerting is top most priority.

Each node populates the state with the respentive information

Merge node - merges results and gives the final response

LangGraph give visualization of the graph

Router vs supervisor
	Supervisor - two and fro between agents and supervisor
	Router - Only routes and one-directional to the agents
	
Agent is a graph in some cases
	`create_react_agent` - a graph is generated
	
Tool Reliability and Agent Failure Modes:
	Tool returns bad data
	LLM makes decision on bad data
	Agent calls tool: wrong args
	Tool fails or returns worse data
	LLM makes worse decision
	Circuit breaker fires
	
Mitigation Strategies
	Retries + exponential backoff
	Timeout limits
	Schema 
	Circuit breaker
	
Simulate a failing tool using probablistic failure

Circuit breaker:
	If circuit open
		Return a fallback response
	If tool call fails
		Retry attempts is incremented to a max limit
		After each attempt, exponential backoff is applied
		set circuit to open - for certain amount of time
		
Working memory
	Current context window
		What the agent is currently using
			User question
			Current tool results
			Current reasoning steps
			...
Short term memory (current session)
	Conversation history
	Session tool results
		Earlier messages in the chat
		Temporary task state
Long term memory
	User preferences
	Past interactions
		Episodic memory
	Patterns (repeated patterns)
	
	
Procedural memory
	Prompt
	Skills
	
	Guides LLM with the workflow
	
Semantic memeory
	RAG
		Knwledge bases are stored

Empisodic memory
	Past interactions
	
Context management challenges?
	Compaction - summarizes conversation history
	
Hallucination - grounding it with knowledge base
	RAG
	
Cost compounding - free up some of its context

How to prove that an agent is working fine?
	Did the agent achieve the user goal?
	Was the answer correct?
	Was the trace correct?
		What are the number of steps to completion?
	Quality metrics
		User satisfaction score
			Thumbs up or thumbs down
	Safety violations
		Did the agent expose PIT?
		
Operational metrics
	End-to-end latency (p95)
	Cost per task
	Error rate
	Loop rate
		% tasks hitting max iteration limits
		
Quality gate
Cost budget
North star

Multi-turn conversation - human -> assistant -> human -> assistant -> ...

If tokens are increasing
	Summarize after few turns (3 say)
		Using LLM
	Replace the history with the summary
	
What is Jev?
	Takes decisions
		Saves token cost
		Routes
		Fast

How does compaction work?
	`SummarizationToolMiddleware`
	
Evaluation & Quality Management:
	Task-level vs system-level evalution - scope and ownership
	Automated vs human evaluation - when to use each an how to combine
	Regression testing for prompts
	
Task-Level (engineer evaluates them)
	One prompt -> one response
		Output relevance
		Fairness
		Format compliance
		Safety
	Owner:
		Engineers
			Runs in CI/CD
			Gates every deploy

System-Level - Checking the entire workflow (across agents)
	Across agents, tools, retrieval, routing
		Task completion rate
		Tool selection accuracy
		Retrieval quality
	
Automated vs Human Evaluation
	Automated - for scale
		CI/CD gating
	Human - judgement, calibration
		Calibrate golden dataset
			Expected behavior is evaluated (to compare)
			
		Periodically sample
		Re-calibrate
			Golden responses are added by humans for the sample questions
			
		AGI arc - golden dataset (public)
		
Evaluation pipeline:
	
Regression Testing for Prompts and Agents
	Prompt regression
	Agent regression
	Model regression
		smith tune langsmith
			Finetuning based on the traces
			
Golden Dataset vs Synthetic Data
Source: Human-verified vs LLM-generated
Quality: High vs Variable
Cost: Expensive vs Cheap
Best use: Hight-stakes gating vs Broad coverage

Building a Golden Dataset
	Production traffic
	Sample diverse examples
		Diversity sampling
			Generate embeddings
			Generate clusters (20 clusters, say)
			Each cluster - 500 examples
			From each cluster, randomly sample questions
	Human review + annotation
	Approve / correct
		Langfuse annotations
	Golden dataset
	
Rate limiting
	How many requests your system accepts in a given period
	Token Bucket rate limiter
		
Fallback
	If it is allowed, goes to the primary LLM
	If no, 
		fallback model
		|
		v
		cache
		|
		v
		static fallback
		
Cost monitoring

Latency
	Streaming responses
	Exact-match caching
	Model selection
	Shorter prompts
	Smaller output limits
	Parallel tool calls
	Semantic caching
	
Production Dashboards
	Langfuse dashboard