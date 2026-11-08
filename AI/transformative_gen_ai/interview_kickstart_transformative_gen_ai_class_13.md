Problem: end-to-end healthcare LLM fine-tuning pipeline
	1. We want to change the model itself
	
Parametric memory - facts that the model knows about the world
	It is preserved in the model
	
Fine-tuning production LLMs is expensive, irreversible, and commonly misapplied because:
	1. Engineers fine-tune before asking whether the base model already handles the domain - Qwen2.5-1.5B already knows medicine
	2. Training loss went down for both experiments; only external evaluation revealed that v1 produced dangerous outputs
	3. A model trained on 112,000 doctor-patient conversations answers stroke questons with diabetes advice - the data was the problem
	4. 2,100 clean WikiDoc examples outperformed 112,000 contaminated ChatDoctor examples on 2 of 3 metrics
	
Qwen/Quen2.5-1.5B-instruct (1.5 B parameters)
	If we train the model with cleaned data, the output is better
		Fine-tuning only helps only if the training is with cleaned data
		
Is my data right?
Fine-tuning ways
How to deploy fine-tuned model
Evaluation

Strategy & Dataset Preparation:

Problem: We need an LLM to perform well in a specific domain
	Most engineers reach for fine-tning immediately. This is almost always wrong
		1. Do a better prompt engineering
		2. Can we supply domain data from outside if the LLM doesn't have domain knowledge?
		3. After that, we can go with fine-tuning

Plompt engineer - jsut pay for tokens
RAG - vector db + embedding - some cost
	1. Takes a few days
Fine-tuning - GPU compute + curation - very expensive
	2. Takes many days
	
Fine-tuning is for training the model with new information that it did not have before (prompt engineering, or RAG will not solve the problem)

Prompt Engineering wins when the model already knows the domain and needs behavioral guidance per request
RAG wins when you need up-to-date facts, source citations, or documents

Fine-tuning
	Inconsistent tone or format?
	...
	
Domain-specific models may need only fewer dimensions (200 vs 1500 or 3000 (general purpose models))

Full-fine-tuning
	Change 1.5 B parameters
		Massive data is fed and it gets re-trained
	Needs teaching everything from scratch
		May forget known data
	We don't control the architecture but it is retraining basically
	
PEFT (LoRA / QLoRA)
	Partial fine-tuning
		We keep what it has learned and tune it partially for new data (it keeps what it knows)
		
	10-50 MB (adapter only)
		Added to base model
		
			request goes through the base model and the adapter
		
	We can stack adapters to learn new skills
	Better quality
	
	Cheaper to train
		May not spend even a dollar
		
PEFT Family: Five Methods
	LoRA
		Parallel lwo-rank AxB matrices added to forzen layers (default for most tasks)
			1. We don't touch the base model at all
				1. Like side roads without touching the main road
		Input goes to original model and separate LoRA model
			The output is combined between the models
				They pass through matrices
				
			Output formula: output = W_frozen(x) + (alpha / r) x B(A(x))
			
			r - 16, rank
				Increases capability to learn more things
			alpha = 32 - scaling
			B init = 0
			
			addition - only controlling how much output should come from adapter layer
			
		
		1536 by 16 x 16 by 1536
		
		Input size: 1536
		Output size: 1536
		
		We can choose 16, 32, ... (rank)
			higher rank gives better capability to the adapter

	QLoRA
	
		We compress parameters in the base model (16 bits to 8 bits, say)
			Converting parameter to smaller precision (reduces the storage)
		
		Quantized LoRA
		
		When to do? memory constrained
			Hardware constraints
			
		This helped a lot in the real world
	
	Prefix Tuning
		Not used anymore
		Very less parameters
			Only 40k parameters
			
		With every input, we add a prefix and train
		
		Learnable soft tokens prepended to every input
		
		It is like lane management in a highway (redirecting inputs)
		
	Adapter Layers
	
		Small MLPs inserted in series between transformer layers
			Multi-level perceptrons
			Small sections that can learn
	
	IA3
	
		Not used
		Learned scaling vectors multiplied against activations
			Each layer gets a vector (100 transformers get 100 vectors)
		Absolute minimum compute
	
			
Quantization
	4-bit quantization
		float16: 2 bytes/param
		4-bit NF4: 0.4 bytes/param
		
		3 GB - 0.75 GB
		
		Quality loss: ~1-2% on most tasks
		
	NF4 - Normal Float 4-bit
		We look at weights and they fall in a small range, we can reduce the number of bits per weight
		
	Double Quantization
		Second level quantization
			static
			while saving
		
Custom data sets:
		
Training Datal:
Ranked by cost and quality trade-off:
	Synthetic
	Curated from Docs
	Expert Annotation
		Domain experts write and label examples.
		Highest quality, highest cost. Justified only when synthetic and curated options are insufficient.
	Production Logs
		Capture real queries and curated responses from youre existing system
		
Quantify the problems:
	Persona contamination
	Boilerplate sign-offs
	Very short answers
	Safety disclaimers - "consult a doctor" (good practice for medical data)
	
`!pip install -q transformers accelerate bitsandbytes torch`

Qwen/Qwen2.5-1.5B-Instruct

	A lot of instructions exist for each model in Huggingface
	
Clean data + gentle training = success

Hugging face allows us to deploy the model
	Paid version
	
Merging with base model - only if required

Deployments
	Serverless
		Model is used occassionally
	Container-based
		Model is used a lot
	Dedicated GPU Endpoint
		Sagemaker
		...
	Model-as-a-Service
		Pay per token
		
What caused us to do the fine-tuning is the metric to use for evaluation

Example metrics:
	Helpfullness
	Accuracy
	Safety