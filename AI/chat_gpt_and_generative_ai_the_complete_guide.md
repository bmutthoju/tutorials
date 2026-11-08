# ChatGTP & Generative AI - The Complete Guide #
## Section 1: Introduction ##
### Welcome to the Course! ###
### What Exactly is Generative AI (and ChatGPT)? ###
1. What is generative AI?
	1. Generative AI refers to a category of artificial intelligence models that are capable of constructing new content - such as text, images, audio, video, or code - that is similar to what a human might produce.
		1. AI Chatbots
		2. AI-powered Applications
			1. AI Agents & Automations
			2. RAG Systems
				1. Retrieve data dynamically and inject it into prompts
			3. Apps using AI
				1. Processing user input
		3. Large Language Models (LLMs)
			1. AI models
			2. Takes any text and produce text, images, etc.

### About the Course ###
1. Foundation
	1. Understanding how they work internally
	2. Using AI Chatbots & Models
	3. Understanding Generative AI & LLMs
		1. ChatGPT
		2. Grok
		3. Gemini
		4. ...
2. Efficient usage
	1. ChatGPT & Co Features
		1. Video & image generation
	2. Prompt Engineering
		1. Tips and tricks
	3. Examples & Use-cases
3. AI-powered Apps & Workflows
	1. RAG, CAG & Finetuning
		1. Workflows
	2. Agents & AUtomations
	3. Custom AI Applications

### Generative AI & Speed of Innovation ###
1. GPT-3 - AI Model
2. Capabilities
	1. Images
	2. Code execution
	3. Audio
	4. Web Search
	5. Deep Research
	6. Agents
3. It is highly dynamic and innovative

### It's not just ChatGPT! ###
1. Key Gen-AI Service Providers - Overview
	1. OpenAI ChatGPT
	2. Google Gemini 
	3. Microsoft Copilot
	4. xAI Grok
	5. Anthropic Claude
		1. The above use proprietary models
			1. We cannot run on our system
2. Open Models: Can be used on our hardware (moderate requirement)
	1. Gemma - Google
	2. DeepSeek
	3. Meta Llama

### It's not just About AI Chatbots! ###
1. There are multiple ways of using Gen-AI
	1. Services/Apps
		1. Service by third-party provider, used through their app/site
			1. AI Chatbots
				1. ChatGPT
				2. Gemini 
				3. Grok
			2. Product Features
				1. Photoshop
				2. Cursor
				3. Excel
	2. Integrated via APIs
		1. API by third-party provider, integrated into your app
			1. OpenAI & Co APIs
				1. Exposed via REST & SDKs
					1. To programmatically access their models
						1. Example: Process user inputs with generative AI
	3. Self-Hosted
		1. Models hosted on your (rented) hardware
			1. Open Models
				1. Llama
				2. DeepSeek
				3. ...
			2. Self-trained Models
				1. If you ahve the resources...

### Results May Differ & Free Model Access May be Limited ###
1. Notes
	1. We will not be able to reproduce the responses.
		1. AI models have a certain degree of "randomness"
		2. Underlying models will evolve and change
	2. Free usage is possible but often not enough
		1. No access to latest most capable features
			1. Plus plan is required

