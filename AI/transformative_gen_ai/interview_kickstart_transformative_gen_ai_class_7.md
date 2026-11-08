# Multimodal Conversational System
Learning Objectives

1. Voice agents
2. Concept of Sub-Graphs in LangGraph
3. Human in The Loop (HITL)
4. Multi-Modal Conversational Agents

Voice agents:
1. Customer support
2. Hands-free interfaces	
	1. Ideal for driving, accessibility, and industrial settings
3. Sales & Outreach 
4. Banking & Finance 
5. Personal Assistants
6. Healthcare Triage
	1. Collect symptoms, guide patients to the right care
7. Language Learning
8. Smart Home Control
	1. Voice-driven device and environment management
	
How do voice agents work?

Audio -> text -> LLM -> text -> Audio

Speech to text (Wishper)        text to speech (Eleven Labs Model / Kutai.ai) (cheaper)
(proprietary version)

--- Cascaded Architecture
	1. More control
		1. We can guide LLM on how text is generated etc.
	2. More cost efficient
	3. Information loss
		1. If there is an error in speech to text, etc.
	4. Maintenance overhead

Audio, Text -> LMMs (Large Multi-Modal Models) -> Audio, Text

	Real-Time Architecture
		1. Vendor lockin 
			1. GPT-Realtime
			2. Eleven Labs
		2. Trained
		3. Easy to setup
		4. It can be more accurate - sarcastic
		5. They can natively understand audio, text, video, etc.
		6. Faster
	
TTS-1 - Text to speech
	1. 1M characters = $15
GPT-Realtime 2
	1. 1M tokens = $32 + $64
	
Tradeoffs: Convenience vs quality vs cost

Voice agents:
Listen - think - Speak

Cascaded Pipeline
	STT -> LLM -> TTS
	
Chained Architecture: The 'Sandwitch'

Example:
Qwen3-TTs, Eleven Lab TTS & STT APIs, OpenAI Whisper, gpt TTS & STT models

User audio -> STT -> Agent -> TTS -> Audio

Realtime Architecture

Audio -> App -> Agent -> App -> Audio
	1. Low latency
	2. Multimodal understanding
	3. Natural conversational flow
		1. Latency
	4. Vocal context understanding
	5. Limited options
	6. Less transparency (no custom agent loop)
	7. Limited flexibility
	
Langgraph

nodes - Agents/ Python functions
Edges - Connections

Subgraphs
	Deep Research Agent
		1. Example: Babyproofing the house
			1. Goes through videos, blogs, ...
			2. Gives a summary
		2. Alternative:
			1. Agent (rewrites user prompt by asking questions to user)
				1. Triggers: 
					1. SubAgent (searches web)
					2. SubAgent (Searches youtube video transcripts)
					3. SubAgent (Internal data sources)
						1. Built using subgraph
				2. Outputs document (final output)
	We can re-use the subgraph in another workflow
	It is also a graph
	
	It is a graph used as a node in another graph
	
	Two ways
		1. Call subgraph in a node
			1. If state-schemas are different
		2. Add a subgraph as a node (cleaner)
			1. If state-schema is shared
			
Multi-Agent Voice Shopping Assistant

Huggingface
	modulate/vfast - word error rate (lower the better)
	microsoft/azure-speech-06-2026
	
LLMOps
	1. Langsmith
	
		Eval -> Deterministic evals (have a group truth dataset)
					1. Sample data from production system
			 -> LLM as a Judge
				1. LLM Council / Panel as a Judge (next level) (multiple models act as a council)
					1. Evaluates if the end-to-end flow is correct
					
Business Metric
	1. User query ~ 2 mins
	2. 1 $ / avg cost for a user query
	3. 4.4/5 - Customer Satisfaction
	
		1. Agent objectives
			1. User query ~ 30 sec
			2. CSAT - 4 / 5
			3. cost per query -> $ 0.75 


If we use LLM Councill / Panel, do majority of them need to agree? Is that the evaluation criteria?			
Not necessarily; an LLM council can use majority voting, weighted voting, consensus, ranking, confidence scores, or a separate judge model—the evaluation criterion depends on the system design.

C4 dataset - open source - can be used for training (Colossal Clean Crawled Corpus)
	1. Open AI has their version of C4
	2. Anthropic has their version of c4
	
`uv` - faster virtual environment (built with Rust)
	1. Instead of `venv`
	2. Install
	
	```
	pip install uv
	```
	
	3. Virtual environment: `uv venv`
	
`import logging`

	logger = logger.getLogger(name)
	...
	
	OPENAI_API_KEY = os.environ.get("OPENAI_API_KEY", "")
	
System prompt
Guardrail
	1. model to filter questions only
		1. LLama - 1B/7B
			1. Classifies questions
		2. Acts as a validator agent
		3. The prompt is routed to powerful models only if it is relevant
			1. Or send only relevant part
	2. Llama Guard - 2024
	3. Nemo agent toolkit nemo guardrail
		1. Library
			1. Prompt-injection attacks can be prevented
	4. Azure content safety
	
	We can index details in Vector DB and build a RAG system for validation (RAG only for internal data)
	+ System prompt
	
	https://github.com/NVIDIA-NeMo/Guardrails
	https://github.com/nsr-19/axiomcart-ai-assistant/tree/main
	
	ChromaDB - Vector DB
	
	Langchain document
	OpenAIEmbeddings
	
	`@tool search_product_catalog(query: str) -> str # decorator`
	
	Indexing using metadata (not full content)
	
LangGraph MemorySaver alternatives:
SqliteSaver
RedisSaver

Pydantic
	1. For structured outputs
	
https://thinkingmachines.ai/blog/interaction-models/
https://openai.com/index/introducing-gpt-live/
https://unmute.sh/
https://learn.microsoft.com/en-us/azure/ai-services/content-safety/quickstart-jailbreak?pivots=programming-language-rest
https://github.com/kunchenguid/no-mistakes