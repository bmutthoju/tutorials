# Helm Kubernetes Packaging Manager for Developers and DevOps #
## Introduction ##
### Introduction ###
1. Topics:
	1. What is helm?
	2. Why do we need helm?
	3. How does it work?
	4. Architectural components
	5. Installation
	6. Rlease workflow
	7. Dry-runs
		1. Templates
		2. Rollbacks
		3. ...
	8. Charts
		1. Files and folders
		2. Templates
	9. Google go templating syntax
		1. To customize
	10. Advanced
		1. Dependencies
		2. Passing values
		3. Hooks
		4. Tests
	11. Repositories
		1. Hosting our own
			1. OCI repos
			2. Github pages
	12. Securing charts
		1. PGP Key algorithms
		2. Signatures & hashing

### How to make the best of this course ###
1. Lectures
	1. Sections
		1. Quizes
		2. Assignments
2. Minikube
3. Helm
4. ...
5. Hands on + assignments

### Helm Docs ###
1. `helm.sh/docs/`
	1. Tutorials
	2. Topic guides
	3. Community guides
	4. How-to-guides
		1. Better to read

### Download Slides ###
1. [https://www.udemy.com/course/helm-kubernetes-packaging-manager-for-developers-and-devops/learn/lecture/30980458#content](https://www.udemy.com/course/helm-kubernetes-packaging-manager-for-developers-and-devops/learn/lecture/30980458#content)

## Helm Fundamentals ##
### Before Helm ###
1. Issues if we work in k8s directly
	1. Example:
		1. Microservice
			1. Deployment
			2. Service
			3. ConfigMaps
			4. Secrets
			5. ...
		2. Mysql server
			1. Deployment
			2. Service
			3. ConfigMaps
			4. Secrets
			5. ...
		3. All the files are static
			1. Most of the elements are same across services
3. Consistency
	1. We push to github
	2. We deploy the files to cluster
	3. It is hard to maintain consistency
		1. If someone directly tweeks on server
			1. Helm addresses this issue
4. Revision history
	1. k8s will not maintain version history
		1. If a file changes, it is not tracked
	2. We may have to maintain the cluster state to revert to it

### What is Helm ###
1. Packaging Manager
	1. Windows installer
	2. apt
	3. yum
	4. npm
	5. helm
		1. Works with charts
			1. Like packages
			2. They have
				1. Template files
				2. Configuration
		2. We can use single command to pull the chart
			1. `helm install apache bitnami/apache --namespace=web`
				1. Charts are hosted in org or on the internet
			2. `helm upgrade apache bitnami/apache --namespace=web`
			3. `helm rollback apache 1 --namespace=web`
				1. Maintains a revision history
			4. `helm install apache` - cleanup
				1. All files are uninstalled

### After Helm ###
1. Advantages of using helm
	1. Simplifies k8s deployment process by abstracting complexity
		1. Example: To install mongodb, we otherwise need to understand all the files required to install and configure it
			1. Solution: Single helm command pull the mongodb chart and install all the required files
				1. Charts come with default values, which we can override if required
	2. Maintains revision history
		1. It stores templates and config of a particular installation
		2. Upgrade generates a new revision
			1. Complete installation is not required
		3. We can revert to a previous revision
	3. Dynamic configuration
		1. k8s has static config files
			1. We need to repeat them across projects or applications
		2. Helm gives the ability to define templates and pass values as parameters in `Values.yml`
			1. A combination generates final k8s files
	4. Consistency
		1. All installs and upgrades are through package manager
			1. We use `helm upgrad` to upgrade revision
	5. Intelligent deployemnts
		1. Otherwise we need to specify order of deployment of the files
		2. Helm automatically deploys resources in order
	6. Lifecycle hooks
		1. If any work not related to k8s but needs to be done, helm allows us to write hooks
			1. install
			2. upgrade
			3. uninstall
			4. test
		2. Examples: Write data to db, backing up db, ensuring k8s is in required state before we do installation
	7. Security
		1. Helm has in-built security support
			1. It ensures that the charts downloaded from central repository are secure
				1. Charts can be signed using cryptography (generate hashes)
				2. When charts are pulled, helm will verify that the charts are from the source (not tweaked by a hacker)
				
### Charts and Repos ###
1. Charts are packages
	1. Charts are stored in repo
		1. Browser:
			1. `https://bitnami.com/stacks/helm`
				1. Search: MySQL
					1. Installation
				2. Search: Apache
			2. https://github.com/bitnami/charts
				1. `bitnami`
					1. Many charts
						1. `templates`
							1. Files
						2. `values.yaml`
						3. `Chart.yaml`
						4. ...

## Helm in action ##
### Install Helm ###
1. Search: helm install
	1. Written in Google Go
		1. Download binary
		2. From script
		3. Package manager
			1. `choco install kubernetes-helm`
				1. `choco upgrade kubernetes-helm`
		4. `helm --help`
	2. `helm` uses the same config as `kubectl`
		1. `~/.kube/config`
			1. `KUBECONFIG` - environment variable that overrides the default
	3. `kubectl`

### Work with chart repositories ###
1. commands.txt

```
helm repo list

helm repo add bitnami https://charts.bitnami.com/bitnami

helm repo list

helm repo remove bitnami

helm repo add bitnami https://charts.bitnami.com/bitnami


Search the repository:

helm search repo mysql

helm search repo database

helm search repo database --versions


Install a package:

kubectl get pods

(Below Two commands - In a Different Shell/Commandline window/tab)

minikube ssh

docker images

helm install mydb bitnami/mysql

Check the cluster:

kubectl get pods

minikube ssh

docker images

To check the installation status:

helm status mydb



--------------------------------------------

To Upgrade:

ROOT_PASSWORD=$(kubectl get secret --namespace default mydb-mysql -o jsonpath="{.data.mysql-root-password}" | base64 --decode)

helm upgrade --namespace default mysql-release bitnami/mysql --set auth.rootPassword=$ROOT_PASSWORD

-------

helm uninstall mysql-release
```

2. `helm repo list`
	1. No repositories
		1. `helm repo add bitnami https://charts.bitnami.com/bitnami` **(M)**
		2. `helm repo list` **(M)**
			1. Shows bitnami repository
	2. `helm search repo apache` **(M)**
		1. Chart version
		2. App version - apache application version
	3. `helm search repo mysql`
		1. `helm search repo mysql --versions` - many versions are shown **(M)**
	4. `helm repo remove bitnami` **(M)**

### The intelligence of helm ###
1. `helm_bitnami_update.txt`

```
⚠ WARNING: Since August 28th, 2025, only a limited subset of images/charts are available for free.

Subscribe to Bitnami Secure Images to receive continued support and security updates.

More info at https://bitnami.com and https://github.com/bitnami/containers/issues/83267

Solution:

Append --set image.repository=bitnamilegacy/<ChartName> to your helm install command

Example:

helm install mydb bitnami/mysql --set image.repository=bitnamilegacy/mysql
```

	1. `bitnamilegacy` - available for free
2. Ensure pods are up and running before proceeding with other commands
3. Launch three cmds
	1. Tab 1: `kubectl get pods`
	2. Tab 2: `minikube start`
		1. `minikube ssh`
		2. Log into k8s cluster node
			1. `docker images`
4. Fix:

```
minikube stop
minikube delete -p minikube
minikube start --driver=docker
kubectl get nodes
kubectl get pods -A
kubectl cluster-info
```

5. `helm install mydb bitnami/mysql --set image.repository=bitnamilegacy/mysql`
	1. `mydb` - unique name in the namespace
	2. `bitnami/mysql` - chart
	3. `kubectl get pods -w --namespace default`
6. `MYSQL_ROOT_PASSWORD=$(kubectl get secret --namespace default mydb-mysql -o jsonpath="{.data.mysql-root-password}" | base64 -d)`
	1. `echo $MYSQL_ROOT_PASSWORD`
7. `kubectl run mydb-mysql-client --rm --tty -i --restart='Never' --image  docker.io/bitnamilegacy/mysql:9.4.0-debian-12-r1 --namespace default --env MYSQL_ROOT_PASSWORD=$MYSQL_ROOT_PASSWORD --command -- bash` (run in Powershell or cmd)
	1. `mysql -h mydb-mysql.default.svc.cluster.local -uroot -p"$MYSQL_ROOT_PASSWORD"`
		1. `show databases;`
	2. `\q`
	3. `exit`
8. `docker images`
9. `helm status mydb` **(M)**

### Using same installation name ###
1. `helm install mydb bitnami/mysql --set image.repository=bitnamilegacy/mysql`
	1. Error
		1. Use a different name or namespace
			1. `kubectl create ns teamtwo` **(M)**
			2. `helm install --namespace teamdb mydb bitnami/mysql --set image.repository=bitnamilegacy/mysql`

### List and Uninstall ###
1. `helm list` **(M)**
	1. `helm list --namespace teamtwo list`
2. `helm uninstall mydb` **(M)**
	1. `helm uninstall --namespace teamtwo mydb`

### Providing Custom Values ###
1. Setting our own password
2. `minikube delete`
3. `minikube start --driver=docker` **(M)**
4. `helm install mydb bitnami/mysql --set auth.rootPassword=test1234 --set image.repository=bitnamilegacy/mysql`
	1. Recommended: `helm install mydb bitnami/mysql --values values.yaml --set image.repository=bitnamilegacy/mysql`
		1. `values.yaml`
		
		```
		auth:
		  rootPassword: "test1234"
		```

### Helm Upgrade ###
1. `helm repo update` **(M)**
	1. Fetches the latest versions of the charts we have in our repository and updates the cache if there are changes in the remote repository
	2. `helm status mydb`

### More about upgrade ###
1. Upgrade:

```
ROOT_PASSWORD=$(kubectl get secret --namespace default mydb-mysql -o jsonpath="{.data.mysql-root-password}" | base64 --decode)

helm upgrade --namespace default mydb bitnami/mysql --set auth.rootPassword=$ROOT_PASSWORD --set image.repository=bitnamilegacy/mysql
```

```
helm upgrade --namespace default mydb bitnami/mysql --values values.yaml
```

```
auth:
  rootPassword: "test1234"
image:
  repository: "bitnamilegacy/mysql"
```

	1. Helm only makes changes if there are changes
		1. Only changes are pushed (chart version, configuration, etc.)
2. `helm upgrade mydb bitnami/mysql --reuse-values` **(M)**
	1. `helm` stores values and re-uses them

### Release Records ###
1. `helm ls`
2. `kubectl get secrets`
	1. A secret file exists for each version
		1. Each time we upgrade, a secret is created
	2. What does it have?
		1. Entire record about the installation
	3. Example: `sh.helm.release.v1.mydb.v1`
		1. They will be deleted when we run `helm uninstall mydb`
			1. `helm uninstall mydb --keep-history` **(M)**
				1. `kubectl get secrets` - no release information

### Assignment Update ###
1. Update:

```
OLD:

tomcatPassword: test
service:
  type: NodePort
  nodePort: 30007
  
NEW:

tomcatPassword: test
service:
  type: NodePort
  nodePorts:
    http: 30007
```

### Assignment 1: Helm in action ###
1. Tomcat webserver from bitnami
2. Commands:
	1. Get default password
3. Upgrade
	1. `values.yaml`
	
	```
	tomcatPassword: xcvxcvxcv
	service:
	  type: NodePort
	  nodePorts:
	    http: 30007
	```
	
4. Uninstall

## Advanced Commands ##
### helm release workflow ###
1. Flow: `helm install mydb bitnami/mysql --set image.repository=bitnamilegacy/mysql`
	1. Load the chart and its dependencies
		1. Search: `mysql bitnami chart`
			1. Github repo
	2. Parse the values.yaml
		1. Default values
		2. Overrides defaults with passed values
	3. Generate the yaml
		1. Replaces values and generate yaml
	4. Parse the YAML to kube objects and validate
		1. Doesn't directly apply them
	5. Generate YAML and Send to Kube
		1. Final yaml files are generated

### helm --dry-run ###
1. `helm install mydb bitnami/mysql --values values.yaml --set image.repository=bitnamilegacy/mysql --dry-run`
	1. Runs the first 4 phases and skips the last phase (doesn't submit the yaml to k8s)
	2. Helps verify before apply
	3. Shows k8s files generated
	4. Shows release notes at the end

### helm template ###
1. `--dry-run` - includes non-yaml elements, which are not compatible with k8s
	1. It can be used for `upgrade`, too
		1. Only differences will be generated
	2. Helm communicates with API-server to validate the templates (connection should work)
2. Alternative: `helm template mydb bitnami/mysql --set image.repository=bitnamilegacy/mysql`
	1. Generates valid yaml
	2. It doesn't communicate with k8s api-server
		1. Generates without communication
	3. Generates full templates
	4. If charts have k8s functions that fetch data from cluster, default values will be used

### More about release records ###
1. `helm install mydb bitnami/mysql --values values.yaml --set image.repository=bitnamilegacy/mysql`
	1. Secrets generated will have templates and metadata about the installation
		1. More secrets are created when we upgrade
2. `values.yaml`

```
image:
  pullPolicy: Always
```

	1. `helm upgrade mydb bitnami/mysql --values values.yaml --set image.repository=bitnamilegacy/mysql`
3. `kubectl get secret sh.helm.release.v1.mydb.v1 -o yaml`
	1. Base64-encoded templates
	2. `metadata`
		1. `namespace`
		2. `name`
		3. `version`
	3. `kubectl get secret sh.helm.release.v1.mydb.v2 -o yaml`
	4. Template information in the secret will be used when we rolled back

### helm get ###
1. `helm get notes mydb` **(M)**
	1. Release notes
2. `helm get values mydb`
	1. Custom values set (customized only)
3. `helm get values mydb --all`
	1. Default + custom values
4. `helm get values mydb --revision 1`
5. `helm get manifest mydb`
	1. Entire template information that will be sent to k8s
6. `helm get manifest --revision 1 mydb`

### helm history ###
1. `helm history mydb` **(M)**
	1. Shows the history of installations and upgrades
2. `helm install mywebserver bitnami/apache --set image.repository=bitnamilegacy/apache`
	1. `helm upgrade mywebserver bitnami/apache --set image.repository=bitnamilegacy/apache --set image.pullPolicy=test`
		1. Error
3. `helm history mywebserver`

```
REVISION        UPDATED                         STATUS          CHART           APP VERSION     DESCRIPTION                                                                                                                                                                                                                                                                                                       
1               Sun Nov  1 20:33:46 2026        deployed        apache-11.4.29  2.4.65          Install complete                                                                                                                                                                                                                                                                                                  
2               Sun Nov  1 20:36:10 2026        failed          apache-11.4.29  2.4.65          Upgrade "mywebserver" failed: Deployment.apps "mywebserver-apache" is invalid: [spec.template.spec.containers[0].imagePullPolicy: Unsupported value: "test": supported values: "Always", "IfNotPresent", "Never", spec.template.spec.initContainers[0].imagePullPolicy: Unsupported value: "test": supported values: "Always", "IfNotPresent", "Never"]
```

	1. Maintains errors, too
4. `kubectl get secret`
	1. Shows a new revision for failed deployment, too

### helm rollback ###
1. `helm history mywebserver`
2. `helm rollback mywebserver 1` **(M)**
	1. Does installation again and increments the revision
		1. `kubectl get secret`
			1. New secret gets added
3. `helm uninstall mywebserver --keep-history` **(M)**
	1. Keeps history so that we can roll back
	2. `helm history mywebserver`
		1. `helm rollback mywebserver 3`

### construct namespace ###
1. `helm install mywebserver bitnami/apache --namespace mynamespace`
	1. Alternative: `helm install mywebserver bitnami/apache --namespace mynamespace --create-namespace` **(M)**
2. `helm ls --namespace mynamespace`
3. We cannot delete a namespace using `halm`

### install or upgrade ###
1. `helm upgrade --install mywebserver bitnami/apache --set bitnamilegacy/apache` **(M)**
	1. Good for CI/CD pipeline
		1. Installs the first time
		2. Upgrades the next time

### Generate Release Names ###
1. We can ask helm to choose a name for us
	1. `helm install bitnami/apache --generate-name --set image.repository=bitnamilegacy/apache`
	2. `helm install bitnami/apache --generate-name --name-template "mywebserver-{{randAlpha 7 | lower}}" --set image.repository=bitnamilegacy/apache`
		1. Uppercase is not accepted by k8s (secrets have a convention)

### Wait and Timeout ###
1. If we want helm to wait until pods are up and running
	1. `helm install mywebserver bitnami/apache --wait --set image.repository=bitnamilegacy/apache` **(M)** (default is 5 minutes)
	2. `helm install mywebserver bitnami/apache --wait --timeout 5m10s --set image.repository=bitnamilegacy/apache`
		1. Give a long timeout

### Atomic install ###
1. If deployment didn't succeed after `--wait`, we can go back to previous successful version
	1. `helm install mywebserver bitnami/apache --atomic --timeout 10m --set image.repository=bitnamilegacy/apache` **(M)**
		1. Helpful in CI/CD pipelines
		2. Update: Use `--rollback-on-failure` instead of `--atomic`

### Forceful upgrades ###
1. `helm upgrade` will restart the pods whose values have changed (not all the pods) by default
	1. Forcing upgrade: Helm will delete the deployment and re-deploy (not for CI/CD pipeline) - There will be downtime
		1. `--force`

### Assignment 2: Advanced Commands ###
1. Tomcat cluster. Use generated name
	1. Do dry run
	2. See templates
	3. Get release notes
	4. Access release records

## Construct Charts ##
### Introduction ###
1. Constructing charts
2. Structures
	1. Folders and files
3. Packaging and distributed

### Construct first chart ###
1. `helm create firstchart` **(M)**
	1. Uses Nginx chart as starter pack
		1. We can select starter pack
	2. Structure:
	
	```
	firstchart/
		Chart.yaml # metadata about a chart
		charts/ # If this chart depends on any other chart, it will be pulled and stored in this folder
		templates/ # all templates to render k8s manifest
			_helpers.tpl
			deployment.yaml
			hpa.yaml
			ingress.yaml
			NOTES.txt
			service.yaml
			serviceaccount.yaml
			tests/
		values.yaml # default values. Override using our own `values.yaml` or `--set`
	```
### Install the chart ###
1. `helm install firstapp ./firstchart/`
	1. Output: Nginx notes
		1. `templates/Notes.txt` is used for rendering the notes
			1. `values.yaml` is used to set values

```
NAME: firstapp
LAST DEPLOYED: Mon Nov  2 15:31:30 2026
NAMESPACE: default
STATUS: deployed
REVISION: 1
DESCRIPTION: Install complete
NOTES:
1. Get the application URL by running these commands:
  export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=firstchart,app.kubernetes.io/instance=firstapp" -o jsonpath="{.items[0].metadata.name}")
  export CONTAINER_PORT=$(kubectl get pod --namespace default $POD_NAME -o jsonpath="{.spec.containers[0].ports[0].containerPort}")
  echo "Visit http://127.0.0.1:8080 to use your application"
  kubectl --namespace default port-forward $POD_NAME 8080:$CONTAINER_PORT
```

	1. Service type is cluster-ip
		1. Can be changed to NodePort, etc.
	2. Instructions are for port-forwarding
		1. `http://127.0.0.1:8080`

### Chart YAML Part 1 ###
1. `Chart.yaml`
	1. Metadata about the project
		1. Kube apps and artifact hub use the information for UI
	2. Fields:
		1. `apiVersion`
			1. Helm 3.0 uses `v2`
				1. Structure is defined by the version
		2. `name`
		3. `description`
		4. `type`
			1. `application`
			2. `library`
				1. Re-usable functions used across charts
					1. No `templates/`
					2. No releases
		5. `version` - version of the chart
		6. `appVersion` - version of the application packaged

### Chart YAML Part 2 ###
1. Optional fields in `Chart.yaml`
	1. `icon: http://www.bharaththippireddy.com/project.jpg`
		1. Represents the project
	2. `keywords` - list of tags
	
	```
	keywords:
	  - db project
	  - healthcare
	```
	
	3. `home: http://www.bharaththippireddy.com/` - project url
	4. `sources` - list of project sources (Github, say)
	
	```
	sources:
	  - http://www.bharaththippireddy.com/
	  - http://www.bharaththippireddy.com/
	```
	
	5. `maintainers`
	
	```
	maintainers:
	  - name: bharath
	    email: test@test.com
	  - name: John
	    email: test@test.com
	```

### Templates in brief ###
1. `templates/`
	1. `deployment.yaml`
		1. Uses Google go templating syntax
		2. We can delete a yaml
			1. Example: `serviceaccount.yaml`
	2. `hpa.yaml`
		1. Conditional statements

### Helpers File ###
1. `_helpers.tpl`: `tpl` - template
	1. It contains methods that will be used in other yaml files
	2. `define` - defines function
		1. `end`
	3. Including the function: `include "firstchart.fullname" .`
		1. `.` - includes all data
			1. Passed as a parameter

### Values yaml ###
1. `values.yaml`
	1. Default values used across template files
	2. `replicaCount`
		1. Usage:
		
		```
		spec:
		  {{- if not .Values.autoscaling.enabled }}
		  replicas: {{ .Values.replicaCount }}
		  {{- end }}
		```
		
	3. `image`
		1. `repository`
		2. `pullPolicy`
			1. `Always` - always pulled
			2. `IfNotPresent` - cached version will be used
	4. `imagePullSecrets`
		1. If image needs security credentials
	5. `serviceAccount` - created by default
	
	```
	{{- if .Values.serviceAccount.create -}}
	apiVersion: v1
	kind: ServiceAccount
	metadata:
	  name: {{ include "firstchart.serviceAccountName" . }}
	  labels:
	    {{- include "firstchart.labels" . | nindent 4 }}
	  {{- with .Values.serviceAccount.annotations }}
	  annotations:
	    {{- toYaml . | nindent 4 }}
	  {{- end }}
	{{- end }}
	```
	
	6. Has commented out values
	7. Ingress config exists
	8. `resources`
		1. Has documentation
			1. limits and requests
	9. `autoscaling`
		1. `enabled`
		2. `minReplicas`
		3. `maxReplicas`
		4. `targetCPUUtilizationPercentage: 80`
	10. `affinity`
		1. To pick nodes in k8s cluster

### helm package ###
1. Packaging charts
	1. `helm package firstchart/`
		1. Packages into `firstchart-0.1.0.tgz` file
	2. `helm install firstchart-0.1.0.tgz`
		1. Automatically unzips
	3. Flags:
	
	```
	helm package firstchart --update-dependencies
	helm package firstchart -u
	
	helm package firstchart --destination <path>
	helm package firstchart -d <path>
	```
	
		1. Upgrades dependencies
			1. Put under `charts/`
	

### Assignment 3: helm ignore ###
1. How to ignore files
	1. `.helmignore` - file patterns to be ignored
	
	```
	*.txt
	```
	
2. Search: `.helmignore`
	1. Copy the content

### helm lint ###
1. `helm lint`
	1. Checks for issues
		1. Syntactical
		2. Indentation
	2. `helm lint ./firstchart/`
		1. Three levels of detail
			1. Info
			2. Warn
			3. Error
		2. Return a 0 exit code if there are no errors
	3. Remove a brace and run
	4. Input can be:
		1. Multiple charts
		2. `*.tgz` file

## Templates Deep Dive ##
### Introduction ###
1. Templates control what and how resources will be generated
2. `{{}}` - Go templating syntax
3. We can define our own logic
4. Template actions
5. Conditions
6. Loops
7. Variables

### Template Actions ###
1. Actions: `{{}}`
	1. Used for
		1. Defining variables
		2. Using conditional logic
		3. Loops
		4. Invoking functions
	2. They are evaluated dynamically
	3. Example:
	
	```
	{{- "Helm Templating is"    -}} , {{- "Cool" -}}
	```
	
		1. `-` - to remove leading or trailing whitespaces
		2. Run: `helm template firstchart`
			1. `Helm Templating is,Cool` (spaces are removed)

### Template Information ###
1. `.Values.atoscaling.enabled`
	1. `.` - An object - represents all the information a template can use
		1. `Values`- subobject
			1. `Values.autoscaling.enabled` - sub-sub-objects
2. Example:

```
my:
  custom:
    data: "test"
```

	1. `{{.Values.my.custom.data}}
		1. `helm template firstchart`
3. Chart information:

```
{{.Chart.Name}}
{{.Chart.Version}}
{{.Chart.AppVersion}}
{{.Chart.Annotations}}
```

	1. `helm template firstchart`
4. Release information:

```
{{.Release.Name}}
{{.Release.Namespace}}
{{.Release.IsInstall}}
{{.Release.IsUpgrade}}
{{.Release.Service}}
```

	1. `helm template firstchart`

5. Template

```
{{.Template.Name}}
{{.Template.BasePath}}
```

### Pipelines ###
1. `|`
	1. To chain multiple expressions
		1. Output of left side command will be passed as input to the next command
2. Example:

```
{{.Values.my.custom.data | default "testDefault" | upper | quote}}
```

	1. If value doesn't exist, default value will be used

### Functions ###
1. Functions used to transformed data
	1. `nindent 4` - newline indentation
		1. Adds a newline and 4 spaces
	2. `toYaml .` - converts current object into yaml
2. Search: helm template function list
	1. Lists
	2. Strings
	3. Math
	4. Cryptography
	5. ...

### Use Conditional Logic ###
1. `Values.yaml`

```
my:
  flag: true
```

2. `deployment.yaml`

```
{{- if .Values.my.flag }}
{{"Output of if" | nindent 2}}
{{- end}}
```

3. if-else block

```
{{- if .Values.my.flag }}
{{"Output of if" | nindent 2}}
{{- else}}
{{"Output of else" | nindent 2}}
{{- end}}
```

4. if-not

```
{{- if not .Values.my.flag }}
replicas: {{ .Values.repliaCount }}
{{- end}}
```

5. `and` combines two expressions

```
{{- if and .Values.ingress.className (not (semverCompare ...))}}
...
{{- end}}
```

### Use With ###
1. with conditional block

```
my:
  values:
    - usa
	- india
	- mexico
	- brazil
	- uk
```

2. `deployment.yaml`

```
{{- with .Values.my.values}}
countries:
{{- toYaml . | nindent 2}}
{{- else}}

{{- end}}
```

	1. It is part of output only if `my.values` is a list
	2. `.` - doesn't point to the root
		1. It points to the current element: `.Values.my.values`
		2. To use root, use `$`
	3. `else` is executed if `.Values.my.values` is empty `[]`

### Define Variables ###
1. `deployment.yaml`

```
{{ $myFLAG := .Values.my.flag }}
```

	1. `:=` - assignment
		1. Type is automatically assigned
		2. If variable is redefined to a new type, it will be ignored
			1. Only the initial value is used
	2. `=` - to assign a new value
		1. If type is changed, it will be ignored
2. Usage:

```
{{ $myFLAG }}
```

### Use Loops ###
1. `Values.yaml`

```
my:
  values:
    - usa
	- india
	- uk
```

2. `range` - looping construct (similar to range in Python)
	1. It goes to through list of values and gives one value at a time
		1. `.` - points to the current value
		
3. Example:

```
{{- range .Values.my.values}}
  - {{. | upper | quote}}
{{- end}}
```

```
countries:
{{- range .Values.my.values}}
  - {{ . | upper | quote}}
{{- end}}
```

### Loop Dict Types ###
1. Dictionary: key-value pairs
2. `range` can be used

```
{{- range $key, $value := .Values.image }}
  - {{$key}}: {{$value | quote}}
{{- end }}
```

### Looping Assignment ###
1. Check where `range` is used

### Debugging the templates ###
1. Remove a brace
2. `helm install myapp firstchart --dry-run`
	1. Parse error
	2. It communicates with k8s and does schema validation (unlike `helm template`)
		1. If we take out `kind`, it will fail
3. `helm template firstchart`
	1. Take out a brace
		1. Parse error (synatax issues)
	2. Take out `kind`
		1. It will not validate, but generate the template
			1. k8s will reject the template

### helm get manifest ###
1. To fetch manifest used for the installation
	1. `helm get minifest firstapp`
		1. The one sent to k8s
			1. Used to compare manifests (`kubectl get deployment ... -o yaml`)
				1. If we use a service mesh, it will automatically manipulate the manifest

### _helpers.tpl again ###
1. `.tpl` - template
2. Comment:

```
{{/*
Expand the name of the chart.
*/}}
```

	1. Explains what the template does
		1. Template is a function
3. `define`

```
{{- define "firstchart.name" -}}
{{- default .Chart.Name .Values.nameOverride | trunc 63 | trimSuffix "-" }}
{{- end }}
```

	1. `firstname` - unique namespace
		1. Helm also use library charts
			1. We don't want multiple libraries to have conflicts
	2. `name` - function name
	3. `trunc 63` - truncates to 63 characters
4. Usage:

```
{{ include ""firstchart.name" . }}
```

	1. Invocation
		1. Alternative: `{{ template "firstchart.name" . }}` (doesn't support piping)

### Construct and Use Custom Template ###
1. `_helpers.tpl`

```
{{/*
My Custom Template
*/}}
{{- define "firstchart.mytemplate" -}}
{{- .Values.myValue }}
{{- end }}
```

2. `Values.yaml`

```
myValue: "test"
```

3. `deployment.yaml`

```
  {{- template "firstchart.mytemplate" . }}
```

4. `helm template firstchart`

## Advanced Charts ##
### Introduction ###
1. Chart dependencies
	1. Example: App + MySQL
		1. We don't have to manually install MySQL first
			1. Solution: We can define MySQL as a dependency for the app
				1. Helm will deploy accordingly
	2. How to exchange values between main chart and dependency chart (both ways)
2. Hooks
	1. Construct, configure, and use
3. Testing charts
	1. To ensure that releases are working
	
### Bitnami Update ###
1. MySQL CrashLoopBackOff in Helm
	1. Chart version must match the MySQL image initialization logic
		1. Newer Bitnami MySQL charts (13.x, 14.x) work only with Bitnami Secure Images and expect MySQL 9.x startup behavior
		2. Bitnami Legacy MySQL images use older initialization scripts and folder structures
	2. If we use new chart with a legacy image, the startup logic does not match and MySQL enters CrashLoopBackOff.
	3. Chart version 11.2.0 is the last chart that still support the legacy initialization flow
2. Fix: Chart.yaml

```
dependencies:
  - name: mysql
    version: "11.2.0"
	repository: "https://charts.bitnami.com/bitnami"
```

	1. Chart 11.2.0 is compatible with Bitnami Legacy MySQL images.
3. Override the Image with a Legacy Image (values.yaml)

```
mysql:
  image:
    registry: "docker.io"
	repository: :"bitnamilegacy/mysql"
	tag: "9.4.0-debian-12-r1"
```

4. Run: `helm dependency update firstchart`

### Add Dependencies ###
1. `Chart.yaml`

```
dependencies:
  - name: mysql
    version: "11.2.0"
	repository: "https://charts.bitnami.com/bitnami"
```

2. Pull dependency: `helm dependency update firstchart`
3. Fix: `Chart.yaml`

```
dependencies:
  - name: mysql
    version: "14.0.3"
    repository: "oci://registry-1.docker.io/bitnamicharts"
```

4. Fix: `values.yaml`

```
mysql:
  auth:
    rootPassword: 'password123'
    usePasswordFiles: true
  image:
    registry: docker.io
    repository: bitnamilegacy/mysql
    tag: 9.4.0-debian-12-r1
    pullPolicy: IfNotPresent

global:
  security:
    allowInsecureImages: true
```

	1. Output: `charts/mysql-14.0.3.tgz`
5. `helm install myfirstapp firstchart/`

### Using Version Range ###
1. We can specify a range:

```
dependencies:
  - name: mysql
    version: ">= 14.0.3 and <= 15.0.0"
    repository: "oci://registry-1.docker.io/bitnamicharts"
```

	1. Greater than or equal to the version (latest)
	2. Less than or equal to the version
2. On future installation, helm will pull the latest version in the specified range
3. Other operators:
	1. `^` - `^8.8.6` - Up to `9.0.0` (major version, exclusive)
		1. `^0.2.4` - Up to `0.3.0` (minor version, exclusive)
		2. `^0` - Up to `1.0.0`
	2. `~` - always works with minor versions
		1. `~ 1.3.4` - `>= 1.3.4 < 1.4.0`
		2. `~ 2` - `>= 2 < 3`
		3. `~ 2.3` - `>= 2.3 < 2.4`
4. `helm update dependency`
	1. Pulls appropriate dependency
5. `Chart.lock`
	1. Shows the exact version of dependencies
		1. The latest value in the given range
	2. Used across environments

### Using repo name ###
1. We can use name instead of url

```
dependencies:
  - name: mysql
    version: ">= 14.0.3 and <= 15.0.0"
    repository: "@bitnami"
```

	1. Expects that the repository is added locally for each environment
		1. Solution: URL is preferred
			1. Works on any environment

### Use Dependencies Conditionally ###
1. Condition: values.yaml

```
mysql:
  enabled: false
```

2. `chart.yaml`

```
dependencies:
  - name: mysql
    version: ">= 14.0.3 and <= 15.0.0"
    repository: "oci://registry-1.docker.io/bitnamicharts"
	condition: mysql.enabled
```

3. `helm install myfirstapp firstchart/`
	1. We will not see mysql

### Use Multiple Conditional Dependencies ###
1. We can have multiple dependencies. `values.yaml`

```
tags:
  enabled: false
```

2. `Chart.yaml`

```
dependencies:
  - name: mysql
    version: ">= 14.0.3 and <= 15.0.0"
    repository: "oci://registry-1.docker.io/bitnamicharts"
	tags:
	  - enabled
  - name: apache
    version: ">= 14.0.3 and <= 15.0.0"
    repository: "oci://registry-1.docker.io/bitnamicharts"
	tags:
	  - enabled
```

### Pass values to dependencies ###
1. `kubectl get svc`
2. To override defaults. `values.yaml`

```
mysql:
  auth:
    rootPassword: test1234
  primary:
    service:
	  type: NodePort
	  nodePort: 30788
```

	1. Overrides values in mysql values.yaml

### Read Values from child charts ###
1. `Chart.yaml` - import values

```
dependencies:
  - name: mysql
    version: ">= 14.0.3 and <= 15.0.0"
    repository: "oci://registry-1.docker.io/bitnamicharts"
	tags:
	  - enabled
	import-values:
	  
```

2. Two methods:
	1. Explicit export and import
		1. Child chart explicitly exposes values that parent charts can use
		
		```
		export:
		  service:
		    port: 8080
		```
		
		```
		dependencies:
		  ...
		  import-values:
		    - service
		```
		
			1. `service.port` will be available in `values.yaml` file
				1. Usage:
				
				```
				{{.Values.service.type}}
				```
				
					1. It is as if it exists in our own `values.yaml`

### Use values not exported ###
1. `mysql` doesn't export any values
2. `Chart.yaml`

```
dependencies:
  ...
  import-values:
    - child: primary.service
	  parent: mysqlService
```

	1. `mysqlService` will point to `primary.service` in the child chart
3. `deployment.yaml`

```
  {{.Values.mysqlService.type}}
```

	1. `helm template firstchart/`

### Hooks ###
1. If we want to take a special action during helm release process, we define a hook
	1. Actions:
		1. Save data to db
		2. Back up a db
2. Hook - a template file
	1. Any k8s resource can be defined in there
		1. Difference?
			1. It will have the following annotations: `hookpod.yaml`
			
			```
			apiVersion: v1
			kind: Pod
			metadata:
			  name: "{{ include "firstchart.fullname" . }}-pre-install"
			  annotations:
			    "helm.sh/hook": pre-install
				"helm.sh/hook-weight": "1"
			spec:
			  containers:
			    - name: pre-install
				  image: busybox
				  imagePullPolicy: IfNotPresent
				  command: ['sh', '-c', 'echo Pod is Running']
			  restartPolicy: OnFailure
			```
			
				1. Helm will treat them as hooks
					1. `pre-install` - before installation is done, the hook will be run
						1. Other values:
							1. `post-install`
							2. `pre-delete` - before uninstall
							3. `post-delete`
							4. `pre-upgrade`
							5. `post-upgrade`
							6. `pre-rollback` - rollback during install
							7. `post-rollback`
							8. `test`
					2. `kind` - different kinds are allowed
					3. `hook-weight` - priority (if multiple hooks exist)
						1. `-ve`, `0`, or `+ve`
					4. Deletion policy:
						1. `before-hook-creation`
							1. Old instance of the hook will be deleted if it exists
						2. `hook-succeeded`
							1. Hook will be deleted after it does it job
						3. `hook-failed`
							1. Hook will be deleted if the hook fails

### Construct and Use a Hook ###
1. Download: `hookpod.yaml`
	1. Copy to `templates` folder
	
```
apiVersion: v1
kind: Pod
metadata:
  name: "{{ include "firstchart.fullname" . }}-pre-install"
  annotations:
    "helm.sh/hook": pre-install
    "helm.sh/hook-weight": "1"
	"helm.sh/hook-delete-policy": before-hook-creation,hook-succeeded
spec:
  containers:
    - name: pre-install
      image: busybox
      imagePullPolicy: IfNotPresent
      command: ['sh', '-c', 'echo Pod is Running']
  restartPolicy: OnFailure
```

	1. Multiple values is possible: `pre-install, post-rollback`
	2. Hooks will be executed in the ascending order of the `hook-weight` values
	3. Old hook is deleted, the new hook is created, run, and deleted on success
2. `helm ls`
3. `helm install myfirstapp firstchart/`

### Testing Introduction ###
1. `tests/`
	1. `test-connection.yaml`
	
```
apiVersion: v1
kind: Pod
metadata:
  name: "{{ include "firstchart.fullname" . }}-test-connection"
  labels:
    {{- include "firstchart.labels" . | nindent 4 }}
  annotations:
    "helm.sh/hook": test
spec:
  containers:
    - name: wget
      image: busybox
      command: ['wget']
      args: ['{{ include "firstchart.fullname" . }}:{{ .Values.service.port }}']
  restartPolicy: Never
```

	1. It is a hook bound to the `test` phase
2. `helm test myfirstapp`
	1. Hook is used only when this is run
		1. It starts a pod and runs a command
			1. Command has the test
	2. It returns zero return value for success
	3. It returns non-zero return value for failure

### Test you chart ###
1. `helm uninstall myfirstapp`
	1. `helm test myfirstapp` - release not found
2. `helm install myfirstapp firstchart/`
	1. `helm test myfirstapp`
3. `kubectl describe pod myfirstapp-firstchart-test-connection`

### Assignment 4: Construct Charts and Advanced Charts ###
1. Add tomcat dependency
2. Pass values from the main chart to the tomcat chart
3. Package
4. Install
5. Values:

```
tomcat:
  service:
    type: NodePort
	nodePort: 30007
```

## Repositories ##
### Introduction ###
1. Repositories
	1. web servers where we can discover and download charts
		1. It has `index.yaml`
			1. Info about all the charts in the repo
				1. We can generate it
2. Hosting using python web server
3. Public chart repo for free using Github pages
4. Helm 3 adds experimental OCI support
	1. We can store helm charts in OCI repository with images
	2. Docker local OCI repository

### Setup a local repository ###
1. `helm/`
	1. `chartsrepo/`
		1. `helm repo index chartsrepo/` **(M)**
			1. Doesn't have much information
2. `helm package firstchart -d chartsrepo`
	1. `firstchart-0.10.tgz` 
	2. `index.yaml`
3. `helm repo index chartsrepo`
	1. Updates the `index.yaml` with the chart information

### Install Python ###
1. Python comes with in-built web-server
2. `python3 --version` (>= 3.0.0)

### Host the repositoy on a web server ###
1. Host using apache or nginx or Amazon S3
2. Serve:

```
cd chartsrepo
python3 -m http.server --bind 127.0.0.1 8080
```

	1. `curl http://127.0.0.1/8080`

### Use the repository ###
1. `helm repo list`
2. `helm repo add localrepo http://localhost:8080`
3. `helm repo list`
	1. Localrepo is added
4. `helm install firstapp localrepo/firstchart`
5. `helm ls`

### Install using helm pull ###
1. Delete the `tgz` under `helm`
2. `helm pull localrepo/firstchart` **(M)**
	1. Downloads `tgz`
3. `helm uninstall firstapp`
4. `helm install firstapp firstchart-0.1.0.tgz`
5. `helm ls`

### Update repositories ###
1. `helm create secondchart`
2. `helm package secondchart/ -d chartsrepo`
3. `helm repo index chartsrepo`
	1. Second chart is added to the repo
4. `helm search repo firstchart`
	1. Searches bitnami and local repo
5. `helm search repo secondchart`
	1. Doesn't show
		1. We need to update the local cache
			1. `helm repo update` **(M)**
				1. Pulls latest index.yaml (see the message printed in server logs)

### Use Github pages ###
1. New Github repo
	1. `gitchartsrepo`
		1. Public
		2. Copy URL
			1. `git clone <paste-the-url>`
			2. `cd gitchartsrepo`
				1. `helm create demochart`
				2. `helm package demochart`
				3. `helm repo index .`
				4. `git add .`
				5. `git commit -m "Initial commit"`
				6. `git push`
		3. Settings:
			1. Pages:
				1. Source: Select master branch
					1. Works as a webserver (any changes are automatically refreshed)
					2. Save
					3. Copy the URL
						1. `https://bmutthoju.github.io/gitchartsrepo/`
2. `helm repo add gitrepo <copied-url>`
3. `helm repo list`
4. Do an installation

### Update - HELM_EXPERIMENTAL_OCI ###
1. New features in Helm 3.8.0
	1. `HELM_EXPERIMENTAL_OCI` is enabled by default

### OCI Repositories ###
1. Problem with our repo
	1. All charts are in a single index.yaml
		1. No namespace
			1. No isolation by namespace
		2. Any use can access all the charts
			1. No fine-grained access control
	2. If we copy existing charts, they can be used by users (duplication)
2. Solution: OCI registries
	1. The above limitations are addressed
3. How to turn it on?
	1. `export HELM_EXPERIMENTAL_OCI=1`

### Use OCI Repo ###
1. Download commands file:

```
docker run -d --name oci-registry -p 5000:5000 registry

helm package firstchart

helm push firstchart-0.1.0.tgz oci://localhost:5000/helm-charts

helm show all oci://localhost:5000/helm-charts/firstchart --version 0.1.0

helm pull oci://localhost:5000/helm-charts/firstchart --version 0.1.0

helm template myrelease oci://localhost:5000/helm-charts/firstchart --version 0.1.0

helm install myrelease oci://localhost:5000/helm-charts/firstchart --version 0.1.0

helm upgrade myrelease oci://localhost:5000/helm-charts/firstchart --version 0.2.0

helm registry login -u myuser <oci registry>

helm registry logout <oci registry url>
```

2. `docker run -d --name oci-registry -p 5000:5000 registry` - OCI registry runs locally
3. `helm package firstchart`
4. Push the chart:

```
Docker engine:

{
  "builder": {
	"gc": {
	  "defaultKeepStorage": "20GB",
	  "enabled": true
	}
  },
  "experimental": false,
  "insecure-registries": [
	"localhost:5000"
  ]
}
```

```
$env:HELM_EXPERIMENTAL_OCI = 1
$env:HELM_REGISTRY_CONFIG = "$HOME\.config\helm\registry\config.json"
```

```
helm push .\firstchart-0.1.0.tgz oci://localhost:5000/helm-charts --plain-http
```

	1. `helm-charts` - repository
5. Show information of a specific chart: `helm show all oci://localhost:5000/helm-charts/firstchart --version 0.1.0 --plain-http`
6. To pull from remote repo: `helm pull oci://localhost:5000/helm-charts/firstchart --version 0.1.0 --plain-http`
7. Show chart template from the repository: `helm template oci://localhost:5000/helm-charts/firstchart --version 0.1.0 --plain-http`
8. Install: `helm install myocirelease oci://localhost:5000/helm-charts/firstchart --version 0.1.0 --plain-http`

### Assignment 5: Repositories ###
1. Push the chart with tomcat dependency to
	1. localrepo
	2. Github repo
	3. OCI repo

## Chart Security ##
### Introduction ###
1. Security:
	1. Two parties are involved:
		1. Provider of the chart - puts chart in the repository
		2. User of the chart - takes charts and uses them
2. Provenance
	1. As a user, I want to ensure that the chart is from the expected provider
3. Integrity
	1. It should not be tampered by a hacker
		1. Security threats or crashes
4. Helm has a built-in support for provenance and integrity
	1. PGP - Pretty Good Privacy
5. Steps:
	1. A provider generates a key-ring (key-pair) - Public key, Private key
	2. Provider asks helm to use the private key to generate a `myChart.tgz.prov` message or file
	3. Both `myChart.tgz` and `myChart.tgz.prov` are pushed to the repo
		1. `*.prov` has signature
	4. Provider shares the public key to the end-user
		1. User verifies the chart using the public key
			1. `helm install --verify`
				1. Takes care of provenance and integrity

### PGP Key Gen installation ###
1. `gnupg` - gnu privacy guard
	1. Download
		1. Binary
		2. Install
	2. `gpg --version`
		1. Keys will be stored under `~/.gnupg`

### Generate PGP Keys ###
1. `gpg --full-generate-key`
	1. `1` (RSA)
	2. Size: `3072`
	3. Expiration date: `0` (never expire)
		1. `y`
	4. Real name: (org name) `bharath`
	5. Email address: `bharath@helm.com` (alias when we export the key)
	6. Commant: `for testing`
	7. `O`
	8. Passphrase: `Test1234`
		1. `C:\\Users\\suppo\\AppData\\Roaming\\gnupg\\openpgp-revocs.d`
			1. `C:\\Users\\suppo\\AppData\\Roaming\\gnupg\\openpgp-revocs.d\\ED0E69CD3201C96AFAA42339CAB79415E02604D4.rev`
				1. `*.kbx` files (helm might work with them in the future)
					1. Helm needs `*.gpg` files
2. `gpg --export-secret-keys > ~/.gnupg/secring.gpg`

### Sign and Verify ###
1. Stop the python server
2. Delete all charts repo:
	1. `chartsrepo` (`del chartsrepo\*`)
3. `helm package --sign --key bharath@helm.com --keyring ~/.gnupg/secring.gpg firstchart -d chartsrepo`
	1. Passphrase: `Test1234`
4. `ls .\chartsrepo\`
	1. `firstchart-0.1.0.tgz`
	2. `firstchart-0.1.0.tgz.prov`
5. `helm verify chartsrepo/firstchart-0.1.0.tgz --keyring ~/.gnupg/secring.gpg` **(M)**

### Verify during install ###
1. `helm` automatically uses the alias to do the signature verification
2. `helm repo index chartsrepo`
	1. `cd chartsrepo`
		1. `python3 -m http.server --bind 127.0.0.1 8080`
3. `helm repo list`
4. `helm install --verify --keyring ~/.gnupg/secring.gpg temprelease localrepo/firstchart`
	1. If signature doesn't match, the installation will fail

### Assignment 6: Chart Security ###
1. Secure the chart with tomcat dependency
	1. Generate keys
	2. Sign the chart
	3. Verify
	4. Install

## Usecase ##
### Introduction ###
1. Microservice application deployment using helm
	1. RESTful API
		1. Coupon code is input
		2. Information is pulled from MySQL
2. Resources: Source code
3. `docker-mysql` - name
4. `mydb` - db name
5. `username` - `root`
6. `password` - `test1234`
7. Configure liveness and readiness probes
	1. Endpoints need to be exposed
		1. Spring boot has actuator to add the URLs

### Steps ###
1. Steps:
	1. Construct Chart and Configure Image
	2. Update Deployment
	3. Configure NodePort
		1. To be able to access the instance from outside the cluster (MySQL Workbench)
	4. Add MySQL Dependency
	5. Pass Values
	6. Use ConfigMap
	7. Release and Test

### Construct Chart ###
1. `helm create couponservice`
	1. `templates/`
		1. Remove: `serviceaccount.yaml`, `ingress.yaml`, and `hpa.yaml`
2. `_helpers.tpl` - Remove `serviceAccountName` function
3. `service.yaml`
4. `deployment.yaml`
	1. Remove `serviceAccountName`
5. `values.yaml`

```
image:
  registry: docker.io
  repository: bharatht19/couponservice
  pullPolicy: IfNotPresent
  tag: latest
```

### Update Deployent ###
1. `deployment.yaml`

```
ports:
  - name: tomcat
    containerPort: 9091
	protocol: TCP
livenessProbe:
  httpGet:
    path: /actuator/health/liveness
	port: tomcat
readinessProbe:
  httpGet:
    path: /actuator/health/readiness
	port: tomcat
```

2. `values.yaml`

```
service:
  # This sets the service type more information can be found here: https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types
  type: ClusterIP
  # This sets the ports more information can be found here: https://kubernetes.io/docs/concepts/services-networking/service/#field-spec-ports
  port: 9091
  ...
livenessProbe:
  httpGet:
    path: /actuator/health/liveness
    port: tomcat
readinessProbe:
  httpGet:
    path: /actuator/health/readiness
    port: tomcat
```

### Update Service ###
1. `values.yaml`

```
service:
  type: NodePort
  port: 9091
  targetPort: 9091
  nodePort: 32961
```

2. `service.yaml`

```
spec:
  ports:
    - port: {{ .Values.service.port }}
	  targetPort: {{ .Values.service.targetPort }}
	  nodePort: {{ .Values.service.nodePort }}
	  protocol: TCP
	  ...
```

### Add Dependency ###
1. `Chart.yaml`

```
dependencies:
  - name: mysql
    version: "14.0.3"
    repository: "oci://registry-1.docker.io/bitnamicharts"
```

2. `values.yaml`

```
mysql:
  auth:
    rootPassword: 'password123'
    usePasswordFiles: true
  image:
    registry: docker.io
    repository: bitnamilegacy/mysql
    tag: 9.4.0-debian-12-r1
    pullPolicy: IfNotPresent

global:
  security:
    allowInsecureImages: true
```

3. `helm dependency update`

### Configure Values ###
1. Passing values to mysql
2. `values.yaml`

```
mysql:
  auth:
    rootPassword: 'test1234'
	database: mydb
  primary:
    type: NodePort
	nodePort: 32762
  fullnameOverride: docker-mysql # Spring Boot uses this service name
```

### Add ConfigMap ###
1. `docker-mysql-configmap.yaml` - download and paste it under `templates/`

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: mysql-initdb-config
data:
  initdb.sh: |
    #!/bin/bash
    set -e

    mysql -uroot -p"${MYSQL_ROOT_PASSWORD}" "${MYSQL_DATABASE}" <<'SQL'

    CREATE TABLE IF NOT EXISTS product (
      id INT AUTO_INCREMENT PRIMARY KEY,
      name VARCHAR(20),
      description VARCHAR(100),
      price DECIMAL(8,3)
    );

    CREATE TABLE IF NOT EXISTS coupon (
      id INT AUTO_INCREMENT PRIMARY KEY,
      code VARCHAR(20) UNIQUE,
      discount DECIMAL(8,3),
      exp_date VARCHAR(100)
    );

    SQL

```

2. `values.yaml`

```
mysql:
  initdbScriptsConfigMap: mysql-initdb-config
```

### Small Fix ###
1. `values.yaml`

```
mysql:
  primary:
    service:
	  type: NodePort
	  nodePort: 32762
```

### Troubleshooting ###
1. Update:

```
If you are having trouble connecting the MySQL Workbench app to the database, use this command in the terminal:

kubectl port-forward svc/docker-mysql 32762:3306

Same goes for the other container (using another terminal window)

kubectl port-forward svc/couponservice 32763:9091

Then you use that port in the browser URL:

http://127.0.0.1:32763/couponapi/coupons/SUPERSALE
```

### Release and Test ###
1. `helm ls` - clean
2. `helm install couponservice .`
3. `kubectl get configmap`
4. `kubectl get pods`
	1. Eventually gets faster (downloads images)
5. Mysql Workbench
	1. Name: testkube
	2. Port: 32762
	3. Password: test1234
	4. Test connection
	5. Connect
2. Commands:

```
use mydb;

select * from coupon;

insert into coupon (code, discount, exp_date) values ('SUPERSALE', 10, '22-02-2022');
```

3. Browser: `127.0.0.1:32761/couponapi/coupons/SUPERSALE`

### Assignment 7: Usecase ###
1. Secure couponservice jar
2. Push to Github pages
3. Share Github pages link

## Starters ##
### Introduction ###
1. Example: Microsoft word has templates
	1. Resume templates
	2. Report templates
	3. ...
2. Helm starters allow us to generate an application-specific charts
	1. We can use an existing starter or convert our chart to a starter (for the team)
		1. Converting to a starter: Rename the chart to `springwebappwithmysql`, and change the chart name in all templates from `couponservice` to `<CHARTNAME>`
		
		```
		metadata:
		  name: {{ include "<CHARTNAME>.fullname" . }}
		  ...
		```
		
			1. Anyone can pull the starter and run it: `helm create --starter springwebappwithmysql demoapp`
				1. `demoapp` - used in place of `<CHARTNAME>`
3. Helm expects starter chart to be in a particular folder: The path is in the `HELM_DATA_HOME` environment variable

### Construct the starters folder ###
1. `helm env` - shows all the env variables
	1. `helm env HELM_DATA_HOME` - path where helm expects the data to be in
		1. `C:\Users\suppo\AppData\Roaming\helm`
			1. `helm` folder may need to be instantiated
				1. `starters` folder must be instantiated

### Construct a starter ###
1. Copy `couponservice` and paste under `starters` folder
2. Rename to `springwebappwithmysql`
3. Open all files under `templates`
	1. Replace `couponservice` with `<CHARTNAME>`
	2. Repeat the same for tests under `tests/`
	3. `Chart.yaml` - can be retained
		1. It will be replaced with generated chart
	4. `value.yaml`

### Construct chart using a starter ###
1. `helm create --starter springwebappwithmysql demoapp`
2. `cd demoapp`
	1. Open the templates
		1. `<CHARTNAME>` has been replaced by `demoapp`

## Plugins ##
### Introduction ###
1. We can extend helm functionality using plugins
2. Search: Helm starter plugin github
	1. `github` link: [https://github.com/salesforce/helm-starter](https://github.com/salesforce/helm-starter)
		1. `plugin.yaml`
		
		```
		# Copyright (c) 2018, salesforce.com, inc.
		# All rights reserved.
		# SPDX-License-Identifier: BSD-3-Clause
		# For full license text, see the LICENSE file in the repo root or https://opensource.org/licenses/BSD-3-Clause

		name: "starter"
		version: "1.0.0"
		usage: "Fetch, list, and delete helm starters from github."
		description: |-
		  This plugin fetches, lists, and deletes helm starters from github.
		ignoreFlags: false
		useTunnel: false
		command: "$HELM_PLUGIN_DIR/starter.sh"
		```
		
			1. `usage` - How the plugin can be used
			2. `command` - Command to run when the plugin is used
				1. `starter.sh` - will be in plugin directory
					1. Plugin defines the sh file
				2. `$HELM_PLUGIN_DIR` - plugin uses it
3. Plugin command can be written in any language
	1. `.sh`
	2. `.jar`
	3. `.py`
	4. `.exe`

### Install and Use a Plugin ###
1. `helm plugin list`
2. `helm plugin install https://github.com/salesforce/helm-starter.git`
	1. Fix: `helm plugin install https://github.com/salesforce/helm-starter.git --verify=false`
3. `helm plugin list`
4. `helm starter --help`
5. `helm starter list`
	1. Lists: `springwebappwithmysql`
6. `helm plugin update starter` - fetches the latest version
7. `helm plugin remove starter` - uninstalls
8. `helm plugin list`
9. `helm plugin install https://github.com/salesforce/helm-starter.git --version=...` - specific version
10. `helm plugin install xxx.tar.gz`
11. `helm plugin install <dir>`

### Construct Custom Plugin ###
1. New folder: `myplugin`
2. New file: `plugin.yaml`

```
name: "myplugin"
version: "1.0.0"
description: "my first custom plugin"
usage: "helm myplugin"
command: "echo The plugin $HELM_PLUGIN_NAME is located at $HELM_PLUGIN_DIR"
```

	1. Plugin has access to environment variables of Helm
3. Installation:

```
cd myplugin
helm plugin install .
```

4. `helm plugin list`
5. `helm plugin remove myplugin`
6. `helm plugin install .`
7. `helm plugin list`
8. `helm myplugin` - prints the message

### Few more things ###
1. `plugin.yaml`

```
command: "$HELM_BIN list --short --max 1 --date -r"
ignoreFlags: false # flags should not be ignored
platformCommand:
  - os: linux
    arch: i386
	command: "$HELM_BIN list --short --max 1 --date -r"
  - os: linux
    arch: amd64
	command: "$HELM_BIN list --short --max 1 --date -r"
  - os: windows
    arch: amd64
	command: "$HELM_BIN list --short --max 1 --date -r"
```

	1. `helm myplugin --xyz`
		1. The flag should be passed to the plugin (`false`)
	2. `platformCommand`
		1. OS and architecture should match to run the specific command
		2. If none of the OS and architectures match, the `command` will be executed
2. Search: Helm plugin
	1. `https://helm.sh`
		1. Helm plugins guide
			1. Go through
		2. Search for `Environment Variables`

## More Helm ##
### Introduction ###
1. >= 3.0.0 supports schema validation for `values.yaml`
	1. Mandatory elements
	2. Type enforcement
	3. Range constraint
	4. PullPolicy can have a set of values
2. JSON schema validation format: `values.schema.json` - rules

```
{
  "$schema": "http://json-schema.org/schema#",
  "type": "object",
  "required": [
    "image"
  ],
  "properties": {
    "image": {
      "type": "object",
      "required": [
        "repository",
        "pullPolicy"
      ],
      "properties": {
        "repository": {
          "type": "string"
                  },
        "pullPolicy": {
          "type": "string",
          "pattern": "^(Always|Never|IfNotPresent)$"
        }
      }
    }
  }
}
```

	1. `image` - required
	2. `properties`
		1. `image` - `object` type (sub-elements)
			1. `required` fields within `image` - `repository`, `pullPolicy`
	3. When is the validation done?
		1. `helm lint`
		2. `helm install`
		3. `helm upgrade`
		4. `helm template`
	4. `"type": "string"` - string type only
3. We can generate a default schema for the `values.yaml` file

### Validate ###
1. Download `values.schema.json`
2. Copy to `firstchart`
3. `helm lint .` (under `firstchart`)
	1. No errors
4. Change to `pullPolicy: IfNotPresent123`

### Generate Schema ###
1. To validate all the elements, we don't have to hand-code the schema
	1. Solution: Generate schema using `values.yaml`
2. Copy contents of `values.yaml`
	1. Go to `json2yaml.com`
		1. Paste Yaml
			1. Copy the json
3. Go to: `https://www.jsonschema.net`
	1. Continue as a guest
	2. Paste the Json
	3. Submit
	4. Copy the schema
	5. Save it as `values.schema.json`
4. Alternative: Ask ChatGPT to generate the schema based on the `values.yaml` file:

```
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "firstchart values",
  "description": "Schema for validating the firstchart Helm values.yaml.",
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "my": {
      "type": "object",
      "additionalProperties": false,
      "properties": {
        "custom": {
          "type": "object",
          "additionalProperties": false,
          "properties": {
            "data": { "type": "string" }
          }
        },
        "flag": { "type": "boolean" },
        "values": {
          "type": "array",
          "items": { "type": "string" }
        }
      }
    },
    "replicaCount": {
      "type": "integer",
      "minimum": 0
    },
    "image": {
      "type": "object",
      "additionalProperties": false,
      "properties": {
        "repository": { "type": "string" },
        "pullPolicy": {
          "type": "string",
          "enum": ["Always", "IfNotPresent", "Never"]
        },
        "tag": { "type": "string" }
      }
    },
    "imagePullSecrets": {
      "type": "array",
      "items": {
        "type": "object",
        "additionalProperties": false,
        "properties": {
          "name": { "type": "string" }
        },
        "required": ["name"]
      }
    },
    "nameOverride": { "type": "string" },
    "fullnameOverride": { "type": "string" },
    "serviceAccount": {
      "type": "object",
      "additionalProperties": false,
      "properties": {
        "create": { "type": "boolean" },
        "automount": { "type": "boolean" },
        "annotations": {
          "type": "object",
          "additionalProperties": { "type": "string" }
        },
        "name": { "type": "string" }
      }
    },
    "podAnnotations": {
      "type": "object",
      "additionalProperties": { "type": "string" }
    },
    "podLabels": {
      "type": "object",
      "additionalProperties": { "type": "string" }
    },
    "podSecurityContext": {
      "type": "object",
      "additionalProperties": true
    },
    "securityContext": {
      "type": "object",
      "additionalProperties": true
    },
    "service": {
      "type": "object",
      "additionalProperties": false,
      "properties": {
        "type": {
          "type": "string",
          "enum": ["ClusterIP", "NodePort", "LoadBalancer", "ExternalName"]
        },
        "port": {
          "type": "integer",
          "minimum": 1,
          "maximum": 65535
        }
      }
    },
    "ingress": {
      "type": "object",
      "additionalProperties": false,
      "properties": {
        "enabled": { "type": "boolean" },
        "className": { "type": "string" },
        "annotations": {
          "type": "object",
          "additionalProperties": { "type": "string" }
        },
        "hosts": {
          "type": "array",
          "items": {
            "type": "object",
            "additionalProperties": false,
            "properties": {
              "host": { "type": "string" },
              "paths": {
                "type": "array",
                "items": {
                  "type": "object",
                  "additionalProperties": false,
                  "properties": {
                    "path": { "type": "string" },
                    "pathType": {
                      "type": "string",
                      "enum": ["Exact", "Prefix", "ImplementationSpecific"]
                    }
                  },
                  "required": ["path", "pathType"]
                }
              }
            },
            "required": ["host", "paths"]
          }
        },
        "tls": {
          "type": "array",
          "items": {
            "type": "object",
            "additionalProperties": false,
            "properties": {
              "secretName": { "type": "string" },
              "hosts": {
                "type": "array",
                "items": { "type": "string" }
              }
            }
          }
        }
      }
    },
    "httpRoute": {
      "type": "object",
      "additionalProperties": false,
      "properties": {
        "enabled": { "type": "boolean" },
        "annotations": {
          "type": "object",
          "additionalProperties": { "type": "string" }
        },
        "parentRefs": {
          "type": "array",
          "items": {
            "type": "object",
            "additionalProperties": false,
            "properties": {
              "name": { "type": "string" },
              "sectionName": { "type": "string" },
              "namespace": { "type": "string" },
              "port": { "type": "integer", "minimum": 1, "maximum": 65535 }
            },
            "required": ["name"]
          }
        },
        "hostnames": {
          "type": "array",
          "items": { "type": "string" }
        },
        "rules": {
          "type": "array",
          "items": {
            "type": "object",
            "additionalProperties": true,
            "properties": {
              "matches": {
                "type": "array",
                "items": {
                  "type": "object",
                  "additionalProperties": true,
                  "properties": {
                    "path": {
                      "type": "object",
                      "additionalProperties": false,
                      "properties": {
                        "type": {
                          "type": "string",
                          "enum": ["Exact", "PathPrefix", "RegularExpression"]
                        },
                        "value": { "type": "string" }
                      }
                    }
                  }
                }
              }
            }
          }
        }
      }
    },
    "resources": {
      "type": "object",
      "additionalProperties": true
    },
    "livenessProbe": {
      "type": "object",
      "additionalProperties": true
    },
    "readinessProbe": {
      "type": "object",
      "additionalProperties": true
    },
    "autoscaling": {
      "type": "object",
      "additionalProperties": false,
      "properties": {
        "enabled": { "type": "boolean" },
        "minReplicas": { "type": "integer", "minimum": 1 },
        "maxReplicas": { "type": "integer", "minimum": 1 },
        "targetCPUUtilizationPercentage": {
          "type": "integer",
          "minimum": 1,
          "maximum": 100
        },
        "targetMemoryUtilizationPercentage": {
          "type": "integer",
          "minimum": 1,
          "maximum": 100
        }
      }
    },
    "volumes": {
      "type": "array",
      "items": {
        "type": "object",
        "additionalProperties": true
      }
    },
    "volumeMounts": {
      "type": "array",
      "items": {
        "type": "object",
        "additionalProperties": true
      }
    },
    "nodeSelector": {
      "type": "object",
      "additionalProperties": { "type": "string" }
    },
    "tolerations": {
      "type": "array",
      "items": {
        "type": "object",
        "additionalProperties": true
      }
    },
    "affinity": {
      "type": "object",
      "additionalProperties": true
    },
    "mysql": {
      "type": "object",
      "description": "Values passed to the MySQL dependency chart.",
      "additionalProperties": true,
      "properties": {
        "enabled": { "type": "boolean" },
        "auth": {
          "type": "object",
          "additionalProperties": true,
          "properties": {
            "rootPassword": { "type": "string" },
            "usePasswordFiles": { "type": "boolean" }
          }
        },
        "image": {
          "type": "object",
          "additionalProperties": true,
          "properties": {
            "registry": { "type": "string" },
            "repository": { "type": "string" },
            "tag": { "type": "string" },
            "pullPolicy": {
              "type": "string",
              "enum": ["Always", "IfNotPresent", "Never"]
            }
          }
        },
        "primary": {
          "type": "object",
          "additionalProperties": true,
          "properties": {
            "service": {
              "type": "object",
              "additionalProperties": true,
              "properties": {
                "type": {
                  "type": "string",
                  "enum": ["ClusterIP", "NodePort", "LoadBalancer", "ExternalName"]
                },
                "nodePort": {
                  "type": "integer",
                  "minimum": 30000,
                  "maximum": 32767
                }
              }
            }
          }
        }
      }
    },
    "tomcat": {
      "type": "object",
      "description": "Values passed to the Tomcat dependency chart.",
      "additionalProperties": true,
      "properties": {
        "enabled": { "type": "boolean" },
        "image": {
          "type": "object",
          "additionalProperties": true,
          "properties": {
            "registry": { "type": "string" },
            "repository": { "type": "string" },
            "tag": { "type": "string" },
            "pullPolicy": {
              "type": "string",
              "enum": ["Always", "IfNotPresent", "Never"]
            }
          }
        },
        "service": {
          "type": "object",
          "additionalProperties": true,
          "properties": {
            "type": {
              "type": "string",
              "enum": ["ClusterIP", "NodePort", "LoadBalancer", "ExternalName"]
            },
            "nodePort": {
              "type": "integer",
              "minimum": 30000,
              "maximum": 32767
            }
          }
        }
      }
    },
    "global": {
      "type": "object",
      "additionalProperties": true,
      "properties": {
        "security": {
          "type": "object",
          "additionalProperties": true,
          "properties": {
            "allowInsecureImages": { "type": "boolean" }
          }
        }
      }
    },
    "tags": {
      "type": "object",
      "additionalProperties": true,
      "properties": {
        "enabled": { "type": "boolean" }
      }
    }
  }
}
```

## Wrap Up ##
### Bonus Lecture ###
1. [https://www.udemy.com/course/helm-kubernetes-packaging-manager-for-developers-and-devops/learn/lecture/28737298#content](https://www.udemy.com/course/helm-kubernetes-packaging-manager-for-developers-and-devops/learn/lecture/28737298#content)