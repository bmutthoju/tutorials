# OpenTelemetry for Observability: The Complete Course
## Section 1: Introduction
### Welcome to the Course!
1. Instrumentation for sync and async services
	1. Metrics
	2. Logs
	3. Traces
2. Standards
	1. OpenTelemetry
3. Lab
4. AI Agents for instrumentation
5. Topics:
	1. Objservability Foundations
		1. SLIs, SLOs, SLAs
		2. Four golden signals
	2. Deploying the Observability Stack
		1. Prometheus
		2. Loki
		3. Tempo
		4. Grafana
		5. Sample application
	3. OpenTelemetry Concepts
		1. Vendor-neutral with OTel APIs, SDKs, Collector
		2. Convensions
	4. Instrumenting Single Services
		1. OTel Collector
		2. Metrics, traces, and logs for Frontend
		3. Log-trace correlation in Grafana
		4. Environment-driven config
	5. Instrumenting Distributed Systems
		1. Signal coverage for Pyton
		2. Nodejs
		3. Distributed context propagation
		4. Custom metrics, spans, Redis exporter
	6. Deploying to Kubernetes
		1. K8s manifests
		2. Configuration management
		3. End-to-end

### Expectations Alignment
1. What this course is about
	1. OpenTelemetry
		1. Covering the most important aspects of working with OpenTelemetry and instrumenting applications in real-world projects
	2. Gaining hands-on experience
	3. Going beyond the basics
		1. Manual instrumentation
		2. Context propagation
		3. Distributed tracing
		4. ...
2. Requirements and prerequisites
	1. Programming: JS, Python, Java, ...
	2. Docker & k8s
	3. Terminal / command line

