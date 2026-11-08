# Hybrid Search & Retrieval
Internals of RAG
Implementation of algorithms

To make intelligent AI systems better

Topics:
Dense Vectors
Sparse Vectors
SPLADE
RRF (Reciprocal Rank Fusion)
Hybrid Search

Already covered:
RAG
Vectors
Embeddings
Vector Databases

Vector Embeddings: numerical representations of data points that express different types of data, including non-mathematical data such as words or images, as an array of numbers that machine learning (ML) models can process
	1. Meanings can embedded (not actual objects)
	
Venctor Databases: It indexes and stores vector embeddings for fast retrieval and similarity search, with capabilities like CRUD operations, metadata filtering, horizontal scaling, and serverless.

Venctor Index: e.g, FAISS
	1. We need to build db management on top of it
		1. Metadata filtering: Not supported
		2. Scalability: Requires custom solutiosn (e.g., K8s)
		3. Real-time Updates: Full re-indexing required
		4. Backups & Collections: Not available
		5. Ecosystem Integration: Limited
		6. Data Security: Not built-in
	2. Use-cases:
		1. POCs
		2. ...
Vector DB:
	1. Data Management: Built-in insert, update, delete
	2. ...
	
Retrieval-Augmented Generation (RAG)

Ingestion
	Collected
	Cleaned
	Indexed into searchable vector format
	
Retrieval
	Info is identified and extracted from the knowledge base based on user queries
	
Augmentation
	Retrieved context is integrated with the original prompt to provide additional knowledge
	
---

Search:
	Semantic search
		1. Converting to embedding
			1. Example: `Amazon echo` does not have an English meaning
				1. Returned items may not contain `Amazon echo` at all
					1. Solution: Direct search (exact search)
		2. Dense index
	Exact search
		1. If a description is given, this will fail but semantic search will succeed
		2. Sparse index

Sparse & Dense Vectors:
Dense Vectors
	Sematic Search
		Capture meaning and context behind a query. Used in semantic search to find conceptually similar results - even without exact keyword matches
	Similarity search doesn't work everywhere
Sparse Vectors
	Capture surace-level term matching. used in lexical search to find exact keyword matches - fast, predictable, and domain-agnostic
	
Why dense and sparse?
	Dense vectors - Where most or all elements are non-zero
		1. Majority of elements in the vector are non-zero
			1. Every value is important
		2. use cases:
			1. Semantic search
			2. Recommendation systems
			3. NLP
			4. Image & Multimodal Search
	Sparse vectors - High-dimensional vectors where most elements are zero
		1. Used in BM25 or TF-IDF algorithms
			1. Why?
				1. Example: "This is an amazing car"
					1. Dense vector - [0.1, 0.2, ....] (512, 1024, ...)
						1. Converting to sparse vector
							1. Depends on vocabulary of a sparse model
								1. All the words we have form a vocabulary object
								2. Each index can be representation of a single word
									1. Size: 30k to 200k size
										1. It is 1 if the word is present and 0 if it is not present
										2. How do we represent it?
											1, key, value pair
												1. 1 -> 1
												2. 2 -> 1
												3. 3 -> 1
												4. 4 -> 1
												5. 7 -> 1
			2. TF-IDF
				1. Term frequency, index document frequency

		2. Why?
			1. More predictable mathcing results
			2. Great for special terms, IDs, and eact phrases
			3. Lightweight and fast

How does embedding work?
	1. Embedding model
		1. Transformers internals
			1. Tokenization
			2. Attention model
				1. Outputs vector
		2. It cannot be reverse engineered
			1. Vector is only a representation of the input (different models have different representations)
			
Where is sparse vector stored?
	It is stored in the Vector DB
	
How are sparse vectors generated?
	Statistical techniques
		TF-IDF (Term Frequency-Inverse Document Frequency)
			1. Assigns weights to words based on frequence and importance across a corpus
				1. TF - how many times does a word repeat?
					1. Example: How many times does `car` appear in a document?
				2. IDF - Words repeated more across documents are scored less
					1. Words repeated less across documents are scored more 
						1. Rare words get more score
					2. Words closer to zero will be made zero
				3. TF and IDF are multiplied together (dot product) for each word
					1. The score is maintained in the sparse vector
		BM25 (Best Matching 25)
			1. A ranking function that improves on TF-IDF for information retrieval
			2. If we have a long document, even rarer words repeat many times
				1. Cuts off by normalization
	They allow us to do exact match
	
