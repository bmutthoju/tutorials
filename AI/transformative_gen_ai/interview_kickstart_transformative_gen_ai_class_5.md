## RAG Pipeline
Previous chats info will be used in subsequent chats
Evaluation offline
What to do if a retrieval metric is looking bad
	1. Agentic RAG
		1. Using intelligence of LLM to understand the complexity of the query and based on that, do retrieval
			1. Example: Book a trip to Japan
				1. Multiple Google searches
					1. How many retrievals required?
					
Knwoledge base
	1. We believe will be useful to answer the question
	2. We break the knowledge into chunks
	3. Embedding models will generate vectors
		1. Similar vectors
	4. Cosine similarity
	5. Stored in Vector DB
	
```
Query -> Query Vector -> Top-K Docs -> Augmented Prompt (prompt - instructions + context) -> Grounded Answer (Generation)
```

When to increase or decrease k?

Choices
	1. API responses can be different from Open AI and Anthropic
	2. DB: Chroma vs Facebook AI Semnatic Search (C and C++)
	
	
What if someone does the choice for you?

LangChain - Ahead of everyone
	1. They give the building block as wrapper over functionality givin by others (DBs, APIs, ...)
		1. We only see LangChain code
			1. They will handle internal implementation
	
	2. It is Open Source framework
		1. Very popular
LangChain Cloud
LangSmith - Tracked and observable
	1. Dashboard
	2. Tools calls
	3. Conversations
	4. Prompts
	5. ...
LangServe

Langflow:

Langflow is an open-source visual tool for building AI and LLM applications using a drag-and-drop interface. It lets you connect models, prompts, tools, memory, and APIs into workflows without writing much code, and you can deploy or export those flows as APIs or Python code.
		
Airflow and Airflow DAG?

Langfuse

How to ensure that the instructions + context doesn't exceed the size limit set for the LLM?

Instructions (limit it) + context (max size can be limited or summarized)
Response - limit it or summarize it

Follow-up questions:
What is the latest iPhone?
What is the price of it?
	1. it - not understandable by a vector db
		1. chat history + current question - generate a standalone question (what is the price of iPhone 17?)
			1. LLM - extra call is made
				1. How much history? Depends on how much an LLM can take
				
Summary + recent chat history
	1. PostgreSQL - old chat history
	2. Redis - recent chats, summary (fast, distributed, but expensive)
	
proofmd.ai
	1. Read is done from cookies
	
https://openai.com/index/scaling-postgresql/

Scaling PostgreSQL to power 800 million ChatGPT users

Chat GPT Memory - just txt files
	
## Evaluation
Certain questions can be used for evaluation
	1. If used by user, sample the requests (evaluation questions)
	2. If new system:
		1. Example: Ask LLM to generate evaluation questions
		
		```
		I am trying to evaluate my Wlamart Sparky AI bot on some user queries, but right now I am ... give 20 queries.
		```
		
		Rank documents based on similarity
		
		How to decide if the top K documents are relevant or not
			1. appen.com
				1. Humans that will do the labeling
			2. AI can do it
				1. ChatGPT
				
				```
				Query: What is the price of iPhone 17?
				Contex: Price of iPad is $999 US
				
				Can you evaluate if the retrieved context is relevant to hte user's question? ...
				```
				
			3. We need subject-matter experts
				1. Human or AI
					1. Always give reasoning - if cheaper
					2. Ask for reasoning only if there is a doubt - cheaper
Metric:
	1. Recall (R)
		1. Out of everything that is labelled relevant, how many did we retrieve?
			1. Top K = 3
				1. How many did my subject matter expert label as relevant?
					1. precision (p) = 2/3 etc.
						1. Out of everything that we retrieve, how many were relevant?
				
Ranking evaluation:
	1. Ranking metrics are different
		1. Mean reciprocal rank
		2. Mean ...
		
R = 0.5, P = 0.66
R = 0.

F1 score = harmonic mean of P and R
= 2 PR / (P + R) = 

	1. Either or both should go up and only then harmonic mean goes up
		1. If they go in opposite direction, you are penalized
		
If harmonic mean goes up, change k
	1. F1-beta scoring

labelstud.io - manual labeling UI

Amazon SageMaker Groundtruth
Amazon Mechanical Trunk

Semi structured data? Ask humans to label

Generation metrics:
	1. Groundedness - the most important metric
		1. Can my generated answer can be fully supported by my retrieved context?
			1. Example: Jar of Jam
				1. Context: Great Value strawberry jam
				2. Answer: Kirkland straweberry jam (competitor brand)
					1. Not grounded by the context
						1. It must be 0.8+
	2. Relevance: Is what the user is expecting?
		1. 0.8+
	3. Completeness: Are we covering all the key points in the document?
		1. Very subjective
			1. 0.8+ (may be it has bias)
		2. This is a tie-breaker for groundedness and relevance
		
Triangulation can be used with AIs and/humans for evaluation
	1. LLMs have a bias - they prefer their own output
	
Retrieval issues:
	1. Precision is high, recall is low
		1. Increase the value of k - simplest
		2. Try smaller chunks
		3. Better embedding model
		4. Go with hybrid retrieval
			1. Vector matching + text matching
	2. Precision is low, recall is high
		1. Most of the time, we are good with this
			1. LLMs are decent with recall
		2. If precision is too low
			1. We can try using metadata filters
				1. Classify the documents and filter
					1. Example: Android phone
						1. Showing android phone case
							1. Filter: phone case - classified as accessories
								1. Phone - main products
		3. MMR (Maximum Margin of Relevance) - <q-doc> - <doc=prev-doc> (penalizing if it is similar to previous document)
			1. hacky
			2. Trying to introduce diversity into the results
	3. Bad generation
		1. Low-groundedness
			1. Not supported by retrieved context
				1. Write more system prompts
					1. "Do not answer if it not supported by the retrieved context"
						1. Give example
						2. Force LLM to site context used
		2. Verification step (high stakes systems - Financial, healthcare, ...)
			1. Redo by writing better
				1. Prompts
				2. Queries to vector DB
				3. ...
			2. Iterating
				1. Customer waits
				2. Costly
		3. Give examples in prompts
		
## Direct RAG vs Agentic RAG
Give some tools
	1. Simple python functions that my LLM can invoke whenever it wants
		1. ReAct prompt (ask for it)
			1. Describe the tools
				1. Standard format
	2. RAG tools - retrieval tools are given - makes them Agentic RAG
	
RAG Pipeline
	Prompt template
	
	lambda_mult * d + (1 - lambda_mult) * d_pd (how much diversity)
	
cosine can range from 0.1 to 0.6 (not 0 to 1)

RAG Pipeline with Chat history.

How to request more clarification from user:
Techniques:

	Agentic RAG can handle it
	Human in the loop (HITL)

Labeled evaluation dataset

Threshold for precision score can be set (not hardcoded k)

## Agentic RAG

Supported tools (Python functions)
	1. SearchSimilarTickets
	2. SearchByCategory
	3. GetTicketsStatistics
	4. GetTicketById

How to convert them to tools?
	
```
@tool
<signature>
# doc
```

OR

In the code

LLM:
1. Give tool in the expected structure OR
2. In code

https://chatgpt.com/share/6a4a0301-0238-83ee-9d8f-1256ce435d66


Generic function to execute any python code

```
pyton_code = """
  <code>
"""

exec(python_code)
```