### Let's Stay Connected!
1. [https://www.linkedin.com/in/lauromueller/](https://www.linkedin.com/in/lauromueller/)
2. DevOps, Cloud, and AI Newsletter: [https://blog.lauromueller.com/](https://blog.lauromueller.com/)

### Course Resources
1. [opentelemetry-slides.pdf](https://att-c.udemycdn.com/2026-03-23_14-35-13-2c43dc3d7e4137d0335b1b3917b86dbd/original.pdf?response-content-disposition=attachment%3B+filename%3Dopentelemetry-slides.pdf&Expires=1790114092&Signature=8odU2jZbOiAs9Dmbv81NVziSvw9yOyfYSwsW86T6P5GBNvvzxgv13PHO8PudMSHtAAIMb8YJu6mv~5QhhGHuDp-F8ihlHyuNbt-E~47QrNPGBm~MN-FJRsRIKTUZQyRs~RnEPfdu72z-xuUhQiV8cAV5twHSpnsWAZ8kqi7eEkwq6tnHpcHh7D0h9cVOxkz2gKu4RSbauMbOcg9oQlRoQ2ZW8pTea4F5xggz2EO5L3t9l~mRKSD75lA~i5x3ZfWOkPTQD1R4FvKKU97sfrg7NZuFOHxPkzyOwgCGSCPcom3vmw9nZZUelpxhubQEyOjqY5YwErPYNqSnpCvOTthvlA__&Key-Pair-Id=K3MG148K9RIRF4)
2. [opentelemetry-course-main.zip](https://att-c.udemycdn.com/2026-03-23_14-35-22-c9c375a19b59aec3be3258ef0c451c8f/original.zip?response-content-disposition=attachment%3B+filename%3Dopentelemetry-course-main.zip&Expires=1790114092&Signature=zwjdff3eUKi1LmSS3jjjZgPvifP7KyIE6gNlQBzjNYyo1LWkoP86M7MAzOCsxlbZFvFEpNAblooYC30RWr7pyaWJtl91gX8~8blPc3FuMYgh80BjD9FTUtifXBylUUpVz9uoOSQEkd2h7YlBg3Ea-VhnJ53Ubp-WAgS1avnIqTrFnHCbi~VbZ0nTOPxxvfswD4HoCx-KPf0I9KLJ-AKES1h3jO3jmiTGfHJwJ1XaaEcU-vSAgzl0mgEeqj6AVatat3qOkhMPpO3o~6CB1vG0aQ7uGzdSnUhAu4xpgIINok-yQApriUmbpz2-FihxSSMj~5DCseuB7pCfDeIlI2JDbw__&Key-Pair-Id=K3MG148K9RIRF4)
3. [GitHub Repository for Course Code](https://github.com/lm-academy/opentelemetry-course)

## Section 2: Local Setup
### My Local Setup
1. VS Code
2. WSL setup
3. TypeScript and Python based
4. `npm`
	1. `node --version`
	2. `npm --version`
	3. `python -V`
		1. `pip` - for virtual environment
		2. `uv` - automatically instantiates a virtual environment

### [Windows Users] Note About Enabling WSL Windows Feature
1. Enable WSL
	1. Start Menu
	2. Search: Turn Windows feature on or off
	3. Tick: Windows Subsystem for Linux
	4. Restart the system

### [Windows Users] Installing Windows Subsystem for Linux (WSL)
1. Microsoft store
	1. Ubuntu
		1. Ubuntu (no version)
		2. Get
		3. Open
			1. Set up username and password
	2. Terminal: Windows PowerShell
		1. `wsl` - opens Ubuntu terminal (VM)
		2. `cd ~` - moves to the home directory
		3. `explorer.exe .` - shows where it is mounted in Windows
	3. `echo "hello" > hello.txt`
		1. file is created in Windows
	4. `cat hello.txt`
2. Explorer > Linux > Ubuntu
3. VS Code
	1. Extensions
		1. `WSL`
			1. Install
			2. Click Remote explorer
				1. Ubuntu
					1. Connect
						1. Starts VS Code in WSL
							1. Open a terminal - It will be in VM
4. `cd ~`
	1. `mkdir dummy`
	2. `cd dummy`
	3. `echo "echo 'hello world'" > say-hi.sh
	4. `chmod +x say-hi.sh`
	5. `./say-hi.sh`
	6. `code .`
		1. Connects to Ubuntu machine

### [Windows Users] Windows Subsystem for Linux Features
1. [https://github.com/lm-academy/opentelemetry-course](https://github.com/lm-academy/opentelemetry-course)
2. `unzip v1.1.0.zip` - starting code
3. `python -m venv .venv` **(M)**
	1. Alternatives:
		1. `pip install -r requirements.txt`
		2. `uv sync` (`uv.lock` and `pyproject.toml`)
4. `compose` - reference only
5. `labs` - reference

### Navigating Course Resources and Folders

## Section 3: Observability Fundamentals
### Section Introduction
1. Observability Foundations
	1. Section overview:
		1. What is Observability:
			1. Understanding system behavior through external signals in distributed architectures
			2. How observability differs from traditional monitoring and why it matters
		2. The Three Pillars
			1. Metrics, logs, and traces as distinct signal types with complementary roles
			2. How combining all three signals privides complete visibility into a system
		3. Metrics and Histograms
			1. Counters, guages, and histograms - when and why to use each type
			2. Reading percentiles (P50, P95, P99) to understand tail latency and user impact
		4. Logs and Traces
			1. Structured logging, severity levels, and capturing event context over time
			2. Trace IDs, spans, and parent-child relationships across distributed services
		5. SLIs, SLOs, and SLAs
			1. Defining user-centric reliability targets and aligning them to service commitments.
			2. The buffer between internal objectives and external contractual agreements.
		6. Error Budgets and the Four Golden Signals
			1. Quantifying acceptable failure to balance reliability and development velocity.
			2. Latency, traffic, errors, and saturation as a universal monitoring baseline.

### What Is Observability?
1. What is observability?
	1. Understanding System Behavior through external signals
		1. Example: E-commerce store
			1. Complicated distributed systems
				1. Inter-service communication between clusters or third party
					1. It should emit signals that will help us understand the system
2. Monitoring vs Observability:
	1. Monitoring
		1. Known questions (are answered)
		2. Predefined dashboards
		3. Known failure modes
		4. "Is the system healthy?"
	2. Observability
		1. Unknown questions (we need to figure out what actually happened)
		2. Exploratory investigation
		3. Unespected behaviors
		4. "Why did this request fail?"
3. Modern system complexity:
	1. Hundreds of microservices vs. Single monolithic applications
	2. Network communication vs. Direct function calls
	3. Dynamic deployment in containers vs. Static servers
	4. Auto-scaling based on demand vs. Peak-load provisioning
	5. Problems emerge from complex interactions between components rather than from single points of failure

### The Three Pillars of Observability
1. Observability Pillars
	1. Metrics: Provide numeric aggregates that can be used to obtain a high-level overview of system health, alerting, and capacity planning.
		1. They are numbers
		2. They are aggregates
			1. Difficult to investigate a single failure point
	2. Logs: Discrete events with rich context that provide the exact error messages and conditions at specific moments
		1. Not enough
			1. If it is a distributed system with many services
				1. We need to trace requests (to connect metrics and logs of each system)
	3. Traces: Request journeys through services that pinpoint bottlenecks and latency sources
2. Don't output as much data as possible
	1. Noise

### Metrics and Metric Types
1. Metrics
	1. Quantitative Measurements of a System
		1. How fast?
		2. How many?
		3. How much?
	2. Examples:
		1. **Request count**: How many HTTP requests?
			1. Only goes up
		2. **Error rate**: What percentage of requests are failing?
		3. **Latency**: How long do requests take to complete?
		4. **CPU usage**: How much CPU are we consuming?
		5. **Active connections**: How many database connections are open?
	3. Types of Metrics:
		1. **Counters**: Monotonically increasing values. They only go up.
			1. Examples: Total HTTP requests, total bytes transferred, total errors
		2. **Guages**: Point-in-time measurements that can go up or down.
			1. Examples: current memory usage, queue depth, CPU percentage.
		3. **Histograms**: Capture distributions of values, providing more insight than just averages.
			1. Examples: p95, p99, and p99.9 for request latency

### Histograms and Percentiles
1. Histograms:
	1. Understand how to read and interpret histograms
		1. Bar chart
			1. x axis: buckets (time range, say)
			2. y axis: occurrences
2. Percentiles:
	1. The pX-Percentile defines a single value Y below which X percent of the observed values lie.
		1. p95 - 95% of the requests have latency below 500ms (5% of requests have latency above 500ms)

### Logs and Structured Logging
1. Logs:
	1. Discrete Records of Events:
		1. Capture the raw details of discrete events
		2. More expensive to store and index than metrics
		3. Human-readable vs. Machine-readable logs.
			1. Easy for humans to follow but hard for machines to parse
				1. Unstructured or inconsistent structure
			2. Machine-readable logs: json
				1. Easy to parse to human-readable logs
		4. Multiple levels: DEBUG, INFO, WARN, ERROR, FATAL
	2. Levels:
		1. DEBUG: Detailed information for debugging. Called function X with parameters Y.
			1. More technical in nature
				1. Not in production
					1. Enabled for temporary investigation
		2. INFO: Normal operations. "User logged in". "Order processed". Helpful for understanding application flow.
		3. WARN: Something unexpected but not an error.
			1. "Rate limit approaching."
			2. "Cache miss."
				1. Potential issues to investigate
					1. Example: Code change is causing cache to not recognize the keys
		4. ERROR: Something failed. "Payment gateway timeout". "Database connection refused". Requires attention.
			1. Usually impacts the end user
				1. There is error handling
		5. FATAL: Critical failure, application can't continue. "Out of memory." "Config file missing".

### Distributed Tracing and Spans
1. Traces:
	1. The complete journey of a request through the system
		1. POST /checkout
			1. Checkout
				1. Validate cart items
			2. Inventory
				1. Check item availability
				2. Sanitize input
					1. SELECT p WHERE...
			3. Payment
				1. Execute payment
				2. Buil invoice
					1. Call Stripe API
						1. Publish order - Checkout service
	2. Trace: The complete story of one request. It has a unique trace ID that follows the request everywhere it goes.
	3. Span: A single operation within a trace. Each service handling the request instantiates one or more spans.
		1. We don't have spans for external services
		2. Elements:
			1. A **name** (like "GET /api/users")
			2. **Start** and **end timestamps**
			3. **Attributes** (key-value pairs, context)
				1. Metadata
					1. Request method
					2. Route
					3. Status code
					4. etc.
			4. A **parent span ID** (relationships)
		3. Information:
			1. The complete path the request took
			2. How long each operation took
				1. Build metrics around it
			3. Parallel vs. sequential operations
			4. Where errors occurred
				1. Leads to logs

### Choosing and Combining Observability Signals
1. Which signals to use?
	1. How the three signals complement each other
		1. Metrics:
			1. Dashboards showing system health
			2. Alerts on abnormal conditions
			3. Capacity planning and trending
				1. To know when autoscaling is happening
				2. Is there a baseline value?
					1. Are they increasing or decreasing?
				3. Is there a trend?
			4. Aggregated views across instances
		2. Logs:
			1. Detailed error messages
				1. Detailed messages of what is going on in the services
			2. Business logic debugging
			3. Audit trails
			4. Raw values and rich context
		3. Traces:
			1. Debugging slow requests
			2. Service dependencies
			3. Finding where errors originate
			4. Optimizing critical paths
	2. Example:
		1. Metrics alert you (**what** - what is the issue?) 
			1. Your alert fires: **HTTP error rate > 1% for 5 minutes**
		2. Traces show you where (**where** - where is the issue?)
			1. You look for traces with **HTTP status 500** and inspect the **trace structure** of failing requests
				1. Which span is causing the issue?
		3. Logs explain why (**why** - why did the issue occur?)
			1. You filter your logs by the trace ID from on failing request, finding the exact error: Payment gateway returned 503 Service Unavailable - rate limit exceeded

### Service Level Indicators
1. Service Level Indicators (SLIs)
	1. What to measure?
		1. Examples:
			1. HTTP Request count
			2. HTTP Request error rate
			3. HTTP request latency
			4. Heap allocation
			5. CPU usage
			6. Pod restarts
			7. Connection pool size
			8. DB query duration
			9. Disk I/O
			10. Memory usage
		2. Is it good to have everything? It is as good as nothing
			1. Service Level Indicators (SLIs)
				1. A Service Level Indicator is a carefully selected metric that **directly measures** a service's behavior **from the user's perspective**.
					1. Examples:
						1. HTTP request latency (impacts the experience of the user)
			2. Examples of good SLIs:
				1. API Svc:
					1. Availability: Percentage of non-5xx responses
						1. More 5xx responses - bad user experience
					2. Latency: Percentage of completion within 500ms
				2. Batch jobs:
					1. Throughput: Percentage of timely completion
					2. Correctness: Percentage of correct completion
				3. DB:
					1. Availability: Percentage of queries that succeed
					2. Latency: Percentage of completion within 100ms
			3. End-user:
				1. It could be an external or an internal user within the company
					1. Example: For platform team, the end users are other teams within the company
			4. Examples of not so important SLIs
				1. Disk I/O (secondary metric)
					1. Added later if this is potentially causing the problem
		3. Qualitative measurements are not good SLIs
			1. Examples:
				1. Customer satisfaction
		4. SLIs should be complete (the entire experience, even with asynchronous workflows)
			1. They should represent the entire experience of the user

### Service Level Objectives
1. SLOs
	1. Set specific target values for SLIs (SLIs are for internal use. They are not committed to external users)
		1. Service Level Objectives (SLOs)
			1. An SLO is a target value for an SLI. It's the promise you make about service quality.
				1. Are we delivering how much we want to internally deliver?
		2. Examples of SLIs
			1. Availability: Percentage of non-5xx responses
			2. Latency: Percentage of completiong within 500ms
			3. ---
			4. Throughput: Percentage of timely completion
			5. Correctness: Percentage of correct completion
		3. Examples of SLOs
			1. 99.95% of requests return non-5xx status codes
			2. 99% of requests complete within 500ms
			3. ---
			4. 99.5% of reports generate within 1 hour of data arrival
			5. 99.99% of calculations match validation checks

### Service Level Agreements
1. SLAs
	1. Contractual agreements with customers (has consequences - legally binding)
		1. SLAs
			1. The contractual commitments you make with your customers regarding a certain SLI. **SLAs should always be less than SLOs**
				1. We don't want to violate SLAs
					1. We should not commit to the SLOs, which are internal
					2. We can also set different SLAs depending on the customer tier
			2. Why not promise more?
				1. Why not promise 99.99% or 99.999% availability?
					1. The answer is **cost** and **opportunity cost**
						1. Each additional nine of availability requires **exponentially more effort**
							1. Examples:
								1. 99% - 7 hours downtime per month
									1. Rlatively easy (with modern practices)
								2. 99.9% - 43 minutes per month
									1. Requires good practices (SE practices, solid architecture)
								3. 99.99% - ~ 4 minutes per month
									1. Requires sophisticated automation (comprehensive test coverage, automated rollback strategies, etc.)
								4. 99.999% - ~ 25 seconds per month (very few companies can achieve this)
									1. Requires massive investment

### Error Budgets and Risk Management
1. Error Budgets
	1. How much you can afford to fail
		1. Example: 99% SLO (1% failure)
	2. The error budget is the difference between 100% and the set SLO. If your SLO is 99.9% availability, your error budget is 0.1% failure. Over a 30-day month:
		1. Total minutes: 43,200
		2. Allowed downtime: 43.2 minutes
		3. That's your error budget
	3. Error budget > 0?
		1. Push risky features faster
		2. Deploy more frequently
		3. Run experiments in production
		4. Take calculated risks
	4. Error budget <= 0?
		1. Freeze risky deployments
		2. Focus on reliability improvements
		3. Pay down technical debt
		4. Investigate and fix the root causes of recent outages
			1. We can look back at recently shipped features and see what broke the SLO

### The Four Golden Signals
1. Google's four metrics that apply to almost every service (good starting point)
	1. **Latency**: How long does it take? (for an operation)
		1. Measure response time for requests
		2. Distinguish between successful request latency and failed request latency
		3. Track percentiles (p50, p95, p99) not just averages
	2. **Traffic**: How much demand?
		1. Measure requests per second, queries per second, or whatever units make sense for your system
		2. Helps normalize other metrics and understand system capacity
	3. **Errors**: What's the rate of failures?
		1. Measure the percentage of requests that fail.
		2. Define errors explicitly (are 4xx responses also errors? Are timeouts errors?)
	4. **Saturation**: How "full" is the system?
		1. Measure resource utilization: CPU, memory, disk, network bandwidth, database connections.
		2. High saturation indicates you're approaching limits and should expect degraded performance soon.
			1. May need to scale the system
2. Some of them are SLIs and some are not
	1. Latency and errors are SLIs
		1. These matter for a user
	2. Traffic and saturation - don't matter from a single user perspective
		1. They are behind the scenes metrics
			1. They have impact on SLIs

## Section 4: Setting Up the Observability Stack
### Section Introduction
1. Setting up the observability stack
	1. Section overview
		1. Local environment setup
		2. Deploy observability backends
			1. Understand the roles of Prometheus, Loki, Tempo, and Grafana as an observability stack
			2. Deploy each service in our Compose application
		3. Application and architecture
			1. The distributed translation application as the instrumentation target for the course
			2. How telemetry signals flow from the application through backends into Grafana (how to use it for fetching data)

### Development Environment Setup
1. Tools:
	1. Docker
		1. `docker --version`
	2. k8s
		1. `kubectl config current-context`
		2. `kubectl create cluster --name observability`
		3. `kubectl version`
			1. `Kustomize` support
	3. Docker compose
2. AI Checkpoints
	1. Environment verification prompt:
		1. "What command should I run to verify all prerequisites for a local Kubernetes cluster?"
	2. What to evaluate:
		1. `docker version`
		2. `kubectl cluster-info`
		3. Docker is running and kubectl can connect to the cluster
		4. The actual commands
	3. Troubleshooting guidance:
		1. "My kubectl cannot connect to the cluster. What are the most common causes and how do I diagnose them?"
	4. What to evaluate:
		1. `minikube status`
		2. `Docker Desktop k8s is enabled`
		3. `kubectl config current-context`
		4. Debugging steps

### Prometheus in 5 Minutes
1. Prometheus in 5 minutes
	1. Understand the main components and characteristics of prometheus
		1. It is a time-series database designed for storing metrics
		2. Pull-based system
			1. Prometheus pulls data from `/metrics` (scrapes metrics data at regular intervals)
				1. Push-gateway: it is used only for short-lived processes or services (in between two scrapes)
	2. Data structure
		1. `http_requests_total{method="GET", path="/api/users"}`
			1. `http_requests_total` - metric name
			2. Labels: (key-value pairs)
				1. `method="GET"`
				2. `path="/api/users"`
					1. Each combination instantiates a new time series
				3. Cardinality: The number of labels
		2. `http_requests_total{method="POST", path="/api/users"}` (a different time series)
	3. PromQL: The Query Language
		1. Query language for time-series metrics data, enabling aggregations and mathematical operations over dimensional data (efficient)
			1. Examples:
				1. **Filter by labels**: using curly braces `http_requests_total{status="500"}`
				2. **Functions** and **operators**: `rate(http_requests_total[5m])` (the number of requests per second averaged over 5m)
				3. **Aggregators** `sum by (path) (rate(http_requests_total[5m]))`
					1. `path` - for each unique endpoint
				4. **Percentiles** `histogram_quantile(0.99, ...)` (`...` - query)
2. Use-case

```
App -> Collector <- scrapes - Prometheus <-----> Grafana
```

	1. Prometheus - data source for Grafana
	2. Collector - OpenTelemetry

### Hands-On Lab: Setting Up Prometheus - Lab Overview
1. `section-setup`
	1. `lab-deploy-prometheus.md`

### Hands-On Lab: Configuring Prometheus
1. Prometheus configuration: `prometheus.yaml`

```yaml
global:
  scrape_interval: 15s
  evaluation_interval: 15s
  
scrape_configs:
  - job_name: 'prometheus'
    static_configs:
	  - targets: ['localhost:9090']
```

	1. `scrape_internal`: Scrape every 15s
	2. `evaluation_interval`: How often Prometheus will evaluate alerting and recording
		1. Too fast for bigger servers
	3. `scrape_configs`:
		1. Configured here explicitly
			1. If we are use k8s propemetheus operator, it can dynamically figure out which targets to scrape (with service discovery)
		2. `prometheus` - Prometheus will reach out to itself and collect metrics from itself
2. `compose.observability.yaml`

```yaml
services:
  prometheus:
    image: prom/prometheus:v3.9.1
	container_name: prometheus
	command:
	  - '--config.file=/etc/prometheus/prometheus.yaml'
	  - '--storage.tsdb.path=/prometheus'
	  - '--storage.tsdb.retention.time=15d'
	volumes:
	  - ./prometheus.yaml:/etc/prometheus/prometheus.yaml:ro
	  - prometheus-data:/prometheus
	ports:
	  - '9090:9090'
	networks:
	  - observability
	restart: unless-stopped
	
volumes:
  prometheus-data:
```

### Hands-On Lab: Launching and Verifying Prometheus
1. `compose.yaml` - orchestrator

```yaml
# Main Docker Compose file for OpenTelemetry Course
# This file includes the observability stack and (soon) application

include:
  - compose.observability.yaml
  
# Shared networks for all services
networks:
  observability:
    driver: bridge
	name: observability
```

2. Start Prometheus:

```bash
docker compose up
```

3. To remove existing containers:

```bash
docker system prune
```

4. View container:

```bash
docker compose ps
```

5. Open: `http://localhost:9090`
	1. Table
	2. Graph
	3. Explain - multiple components of the system
	4. Query: `scrape_duration_seconds` (auto-complete)
		1. Shows for localhost:9090
	5. Query: `rate(prometheus_http_requests_total[5m])`
	6. Memory usage query: `process_resident_memory_bytes / 1024 / 1024` (in MB)
	7. Uptime query: `time() - process_start_time_seconds`
	8. Status: Target health
		1. Shows prometheus health

### Loki in 5 Minutes
1. Loki:
	1. Understand the main components and characteristics of Loki
		1. Log aggregation system designed to be cost-effective and scalable
			1. It is different:
				1. It indexes only the metadata instead of every word from the log stream
					1. Metadata indexing:
						1. Log entry:
							1. Timestamp: `2024-01-15 10:00:05`
							2. Key-value pairs (labels): `service=api`, `level=error`
							3. Log content: `Payment for cart {id} failed`
						2. Loki storage:
							1. Label index - indexes timestamp and labels
							2. Log contents - stored in chunks in a non-indexed database
	2. LogQL: The Query Language
		1. Query language for log data that combines label selection with log stream filtering and parsing (inspired by PromQL)
			1. Filter by labels using cury braces: `{job="frontend", environment="production"}`
			2. Line filters for content search: `{job="frontend"} |= "error" |~ "timeout|failed"`
				1. Pipelines
					1. Select logs that contain "error"
					2. Filter to look for `timeout` or `failed`
			3. Parsers extract structured data: `{job="frontend"} | json | status_code >= 500`
				1. Pipeline for structured logs
				2. Extract all json attributes and filter by status code
					1. Expensive to parse json for a lot of values
			4. Log rates and volumes: `sum(rate({job="frontend"} |= "error" [5m]))`
				1. Total error rate of frontend jobs over 5m
2. Architecture:

```
SDK - inject trace IDs into logs -> App ---> Collector - forwards logs to Loki -> Loki <- data source for -> Grafana
```

### Hands-On Lab: Setting Up Loki - Lab Overview
1. `lab-deploy-loki.md`
2. `compose/loki-config.md`

```yaml
auth_enabled: false

server:
  http_listen_port: 3100
  
ingester:
  lifecycler:
    ring:
	  kvstore:
	    store: inmemory
	  replication_factor: 1
  chunk_idle_period: 5m
  chunk_retain_period: 30s
  
schema_config:
  configs:
    - from: 2024-01-01
	  store: tsdb
	  object_store: filesystem
	  schema: v13
	  index:
	    prefix: index_
		period: 24h
		
storage_config:
  tsdb_shipper:
    active_index_directory: /loki/index
	cache_location: /loki/cache
  filesystem:
    directory: /loki/chunks
	
limits_config:
  retention_period: 168h
  
compactor:
  working_directory: /loki/compactor
  compaction_interval: 10m
  retentin_enabled: true
  delete_request_store: filesystem
```

	1. Loki listens on `3100`
	2. `ingester` - Part of the system that will receive new logs
		1. `replication_factor: 1` - no backup
	3. `schema_config` - configuring log schema
		1. `store: tsdb` - time series database
		2. `schema: v13` - internal schema version
	4. `compactor` - for compacting information so that Loki would not consume as much storage as it would otherwise
		1. Checks every 10m and checks if a log has exceeded a retention period and deletes old logs
3. `compose.observability.yaml`

```yaml
services:
  loki:
    image: grafana/loki:3.6.6
	container_name: loki
	user: root
	command:
	  - '-config.file=/etc/loki/loki.yaml'
	  - '-target=all'
	volumes:
	  - ./loki-config.yaml:/etc/loki/loki.yaml:ro
	  - loki-data:/loki
	  - loki-wal:/wal
	ports:
	  - '3100:3100'
	networks:
	  - observability
	restart: unless-stopped
	
volumes:
  loki-data:
  loki-wal:
```

3. Run `docker compose up` (if it doesn't work, run `docker compose down` first)
4. `docker compose ps`
5. Loki exposes REST API on port 3100:

```
# Check health
curl http://localhost:3100/ready

# Check metrics
curl http://localhost:3100/metrics

# List label names (may be empty at first)
curl http://localhost:3100/loki/api/v1/labels
```

6. Check Loki Metrics in Prometheus
	1. Loki exposes Prometheus metrics> Add Loki as a scrape target:
	2. Edit `compose/prometheus.yaml`
	
	```yaml
	scrape_configs:
	  - job_name: 'prometheus'
	    static_configs:
		  - targets: ['localhost:9090']
		  
	  - job_name: 'loki'
	    static_configs:
		  - targets: ['loki:3100']
	```
	
	3. Reload Prometheus config:
	
	```
	docker compose restart prometheus
	```

### Hands-On Lab: Deploying Loki
1. Check Loki:

```
docker compose ps

docker network inspect observability
```

```
# Check health
curl http://localhost:3100/ready

# Check metrics - Prometheus friends. Prometheus can scrape them.
curl http://localhost:3100/metrics

# List label names (may be empty at first)
curl http://localhost:3100/loki/api/v1/labels
```

### Hands-On Lab: Connecting Loki to Prometheus
1. Queries: `loki_`

### Hands-On Lab: Testing Loki Log Ingestion
1. Generate Agent instructions: Github Copilot + Claude Saunet 4.5
	1. `scratchpad.md`
	
	```
	I have a project defined under the `compose` folder and I ahve just deployed the loki service. I'd like you to generate a short and concise script to help me validate that Loki can receive, process, and store log stat. The script should use curl (or an equivalent available in my system) and avoid checking the details of Loki. I'm running on Windows.
	
	Desired outout:
	- One script that sends some log data and confirms that they are stored in Loki.
	- One script that cleans up the data.
	- A few PromQL queries to check Loki metrics.
	
	Rules:
	- Be concise, avoid over-engineering.
	- Document the instructions and commands as if I were a novice in Loki and Prometheus.
	```
	
2. valiadate-loki.sh

```bash
#!/usr/bin/env bash
set -euo pipefail

LOKI_URL="http://localhost:3100"
TEST_ID="$(printf '%08x%08x%08x%08x' \
  "$(((RANDOM << 15) | RANDOM))" \
  "$(((RANDOM << 15) | RANDOM))" \
  "$(((RANDOM << 15) | RANDOM))" \
  "$(((RANDOM << 15) | RANDOM))")"
MESSAGE="Loki validation ${TEST_ID}"
NOW="$(date +%s)"
TIMESTAMP_NS="${NOW}000000000"
START_NS="$((NOW - 120))000000000"
END_NS="$((NOW + 60))000000000"

printf '{"streams":[{"stream":{"job":"loki-validation","test_id":"%s"},"values":[["%s","%s"]]}]}' \
  "$TEST_ID" "$TIMESTAMP_NS" "$MESSAGE" |
  curl --fail --silent --show-error \
    --request POST "$LOKI_URL/loki/api/v1/push" \
    --header 'Content-Type: application/json' \
    --data-binary @-

QUERY="{job=\"loki-validation\",test_id=\"${TEST_ID}\"}"
for _ in {1..15}; do
  RESULT="$(curl --fail --silent --show-error --get \
    "$LOKI_URL/loki/api/v1/query_range" \
    --data-urlencode "query=${QUERY}" \
    --data-urlencode "start=${START_NS}" \
    --data-urlencode "end=${END_NS}" \
    --data-urlencode 'limit=10')"
  if [[ "$RESULT" == *"$MESSAGE"* ]]; then
    echo "SUCCESS: Loki returned the test log."
    echo "To clean it up, run: bash cleanup-loki.sh ${TEST_ID}"
    exit 0
  fi
  sleep 1
done

echo "ERROR: The test log was sent, but not found in Loki. Test ID: ${TEST_ID}" >&2
exit 1
```

3. cleanup-loki.sh

```bash
#!/usr/bin/env bash
set -euo pipefail

if [[ $# -ne 1 || ! "$1" =~ ^[0-9a-fA-F]{32}$ ]]; then
  echo "Usage: bash cleanup-loki.sh <32-character-test-id>" >&2
  exit 2
fi

LOKI_URL="http://localhost:3100"
TEST_ID="$1"
QUERY="{job=\"loki-validation\",test_id=\"${TEST_ID}\"}"
NOW="$(date +%s)"
START="$((NOW - 86400))"
END="$NOW"

curl --fail --silent --show-error --get --request POST \
  "$LOKI_URL/loki/api/v1/delete" \
  --data-urlencode "query=${QUERY}" \
  --data-urlencode "start=${START}" \
  --data-urlencode "end=${END}"
echo "Deletion requested for test ID ${TEST_ID}. Loki applies deletions asynchronously."
```

4. README.md

```bash
# Loki quick check

Start the stack if it is not already running (PowerShell):

```powershell
docker compose -f .\compose\compose.yaml up -d
```

## PowerShell (Windows)

```powershell
powershell -ExecutionPolicy Bypass -File .\compose\test_scripts\validate-loki.ps1
```

## Bash (Git Bash, WSL, or Linux)

These scripts require `curl`. Run them from the `compose/test_scripts` directory:

```bash
bash validate-loki.sh
```

Both validation scripts send a uniquely labeled test log, query Loki to confirm it can be read back, then print a unique test ID and cleanup command. In PowerShell, run:

```powershell
powershell -ExecutionPolicy Bypass -File .\compose\test_scripts\cleanup-loki.ps1 -TestId YOUR_TEST_ID
```

In Bash, run from `compose/test_scripts`:

```bash
bash cleanup-loki.sh YOUR_TEST_ID
```

Loki queues deletions; it may take a while before the data is physically removed.

## Prometheus checks

Open [http://localhost:9090](http://localhost:9090), enter a query in the query box, and select **Execute**. For the rate queries, wait about 30 seconds so Prometheus can collect at least two samples.

```promql
up{job="loki"}
```

`1` means Prometheus can reach Loki.

```promql
sum(rate(loki_distributor_lines_received_total[5m]))
```

Log lines received per second over the last five minutes. This should rise after the test sends its log.

```promql
sum(rate(loki_distributor_bytes_received_total[5m]))
```

Bytes received per second over the last five minutes. A rate of `0` is normal when no logs have recently been sent.
```

### Hands-On Lab: Exploring Loki Metrics
1. loki-promql-queries.md

### Tempo in 5 Minutes
1. Understadn the main components and characteristics of temp:
	1. Tempo: Distributed tracing backend designed to store traces cost-effectively at scale
		1. Metadata indexing:
			1. Trace entry:
				1. Trace ID -> Minimal Index
				2. service=api, level=error (labels) -> Minimal Index
				3. Spans, Contents -> Compressed form in a different db
		2. TraceQL: The query language
			1. Query language for distributed traces that enables searching spans by attributes and analyzing trace structure
				1. Filter by attributes: `{service.name="frontend" && http.request.method="GET"}`
				2. Duration filtering: `{service.name="frontend" && duration > 100ms}` (spans with duration > 100ms)
				3. Structural queries (parent-child): `{span.http.method="GET"} >> {status = error}`
					1. Children: Operations within operations
				4. Aggregations: `count({status = error}) by (resource.service.name)`
2. Architecture:

```
SDK - takes care of context propagation -> App -> Collector - forwards traces to Tempo -> Tempo <- data source -> Grafana
```
	
	1. context propagation - propagation of a single trace-id across services

### Hands-On Lab: Setting Up tempo - Lab Overview
1. `compose/tempo-config.yaml`

```yaml
server:
  http_listen_port: 3200
  
distributor:
  receivers:
    otlp:
	  protocols:
	    grpc:
		  endpoint: 0.0.0.0:4317
		http:
		  endpoint: 0.0.0.0:4318
		  
storage:
  trace:
    backend: local
	local:
	  path: /var/tempo/traces
	wal:
	  path: /var/tempo/wal
	  
query_frontend:
  search:
    max_duration: 0s
ingester:
  max_block_duration: 5m
  
compactor:
  compaction:
    block_retention: 72h
```

	1. `distributor` - Open Telemetry protocol is configured here
		1. Tempo will receive trace data from OpenTelemetry via the two endpoints
2. `compose.observability.yaml`

```yaml
services:
  tempo:
    image: grafana/tempo:2.10.1
	container_name: tempo
	command:
	  - '-config.file=/etc/tempo/tempo.yaml'
	  - '-target=all'
	volumes:
	  - ./tempo-config.yaml:/etc/tempo/tempo.yaml:ro
	  - tempo-data:/var/tempo
	ports:
	  - '3200:3200'
	networks:
	  - observability
	restart: unless-stopped

volumes:
  tempo-data:
```

3. Testing:

```bash
# Check ready status
curl http://localhost:3200/ready

# Check metrics endpoint
curl http://localhost:3200/metrics | head -20
```

4. Add Tempo to Prometheus Scrape Targets:

```yaml
scrape_configs:
  - job_name: 'prometheus'
    static_configs:
	  - targets: ['localhost:9090']
  - job_name: 'loki'
    static_configs:
	  - targets: ['loki:3100']
  - job_name: 'tempo'
    static_configs:
	  - targets: ['tempo:3200']
```

5. Reload Prometheus:

```
docker compose restart prometheus
```

### Hands-On Lab: Deploying Tempo
1. Query: `tempo`

### Hands-On Lab: Setting Up Grafana - Lab Overview
1. Deploying Grafana: Visualization layer. Configure sources as Prometheus, Tempo, and Loki
2. `compose/grafana-datasources.yaml`

```yaml
apiVersion: 1

datasources:
  - name: Prometheus
    type: prometheus
	access: proxy
	url: http://prometheus:9090
	isDefault: true
	editable: false
	jsonData:
	  timeInterval: 15s
	  httpMethod: POST
	  
  - name: Loki
    type: loki
	access: proxy
	url: http://loki:3100
	editable: false
	jsonData:
	  maxLines: 1000
	  
  - name: Tempo
    type: tempo
	access: proxy
	url: http://tempo:3200
	editable: false
	jsonData:
	  tracesToLogsV2:
        datasourceUid: Loki
        tags: ['job', 'instance']
      tracesToMetrics:
        datasourceUid: Prometheus
      serviceMap:
        datasourceUid: Prometheus	  
```

3. `compose.observability.yaml`

```yaml
services:
  grafana:
    image: grafana/grafana:12.3
	container_name: grafana
	environment:
	  - GF_AUTH_ANONYMOUS_ENABLED=true
	  - GF_AUTH_ANONYMOUS_ORG_ROLE=Admin
	  - GF_SECURITY_ADMIN_PASSWORD=admin
    volumes:
	  - ./grafana-datasources.yaml:/etc/grafana/provisioning/datasources/datasources.yaml:ro
	  - grafana-data:/var/lib/grafana
	ports:
	  - '3000:3000'
	networks:
	  - observability
	restart: unless-stopped
	depends_on:
	  - prometheus
	  - loki
	  - tempo
	  
volumes:
  grafana-data:
```

4. Start:

```
docker compose up
```

5. Verify: http://localhost:3000
	1. Verify data sources
	2. Explore Prometheus metrics:
		1. `up`
		2. `up{job="Loki"}`
		3. `rate(prometheus_http_requests_total[5m])` - request rate
6. AI Checkpoints:

### Hands-On Lab: Deploying and Connecting Grafana
1. http://localhost:3000
	1. Explore - to work with different data sources
		1. Prometheus
		2. Loki
		3. Tempo
2. Test:

```
up
up{job="Loki"}
rate(prometheus_http_requests_total[5m])
```

3. Adding Grafana job to Prometheus configuration:

```yaml
scrape_configs:
  - job_name: 'grafana'
    static_configs:
	  - targets: ['grafana:3000']
```

3. Connections:
	1. Data sources
		1. Loki
			1. Test
		2. Temo
		3. Prometheus

### Hands-On Lab: Deploying the Translation Application - Lab Overview
1. Redis-based job queueing and Server-Sent Events (SSE) for real-time updates.
2. Overview:
	1. Frontend Service: Express.js/TypeScript server
	2. Worker Service: Python-based
	3. Redis: Message broker
		1. pub/sub
		2. Session store
3. `compose/compose.app.yaml`

```yaml
# Application Services
# Translation app with frontend, worker, and Redis

services:
  redis:
    image: redis:8.6.0-alpine
	container_name: redis
	ports:
	  - '6379:6379'
	networks:
	  - app
	healthcheck:
	  test: ['CMD', 'redis-cli', 'ping']
	  interval: 5s
	  timeout: 3s
	  retries: 5
	restart: unless-stopped
	
  frontend:
    image: lmacademy/web-translator-frontend:v1.1.0
	container_name: frontend
	ports:
	  - '3001:3000'
	environment:
	  - REDIS_HOST=redis
	  - REDIS_PORT=6379
	  - PORT=3000
	  - LOG_LEVEL=info
	  - SOURCE_LANGUAGE=en
	depends_on:
	  redis:
	    condition: service_healthy
    networks:
	  - app
	restart: unless-stopped
	
  worker:
    image: lmacademy/web-translator-worker:v1.1.0
	container_name: worker
	environment:
	  - REDIS_HOST=redis
	  - REDIS_PORT=6379
	  - LOG_LEVEL=info
	  - SOURCE_LANGUAGE=en
    depends_on:
	  redis:
	    condition: service_healthy
    networks:
	  - app
	restart: unless-stopped
```

4. `compose/compose.yaml`

```yaml
# Main Docker Compose file for OpenTelemetry Course
# This file includes the observability stack and application

include:
  - compose.observability.yaml
  - compose.app.yaml
  
# Shared networks for all services
networks:
  observability:
    driver: bridge
	name: observability
  app:
    driver: bridge
	name: app
```

5. Deploy:

```bash
docker compose up -d
```

6. Verify:

```
# Check observability network
docker network inspect observability

# Check app network
docker network inspect app
```

7. Test:

```
http://localhost:3001
```

8. Monitor Redis activity:

```
# Access Redis CLI
docker exec -it redis redis-cli

# Check queue length (should be 0 after translations complete)
LLEN translation:jobs

# List all keys (sessions are stored as hashes)
KEYS *

# Inspect a session (replace SESSION_ID with actual ID from URL)
HGETALL session:SESSION_ID

# Check pub/sub channels
PUBSUB CHANNELS

# Exit Redis CLI
exit
```

9. Check container logs:

```bash
# Frontend logs (HTTP requests, SSE connections)
docker compose logs frontend --tail=50

# Worker logs (job processing, translation times)
docker compose logs worker --tail=50

# Redis logs
docker compose logs redis --tail=50
```

### Hands-On Lab: Deploying the Sample Application
1. http://localhost:3001

### Full Stack Architecture Overview
1. System Architecture
	1. Understand the application and observability stack we will work with
		1. frontend - adds translation jobs to queue -> Redis Queue - picks translation jobs from queue -> Worker -> Redis Queue -> frontend
			1. frontend -> Metrics | logs | traces
			2. Redis -> Metrics | logs | traces
			3. Worker -> Metrics | logs | traces
				1. OTEL Collector
					1. Prometheus
					2. Tempo
					3. Loki
						1. Grafana

## Section 5: Introduction to OpenTelemetry
### Section Introduction
1. Introduction to OpenTelemetry Concepts
	1. Section overview
		1. What is OpenTelemetry and why it exists
		2. APIs and SDKs (within OpenTelemetry)
			1. Understand the separation between the two
		3. Automatic and manual instrumentation
			1. Auto-instrumentation for out-of-the-box framework coverage with no code changes
			2. Manual instrumentation for capturing custom business logic and domain context
		4. OpenTelemetry Collector
		5. Semantic Conventions - standards (signals across languages, frameworks, etc.)

### What is OpenTelemetry?
1. Understand what OpenTelemetry is and why it exists
	1. Instrumenting application
		1. Without OpenTelemetry
			1. New relic - its own API
			2. Datadog - its own API
			3. Prometheus
			4. Tempo
			5. Jaeger
			6. ...
				1. OpenTelemetry solves the problem
		2. OpenTelemetry:
			1. An observability framework and toolkit designed to construct and manage telemetry data such as traces, metrics, and logs
				1. It is not yet another backend to store and visualize your data
				2. It is a standardized, vendor-neutral layer between your application and whatever backend you use
					1. **Vendor-neutral APIs** - for constructing telemetry data.
						1. You call OpenTelemetry APIs, not vendor-specific ones.
					2. **SDKs** - that implement those APIs and handle the complexity of batching, sampling, and exporting data.
					3. **Automatic instrumentation libraries** for popular frameworks and languages.
					4. **OpenTelemetry Collector** - a vendor-agnostic pipeline that can receive, process, and export telemetry data.
	2. OpenTelemetry:
		1. An observability framework and toolkit designed to construct and manage telemetry data such as traces, metrics, and logs
		2. Vendor Neutrality:
			1. You instrument once and can switch backends without changing your code. Want to evaluate three different tracing backens? No problem!
		3. Industry standardization:
			1. OpenTelemetry is backed by all major observability vendors. Prometheus, Grafana, DataDog, New Relic - they all support OpenTelemetry
				1. Even for GenAI, AI agents, etc.
		4. Rich ecosystem:
			1. Because OpenTelemetry is a standard, there's a huge library of automatic instrumentation. Most of your telemetry can be generated automatically!
				1. We can focus on instrumenting business logic instead of HTTP logic (a library will do the HTTP instrumentation)

### APIs, SDKs, and Their Separation
1. OpenTelemetry APIs and SDKs (tightly connected)
	1. OpenTelemetry API - for long-term stability
		1. Collection of interfaces and abstract types that define what a **Span** is, what a **Metric** is, and how to construct them. (high level)
	2. OpenTelemetry SDKs - evolve quickly with newer features
		1. The actual implementation of those interfaces. It's the code that constructs real spans, batches them, samples traces, etc.
2. OpenTelemetry API example:

```python
class Span(abc.ABD):
  """A span represents a single operation within a trace."""
  
  @abc.abstractmethod
  def get_span_context(self) -> "SpanContext":
    """Gets the span's SpanContext.
	
	Get an immutable, serializable identifier for this span that can be
	used to construct new child spans.
	
	Returns:
	  A :class:`opentelemetry.trace.SpanContext` with a copy of this span's immutable state
	"""
	
  @abc.abstractmethod
  def set_attributes(
    self, attributes: typing.Mapping[str, types.AttributeValue]
  ) -> None:
    """Sets Attributes.
	
	Sets Attributes with the key and value passed as arguments dict.
	
	Note: The behavior of 'None' value attributes is undefined, and hence
	strongly discouraged. It is also preferred to set attributes at span
```

3. SDK implementation example:

```python
class Span(trace_api.Span, ReadableSpan):
  """See `opentelemetry.trace.Span`.
  
  Users should construct `Span` objects via the `Tracer` instead of this 
  constructor.
  
  Args:
    name: The name of the operation this span represents
	context: The immutable span context
	parent: This span's parent's `opentelemetry.trace.SpanContext`, or
	  ...
  """
  
  def get_span_context(self):
    return self._context
	
  def set_attributes(
  
  ) -> None:
    with self._lock:
	  if self._end_time is not None:
	    logger.warning("Setting attribute on ended span.")
		return
		
	  for key, value in attributes.items():
	    self._attributes[key] = value
	...
```

	1. Frameworks like Flast, FastAPI, Express, should depend on the API.
		1. Import API
			1. The application team should configure the SDK in the application code.
4. Typescript example:

```typescript
// In instrumentation.ts - SDK configuration
import { NodeSDK } from '@opentelemetry/sdk-node';
import { OTLPTraceExporter } from '@opentelemetry/exporter-trace-...'

const sdk = new NodeSDK({
  traceExporter: new OTLPTraceExporter({
    url: 'http://otel-collector:4318/v1/traces',
  }),
  serviceName: 'translator-api',
});

sdk.start();
```

	1. SDK config happens during startup
	
5. Typescript example: `app.ts`

```typescript
// In app.ts - API usage
import { trace } from '@opentelemetry/api'; // abstraction

const tracer = trace.getTracer('translator');

app.post('/', (req, res) => {
  const span = tracer.startSpan('translate_content');
  // ... business logic ...
  span.end();
});
```

	1. The rest of our application code (and the underlying framework) depends on the API, not directly on the SDK.
6.OpenTelemetry SDKs
	1. When you configure the OpenTelemetry SDK in your application, what are you actually specifying?
		1. **Exporters**: Where should telemetry go? OTLP to a Collector? Directly to Prometheus? To the console for debugging?
			1. What are the exporters.
		2. **Processors**: How should telemetry be processed? Batch spans for efficiency? Sample only a percentage of traces? Add custom attributes?
		3. **Samplers**: Which traces should be recorded? Sample 100% for development? 10% for production? Use probabilistic sampling?
		4. **Resource attributes**: What metadata should be attached? Service name, version, deployment environment?

### Automatic and Manual Instrumentation
1. Understand the differences between automatic and manual instrumentation
	1. Automatic instrumentation
		1. You get telemetry for frameworks and libraries without writing any code.
		2. OpenTelemetry provides instrumentation libraries for popular frameworks
			1. Node.js
			2. Python
			3. Go
			4. ...
	2. Manual Instrumentation
		1. Explicitly write code to construct spans, add attributes, and record metrics
		2. Why?
			1. Automatic instrumentation doesn't know about your business logic. It knows that you called a database, but it doesn't know what business operation that database call was part of.
				1. Example: Spans that represent business logic:
					1. `HTTP POST /images`
						1. `upload_article_images` - when we are uploading articles (not any image)
						2. `upload_user_profile_images` - different context
				2. Example: Redis Queue (Automatic)
				
				```
				Span: BLPOP translation: jobs
				  - db.system: redis
				  - db.operation: BLPOP
				```
				
					1. Manual: (more business-related information. More context. More semantics)
					
					```
					Span: process_translation_job
					  - translation.job_id: abc-123
					  - translation.target_language: es
					  - translation.status: success
					```
					
2. Which one to use?
	1. That depends! Normally start with auto-instrumentation: many metrics with little effort.
	2. Once instrumented, extend the code base to include manual instrumentation for relevant business operations.

### The OpenTelemetry Collector
1. The OpenTelemetry Collector:
	1. Vendor-agnostic telemetry data pipeline that can receive telemetry data in multiple formats, process it in various ways, and export it to one or more backends.
		1. The pipeline can have multiple stages
	2. [https://opentelemetry.io/docs/collector/](https://opentelemetry.io/docs/collector/)
		1. Receivers - recieve data from multiple providers (data ingesters)
			1. OTLP (protocol)
			2. Jaeger
			3. Prometheus
		2. Processors - perform different operations
			1. Batching
			2. Adding attributes
			3. Filter data
		3. Exporters - export data to multiple providers
			1. OTLP
			2. Jaeger
			3. Prometheus
	3. Integrates with OTLP, and others
2. Deployment patterns
	1. Agent deployment
		1. Run a collector instance on every host or pod alongside your applications
	2. Gateway deployment
		1. Run the collector as a centrallized service that multiple applications send to
			1. Example: k8s deployment
3. Should I / When to use the Collector? There are some pretty good reasons and use cases:
	1. Not needed
		1. We can send data directly to configured backend
			1. Simple setups don't need a collector
		2. We can configure SDK to send data to a collector and configure the collector to send data to the backend
	2. Use-cases:
		1. **Decouple backends from application code**: The collector configuration is separate from your app code, so you can change exporters independently. (SDK config doesn't need to be touched. Only collector config needs to change)
		2. **Send telemetry to multiple backends simultaneously**: Maybe you're evaluating tools, or you want both an internal Prometheus and an external vendor
		3. **You want centralized sampling or filtering**: Rather than configuring sampling in every application, configure it once in the Collector
		4. **Legacy migrations**: The Collector can receive Jaeger or Zipkin traces and forward them as OTLP, letting you migrate incrementally
		5. **Transform or enrich data**: Add attributes, scrub sensitive data, or reshape telemetry before it reaches backends

### Semantic Conventions
1. Standardized naming rules for Spans, Metrics, and Attributes
	1. Semantic conventions
		1. They define a standard vocabulary for telemetry data. Everyone follows them, independently of language or framework
			1. Span names: What should a span be called?
			2. Attribute names: What should attributes be called? Not `db_name` or `databaseName` but `db.name`
			3. Attribute values: What values are allowed? Status codes are integers, HTTP methods are uppercase (`GET`, `POST`)
			4. Required vs. Optional: Which attributes must always be present versus which are nice-to-have?
		2. Different teams send data with the same syntax:
			1. Node: `http.request.method`, `http.response.status_code`
			2. Python: `http.request.method`, `http.response.status_code`
			3. Go: `http.request.method`, `http.response.status_code`
	2. OpenTelemetry provides the semantic conventions
	
	```javascript
	import {
	  SEMATTRS_HTTP_METHOD,
	  SEMATTRS_HTTP_STATUS_CODE,
	} from @opentelemetry/semantic-conventions;
	
	span.setAttribute(SEMATTRS_HTTP_METHOD, 'GET');
	span.setAttribute(SEMATTRS_HTTP_STATUS_CODE, 200);
	```
	
	```python
	from opentelemetry.semconv.trace import SpanAttributes
	
	span.set_attribute(SpanAttributes.HTTP_METHOD, "GET")
	span.set_attribute(SpanAttributes.HTTP_STATUS_CODE, 200)
	```
	
2. Advantages of using constants:
	1. You can't typo the attribute names
	2. Auto-complete helps you discover available conventions
	3. Your code stays up-to-date if convention names evaolve
	4. It's self-documenting: readers know you're following standards
3. We can also define our own attributes!

```
span.setAttribute('myapp.user.tier', 'premium');
span.setAttribute('myapp.feature.flag.new_ui', true);
span.setAttribute('myapp.experiment.variant', 'B');
```

	1. Use namespaces
	2. Use hierarchy

## Section 6: Setting Up the OpenTelemetry Collector
### Section Introduction
1. Section overview:
	1. Setting up the OpenTelemetry collector
		1. Deploying the collector as a vendor-agnostic pipeline between the application and observability backends.
		2. Verifying end-to-end data flow and monitoring the collector's own operational health.
	2. Instrumenting metrics
		1. Applying automatic instrumentation for framework-level metrics and constructing business metrics
		2. Enriching metrics with dimensional labels and exploring them in Prometheus [and Grafana]
	3. Instrumenting Traces
		1. Capturing framework spans automatically and constructing custom spans for business logic.
		2. Managing span lifecycle, handling errors, and refactoring instrumentation for maintainability.
	4. Instrumenting Logs
		1. Configuring structured logging with trace context injection and adding manual log statements.
		2. Setting up log-trace correlation in Grafana and externalizing configuration through environment variables.

### Hands-On Lab: Local Development Environment Setup - Lab Overview
1. Migration:
	1. `compose/compose.dev.yaml` - docker files + hot reload
	2. `compose/compose.prod.yaml` - registry images
2. `compose.dev.yaml`

```yaml
# Development Environment
# Usage: docker compose -f compose.dev.yaml up

include:
  - compose.observability.yaml
  - compose.app.yaml
  
services:
  frontend:
    build:
	  context: ../app-versions/code/frontend
	  dockerfile: Dockerfile.dev
	  target: development
	volumes:
	  # Mount source code for hot reload
	  - ../app-versions/code/frontend/src:/app/src:ro
	  - ../app-versions/code/frontend/tsconfig.json:/app/tsconfig.json:ro
	environment:
	  - NODE_ENV=development
	  - LOG_LEVEL=debug
	command: npm run dev
	
  worker:
    build:
	  context: ../app-versions/code/worker
	  dockerfile: Dockerfile.dev
	volumes:
	  # Mount source code for hot reload
	  - ../app-versions/code/worker/src:/app/src:ro
	  # Preserve translation models (large, slow to download)
	  - worker-models:/root/.local/share/argos-translate
	environment:
	  - PYTHONUNBUFFERED=1
	  - LOG_LEVEL=debug
	command: watchmedo auto-restart --directory=./src --pattern="*.py" --recursive -- python -m src.main
	
volumes:
  worker-models:
  
networks:
  observability:
    driver: bridge
	name: observability
  app:
    driver: bridge
	name: app
```

3. `compose.prod.yaml`

```yaml
# Production Environment
# Usage: docker compose -f compose.prod.yaml up

include:
  - compose.observability.yaml
  - compose.app.yaml
  
services:
  frontend:
    image: lmacademy/web-translator-frontend:v1.1.0
	
  worker:
    image: lmacademy/web-translator-worker:v1.1.0
	
networks:
  observability:
    driver: bridge
	name: observability
  app:
    driver: bridge
	name: app
```

4. Delete the `image: lmacademy/web-translator-<frontend|worker>:v1.1.0` from both `frontend` and `worker` services.
	1. Field will be set from within the `compose.prod.yaml`
	2. For `compose.dev.yaml`, we will use the `build` context instead of an image tag.
5. Start development environment:

```bash
# From the compose/ directory
docker compose -f compose.dev.yaml up --build
```

	1. `--build` - ensures development Dockerfiles are built (?)
6. Switch to production mode:

```bash
# Stop development environment
docker compose -f compose.dev.yaml down

# Start production environment (pulls images from registry)
docker compose -f compose.produ.yaml up -d
```

7. Install npm packages locally:

```
cd app-versions/code/frontend
npm ci

cd ../worker
curl -LsSf https://astral.sh/uv/install.sh | sh

# Install Python 3.14
uv python install 3.14

# Pin the project to Python 3.14
uv python pin 3.14

# Remove the existing virtual environment
rm -rf .venv

# Recreate the environment and install dependencies
uv sync --all-extras # This or the next one. venv automatically created

# Alternative
pip install -r requirements.txt # requires venv
```

### Hands-On Lab: Configuring the Development Environment
1. `compose.prod.yaml`

```yaml
# Main Docker Compose file for OpenTelemetry Course
# This file includes the observability stack and (soon) application
include:
  - compose.observability.yaml
  - compose.app.yaml

services:
  frontend:
    image: lmacademy/web-translator-frontend:v1.1.0
  worker:
    image: lmacademy/web-translator-worker:v1.1.0

# Shared networks for all services
networks:
  observability:
    driver: bridge
    name: observability
  app:
    driver: bridge
    name: app
```

2. `compose.app.yaml`

```yaml
# Application Services
# Translation app with frontend, worker, and Redis

services:
  redis:
    image: redis:8.6.0-alpine
    container_name: redis
    ports:
      - '6379:6379'
    networks:
      - app
    healthcheck:
      test: ['CMD', 'redis-cli', 'ping']
      interval: 5s
      timeout: 3s
      retries: 5
    restart: unless-stopped

  frontend:
    container_name: frontend
    ports:
      - '3001:3000'
    environment:
      - REDIS_HOST=redis
      - REDIS_PORT=6379
      - PORT=3000
      - LOG_LEVEL=info
      - SOURCE_LANGUAGE=en
    depends_on:
      redis:
        condition: service_healthy
    networks:
      - app
    restart: unless-stopped

  worker:
    container_name: worker
    environment:
      - REDIS_HOST=redis
      - REDIS_PORT=6379
      - LOG_LEVEL=info
      - SOURCE_LANGUAGE=en
    depends_on:
      redis:
        condition: service_healthy
    networks:
      - app
    restart: unless-stopped
```

3. Start:

```yaml
docker compose -f compose.prod.yaml up
```

4. `compose.dev.yaml`

```yaml
# Main Docker Compose file for OpenTelemetry Course
# This file includes the observability stack and (soon) application
include:
  - compose.observability.yaml
  - compose.app.yaml

services:
  frontend:
    build:
      context: ../app-versions/code/frontend
      dockerfile: Dockerfile.dev
      target: development
    volumes:
      # Mount source code for hot reload
      - ../app-versions/code/frontend/src:/app/src:ro
      - ../app-versions/code/frontend/tsconfig.json:/app/tsconfig.json:ro
    environment:
      - NODE_ENV=development
      - LOG_LEVEL=debug
    command: npm run dev
  worker:
    build:
      context: ../app-versions/code/worker
      dockerfile: Dockerfile.dev
    volumes:
      # Mount source code for hot reload
      - ../app-versions/code/worker/src:/app/src:ro
      # Preserve translation models (large, slow to download)
      - worker-models:/root/.local/share/argos-translate
    environment:
      - PYTHONUNBUFFERED=1
      - LOG_LEVEL=debug
    command: watchmedo auto-restart --directory=./src --pattern="*.py" --recursive -- python -m src.main

volumes:
  worker-models:

# Shared networks for all services
networks:
  observability:
    driver: bridge
    name: observability
  app:
    driver: bridge
    name: app
```

### The OpenTelemetry Collector
1. OpenTelemetry Collector
	1. Expore the use case and architecture of the OpenTelemetry collector
		1. Without collector
			1. Each service needs to connect to multiple backens (N x M problem)
		2. With a collector
			1. Each service connects to OTEL collector
			2. Backends pull data from the collector
2. Collector's architecture

```
OTel Collector

Receiver       Processors                                           Exporters

[OTLP gRPC] -> Metrics pipeline (memory_limiter -> batch -> ...) -> Prometheus
[OTLP HTTP] -> Traces Pipeline (memory_limiter -> batch -> ...)  -> otlp/tempo
[...]       -> Logs pipeline (memory_limiter -> batch -> ...)    -> otlphttp/loki
```

3. Examples:

```
processors:
  memory_limiter:
    check_interval: 1s
	limit_mib: 512 # drops data after this limit
	spike_limit_mib: 128 # solt limit. Backpressure is applied
  batch:
    timeout: 10s # flush every 10 seconds
	send_batch_size: 1024 # flush when this size is reached
	send_batch_max_size: 2048
```

4. Other processors:
	1. attributes
		1. to add, update, delete, or hash specific attributes of telemetry data
	2. filter
		1. To drop specific entries (by attributes or names)
	3. tail_sampling
		1. Samples after seeing full traces
	4. k8sattributes
		1. Enrich with pod, node, and namespace metadata
	5. transform
		1. To mutate telemetry data with OTTL expressions

### Hands-On Lab: Setting Up the OTel Collector - Lab Overview
1. `compose/otel-collector-config.yaml`

```yaml
receivers:
  otlp:
    protocols:
	  grpc:
	    endpoint: 0.0.0.0:4317
	  http:
	    endpoint: 0.0.0.0:4318
processors:
  batch:
    timeout: 10s
	send_batch_size: 1024
  memory_limiter:
    check_interval: 1s
	limit_mib: 512
exporters:
  otlp/tempo: # grpc
    endpoint: tempo:4317
    tls:
	  insecure: true
  prometheus:
    endpoint: 0.0.0.0:8889
  otlphttp/loki: # http
    endpoint: http://loki:3100/otlp
	tls:
	  insecure: true
service:
  pipelines:
    traces: # Pipeline
	  receivers: [otlp]
	  processors: [memory_limiter, batch]
	  exporters: [otlp/tempo]
	metrics:
	  receivers: [otlp]
	  processors: [memory_limiter, batch]
	  exporters: [prometheus]
	logs:
	  receivers: [otlp]
	  processors: [memory_limiter, batch]
	  exporters: [otlphttp/loki]
```

	1. OTLP receiver: accepts both gRPC (4317) and HTTP (4318) protocols
	2. Batch processor: groups telemetry data for efficient export (10s timeout or 1024 items)
	3. Memory limiter: Prevents out-of-memory errors by limiting to 512 MiB
	4. Exporters: Send data to Tempo (traces), Prometheus (metrics), and Loki (logs)
	5. Pipelines: Define separate data flows for traces, metrics, and logs
2. `compose/compose.observability.yaml`

```
services:
  otel-collector:
    image: otel/opentelemetry-collector-contrib:0.146.1
	container_name: otel-collector
	command: ['--config=/etc/otel-collector-config.yaml']
	volumes:
	  - ./otel-collector-config.yaml:/etc/otel-collector-config.yaml:ro
	ports:
	  - '4317:4317' # OTLP gRPC
	  - '4318:4318' # OTLP HTTP
	  - '8889:8889' # Prometheus metrics exporter
	networks:
	  - observability
	  - app
	restart: unless-stopped
	depends_on:
	  - prometheus
	  - loki
	  - tempo
	  
# ... existing services (prometheus, loki, tempo, grafana) ...
```

	1. Receives data from `app` and sends data to `observability`
3. `compose/prometheus.yaml` - add collector as a scrape target:

```yaml
scrape_configs:
  # ... existing jobs (prometheus, loki, tempo, grafana) ...
  
  - job_name: 'otel-collector'
    static_configs:
	  - targets: ['otel-collector:8889']
```

4. Ensure Tempo accepts OTLP: `compose/tempo-config.yaml` (receives data from OpenTelemetry collector)

```yaml
distributor:
  receivers:
    otlp:
	  protocols:
	    grpc:
		  endpoint: 0.0.0.0:4317
		http:
		  endpoint: 0.0.0.0:4318
```

5. Start the complete observability stack:

```
cd compose/
docker compose -f compose.dev.yaml down # Stop existing services
docker compose -f compose.dev.yaml up -d # start with Collector included
```

6. Wait for all services to start. Monitor the startup with:

```
docker compose -f compose.dev.yaml logs -f otel-collector
```

7. Verify collector is running:

```
# Check all services are up
docker compose -f compose.dev.yaml ps

# Check Collector logs - look for success messages
docker compose -f compose.dev.yaml logs otel-collector | tail -30

# You should see a message like:
# "Everything is ready. Begin running and processing data."
```

8. Test that collector endpoints are accessible:

```
# Test HTTP endpoint (should return 404, which confirms it's listening)
curl -i http://localhost:4318/

# Check Collector's own metrics are exposed
curl -s http://localhost:8889/metrics | head -20
```

### Hands-On Lab: Deploying the OTel Collector
### Hands-On Lab: Testing the OTel Collector - Lab Overview
1. Test trace to collector:

```bash
curl -X POST http://localhost:4318/v1/traces \
  -H "Content-Type: application/json" \
  -d '{
    "resourceSpans": [{
	  "resource": {
	    "attributes": [
		  {"key": "service_name", "value": {"stringValue": "test-app"}}
		]
	  },
	  "scopeSpans": [{
	    "scope": {"name": "test-instrumentation"},
		"spans": [{
		  "traceId": "'$(openssl rand -hex 16)'",
		  "spandId": "'$(openssl rand -hex 8)'",
		  "name": "test-operation",
		  "kind": 1,
		  "startTimeUnixNano": "'$(date +%s)000000000'",
		  "endTimeUnixNano": "'$(( $(date +%s) + 1 ))000000000'",
		  "status": {"code": 0}
		}]
	  }]
	}]
  }'
```

2. `http://localhost:3000`

```
Go to Explore -> Select Tempo
Click Search tab -> Run query
Find your trace with service.name = "test-app"
Click on it to see the span details
```

3. Check collector metrics:

```
http://localhost:9090
```

```
# Collector is up
up{job="otel-collector"}

# Spans were received
otelcol_receiver_accepted_spans

# Spans were sent to Tempo
otelcol_exporter_sent_spans{exporter="otlp/tempo"}

# No errors
otelcol_receiver_refused_spans
otelcol_exporter_send_failed_spans
```

### Hands-On Lab: Verifying End-to-End Data Flow
1. AI:

```
I have this CURL request, please make it send 5 traces instead of a single one

```
curl -X POST http://localhost:4318/v1/traces \
  -H "Content-Type: application/json" \
  -d '{
    "resourceSpans": [{
      "resource": {
        "attributes": [
          {"key": "service.name", "value": {"stringValue": "test-app"}}
        ]
      },
      "scopeSpans": [{
        "scope": {"name": "test-instrumentation"},
        "spans": [{
          "traceId": "'$(openssl rand -hex 16)'",
          "spanId": "'$(openssl rand -hex 8)'",
          "name": "test-operation",
          "kind": 1,
          "startTimeUnixNano": "'$(date +%s)000000000'",
          "endTimeUnixNano": "'$(( $(date +%s) + 1 ))000000000'",
          "status": {"code": 0}
        }]
      }]
    }]
  }'
```
```

```
curl -X POST http://localhost:4318/v1/traces \
  -H "Content-Type: application/json" \
  -d '{
    "resourceSpans": [{
      "resource": {
        "attributes": [
          {"key": "service.name", "value": {"stringValue": "test-app"}}
        ]
      },
      "scopeSpans": [{
        "scope": {"name": "test-instrumentation"},
        "spans": [
          {
            "traceId": "'$(openssl rand -hex 16)'",
            "spanId": "'$(openssl rand -hex 8)'",
            "name": "test-operation-1",
            "kind": 1,
            "startTimeUnixNano": "'$(date +%s)000000000'",
            "endTimeUnixNano": "'$(date +%s)000000000'",
            "status": {"code": 0}
          },
          {
            "traceId": "'$(openssl rand -hex 16)'",
            "spanId": "'$(openssl rand -hex 8)'",
            "name": "test-operation-2",
            "kind": 1,
            "startTimeUnixNano": "'$(date +%s)000000000'",
            "endTimeUnixNano": "'$(date +%s)000000000'",
            "status": {"code": 0}
          },
          {
            "traceId": "'$(openssl rand -hex 16)'",
            "spanId": "'$(openssl rand -hex 8)'",
            "name": "test-operation-3",
            "kind": 1,
            "startTimeUnixNano": "'$(date +%s)000000000'",
            "endTimeUnixNano": "'$(date +%s)000000000'",
            "status": {"code": 0}
          },
          {
            "traceId": "'$(openssl rand -hex 16)'",
            "spanId": "'$(openssl rand -hex 8)'",
            "name": "test-operation-4",
            "kind": 1,
            "startTimeUnixNano": "'$(date +%s)000000000'",
            "endTimeUnixNano": "'$(date +%s)000000000'",
            "status": {"code": 0}
          },
          {
            "traceId": "'$(openssl rand -hex 16)'",
            "spanId": "'$(openssl rand -hex 8)'",
            "name": "test-operation-5",
            "kind": 1,
            "startTimeUnixNano": "'$(date +%s)000000000'",
            "endTimeUnixNano": "'$(date +%s)000000000'",
            "status": {"code": 0}
          }
        ]
      }]
    }]
  }'
```

```
docker compose -f compose.dev.yaml logs otel-collector
```

### Hands-On Lab: Monitoring the OTel Collector
1. To expose internal metrics of OTel Collector (not by otlp)
2. `otel-collector-config.yaml`

```
service:
  telemetry:
    metrics:
	  readers:
	    - pull: 
	        exporter:
		      prometheus:
		        host: "0.0.0.0"
			    port: 8888
```

3. `prometheus.yaml`

```
scrape_configs:
  ...
  - job_name: 'otel-collector-internal'
    static_configs:
	  - targets: ['otel-collector:8888']
```

4. `compose.observability.yaml`

```
services:
  ...
  otel-collector:
    ...
	ports:
	  ...
	  '8888:8888' # OTel Internal metrics
```

5. Bring up the services:

```
docker compose -f compose.dev.yaml up --build
```

```
curl -X POST http://localhost:4318/v1/traces \
  -H "Content-Type: application/json" \
  -d '{
    "resourceSpans": [{
      "resource": {
        "attributes": [
          {"key": "service.name", "value": {"stringValue": "test-app"}}
        ]
      },
      "scopeSpans": [{
        "scope": {"name": "test-instrumentation"},
        "spans": [
          {
            "traceId": "'$(openssl rand -hex 16)'",
            "spanId": "'$(openssl rand -hex 8)'",
            "name": "test-operation-1",
            "kind": 1,
            "startTimeUnixNano": "'$(date +%s)000000000'",
            "endTimeUnixNano": "'$(date +%s)000000000'",
            "status": {"code": 0}
          },
          {
            "traceId": "'$(openssl rand -hex 16)'",
            "spanId": "'$(openssl rand -hex 8)'",
            "name": "test-operation-2",
            "kind": 1,
            "startTimeUnixNano": "'$(date +%s)000000000'",
            "endTimeUnixNano": "'$(date +%s)000000000'",
            "status": {"code": 0}
          },
          {
            "traceId": "'$(openssl rand -hex 16)'",
            "spanId": "'$(openssl rand -hex 8)'",
            "name": "test-operation-3",
            "kind": 1,
            "startTimeUnixNano": "'$(date +%s)000000000'",
            "endTimeUnixNano": "'$(date +%s)000000000'",
            "status": {"code": 0}
          },
          {
            "traceId": "'$(openssl rand -hex 16)'",
            "spanId": "'$(openssl rand -hex 8)'",
            "name": "test-operation-4",
            "kind": 1,
            "startTimeUnixNano": "'$(date +%s)000000000'",
            "endTimeUnixNano": "'$(date +%s)000000000'",
            "status": {"code": 0}
          },
          {
            "traceId": "'$(openssl rand -hex 16)'",
            "spanId": "'$(openssl rand -hex 8)'",
            "name": "test-operation-5",
            "kind": 1,
            "startTimeUnixNano": "'$(date +%s)000000000'",
            "endTimeUnixNano": "'$(date +%s)000000000'",
            "status": {"code": 0}
          }
        ]
      }]
    }]
  }'
```

```
curl -is http://localhost:8888/metrics
```

6. Prometheus:
	1. Explore > Prometheus > Builder
		1. `otelcol_receiver_accepted_spans_total`
		2. `otelcol_exporter_sent_spans_total`
	2. Prometheus targets: otel-collector
		1. Needs restart

## Section 7: Instrumenting Metrics with OpenTelemetry
### OpenTelemetry Metrics Architecture
1. Metrics Instrumentation
	1. Understand the role of the OpenTelemetry SDK and instrumentation techniques
		1. End-to-end data flow
		
		```
		translation.ts					OTel Meter    			PeriodicExporting MetricReader    						Collector   					Prometheus
		      |							|
			  - counter.add(1, ...) ->	In memory aggregation
															<- Export tick (10s) -
															- Cumulative metrics ->
																						- POST /v1/metrics (OLTP JSON)
																															<- Scrape :8889/metrics -
																															- Prometheus text metrics ->
		```
		
			1. `counter.add(1, ...)` - generates metrics
				1. `@opentelemetry/api` - package
2. `instrumentation.ts`

```
const sdk = new NodeSDK({
  serviceName: 'translation-frontend',
  metricReader: new PeriodicExportingMetricReader({
    exporter: new OTLPMetricExporter({
	  url: 'http://otel-collector:4318/v1/metrics',
	}),
	exportIntervalMillis: 10000, // push every 10 s
  }),
  instrumentations: [getNodeAutoInstrumentations()],
})
```

	1. Auto-Instrumentation
		1. `http_server_duration_milliseconds_count{...}`
		2. `nodejs_eventloop_utilization_ratio{...}`
		3. ...
3. `metrics.ts` - manual instrumentation

```
import { metrics } from '@opentelemetry/api';

const meter = metrics.getMeter('translation-frontend', '1.0.0');

export const translationRequestsCounter = meter.createCounter(
  'translation.requests.total',
  { description: 'Total translation requests' },
);
```

4. `translation.ts` - using the counter

```typescript
import { translationRequestsCounter } from '../metrics';

router.post('/', async (req, res) => {
  ...
  translationRequestsCounter.add(1, {
    status: 'success',
	language_count: targetLanguages.length.toString(),
  });
```

### Hands-On Lab: Auto Instrumentation for Metrics - Lab Overview
1. Auto-instrumentations
2. Intall OpenTelemetry Packages

```
cd app-versions/code/frontend
npm install --save \
  @opentelemetry/sdk-node@0.212.0 \
  @opentelemetry/auto-instrumentations-node@0.70.1 \
  @opentelemetry/exporter-metrics-otlp-http@0.212.0
```

3. Construct `src/instrumentation.ts`

```
import { NodeSDK } from "@opentelemetry/sdk-node";
import { getNodeAutoInstrumentations } from "@opentelemetry/auto-instrumentations-node";
import { OTLPMetricExporter } from "@opentelemetry/exporter-metrics-otlp-http";
import { PeriodicExportingMetricReader } from '@opentelemetry/sdk-metrics';

const sdk = new NodeSDK({
  serviceName: 'translation-frontend',
  metricReader: new PeriodicExportingMetricReader({
    exporter: new OTLPMetricExporter({
      url: 'http://otel-collector:4318/v1/metrics',
    }),
    exportIntervalMillis: 10000,
  }),
  instrumentations: [getNodeAutoInstrumentations()]
});

sdk.start();
```

4. Update `src/index.ts`

```
import './instrumentation';
import express from 'express';
// ... rest of imports
```

5. Deploy:

```
cd compose/
docker compose -f compose.dev.yaml up --build
```

	1. Rebuilds images with the changes
6. Generate traffic:

```
curl -X POST http://localhost:3001/api/translate \
  -H "Content-Type: application/json" \
  -d '{"text": "Hello world", "targetLanguages": ["es", "fr"]}'
```

```
curl -is http://localhost:8889/metrics
```

7. Verify in Prometheus: `http://localhost:9090`

```
http_server_duration_milliseconds_count{exported_job="translation-frontend"}
rate(http_server_duration_milliseconds_count{exported_job="translation-frontend"}[1m])
nodejs_eventloop_utilization_ratio{exported_job="translation-frontend"}
```

### Hands-On Lab: Applying Auto Instrumentation for Metrics
1. Execute the commands
2. Prometheus:
	1. Query

### Hands-On Lab: Manual Instrumentation for Metrics - Lab Overview
1. Manual instrumentation:
2. `src/metrics.ts`

```typescript
import { metrics } from '@opentelemetry/api';

const meter = metrics.getMeter('translation-frontend', '1.0.0');

export const translationRequestsCounter = meter.createCounter(
  'translation.requests.total',
  {
    description: 'Total translation requests'
  },
);

export const jobsEnqueuedCounter = meter.createCounter(
  'translation.jobs.enqueued.total',
  {
    description: 'Total translation jobs enqueued'
  },
);

export const requestDuration = meter.createHistogram(
  'translation.request.duration',
  {
    description: 'Translation request processing time',
    unit: 'ms'
  },
);

export const validationErrorsCounter = meter.createCounter(
  'translation.validation.errors.total',
  {
    description: 'Translation validation errors'
  },
);
```

3. `src/routes/translation.ts`

```
import { Router } from 'express';
import { v4 as uuidv4 } from 'uuid';
import type { Request, Response } from 'express';
import type { QueueService } from '../services/queue.js';
import type { SSEManager } from '../services/sse.js';
import type {
  TranslateRequest,
  TranslateResponse,
  SessionResponse,
  TranslationJob,
  JobStatus,
  TranslationSession,
} from '../types.js';
import { SUPPORTED_LANGUAGES } from '../types.js';
import {
  translationRequestsCounter,
  jobsEnqueuedCounter,
  requestDuration,
  validationErrorsCounter,
} from '../metrics';

export interface TranslationRouterDeps {
  queueService: QueueService;
  sseManager: SSEManager;
}

export function createTranslationRouter(deps: TranslationRouterDeps): Router {
  const router = Router();
  const { queueService, sseManager } = deps;

  // POST /api/translate - Submit translation request
  router.post('/', async (req: Request, res: Response) => {
    const start = Date.now();
    
    try {
      const body = req.body as TranslateRequest;

      // Validate text
      if (!body.text || typeof body.text !== 'string' || !body.text.trim()) {
        validationErrorsCounter.add(1, { 
          error_type: 'empty_text'
        });
        res.status(400).json({
          error: 'Text is required',
          details: 'Text must be a non-empty string',
        });
        return;
      }

      // Validate targetLanguages
      if (
        !Array.isArray(body.targetLanguages) ||
        body.targetLanguages.length === 0
      ) {
        validationErrorsCounter.add(1, {
          error_type: 'invalid_languages'
        });
        res.status(400).json({
          error: 'At least one target language is required',
          details: 'targetLanguages must be a non-empty array',
        });
        return;
      }

      // Check max languages
      if (body.targetLanguages.length > 3) {
        validationErrorsCounter.add(1, {
          error_type: 'invalid_languages'
        });
        res.status(400).json({
          error: 'Maximum 3 target languages allowed',
          details: `You requested ${body.targetLanguages.length} languages`,
        });
        return;
      }

      // Validate each language
      const unsupportedLanguages = body.targetLanguages.filter(
        (lang) => !SUPPORTED_LANGUAGES.includes(lang as any),
      );

      if (unsupportedLanguages.length > 0) {
        validationErrorsCounter.add(1, {
          error_type: 'invalid_languages'
        });
        res.status(400).json({
          error: `Unsupported language: ${unsupportedLanguages.join(', ')}`,
          supportedLanguages: [...SUPPORTED_LANGUAGES],
        });
        return;
      }

      // Track successful request
      translationRequestsCounter.add(1, {
        status: 'success',
        language_count: body.targetLanguages.length.toString(),
      });

      // Create session
      const sessionId = uuidv4();
      const jobs = new Map<string, JobStatus>();

      // Create and enqueue jobs
      const jobsList: TranslationJob[] = [];

      for (const targetLanguage of body.targetLanguages) {
        const jobId = uuidv4();
        const job: TranslationJob = {
          jobId,
          sessionId,
          text: body.text,
          sourceLanguage: 'en',
          targetLanguage,
          createdAt: new Date().toISOString(),
        };

        jobsList.push(job);
        jobs.set(targetLanguage, { status: 'queued' });

        // Enqueue job
        await queueService.enqueueJob(job);

        
        // Track each job enqueued
        jobsEnqueuedCounter.add(1, {
          target_language: targetLanguage
        });

        // Track request duration
        requestDuration.record(Date.now() - start, {
          target_language_count: body.targetLanguages.length.toString(),
        });
      }

      // Save session
      const session: TranslationSession = {
        sessionId,
        text: body.text,
        sourceLanguage: 'en',
        status: 'queued',
        jobs,
      };

      await queueService.saveSession(session);

      // Return response
      const response: TranslateResponse = {
        sessionId,
        status: 'queued',
        jobs: jobsList.map((job) => ({
          jobId: job.jobId,
          targetLanguage: job.targetLanguage,
          status: 'queued',
        })),
      };

      console.log(
        `Created translation session ${sessionId} with ${jobsList.length} jobs`,
      );
      res.status(201).json(response);
    } catch (error) {
      console.error('Error creating translation session:', error);
      res.status(500).json({
        error: 'Internal server error',
        details: error instanceof Error ? error.message : 'Unknown error',
      });
    }
  });

  // GET /api/translate/:sessionId - Get session status
  router.get('/:sessionId', async (req: Request, res: Response) => {
    try {
      const { sessionId } = req.params as unknown & { sessionId: string };

      const session = await queueService.getSession(sessionId);

      if (!session) {
        res.status(404).json({ error: 'Session not found' });
        return;
      }

      // Convert Map to object for JSON response
      const translations: Record<string, JobStatus> = {};
      for (const [lang, jobStatus] of session.jobs.entries()) {
        translations[lang] = jobStatus;
      }

      const response: SessionResponse = {
        sessionId: session.sessionId,
        text: session.text,
        status: session.status,
        translations,
      };

      res.json(response);
    } catch (error) {
      console.error('Error fetching session:', error);
      res.status(500).json({
        error: 'Internal server error',
        details: error instanceof Error ? error.message : 'Unknown error',
      });
    }
  });

  // GET /api/translate/:sessionId/events - SSE endpoint
  router.get('/:sessionId/events', async (req: Request, res: Response) => {
    try {
      const { sessionId } = req.params as unknown & { sessionId: string };

      // Verify session exists
      const session = await queueService.getSession(sessionId);

      if (!session) {
        res.status(404).json({ error: 'Session not found' });
        return;
      }

      // Add SSE connection
      sseManager.addConnection(sessionId, res);

      console.log(`Client connected to SSE for session ${sessionId}`);
    } catch (error) {
      console.error('Error establishing SSE connection:', error);
      res.status(500).json({
        error: 'Internal server error',
        details: error instanceof Error ? error.message : 'Unknown error',
      });
    }
  });

  return router;
}
```

4. Deploy:

```
cd compose/
docker compose -f compose.dev.yaml up --build frontend
```

5. Requests:

```
# Successful requests with different language combinations
curl -X POST http://localhost:3001/api/translate \
  -H "Content-Type: application/json" \
  -d '{"text": "Hello", "targetLanguages": ["es"]}'
  
curl -X POST http://localhost:3001/api/translate \
  -H "Content-Type: application/json" \
  -d '{"text": "Hello", "targetLanguages": ["es", "fr", "de"]}'
  
# Validation errors
curl -X POST http://localhost:3001/api/translate \
  -H "Content-Type: application/json" \
  -d '{"text": "", "targetLanguages": ["es", "fr", "de"]}'
```

6. Verify in Prometheus:

```
translation_requests_total # Request count by language combination
rate(translation_requests_total[5m]) # Request rate
translation_jobs_enqueued_total{target_langauge="es"} # Jobs per langauge
histogram_quantile(0.95, rate(translation_request_duration_bucket[5m])) # 95th percentile latency
translation_validation_errors_total # validation failures by error type
```

### Hands-On Lab: Constructing Custom Business Metrics
1. `translation.requests.total` - replaced with `_`s
	1. `translation` - namespace
2. `error_type` - label
	1. Keep the cardinality bounded (or else it might slow down the metrics backend)

### Hands-On Lab: Exploring Custom Metrics in Prometheus
1. Run `curl` requests
2. Prometheus:
	1. `translation_requests_total`
	2. `sum(translation_requests_total)`

## Section 8: Instrumenting Traces with OpenTelemetry
### OpenTelemetry Traces Architecture
1. Understand the role of the OpenTelemetry SDK and instrumentation techniques
2. End-to-end data flow:

```
Client				Node HTTP		Route Handler						OTel SDK		Collector						Tempo
- POST /translate ->
					- Start span POST /translate -------------------->
					- Call handler ->
									  startActiveSpan
									- construct_translatioN_job ----->
									  startActiveSpan
									- enqueue_jobs ------------------>
									- End enqueue_jobs -------------->
									- End construct_translatioN_job ->
					- End span POST /translate ---------------------->
																		- Export spans
																		  (OTLP HTTP) ->
																						- Forward via OTLP Exporter ->
																	
```

3. `instrumentation.ts`

```
const sdk = new NodeSDK({
  ...
  traceExporter: new OTLPTraceExporter({
    url: 'http://otel-collector:4318/v1/traces',
  }),
  ...
  instrumentations: [getNodeAutoInstrumentations()],
});

sdk.start();
```

4. Manual instrumentation: `translation.ts`

```
// src/routes/translation.ts
const tracer = trace.getTracer("translation-frontend", '1.0.0');

router.post('/', async (req, res) => {
  return tracer.startActiveSpan("<span_name>", async (span) => {
    try {
	  // Business logic here
	  span.setAttribute('translation.text_length', body.text.length);
	  span.setAttribute('translation.target_languages', langs.join(','));
	  
	  // ... do work ...
	  
	  span.setStatus({ code: SpanStatusCode.OK });
	} catch (err) {
	  span.recordException(err as Error);
	  span.setStatus({
	    code: SpanStatusCode.ERROR,
		message: String(err)
	  });
	  throw err;
	} finally {
	  span.end(); // always end the span
	}
  });
});
```

	1. Manual instrumentation:
		1. Calling `startActiveSpan` automatically sets the new span as a child of the currently active span, so no need to pass context manually

### Hands-On Lab: Auto Instrumentation for Traces - Lab Overview
1. `src/instrumentation.ts`
2. `@opentelemetry/exporter-trace-otlp-http`

```
cd app-versions/code/frontend
npm install --save-exact \
  @OpenTelemetry/exporter-trace-otlp-http@0.212.0
```

3. `src/instrumentation.ts`

```
import { NodeSDK } from '@opentelemetry/sdk-node';
import { getNodeAutoInstrumentations } from '@opentelemetry/auto-instrumentations-node';
import { OTLPMetricExporter } from '@opentelemetry/exporter-metrics-otlp-http';
import { PeriodicExportingMetricReader } from '@opentelemetry/sdk-metrics';
import { OTLPTraceExporter } from '@opentelemetry/exporter-trace-otlp-http';

const sdk = new NodeSDK({
  serviceName: 'translation-frontend',
  traceExporter: new OTLPTraceExporter({
    url: 'http://otel-collector:4318/v1/traces',
  }),
  metricReader: new PeriodicExportingMetricReader({
    exporter: new OTLPMetricExporter({
      url: 'http://otel-collector:4318/v1/metrics',
    }),
    exportIntervalMillis: 10000,
  }),
  instrumentations: [getNodeAutoInstrumentations()]
});

sdk.start();
```

4. Deploy:

```
cd compose/
docker compose -f compose.dev.yaml up --build
```

5. Generate traffic:

```
curl -X POST http://localhost:3001/api/translate \
 -H "Content-Type: application/json" \
 -d '{"text": "Hello world", "targetLanguages": ["es", "fr"]}'
```

6. Verify in Grafana Tempo: http://localhost:3000 -> Explore -> Tempo
	1. Search: `translation-frontend`
	2. Expect span hierarchy:
	
	```
	POST /api/translate (HTTP span)
	 +- Redis LPUSH (job enqueue for "es")
	 +- Redis LPUSH (job enqueue for "fr")
	 +- Redis HSET (session data)
	```
	
7. Examine Span Attributes: HTTP span

```
http.request.method: POST
http.route: /api/translate
http.response.status_code: 200
server.address, server.port
```

8. Redis spans:

```
db.system: redis
db.operation: LPUSH or HSET
db.statement
```

### Hands-On Lab: Applying Auto Instrumentation for Traces
1. Grafana
	1. Tempo
		1. Search
			1. Service Name: `translation-frontend`
				1. Run query
				2. Select a trace
2. Auto-tracing is technical
	1. No business-related information

### Hands-On Lab: Manual Instrumentation for Traces - Lab Overview
1. `src/routes/translation.ts`
	1. Trace logic is mixed with the business logic
		1. Alternative solution:
			1. AOP
			2. Wrapper functions
			3. Decorators
2. Deploy:

```
cd compose/
docker compose -f compose.dev.yaml up --build
```

5. Generate traffic:

```
curl -X POST http://localhost:3001/api/translate \
 -H "Content-Type: application/json" \
 -d '{"text": "Hello world", "targetLanguages": ["es", "fr"]}'
```

6. Verify in Grafana Tempo

```
POST /api/translate (auto)
  + construct_translation_session (manual)
    + validate_request (manual)
	+ enqueue_translation_jobs (manual)
	  + Redis LPUSH (auto) - es
	  + Redis LPUSH (auto) - fr
	  + Redis LPUSH (auto) - de
```

7. Examine custom attributes: Click on `construct_translation_session`

```
translation.text_length
translation.target_language_count
translation.target_languages
translation.session_id
```

8. Click on `enqueue_translation_jobs`

```
translation.jobs_count
```

### Hands-On Lab: Constructing Custom Spans
1. Tracer: `tracer.ts`

```
import { trace } from "@opentelemetry/api";

export const tracer = trace.getTracer('translation-frontend', '1.0.0');
```

2. `src/routes/translation.ts`

```

```

### Hands-On Lab: Fixing a Bug in Instrumented Code
### Hands-On Lab: Refactoring Instrumentation Code

## Section 9: Instrumenting Logs with OpenTelemetry
### OpenTelemetry Logs Architecture
### Hands-On Lab: Auto Instrumentation for Logs - Lab Overview
### Hands-On Lab: Applying Auto Instrumentation for Logs
### Hands-On Lab: Teting Log Instrumentation
### Hands-On Lab: Manual Instrumentation for Logs - Lab Overview
### Hands-on Lab: Adding Manual Log Statements
### Hands-On Lab: Log-Trace Correlations in Grafana - Lab Overview
### Hands-On Lab: Configuring Log-Trace Correlations
### Hands-On Lab: Externalizing Configuration - Lab
### Hands-On Lab: Applying Configuration Refactoring

## Section 10: Instrumenting the Worker Service
### Section Introduction
### Hands-On Lab: Worker Metrics Auto-Instrumentation - Lab Overview
### Hands-On Lab: Applying Worker Metrics Auto-Instrumentation
### Hands-On Lab: Worker Logs Auto-Instrumentation - Lab Overview
### Hands-On Lab: Applying Worker Logs Auto-Instrumentation
### Hands-On Lab: Worker Traces Auto-Instrumentation - Lab Overview
### Hands-On Lab: Applying Worker Traces Auto-Instrumentation

## Section 11: Distributed Context Propagation
### Context Propagation Concepts
### Hands-On Lab: Frontend-to-Worker Propagation - Lab Overview
### Hands-On Lab: Injecting Trace Context in the Frontend
### Hands-On Lab: Extracting Trace Context in the Worker
### Hands-On Lab: Testing Distributed Trace Connectivity
### Hands-On Lab: Worker-to-Frontend Propagation - Lab Overview
### Hands-On Lab: Completing Bidirectional Propagation

## Section 12: Advanced Worker Instrumentation
### Hands-On Lab: Worker Custom Metrics - Lab Overview
### Hands-On Lab: Implementing Worker Custom Metrics
### Hands-On Lab: Testing Worker Custom Metrics
### Hands-On Lab: Worker Custom Spans - Lab Overview
### Hands-On Lab: Implementing Worker Custom Spans
### Hands-On Lab: Redis Exporter Pattern - Lab Overview
### Hands-On Lab: Deploying the Redis Exporter
### Hands-On Lab: Environment-Driven Configuration - Lab Overview
### Hands-On Lab: Applying Environment-Driven Configuration
### Hands-On Lab: Structured Logging for the Worker - Lab Overview
### Hands-On Lab: Migrating Worker Logs to Structured Format
### Hands-On Lab: Testing Structured Log Output

## Section 13: Deploying to Kubernetes
### Section Introduction
### Hands-On Lab: Application Kubernetes Manifests - Lab Overview
### Hands-On Lab: Constructing Application Manifests
### Hands-On Lab: Observability Stack Manifests - Lab Overview
### Hands-On Lab: OTel Collector Kubernetes Manifest
### Hands-on Lab: Observability Backends Manifests
### Hands-On Lab: Kube State Metrics Menifests
### Hands-On Lab: Auditing Manifests with AI
### Hands-On Lab: Setting up Kustomize - Lab Overview
### Hands-On Lab: Implementing Kustomize Configuration
### Hands-On Lab: Verifying Kubernetes Manifests - Lab Overview
### Hands-On Lab: Validating Generated Manifests
### Hands-On Lab: Deploying to Kubernetes - Lab Overview
### Hands-On Lab: Applying Manifests to the Cluster
### Hands-On Lab: Fixing Telemetry Collection Bugs
### Hands-On Lab: Verifying Telemetry Data - Lab Overview
### Hands-On Lab: Verifying Telemetry End to End

## Section 14: Conclusion
### Congratulations!
### BONUS: Course Discounts!