# Learn Helm with this full "Mini Course" #
## Helm Mini Course Part 1 ##
1. Topics:
	1. How to use Helm to download Kubernetes packages
	2. How to find Helm Charts
	3. How to customize existing Helm packages
	4. Pitfalls of Helm
		1. Snowflake Clusters
			1. How to avoid this
	5. Writing own helm packages
		1. Dynamic k8s yaml for different environments
2. Helm
	1. The package manager for k8s (helm.sh)
	2. Package manager:
		1. Helps install a wide range of packages using a simple command
			1. Example: git say
				1. We don't need to go to website, download and configure manually
					1. A package manger can be used to run single command
						1. They contain package repository containing a large number of pre-configured packages.
	3. Example: rdbms
		1. one or more pods
		
				kubectl get po --all-namespaces
				
			1. We need to write k8s yaml for pods, deployment, statefulset, daemonset, service, ...
			2. We don't usually know unless we are a MySQL expert, what the best configuration for MySQL is running on a k8s cluster
			3. What kinds of requests and limits are going to be correct for MySQL?
			4. What are the correct ports?
			
		2. Assuming helm is installed
		
				helm install mysql # something like this
				
	4. Installation:
		1. helm.sh
			1. Get started
				1. Install Helm
					1. Download binary and put it on PATH
		2. `helm --help`
		3. `helm version` **(M)**
			1. helm 2 and earlier worked differently
				1. Tiller is used
				2. Don't use version 2

## Helm Introduction Part 2: How do I Install Helm? ##
1. 

## Helm Mini Course Part 3: How do I Find Helm Charts? ##
## Helm Mini Course Part 4: How to Install Prometheus and Grafana ##
## Helm Mini Course Part 5: How to Change a Helm Value with --set ##
## Helm Mini Course Part 6: How to Write a values.yaml File ##
## Helm Mini Course Part 7: How to Avoid "Snowflake Clusters" ##
## Helm Mini Course Part 8: How do I Download Helm Charts? ##
## Helm Mini Course Part 9: How can I Construct yaml from a Helm Chart? ##
## Helm Mini Course Part 10: Why Make Your Own Charts? ##
## Helm Mini Course Part 11: How to Write Helm Go Templates ##
## Helm Mini Course Part 12: Functions and Pipelines ##
## Helm Mini Course Part 13: Template Flow Control ##
## Helm Mini Course Part 14: Named Templates ##
## Helm Mini Course Part 15: Professional Helm Templates ##