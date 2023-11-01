# The Twelve-Factor App #
## Introduction ##
1. Software delivery patterns:
	1. web-apps
	2. software-as-a-service
2. Purpose of the twelve-factor app:
	1. **Methodology for building software-as-a-service apps**
	2. It enables the following:
		1. Use **declarative** formats for setup automation
			1. To minimize time and cost for new developers joining the project
		2. Have a **clean contract** with the underlying OS
			1. Offers **maximum portability** between execution environments
		3. Are suitable for **deployment** on modern **cloud platforms**
			1. Obviates the need for server and system adiministration
		4. **Minimize divergence** between development and production
			1. Enables **continuous deployment** for maximum agility
		5. And can **scale up** without significant changes to tooling, architecture, or development practices
3. Applicable to apps written in any programming language
4. Applicable to apps that use any combination of backing services
	1. Backing services:
		1. Database
		2. Queue
		3. Memory cache
		4. ...

## Background ##
1. The document is based on experience and observations on software-as-a-service apps
2. The methodology is based on triangulation of ideal practices for app development paying attention to:
	1. The dynamics of the organic growth of an app over time
	2. The dynamics of collaboration between developers working on the app's codebase
	3. Avoiding the cost of software erosion
		1. [Avoiding the cost of software erosion](http://blog.heroku.com/archives/2011/6/28/the_new_heroku_4_erosion_resistance_explicit_contracts/)
3. Provide a shared vocabulary for discussing some systemic problems
4. Offer a broad conceptual solutions to the problems with accompanying terminology
	1. Inspired by:
		1. Patterns of Enterprise Application Architecture
		2. Refactoring

## Who Should Read This Document? ##
1. **Any developer building applications which run as a service**
2. **Ops engineers who deploy or manage such applications**

## The Twelve Factors ##
### Codebase ###
1. **One codebase tracked in revision control, many deploys**
2. A twelve-factor app is **always tracked in a version control system**
	1. Options:
		1. Git
		2. Mercurial
		3. Subversion
	2. A copy of the revision tracking database is called a code repository (code repo OR repo)
3. **Codebase**: 
	1. A single repo (in a centralized revision control system like Subversion)
	2. Set of repos who share a root commit (in a decentralized revision control system like Git)
4. **There is always a one-to-one correlation between codebase and the app**
	1. If there are multiple code-bases, it is not an app
		1. It is a distributed system
			1. Each component in a distributed system is an app
			2. Each component can individually comply with twelve-factor
	2. **Multiple apps sharing the same code is a violation of twelve-factor**
		1. Solution: **Factor shared code into libraries which can be included through the** [dependency manager](https://12factor.net/dependencies)
5. There is only one codebase per app, but **there will be many deploys of the app**
	1. **deploy is a running instance of the app**
		1. Typically:
			1. A production site
			2. One or more staging sites
			3. A copy of the app running in every developer's development environment
		2. Codebase is the same across all deploys
			1. **Different versions may be active in each deploy**
				1. Example: Developer has commits not yet deployed to staging
					1. Staging has some commits not yet deployed to production
			2. They are deploys of the same app

### Dependencies ###
1. **Explicitly declare and isolate dependencies**
2. Most programming languages offer a packaging system for distributing support libraries
	1. CPAN for Perl
	2. Rubygems for Ruby
3. **Site packages**: Libraries installed through a packaging system can be installed system-wide
4. **Vendoring or Bundling**: Libraries scoped into the directory containing the app
5. **A twelve-factor app never relies on implicit existence of system-wide packages**
	1. It **declares all dependencies, completely and exactly, via a dependency declaration manifest**
	2. It **uses a dependency isolation tool during execution to ensure that no implicit dependencies "leak in" from the surrounding system**
6. Full and explicit dependency specification is applied uniformly to both production and development
7. Examples:
	1. Ruby:
		1. Bundler:
			1. Offers `Gemfile` manifest format for dependency declaration
			2. Offers `bundle exec` for dependency isolation
	2. Python:
		1. Pip: used for dependency declaration
		2. Virtualenv: For isolation
	3. C:
		1. Autoconf: for dependency declaration
		2. Static linking: for dependency isolation
8. **Dependency declaration & isolation must always be used together**
	1. Only one or the other is not sufficient to satisfy twelve-factor
9. Benefits of explicit dependency declaration:
	1. Simplifies setup for developers new to the app:
		1. New developer can check out the app's codebase onto their development machine
		2. The codebase requires only language runtime and dependency manager installed as pre-requisites
		3. They can run the app's code with a deterministic build command
			1. Example:
				1. Ruby/Bundler: `bundle install`
				2. Clojure/Leiningen: `lein deps`
10. Twelve-factor apps do not rely on implicit existence of any **system tools**
	1. Exmaple: Shelling out to ImageMagick
	2. Example: `curl`
	3. The tools may or may not be available in the system
	4. The version of the tools in the system may not be compatible with the app
	5. What if app needs to shell out to a system tool?
		1. Solution: **Tool is vendored into the app**

### Config ###
1. **Store config in the environment**
2. An **app's config is everything that is likely to vary between deploys**
	1. Deploys:
		1. Staging
		2. Production
		3. Developer environments
		4. ...
	2. This includes:
		1. **Resource handles to the database, memcached, and other backing services**
			1. [Backing services](https://12factor.net/backing-services)
		2. **Credentials to external services such as Amazon S3 or Twitter**
		3. **Per-deploy values**
			1. **Such as the canonical hostname for the deploy**
3. Storing config as constants in the code is a violation of twelve-factor
	1. Solution: **Strict separation of config from code**
		1. Config varies substantially across deploys, code does not
	2. **Litmus test for whether an app has all config correctly factored out of the code**
		1. Whether the code could be made open source at any moment, without compromising any credentials
4. The definition of "config" does not include internal application config
	1. Example: `config/routes.rb` in Rails
		1. How code modules are connected in Spring
			1. [http://docs.spring.io/spring/docs/current/spring-framework-reference/html/beans.html](http://docs.spring.io/spring/docs/current/spring-framework-reference/html/beans.html)
	2. Why?
		1. This type of config does not vary between deploys
			1. It can be done in the code
5. An approach to config:
	1. Use config files which are not checked into revision control
		1. `config/database.yml` in Rails
	2. Pros: An improvement over using constants checked into the code repo
	3. Cons: 
		1. Easy to mistakenly checkin a config file to the repo
		2. A tendancy for config files to be scattered about in different places and different formats
			1. Makes it harder to see and manage all config in one place
		3. The config files tend to be language- or framework-specific
6. **A twelve-factor app stores config in environment variables**
	1. Pros: 
		1. Env variables are easy to change between deploys without changing any code
		2. There is little chance of them being checked into code repo accidentally
		3. They are language- and OS-agnostic standard
			1. Unline custom config files
			2. Unlike other config mechanisms such as Java System Properties
7. Grouping:
	1. Apps might batch config into named groups (called "environments") named after specific deploys (`development`, `test`, and `production` environments in Rails)
	2. Cons:
		1. Does not scale cleanly
			1. If more deploys of the app are created, new environment names are needed (`staging`, `qa`, ...)
			2. As the project grows, developers may add their own special environments like (`joes-staging`)
				1. The above results in combinatorial explosion of config
					1. Makes managing deploys of app very brittle
8. **In twelve-factor app, env vars are granular controls, each fully orthogonal to other env vars**
	1. The env vars are never grouped together as "environments"
		1. They must be managed independently for each deploy
			1. Pros: Scales up smoothly as the app naturally expands into more deploys over its lifetime

### Backing Services ###
1. **Treat backing services as attached resources**
2. **Backing service:**
	1. It is any service the app consumes over the network as part of its normal operation
		1. Examples:
			1. Datastores (MySQL, CouchDB)
			2. Messaging/Queueing systems (RabbitMQ, Beanstalkd)
			3. SMTP services for outbound email (Postfix)
			4. Caching systems (Memcached)
	2. Traditional deployment:
		1. Backend services are managed by the same systems adims who deploy the app's runtime (locally managed services)
		2. App may have services provided and managed by third parties
			1. Examples: SMTP services (Postmark)
				2. Metrics-gathering services (New Relic, Loggly)
				3. Binary asset services (Amazon S3)
				4. API-Accessible consumer services (Twitter, Google Maps, Last.fm)
	3. **Code for a twelve-factor app makes no distinction between local and third party services**
		1. Both local and third-party services are considered as **attached resources** 
		2. They are accessed via a URL or other locator/credentials stored in the config
		3. A deploy of a twelve-factor app should be able to swap out a local MySQL database with a managed third party (Amazon RDS say) without any changes to the app's code
		4. A local SMTP server should be swapped with a third-party SMTP service without code changes
			1. Postmark
		5. In all cases, only the resource handle in the config needs to change
	4. **Each distinct backing service is a resource**
		1. Example: MySQL database is a resource
			2. Two MySQL databases (used for sharding at application layer) qualify as two distinct resources
		2. A twelve-factor app treats the databases as **attached resources**
			1. **Loose coupling to the deploy they are attached to**
		3. Attached Resources:
		
			![attached-resources.png](attached-resources.png)
				
	5. Resources can be attached to and detached from deploys at will
		1. Example: If app's database is misbehaving due to a hardware issue, app's admin might spin up a new database server restored from a recent backup
			1. The current prod database could be detached
			2. The new database could be attached without any code changes

### Build, Release, Run ###
1. **Strictly separate build and run stages**
2. Codebase is transformed into a (non-development) deploy through three stages:
	1. Build stage: It is a transform which converts a code repo into an executable bundle known as a build
		1. Uses a version of the code at a commit specified by the deployment process
		2. Fetches vendor dependencies and compiles binaries and assets
	2. Release stage: Takes the build produced by the build stage and combines it with deploy's current config
		1. The resulting **release** contains build and config
			1. It is ready for immediate execution in the execution environment
	3. Run stage:
		1. Aka runtime
		2. It runs the app in the execution environment
			1. Usually by launching a set of app's processes against a selected release
3. Three stages example:

	![release.png](release.png)

3. **A twelve-factor app uses strict separation between the build, release, and run stages**
	1. Example: It is impossible to make changes to the code at runtime
		1. There is no way to propagate the changes to the build stage
4. Deployment tools usually offer release management tools
	1. Which can include the ability to roll back to a previous release
		1. Example: **Capistrano** deployment tool stores releases in a subdirectory named `releases`
			1. The current release is a symlink to the current release directory
			2. `rollback`: The command that makes it easy to quickly roll back to a previous release
5. **Every release should always have a unique release ID**
	1. Example: timestamp of the release (`2011-04-06-20:32:17`)
	2. Example: incrementing number (`v100`)
	3. Releases are **append only ledger**
		1. A release cannot be mutated once created
			1. Any change must instantiate a new release
6. Builds are initiated by app's developers whenever new code is committed
7. Runtime execution can happen automatically in certain cases such as:
	1. Server reboot
	2. Crashed process being restarted by the process manager
8. **Run stage should be kept to as few moving parts as possible**
	1. Why?
		1. Problems that prevent an app from running can cause it to break in the middle of the night when no developers are on hand
9. **Build stage can be more complex:
	1. Why?
		1. Errors are always in the foreground for a developer who is driving the deploy

### Processes ###
1. **Execute the app as one or more stateless processes**
2. **The app is executed in the execution environment as one or more processes**
3. Case 1: Simple case
	1. Code is stand-alone script
	2. Execution environment is a developer's local laptop with installed language runtime
	3. Process is launched via the command line
		1. Example: `python my_script.py`
4. Case 2: Sophisticated app
	1. Prod deployment may use many process types
	2. The app may be instantiated into zero or more running processes
5. **Twelve-factor processes are stateless and share-nothing**
	1. Any data that needs to persist **must be stored in a stateful backing service, typically in a database**
	2. **Memory space or filesystem** of the process can be used as a brief, **single-transaction cache**
		1. Example:
			1. Downloading a large file
			2. Operating on it
			3. Storing the results of the operation in the database
	3. **Twelve-factor app never assumes that anything cached in memory or on disk will be available on a future request or job**
		1. Why?
			1. If there are many processes of each type running, there are high chances that any future requests will be served by a different process
			2. If running only one process, a restart (triggered by code deploy, config change, or other execution environment relocating the process to a different physical location) will usually wipe out all local (e.g., memory and filesystem) state
	4. Asset packagers like django-assetpackager use the filesystem as a cache for compiled assets
		1. **Twelve-factor app prefers to do this compiling during the build stage**
			1. Asset packagers such as Jammit and the Rails asset pipeline can be configured to package assets during the build stage
	5. Some web systems rely on "sticky sessions"
		1. Caching user session data in memory of the app's process and expecting future requests from the same visitor to be routed to the same process
		2. **Sticky sessions are a violation of twelve-factor and should never be used or relied on**
			1. Solution: Session state is a good candidate of a datastore that offers time-expiration, such as Memcached or Redis

### Port Binding ###
1. **Export services via port binding**
2. Scenario: Web apps are sometimes executed inside a webserver container
	1. Example: PHP apps might run as a module inside Apache HTTPD
	2. Example: Java apps might run inside Tomcat
3. **A twelve-factor app is completely self-contained**
	1. It does not rely on runtime injection of a webserver into the execution environment to instantiate a web-facing service
	2. Web app **exports HTTP as a service by binding to a port**
		1. It listens to requests coming in on the port
4. In local development environment, developer visits a service URL like `http://localhost:5000/` to access service exported by the app
5. In deployment, a routing layer handles routing requests from a public-facing hostname to the port-bound web processes
6. Implementation:
	1. **Using dependency declaration** ([https://12factor.net/dependencies](https://12factor.net/dependencies)) **to add a webserver library to the app**
		1. Example: 
			1. **Tornado** for Python
			2. **Thin** for Ruby
			3. **Jetty** for Java (and other JVM-based languages)
	2. **It happens entirely in user space**
		1. **Within the app's code**
			1. Contract with the execution environment: Binding to a port to serve requests
7. Any kind of server software can be run via a process binding to a port and awaiting incoming requests (not just HTTP)
	1. Examples:
		1. Ejabberd (speaking XMPP)
		2. Redis (speaking the Redis protocol)
8. **Port-binding approach means that one app can become the backing service for another app**
	1. By providing the URL to the backing app as a resource handle in the config for the consuming app

### Concurrency ###
1. **Scale out via the process model**
2. A **computer program** when run, is **represented by one or more processes**
	1. Example web-apps: They have taken many process-exuction forms
		1. PHP processes run as child process of Apache
			1. The processes are started on demand as needed by request volume
		2. Java process takes opposite approach
			1. JVM provides one massive uberprocess
			2. It reserves a large block of system resources (CPU and memory) on startup
			3. Concurrency is managed internally via threads
		3. In the above cases, the running process(es) is/are only minimally visible to the developers of the app
3. **In a twelve-factor app, processes are a first class citizen**
	1. Inspired from the unix process model for unning service daemons
	2. App can be architected (by developers) to handle diverse workloads by assigning each type of work to a process type
		1. Example: 
			1. HTTP requests may be handled by a web process
			2. Long-running background tasks handled by a worker process
	3. **Individual processes can still handle their own internal multiplexing:**
		1. **via threads inside the runtime VM**
		2. **async/evented model found in tools such as EventMachine, Twisted, or Node.js**
		3. Problem: Individual VM can only grow so large (vertical scale)
			1. Solution: Application must be able to span multiple processes running on multiple physical machines
	4. Process model shines when it is time to scale out
		1. Pros: Since twelve-factor apps processes are **share-nothing**, **horizontally partitionable**, adding more concurrency is a simple and reliable operation
			1. **The array of process types and number of processes of each type is known as the process formation**
	5. **Twelve-factor app processes should never daemonize or write PID files**
		1. The **app must rely on OS's process manager instead to manager output streams, respond to crashed processes, and handle user-initiated restarts and shutdowns**
			1. Example: on systemd
			2. Example: Distributed process manager on the cloud platform
			3. Example: Tool like **Foreman** ([http://blog.daviddollar.org/2011/05/06/introducing-foreman.html](http://blog.daviddollar.org/2011/05/06/introducing-foreman.html)) in development

### Disposability ###
1. **Maximize robustness with fast startup and graceful shutdown**
2. **A twelve-factor app's processes are disposable**
	1. **Means they can be started or stopped at a moment's notice**
		1. Pros:
			1. Facilitates fast elastic scaling
			2. Facilitates rapid deployment of code or config changes
			3. Facilitates robustness of production deployes
	2. Processes **should strive to minimize startup time**
		1. Ideally, a process takes a few seconds from the time the launch command is executed until the process is up and ready to receive requests or jobs
			1. Pros:
				1. Fast startup time
					1. Provides more agility for the release process and scaling up
					2. Aids robustness
						1. Because process manager can more easily move processes to new physical machines when warranted
3. **Processes shut down gracefully when they receive a SIGTERM signal from the process manager**
	1. Consider web-process:
		1. Graceful shutdown implementation:
			1. Cease to listen on the service port (refusing any new requests)
			2. Allow current requests to finish
				1. HTTP requests are short (no more than a few seconds)
				2. Long poling: Client should seamlessly attempt to reconnect when connection is lost
			3. Then exit
	2. Consider worker process:
		1. Graceful shutdown implementation:
			1. Return current job to work queue
				1. Example: RabbitMQ - worker can send `NACK`
				2. Example: Beanstalkd - Job is returned to the queue automatically whenever a worker disconnects
			2. Lock-based systems (Delayed Job - [https://github.com/collectiveidea/delayed_job#readme](https://github.com/collectiveidea/delayed_job#readme)) need to be sure to release their lock on the job record
					1. It is implicit that jobs are reentrant ([reentrant](http://en.wikipedia.org/wiki/Reentrant_%28subroutine%29))
						1. **Achieved by wrapping results in a transaction, or making the operation idempotent**
							1. Idempotent: Operations that can be applied multiple times without changing the result beyond the initial application of the operation.
	3. Processes should be **robust against sudden death**
		1. In the case of underlying hardware failure
			1. Less common but it can happen
				1. Solution: **Use robust queueing backend (Beanstalkd) that returns jobs to the queue when clients disconnect or time out**
	4. **A twelve-factor app is architected to handle unexpected, non-graceful terminations**
		1. [Crash-only design](http://lwn.net/Articles/191059/) takes the concept to its [logical conclusion](https://docs.couchdb.org/en/latest/intro/overview.html)
			1. **Crash-only software is software that crashes safely and recovers quickly**
				1. The only way to stop it is to crash it
				2. The only way to start it is to recover
		
### Dev/Prod Parity ###
1. **Keep development, staging, and production as similar as possible**
2. History:
	1. There were substaintial gaps between development (a developer making live edits to a local deploy of the app) and production (a running deploy of the app accessed by end users)
		1. The gaps manifest in three areas:
			1. **The time gap:** A developer may work on code that takes days, weeks, or even months to go into production
			2. **The personnel gap:** Developers write code, ops egineers deploy it
			3. **The tools gap:** Developers may be using a stack like Nginx, SQLite, and OS X, while the production deploy uses Apache, MySQL, and Linux
3. **A twelve-factor app is designed for continuous deployment by keeping the gap between development and production small**
	1. Addressing the three gaps:
		1. **Make the time gap small:** developer may write code and have it deployed hours or even minutes later
		2. **Make the personnel gap small:** Developers who wrote code are closely involved in deploying it and watching its behaviour in production
		3. **Make the tools gap small:** Keep development and production as similar as possible
	2. Summary into a table:
		1. Traditional app
			1. Time between deploys
				1. Weeks
			2. Code authors vs code deployers
				1. Different people
			3. Dev vs production environments
				1. Divergent
		2. Twelve-factor app
			1. Time between deploys
				1. Hours
			2. Code authors vs code deployers
				1. Same people
			3. Dev vs production environments
				1. As similar as possible
4. **Backing Services (database, queueing system, cache, ...)**: Area where dev/prod parity is important
	1. Solution: Many languages offer libraries which simplify access to backing service
		1. Using *adapters* to different types of services say
		2. Example:
			1. Database
				1. Language: Ruby/Rails
				2. Library: ActiveRecord
				3. Adapters: MySQL, PostgreSQL, SQLite
			2. Queue
				1. Language: Python/Django
				2. Library: Celeray
				3. Adapters: RabbitMQ, Beanstalkd, Redis
			3. Cache
				1. Language: Ruby/Rails
				2. Library: ActiveSupport::Cache
				3. Memory, filesystem, Memcached
5. Temptation:
	1. Developers often using lightweight backing service in local environment
	2. A more serious and robust backing service will be used in production
	3. Example: SQLite locally and PostgreSQL in production
		1. Local process memory for caching and Memcached in production
6. **A twelve-factor developer resists the urge to use different backing services between development and production**
	1. Differences between backing services means tiny incompatibilities cropping up
		1. These incompatibilities can cause code that worked and passed tests in development or staging to fail in production
			1. They can cause friction that disincentivizes continous deployment
				1. The cost of the friction and subsequent dampening of continous deployment is extremely high when considered in aggregate over the lifetime of an application
	2. Solution: Lightweight local services are less compelling now than they were before
		1. Modern backing services such as Memcached, PostgreSQL, and RabbitMQ are not difficult to install and run
			1. Due to modern packaging systems
				1. Homebrew
				2. apt-get
		2. Declarative provisioning tools (Chef, Puppet, ...) combined with light-weight environments such as Docker, Vagrant, ... **allow developers to run local environments which closely approximate production environments**
			1. The cost of installing and using the systems is low compared to the benefit of dev/prod parity and continous Deployment
7. Adapters:
	1. They are useful because they make proting to new backing services relatively painless
8. **All deploys of the app (developer environments, staging, production) should be using the same type and version of each of the backing services**

### Logs ###
1. **Treat logs as event streams**
2. Logs provide visibility into the behavior of a running app
	1. In server side environment, the logs are commonly written to a file on disk ("logfile")
		1. It is just an output format
3. **Logs are a stream of aggregated, time-ordered events collected from the output streams of all running processes and backing services**
	1. Logs in raw form are typically a text format with one event per line (backtraces from exceptions may span multiple lines)
	2. Logs have no fixed beginning or end
	3. Logs flow continously as long as the app is operating
4. **A twelve-factor app never concerns itself with routing or storage of its output stream**
	1. It **should not attempt to write or or manage logfiles**
		1. Each running process writes to:
			1. event stream, unbuffered, to `stdout`
				1. Local development: Developer will view the stream in foreground of their terminal to observe app's behavior
				2. Staging or Production deploys: Each process' stream will be captured by execution environment
					1. The execution environment collates together will all other streams from the app
					2. The execution environment routes the logs to one or more final destinations
						1. For viewing
						2. For long-term archival
					3. The archival destinations are **not visible to or configurable by the app**
						1. **It is completely managed by the execution environment**
							1. Implementations: Open-source log routers ([Logplex](https://github.com/heroku/logplex), and [fluentd](https://github.com/fluent/fluentd))
				3. **Event stream for an app can be:**
					1. Routed to a file
					2. Watched via realtime tail in a terminal
					3. Sent to log indexing and analysis system such as
						1. [Splunk](http://www.splunk.com/)
					4. Sent to a general-purpose data warehousing system such as
						1. [Hadoop/Hive](http://hive.apache.org/)
					5. The systems give power and flexibility for introspecting the app's behavior over time which includes:
						1. Finding specific events in the past
						2. Large-scale graphing of trends (requests per minute say)
						3. Active alerting according to user-defined heuristics (alert when the quantity of errors per minute exceeds a certain threshold)

### Admin Processes ###
1. **Run admin/management tasks as one-off processes**
2. Process formation is an array of processes that are used to do the app's regular business (handling web requests say) as it runs
3. Developers will wish to do one-off admin or maintenance tasks for the app such as:
	1. Running database migration
		1. Example: `manage.py migrate` in Django
		2. Example: `rake db:migrate` in Rails
	2. Running a console (known as REPL shell) to run arbitrary code or inspecting app's models against live database
		1. Example: Languages provide REPL by running interpreter without arguments
			1. `python`
			2. `perl`
		2. Example: Some languages provide separate command:
			1. `irb` for Ruby
			2. `rails console` for Rails
	3. Runing one-time scripts committed into app's repo
		1. Example: `php scripts/fix_bad_records.php`
4. **One-off admin processes should be run in an identical environment as the regular long-running processes of the app**
	1. **They must run against a release, using the same codebase and config as any process run against the release**
	2. **Admin code must ship with application code to avoid synchronization issues**
	3. **The same dependency isolation techniques should be used on all process types**
		1. Example:
			1. Ruby web process uses `bundle exec thin start`
			2. Ruby database migration should use `bundle exec rake db:migrate`
			3. Python program using Virtualenv should use the vendored `bin/python` for running both Tornado webserver and any `manage.py` admin processes
5. **Twelve-factor strongly favors languages which provide a REPL shell out of the box**
	1. This makes it easy to run one-off scripts
		1. Local deploy: Developers invoke one-off admin processes by a direct shell command inside the app's checkout directory
		2. Production deploy: Developers can use SSH or other remote cammand execution mechanism provided by the deploy's execution environment to run such process