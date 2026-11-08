# Live Safe, Evaluated and Cost Optimized Agents Class with Vinoth

Checklist before production
Key aspects in production
	For resilience
	
Reliability
Governance
GPU Optimization
Optimization techniques

LangSmith (other similar tools exist)
	Native integration with LangGraph
	
https://github.com/jeev1992/fintech-agent-observability-evaluation.git
	
	pip install -r requirements.txt
	
	Configure OpenAI API key and GOOGLE API key
	
LangSmith
	Datasets + A/B Experiments

DeepEval
	Faithfulness . MRR . G-Eval
	
Module c: Input Guardrails
	Open AI Moderation API
	Regex Guard
	LLM Injection Classifier
	Presidio PII Redaction
	
Agents
	Supervisor classify_intent()	
		Account Agent
			MOCK_ACCOUNTS dict
		Escalation Agent
			Empathetic handoff
				Support tickets
		Policy Agent
			RAG
			Chroma
			4 docs
		
Observability
	What went wrong?
	Are the business KPIs being met?
	
	Agents space
		
LLM - Predicts the next token based on prompt
	Returns the most probable token among many tokens
		Needs better observability platform because it is non-deterministic
		
Observability vs Logging vs Monitoring
	Logging
		Splunk
		ELK stack
	Monitoring
		Metrics
			System
			User
			Performance
			p99, p95
			...
		Kibana
	Observability
		Traces
		...
		
MOCK_ACCOUNTS

Lost in the middle - top portion and bottom portion are used effectively but not the middle part of the context

Failure points
	Retrieval errors
	Routing issues (to wrong agents)
	