What if we mix both?
	Amazon dot (not semantic) -> Amazon echo (exact)
		1. It should be both
			1. Solution: Neural Sparse Embedding Models
				1. It does exact matching but also uses synonyms
					1. Vegetation, rain forests, etc...
				2. Example: SPLADE, UniCOIL
				3. Learned methods that generate sparse representations by training on large datasets - combining the efficinecy of sparse vectors with the intelligence of neural networks
		2. We need to combine
			1. Statistical
			2. Semantic
			3. Neural Sparse Embeddings
			
How do vector stores find similarity?
	We need a way to measure differences between vectors
		Cosine similarity
			1. It is high for similar vectors
	Four main
		Manhatten distance
			Sum of absolute distances
				High-dimensional sparse data
				Robust comparisons
		**Euclidean
			Distance between two points
			Use cases:
				Spacial data
				Image embeddings
		**Cosine
			We are only concerned about the angle between the vectors
				The closer the angle, the more similar they are
			It doesn't care about the distance (magnitude)
			Best for text embeddings
				NLP
				Semantic search
				text embeddings
		Chebyshev
			`max(|ai - bi|)`
			Grid-based movement
				Map-based
			Feature-dominant comparisons

Search
	It is the nearest neighbour search
		K Nearest Neighbors (k-NN)
			Take all scores
			Descending order
			Take top k
				Problem: For each query, we need to scan all the vectors (time increases with the number of vectors)
					It does not scale
			Most accurate
		Approximate Nearest Neighbor (ANN) (close to KNN)
			Reduces computational time
				Can get up to log N complexity
				Tradeoff is very little (99.5% say)
			It builds index structures to narrow down
				Idea?
					HNSW - Graph-Based Indexing - Hierarchical Navigable Small World
						Hierarchical proximity graph - stacking layers of proximity links between vectors
							Small world?
								Based on linked-lists
								
							Concept 1: Skip Linked List
								Layers of dataset
								At every level, a part of the set exists in decreasing order
								We can only enter from the top
							Concept 2: Navigable Small Worlds
								If we put all people in a graph, relationships between any two people can be done with 3-4 links (3-4 people in between)
								Each vector is a node
								Edges: Distance is the edge (cosine difference)
									We calculate the cosine score during creation (there is upfront cost)
								With query, we can enter any node
									In 3-4 steps, we can get to the smallest one
									Traverse to the smallest cosine similarity among neighbors
									Repeat traversal
									We eventually read a node that has the most semantic similarity
									We pick the top k such nodes
									We check only a subset of nodes in total
							
							HNSW combines both concepts
								Layer 2 - a smaller percentage of the navigable small world
								Layer 1 - a percentage of the navigable small world
								Layer 0 - complete navigable small world
								
								We start at Layer 2 - stop at the smallest similar node
								Go to layer 1 - continue searching
								Go to layer 0 - continue searching

								Each layer can have a fixed number of nodes
								The actual nodes can be randomized
								
HNSW - How Search Works
	Top down
		Find entry point
		Follow proximity links
			Move gradually to the nearest vector along the available proximity links at that layer
		Drop to lower layer
		Repeat until bottom

There are other algorithms
	HNSW is the best now

What about sparse?
	Inverted index
		Same structure powering traditional search engines like Elastisearch
		How does it work?
			Maps each unique term to documents
			TF-IDF Score is used to rank the documents
			
			Inverted Index
				Key-value lookup (dictionary)
				Build a dictionary of all the words that were activated
					Tuples
					word1 -> ((document11, score), (document12, score), ...)
					word2 -> ((document21, score), (document22, score), ...)
					word3 -> ((document31, score), (document32, score), ...)
					...
					
				Search:
					Amazon Eco
						Amazon -> docs
						Eco -> docs
							Finds union or intersection
							Picks top k
							
		Benefits
			O(1) lookup
			No parsing all vectors
			
Forward index -convert to-> Inverted index

Trade-off: exact but limited to term matching
	If exact match fails, it does not return anything
		So we want it to be flexible and use semantic search
			Solution: Neural Sparse Embedding Models
				1. SPLADE
					1. Synonym match
						1. Solves vocabulary mismatch problem
		
Neural Sparse Embedding Models:
	We take a word of interest, we also put similar, high quality words with it
		Example: rainforsts -> forest, jungles, lands
	Implementation: SPLADE
		1. Learnable model
			1. Small model
		2. SPLADE - Learnable Sparse Embeddings (a performant model)
			1. It is a pre-trained models like BERT can identify connections between words and use that knowledge to enhance sparse vector embeddings - in two powerful ways
			2. Steps:
				1. Term Weighting
					1. Weighs the relevance of different terms intelligently.
				2. Term Explansion
					1. Includes alternative but relevant terms beyond those found in the original sequence - enriching the sparse vector with semantically related vocabulary the original text didn't explicitly contain
					
					Inverted Index is expanded with synonyms and documents are mapped
					
	It must be done online and offline
		1. Query is also expanded with SPLADE model
		
	Example:
		Query: "do any large monkeys come from the jungles of Indonesia?"
		
	Benefits
		Improved efficiency
		Reduced Computational Resources
		Enhanced Accuracy
		
