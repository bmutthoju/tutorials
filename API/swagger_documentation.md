# Swagger #
## What is Open API ##
### What is Open API ###
#### OpenAPI Specification ####
1. Formerly Swagger Specification
2. It is a description format for REST APIs
3. An OpenAPI file allows describing an entire API
	1. Includes:
		1. Available endpoints (`/users`)
		2. Operations on each endpoint (`GET /users`, `POST /users`)
		3. Operation parameters
			1. Input for each operation
			2. Output for each operation
		4. Authentication methods
		5. Contact information
		6. License
		7. Terms of use
		8. ...
4. API specs can be written in YAML or JSON
	1. Format is easy to learn and is readable to both humans and machines
		1. [OpenAPI 3.0 Specification](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.3.md)

### What is Swagger? ###
1. **Swagger** - A set of opern-source tools built around the OpenAPI specification that can help us design, build, document & consume REST APIs
	1. Major Swagger tools:
		1. [Swatter Editor](https://editor.swagger.io/?_ga=2.234619932.302509186.1699517040-1271258264.1699235200) - Browser-based editor where we can write OpenAPI definitions
		2. [Swagger UI](https://github.com/swagger-api/swagger-ui) - Renders OpenAPI definitions as interactive documentation
		3. [Swagger Codegen](https://github.com/swagger-api/swagger-codegen) - Generates server stubs and client libraries from an OpenAPI definition
		4. [Swagger Editor Next (beta)](https://editor-next.swagger.io/?_ga=2.234014108.302509186.1699517040-1271258264.1699235200) - Browser-based editor where you can write and review OpenAPI and AsyncAPI definitions
		5. [Swagger Core](https://github.com/swagger-api/swagger-core) - Java related libraries for constructing, consuming, and working with OpenAPI definitions
		6. [Swagger Parser](https://github.com/swagger-api/swagger-parser) - Standalone library for parsing OpenAPI definitions
		7. [Swagger APIDom](https://github.com/swagger-api/apidom) - Provides single, unifying structure for describing API across various description langauges (OpenAPI, RAML, API Blueprint) and serialization formats (XML, YAML, or JSON)

### Why Use OpenAPI? ###
1. Ability of APIs to describe their own structure is root of all awesomeness in OpenAPI
	1. Once written, OpenAPI spec and Swagger tools can drive API development further in various ways:
		1. Design-first users: use [Swagger Codegen](https://github.com/swagger-api/swagger-codegen) to **generate a server stub** for our API
			1. Once we implement the server logic, the API is ready to go live
		2. Use [Swagger Codegen](https://github.com/swagger-api/swagger-codegen) to **generate client libraries** for our API in 40 languages
		3. Use [Swagger UI](https://github.com/swagger-api/swagger-ui) to generate **interactive API documentation** that lets users try out API calls directly in the browser
		4. Use spec to connect API-related tools to our API
			1. Example: Import the spec to [SoapUI](https://soapui.org/?_ga=2.121725449.302509186.1699517040-1271258264.1699235200) to construct automated tests for our API
		5. And more!
			1. Check [open-source](https://swagger.io/tools/open-source/open-source-integrations/) tools that integrate with Swagger
			2. Check [commercial tools](https://swagger.io/commercial-tools/) tools that integrate with Swagger

## Basic Structure ##
1. We can write OpenAPI definitions in [YAML](https://en.wikipedia.org/wiki/YAML) or [JSON](https://en.wikipedia.org/wiki/JSON)
	1. YAML examples are used but JSON works equally well
2. Example definition (using OpenAPI 3.0):

		openapi: 3.0.0
		info:
			title: Sample API
			description: Optional multiline or single-line description in [CommonMark](http://commonmark.org/help/) or HTML.
			version: 0.1.9
		
		servers:
			- url: http://api.example.com/v1
			  description: Optional server description, e.g. Main (production) server
			- url: http://staging-api.example.com
			  description: Optional server description, e.g. Internal staging server for testing

		paths:
			/users:
				get:
					summary: Returns a list of users.
					description: Optional extended description in CommonMark or HTML.
					responses:
						'200': # status code
							description: A JSON array of user names
							content:
								application/json:
									schema:
										type: array
										items:
											type: string

	1. All keyword names are cast-sensitive

### Metadata ###
1. Every API definition must include version of the OpenAPI Specification that the definition is based on:

		openapi: 3.0.0

	1. OpenAPI version defines the overall structure of an API definition
		1. What we can document and how we document it
	2. [semantic versioning](http://semver.org/) is used with three-part version number
		1. Available versions: 3.0.0, 3.0.1, 3.0.2, and 3.0.3 (they are functionally the same)
	3. `info` section contains API info: `title`, `description` (optional), `version`:

			info:
				title: Sample API
				description: Optional multiline or single-line description in [CommonMark](http://commonmark.org/help/) or HTML.
				version: 0.1.9

		1. `title` - It is our API name
		2. `description` - Extended info about our API
			1. It can be [multiline](http://stackoverflow.com/a/21699210) and supports [CommonMark](http://commonmark.org/help/) (dialect of Markdown) for rich text representation
				1. HTML is supported to the extent provided by CommonMark ([HTML Blocks in CommonMark 0.27 Specification](http://spec.commonmark.org/0.27/)
		3. `version` - arbitrary string that specifies the version of our API (not the file revision of the `openapi` version)
			1. We can use semantic versioning: `major.minor.path`
			2. We can use arbitrary string like `1.0-beta` or `2017-07-25`
		4. `info` - supports additional keywords for
			1. Contact information
			2. License
			3. Terms of service
			4. ...
			5. [Info Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.3.md#infoObject)

### Servers ###
1. The `servers` section specifies the API server and base URL
	1. We can define one or several servers (production, sandbox, ...)

			servers:
				- url: http://api.example.com/v1
				  description: Optional server description, e.g. Main (production) server
				- url: http://staging-api.example.com
				  description: Optional server description, e.g. Internal staging server for testing

		1. **All API paths are relative to the server URL**
			1. `/users` means: `http://api.example.com/v1/users` or `http://staging-api.example.com/users` (depending on the server used)
		2. [API Server and Base Path](https://swagger.io/docs/specification/api-host-and-base-path/)

### Paths ###
1. `paths` - defines individual endpoints (paths) in our API, and
	1. HTTP methods (operations) supported by the endpoints
	2. Example: `GET /users` can be described as:

			paths:
				/users:
					get:
						summary: Returns a list of users.
						description: Optional extended description in CommonMark or HTML
						responses:
							'200':
								description: A JSON array of user names
								content:
									application/json:
										schema:
											type: array
											items:
												type: string

		1. Operation definition includes:
			1. Parameters
			2. Request body (if any)
			3. Possible response status codes (200 OK, 404 Not Found)
				1. Response contents
		2. [Paths and Operations](https://swagger.io/docs/specification/paths-and-operations/)

### Parameters ###
1. Operations can have parameters passed via:
	1. URI path (`/users/{userId}`)
	2. Query string (`/users?role=admin`)
	3. Headers (`X-CustomHeader: Value`)
	4. Cookies (`Cookie: debug=0`)
2. We can define:
	1. Parameter
		1. Data types
		2. Format
		3. Whether they are required or optional
		4. ...
3. Example:

		paths:
			/users/{userId}:
				get:
					summary: Returns a user by ID
					parameters:
						- name: userId
						  in: path
						  required: true
						  description: Parameter description in CommonMark or HTML.
						  schema:
							type: integer
							format: int64
							minimum: 1
					responses:
						'200':
							description: OK

	1. [Describing Parameters](https://swagger.io/docs/specification/describing-parameters/)

### Request Body ###
1. If an operation sends a request body, use `requestBody` keyword to describe the body content and media type

		paths:
			/users:
				post:
					summary: Creation of user.
					requestBody:
						required: true
						content:
							application/json:
								schema:
									type: object
									properties:
										username:
											type: string
					responses:
						'201':
							description: Created

	1. [Describing Request Body](https://swagger.io/docs/specification/describing-request-body/)

### Responses ###
1. For each operation, we can define status codes (200 OK, 404 Not Found), and response body `schema`
	1. Schemas can be defined inline or referenced via `$ref` **(M)**
2. We can provide example responses for different content types:

		paths:
			/users/{userId}:
				get:
					summary: Returns a user by ID.
					parameters:
						- name: userId
						  in: path
						  required: true
						  description: The ID of the user to return
						  schema:
							type: integer
							format: int64
							minimum: 1
					responses:
						'200':
							description: A user object.
							content:
								application/json:
									schema:
										type: object
										properties:
											id:
												type: integer
												format: int64
												example: 4
											name:
												type: string
												example: Jessica Smith
						'400':
							description: The specified user ID is invalid (not a number)
						'404':
							description: A user with the specified ID was not found.
						default:
							description: Unexpected error

	1. Response HTTP status codes must be enclosed in quotes: '200' (OpenAPI 2.0 did not require this)
	2. [Describing Responses](https://swagger.io/docs/specification/describing-responses/)

### Input and Output Models ###
1. Global `components/schemas` **(M)** section lets us define **common data structures** used in the API
	1. They can be referenced via `$ref` whenever a schema is required
		1. In
			1. Parameters
			2. Request bodies
			3. Response bodies
2. Example:
	1. JSON Object

			{
				"id": 4,
				"name": "Arthur Dent"
			}

	2. Representation:

			components:
				schemas:
					User:
						type: object
						properties:
							id:
								type: int64
								example: 4
							name:
								type: string
								example: Arthur Dent
					# Both properties are required
					required:
						- id
						- name

	3. Reference: In request body schema and response body schema:

			paths:
				/users/{userId}:
					get:
						summary: Returns a user by ID.
						parameters:
							- in: path
							  name: userId
							  required: true
							  schema:
								type: integer
								format: int64
								minimum: 1
						responses:
							'200':
								description: OK
								content:
									application/json:
										schema:
											$ref: '#/components/scheams/User'
				/users:
					post:
						summary: Constructs a new user.
						requestBody:
							required: true
							content:
								application/json:
									schema:
										$ref: '#/components/schemas/User'
						response:
							'201':
								description: Created

### Authentication ###
1. `securitySchemas` and `security` keywords are used to describe athentication methods used in API

		components:
			securitySchemas:
				BasicAuth:
					type: http
					schema: basic

		security:
			- BasicAuth: []

	1. Supported authentication methods:
		1. HTTP authentication: [Basic](https://swagger.io/docs/specification/authentication/basic-authentication/), [Bearer](https://swagger.io/docs/specification/authentication/bearer-authentication/), ...
		2. [API Key](https://swagger.io/docs/specification/authentication/api-keys/): As
			1. Header
			2. Query Parameter
			3. Cookies
		3. [OAuth2](https://swagger.io/docs/specification/authentication/oauth2/)
		4. [OpenID Connect Discovery](https://swagger.io/docs/specification/authentication/openid-connect-discovery/)

### Full Specification ###
1. Full OpenAPI 3.0 Spec: [https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.3.md](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.3.md)

## API Server and Base URL ##
1. All API endpoints are relative to the base URL
	1. Example: Assuming the base URL is `https://api.example.com/v1`, the `/users` endpoint refers to `https://api.example.com/v1/users`

			https://api.example.com/v1/users?role=admin&status=active

2. In Open API 3.0, `servers` array is used to specify one or more base URLs for the API (it replaces `host`, `basePath`, and `schemas` keywords used in OpenAPI 2.0)
3. Each server has `url` and optional Markdown-formatted `description`

		servers:
			- url: https://api.exmaple.com/v1	# The "url: " prefix is required

4. We can have multiple servers (production, sandbox):

		servers:
			- url: https://api.example.com/v1
			  description: Production server (uses live data)
			- url: https://sandbox-api.example.com:8443/v1
			  description: Sandbox server (uses test data)

### Server URL Format ###
### Server Templating ###
### Examples ###
#### HTTPS and HTTP ####
### Production, Development and Staging ###
### SaaS and On-Premise ###
### Regional Endpoints for Different Geographical Areas ###
### Overriding Servers ###
### Relative URLs ###
### References ###