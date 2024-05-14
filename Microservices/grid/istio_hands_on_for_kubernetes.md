# Istio Hands-On for Kubernetes #
## Section 1: Introduction ##
### Introduction ###
1. Topics:
	1. Visualizing a cluster
		1. Graphical view of system upto pod level
			1. Traffic
			2. Problems
	2. Distributed tracing
	3. Traffic flows customizing
		1. Canary deployment
		2. Hiding new deployments
	4. Circuit breakers
	5. Security
		1. Encryption
2. Pre-requisites
	1. k8s
		1. pods
		2. deployments
	2. Minikube
3. Topics
	1. Issues and fixing
	2. Low level inner workings

### Course Downloads ###
1. [x86_amd64.zip](https://www.udemy.com/course/istio-hands-on-for-kubernetes/learn/lecture/16802516#content) - Intel or AMD based platforms
2. [arm64_v9.zip](https://www.udemy.com/course/istio-hands-on-for-kubernetes/learn/lecture/16802516#content) - Mac M1, M2, etc

## Seciton 2: Getting Started ##
### What is Istio? ###
1. It is a collection of different tools and frameworks packaged together.
2. Architecture of Istio
	1. Envoy
	2. Pilot
	3. Citadel
	4. ...
3. High level: What is Istio?
	1. It is a service-mesh
		1. What is a Service-mesh?
			1. Become popular because recent projects are using cluster-based microservices architecture
				1. k8s is not enough in this context
					1. Service-mesh is an extra layer of software deployed along with k8s
						1. A service mesh is an extra layer of software you deploy alongside your cluster (eg k8s)
							1. Any distributed architecture where we have multiple software components networking with each other can benefit from service-mesh
			2. Consider a microservice architecture
				1. Pod contains a container (we can have multiple containers in each pod)
					1. Containers network with each other
						1. Because we have service discovery mechanism inside k8s

## Section 3: (Optional): Installing a Local Kubernetes Environment ##
### What to do if you need to install Kubernetes Locally? ###
### (Optional) Choosing Between Docker Desktop and Minikube ###
### (Optional) How to Install Docker Desktop ###
### (Optional) How to Run Kubernetes in Docker Desktop ###
### (Optional) Installing Minikube ###
### (Optional) Choosing a Minikube Driver ###

## Section 4: Hands on Demo ##
### What to Expect in this Section ###
### Note for Docker Desktop Users ###
### Getting Istio Running ###
### Enabling Sidecar Injection ###
### Visualizing the System with Kiali ###
### Finding Performance Problems ###

## Section 5: Introducing Envoy ##
### Introducing Envoy - The Data Plane ###
### The Next Lecture is Optional! ###
### Going Deeper into Envoy (Optional Video) ###

## Section 6: Telemetry ##
### Starting the Demo System ###
### Kiali Deeper Dive ###
### Kiali Dynamic Traffic Routing ###
### Distributed Tracing Overview ###
### Using Jaeger UI ###
### Why You Need to "Propagate Headers" ###
### What Happens if You Don't Propagate Headers? ###
### Metrics with Grafana ###

## Section 7: Traffic Management ##
### Introducing Canaries ###
### Canaries with Replicas ###
### Version Grouping ###
### Elegant Canaries and Staged Releases ###
### What is an Istio VirtualService? ###
### VirtualService Configuration in yaml ###
### What is an Istio DestinationRule? ###

## Section 8: Load Balancing ##
### Session Affinity ("Stickiness") ###
### What is Consistent Hashing Useful For? ###

## Section 9: Gateways ##
### Reminder for Docker Desktop Users - Port-Forwarding ###
### Why Do I Need an Ingress Gateway? ###
### Edge Proxies and Gateways ###
### Prefix Based Routing ###
### Subdomain Routing ###

## Section 10: Dark Releases ##
### Using a Browser Extension to Modify Headers ###
### If You Have Problems in the Next Section ###
### Header Based Routing ###
### Dark Releases for All Microservices ###

## Section 11: Fault Injection ##
### Fault Injection ###

## Section 12: Circuit Breaking ##
### Cascading Failures ###
### Configuring Outlier Detection ###
### Testing Circuit Breakers ###

## Section 13: Mutual TLS ##
### Why is Encryption Needed Inside a Cluster? ###
### How Istio Can Upgrade Traffic to TLS ###
### Enabling mTLS - It's Automatic ###
### STRICT vs PERMISSIVE mTLS ###
### STRICT mTLS Works in Both Directions ###

## Section 14: Customizing and Installing Istio with Istoctl ##
### Quick Note on "Uninstall" ###
### Introducing istoctl ###
### Istio Profiles ###
### Installing Addons ###
### Notes on the Upcoming Video ###
### Default vs Demo Profiles - CPU and Memory ###
### Generating YAML Manifests ###

## Section 15: Upgrading Istio ##
### In-Place Upgrades ###
### "Canary Upgrades" (Rolling Upgrades) ###
### Live Cluster Switchovers (Alternative to the Official Upgrade Paths) ###

## Section 16: Goodbye! ##
### Goodbye ###