Hybrid Search - Combining the best of lexical and semantic search.
	It blends two or more search methods into a single ranked list to improve relevance and recall
	
	Precision
		Example: 30 items in vector store
			8 items are relevant to query say
			Let us say we want items with > 0.8 and max 10 items
				Precision: Out of the items retrieved (6 say), how many are relevant to our query?
					80% say
	Recall
		Out of all the relevant ones to the query, how many did we retrieve
		
	Ideally, we want to maximize both
	
	If ranking algorithm is bad, we will choose poor results
	
	Lexical search - helps with precision
	Semantic search - helps with recall
	
	Both cannot be achieved at the same time
		We need to look for a stradeoff
		
	Steps:
		We query on both dense and sparse parts
		Scores are normalized for both the results (they have different scales)
		RRF - ranking
		Final ranked results
		
Why Hybrid Search Wins?
	Better releavance than either approach alone
	Handles both exact and fuzzy queries
	Reduces common failure modes
	Builds user trust
	
When to consider hybrid search?
	Code repository?
		Semantic understanding will not help
		Keyword search is better

	Mental health Forum
		Users search for advice or experiences related to their feelings
		Semantic Search
		
	Shopping App
		Hybrid search
		
Usecases:
	RAG pipelines
	Enterprise knowledge bases
	E-commerce
	Customer support search
	
Drawbacks of Hybrid Search
	Increased implementation complexity
		More components
		Multiple search algos
		Deep technical understanding is required
		
	Balancing Precision vs. Context
		Over-relying on one method diminishes the benefits of the other
			Getting result quality is not easy
			
RRF:
	How does it work?
		Run each search separately
		Fusion
			Two lists are merged
		Final ranked list
			Prioritizes and ranks based on relevance
			
	Reciprocal Rank Fusion (RRF)
		The key to hybrid search is the fusion step - how you mrege and rank the two result sets determines the quality of the final output
			RRF is a rank aggregation method that combines multiple ranked lists into a single, unified ranking - without needing relevance scores from each individual search method. It works by assigning each result a score based on its position (rank) in each list, then summing those scores to produce a final ranking
			
			Semantic
				1. D1
				2. D2
				3. D3
			Exact
				1. D3
				2. D1
				3. D4
				
			RRF: D1 - reciprodal of each position in the lists
				1 / (1 + 60) + 1 / (2 + 60) (60 added to avoid 1 / 1) 
				
			Elements that are in common and higher positions, they will get a highest score
			Elements that are not in one of them will go to the bottom
			
			Take top k
			
	Works for 60% of the usecases
			
	There are other ranking algorithms
		Using LLM
		Neural Networks (BERT say)
		...
		
Evaluation:
	We need a golden dataset
	We need to run tests
		Check relevance
		Check accuracy
		Check recall
		...

Observability
	Grafana
	...

Code:

Qdrant - vector database
	Open source
Viviate
Pinecone

FastEmbed
	Can run on CPU
		Lightweight Python library for generating fast, accurate, state-of-the-art embeddings
		
Langfuse - opersource

Qdrant
	Add a collection of documents to the engine
	Query the collection to retrieve the most relevant documents
	Implement hybrid search with sparse and dense vectors
	Apply RRF fusion and reranking
	
	Filter for metadata
	Scalable & production-ready
	Open-Source or Cloud (managed)
	
	Data structure
		Collections (like table)
		Points (data structure that contains vector + metadata)
			Unique ID
			One or more vectors (dense and/or sparse)
				Multiple versions of the vector
			An optional payload (metadata)
		Payload
			Key-value metadata attached to each point
			
FastEmbed
	Native SPLADE Support
		
	ONNX Runtime (50 MB), no PyTorch
		But slower than PyTorch
	Optimized for CPU
	Lightweight
	
Notebook:

SPLADE - TF-IDF + term expansion (using trained neural network)

!pip install -qU qdrant-client fastembed datasets transformers

	datasets - mock data
		Amazon ESCI (Exact, Substitute, Complement, Irrelevant)
			For each query, it tells which of the results are the above four types (m x n)
	transformers - manipulate embedding models
	
	By default Qdrant uses HNSW algorithm for indexes
	
We can use the tool in search bar in production