### Course Slides & Discord Community ###
1. [https://academind.com/community/](https://academind.com/community/)
2. [Slies](https://www.udemy.com/course/chatgpt-bard-bing-complete-guide-to-chatgpt-openai-apis/learn/lecture/37791138#overview)

## Section 2: Understanding ChatGPT & LLMs - A Look Behind the Scenes ##
### Module Introduction ###
1. Behind the scenes
2. How were they trained and work?
3. How is input processed?
4. Modern applications and models

### ChatGPT as an Application Shell for LLMs ###
1. `What happens under the hood when I ask you a question?`
	1. Model vs Application
		1. Prompt
		2. AI Application
			1. ChatGPT
		3. Potential Pre-processing Step
			1. Could filter, format or change your prompt
				1. Pre-processing
					1. Re-formatted
					2. Cleaned
		4. LLM
			1. Cleaned and reformatted input + chat history
				1. Chat history: Inputs + responses + follow-up questions
				2. History is also manged by ChatGPT
			2. Prompt Augmentation
				1. Contains visible and "invisible" (app-generated) messages to control AI model output
				2. Extra instructions may be injected into prompts & chat messages
					1. Example: "System prompt"
				3. System prompt: General information
					1. Config message
						1. Tone
						2. Block certain inputs
						3. ...
			3. Model produces output text
				1. Application can validate the output
2. Other ways to interact with models
	1. AI API
		1. It might be processing
		2. We can set system message
	2. Self-hosted models
		1. Almost no processing

### LLMs & Neural Networks ###
1. LLM - GPT 4o, etc.
	1. Large Language Models
		1. They deal with language
	2. They are trained as neural networks with billions of parameters
		1. Trained with transformer architecture (?)
		2. It models human brain
	3. A lot of training data is needed
		1. Data - from the internet
			1. Collected
			2. Cleaned
			3. Filtered
			4. ...
		2. Used to train the foudnation model
2. They understand relation between words and sentences

### LLMs are Token Prediction Machines! ###
1. Every word (token) is assigned a token id (number)
	1. ~ 200,000 ids
		1. They are not one-to-one mappings
	2. Case sensitive ('Hello' and 'hello' have different tokens)
2. Token ids are translated into vector embeddings (a long list of numbers)\
	1. To capture relations between certain tokens
	2. It is like storing tokens in a multi-dimensional space so that related words are stored together in the space
		1. 2-D space - water, cold; hot, fire
	3. Open AI has APIs to produce vector embeddings ourselves
	4. The vector embeddings are fed into the training process
		1. It may take multiple months to process the data2
		2. It may be very expensive
	5. The model can then predict the output based on the input
		1. If we feed a sequence of tokens, we get predictions for future tokens that follow the input sequence to overall produce a meaningful sequence
	6. Next tokens have probabilities
		1. Most likely one is chosen
3. LLMs are token prediction machines

### From Foundation to Assitant Models ###
1. Foundation model
	1. Foundation models are LLMs that can complete word / token sequences
		1. They don't necessarily made for great AI assistants or chatbots, though!
			1. If we ask a question, we might get more questions
				1. What's the meaning of life?
					1. That's the question. And also: WHy do we even exist? Will we ever find out?
				2. Fix?
					1. Fine-tuning phase
					
					```
					Foundation model - Finetuning Process -> Assistant Model
					```
					
						1. During finetuning, the foundation model is used as a base to train a finetuned assistant model
						2. Finetuning is performed by adding (human-generated) training data that simulate human <=> AI assistant interactions
							1. Made-up conversations were generated between humans and AI assistants for first LLMs
								1. It reflected the behavior we want from the model
								2. It has questions and conversations
									1. How it should play out between humans and assistant
						3. Assitant models are still LLMs that predict futer tokens
							1. But they are finetuned to generate tokesn in-line with the finetuning data
								1. Instead of questions, answers will be generated
						4. Further training is done by using already working LLMs as inputs without human generated training data
						5. Finetuning may cause the model to
							1. Be user-friendly
							2. Not answer certain questions
						6. Nicer tokens are predicted after finetuning

### Onwards to Reasoning Models ###
1. Reasoning models
	1. Think before providing the final answer
		1. They are not actually thinking
			1. They are predicting tokens
				1. They were finetuned to predict thinking tokens first, before providing the final response
	2. Example: Take an old LLM
		1. `Think step by step (and outline your thought process) before answering!`
			1. Chain-of-thought prompting
				1. The longer the sequence is, the better the token prediction gets (not always true)
					1. Example: Math problems
						1. Smaller problems - solution is correct because it is in the training set
						2. Larger and more complex problems - it might hallucinate
							1. Solution: Force them to describe the solution process in detail - increases likelihood of getting correct result
								1. Better solution: Make them write and execute code that performs the calculation
									1. Example:

									```
									Add the numbers: 4634543634543566435434 and 98459083405843054545 and give the result. Solve the problem using the following steps: 
									
									1. Generate a Python function that adds large numbers (numbers that exceed the long precision). 
									2. Call the Python function with the given inputs. 
									3. Show the result of running the function.
									```
									
	3. Reasoning models
		1. Reasoning mode is built into them
			1. They could be fed with questions + thought processes during fine-tuning
		2. Different approach is used
			1. Onwards to Reasoning Models
			
			```
			Finetuned Instruct Model - Reinforcement Learning -> Reasoning Model
											^
											|
										Evaluation Model
			```
			
				1. During the training phase, problems are given to the instruct model
				2. The responses / results are then evaluated & graded by a separate evaluation model
				3. That feedback is then used to adjust the LLM parameters until satisfying results are produced consistently
				4. Going through an initial "thinking process:" was "learned" during this training phase
		3. Over time, by solving thousands of problems, the model thinks (so to say)
			1. This trains the model to produce thought process tokens first before it generates the response

### Understanding the Context Window & Limitations ###
1. LLMs have Context Windows
	1. Chat History
		1. Your messages
			1. Your questions & follow-up messages
		2. Your attachments
			1. PDF documents, images, ...
		3. Model responses
			1. AI-generated responses
		4. Invisible messages
			1. System prompts, other app-controlled messages
	2. Chat history might get very long
		1. Chat GPT might parse and extract text from documents
		2. The more the text is, the more complex the relationship is
			1. It must be trained to do that
		3. It is called context window
			1. Old models had short context windows
		4. Newer models are more capable
			1. Google Gemini - millions of tokens
				1. May degrade for large input
					1. Example usage: Summarizing a scientific paper attached as a PDF
		5. Cheaper models have smaller context windows
			1. Use a model with a large context window

### Beware of Hallucinations! ###
1. LLM providers have set up guardrails making hallucinations less likely
	1. If we ask the model something it doesn't know, it may detect and give an automated response - Sorry I can't answer this
		1. Done during finetuning process
	2. Example: "What's my favorite color?"
2. Responses should be double checked for errors (hallucinations)

### The Problem with the Knowledge Cutoff Date ###
1. When training process starts, we cannot feed more data while it is going on
	1. If we ask something recent, it cannot know that
		1. It will likely end up hallucinating or give default response
2. Solutions:
	1. Prevent Hallucinations
		1. Finetune data to "detect" questions it's likely not able to answer
		2. Generate a generic response
			1. Sorry, I don't know that
	2. Solution 2: Expand knowledge
		1. Give AI application access to web search & fintetune to detect relevant questions
			1. Application can perform web search & include results in the context (in the chat history)
		2. Web search can also go wrong
			1. It depends on what the model searches and gets

### How LLMs Use Tools ###
1. Some of the AI chatbots use certain tools
	1. Search the web
	2. Write and execute code
		1. Solving math problems
	3. How AI Assistants Use Tools
		1. AI Assistant
			1. Chat History
				1. Includes description of available tools
				
				```
				You can use these tools:
				- Web Search: use by outputting WEB SEARCH: <search term>
				```
				
					1. Additional message inserted: Use the following tools if you think you need to
						1. It is part of the context window
						2. It is probably how the model was trained
				2. Example: `WEB SEARCH: who is the current US president?`
					1. It is handed over to chatGPT application
				3. Application executes prepared code to perform web search with requested search term (written by Open AI)
					1. The code gets the query
					2. Extracts content
				4. The extracted content is handed to the chat history (as invisible message)
					1. Chat sees that it asked for a web-search, it got the websearch results, and it can use the input and the results to give a meaningful response
						1. They are trained to communicate (output tokens) when they want to use a tool
				5. LLM doesn't use the tool, but the application uses the code
					1. LLMs are likely to ask for the tools for certain tasks based on system prompt etc, training, finetuning, etc.

### Module Summary ###
1. Limitations
2. Token prediction mechanism
3. Training and finetuning + application shell + tools provided by the shell
4. Hallucination
5. Knowledge cutoff

## Section 3: ChatGPT Basics ##
### Module Introduction ###
1. Topics: ChatGPT
	1. Basic & Advanced Features
		1. The AI chatbot with most features
	2. Make Sense of the Different Models
		1. Provided by Chat GPT
	3. Managing Prompts & Chat History
	4. ChatGPT Tools
		1. Built-in
		2. How to control tool usage

### ChatGPT - Free vs Paid ###
1. Free - certain features are not available
	1. No sign up required
	2. Less capable model (no model version shown)
2. Paid version
	1. Features
		1. Input box
		2. New chat

### A Tour Through The ChatGPT Interface ###
1. Features
	1. Input box
	2. Chat vs voice mode
	3. Upload files
		1. It's content and prompt will be sent to Chat GPT
			1. We can ask questions about the text
			2. We can ask summary
		2. We can upload multiple files
	4. Tools
		1. Search
		2. Deep research
		3. Image
		4. ...
	5. Model picker
		1. They are good at different tasks
	6. Sidebar
		1. Past chats
			1. Revisit or continue
		2. Sora
		3. Library of assets
			1. Images
		4. Explore GPTs
			1. Customized versions of Chat GPT
			2. We can make one
		5. Temporary chat
			1. It doesn't appear in history
			2. It won't be used for training
			3. It won't update chat-gpt's memory
				1. Memory: Contains main takeaways
					1. An understanding of me and my main problems, writing style, questions I have, etc, past conversations
			4. Every conversation has its own history
				1. Considered when we send a prompt to ChatGPT
					1. Takes important of every conversation are memorized
						1. It builds an overall picture of me and my topics
		6. Provile picture
			1. Plan
			2. Tasks
			3. Custom GPTs
			4. Settings

### Making Sense of Models & The Model Picker ###
1. Models change over time
	1. Free version:
		1. No choice
	2. Paid
		1. Few or more models
2. Why so many?
	1. Historic reasons & innovation in LLM space
	2. OpenAI has simplified the choices
	3. Some models are good at quick responses
		1. Which don't require deep thinking or knowledge
			1. Thinking: Better quality token generation
	4. Deep thinking
		1. o3, o4 - for complex problems
			1. Finetuned for chain of thought prompting
				1. They first describe steps to solve the problem
					1. A solution process
				2. They then follow the steps to solve the problem
			2. GPT-4o
				1. Quick
			3. o3 - Advanced reasoning
				1. Takes time to generate answers
				2. Complex problems
					1. Advanced coding problems
					2. Advanced math problems
					3. Riddles
					4. ...
				3. Example: `How much revenue do I need to make next year if I have variable costs of 20% of revenue and fixed costs of $500,000 per year?`
					1. Gives how it will solve it and then solves it
		2. 4o-mini - not reasoning model (basic questions)
			1. Even quicker than 4o
		3. 4.5 - new model (research preview)
			1. Better at writing and exploring ideas
				1. Email
				2. Article (short)
		4. o4-mini, o4-mini-high
			1. Think before they answer
				1. Bit quicker
			2. o4-min-high
				1. Quicker but better at coding
	5. GPT-4o - good for most tasks

### Writing Prompts - The Basics ###
1. Start with a base model
2. Prompt engineering
	1. To get most out of Chat GPT
3. **A prompt should describe the problem as concisely as possible and should contain all the necessary details that Chat GPT needs to know**
	1. Example:
	
```
Your are an AI expert.

Give me a short list of key features & example use-cases offered by ChatGPT and Large Language Models in general.

Avoid unnecessary explanations, just give me that list.
```
	
		1. Input prompt can be as big as an article
			1. Can copy and paste

```
You are in AI expert.

Here's an article I wrote:

<article>
 <paste-the-article>
</article>

Please summarize the above article. Summarize it as a list.
```

	1. HTML tags: Help LLMs understand the prompt a bit better
	2. Everything is sent to Chat GPT
4. If we send another prompt to ChatGPT, it would be the entire history along with the prompt sent to the LLM
	1. Initial prompt + answer + follow up message + ...
		1. Context window becomes fuller

### Editing Prompts & Regenerating Responses ###
1. Buttons
	1. Prompt
		1. Copy
		2. Edit
			1. Change the prompt
				1. New response will be generated
					1. We can switch between old and new prompts
						1. We can fork between the responses and work on each one of them
							1. Different threads (chat history) are created (branches)
			2. A tree of threads can be created
	2. Response
		1. Linked to each prompt
		2. Options:
			1. Change model and regenerate
		3. Response history is stored

### Using Speech as Input ###
1. New chat
	1. Voice buttons
		1. First button: Dictating text to Chat GPT
			1. Transcribed and inserted into the Chat input
		2. Second button: Voice mode
			1. Switch to a different way of interacting
				1. Setup voice
			2. Replies with AI generated voice
				1. Shows transcribed text
					1. We can't regenerate or edit

### Using Web Search in ChatGPT ###
1. Tools: Can be explicitly enable (now ChatGPT can automatically use them)
	1. Websearch: Search
		1. It may not know the answer without websearch - because of knowledge cutoff date
			1. `What's the latest AI model released by Google?`
				1. Model has been finetuned with similar demo questions that imply websearch - Chat GPT does it automatically

### Using The Deep Research Tool ###
1. Tool: Deep research
	1. Chat GPT will come up with good websearch terms
	2. Chat GPT will perform the websearch
	3. Chat GPT will aggregate the results
	4. Chat GPT will evaluate the results
	5. Chat GPT may perform more websearch
	6. ...
		1. It behaves like a research assistant
			1. Research
			2. Evaluate information
			3. Generate a response
2. Example:

```
Give me an overview of leading LLms available as of May 2025.
```

	1. It might have follow-up questions
	2. It generates a plan as to how it wants to perform the research
	3. It then does the research
		1. It can take a while (may be an hour too)
			1. We can open another chat to continue
		2. Activity
		3. Sources
3. LLM tells what tools it wants to execute and the application executes the code corresponding the tools

### Generating Images with ChatGPT ###
1. Select: `Create image`
	1. `A dog riding a bike`
2. We don't have to enable explicitly
	1. `Generate an image of a tree in a forest`

### Using Canvas Mode ###
1. Canvas tool
	1. `Write a short essay about rabbits`
		1. Special way of looking at your chat
			1. Long text responses (say) (outsourced into a new window)
	2. To make it easier to work on long text or code
		1. We can add annotations
			1. To edit individual parts
				1. Select the part and click ask chat gpt
					1. Ask what changes we want

### Having ChatGPT Execute Code & QR Code Generation Example ###
1. Code generation and execution tool
	1. `Give me the Python code for drawing a straight line in a line chart`
		1. For Python code, Chat GPT can execute it
			1. `Please execute the code and draw that chart`
				1. It runs it in a sandbox environment (runs on servers provided by Open AI)
					1. Cannot execute all python code
					2. Cannot execute non-python code (as of then)
						1. Supports other languages now
2. Generating QR codes
	1. `Write & execute Python code that generates a QR code that links to this page: https://maximilian-schwarzmueller.com/`
		1. Generates and executes Python code and outputs results
			1. Download link is shown

### Tool Availability ###
1. We may not have access to all tools
	1. Depends on the plan
2. All tools are not available for all models

### Understanding & Configuring Custom Instructions ###
1. Settings we can tweek
2. Customizing
	1. User profile image
		1. Customize ChatGPT (or Settings > Personalization)
			1. It applies to all future chats
				1. What should ChatGPT call you?
				2. What do you do?
					1. Context about you
						1. Helps get better results (if related to you or your profession)
				3. What traits should ChatGPT have?
					1. Examples:
					
					```
					Short response, adopt a skeptical, questioning approach.
					```
					
						1. Influences which kind of tokens it generates
				4. Anything else ChatGPT should know about you?
					1. Family
					2. Friends
					3. Net worth
					4. ...
				5. ChatGPT capabilities
					1. Check or uncheck
	2. Alternative
		1. Prompt engineering way to control per chat

### Key Settings, Memory & Privacy ###
1. Settings:
	1. General
		1. Theme 
		2. Always show code when using data analyst.
		3. Show follow up suggestions in chats
		4. Language - Auto-detect
		5. Archive
		6. Delete chats
		7. ...
	2. Notifications:
		1. Tasks
	3. Personalization
		1. Memory
			1. Enable or disable
				1. Enable: Chat GPT extracts key information for different chats and consider them for future conversations
					1. For long-term understanding of you and your topics on various conversations
			2. We can manage
			3. We can delete
				1. We don't have to repeat what was already discussed
	4. Speech
		1. Main language
		2. Voice
	5. Data controls
		1. Model improvement
			1. Sends conversations, prompts, and data to Open API for further training
	6. Export data
	7. Builder profile
		1. For custom GPTs
			1. It has public information that will be shared about me when I publish custom GPTs with the world
	8. Connected apps
		1. Apps we can use for file uploads
			1. Google drive
			2. Microsoft OneDrive
			3. ...
	9. Security
	10. Subscription
		1. Upgrade plan

### Working with ChatGPT Projects ###
1. Projects (feature)
	1. A place that groups chats, files, and custom instructions into one place
		1. If we have a bigger project
			1. Multiple chats to operate on same documents (pdfs, docs, ...)
	2. Example:
		1. Sales Analysis
			1. Same functions
		2. Files can be added only to this this chat or all chats 
	3. Project-specific instructions
		1. Will apply to all chats in this project
	4. We can see a history of chats

### Scheduling Tasks ###
1. Tasks (feature)
	1. To ask AI to complete recurring tasks
		1. Example: Weekly/monthly summary of AI news
		2. Example: Try your own
	2. We can start a chat and use a model that supports tasks
		1. o3 and o4 mini
	3. Example: `Generate a daily summary of recent AI news, especially news related to LLMs. I need that summary every day at 9 AM.`
		1. Chat GPT sets up a task
			1. Click for details (shows schedule)
		2. Notifications: Email
	4. Good for summaries and reports

### Exploring GPTs (custom ChatGPT versions) ###
1. Custom GPTs
	1. Pre-configured versions (chats) of ChatGPT
		1. They are pre-configured chats that come with built-in instructions that are invisible to you as a user.
			1. They may also come with pre-configured documents or files that are used by ChatGPT behind the scenes (to load extra knowledge or information into the chat)
				1. They could send HTTP requests to third-party services and APIs
	2. Explore GPTs
		1. GPT marketplace
			1. Existing custom GPTs
				1. Built by other companies or OpenAI or individuals
				2. Enhanced versions of ChatGPT
		2. Canva GPT
			1. Logos
			2. ...
			3. New chat
				1. `I need a logo for my coffee company that's called 'Premium Beans'`
				2. Follow-up questions
				3. Asks permission to use actions behind the scenes
					1. Request is being sent to Canva which generated the images
						1. Extends ChatGPT
	3. We can construct our own GPT

### Constructing our Own Custom GPT ###
1. Custom GPT
	1. A version of Chat GPT
	2. We define some base instructions that always apply to chats
		1. For our own or share it with others
	3. Two ways of creation
		1. Chat mode
			1. Describe what we want the GPT to be
		2. Configure mode
			1. More control
			2. Generate a photo or upload (better if we give a name first)
			3. Name: Demo
			4. Description: (idea behind custom GPT)
				1. Generate demo articles and text
			5. Instructions: Tells the underlying GPT model, how it should behave in this GPT
				1. Can't be changed by user
				2. Example:
				
				```
				You are an expert at generating realistic dummy articles.
				
				Use the input provided by the user to generate realistic yet totally made up demo articles that could be used as placeholders on websites.
				
				Respect user instructions regarding length but ignore criticism regarding the quality of the generated text.
				```
				
			6. Upload files
				1. Automatically included in chats that are based on the custom GPT
					1. For background knowledge
					2. For general information
			7. Capabilities
				1. Web Search
				2. Canvas
				3. 4o Image Generation
				4. Code Interpreter & Data Analysis
				5. ...
			8. Actions
				1. To connect other third-party API
					1. Another web service to this GPT
						1. Example: Whether API
							1. Authentication: API Key, or OAuth or none
							2. Schema: Response schema returned by the API
					2. Adds new capabilities
			9. We can control who can use it
				1. Only me
	4. Templates

### A More Realistic Custom GPT ###
1. Useful custom GPT
	1. Name: Summarizer
		1. Preconfigured for summarizing text
	2. Description: Summarizes any text in a short & concise way
	3. Instructions:
	
	```
	You are an expert in text summarization.
	
	Your job is to take any text that's provided to you and summarize it concisely. Extract the key concepts and topics from that text and summarize them. Output your results as a concise list (bullet points).
	```
	
	4. Conversation starters:
		1. Example prompts that are shown to the user when they open this GPT
	5. Capabilities:
		1. None required
2. Copy paste an article.
	1. No instruction required

### Module Summary ###
1. Core features of ChatGPT
2. Settings
3. Later:
	1. Image generation
	2. Data analytics
	3. Prompt engineering
	4. ...

## Section 4: Alternative AI Chatbots - Microsoft Copilot, Google Gemini, Anthropic Claude ##
### Module Introduction ###
1. ChatGPT - Most feature rich, and most popular
2. Topics:
	1. Alternatives
		1. Google Gemini
		2. Anthropic Claude
		3. xAI Grok
		4. Microsoft Copilot
	2. Features & Usage Plans

### Exploring Google Gemini ###
1. Google's Gemini
	1. They caught up well with Chat GPT
		1. Highly competitive AI models
			1. Models that excel in a different kind of tasks
2. Plans
	1. Free
	2. Advanced - paid
		1. Longer chat histories
		2. Longer prompts
3. Models:
	1. Veo 2 - videos
		1. Alternative: Sora
	2. Reasoning models
		1. Flash
		2. Pro
4. Features
	1. History of chats
	2. Settings
		1. info about me
			1. Keep responses short
			2. Name
			3. ...
5. Apps
	1. Google services
		1. Gmail
		2. YouTube
		3. Maps
			1. Routes
		4. ...
6. Chat
	1. Uplaod files
		1. Local
		2. Drive
		3. Code
			1. Fixing
			2. Generating
	2. Canvas
		1. Example: Write an article
			1. Simplifies tweeking or working with the text
7. Models:
	1. Flash - quick and easy responses
	2. Thinking models
	3. Deep research - Deep Research with 2.5 Pro
		1. Good for
			1. Making plans
			2. Doing behind the scenes web-search
			3. Evaluating results
			4. Generating report based on the research
8. Voice input
	1. Not interactive in web
	2. Richer voice mode in mobile app

### Gemini, Web Search & "Double Checking" ###
1. Gemini will always consider web-search results (no activation required)
	1. Google uses their index and database to improve results
		1. Sources are shown in results
	2. Google decides how much websearch will be done
	3. Sometimes, websearch sources are not added in the response
2. Double-check response feature
	1. Uses Google and searches Google to verify response
		1. Which parts are guaranteed to be correct and which sources prove that the sources are correct
			1. No hard guarantee though
	2. Gives confidence
3. Advantages:
	1. Double check
	2. Good models

### Using Gemini Indirectly via Search ###
1. Google.com
	1. `What's chatgpt`
		1. Overview - summary
		2. Cannot ask follow-up questions
		3. References web-search results
			1. Reduces hallucinations

### Exploring Anthropic Claude ###
1. Claude chatbot
	1. Free but account
	2. Paid plans
		1. More features
2. Features
	1. Chat history
	2. Settings
		1. Customize behavior
		2. Appearance
	3. Tweek writing style
		1. Style for response per prompt
		
	4. Upload files
	5. Reference code in GitHub
		1. Or use screenshots
	6. Use different models
		1. Sonnet - popular for code
			1. Generating and evaluating
				1. Use for code-related work

### Exploring Grok ###
1. Grok AI chatbot
	1. Integrated into X
2. Paid X account
	1. It can search the web
	2. Upload files
	3. Enter deep search mode
		1. Another more deep research
	4. Think mode
		1. One model can be switched to this or not
	5. Edit image
	6. Tools
		1. Web search
		2. ...
	7. X
		1. Explain this post button
		2. Use case: Research on news and posts on X

### Exploring Microsoft Copilot ###
1. Copilot
	1. Free or paid plan
		1. Paid version - full access to all the features and models
	2. New page
		1. Canvas mode
	3. Chat
		1. Files 
		2. Voice mode
			1. Interactive like Chat GPT
		3. Switch models
			1. Quick response
			2. Think Deeper
	4. Settings
		1. Theme
		2. Voice
		3. Language
	5. Integrated copilot in Microsoft products
		1. Word
		2. Excel
		3. ...
	6. Edge browser
		1. Coplit button
			1. To use insdie browser
				1. Has access to website we are currently on
					1. We can ask questions about the website
		2. Voice mode

## Section 5: Running LLMs Locally via LM Studio ##
### Module Introduction ###
1. Running LLMs locally
	1. ChatGPT & Co vs Self-hosted solutions
		1. ChatGPT & Co Disadvantages
		2. Exploring Open Models
			1. Google's Gemma models
			2. Meta's LLaMa models
			3. DeepSeek models
				1. To overcome disadvantages
		3. Understanding Quantization
			1. Depends on hardware
			2. LM Studio
				1. To run on own systems
2. Weights / parameters are "open"
	1. Not the code / algorithm that are open
	2. We can run them for free

### Why Would You Use Open LLMs? ###
1. Disadvantages with proprietary models
	1. Cost
		1. Most models are not accessible for free
			1. May need to pay multiple providers
				1. Some models are better at something
					1. Anthropic - code
					2. ChatGPT - research
		2. Having multiple subscriptions can add up
		3. API access is charged based on usage
			1. Pretty big, pretty quickly
	2. Availability
		1. No access without a (stable) internet connection
			1. Run on servers and data centers
			2. Services may go offline (e.g., due to demand)
		2. Usage limits may apply
	3. Privacy
		1. Especially for companies
		2. You're sharing your data with the model providers
			1. Even if you opt out, you cannot know with certainty
				1. Company policies may not allow sharing data
		3. Usage restrictions may apply
2. If you want / need to use the most powerful, versatile and knowledgable models, there's (almost) no way around ChatGPT & Co
	1. They always win in benchmark
3. Deepseek - Open source
	1. Requires ~ 1.4 TB of GPU memory
		1. Not practically possible
	2. Running / self-hosting large LLMs is very difficult & costly

### Finding & Understanding Open LLMs ###
1. Idea
	1. We can use the models for free and run locally
		1. We can train parameters
			1. No payment required
2. Alternatives
	1. Hugging Face
		1. To explore open models - for finding them
			1. Providers share the models here
	2. deepseek-r1
		1. Can explore
			1. Statistics
	3. gemma - open source
	4. Leaderboard
		1. Models can be great at certain benchmarks
		2. Displays both proprietary and open models
3. Onwards To Open-Source Models
	1. Most open-source models are smaller (i.e, less parameters) than the most capable proprietary models
		1. Smaller -> Less capable
			1. For many tasks, a small, locally running model may be equally good or even better than ChatGPT & Co
				1. Examples:
					1. Summarization tasks
					2. Data extraction tasks
					3. Local knowledge tasks
4. Super LLMs are hard to run locally

### Hardware Requirements & Quantization ###
1. Open-Source models
	1. Meta's Llama Models
	2. Google's Gemma Models
	3. DeepSeek's Models
2. Huggingface:
	1. Community has generated finetuned models
		1. Quantizations
			1. Helps run models locally
3. Understanding Quantization
	1. LLMs
		1. Consists of Billions of parameters
			1. They are numbers derived during pre-training and finetuning stages
				1. The numbers control the likely next tokens when we provide an input
				2. Parameter - Float16 / Float32 numbers (fractional numbers)
					1. They can be stored with certain precision
						1. Higher numbers need more space (vRAM)
							1. All the numbers need to be loaded into memory (for GPU) (not CPU)
							2. 1 billion parameters - small model
								1. Deepseek - 685 Billion parameters
								2. 1 Billion - 2 GB vRAM is required
								3. 27 Billion - 54 GB vRAM
		2. Quantization
			1. Solution: To reduce the space that's needed models into memory
				1. To run locally or remotely
			2. Parameter values are simplified with a mathematical process that reduces their precision
				1. Slightly underperforms but a lot of space is saved
					1. To int4 / int8
			3. Example: With 4 bit quantization, a 1bn model only needs 0.5 GB of (V)RAM (1/4th the original size)
			4. Modern techniques are good at keeping performance stable and deliver gains
			5. Based on base model
		3. Gemma is quantized and it can be run locally

### Software Options For Running LLMs Locally & Installing LM Studio ###
1. Running LLMs locally
	1. Huggingface
		1. Use this model
			1. Transformers - library (programmatic way)
			2. Local apps
				1. LM Studio
				2. Ollama
					1. Good option
2. There are different solutions that make running open-source LLMs locally a breeze
	1. LM Studio
		1, Most user-friendly
	2. Ollama
	3. llama.cpp
		1. Bit tricky
			1. Docker is used
3. We can use open-source models programmatically via Ollama & Co APIs OR via Huggingface transformers library
4. LM Studio
	1. Desktop application
	2. Model catalog
		1. Gemma models
		2. DeepSeek R1 based models
	3. Download
	4. Install
	5. Open
		1. Switch modes (to change tools)
			1. User
				1. Select a model to load
					1. Settings: Model search:
						1. Install models
							1. We can select quantized models of different precision
			2. Power user
			3. Developer
				1. Inspect which requests I can send to an API
		2. Resources
			1. RAM, CPU (bottom right)
				1. We can partially loaded into RAM and vRAM

### Example Use-Cases: Text Summarization & Data Analysis ###
1. Gemma model - 128k tokens into the context
	1. 8k tokens output
	2. We can include significant amount of knowledge or data
	3. It can generate code (good)
	4. Good at extracting information
	5. Upload files
		1. PDF
			1. Allowed
			2. Turn off Wifi
			3. Summarize the article

### Hosting Open Models ###
1. Self-hosting LLMs
	1. You can also run (host) open-source models on owned / rented servers
		1. On-premise / VPS (rent it)
			1. You own / rent & configure the server
			2. You manage the software and install Ollama / LM Studio etc.
			3. Expose an API
				1. To other servers
				2. ...
					1. We need network
			4. You configure the network
				1. For hosting
					1. Need some technical expertise
		2. Managed Service
			1. Amazon Bedrock
				1. To run open source models or provided by Amazon
			2. You select models & features -> No setup required
			3. No technical expertise required
			4. You pay for the usage
				1. Could be more expensive compared to servers

## Section 6: Prompt Engineering ##
### Module Introduction ###
1. Prompt Engineering
	1. Ensuring Good results (relevant to everyone)
		1. What & why?
		2. Understanding key techniques
		3. Best practices & recommendations

### Use Prompt Templates ###
1. Use prompt templates
	1. An efficient way of quickly getting good results
		1. [https://promptsdb.ai](https://promptsdb.ai/)
			1. Text analysis
			2. Generation
			3. Image generation
			4. ...

### Prompt Engineering: What & WHy? ###
1. What is prompt engineering?
	1. What is a prompt?
		1. Whatever we enter into Chat input box
			1. Question or request
		2. Whatever we send to an AI model
		3. It is the message we are sending to AI
	2. It is the skill of crafting great prompts
		1. Good prompts -> Good results
			1. Example: More context that is relevant
		2. Great prompts -> Great results
		3. Bad prompts -> Bad results

### Prompt Engineering & ChatGPT Custom ###
1. Chat GPT
	1. Customize ChatGPT
		1. What traits should ChatGPT have?
			1. Behavioral traits to use and show
				1. `Be brief in all your responses, unless told otherwise`
		2. General info about me
		3. General instructions
			1. `I'm not interested in politics at all - definitely avoid it unless explicitly asked for it.`

### Prompt Engineering Goals ###
1. Main Prompt Engineering Goals
	1. Control Output Content: You want the LLM to generate content that you can use with as little modifications as possible. Of course, you also want a response that's correct, contains no hallucinations and meets any other requirements you might have
		1. A LinkedIn Post
		2. Blog post
		3. Code snippet
		4. ...
			1. We can control the following:
				1. How long should it be?
				2. How detailed?
				3. Which tone should be used?
	2. Control Output Format: For some (but not all) use-cases, you also might care about hte format you might want a response formatted as JSON or markdown or maybe you need text that's structured as a list of bullet points
		1. Plain text - email 
			1. Inherent structure
		2. Markdown
		3. JSON
		4. ...
2. What defines a good prompt?

### The Core Elements of a Good Prompt ###
1. What defines a good prompt?
	1. Instruction
		1. Your task / Goal / Question
	2. + Helpful context (prompt engineering)
		1. Give a role
			1. Example: `You are an expert LinkedIn marketer`
		2. Relevant information
			1. Any extra info that improves the chances of AI generating a helpful response
		3. Examples
		4. Constraints
			1. Example: `Construct a short post about hte rise of generative AI` (not long post)
	3. Irrelevant information must be avoided
	4. Complex (multi-task) prompts should be avoided
		1. Split them into multiple prompts

### It's a Chat! Use it! ###
1. ChatGPT output is a starting point
	1. Fine-tune & adjust as needed
		1. Using the starting point
			1. Adjust the output
2. Refine results over time
	1. It's a chat!
		1. Tell the AI which parts need adjustments
			1. Example: `Remove the Emojis and all hashtags`

### Time to Practice: Your Tasks ###


### Time to Practice: Solution (1/3) ###
### Time to Practice: Solution (2/3) ###
### Time to Practice: Solution (3/3) ###
### Onwards to Specific Prompt Engineering ###
### Zero-,One- & Few-Shot Prompting ###
### Finetuning vs Few-Slot Prompting ###
### Few-Shot Prompting to Control Output ###
### Using Delimiters to Structure Prompts ###
### Contextual Prompting & Including Relevant Data + Information ###
### Chain-of-Thought Prompting ###
### Reasoning Models & Chain-of-Thought Prompting ###
### Split Complex Problems Into Simpler Ones ###
### Ask-Before-Answer Prompting ###
### Persona Prompting ###
### Self-Reflective Prompting ###
### Negative Prompting ###
### Controlling The Output Format ###
### Let the AI Help You with Prompting! ###
### Using Provider-specific Prompt Guides ###
### Module Summary ###
### LEGACY LECTURES BELOW ###
### Time to Practice II: Your Tasks ###
### Time to Practice II: Solution (1/3) ###
### Time to Practice II: Solution (2/3) ###
### Time to Practice II: Solution (3/3) ###
### Contextual Prompting ###
### Emotional Prompting ###
### Laddering Prompting ###
### Using ChatGPT for Prompting ###
### Find out Which Information is Missing ###
### Self-evaluative Prompting ###
### ChatGPT-powered Problem Splitting ###
### Let ChatGPT Share its Thought Process (Chain of Thought Prompting) ###
### Reversing Roles ###
### More Prompts & Finding Prompt Inspirations ###
### Super Prompts Like CAN & DAN ###
### Module Summary ###

## Section 7: Generating & Analyzing Images with ChatGPT ##
### Module Introduction ###
### AI Image Generation - An Overview ###
### Generating Images with AI (ChatGPT) ###
### It's Not Just ChatGPT - Exploring Alternatives ###
### A First Glimpse At Midjourney ###
### Integrated AI Generation (Example: Photoshop) ###
### Context Matters! ###
### Prompt Engineering Matters! ###
### Is Also Has Limitations & Problems ###
### Constructing Illustrations ###
### Refining Images via Chat Messages ###
### Controlling Aspect Ratio ###
### Adding Text To Images ###
### Including Images In Prompts ###
### Generating Images Based On Other Images ###
### Demo: Constructing a Website Based on an Uploaded Image ###
### Generating Videos with AI & Sora ###
### Alternative: AI Video Generation via Veo 2 & Limitations ###

## Section 8: Using ChatGPT For Utility Tasks ##
### Module Introduction ###
### Researching Information with ChatGPT ###
### Summarizing Text & Information ###
### Translations & Tone Adjustments ###
### Using ChatGPT for Proofreading ###
### Writing Utility Scripts with ChatGPT ###

## Section 9: Research & Data Analysis with ChatGPT & Generative AI ##
### Module Introduction ###
### Performing Web Search with AI ###
### Performing Data Analysis with AI ###
### Working with Charts ###
### Analyzing Unstructured Data ###
### Data Extraction & Checking for Hallucinations ###
### Exploring Canvas Mode ###
### LEGACY LECTURES BELOW ###
### What is Advanced Data Analysis & One Word About Restrictions ###
### How to Use the Advanced Data Analysis Feature ###
### Uploading Files & Restrictions Workaround ###
### Downloading Files ###
### Prompt Engineering & Result Limitation ###
### Forcing ChatGPT to Use Advabced Data Analysis ###
### Disabling the Code Editor for Specific Parts of the Task ###
### Extracting Data from Files ###
### Dummy Data Generation ###
### Data Analytics Intro ###
### Data Preparation with Andvanced Data Analysis Support ###
### Analyzing & Visualizing Data ###
### Analyzing & Transforming Images ###
### Editing & Constructing Images ###
### Using the Advanced Data Analysis for Optical Character Recognition (OCR) ###

## Using ChatGPT for Content Creation ##
### Module Introduction ###
### How Amazing Articles Can be Generated with ChatGPT ###
### Constructing Articles - Step-by-Step ###
### Using a Single Prompt to Construct Articles ###
### Finding Creative Titles & Summarizing Text in Seconds ###
### Brainstorming Content: Articles, Blog Posts, Deep Dives & More ###
### Writing Professional (YouTube) Video Scripts with ChatGPT ###
### What is Copywriting? ###
### Using ChatGPT as Copywriter ###
### Boosting Your Social Media Accounts with ChatGPT ###
### Preparing Interviews ###
### Prevolutionizing Job-Related Writing ###
### Writing Outstanding CVs & Cover Letters for Your Next Application ###
### Constructing Job Offers & Contracts ###
### Letting ChatGPT Find the Right Words in Emails ###
### Constructing Sample Data with ChatGPT (e.g. JSON & CSV) ###

## Midjourney - An Introduction ##
### Module Introduction ###
### There Also is a Web Version Available ###
### Using Midjourney in Discord ###
### Constructing our First Images ###
### Understanding Variations, Upscaling & Regenerations ###
### Editing Upscaled Images ###
### Exploring the Settings ###
### Your Prompts & Images are Public! ###
### Getting Inspired by Community Prompts ###
### Deleting Images From Midjourney ###
### Uploading & Describing Images ###
### Blending Images ###
### How to Continue ###

## Deep Dive: Writing Efficient Prompts with Midjourney ##
### Module Introduction ###
### Different Version - Different Image ###
### Constructing a Prompting Template ###
### Defining the Details ###
### The Medium: From Photo to Comic to 3D-Animations ###
### Defining the Main Content of the Image ###
### Changing the Perspective ###
### Selecting an Image Style ###
### Working with the Blackground & the Atmosphere ###
### Constructing Photorealistic Food Images with Three Words ###
### Reconstructing Art & Artist Styles ###
### Recreating Movie Styles ###
### Understanding Parameters ###
### Parameters in Practice ###
### Constructing Custom Options / Custom Parameters with / prefer ###
### Constructing Reusable Prompt Templates with Custom Parameters ###
### Constructing Icons ###
### The Remix Mode ###

## Hands-on: ChatGPT & Midjourney for Content Creation ##
### Module Introduction ###
### Generating A List of Keywords (with Ask-Before-Answering) ###
### Constructing an Outline (Emotional Prompting + Laddering Technique) ###
### Constructing the Post (with Ask-Before-Answreing) ###
### Identifying Improvement Potential with ChatGPT ###
### Generating Images with ChatGPT ###
### Generating Images with Help of ChatGPT ###
### Generating a Thumbnail with Midjourney ###
### SEO with ChatGPT ###
### Adding Links to the Article ###
### Formatting as Markdown & Facing ChatGPT Limitations / Problems ###
### Generating a YouTube Script ###
### Constructing a Newletter Email ###
### Generating a Tweet & Module Summary ###

## Exploring Other AI Tools to Construct Images & Speeches ##
### Module Introduction ###
### Getting Started with Dall-E 2/3 ###
### Editing Images with Inpainting ###
### Expanding Images with Outpainting ###
### Editing Uploaded Images ###
### Introducing ElevenLabs' Generative Voice AI ###
### Reconstructing Your Voice with Generative AI ###

## Using ChatGPT for Programming & Development ##
### Module Introduction ###
### Using ChatGPT with & Without Programming Experience ###
### Using ChatGPT for Building Entire Applictions ###
### Using Generated Code & Letting ChatGPT Help You ###
### Iterative Development Test & Improve ###