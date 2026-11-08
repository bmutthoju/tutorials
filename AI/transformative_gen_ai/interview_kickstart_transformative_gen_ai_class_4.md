# RAG (Retrieval-Augmented Generation) - Interview & Project Notes

## What is RAG?

**RAG (Retrieval-Augmented Generation)** is an AI architecture that retrieves relevant information from external knowledge sources and provides it to an LLM before generating a response.

**Flow:**

```
User Query
      │
      ▼
Query Embedding
      │
      ▼
Vector Database (Top-K Retrieval)
      │
      ▼
Relevant Context
      │
      ▼
Prompt Augmentation
      │
      ▼
LLM
      │
      ▼
Final Answer
```

Example:

* **Walmart Sparky** uses RAG to retrieve product catalog information before generating responses.

---

# Why RAG?

LLMs have several limitations:

### 1. Knowledge Cutoff

Models are trained only until a certain date.

Example:

* GPT-3.5 Turbo
* GPT-4
* Gemini

They do **not** know information published after training.

---

### 2. Private Data

LLMs cannot access:

* Company documentation
* Confluence
* Internal APIs
* Product catalogs
* PDFs
* CRM data

unless provided during inference.

---

### 3. Grounding & Business Control

Organizations want responses based on **their own knowledge**, not generic internet knowledge.

Example:

Customer:

> Recommend a laptop.

Business wants:

* Their inventory
* Their pricing
* Their promotions

not competitors' products.

This is called **grounding**.

---

# RAG Pipeline

## Step 1 — Build the Knowledge Base

Possible sources:

* PDFs
* HTML
* Markdown
* Confluence
* SharePoint
* Product catalogs
* Databases
* APIs

---

## Step 2 — Chunk Documents

Large documents are split into smaller pieces.

Each chunk should be:

* self-contained
* semantically meaningful
* small enough for retrieval

Typical sizes:

* 300–1000 tokens
* 10–20% overlap

---

## Step 3 — Generate Embeddings

An **embedding model** converts text into a dense numerical vector.

Example models:

* OpenAI `text-embedding-3-small`
* OpenAI `text-embedding-3-large`
* Gemini Embedding
* BGE
* E5

Example:

```
"Car insurance"
↓

[0.24, -0.92, 0.17, ...]
```

The vector captures **semantic meaning**, not keywords.

---

## Step 4 — Store in a Vector Database

Each chunk is stored as:

```
ID
Chunk Text
Embedding Vector
Metadata
```

Metadata examples:

* filename
* page number
* author
* section
* category
* timestamp

---

## Step 5 — Query Time

When the user asks a question:

```
Question
      │
Embedding Model
      │
Query Vector
      │
Vector Search
      │
Top-K Chunks
```

These chunks become the context for the LLM.

---

## Step 6 — Prompt Augmentation

Example prompt:

```text
System:
Answer only using the provided context.

Question:
<user question>

Context:
<retrieved chunks>
```

The retrieved context reduces hallucinations and allows smaller, cheaper models to perform well.

---

# Why Embeddings?

Traditional SQL or keyword search requires exact matches.

Example:

```
vehicle insurance
```

vs.

```
car insurance
```

Keyword search may fail.

Embedding search succeeds because both phrases have similar semantic vectors.

---

# Similarity Metrics

## 1. Cosine Similarity (Most Common)

Measures the angle between vectors.

```
cos(0°)   = 1   (identical)
cos(90°)  = 0   (unrelated)
cos(180°) = -1  (opposite)
```

Advantages:

* Ignores vector magnitude
* Fast
* Excellent for semantic search

---

## 2. Euclidean Distance

Straight-line distance.

Accurate but computationally more expensive in high-dimensional spaces.

---

## 3. Manhattan Distance

```
|x1-x2| + |y1-y2|
```

Simple but less suitable for semantic similarity.

---

# Vector Databases

Purpose:

Efficient nearest-neighbor search over millions or billions of vectors.

Popular databases:

* Pinecone
* Milvus
* Weaviate
* Qdrant
* Chroma
* FAISS (library)
* Elasticsearch (vector support)
* Vespa

Typical record:

```
ID
Chunk
Vector
Metadata
```

---

# Approximate Nearest Neighbor (ANN)

Exact vector search is expensive.

Vector databases use ANN algorithms.

Popular algorithms:

* HNSW (Hierarchical Navigable Small World)
* IVF
* PQ

These return very accurate results with much lower latency.

---

# Chunking Techniques

## 1. Fixed-Size Chunking

Example:

```
500 tokens
```

Pros

* Simple
* Fast

Cons

* May split sentences
* Loses semantic continuity

Use chunk overlap (10–20%).

---

## 2. Recursive Chunking (Most Popular)

Split only when necessary:

```
Document
    ↓
Sections
    ↓
Paragraphs
    ↓
Sentences
    ↓
Words
```

Advantages:

* Fast
* Cheap
* Preserves structure

Widely used in production.

---

## 3. Semantic Chunking

Goal:

Each chunk discusses a single topic.

Method:

* Embed sentences
* Merge semantically similar sentences

Pros:

* Better retrieval quality

Cons:

* Slower
* Requires threshold tuning
* Higher embedding cost

---

## 4. Structure-Based Chunking

Uses document hierarchy.

Examples:

* HTML
* Markdown
* Confluence
* Wikipedia

Preserves parent-child relationships.

Best for well-structured documents.

---

## 5. LLM-Based Chunking

Ask an LLM to split the document.

Highest quality but:

* Slow
* Expensive

Usually reserved for high-value datasets.

---

# Chunking Evaluation

Evaluate:

* Chunking strategy
* Chunk size
* Chunk overlap
* Top-K value
* Embedding model
* Retrieval quality

---

# Top-K Retrieval

The vector database returns the **K** most relevant chunks.

Typical values:

```
K = 3–10
```

Too small:

* Missing information

Too large:

* Adds irrelevant context
* Increases token cost

---

# Maximum Marginal Relevance (MMR)

Problem:

Top results may be nearly identical.

MMR balances:

* Relevance
* Diversity

It penalizes duplicate or highly similar chunks, improving context quality.

---

# Metadata Filtering

Retrieve documents using metadata before vector search.

Examples:

* customer = Walmart
* language = English
* category = Insurance
* year = 2025

This improves retrieval precision.

---

# Embedding Models

The embedding model determines:

* Vector dimension
* Semantic quality
* Cost
* Latency

General rule:

Higher-dimensional embeddings often improve retrieval quality but require more storage and computation.

---

# Temperature

Controls randomness during text generation.

```
Temperature = 0
```

* Deterministic
* Best for RAG

Higher temperature:

* More creative
* Less predictable

---

# Context Window

Modern LLMs support very large context windows (up to ~1M tokens in some models).

However:

* Larger context increases latency and cost.
* Retrieval quality often degrades if too much irrelevant context is included.

Retrieving only the most relevant chunks generally yields better results than sending entire documents.

---

# Cost Considerations

Vector database creation:

* One-time indexing cost

Embedding generation:

* Cheap compared to LLM inference

Inference:

* RAG reduces prompt size
* Enables use of smaller, faster, and less expensive models

---

# LlamaIndex

A framework for building RAG applications.

### Index Types

### 1. Vector Index

Default for semantic retrieval.

---

### 2. Summary Index

Stores summaries of documents.

Useful for:

* Long reports
* High-level document understanding

---

### 3. Tree Index

Creates hierarchical summaries.

Suitable only when documents naturally have a tree structure.

Can underperform on flat documents.

---

### 4. Keyword Index

LLM extracts keywords.

Queries are matched using exact keywords.

Best for:

* IDs
* Aadhaar numbers
* Order numbers
* Product SKUs

---

### 5. Hybrid Retrieval

Combines:

```
Keyword Search
+
Vector Search
```

Results are merged and re-ranked (e.g., Reciprocal Rank Fusion).

Best of both worlds:

* Exact matching
* Semantic matching

---

# Vespa

An open-source search engine supporting:

* Hybrid retrieval
* Vector search
* Keyword search
* Ranking pipelines

Also consider:

* Elasticsearch (vector support)
* OpenSearch

---

# LangChain & LangGraph

Frameworks for building LLM workflows.

Typical routing architecture:

```
User Query
      │
Intent Classification
      │
      ├── Product RAG
      ├── HR RAG
      ├── Finance RAG
      └── Legal RAG
```

Each domain can use its own:

* Knowledge base
* Embedding model
* Vector database
* Retrieval strategy

This pattern is known as **RAG routing** or **multi-agent RAG**.

---

# Supporting Tools

| Tool              | Purpose                                             |
| ----------------- | --------------------------------------------------- |
| LangChain         | LLM orchestration                                   |
| LlamaIndex        | RAG framework                                       |
| BeautifulSoup     | HTML parsing                                        |
| Unstructured.io   | Convert unstructured documents into structured text |
| OpenTelemetry     | Observability and tracing                           |
| NumPy `argsort()` | Returns indices that would sort an array            |

---

# PandasAI

Allows natural language interaction with Pandas DataFrames.

Flow:

```
Question
     ↓
LLM
     ↓
Generate Pandas Code
     ↓
Execute
     ↓
Return Result
```

Example:

> "Which customer spent the most last month?"

The LLM generates the appropriate Pandas code, executes it, and returns the answer.

---

# Interview Quick Revision

### Why use RAG?

* Access latest information
* Use private enterprise data
* Reduce hallucinations
* Ground responses
* Lower inference cost

### Best Chunking Strategy

* Recursive chunking (general-purpose)
* Structure-based chunking (structured documents)
* Semantic chunking (higher accuracy, slower)

### Most Common Similarity Metric

* Cosine similarity

### Important Evaluation Metrics

* Retrieval precision
* Recall
* Answer faithfulness
* Context relevance
* Latency
* Cost

### Common Production Stack

```
Documents
     ↓
Chunking
     ↓
Embedding Model
     ↓
Vector Database
     ↓
Retriever
     ↓
Prompt Augmentation
     ↓
LLM
     ↓
Final Answer
```

### Common Interview Questions

* What problem does RAG solve?
* Why use embeddings instead of keyword search?
* Why is cosine similarity preferred?
* What is chunk overlap and why is it important?
* What is Top-K retrieval?
* What is hybrid search?
* What is MMR (Maximum Marginal Relevance)?
* How do you evaluate a RAG system?
* When should you use semantic vs. recursive chunking?
* How would you reduce hallucinations in a production RAG application?
