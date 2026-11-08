1. Observability
	1. Bigquery
	2. Langsmith
		1. Platform
	3. Dynatrace
2. AI-Engineer
	1. Be full-stack
		1. Front-end
		2. Back-end
	2. Language: Python, JavaScript, TypeScript
	3. LLM APIs - how to connect to APIs
		1. Anthropic
		2. OpenAI
		3. Gemini
		4. Ollama
	4. Frameworks
		1. Langchain
		2. Google ADK
		3. Langgraph
		4. CrewAI
		5. Autogen
		6. ...
	5. Vector DBs
		1. Pinecone
		2. Chroma
		3. Weaviate
		4. PGVector
		5. ...
	6. Web Frameworks
		1. Fast API
		2. Streamlet
		3. Chainlet
		4. React
	7. Cloud
		1. AWS
			1. Bedrock
		2. GCP
			1. Agent Planner / Vertex AI
		3. Azure
			1. Data Foundry
	8. DevOps / MLOps
		1. Docker
		2. Langsmith
		3. Github actions
		4. IAC
			1. Terraform
		5. Artifactory
	9. Evaluation
		1. Ragas
		2. DeepEval
		3. Langsmith
		4. Autorater (LLM & Judge)
	10. Security - Guardrail
		1. Model Armor
		2. Prisma Airs
		
Assignment: The Autonomus IT Support Agent
	1. Agent decides whether to act or escalate
	2. Flow:
		1. User reports an issue
		2. Agent sends issue details + tool definition to LLM
		3. LLM decides which tool to call
		4. Agent calls Python function
		5. Agent sends back result to LLM
		6. LLM either calls another tool or responds
	3. All responses are stored for future calls
	
Pandas:
It is like excel
It is for structured data
Each column is a series
Table: Data frame

Formats:
csv
url (pointing to csv)

```
df = pd.read_csv(<file-name>)
```

It can be formatted as a dictionary and converted to a data frame

```
import pandas as pd
```

Cleaning
	1. Filtering
	2. Filling
	3. ...

Integrate with other libraries
	1. Matplotlib
	2. ...
	
Filtering
	1. Duplicate removal
	2. Some criteria

Filtering based on `loc` and `iloc` methods (location, integer location)

loc:

df['age']

df.loc['age', 'education']
df.iloc[0:3, [1, 2]]

Single or multiple columns

Conditions:

>, <, >=, <=, ==, !=, &, |

age > 30 & subject == "c-s"

df.drop() - to drop an index

```
import pandas as pd
```

```
s1 = pd.series([11, 21, 31, 53, 93, 23])

data = {'city': [], ...}
df = pd.df(data);

df = pd.read_csv(csv_url)

df.head(10)
df['Age']
df[['Age', 'Name', 'Survived']]

df.info()
df.describe() # For numerical fields

df['Pclass'].value_counts()
df[df['Pclass'] == 1] # Fetches true values

df[df['Pclass'] == 1 & ..]

df.groupby('Pclass').agg({
  'Age': 'mean',
  'Fare': 'median'
})
```

mode: Highest occurance

```
df.groupby('Pclass').agg({
  'Age': ['mean', 'median', 'count', 'sum'],
  'Fare': 'median'
})
```

```
custoemr.loc[0 : 1, ['Age', 'Education']]
customer.iloc[[0, 2], [0, 1, 3]]
```

```
filter = customer['Name'].str.contains(r'[m]', regex = True)
customer_filtered = customer[filter]
```

```
df.sort_values('Age')
df.sort_values('Age', ascedning = False)
```

```
df['Age'].dropna()

df['Age'].isna().sum()

df['Age'].filna(69.23)
```

```
df.sort_values[by = ['Score', 'Age'], ascending = [False, True])
```