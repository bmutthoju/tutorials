# Terraform 101: The Ultimate Hands-On Guide [Azure Edition]
## Section 1: Getting Started: Meet Your Instructor and Discover Terraform
### Introduction
1. Mastering Terraform
	1. VMs
	2. K8s 
	3. Serverless
2. Mastering Terraform: Book - Amazon
3. Azure terraform - YouTube channel

### What is Infrastructure-as-Code?
1. IaC
	1. Codifies provisioning infrastructure
		1. Automates setup process and configuration of the environment
	2. Consistent and repeatable process

### What is Terraform?
1. Infrastructure orchestration tool was required
	1. Azure ARM templates
	2. AWS Cloud formation
		1. To declare what cloud infrastructure should look like
			1. Virtual networks
			2. Storage accounts
			3. S3 buckets
			4. EC2 instances
			5. ...
				1. Cloud providers take care of the rest of the setup
		2. We need to learn AWS-specific syntax and tools
			1. Solution: Terraform - cloud-agnostic alternative (not tied to a specific cloud provider)
				1. It uses declarative approach (like AWS cloud formation)
				2. Developers need to learn Terraform once and use the knowledge to work with different cloud environments
			2. It works with on-premises platforms to boot
			3. Note: It is not a write once and run anywhere infrastructure as code tool
				1. If we write terraform for AWS, it only works on AWS
					1. It only offers a common:
						1. Syntax
						2. Mechanics of working with the tool
						3. Language
			4. Developers can leverage the distinct capabilities and prowesses of the cloud platforms they want to build their systems on
			5. Terraform's own light-weight functional language: HCL - Hashicorp Configuration Language (balances productivity and solution sophistication)
				1. It is iterative:
					1. It was built to start small and evolve the code and solution over time

## Section 2: Key Concepts for Terraform and Infrastructure-as-Code
### Section Introduction
1. Vocabulary

### Idempotence
1. Idempotence:
	1. If we run a complex set of actions repeatedly, we should get the same outcome
		1. The process is idempotent
	2. Terraform is idempotent infrastructure code tool
		1. The config we specify within HCL defines the final outcome (desired state)
			1. `terraform apply` - running it repeatedly doesn't change the outcome
				1. It doesn't change the state the second time

### Immutability
1. Immutable:
	1. Mutable: Can something change or be replaced?
		1. Can something be changed or manipulated in-place
	2. Immutable: Cannot change
	3. Example: Manual provisioning
		1. Changing settings
		2. Moving props
			1. Mutable
				1. We can go to AWS and change infrastructure
	4. How can we make infrastructure immutable?
		1. We can generate snapshots and artifacts
			1. We can revert back to the state
				1. Versioning
					1. Example: VM image is captured
		2. Terraform:
			1. It allows us to produce a compiled plan that gives us a point-in-time snapshot of the change we want to invoke in an environment
				1. It gives us a state file that describes the current configuration of the environment
				2. Compile plan - it only gives us a roadmap to go from point A to point B when there is a change at a precise moment in time
				3. State - Gives us a historical document that describes what terraform is expecting the environment to look like (snapshot)
				4. Immutability - Each version of the code is an immutable artifact
					1. Terraform needs version control system
						1. Helps revert back to last-known good configuration

### Encapsulation
1. Encapsulation in IaC:
	1. Grouping a cohesive set of responsibility into a single component
		1. Exposing the pre-conditions and post-conditions as interface
			1. Inputs - Things that the component requires to perform the responsibility
			2. Outputs - By-products of performing the responsibility
	2. Essential for terraform
		1. We encapsulate functionality inside a terraform module
	3. Logical boundary - module
		1. Boundary of a module - folder (physical boundary)
			1. It contains .tf files
				1. They contain resources and blocks (logical components)
				2. They contain the internal implementation detail of the module
	4. Encapsulation abstracts the module
2. Consumers just need to know inputs, outputs, and what the module does

### Cohesion
1. Cohesion - focusing a module or a component on a specific task or responsibility
	1. It makes a software component
		1. Easier to maintain
		2. Easier to understand
		3. Easier to extend
	2. A very important design principle when building infrastructure as code
	3. It is used to support certain use-cases

### Declarative vs. Imperative
1. Declarative
	1. We just describe what the outcome should be
	2. Terraform: We just describe the resources
		1. Terraform handles planning and executing the plan to meet the requirement
2. Imperative
	1. We give the procedure and all the details of how to go from the input to the output
		1. Individual commands are executed in sequence

### What is DRY?
1. DRY:
	1. Problem with applying DRY in IaC
		1. Many layers of abstraction that obfuscate the actual intent of the original author
			1. Unlike in traditional software, we don't have tools to do robust testing, so we cannot afford such complexity
				1. The testing can be done in memory
			2. Terraform depends on the Cloud platform (it cannot do anything meaningful in isolation)
			3. Solution: IaC developer needs to define modules very cleanly and very concisely about their intent and what they are about to do
				1. It should be visible and obvious to anyone
				2. Prioritize clarity over perceived technical elegance
		2. We have limited debug capability (due to coupling with cloud)
			1. Solution: Pealing like an onion
				1. Start at the very core of the infrastructure and layering on top piece by piece
					1. Go from nothing to full environment
						1. Helps test every step of the way
	2. WET - Write everything twice
		1. Better approach for IaC

## Section 3: Setup Your Windows Development Environment for Terraform
### Installing Visual Studio Code (VS Code) on Windows
1. Install VS Code

### Installing Chocolatey Package Manager on Windows
1. Chocolatey - package manager (like apt, yum, brew)
	1. chocolatey.org
		1. Copy powershell command
		2. Run powershell as an admin
		3. Paste the command
		4. `choco` - shows version
			1. To upgrade: `choco upgrade chocolatey`

### Installing Terraform on Windows
1. Terraform works across platforms
	1. terraform.io
		1. Install using Chocolatey: cmd
		
		```
		choco install terraform -y
		refreshenv
		terraform --version
		```

### Setup HashiCorp Terraform Extension for Visual Studio Code
1. Extensions: Search for terraform (hashicorp)
	1. Handles formatting
	2. Settings
		1. `format`
			1. Editor: Format On Save - check it

### Installing the Azure CLI on Windows
1. Azure CLI
	1. Provisioning resources
	2. See information about available resources
2. Search: Azure CLI
	1. Windows
	2. Using Chocolatey
	
	```
	choco install azure-cli -y
	refreshenv
	az --version
	```

### Installing Git on Windows
1. Search: Git
2. Install using Choco:

```
choco install git -y
```

3. Git bash in VS Code

### Setup Source Code Folder on Windows
1. `C:/Users/<user>/source/repos`
	1. Drag to quick access menu

## Section 4: Terraform Fundamentals: Core Concepts and Syntax
### Section Introduction
1. Syntax of HCL
2. See how terraform works without cloud

### Construct Your First Terraform Resource
1. `repos/Terraform101/Lab1`
	1. The folder in which we are in is the working directory of Terraform when we run it
		1. It scans the directory for all the files it needs to process
	2. `main.tf`
	
	```
	<block-type> <resource-type> <object-reference-the-resource-name> {
	  <attributes> = <value>
	}
	```
	
	```
	resource random_string suffix {
	  length = 6
	}
	```

### First Time Using the Terraform Core Workflow
1. `terraform init`
	1. Initializing the current working directory
		1. Backend initialization
			1. Where terraform stores its state (in a state file)
		2. Provider initialization
			1. Find provider for the resource
			2. Install provider: `hashicorp/random v3.6.3`
				1. Provider provides resources
	2. Adds new files and folders
		1. `.terraform`
			1. `LICENSE.txt`
			2. `terraform-provider-random_v3.9.1_x5.exe` (provider)
		2. `.terraform.lock.hcl`
2. `terraform plan`
	1. It detects that a new resource needs to be created
	2. It also shows what it is planning to do instantiate the resource (`+create`)
	3. Shows default values for optional attributes
	4. Plan is done in memory (nothing is written)
3. `terraform apply`
	1. It runs the plan again and asks for your permission
		1. `yes`
			1. Random string gets created
	2. If we run it again, it checks state to see if anything changed and doesn't do anything
		1. `terraform.tfstate`
			1. json
				1. Array of resources
					1. resource
						1. Provider
						2. Instances
							1. Result: <random-string>
4. `main.tf`

```
resource random_string suffix {
  length = 6
  upper = false
}
```

	1. `terraform plan` - shows that resource needs to be destroyed and recreated
	2. `terraform apply`
5. `special = false`
6. We want to retain the random number across `terraform apply` commands because we don't want our resources to get a new name each time
7. `terraform destroy`
	1. Destroys the entire environment
	2. Runs a terraform plan to show what it is going to destroy
	3. Removes resources from the `tfstate` file

### Whiteboard: Terraform Core Workflow
1. Three places
	1. Code
		1. Random string
		2. Plan against the code
			1. Looked at the state file
			2. Discovered that resource needs to be created
		3. Apply
			1. Provisioned a random string
			2. The string is stored in the state file
		4. `upper = false`
		5. Plan
			1. Looks at the state file
			2. It sees the random string and finds that it is invalid
			3. It finds that it needs to replace
		6. Apply
			1. Updates state file
			2. Updates environment (state file in this case)
		7. Destroy
	2. State
		1. Random string
	3. Environment
		1. It is the state file in this case

### Construct Your First Input Variable
1. Input variables
	1. To pass parameters to terraform config
		1. Allows us to change what the configuration does through well-placed and intelligently designed input variables
	2. Enables customization by others
	3. Re-use: for different environments
		1. To reduce cost
		2. To turn features on or off in a certain context
			1. Example: Dev vs production
			2. Example: Autoscale settings
			3. Example: Region and availability zone (usually customized)
2. Two input variables
	1. Application name
	2. Environment
3. `variables.tf` - processed automatically

```
variable application_name {

}
```

	1. Terraform tries to figure out the type if not specified
4. `terraform plan`
	1. Enter an application name: `marksblog`
5. Specifying value in the commandline:

```
terraform plan -var "application_name=marksblog" # **(M)**
```

6. More variables:

```
variable environment_name {

}
```

7. `terraform plan -var "application_name=marksblog" -var "environment_name=dev"`
	1. If not specified, terraform prompts for the value
8. `terraform apply -var "application_name=marksblog" -var "environment_name=dev"`
	1. Since we are not using the variables, it does not affect the plan (tfstate file doesn't record them)

### Local Variables
1. Defined inside terraform config
	1. Like globals inside a class, say
	2. Convenient for re-usable constants or intermediate values
		1. For stiching together a composite of values coming from other places (input varibles, resources, etc.)
2. They don't get their own block
	1. They share a block
	2. There can be multiple locals blocks in a single file
	3. We can declare locals blocks in every terraform file
3. Syntax: main.tf

```
locals {
  environment_prefix = "marksblog-dev"
}
```

	1. Other blocks can reference the local
	2. `terraform plan` doesn't affect the outcome

### Construct Your First Output
1. Outputs are used to extract values from terraform (from resources) to pass it forward to other tools like:
	1. Ansible
	2. Kubernetes
2. They define the outbound contract
3. `outputs.tf` - convention

```
output application_name {
  value = var.application_name
}
```

	1. `var.application_name` - refers to input variable
	2. `terraform plan -var "application_name=marksblog" -var "environment_name=dev"`
	3. `terraform plan -var "application_name=marksblog" -var "environment_name=dev"`
4. `terraform output application_name`
	1. Returns the output value
5. `outputs.tf`

```
output environment_name {
  value = var.environment_name
}

output environment_prefix {
  value = local.environment_prefix
}
```

### String Interpolation
1. It is concatenating strings together and embedding symbols in string constants
2. `main.tf`

```
locals {
  environment_prefix = "${var.application_name}-${var.environment_name}"
}
```

### Defining Your Required Providers
1. We need to define providers (no automatic discovery)
	1. We don't want the latest version each time
		1. We need to pin the versions for predictability
2. `versions.tf`

```

```

	1. `random` - provider name
	2. `source` - organization that published it
	3. `~> ` - Pessimistic. Patch releases are allowed (it will not contain breaking changes) - they may have fixes
		1. `= ` - use the exact version
		2. `>= ` - any version that is greater than or equal to the specified version

### Referencing Resource Outputs
1. Resources have inputs and outputs
	1. `result` - it contains the output
2. `outputs.tf`

```
output suffix {
  value = random_string.suffix.result
}
```

	1. `random_string` - resource type
	2. `suffix` - resource name
3. `main.tf`

```
locals {
  environment_prefix = "${var.application_name}-${var.environment_name}-${random_string.suffix.result}"
}
```

4. We connect the dots by passing outputs of resources to other resources as inputs

### RTFM: Looking Up Documentation for Terraform Resources
1. To find information about resource inputs and outputs
	1. `https://registry.terraform.io` - all providers and the documentation
		1. `Random`
			1. Documentation
				1. Resources
					1. Search: `random_string`
						1. Required inputs
						2. Optional inputs
						3. Outputs

### Default Input Variables Files
1. Input variable files - solution for not using long CLI commands (`-var "application_name=marksblog"`)
	1. Concise way of storing config
	2. Extension: `tfvars`
	3. Terraform automatically loads file with two distinct names:
		1. `terraform.tfvars`
		2. `*.auto.tfvars`
			1. We either use the first or the second
2. `terraform.tfvars`

```
application_name = "marksblog"
environment_name = "dev"
```

3. `default.auto.tfvars`

```
application_name = "marksblog"
environment_name = "dev"
```

### Using Input Variable Files for Environment Configuration
1. Excellent for storing config values that span across environments
	1. Environment name changes across environments
		1. Use any name for the tfvars files
2. `default.auto.tfvars`

```
application_name = "marksblog"
```

3. `dev.tfvars`

```
environment_name = "dev"
```

4. How to pass `dev.tfvars`?

```
terraform apply -ver-file dev.tfvars
``` 

### Managing Input Variable Files for Multiple Environments
1. `test.tfvars`

```
environment_name = "test"
```

2. `prod.tfvars`

```
environment_name = "prod"
```

3. Grouping:
	1. `env-dev.tfvars`
	2. `env-test.tfvars`
	3. `env-prod.tfvars`
4. Grouping: Another technique:

```
env/
  dev.tfvars
  test.tfvars
  prod.tfvars
```

```
terraform apply -var-file ./env/dev.tfvars
```

### Sensitive Inputs and Outputs
1. Secrets - inputs and outputs
	1. We don't want to show secrets in console
	2. Terraform sometimes provisions using secret management services
2. `variables.tf`

```
variable api_key {
  sensitive = true
}
```

	1. When we run `terraform apply`, the input is not displayed on the console when typed
3. `outputs.tf`

```
output api_key {
  value = var.api_key
}
```

	1. When we run `terraform.apply` and enter the input, it throws an error: `Output refers to sensitive values`
		1. Does it work with string interpolation?
		
		
		```
		output api_key {
		  value = "${var.api_key}bar"
		}
		```
		
			1. Still throws an error
	2. Fix:
	
	```
	output api_key {
	  value = "${var.api_key}"
	  sensitive = true
	}
	```
	
		1. Shows that the output is sensitive
		2. `terraform output api_key`
			1. Shows the output
		3. We must execute terraform in a trusted machine
			1. The machine stores the sensitive inputs and outputs in state locally
				1. Solution: Terraform state files must be encrypted at rest
					1. Apply the principle of least privilege

### Passing Input Variable Values using Environment Variables using PowerShell
1. `tfvars` - are in source code
	1. It should not contain secrets
2. Use powershell to set the environment variables

```
$env:MARKSBLOG_API_KEY = "foo"

$env:MARKSBLOG_API_KEY
```

3. Terraform needs a specific naming convention for environment variables

```
$env:TF_VAR_api_key = "foo"

$env:TF_VAR_api_key
```

	1. `api_key` - case-sentive replica of the actual variable in the file
	2. Run: `terraform apply -var-file ./env/prod.tfvars`
		1. It doesn't prompt

### Passing Input Variable Values using Environment Variables using BASH
1. Bash

```
echo $TF_VAR_api_key # empty

export TF_VAR_api_key=foo

echo $TF_VAR_api_key
```

2. Run: `terraform apply -var-file ./env/prod.tfvars`

### Input Variable Value Selection Order
1. The order of priority in which terraform is going to accept input variable values
	1. Important to remember
		1. Tip: Do not set the same input variable using multiple methods
			1. Incorrect values can go unnoticed
2. Order:
	1. First: environment variables
		1. Have a strategy to compartmentalize environment variables (in a context)
			1. Within a container
			2. Within a context
				1. Avoid environment variable leakage
		2. Use only for secrets
	2. Second: Default tarraform var files (`terraform.tfvars`, `*.auto.tfvars`)
		1. Pick only one
		2. Use for application-wide settings
	3. Third: `-var` and `-var-file`
		1. For each environment
	4. Last: Manual input
		1. Not required

### Deep Dive: Input Variable Value Selection Order
1. `Terraform101/InputVariables`
2. `InputVariables/custom.tfvars`

```
foo = "red"
```

3. `InputVariables/main.tf`
4. `InputVariables/outputs.tf`

```
output foo {
  value = var.foo
}
```

5. `InputVariables/terraform.tfvars`
6. `InputVariables/variables.tf`

```
variable foo {
  type = string
}
```

7. `terraform apply`
8. `terraform apply -var-file custom.tfvars`
9. `terraform apply -var-file custom.tfvars -var foo=blue` (the last one sets the final value)
	1. `terraform apply -var foo=blue -var-file custom.tfvars`
		1. The order matters
10. `default.auto.tfvars`

```
foo = "yellow"
```

	1. `terraform apply`
		1. `terraform.tfvars` is processed first
		2. `default.auto.tfvars` is processed next
11. Environment variables

```
export TF_VAR_foo=purple
echo $TF_VAR_foo
```

	1. Remove all the other variables and run `terraform apply`

### Input Variable Types
1. "" - string
2. It is good practice to explicitly define the type
	1. For future authors
	2. For predictability
3. `variables.tf`

```
variable application_name {
  type = string
}

variable environment_name {
  type = string
}

variable api_key {
  type = string
  sensitive = true
}

variable instance_count {
  type = number
}
```

4. `prod.tfvars`

```
instance_count = 4
```

5. Boolean:

```
variable enabled {
  type = bool
}
```

6. Other types: Complex objects

```
variable "regions" {
  type = list(any)
}
```

```
variable "regions" {
  type = list(string)
}

variable "region_instance_count" {
  type = map(string)
}

variable "region_set" {
  type = set(string)
}
```

7. prod.tfvars

```
regions = ["westus", "eastus"]
region_instance_count = {
  "westus" = 4
  "eastus" = 8
}
region_set = ["westus", "eastus"]
```

8. Accessing: outputs.tf

```
ouitput primary_region {
  value = var.regions[0]
}

output primary_region_instance {
  value = var.region_instance_count["westus"]
}
```

9. Further customization:

```
output primary_region_instance {
  value = var.region_instance_count[var.regions[0]]
}
```

10. Complex object: `variables.tf`

```
variable "sku_settings" {
  type = object({
    kind = string
    tier = string
  })
}
```

11. prod.tfvars

```
sku_settings = {
  kind = "P"
  tier = "Business"
}
```

	1. Helps group attributes that are coupled to each other
12. outputs.tf

```
output "kind" {
  value = var.sku_settings.kind
}
```

### Input Variable Validation
1. To prevent users from passing invalid input values
2. Expression can reference any block (watch out for circular dependencies)
3. `variables.tf`

```
variable application_name {
  type = string

  validation {
    condition = length(var.application_name) <= 12
    error_message = "Application Name must be less than or equal to 12 characters"
  }
}

// ...

variable "instance_count" {
  type = number

  validation {
    condition = var.instance_cout > 1 && var.instance_count < 10 && var.instance_count % 2 != 0
    error_message = "Must be between 1 and 10"
  }
}
```

13. Business rules: We can set them in the validation
14. Locals: `validation.tf`:

```
locals {
  min_nodes = 5
  max_nodes = 10
}
```

15. Accessing locals: variables.tf

```
variable instance_count {
  type = number

  validation {
    condition = var.instance_count >= local.min_nodes && var.instance_count <= local.max_nodes && var.instance_count % 2 != 0
    error_message = "Must be between 5 and 10"
  }
}
```

### Adding Comments
1. `//`

```
// Application Name
```

2. `#`

```
# Application Name
```

3. `/* ... */`

```
/*
Application
*/
```

### Using Workspaces
1. Terraform by default sets up a default workspace
2. Multiple workspaces
	1. Helps us switch between different instances of our root module
		1. Instance? State file
			1. Allows us to support multiple environment
				1. Problem: If we want to run terraform against a different environment, we cannot do with with default workspace because there is only one state file
					1. Solution: Additional state files for different environments
						1. We can assign a different name
						2. We can switch between them
3. `terraform workspace list`

```
* default
```

4. `terraform workspace new dev` **(M)**

```
terraform workspace list
```

5. Switching to default workspace: `terraform workspace select default` **(M)**
6. `terraform workspace new test`
	1. `terraform apply -var-file ./env/test.tfvars`
7. Where are the state files stored?
	1. Local backend
	
	```
	terraform.tfstate # prod
	terraform.tfstate.d
		+- dev
			+- terraform.tfstate
		+- test
			+- terraform.tfstate
	```
	
	2. The implementation details are different for cloud (maybe appends workspace name)
		1. S3
		2. Azure blob
		3. ...

### List and Count
1. Iterating across a collection:
2. List and count meta-argument
3. Different resources for each region

```
resource "random_string" "list" {

  count = 2

  length = 6
  upper = false
  special = false
}
```

4. Getting length from a list

```
resource "random_string" "list" {

  count = length(var.regions)

  length = 6
  upper = false
  special = false
}
```

### Maps and For Each
1. Iterating over a map
	1. To set up an infrastructure per key iteratively
		1. A key can be mapped to an object
			1. Each object can be a graph of resources
2. `main.tf`

```
resource "random_string" "map" {

  for_each = var.region_instance_count

  length = 6
  upper = false
  special = false
}
```

### Booleans and Conditionals
1. `if` block
	1. HCL is a functional language
2. Used to turn on or off a resource
3. `main.tf`

```
resource "random_string" "if" {
  
  count = var.enabled ? 1 : 0
  
  length = 6
  upper = false
  special = false
}
```

### Using the Terraform Module Registry
1. Modules
	1. To group resources together, package them up and deliver as one component to be used in terraform solution
		1. Every terraform project is a module
			1. Root module
			2. Re-usable module
	2. Terraform module registry
		1. Anyone can publish modules there
		2. [registry.terraform.io](registry.terraform.io)
			1. Modules
				1. Providers
					1. Search: random
						1. `hashicorp/module`
						
						```
						module "alpha" {
						  source = "hashicorp/module/random"
						  version = "1.0.0"
						}
						```
						
							1. Put it in `main.tf`
							2. It doesn't have a module type
								1. Defined by the `source`
							3. We need a better name than `"module"`
							4. When we add a module reference, we need to re-run `terraform init`
							5. `.terraform/modules/module/{main.tf,outputs.tf,variables.tf}` (copy of the code)	
						2. `outputs.tf`
						
						```
						output "alpha" {
						  value = module.alpha.random_string
						}
						```
						
						3. `terraform apply -var-file ./env/test.tfvars`

### Constructing Your First Module
1. Local modules
2. `modules/rando`

```
resource random_string suffix {
  length = var.length
  upper = false
  special = false
}
```

3. `main.tf`

```
module "charlie" {
  source = "./modules/rando"
  length = 8
}
```

	1. `terraform init`
	2. Versioning is not required for local modules
4. `modules/rando/variables.tf`

```
variable length {
  type = number
}
```

5. `modules/rando/outputs.tf`

```
output "random_string" {
  value = random_string.rando.result
}
```

6. `outputs.tf`

```
output "charlie" {
  value = module.charlie.random_string
}
```

### Module Encapsulation
1. To encapsulate sophisticated environment
	1. To provision an environment in a particular region
2. Modules help us organize code into manageable chunks.
3. `modules/regional-stamp/main.tf`

```
resource random_string virtual_machines {
  length = 10
  upper = false
  special = false
}
```

4. `modules/regional-stamp/variables.tf`

```
variable "region" {
  type = string
}

variable "name" {
  type = string
}

variable "min_node_count" {
  type = number
}

variable "max_node_count" {
  type = number
}
```

5. `modules/regional-stamp/outputs.tf`

```
output "random_string" {
  value = random_string.virtual_machines.result
}
```

6. `main.tf`

```
resource random_string suffix {
  length = 6
  upper = false
  special = false
}

locals {
  environment_prefix = "${var.application_name}-${var.environment_name}-${random_string.suffix.result}"
}

module "regionA" {
  source = "./modules/regional-stamp"
  region = "westus"
  name = "foo"
  min_node_count = 4
  max_node_count = 8
}

module "regionB" {
  source = "./modules/regional-stamp"
  region = "eastus"
  name = "fooB"
  min_node_count = 4
  max_node_count = 8
}
```

7. Run:

```
terraform init
terraform apply -var-file ./env/test.tfvars
```

### Region Count.Index
1. `main.tf`

```
locals {
  environment_prefix = "${var.application_name}-${var.environment_name}-${random_string.suffix.result}"
  regional_stamps = [
    {
      region = "westus"
      name = "foo"
      min_node_count = 4
      max_node_count = 8
    },
    {
      region = "eastus"
      name = "bar"
      min_node_count = 4
      max_node_count = 8
    }
  ]
}

module "regional_stamps" {
  source = "./modules/regional-stamp"

  count = length(local.regional_stamps)

  region = local.regional_stamps[count.index].region
  name = local.regional_stamps[count.index].name
  min_node_count = local.regional_stamps[count.index].min_node_count
  max_node_count = local.regional_stamps[count.index].max_node_count
}
```

2. `modules/regional-stamp/outputs.tf`

```
output "name" {
  value = var.name
}
```

3. `outputs.tf`

```
output "regionaA" {
  value = module.regional_stamps[0].name
}

output "regionaB" {
  value = module.regional_stamps[1].name
}
```

### Region ForEach.Value
1. `main.tf`

```
resource random_string suffix {
  length = 6
  upper = false
  special = false
}

locals {
  environment_prefix = "${var.application_name}-${var.environment_name}-${random_string.suffix.result}"
  regional_stamps = {
    "foo" = {
      region = "westus"
      min_node_count = 4
      max_node_count = 8
    },
    "bar" = {
      region = "eastus"
      min_node_count = 4
      max_node_count = 8
    }
  }
}

module "regional_stamps" {
  source = "./modules/regional-stamp"

  for_each = local.regional_stamps

  region = each.value.region
  name = each.key
  min_node_count = each.value.min_node_count
  max_node_count = each.value.max_node_count
}
```

2. `outputs.tf`

```
output "regionA" {
  value = module.regional_stamps["foo"].name
}

output "regionB" {
  value = module.regional_stamps["bar"].name
}
```

### Terraform Console
1. We don't need a terraform output
2. `terraform console` **(M)** (we can enter the output to get the value)

```
random_string.suffix

random_string.suffix.result

local.environment_prefix

var.application_name

var.environment_name # known after the apply

random_string.suffix.result

local.regional_stamps

local.regional_stamps["foo"]

local.regional_stamps["foo"].region

exit
```

	1. We can see the outputs that needs to be passed to other resources

## Section 5: Setup and Access Your Azure Subscription
### Sign Up for an Azure Subscription
1. Pay-as you go - has free-tier
	1. Recommended

### What about the Free Tier?
1. `portal.azure.com`
2. View remaining credit
	1. CosmosDB account
	2. Azure Storage
		1. Expires every month
			1. Limited usage per month

### Logging into the Azure Portal
1. Resource groups
	1. Every deployment is in a resource group
2. All resources view
3. Subscriptions
	1. Subscription ID - important
	2. Default directory
4. Entra ID
	1. Tenant
		1. Tenant ID
			1. All authentication is done through entra ID tenant
				1. Any human or machine identity should be registered within the tenant

### Logging in with the Azure CLI
1. `az --version`
2. `az login`

## Section 6: Getting Started with Azure and Terraform
### Section Introduction
1. Setup
	1. Terraform Azure provider - `azurerm`
	2. Promision Azure infra
	3. Provision Azure storage account
		1. Important
			1. Terraform state files
	4. Azure monitor and key-vault
		1. Important

### Configure the Azure Terraform Provider
1. `Lab2`

```
main.tf
outputs.tf
variables.tf
versions.tf
```

2. [https://registry.terraform.io/providers/hashicorp/azurerm/4.8.0](https://registry.terraform.io/providers/hashicorp/azurerm/4.8.0)
	1. Latest: [https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs)
3. Azure CLI authentication
4. `versions.tf`

```
# We strongly recommend using the required_providers block to set the
# Azure Provider source and version being used
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "=5.0.0"
    }
  }
}

# Configure the Microsoft Azure Provider
provider "azurerm" {
  features {}
}
```

	1. `provider`
		1. Control features
		2. Azurerm needs authentication
5. `terraform init -upgrade`
6. Specify subscription id - `>= v4.0.x` (default is not taken)
	1. Get subscription id from portal

	```
	provider "azurerm" {
	  features {}
	  subscription_id = "..."
	}
	```
	
	2. Another way to get the id: `az account show` **(M)** or `az account list` (shows all the subscriptions)
	3. If we want to use terraform to provision in different subscriptions?
		1. Environment variable.
		2. Remove:
		
		```
		subscription_id = "..."
		```
		
		3. Powershell:
		
		```
		$env:ARM_SUBSCRIPTION_ID = "..."
		```
		
		4. Bash:
		
		```
		export ARM_SUBSCRIPTION_ID="..."
		```

### Construct an Azure Resource Group
1. Most important resource: Azure resource group
2. `main.tf`

```
resource "azurerm_resource_group" "main" {
  name = "rg-foobar"
  location = "westus3"
}
```

3. `terraform apply`
4. Check resource group in portal

### Resource Group Naming Conventions
1. Naming convention
	1. Define consistent naming convention
		1. Unique application name
		2. Unique environment name
			1. Better navigation experience
2. variables.tf

```
variable application_name {
  type = string
}

variable environment_name {
  type = string
}
```

3. `main.tf`

```
resource "azurerm_resource_group" "main" {
  name = "rg-${var.application_name}-${var.environment_name}"
  location = "westus3"
}
```

4. We can start with a primary region and add more regions (even with resources with multi-region support)
5. `main.tf`

```
resource "azurerm_resource_group" "main" {
  name = "rg-${var.application_name}-${var.environment_name}"
  location = var.primary_location
}
```

6. `variables.tf`

```
variable application_name {
  type = string
}

variable environment_name {
  type = string
}

variable "primary_location" {
  type = string
}
```

7. `env/dev.tfvars`

```
environment_name = "dev"
```

8. `env/prod.tfvars`

```
environment_name = "prod"
```

9. `terraform.tfvars`

```
application_name = "marksblog"
primary_location = "westus3"
```

10. `terraform apply -var-file ./env/prod.tfvars`

### Construct an Azure Storage Account
1. Provisioning storage account
2. Terraform registry
	1. Filter: storage
		1. Azurerm storage account
3. Register resource provider:

```
az provider register --namespace Microsoft.Storage
```

4. `main.tf`

```
resource "azurerm_resource_group" "main" {
  name = "rg-${var.application_name}-${var.environment_name}"
  location = var.primary_location
}

resource "random_string" "suffix" {
  length = 10
  upper = false
  special = false
}

resource "azurerm_storage_account" "main" {
  name                     = "st${random_string.suffix.result}"
  resource_group_name      = azurerm_resource_group.main.name
  location                 = azurerm_resource_group.main.location
  account_tier             = "Standard"
  account_replication_type = "GRS"
}
```

5. `terraform.tfvars`

```
application_name = "terraform-state"
primary_location = "westus3"
```

6. `versions.tf`

```
# We strongly recommend using the required_providers block to set the
# Azure Provider source and version being used
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "=5.0.0"
    }
    random = {
      source = "hashicorp/random"
      version = "~> 3.9.1"
    }
  }
}

# Configure the Microsoft Azure Provider
provider "azurerm" {
  features {}
}
```

7. Deploy:

```
terraform init

terraform apply -var-file ./env/prod.tfvars
```

### Construct a Terraform State Environment
1. `terraform workspace list`
2. `terraform workspace new dev`
3. `terraform workspace list`
4. Deploy

```
terraform init
terraform apply -var-file ./env/dev.tfvars
```

### Constructing a Blob Storage Container for Terraform State Files
1. Blob storage container - to save terraform state
2. `main.tf`

```
resource "azurerm_storage_container" "tfstate" {
  name                  = "tfstate"
  storage_account_id    = azurerm_storage_account.main.id
  container_access_type = "private"
}
```

	1. `terraform apply -var-file ./env/dev.tfvars`
3. `terraform workspace select default`
	1. `terraform apply -var-file ./env/prod.tfvars`

### Resource Naming Convention Abbreviations
1. List of prefixes to use based on resource type
2. Search: 'azure naming convention prefix abbreviations'
	1. Abbreviation recommendations for Azure resources

### Configure Terraform Remote State with an Azure Storage Backend
1. New Lab: `Lab3`
	1. Backend is only responsible for storing terraform state
		1. Each provider has a backend to store terraform state
2. Search: Azurerm backend on `registry.terraform.io` - [https://developer.hashicorp.com/terraform/language/backend/azurerm#microsoft-entra-id](https://developer.hashicorp.com/terraform/language/backend/azurerm#microsoft-entra-id)
	1. `key` - Unique id for terraform workspace state file (for every intance of our solution)
3. `versions.tf`

```
# We strongly recommend using the required_providers block to set the
# Azure Provider source and version being used
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "=5.0.0"
    }
    random = {
      source = "hashicorp/random"
      version = "~> 3.9.1"
    }
  }
  backend "azurerm" {
    resource_group_name = "rg-terraform-state-dev"
    storage_account_name = "sti2s6v44too"
    container_name = "tfstate"
    key = "observability-dev"
  }
}

# Configure the Microsoft Azure Provider
provider "azurerm" {
  features {}
}
```

4. `variables.tf`

```
variable application_name {
  type = string
}

variable environment_name {
  type = string
}

variable "primary_location" {
  type = string
}
```

5. `terraform.tfvars`

```
application_name = "observability"
primary_location = "westus3"
```

6. `env/dev.tfvars`

```
environment_name = "dev"
```

7. `main.tf`

```
resource "azurerm_resource_group" "main" {
  name = "rg-${var.application_name}-${var.environment_name}"
  location = var.primary_location
}
```

8. `terraform init`
	1. Stores state file in the backend
		1. A copy is stored in `.terraform/terraform.tfstate`
	2. `observability-dev` - portal
		1. Edit
			1. Empty file
9. Set subscription id: `export ARM_SUBSCRIPTION_ID=...`
10. `terraform apply -var-file ./env/dev.tfvars`
	1. `observability-dev`
		1. Only people with access to portal have access to the file
			1. We need to protect it on the portal also using a security profile

### Whiteboard: Terraform State Backend Deep Dive
1. Subscription
	1. `rg-terraform-state-dev`
		1. `st<random-string>` (storage account)
			1. `tfstate` (container)
2. Terraform by default connects to storage account over the internet
	1. Using backend configuration
		1. Azure backend
		2. Where is the backend?
			1. Resource group
			2. Storage account
			3. Blob storage container
			4. Backend key
				1. Unique id for a terraform workspace (per environment)
					1. Where in the storage container the state file lives - makes the physical file name
				2. A combo of application name and environment

### Setup Azure Log Analytics Workspace
1. Search: log analytics workspace - [https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/log_analytics_workspace](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/log_analytics_workspace)

```
resource "azurerm_log_analytics_workspace" "main" {
  name                = "log-${var.application_name}-${var.environment_name}"
  location            = azurerm_resource_group.main.location
  resource_group_name = azurerm_resource_group.main.name
  sku                 = "PerGB2018"
  retention_in_days   = 30
}
```

2. `az provider register --namespace Microsoft.OperationalInsights`
2. `terraform apply -var-file ./env/dev.tfvars`
3. `log-observability-dev`

### Whiteboard: Compartmentalizing Shared Services like Observability
1. Observibiilty stack: Logs, metrics, ...
	1. Contexts
		1. Enterprise-wide angle
		2. Platform engineering angle3
		3. Individual application workload angle
	2. Observability stack will be used by multiple components (shared across deployments)
		1. We want it shared because we want a common timeline across services
2. One observability stack per application (shared by multiple components)
3. Enterprise-wide observability stack
	1. Different apps share
	2. Stakeholders
		1. EA
		2. SecOps team
		3. Incident management
			1. They need access to a broader segment of enterprise application portfolio
	3. Compartmentalization
		1. a single application can send to its resource group

### Construct a Local Runner
1. To configure Terraform to use the correct backend state and context
	1. Solution: Script
		1. Boilerplate to set the context
2. `Lab3`
3. `env/dev.tfvars`

```
```

4. `main.tf`

```
resource "azurerm_resource_group" "main" {
  name = "rg-${var.application_name}-${var.environment_name}"
  location = var.primary_location
}

resource "azurerm_log_analytics_workspace" "main" {
  name                = "log-${var.application_name}-${var.environment_name}"
  location            = azurerm_resource_group.main.location
  resource_group_name = azurerm_resource_group.main.name
  sku                 = "PerGB2018"
  retention_in_days   = 30
}
```

5. `outputs.tf`

```
```

6. `terraform.tfvars`

```
primary_location = "westus3"
```

7. `variables.tf`

```
variable application_name {
  type = string
}

variable environment_name {
  type = string
}

variable "primary_location" {
  type = string
}
```

8. `varsions.tf`

```
# We strongly recommend using the required_providers block to set the
# Azure Provider source and version being used
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "=5.0.0"
    }
    random = {
      source = "hashicorp/random"
      version = "~> 3.9.1"
    }
  }
  backend "azurerm" {
  }
}

# Configure the Microsoft Azure Provider
provider "azurerm" {
  features {}
}
```

9. `.debug-dev.sh`

```
# set the subscription
export ARM_SUBSCRITPTION_ID="135e59de-2f16-4f7f-9636-7166562f25be"

# set the application / environment
export TF_VAR_application_name="observability"
export TF_VAR_environment_name="dev"

# set the backend
export BACKEND_RESOURCE_GROUP="rg-terraform-state-dev"
export BACKEND_STORAGE_ACCOUNT="sti2s6v44too"
export BACKEND_STORAGE_CONTAINER="tfstate"
export BACKEND_KEY="${TF_VAR_application_name}-${TF_VAR_environment_name}"

# run terraform
terraform init \
  -backend-config="resource_group_name=${BACKEND_RESOURCE_GROUP}" \
  -backend-config="storage_account_name=${BACKEND_STORAGE_ACCOUNT}" \
  -backend-config="container_name=${BACKEND_STORAGE_CONTAINER}" \
  -backend-config="key=${BACKEND_KEY}"

terraform $* # all input parameters

rm -rf .terraform
```

10. `.debug-prod.sh`

```
# set the subscription
export ARM_SUBSCRITPTION_ID="135e59de-2f16-4f7f-9636-7166562f25be"

# set the application / environment
export TF_VAR_application_name="observability"
export TF_VAR_environment_name="prod"

# set the backend
export BACKEND_RESOURCE_GROUP="rg-terraform-state-prod"
export BACKEND_STORAGE_ACCOUNT="stygbtvj4q8a"
export BACKEND_STORAGE_CONTAINER="tfstate"
export BACKEND_KEY="${TF_VAR_application_name}-${TF_VAR_environment_name}"

# run terraform
terraform init \
  -backend-config="resource_group_name=${BACKEND_RESOURCE_GROUP}" \
  -backend-config="storage_account_name=${BACKEND_STORAGE_ACCOUNT}" \
  -backend-config="container_name=${BACKEND_STORAGE_CONTAINER}" \
  -backend-config="key=${BACKEND_KEY}"

terraform $* # all input parameters

rm -rf .terraform # Clean up will save disk space
```

11. Deploy:

```
chmod +x ./.debug-dev.sh
./.debug-dev.sh plan
./.debug-dev.sh apply
```

```
chmod +x ./.debug-prod.sh
./.debug-prod.sh plan
./.debug-prod.sh apply
```

### Construct an Azure KeyVault
1. `Lab4`
2. `env/dev.tfvars`

```
environment_name = "dev"
```

3. `env/prod.tfvars`

```
environment_name = "prod"
```

4. `main.tf`

```
resource "azurerm_resource_group" "main" {
  name = "rg-${var.application_name}-${var.environment_name}"
  location = var.primary_location
}
```

5. `outputs.tf`

```
```

6. `terraform.tfvars`

```
application_name = "devops"
primary_location = "westus3"
```

7. `variables.tf`

```
variable application_name {
  type = string
}

variable environment_name {
  type = string
}

variable "primary_location" {
  type = string
}
```

8. `versions.tf`

```
# We strongly recommend using the required_providers block to set the
# Azure Provider source and version being used
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "=5.0.0"
    }
    random = {
      source = "hashicorp/random"
      version = "~> 3.9.1"
    }
  }
  backend "azurerm" {
    resource_group_name = "rg-terraform-state-dev"
    storage_account_name = "sti2s6v44too"
    container_name = "tfstate"
    key = "devops-dev"
  }
}

# Configure the Microsoft Azure Provider
provider "azurerm" {
  features {}
}
```

9. `terraform init`
10. `terraform apply -var-file ./env/dev.tfvars`
11. Search: keyvault
12. `main.tf`

```
resource "azurerm_resource_group" "main" {
  name = "rg-${var.application_name}-${var.environment_name}"
  location = var.primary_location
}

resource "random_string" "keyvault_suffix" {
  length = 6
  upper = false
  special = false
}

resource "azurerm_key_vault" "main" {
  name                        = "kv-${var.application_name}-${var.environment_name}-${random_string.keyvault_suffix.result}"
  location                    = azurerm_resource_group.main.location
  resource_group_name         = azurerm_resource_group.main.name
  rbac_authorization_enabled  = false
  tenant_id                   = "86b6f4bb-c58f-44b0-8a2a-f39c4305bf5f" # All Azure Keyvaults are tied to an entra-id tenant. Microsoft Entra ID
  sku_name = "standard"
}
```

	1. Keyvault needs to be globally unique
	2. `az provider register --namespace Microsoft.KeyVault`
	3. `terraform apply -var-file ./env/dev.tfvars`

### Get the Current Terraform User Context
1. Datasource to access client info: subscription, entra id tenant (we have authenticated with)
	1. Avoids hardcoding
2. In most cases we want the keyvault to be tied to the tenant in which the keyvault is provisioned
3. `azure_client_config` (under base)
4. `main.tf`

```
resource "azurerm_resource_group" "main" {
  name = "rg-${var.application_name}-${var.environment_name}"
  location = var.primary_location
}

resource "random_string" "keyvault_suffix" {
  length = 6
  upper = false
  special = false
}

data "azurerm_client_config" "current" { 
} # Looks at the current authentication context of the current Azure provider

resource "azurerm_key_vault" "main" {
  name                        = "kv-${var.application_name}-${var.environment_name}-${random_string.keyvault_suffix.result}"
  location                    = azurerm_resource_group.main.location
  resource_group_name         = azurerm_resource_group.main.name
  rbac_authorization_enabled  = false
  tenant_id                   = data.azurerm_client_config.current.tenant_id # All Azure Keyvaults are tied to an entra-id tenant. Microsoft Entra ID
  sku_name = "standard"
}
```

### Construct an Azure Role Assignment
1. Role assignment
	1. Grant user or machine identities access to certain services we provision with Azure
		1. Certain services have data plane
			1. Azure KeyVault - we need certain permissions for CRUD
2. ID used by Terraform has sufficient access within the key-vault
3. Search: `role_assignment`
	1. `azurerm_role_assignment` - a generic resource that can be applied to any other resource or scope
		1. Three pieces
			1. Who has access? `principal_id` (human or machine)
			2. What role (set of permissions)? `role_definition_name`
			3. What is the context in which the entity has the specified role? `scope` (keep it as narrow as possible)
				1. Individual resource
				2. Resource group
				3. Subscription
				4. Management group
4. `main.tf`

```
resource "azurerm_role_assignment" "terraform_user" {
  scope                = azurerm_key_vault.main.id
  role_definition_name = "Key Vault Administrator"
  principal_id         = data.azurerm_client_config.current.object_id
}
```

	1. Built-in role definitions:
		1. Search: Azure built-in keyvault roles
	2. `terraform apply -var-file ./env/dev.tfvars`
	3. Verification:
		1. `kv-devops-dev-<random>`
			1. Key Vault Administrator: `<current-user>`
			2. Resource-level permission

### Enable RBAC on KeyVault
1. Two ways to manage access
	1. Access policies - KeyVault's internal mechanism to grant permissions within a KeyVault
		1. Only way earlier
	2. Azure RBAC
		1. Grant access using Azure role assignments (previous lecture)
		2. Needs enabling the feature (default is access policies)
2. `azurerm_key_vault`
3. `azurerm_key_vault_access_policy` - specific to KeyVault
4. Enabling Azure RBAC: `rbac_authorization_enabled`

```
resource "azurerm_key_vault" "main" {
  name                        = "kv-${var.application_name}-${var.environment_name}-${random_string.keyvault_suffix.result}"
  location                    = azurerm_resource_group.main.location
  resource_group_name         = azurerm_resource_group.main.name
  rbac_authorization_enabled  = true
  tenant_id                   = data.azurerm_client_config.current.tenant_id # All Azure Keyvaults are tied to an entra-id tenant. Microsoft Entra ID
  sku_name = "standard"
}
```

### Construct a Local Runner
1. `env/dev.tfvars`

```
```

2. `env/prod.tfvars`

```
```

3. `.debug-dev.sh`

```
# set the subscription
export ARM_SUBSCRITPTION_ID="135e59de-2f16-4f7f-9636-7166562f25be"

# set the application / environment
export TF_VAR_application_name="devops"
export TF_VAR_environment_name="dev"

# set the backend
export BACKEND_RESOURCE_GROUP="rg-terraform-state-dev"
export BACKEND_STORAGE_ACCOUNT="sti2s6v44too"
export BACKEND_STORAGE_CONTAINER="tfstate"
export BACKEND_KEY="${TF_VAR_application_name}-${TF_VAR_environment_name}"

# run terraform
terraform init \
  -backend-config="resource_group_name=${BACKEND_RESOURCE_GROUP}" \
  -backend-config="storage_account_name=${BACKEND_STORAGE_ACCOUNT}" \
  -backend-config="container_name=${BACKEND_STORAGE_CONTAINER}" \
  -backend-config="key=${BACKEND_KEY}"

terraform $* # all input parameters

rm -rf .terraform
```

4. `.debug-prod.sh`

```
# set the subscription
export ARM_SUBSCRITPTION_ID="135e59de-2f16-4f7f-9636-7166562f25be"

# set the application / environment
export TF_VAR_application_name="devops"
export TF_VAR_environment_name="prod"

# set the backend
export BACKEND_RESOURCE_GROUP="rg-terraform-state-prod"
export BACKEND_STORAGE_ACCOUNT="stygbtvj4q8a"
export BACKEND_STORAGE_CONTAINER="tfstate"
export BACKEND_KEY="${TF_VAR_application_name}-${TF_VAR_environment_name}"

# run terraform
terraform init \
  -backend-config="resource_group_name=${BACKEND_RESOURCE_GROUP}" \
  -backend-config="storage_account_name=${BACKEND_STORAGE_ACCOUNT}" \
  -backend-config="container_name=${BACKEND_STORAGE_CONTAINER}" \
  -backend-config="key=${BACKEND_KEY}"

terraform $* # all input parameters

rm -rf .terraform # Clean up will save disk space
```

5. `versions.tf`

```
# We strongly recommend using the required_providers block to set the
# Azure Provider source and version being used
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "=5.0.0"
    }
    random = {
      source = "hashicorp/random"
      version = "~> 3.9.1"
    }
  }
  backend "azurerm" {
  }
}

# Configure the Microsoft Azure Provider
provider "azurerm" {
  features {}
}
```

6. Deploy:

```
chmod +x ./.debug-dev.sh
chmod +x ./.debug-prod.sh

./.debug-dev.sh apply
./.debug-prod.sh apply
```

### Whiteboard: DevOps Infrastructure and Infrastructure Composition
1. Data plane
	1. KeyVault has one
		1. Resources that live inside
			1. Not managed by ARM
			2. Needs explicit access to manipulate data
2. Control plane
	1. ARM
3. Data-plane resources
	1. Secrets
	2. Keys
	3. Certificates
	4. ...
4. Workload
	1. Leverages
		1. Observability stack
		2. DevOps infrastructure
			1. Secrets management
			2. Terraform state
5. Infrastructure can be broken down into different chunks of functionality
6. Hooking DevOps to Observability

### Construct an Azure Monitor Diagnostic Setting
1. Attaching Azure monitor to the resources
2. Portal
	1. `kv-devops-dev-<random>`
		1. Monitoring
			1. Alerts
			2. Metrics
			3. Diagnostic settings
				1. Manually set click ops
			4. Logs
			5. Insights
			6. Workbooks
3. registry.terraform.io
	1. `azurerm_monitor_diagnostic_setting`
4. Resource vs Data source
	1. Data source - If a resource is provisioned by someone else and we know that it exists
		1. We just want to reference it
	2. `id` - used by ARM to uniquely identify a resource
		1. Fully qualified name
	3. `workspace_id` - Workspace id
5. `main.tf`

```
resource "azurerm_resource_group" "main" {
  name = "rg-${var.application_name}-${var.environment_name}"
  location = var.primary_location
}

resource "random_string" "keyvault_suffix" {
  length = 6
  upper = false
  special = false
}

data "azurerm_client_config" "current" { 
} # Looks at the current authentication context of the current Azure provider

resource "azurerm_key_vault" "main" {
  name                        = "kv-${var.application_name}-${var.environment_name}-${random_string.keyvault_suffix.result}"
  location                    = azurerm_resource_group.main.location
  resource_group_name         = azurerm_resource_group.main.name
  rbac_authorization_enabled  = true
  tenant_id                   = data.azurerm_client_config.current.tenant_id # All Azure Keyvaults are tied to an entra-id tenant. Microsoft Entra ID
  sku_name = "standard"
}

resource "azurerm_role_assignment" "terraform_user" {
  scope                = azurerm_key_vault.main.id
  role_definition_name = "Key Vault Administrator"
  principal_id         = data.azurerm_client_config.current.object_id
}

data "azurerm_log_analytics_workspace" "observability" {
  name = "log-observability-dev"
  resource_group_name = "rg-observability-dev"
}

resource "azurerm_monitor_diagnostic_setting" "main" {
  name               = "diag-${var.application_name}-${var.environment_name}-${random_string.keyvault_suffix.result}"
  target_resource_id = azurerm_key_vault.main.id

  log_analytics_workspace_id = data.azurerm_log_analytics_workspace.observability.id

  enabled_log {
    category = "AuditEvent"
  }

  enabled_metric {
    category = "AllMetrics"
  }
}
```

6. `az provider register --namespace Microsoft.Insights`
6. `./.debug-dev.sh apply`

### Use the Azure Portal to Discover Azure Monitor Diagnostic Setting Configuration
1. Portal
	1. Pass different values for logs
		1. Portal:
			1. Key vault
				1. Monitoring > Diagnostic settings
					1. Add or Edit
						1. JSON View - ARM template code
2. `main.tf`

```
resource "azurerm_monitor_diagnostic_setting" "main" {
  name               = "diag-${var.application_name}-${var.environment_name}-${random_string.keyvault_suffix.result}"
  target_resource_id = azurerm_key_vault.main.id

  log_analytics_workspace_id = data.azurerm_log_analytics_workspace.observability.id

  enabled_log {
    category = "AuditEvent"
  }

  enabled_log {
    category = "AzurePolicyEvaluationDetails"
  }

  enabled_metric {
    category = "AllMetrics"
  }
}
```

```
resource "azurerm_monitor_diagnostic_setting" "main" {
  name               = "diag-${var.application_name}-${var.environment_name}-${random_string.keyvault_suffix.result}"
  target_resource_id = azurerm_key_vault.main.id

  log_analytics_workspace_id = data.azurerm_log_analytics_workspace.observability.id

  enabled_log {
    category_group = "audit"
  }

  enabled_log {
    category_group = "allLogs"
  }

  enabled_metric {
    category = "AllMetrics"
  }
}
```

3. Use portal and Terraform registry to understand how to set different options.

## Section 7: Automate Foundational Azure Compute and Networking Services with Terraform
### Section Introduction
1. Core Azure networking and compute services
	1. Virtual network
	2. Virtual machine

### Construct a Virtual Network
1. `Lab5`
	1. Documentation: `azurerm_virtual_network`
		1. It is multi-modal
			1. Subnets can be nested blocks or independent resources
				1. Use standalone whenever possible
					1. Reason: We can reference an existing resource and add items to it
						1. We don't run into issues when we manage the original resource
2. CIDR - 10.0.0.0/16 (2^(32 - 16) = 65,536 addresses in the network)
	1. Happy medium: 10.0.0.0/22 = 1024 addresses
	2. We don't want a common addresses space
		1. Peering can cause conflicts
			1. Solution: IP address management solution - organization-wide
		2. Pick something different: `10.39.0.0/22`
3. `main.tf`

```
resource "azurerm_resource_group" "main" {
  name = "rg-${var.application_name}-${var.environment_name}"
  location = var.primary_location
}

resource "azurerm_virtual_network" "main" {
  name                = "vnet-${var.application_name}-${var.environment_name}"
  location            = azurerm_resource_group.main.location
  resource_group_name = azurerm_resource_group.main.name
  address_space       = ["10.39.0.0/22"]
}
```

	1. `NetworkWatcherRG` - created automatically
		1. Set up
			1. Required for VN
		2. Stays even with `terraform destroy`
		3. It doesn't reflect the code
			1. Not predictable
4. `az provider register --namespace Microsoft.Network`
5. Force-unlock if required: `./.debug-dev.sh force-unlock 67e8ca2a-04b0-9343-b89c-4422c26f693a`
6. `./.debug-dev.sh apply`

### Construct a Subnet
1. `azurerm_subnet`
2. `main.tf`

```
resource "azurerm_resource_group" "main" {
  name = "rg-${var.application_name}-${var.environment_name}"
  location = var.primary_location
}

resource "azurerm_virtual_network" "main" {
  name                = "vnet-${var.application_name}-${var.environment_name}"
  location            = azurerm_resource_group.main.location
  resource_group_name = azurerm_resource_group.main.name
  address_space       = ["10.39.0.0/22"]
}

// 10.39.0.0/24
resource "azurerm_subnet" "alpha" {
  name                 = "snet-alpha"
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = ["10.39.0.0/24"]
}

// 10.39.1.0/24
resource "azurerm_subnet" "bravo" {
  name                 = "snet-bravo"
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = ["10.39.1.0/24"]
}

// 10.39.2.0/24
resource "azurerm_subnet" "charlie" {
  name                 = "snet-charlie"
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = ["10.39.2.0/24"]
}

// 10.39.3.0/24
resource "azurerm_subnet" "delta" {
  name                 = "snet-delta"
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = ["10.39.3.0/24"]
}
```

	1. 5 IP addresses are reserved for Azure per subnet

### Use CIDR Subnet
1. CIDR subnet - Used to calculate subnet address spaces from a base address space
	1. Advantages
		1. More manageable infra code
		2. No need for humans to author
2. `env.dev.tfvars`

```
base_address_space = "10.39.0.0/22"
```

3. `main.tf`

```
resource "azurerm_resource_group" "main" {
  name = "rg-${var.application_name}-${var.environment_name}"
  location = var.primary_location
}

resource "azurerm_virtual_network" "main" {
  name                = "vnet-${var.application_name}-${var.environment_name}"
  location            = azurerm_resource_group.main.location
  resource_group_name = azurerm_resource_group.main.name
  address_space       = [var.base_address_space]
}

locals {
  alpha_address_space = cidrsubnet(var.base_address_space, 2, 0)
  bravo_address_space = cidrsubnet(var.base_address_space, 2, 1)
  charlie_address_space = cidrsubnet(var.base_address_space, 2, 2)
  delta_address_space = cidrsubnet(var.base_address_space, 2, 3)
}

// 10.39.0.0/24
resource "azurerm_subnet" "alpha" {
  name                 = "snet-alpha"
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = [local.alpha_address_space]
}

// 10.39.1.0/24
resource "azurerm_subnet" "bravo" {
  name                 = "snet-bravo"
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = [local.bravo_address_space]
}

// 10.39.2.0/24
resource "azurerm_subnet" "charlie" {
  name                 = "snet-charlie"
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = [local.charlie_address_space]
}

// 10.39.3.0/24
resource "azurerm_subnet" "delta" {
  name                 = "snet-delta"
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = [local.delta_address_space]
}
```

4. `variables.tf`

```
variable application_name {
  type = string
}

variable environment_name {
  type = string
}

variable "primary_location" {
  type = string
}

variable "base_address_space" {
  type = string
}
```

5. `./.debug-dev.sh apply -var-file ./env/dev.tfvars`
6. `./.debug-dev.sh console`
	1. `local.alpha_address_space`
	2. `local.delta_address_space`

### Switchbacking
1. Switchbacking - finding a safer route up the mountain by making zig-zags. There are rest-points
	1. Similarly, IaC cannot be done in one stretch from point A to point B. We need stops in between
2. What if we change our address space?
	1. `10.39.0.0` to `10.40.0.0`
		1. Does it work? It doesn't work
			1. Implicit relationships sometimes cannot be figured out by Terraform
				1. We cannot change the VN address without changing subnets
					1. Alternative:
						1. Delete subnets temporarily
						2. Run Terraform apply
						3. Change the address of VNet
						4. Add the subnets back
						5. Run Terraform apply

### Drop Construct
1. `./.debug-dev.sh destroy`
	1. Not recommended if we have dependencies within the network
2. `./.debug-dev.sh apply -var-file ./env/dev.tfvars`
3. Production:
	1. Works for blue-green deployment

### Construct a Network Security Group
1. Security group: To allow or block traffic
	1. They can be attached to one or more subnets
2. `registry.terraform.io`
	1. Search: `azurerm_network_security_group`
3. Name: Should reflect the functionality (not the subnet)
	1. Web traffic (HTTP/HTTPS)
	2. DB traffic
	3. SSH
4. `main.tf`

```
resource "azurerm_network_security_group" "remote_access" {
  name                = "nsg-${var.application_name}-${var.environment_name}-remote-access"
  location            = azurerm_resource_group.main.location
  resource_group_name = azurerm_resource_group.main.name

  security_rule {
    name                       = "ssh"
    priority                   = 100
    direction                  = "Inbound"
    access                     = "Allow"
    protocol                   = "Tcp"
    source_port_range          = "*"
    destination_port_range     = "22"
    source_address_prefix      = "*"
    destination_address_prefix = "*"
  }
}
```

5. `registry.terraform.io`
	1. Search: `azurerm_subnet_network_security_group_association`
6. `main.tf`

```
resource "azurerm_subnet_network_security_group_association" "alpha_remote_access" {
  subnet_id                 = azurerm_subnet.alpha.id
  network_security_group_id = azurerm_network_security_group.remote_access.id
}
```

7. Needs it be made more secure

### Lookup My IP Address
1. Making it more secure:
	1. Source address: Find out my IP address and set it as a prefix
		1. Google.com: What is my public ip address
2. `main.tf`

```
resource "azurerm_subnet_network_security_group_association" "alpha_remote_access" {
  subnet_id                 = azurerm_subnet.alpha.id
  network_security_group_id = azurerm_network_security_group.remote_access.id
}
```

3. Public IP can change. How to automate it.
	1. HTTP data source
4. `main.tf`

```
resource "azurerm_network_security_group" "remote_access" {
  name                = "nsg-${var.application_name}-${var.environment_name}-remote-access"
  location            = azurerm_resource_group.main.location
  resource_group_name = azurerm_resource_group.main.name

  security_rule {
    name                       = "ssh"
    priority                   = 100
    direction                  = "Inbound"
    access                     = "Allow"
    protocol                   = "Tcp"
    source_port_range          = "*"
    destination_port_range     = "22"
    source_address_prefix      = chomp(data.http.my_ip.response_body)
    destination_address_prefix = "*"
  }
}

resource "azurerm_subnet_network_security_group_association" "alpha_remote_access" {
  subnet_id                 = azurerm_subnet.alpha.id
  network_security_group_id = azurerm_network_security_group.remote_access.id
}

data "http" "my_ip" {
  url = "https://api.ipify.org"
}
```

### Construct Public IP Address
1. `Lab6`
2. `./env/dev.tfvars` & `./env/prod.tfvars`

```
```

3. `.debug-dev.sh`

```
# set the subscription
export ARM_SUBSCRITPTION_ID="135e59de-2f16-4f7f-9636-7166562f25be"

# set the application / environment
export TF_VAR_application_name="linuxvm"
export TF_VAR_environment_name="dev"

# set the backend
export BACKEND_RESOURCE_GROUP="rg-terraform-state-dev"
export BACKEND_STORAGE_ACCOUNT="sti2s6v44too"
export BACKEND_STORAGE_CONTAINER="tfstate"
export BACKEND_KEY="${TF_VAR_application_name}-${TF_VAR_environment_name}"

# run terraform
terraform init \
  -backend-config="resource_group_name=${BACKEND_RESOURCE_GROUP}" \
  -backend-config="storage_account_name=${BACKEND_STORAGE_ACCOUNT}" \
  -backend-config="container_name=${BACKEND_STORAGE_CONTAINER}" \
  -backend-config="key=${BACKEND_KEY}"

terraform $* # all input parameters

rm -rf .terraform
```

4. `.debug-prod.sh`

```
# set the subscription
export ARM_SUBSCRITPTION_ID="135e59de-2f16-4f7f-9636-7166562f25be"

# set the application / environment
export TF_VAR_application_name="linuxvm"
export TF_VAR_environment_name="prod"

# set the backend
export BACKEND_RESOURCE_GROUP="rg-terraform-state-prod"
export BACKEND_STORAGE_ACCOUNT="stygbtvj4q8a"
export BACKEND_STORAGE_CONTAINER="tfstate"
export BACKEND_KEY="${TF_VAR_application_name}-${TF_VAR_environment_name}"

# run terraform
terraform init \
  -backend-config="resource_group_name=${BACKEND_RESOURCE_GROUP}" \
  -backend-config="storage_account_name=${BACKEND_STORAGE_ACCOUNT}" \
  -backend-config="container_name=${BACKEND_STORAGE_CONTAINER}" \
  -backend-config="key=${BACKEND_KEY}"

terraform $* # all input parameters

rm -rf .terraform # Clean up will save disk space
```

5. `main.tf`

```
resource "azurerm_resource_group" "main" {
  name = "rg-${var.application_name}-${var.environment_name}"
  location = var.primary_location
}
```

6. `terraform.tfvars`

```
primary_location = "westus3"
```

7. `variables.tf`

```
variable application_name {
  type = string
}

variable environment_name {
  type = string
}

variable "primary_location" {
  type = string
}
```

8. `versions.tf`

```
# We strongly recommend using the required_providers block to set the
# Azure Provider source and version being used
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "=5.0.0"
    }
    random = {
      source = "hashicorp/random"
      version = "~> 3.9.1"
    }
  }
  backend "azurerm" {
  }
}

# Configure the Microsoft Azure Provider
provider "azurerm" {
  features {}
}
```

9. `azurerm_public_ip`
10. `main.tf`

```
resource "azurerm_public_ip" "vm1" {
  name                = "pip-${var.application_name}-${var.environment_name}-vm1"
  resource_group_name = azurerm_resource_group.main.name
  location            = azurerm_resource_group.main.location
  allocation_method   = "Static"
}
```

11. We can associate a public IP address as an internet-accessible end-point that we can connect with something in Azure

### Construct Network Interface Card
1. NIC - Virtual Network Interface Card
	1. Used to connect the VM to the IP address
2. Search: `azurerm_network_interface`
3. `main.tf`

```
resource "azurerm_resource_group" "main" {
  name = "rg-${var.application_name}-${var.environment_name}"
  location = var.primary_location
}

resource "azurerm_public_ip" "vm1" {
  name                = "pip-${var.application_name}-${var.environment_name}-vm1"
  resource_group_name = azurerm_resource_group.main.name
  location            = azurerm_resource_group.main.location
  allocation_method   = "Static"
}

data "azurerm_subnet" "alpha" {
  name = "snet-alpha"
  virtual_network_name = "vnet-network-dev"
  resource_group_name = "rg-network-dev"
}

resource "azurerm_network_interface" "vm1" {
  name                = "example-nic"
  location            = azurerm_resource_group.main.location
  resource_group_name = azurerm_resource_group.main.name

  ip_configuration {
    name                          = "public"
    subnet_id                     = data.azurerm_subnet.alpha.id
    private_ip_address_allocation = "Dynamic" # Should be in the range of the subnet
    public_ip_address_id = azurerm_public_ip.vm1.id
  }
}
```

4. NIC
	1. It is on two network
		1. Public internet (via public IP)
			1. Allows us to route external traffic using the public IP address
		2. Private Virtual Network (via private IP)
			1. Allows us to route internal traffic using the private IP address

### Construct an SSH Key
1. ssh key - tsl provider - tls private key resource
	1. New ssh keys can be created
2. Search: `tls_private_key`
	1. RSA
3. `main.tf`

```
# RSA key of size 4096 bits
resource "tls_private_key" "vm1" {
  algorithm = "RSA"
  rsa_bits  = 4096
}
```

4. `./.debug-dev.sh apply -var-file ./env/dev.tfvars`
	1. `./.debug-dev.sh console`
	
	```
	tls_private_key.vm1
	tls_private_key.vm1.public_key_openssh
	```

### Construct a Linux Virtual Machine
1. registry.terraform.io
	1. `azurerm_linux_virtual_machine` (`azurerm_virtual_machine` - old)
		1. `source_image_reference` - looks up a VM image in the Azure marketplace and uses it as the start
2. `main.tf`

```
resource "azurerm_linux_virtual_machine" "vm1" {
  name                = "vm1${var.application_name}${var.environment_name}"
  resource_group_name = azurerm_resource_group.main.name
  location            = azurerm_resource_group.main.location
  size                = "Standard_D2s_v7"
  admin_username      = "adminuser"
  network_interface_ids = [
    azurerm_network_interface.vm1.id,
  ]

  admin_ssh_key {
    username   = "adminuser"
    public_key = tls_private_key.vm1.public_key_openssh
  }

  os_disk {
    caching              = "ReadWrite"
    storage_account_type = "Standard_LRS"
  }

  source_image_reference {
    publisher = "Canonical"
    offer     = "0001-com-ubuntu-server-jammy"
    sku       = "22_04-lts-gen2"
    version   = "latest"
  }
}
```

3. `az provider register --namespace Microsoft.Compute`
4. `./.debug-dev.sh apply -var-file ./env/dev.tfvars`
5. `az vm list-skus --location westus3 --size Standard_D --all --output table`
	1. [https://learn.microsoft.com/en-us/azure/azure-resource-manager/troubleshooting/error-sku-not-available?tabs=azure-cli](https://learn.microsoft.com/en-us/azure/azure-resource-manager/troubleshooting/error-sku-not-available?tabs=azure-cli)

### Construct Linux VM Local SSH
1. We need to get the SSH key onto the machine
2. `main.tf`

```
resource "local_file" "private_key" {
  content = tls_private_key.vm1.private_key_pem
  filename = pathexpand("~/.ssh/vm1")
  file_permission = "0600"
}

resource "local_file" "public_key" {
  content = tls_private_key.vm1.public_key_openssh
  filename = pathexpand("~/.ssh/vm1.pub")
}
```

3. `outputs.tf`

```
output "public_ip_address" {
  value = azurerm_public_ip.vm1.ip_address
}
```

4. Connect:

```
ssh -i ~/.ssh/vm1 adminuser@57.154.21.240
```

### VM Connection Options
1. What if multiple people need addess to the VM?
	1. Options:
		1. Portal:
			1. Connect
				1. SSH
				2. RDP
				3. Native tools
				4. Azure CLI
			2. Connect via Bastion
				1. Service
					1. Indirect remote access
						1. No need to open a port
					2. We can connect to the VM using HTTPS

### Reorganize Subnets
1. Bastion needs a subnet for itself with a special name
2. Use apex subnet (inital addresses) - recommendation
3. Change `alpha` to `bravo` for SSH in `main.tf`

```
data "azurerm_subnet" "bravo" {
  name = "snet-bravo"
  virtual_network_name = "vnet-network-dev"
  resource_group_name = "rg-network-dev"
}

resource "azurerm_network_interface" "vm1" {
  name                = "example-nic"
  location            = azurerm_resource_group.main.location
  resource_group_name = azurerm_resource_group.main.name

  ip_configuration {
    name                          = "public"
    subnet_id                     = data.azurerm_subnet.bravo.id
    private_ip_address_allocation = "Dynamic" # Should be in the range of the subnet
    public_ip_address_id = azurerm_public_ip.vm1.id
  }
}
```

4. We cannot connect using ssh now.

### Construct a Bastion Host Subnet
1. Removing Subnet Alpha for Azure Bastion
	1. We need fewer than 256 address space
		1. Atleast `/26` = 64 addresses
2. `Lab5/main.tf`

```
resource "azurerm_resource_group" "main" {
  name = "rg-${var.application_name}-${var.environment_name}"
  location = var.primary_location
}

resource "azurerm_virtual_network" "main" {
  name                = "vnet-${var.application_name}-${var.environment_name}"
  location            = azurerm_resource_group.main.location
  resource_group_name = azurerm_resource_group.main.name
  address_space       = [var.base_address_space]
}

locals {
  # alpha_address_space = cidrsubnet(var.base_address_space, 2, 0)
  bastion_address_space = cidrsubnet(var.base_address_space, 4, 0)
  bravo_address_space = cidrsubnet(var.base_address_space, 2, 1)
  charlie_address_space = cidrsubnet(var.base_address_space, 2, 2)
  delta_address_space = cidrsubnet(var.base_address_space, 2, 3)
}

// 10.39.0.0/24
# resource "azurerm_subnet" "alpha" {
#   name                 = "snet-alpha"
#   resource_group_name  = azurerm_resource_group.main.name
#   virtual_network_name = azurerm_virtual_network.main.name
#   address_prefixes     = [local.alpha_address_space]
# }
// 10.39.0.0/26
// Start: 10.39.0.0, End: 10.39.0.63
resource "azurerm_subnet" "bastion" { 
  name                 = "AzureBastionSubnet" # name of the service should match this
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = [local.bastion_address_space]
}


// 10.39.1.0/24
resource "azurerm_subnet" "bravo" {
  name                 = "snet-bravo"
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = [local.bravo_address_space]
}

// 10.39.2.0/24
resource "azurerm_subnet" "charlie" {
  name                 = "snet-charlie"
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = [local.charlie_address_space]
}

// 10.39.3.0/24
resource "azurerm_subnet" "delta" {
  name                 = "snet-delta"
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = [local.delta_address_space]
}

resource "azurerm_network_security_group" "remote_access" {
  name                = "nsg-${var.application_name}-${var.environment_name}-remote-access"
  location            = azurerm_resource_group.main.location
  resource_group_name = azurerm_resource_group.main.name

  security_rule {
    name                       = "ssh"
    priority                   = 100
    direction                  = "Inbound"
    access                     = "Allow"
    protocol                   = "Tcp"
    source_port_range          = "*"
    destination_port_range     = "22"
    source_address_prefix      = chomp(data.http.my_ip.response_body)
    destination_address_prefix = "*"
  }
}

# resource "azurerm_subnet_network_security_group_association" "alpha_remote_access" {
#   subnet_id                 = azurerm_subnet.alpha.id
#   network_security_group_id = azurerm_network_security_group.remote_access.id
# }

data "http" "my_ip" {
  url = "https://api.ipify.org"
}
```

3. Deploy

```
./.debug-dev.sh apply -var-file ./env/dev.tfvars
```

### Construct a Bastion Host
1. Search: `azurerm_bastion_host`
2. `main.tf`

```
resource "azurerm_resource_group" "main" {
  name = "rg-${var.application_name}-${var.environment_name}"
  location = var.primary_location
}

resource "azurerm_virtual_network" "main" {
  name                = "vnet-${var.application_name}-${var.environment_name}"
  location            = azurerm_resource_group.main.location
  resource_group_name = azurerm_resource_group.main.name
  address_space       = [var.base_address_space]
}

locals {
  # alpha_address_space = cidrsubnet(var.base_address_space, 2, 0)
  bastion_address_space = cidrsubnet(var.base_address_space, 4, 0)
  bravo_address_space = cidrsubnet(var.base_address_space, 2, 1)
  charlie_address_space = cidrsubnet(var.base_address_space, 2, 2)
  delta_address_space = cidrsubnet(var.base_address_space, 2, 3)
}

// 10.39.0.0/24
# resource "azurerm_subnet" "alpha" {
#   name                 = "snet-alpha"
#   resource_group_name  = azurerm_resource_group.main.name
#   virtual_network_name = azurerm_virtual_network.main.name
#   address_prefixes     = [local.alpha_address_space]
# }
// 10.39.0.0/26
// Start: 10.39.0.0, End: 10.39.0.63
resource "azurerm_subnet" "bastion" { 
  name                 = "AzureBastionSubnet" # name of the service should match this
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = [local.bastion_address_space]
}

// 10.39.1.0/24
resource "azurerm_subnet" "bravo" {
  name                 = "snet-bravo"
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = [local.bravo_address_space]
}

// 10.39.2.0/24
resource "azurerm_subnet" "charlie" {
  name                 = "snet-charlie"
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = [local.charlie_address_space]
}

// 10.39.3.0/24
resource "azurerm_subnet" "delta" {
  name                 = "snet-delta"
  resource_group_name  = azurerm_resource_group.main.name
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = [local.delta_address_space]
}

# resource "azurerm_network_security_group" "remote_access" {
#   name                = "nsg-${var.application_name}-${var.environment_name}-remote-access"
#   location            = azurerm_resource_group.main.location
#   resource_group_name = azurerm_resource_group.main.name

#   security_rule {
#     name                       = "ssh"
#     priority                   = 100
#     direction                  = "Inbound"
#     access                     = "Allow"
#     protocol                   = "Tcp"
#     source_port_range          = "*"
#     destination_port_range     = "22"
#     source_address_prefix      = chomp(data.http.my_ip.response_body)
#     destination_address_prefix = "*"
#   }
# }

# resource "azurerm_subnet_network_security_group_association" "alpha_remote_access" {
#   subnet_id                 = azurerm_subnet.alpha.id
#   network_security_group_id = azurerm_network_security_group.remote_access.id
# }

data "http" "my_ip" {
  url = "https://api.ipify.org"
}

resource "azurerm_public_ip" "bastion" {
  name                = "pip-${var.application_name}-${var.environment_name}-bastion"
  location            = azurerm_resource_group.main.location
  resource_group_name = azurerm_resource_group.main.name
  allocation_method   = "Static"
  sku                 = "Standard"
}

resource "azurerm_bastion_host" "main" {
  name                = "bas-${var.application_name}-${var.environment_name}"
  location            = azurerm_resource_group.main.location
  resource_group_name = azurerm_resource_group.main.name

  ip_configuration {
    name                 = "configuration"
    subnet_id            = azurerm_subnet.bastion.id
    public_ip_address_id = azurerm_public_ip.bastion.id
  }
}
```

3. Portal

### Store the SSH Key in Key Vault
1. We don't want to connect from local machine
2. Technique: Systematic deconstruction - As we tear something down, we build something else piece by piece.
3. Search: `azurerm_key_vault_secret`

```
resource "azurerm_resource_group" "main" {
  name = "rg-${var.application_name}-${var.environment_name}"
  location = var.primary_location
}

resource "azurerm_public_ip" "vm1" {
  name                = "pip-${var.application_name}-${var.environment_name}-vm1"
  resource_group_name = azurerm_resource_group.main.name
  location            = azurerm_resource_group.main.location
  allocation_method   = "Static"
}

data "azurerm_subnet" "bravo" {
  name = "snet-bravo"
  virtual_network_name = "vnet-network-dev"
  resource_group_name = "rg-network-dev"
}

resource "azurerm_network_interface" "vm1" {
  name                = "example-nic"
  location            = azurerm_resource_group.main.location
  resource_group_name = azurerm_resource_group.main.name

  ip_configuration {
    name                          = "public"
    subnet_id                     = data.azurerm_subnet.bravo.id
    private_ip_address_allocation = "Dynamic" # Should be in the range of the subnet
    public_ip_address_id = azurerm_public_ip.vm1.id
  }
}

# RSA key of size 4096 bits
resource "tls_private_key" "vm1" {
  algorithm = "RSA"
  rsa_bits  = 4096
}

data "azurerm_key_vault" "main" {
  name = "kv-devops-dev-qtrtr1"
  resource_group_name = "rg-devops-dev"
}

resource "azurerm_key_vault_secret" "vm1_ssh_private" {
  name         = "vm1-ssh-private"
  value        = tls_private_key.vm1.private_key_pem
  key_vault_id = data.azurerm_key_vault.main.id
}

resource "azurerm_key_vault_secret" "vm1_ssh_public" {
  name         = "vm1-ssh-public"
  value        = tls_private_key.vm1.public_key_openssh
  key_vault_id = data.azurerm_key_vault.main.id
}

resource "azurerm_linux_virtual_machine" "vm1" {
  name                = "vm1${var.application_name}${var.environment_name}"
  resource_group_name = azurerm_resource_group.main.name
  location            = azurerm_resource_group.main.location
  size                = "Standard_D2s_v7"
  admin_username      = "adminuser"
  network_interface_ids = [
    azurerm_network_interface.vm1.id,
  ]

  admin_ssh_key {
    username   = "adminuser"
    public_key = tls_private_key.vm1.public_key_openssh
  }

  os_disk {
    caching              = "ReadWrite"
    storage_account_type = "Standard_LRS"
  }

  source_image_reference {
    publisher = "Canonical"
    offer     = "0001-com-ubuntu-server-jammy"
    sku       = "22_04-lts-gen2"
    version   = "latest"
  }
}
```

4. Portal: Key vault
	1. Find the keys

### Connect to VM through the Azure Bastion
1. Portal:
	1. VM
		1. Connect via Bastion
			1. Authentication Type: SSH Private Key from Azure Key Vault
			2. Username: adminuser
			3. Azure Key Vault Secret:
				1. Subscription: `pay-as-you-go-2`
				2. Azure Key Vault: `kv-devops-dev-qtrtr1`
				3. Azure Key Vault Secret: `vm1-ssh-private`
			4. Connect
				1. Always allow
			5. Connects to Linux VM
				1. `whoami`
	2. Happens over HTTPS
2. Next level: VPN
	1. More cost
	2. More complex

### Explore Entra ID as an Authentication Option
1. Problem: All users will use the same admin user id and the keys to log into the machine
	1. We lose track of who is logging in
	2. If someone knows the user name and the SSH key, they can gain access
2. We need to know who is logging in and with what credentials
	1. Solution: Entra ID (Formerly Azure AD) authentication
3. How to add entra ID?
	1. By adding VM extensions
		1. For Windows or Linux
		2. They add functionality
4. Portal:	
	1. VM
		1. Settings
			1. Extensions + applications
				1. Add:
					1. Takes you to marketplace
					2. Select: Azure AD based SSH Login
					3. Next
					4. Next
					5. View information template (sometimes available after provisioning)
						1. virtualMachines/extensions
						2. Properties (copy them)
					6. It runs scripts to set up the functionality
		2. System assigned identity
			1. AADSSHLogin requires it
			2. Giving an identity to VM that it can run as
				1. MSI - Managed identity
	2. Click-ops helps us gather the requirements
	3. Security
		1. Identity
			1. System assigned - It generates an entra id application identitity for us
				1. Some platforms use this only
				2. Enable it
					1. Object (principal) ID - facilitates end user authentication with entra id
			2. User assigned - pre-provisioned by user and associated - preferred
	4. Bastion:
		1. Role assignments are required
			1. People need permission
	5. VM:
		1. Role assignment
			1. Virtual Machine User Login
				1. Select yourself
				2. Assign
			2. Virtual Machine Administrator Login
	6. Bastion:
		1. Microsoft Entra ID
			1. Connect
				1. Logs in
					1. `whoami`
						1. The user
	7. Cleanup

### Add System Assigned Managed Identity to a Virtual Machine
1. `Lab6`
2. `main.tf`

```
resource "azurerm_linux_virtual_machine" "vm1" {
  name                = "vm1${var.application_name}${var.environment_name}"
  resource_group_name = azurerm_resource_group.main.name
  location            = azurerm_resource_group.main.location
  size                = "Standard_D2s_v7"
  admin_username      = "adminuser"
  network_interface_ids = [
    azurerm_network_interface.vm1.id,
  ]

  identity {
    type = "SystemAssigned"
  }

  admin_ssh_key {
    username   = "adminuser"
    public_key = tls_private_key.vm1.public_key_openssh
  }

  os_disk {
    caching              = "ReadWrite"
    storage_account_type = "Standard_LRS"
  }

  source_image_reference {
    publisher = "Canonical"
    offer     = "0001-com-ubuntu-server-jammy"
    sku       = "22_04-lts-gen2"
    version   = "latest"
  }
}
```

3. `./.debug-dev.sh apply -var-file ./env/dev.tfvars`

### Enable Entra ID Authentication using a Virtual Machine Extension
1. `registry.terraform.io`
	1. `azurerm_virtual_machine_extension`
		1. Use copied properties
2. `main.tf`

```
resource "azurerm_virtual_machine_extension" "entra_id_login" {
  name                 = "${azurerm_linux_virtual_machine.vm1.name}-AADSSHLoginForLinux"
  virtual_machine_id   = azurerm_linux_virtual_machine.vm1.id
  publisher            = "Microsoft.Azure.ActiveDirectory"
  type                 = "AADSSHLoginForLinux"
  type_handler_version = "1.0"
  auto_upgrade_minor_version = true
}

data "azurerm_client_config" "current" {
}

resource "azurerm_role_assignment" "entra_id_user_login" {
  scope = azurerm_linux_virtual_machine.vm1.id
  role_definition_name = "Virtual Machine User Login"
  principal_id = data.azurerm_client_config.current.object_id
}
```

3. `./.debug-dev.sh apply -var-file ./env/dev.tfvars `
4. Portal:
	1. Connect
	2. Microsoft Entra ID
	3. Connect

## Section 8: Automating Identity & Access Management on Entra ID
### Introducing the Entra ID Terraform Provider "azuread"
1. It is not enough from a long-term point of view
	1. It is not a good practice to assign role assignment to individual users
		1. Solution?
			1. We can assign role assignment to a specific group
				1. Security group over an Entra ID
2. Provider: `azuread` (to manage entra id id provider) (Azure Active Directory)
	1. Search: `azuread` 
		1. Instantiate users and manage them
		2. Reference existing users
		3. Instantiate groups and manage them
		4. Reference existing groups
		5. Applications
			1. ...
	2. `azuread_group`
		1. User permissions
		2. Service principal setup
3. `main.tf`

```
resource "azuread_group" "example" {
  display_name     = "example"
  mail_enabled     = true
  mail_nickname    = "ExampleGroup"
  security_enabled = true
  types            = ["Unified"]

  owners = [
    data.azuread_client_config.current.object_id,
    azuread_user.group_owner.object_id,
  ]
}
```

### Setup the Entra ID Terraform Provider "azuerad"
1. Add `azuread` provider
2. `versions.tf`

```
# We strongly recommend using the required_providers block to set the
# Azure Provider source and version being used
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "=5.0.0"
    }
    azuread = {
      source = "hashicorp/azuread"
      version = "~> 3.2.0"
    }
    random = {
      source = "hashicorp/random"
      version = "~> 3.9.1"
    }
  }
  backend "azurerm" {
  }
}

# Configure the Microsoft Azure Provider
provider "azurerm" {
  features {}
}
```

3. `tenant_id` - if required
	1. `az login` and setting subscription ties the resource to the entra id

### Construct an Entra ID Group
1. `azuread_client_config`
	1. Excludes
		1. No subscription
	2. Includes
		1. Entra ID tenant
		2. Current logged-in user
2. `azurerm_client_config`
	1. Includes
		1. Subscription
		2. Entra ID tenant
		3. Current logged-in user
3. `iam.tf`

```
data "azuread_client_config" "current" {
}

resource "azuread_group" "remote_access_users" {
  display_name     = "${var.application_name}-${var.environment_name}-remote-access-users"
  owners = [data.azuread_client_config.current.object_id]
  security_enabled = true
}
```

4. `./.debug-dev.sh apply -var-file ./env/dev.tfvars`
	1. `./.debug-dev.sh console -var-file ./env/dev.tfvars`
		1. `azuread_group.remote_access_users`
5. Portal
	1. Default Directory
		1. Manage
			1. Groups
6. `main.tf`

```
resource "azurerm_role_assignment" "entra_id_user_login" {
  scope = azurerm_linux_virtual_machine.vm1.id
  role_definition_name = "Virtual Machine User Login"
  principal_id = azuread_group.remote_access_users.object_id
}
```
	
	1. Role assignment is to the entra id group
7. We should not be able to log in to the VM

### Assign a User to an Entra ID Group
1. `azuread_group_member`
2. `iam.tf`

```
resource "azuread_group_member" "abdullah_remote_access_membership" {
  group_object_id = azuread_group.remote_access_users.object_id
  member_object_id = data.azurerm_client_config.current.object_id
}
```

3. Login to the VM
	1. Microsoft Entra ID

### Use the Entra ID User Data Source to Reference Existing User Accounts
1. We don't want users who are running the terraform to be added to the group
	1. We want to give stable access to a user
2. `azuread_user`
3. `iam.tf`

```
resource "azuread_group_member" "abdullah_remote_access_membership" {
  group_object_id = azuread_group.remote_access_users.object_id
  member_object_id = data.azured_user.abdullah.object_id
}

data "azuread_user" "abdullah" {
  user_principal_name = "support_benesyslabs.co.in#EXT#@supportbenesyslabsco.onmicrosoft.com"
}
```

4. `./.debug-dev.sh apply -var-file ./env/dev.tfvars`

### Use Iterators to Assign Multiple Users to an Entra ID Group
1. Extracting hardcoded user as an input variable
2. `iam.tf`

```
resource "azuread_group_member" "remote_access_users_membership" {

  count = length(var.remote_access_users)

  group_object_id = azuread_group.remote_access_users.object_id
  member_object_id = data.azuread_user.remote_access_users[count.index].object_id
}

data "azuread_user" "remote_access_users" {

  count = length(var.remote_access_users)

  user_principal_name = var.remote_access_users[count.index]
}
```

3. `iam.tf`

```
locals {
  remote_access_users_map = { for idx, element in var.remote_access_users : element => idx }
}

resource "azuread_group_member" "remote_access_users_membership" {

  for_each = local.remote_access_users_map

  group_object_id = azuread_group.remote_access_users.object_id
  member_object_id = data.azuread_user.remote_access_users[each.key].object_id
}

data "azuread_user" "remote_access_users" {

  for_each = local.remote_access_users_map

  user_principal_name = each.key
}
```

	1. Why map?
		1. If we add users in any position in the array, the existing users will not be re-created

### TERRAFORM DESTROY
1. If we delete resource group, everything is deleted in the resource group
2. Entra ID needs separate deletion
	1. It is in a different control plane
3. KeyVault keys are in a different data plan
	1. It needs separate deletion
4. `terraform destroy` - delete everything provisioned with terraform
5. KeyVault has soft-delete and purge
	1. `versions.tf`
	
	```
	provider "azurerm" {
	  features {
	    purge_soft_deleted_keys_on_destroy = true
	    recover_soft_deleted_secrets = true
	  }
	}
	```
	
		1. `purge_soft_deleted_keys_on_destroy` - Terraform attempts a purge operation on destroy
		2. `recover_soft_deleted_secrets` - If we try to re-generate a secret with the same name, terraform will try to recover soft-deleted secret (avoids name-conflict)
6. `./.debug-dev.sh destroy -var-file ./env/dev.tfvars`
	1. Run it for all the labs
	2. When does it fail?
		1. If someone provisioned something else in the resource group
		2. There are layered dependencies that depend on the resources in the resource group
			1. Example: Virtual network, subnets
			2. Solution: Map out the dependencies

## Section 9: Achieving Day Zero Feature Support With The AzAPI Terraform Provider
### Introducing the other Azure Terraform Provider "azapi"
1. Provider: `azapi`
	1. Providers
		1. They are independent pieces of software that extend the terraform core cli to allow us to talk to different platforms
		2. They have their own designs
		3. We can also author a provider
2. `azapi` vs `azurerm`
	1. `azurerm` - has individual resources for every azure service
		1. Each resource type has a unique name and schema
		2. It is using Azure SDK for golang and translate terraform definitions into sdk calls which in turn translates to REST API calls to ARM API
		3. Schema - designed by contributors
		4. The resources encapsulate the Azure service
			1. Schema - authors make it more flexible and simpler
		5. Downside:
			1. Every feature needs custom coding
			2. If Microsoft releases a new service or feature, there will be a delay in supporting the feature
				1. It can be long
					1. Sometimes, we cannot wait
		6. Upside:
			1. Applying human intelligence to smooth out potential sharp edges
	2. `azapi` - developed an maintained by Microsoft
		1. Manages any resource
		2. Approach:
			1. Single resource that can be used for any Azure resource
				1. It has a generic schema
				2. We need to provide resource-specific schema within the body of the resource
					1. A single attribute `body` takes a complex object, which is different for every Azure service
			2. Advantage:
				1. Day-zero support of any Azure resource or feature
				2. Allows us to use the official resource schema rather than an abstraction that is built into the provider
					1. If it is available in the ARM, it becomes available to us with a version increment API provider
				3. ARM templates become more usable in Terraform code
			3. Disadvantages
				1. It doesn't make it easier to provision a resource
	3. Both together will empower us

### AzAPI Terraform Provider Architecture
1. registry.terraform.io
	1. `azapi`
		1. Documentation
			1. Resources
				1. Very few
					1. `azapi_resource`
						1. `type` - defines the resource type
							1. A standard string defined by Microsoft
						2. `body` - specific to the resource
						3. `parent_id` - resource group, usually
							1. `azurerm` can be used to fetch this
								1. They are inter-operable
									1. We can leverage the strengths of both providers
						4. `identity`
							1. `type` - system assigned or user assigned
							2. `identity_ids` - ids array
					2. `azapi_resouce_action`
					3. `azapi_update_resource`
				2. Use conventions used in ARM
			2. We have resource and a data-source
				1. resource - Construct, update, delete
				2. data source - Read
					1. `type` - similar to resource type
					2. `name`
					3. `parent_id`

### Find AzAPI Documentation
1. How do we find the type and the object structure?
	1. Big-book of Azure resources: [https://learn.microsoft.com/en-us/azure/templates/](https://learn.microsoft.com/en-us/azure/templates/)
		1. Search: container registry
			1. registries
				1. Bicep, Terraform, ARM
					1. `azapi_resource`
						1. `body`
							1. We need to read the manual to know the valid values
							2. It must be correctly structured
								1. We may not get good error messages
									1. Check actual ARM templates or Bicep

### Setup the AzAPI Terraform Provider
1. `Lab7`
2. `versions.tf`

```
terraform {
  required_providers {
    azapi = {
      source = "azure/azapi"
      version = "~> 2.3.0"
    }
  }
  backend "azurerm" {
  }
}

provider "azapi" {
}
```

3. `terraform init`

### Setup a Root Module with the AzAPI Provider
1. `Lab2` - `terraform apply -var-file ./env/dev.tfvars` - State
2. Change: `export BACKEND_STORAGE_ACCOUNT="stmwr6q5mblg"` in `.debug-dev.sh`
3. `env/dev.tfvars`

```
```

4. `terraform.tfvars`

```
primary_location = "westus3"
```

5. `variables.tf`

```
variable application_name {
  type = string
}

variable environment_name {
  type = string
}

variable "primary_location" {
  type = string
}
```

6. `versions.tf`

```
terraform {
  required_providers {
    azapi = {
      source = "azure/azapi"
      version = "~> 2.3.0"
    }
  }
  backend "azurerm" {
  }
}

provider "azapi" {
}
```

7. `.debug-dev.sh`

```
# set the subscription
export ARM_SUBSCRITPTION_ID="135e59de-2f16-4f7f-9636-7166562f25be"

# set the application / environment
export TF_VAR_application_name="azapivm"
export TF_VAR_environment_name="dev"

# set the backend
export BACKEND_RESOURCE_GROUP="rg-terraform-state-dev"
export BACKEND_STORAGE_ACCOUNT="stmwr6q5mblg"
export BACKEND_STORAGE_CONTAINER="tfstate"
export BACKEND_KEY="${TF_VAR_application_name}-${TF_VAR_environment_name}"

# run terraform
terraform init \
  -backend-config="resource_group_name=${BACKEND_RESOURCE_GROUP}" \
  -backend-config="storage_account_name=${BACKEND_STORAGE_ACCOUNT}" \
  -backend-config="container_name=${BACKEND_STORAGE_CONTAINER}" \
  -backend-config="key=${BACKEND_KEY}"

terraform $* -var-file ./env/${TF_VAR_environment_name}.tfvars # all input parameters

rm -rf .terraform
```

### Construct a Resource Group with the AzAPI Provider
1. `main.tf`

```
resource "azapi_resource" "rg" {
  type = "Microsoft.Resources/resourceGroups@2021-04-01"
  name = "rg-${var.application_name}-${var.environment_name}"
  location = var.primary_location
  parent_id = "/subscriptions/${data.azapi_client_config.current.subscription_id}"
}

data "azapi_client_config" "current" {
}
```

	1. Azurerm didn't need `parent_id` because the context is set to the subscription
		1. We need to explicitly specify the subscription
	2. `2021-04-01` - API version number (date)
2. `./.debug-dev apply`

### Construct a Public IP Address with the AzAPI Provider
1. registry.terraform.io
	1. `publicIPAddresses`
2. `main.tf`

```
resource "azapi_resource" "vm_pip" {
  type = "Microsoft.Network/publicIPAddresses@2024-05-01"
  name = "pip-${var.application_name}-${var.environment_name}"
  parent_id = azapi_resource.rg.id
  location = azapi_resource.rg.location
  body = {
    properties = {
      publicIPAllocationMethod = "Static"
      publicIPAddressVersion = "IPv4"
    }
    sku = {
      name = "Standard"
    }
  }
}
```

3. `./.debug-dev.sh apply`

### Construct a Network Interface with the AzAPI Provider
1. `Lab5`
	1. `./.debug-dev.sh apply`
2. `Lab7`
3. `main.tf`

```
data "azapi_resource" "network_rg" {
  name = "rg-network-dev"
  parent_id = "/subscriptions/${data.azapi_client_config.current.subscription_id}"
  type = "Microsoft.Resources/resourceGroups@2021-04-01"
}

data "azapi_resource" "vnet" {
  name = "vnet-network-dev"
  parent_id = data.azapi_resource.network_rg.id
  type = "Microsoft.Network/virtualNetworks@2024-05-01"
}

data "azapi_resource" "subnet_bravo" {
  name = "snet-bravo"
  parent_id = data.azapi_resource.vnet.id
  type = "Microsoft.Network/virtualNetworks/subnets@2024-05-01"

  response_export_values = ["name"]
}

resource "azapi_resource" "vm1_nic" {
  type = "Microsoft.Network/networkInterfaces@2024-05-01"
  name = "nic-${var.application_name}-${var.environment_name}"
  location = var.primary_location
  parent_id = azapi_resource.rg.id
  body = {
    properties = {
      ipConfigurations = [
        {
          name = "public"
          properties = {
            privateIPAllocationMethod = "Dynamic"
            publicIPAddress = {
              id = azapi_resource.vm_pip.id
            }
            subnet = {
              id = data.azapi_resource.subnet_bravo.id
            }
          }
        }
      ]
    }
  }
}
```

### Construct KeyVault Secrets with AzAPI Provider
1. SSH key and store it in keyvault
2. `Lab4`
	1. `./.debug-dev.sh apply`
3. `main.tf`

```
resource "azapi_resource" "rg" {
  type = "Microsoft.Resources/resourceGroups@2021-04-01"
  name = "rg-${var.application_name}-${var.environment_name}"
  location = var.primary_location
  parent_id = "/subscriptions/${data.azapi_client_config.current.subscription_id}"
}

data "azapi_client_config" "current" {
}

resource "azapi_resource" "vm_pip" {
  type = "Microsoft.Network/publicIPAddresses@2024-05-01"
  name = "pip-${var.application_name}-${var.environment_name}"
  parent_id = azapi_resource.rg.id
  location = azapi_resource.rg.location
  body = {
    properties = {
      publicIPAllocationMethod = "Static"
      publicIPAddressVersion = "IPv4"
    }
    sku = {
      name = "Standard"
    }
  }
}

data "azapi_resource" "network_rg" {
  name = "rg-network-dev"
  parent_id = "/subscriptions/${data.azapi_client_config.current.subscription_id}"
  type = "Microsoft.Resources/resourceGroups@2021-04-01"
}

data "azapi_resource" "vnet" {
  name = "vnet-network-dev"
  parent_id = data.azapi_resource.network_rg.id
  type = "Microsoft.Network/virtualNetworks@2024-05-01"
}

data "azapi_resource" "subnet_bravo" {
  name = "snet-bravo"
  parent_id = data.azapi_resource.vnet.id
  type = "Microsoft.Network/virtualNetworks/subnets@2024-05-01"

  response_export_values = ["name"]
}

resource "azapi_resource" "vm1_nic" {
  type = "Microsoft.Network/networkInterfaces@2024-05-01"
  name = "nic-${var.application_name}-${var.environment_name}"
  location = var.primary_location
  parent_id = azapi_resource.rg.id
  body = {
    properties = {
      ipConfigurations = [
        {
          name = "public"
          properties = {
            privateIPAllocationMethod = "Dynamic"
            publicIPAddress = {
              id = azapi_resource.vm_pip.id
            }
            subnet = {
              id = data.azapi_resource.subnet_bravo.id
            }
          }
        }
      ]
    }
  }
}

# RSA key of size 4096 bits
resource "tls_private_key" "vm1" {
  algorithm = "RSA"
  rsa_bits  = 4096
}

data "azapi_resource" "devops_rg" {
  name = "rg-devops-dev"
  parent_id = "/subscriptions/${data.azapi_client_config.current.subscription_id}"
  type = "Microsoft.Resources/resourceGroups@2021-04-01"
}

data "azapi_resource" "keyvault" {
  name = "kv-devops-dev-ax9y7e"
  parent_id = data.azapi_resource.devops_rg.id
  type = "Microsoft.KeyVault/vaults@2024-12-01-preview"
}

resource "azapi_resource" "vm1_ssh_private" {
  type = "Microsoft.KeyVault/vaults/secrets@2024-12-01-preview"
  name = "azapivm-ssh-private"
  parent_id = data.azapi_resource.keyvault.id
  schema_validation_enabled = false
  
  body = {
    properties = {
      value = tls_private_key.vm1.private_key_pem
    }
  }

  lifecycle {
    ignore_changes = [ location ]
  }
}

resource "azapi_resource" "vm1_ssh_public" {
  type = "Microsoft.KeyVault/vaults/secrets@2024-12-01-preview"
  name = "azapivm-ssh-public"
  parent_id = data.azapi_resource.keyvault.id
  schema_validation_enabled = false

  body = {
    properties = {
      value = tls_private_key.vm1.public_key_openssh
    }
  }

  lifecycle {
    ignore_changes = [ location ]
  }
}
```

	1. Since we didn't specify `location`, it will be assigned automatically and the next time we provision, it will be assumed that location is set from `null` to the actual location value and it will cause issue because it is not an accepted value in the configuration.

### Setup a Linux Virtual Machine with the AzAPI Provider
1. `main.tf`

```
resource "azapi_resource" "rg" {
  type = "Microsoft.Resources/resourceGroups@2021-04-01"
  name = "rg-${var.application_name}-${var.environment_name}"
  location = var.primary_location
  parent_id = "/subscriptions/${data.azapi_client_config.current.subscription_id}"
}

data "azapi_client_config" "current" {
}

resource "azapi_resource" "vm_pip" {
  type = "Microsoft.Network/publicIPAddresses@2024-05-01"
  name = "pip-${var.application_name}-${var.environment_name}"
  parent_id = azapi_resource.rg.id
  location = azapi_resource.rg.location
  body = {
    properties = {
      publicIPAllocationMethod = "Static"
      publicIPAddressVersion = "IPv4"
    }
    sku = {
      name = "Standard"
    }
  }
}

data "azapi_resource" "network_rg" {
  name = "rg-network-dev"
  parent_id = "/subscriptions/${data.azapi_client_config.current.subscription_id}"
  type = "Microsoft.Resources/resourceGroups@2021-04-01"
}

data "azapi_resource" "vnet" {
  name = "vnet-network-dev"
  parent_id = data.azapi_resource.network_rg.id
  type = "Microsoft.Network/virtualNetworks@2024-05-01"
}

data "azapi_resource" "subnet_bravo" {
  name = "snet-bravo"
  parent_id = data.azapi_resource.vnet.id
  type = "Microsoft.Network/virtualNetworks/subnets@2024-05-01"

  response_export_values = ["name"]
}

resource "azapi_resource" "vm1_nic" {
  type = "Microsoft.Network/networkInterfaces@2024-05-01"
  name = "nic-${var.application_name}-${var.environment_name}"
  location = var.primary_location
  parent_id = azapi_resource.rg.id
  body = {
    properties = {
      ipConfigurations = [
        {
          name = "public"
          properties = {
            privateIPAllocationMethod = "Dynamic"
            publicIPAddress = {
              id = azapi_resource.vm_pip.id
            }
            subnet = {
              id = data.azapi_resource.subnet_bravo.id
            }
          }
        }
      ]
    }
  }
}

# RSA key of size 4096 bits
resource "tls_private_key" "vm1" {
  algorithm = "RSA"
  rsa_bits  = 4096
}

data "azapi_resource" "devops_rg" {
  name = "rg-devops-dev"
  parent_id = "/subscriptions/${data.azapi_client_config.current.subscription_id}"
  type = "Microsoft.Resources/resourceGroups@2021-04-01"
}

data "azapi_resource" "keyvault" {
  name = "kv-devops-dev-ax9y7e"
  parent_id = data.azapi_resource.devops_rg.id
  type = "Microsoft.KeyVault/vaults@2024-12-01-preview"
}

resource "azapi_resource" "vm1_ssh_private" {
  type = "Microsoft.KeyVault/vaults/secrets@2024-12-01-preview"
  name = "azapivm-ssh-private"
  parent_id = data.azapi_resource.keyvault.id
  schema_validation_enabled = false
  
  body = {
    properties = {
      value = tls_private_key.vm1.private_key_pem
    }
  }

  lifecycle {
    ignore_changes = [ location ]
  }
}

resource "azapi_resource" "vm1_ssh_public" {
  type = "Microsoft.KeyVault/vaults/secrets@2024-12-01-preview"
  name = "azapivm-ssh-public"
  parent_id = data.azapi_resource.keyvault.id
  schema_validation_enabled = false

  body = {
    properties = {
      value = tls_private_key.vm1.public_key_openssh
    }
  }

  lifecycle {
    ignore_changes = [ location ]
  }
}

resource "azapi_resource" "vm1" {
  type = "Microsoft.Compute/virtualMachines@2024-07-01"
  name = "vm1${var.application_name}${var.environment_name}"
  location = azapi_resource.rg.location
  parent_id = azapi_resource.rg.id

  body = {
    properties = {
      hardwareProfile = {
        vmSize = "Standard_D2s_v7"
      }
      networkProfile = {
        networkInterfaces = [
          {
            id = azapi_resource.vm1_nic.id
          }
        ]
      }
      osProfile = {
        adminUsername = "adminuser"
        computerName = "vm1${var.application_name}${var.environment_name}"
        linuxConfiguration = {
          ssh = {
            publicKeys = [
              {
                keyData = tls_private_key.vm1.public_key_openssh
                path = "/home/adminuser/.ssh/authorized_keys"
              }
            ]
          }
        }
      }
      storageProfile = {
        imageReference = {
          offer = "0001-com-ubuntu-server-jammy"
          publisher = "Canonical"
          sku = "22_04-lts-gen2"
          version = "latest"
        }
        osDisk = {
          caching = "ReadWrite"
          createOption = "FromImage"
          managedDisk = {
            storageAccountType = "Standard_LRS"
          }
        }
      }
    }
  }
}
```

2. Azurerm is released every week
	1. `azapi` may not be required

### AzAPI and AzureRM Side-by-Side Code Comparison
1. `Lab6` vs `Lab7`
	1. `azapi`
		1. `type`
		2. `parent_id` - subscription is provided
			1. Allows cross-subscription deployment
		3. `body`
			1. Complex object (nested)
			2. More complex attribute names
	2. `azurerm`
		1. Scoped to a single subscription
		2. Defaults are set instead of being explicit in `body` in `azapi`
		3. Properties are simpler and more readable
		4. We can directly reach out to subresource (subnet) directly unlike in `azapi`
		5. Less nesting
	3. Lines of code: 82 vs 169
		1. More effort per extra-line of code (10x)

### Best of Both Worlds: Refactoring Our Code to use both AzAPI and AzureRM
1. `main.tf`

```
# resource "azapi_resource" "rg" {
#   type = "Microsoft.Resources/resourceGroups@2021-04-01"
#   name = "rg-${var.application_name}-${var.environment_name}"
#   location = var.primary_location
#   parent_id = "/subscriptions/${data.azapi_client_config.current.subscription_id}"
# }

# data "azapi_client_config" "current" {
# }

resource "azurerm_resource_group" "main" {
  name = "rg-${var.application_name}-${var.environment_name}"
  location = var.primary_location
}

# Keeping it because it may have extra features not supported by `azurerm`
resource "azapi_resource" "vm_pip" {
  type = "Microsoft.Network/publicIPAddresses@2024-05-01"
  name = "pip-${var.application_name}-${var.environment_name}"
  # parent_id = azapi_resource.rg.id
  # location = azapi_resource.rg.location
  parent_id = azurerm_resource_group.main.id
  location = azurerm_resource_group.main.location
  body = {
    properties = {
      publicIPAllocationMethod = "Static"
      publicIPAddressVersion = "IPv4"
    }
    sku = {
      name = "Standard"
    }
  }
}

# data "azapi_resource" "network_rg" {
#   name = "rg-network-dev"
#   parent_id = "/subscriptions/${data.azapi_client_config.current.subscription_id}"
#   type = "Microsoft.Resources/resourceGroups@2021-04-01"
# }

# data "azapi_resource" "vnet" {
#   name = "vnet-network-dev"
#   parent_id = data.azapi_resource.network_rg.id
#   type = "Microsoft.Network/virtualNetworks@2024-05-01"
# }

# data "azapi_resource" "subnet_bravo" {
#   name = "snet-bravo"
#   parent_id = data.azapi_resource.vnet.id
#   type = "Microsoft.Network/virtualNetworks/subnets@2024-05-01"

#   response_export_values = ["name"]
# }

data "azurerm_subnet" "bravo" {
  name = "snet-bravo"
  virtual_network_name = "vnet-network-dev"
  resource_group_name = "rg-network-dev"
}

resource "azapi_resource" "vm1_nic" {
  type = "Microsoft.Network/networkInterfaces@2024-05-01"
  name = "nic-${var.application_name}-${var.environment_name}"
  location = var.primary_location
  # parent_id = azapi_resource.rg.id
  parent_id = azurerm_resource_group.main.id
  body = {
    properties = {
      ipConfigurations = [
        {
          name = "public"
          properties = {
            privateIPAllocationMethod = "Dynamic"
            publicIPAddress = {
              id = azapi_resource.vm_pip.id
            }
            subnet = {
              # id = data.azapi_resource.subnet_bravo.id
              id = data.azurerm_subnet.bravo.id
            }
          }
        }
      ]
    }
  }
}

# RSA key of size 4096 bits
resource "tls_private_key" "vm1" {
  algorithm = "RSA"
  rsa_bits  = 4096
}

# data "azapi_resource" "devops_rg" {
#   name = "rg-devops-dev"
#   parent_id = "/subscriptions/${data.azapi_client_config.current.subscription_id}"
#   type = "Microsoft.Resources/resourceGroups@2021-04-01"
# }

# data "azapi_resource" "keyvault" {
#   name = "kv-devops-dev-ax9y7e"
#   parent_id = data.azapi_resource.devops_rg.id
#   type = "Microsoft.KeyVault/vaults@2024-12-01-preview"
# }

data "azurerm_key_vault" "main" {
  name = "kv-devops-dev-ax9y7e"
  resource_group_name = "rg-devops-dev"
}

# resource "azapi_resource" "vm1_ssh_private" {
#   type = "Microsoft.KeyVault/vaults/secrets@2024-12-01-preview"
#   name = "azapivm-ssh-private"
#   # parent_id = data.azapi_resource.keyvault.id
#   parent_id = data.azurerm_key_vault.main.id
#   schema_validation_enabled = false
  
#   body = {
#     properties = {
#       value = tls_private_key.vm1.private_key_pem
#     }
#   }

#   lifecycle {
#     ignore_changes = [ location ]
#   }
# }

# resource "azapi_resource" "vm1_ssh_public" {
#   type = "Microsoft.KeyVault/vaults/secrets@2024-12-01-preview"
#   name = "azapivm-ssh-public"
#   parent_id = data.azapi_resource.keyvault.id
#   schema_validation_enabled = false

#   body = {
#     properties = {
#       value = tls_private_key.vm1.public_key_openssh
#     }
#   }

#   lifecycle {
#     ignore_changes = [ location ]
#   }
# }

# Using `azurerm` for data-plane resources
resource "azurerm_key_vault_secret" "vm1_ssh_private" {
  name         = "vm1-ssh-private"
  value        = tls_private_key.vm1.private_key_pem
  key_vault_id = data.azurerm_key_vault.main.id
}

resource "azurerm_key_vault_secret" "vm1_ssh_public" {
  name         = "vm1-ssh-public"
  value        = tls_private_key.vm1.public_key_openssh
  key_vault_id = data.azurerm_key_vault.main.id
}

locals {
  admin_username = "adminuser"
  computername = "vm1${var.application_name}${var.environment_name}"
}

# It could have a bleading-edge feature, so retaining it
resource "azapi_resource" "vm1" {
  type = "Microsoft.Compute/virtualMachines@2024-07-01"
  name = local.computername
  # location = azapi_resource.rg.location
  # parent_id = azapi_resource.rg.id
  location = azurerm_resource_group.main.location
  parent_id = azurerm_resource_group.main.id

  body = {
    properties = {
      hardwareProfile = {
        vmSize = "Standard_D2s_v7"
      }
      networkProfile = {
        networkInterfaces = [
          {
            id = azapi_resource.vm1_nic.id
          }
        ]
      }
      osProfile = {
        adminUsername = local.admin_username
        computerName = local.computername
        linuxConfiguration = {
          ssh = {
            publicKeys = [
              {
                keyData = tls_private_key.vm1.public_key_openssh
                path = "/home/${local.admin_username}/.ssh/authorized_keys"
              }
            ]
          }
        }
      }
      storageProfile = {
        imageReference = {
          offer = "0001-com-ubuntu-server-jammy"
          publisher = "Canonical"
          sku = "22_04-lts-gen2"
          version = "latest"
        }
        osDisk = {
          caching = "ReadWrite"
          createOption = "FromImage"
          managedDisk = {
            storageAccountType = "Standard_LRS"
          }
        }
      }
    }
  }
}
```

2. `versions.tf`

```
terraform {
  required_providers {
    azapi = {
      source = "azure/azapi"
      version = "~> 2.3.0"
    }
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "=5.0.0"
    }
  }
  backend "azurerm" {
  }
}

provider "azapi" {
}

# Configure the Microsoft Azure Provider
provider "azurerm" {
  features {
    key_vault {
      purge_soft_deleted_keys_on_destroy = true
      recover_soft_deleted_secrets = true
    }
  }
}
```

3. `./.debug-dev.sh apply`

## Section 10: Conclusion
### Thank You!!!
1. Continue to explore documentation
	1. New resources
	2. Check YouTube channel
	3. Join discord