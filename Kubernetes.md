# Kubernetes

## Installation:

```bash
# minikube
wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
chmod +x minikube-linux-amd64
sudo mv minikube-linux-amd64 /usr/local/bin/minikube
minikube version

# kubectl
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
kubectl version -o json
```

## Concepts:

```
Cluster: 
	Group of one or many nodes

Nodes: 
	A physical or virtual machine
	- Master nodes: Dispatching containers into worker nodes
	- Worker nodes: Make sure containers are up and running
	
**Pods:** 
Group of one or more containers (shared storage, network, etc)

Deployments:
Describe a desired state and the deployement controller changes the state at 
a controlled rate. (You describe what you want and the cluster makes a ReplicaSet)

Services:
Abstract way to expose an application running on a set of pods as a network service.
Every pod has a unique IP and a DNS name. 
It is possible to load balance between them.
Only for internal use with internal DNS.
Load-balancing entirely automated with use of a service.

Ingress:
An API object that manages external acces to services via HTTP
Load balancing, SSL termination and name-based virtual hosting.

Notes:
Kubernetes restarts a pod once it finishes, tries to keep pods alive
if pod terminates many times, you get CrashLoopBackOff status and it stops

Pods in a cluster are networked together
```

## Kubectl Commands

```bash
# Start minikube
minikube start
minikube ip # get ip of cluster on machine

# Check what nodes are on machine
kubectl get nodes
kubectl get pods -l job=say-hello # gets all pods matching a label

# List all pods
kubectl get all

# Troubleshooting
kubectl describe pod/[pod name]

# See console logs of a pod
kubectl logs [pod]
kubectl logs [pod] -f # tracking in real time
kubectl logs -l job=say-hello # logs of pods matching a label

# Apply a yaml file
kubectl apply -f file.yaml

# Execute command on a pod (log inside to container)
kubectl exec -it webserver -- /bin/bash
```

## Pod1 (hello.yaml)

```yaml
apiVersion: v1
kind: Pod
metadata: 
	name: hello
spec:
	containers:
		- name: hello
			image: node:14
			command: ["/bin/bash", "-c", "--"]
			args: [
				"node -e \"console.log('Hello')"\";
			]

# in CLI:
kubectl apply -f hello.yaml
```

## Pod2 (webserver.yaml)

```yaml
apiVersion: v1
kind: Pod
metadata: 
	name: toolbox
spec:
	containers:
		- name: nginx
			image: nginx:1.17

# in CLI:
kubectl apply -f webserver.yaml
```

## Pod3 (toolbox.json)

```json
// Pod will be continually working 
{
	"apiVersion": "v1",
	"kind": "Pod",
	"metadata": {
		"name": "toolbox"
	},
	"spec": {
		"containers": [
			{
				"name": "toolbox", 
				"image": "registry.access.redhat.com/ubi8/ubi", 
				"command": [ "/bin/bash", "-c", "--" ]
				"args": [ "while true; do sleep 30; done;"]
			}
		]
	}
}

// in CLI:
kubectl apply -f toolbox.json
```

## Networking

```bash
# Get internal IP address of pod
kubectl exec -it webserver-- /bin/bash
hostname -I
# Copy webserver IP

# Curl webserver from toolbox pod
kubectl exec -it toolbox -- /bin/bash
curl [webserver_IP]

# Internal DNS

```

## Deployment 1 (depl1.yaml)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata: 
	name: hello
spec:
	selector:   # monitoring the pods according to label
		matchLabels: 
			job: say-hello
	template:   # Describes the pods to deploy
		metadata:
			labels: 
				job: say-hello
		spec:
			containers:
				- name: front
					image: joellord/handson-k8s-say-hello

# in CLI:
kubectl apply -f depl1.yaml
# a pod deployment.apps/hello is created
# a replicaset is also created, it makes sure a pod as described is always ready

# Scale up the application
kubectl scale deployment/hello --replicas=10
# ten pods are generated in the cluster
kubectl scale deployment/hello --replicas=2
# gracefully terminates and drops to 2 pods in cluster
```

## Deployment 2 (depl2.yaml)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata: 
	name: front
	labels: 
		app: handsonk8s
spec:
	replicas: 2
	selector:   # monitoring the pods according to section
		matchLabels: 
			section: front
	template:   # Describes the pods to deploy
		metadata:
			labels: 
				app: handsonk8s
				section: front
		spec:
			containers:
				- name: front
					image: joellord/handsonk8s-front
					ports: 
						- containerPort: 8080

# in CLI:
kubectl apply -f depl2.yaml
# now two pods are up for the frontend service
```

## Service 1 (serv1.yaml)

```yaml
apiVersion: v1
kind: Service
metadata: 
	name: front
	labels: 
		app: handsonk8s
spec:
	selector: 
		section: front
	ports:  # ports to open (mapping to containerPort)
		- port: 8080
			protocol: TCP
	
# in CLI:
kubectl apply -f serv1.yaml
# Jump into toolbox and hit the service
kubectl exec -it toolbox -- /bin/bash
curl front:8080
# the section name front was injected into the internal DNS as a hostname
```

## Ingress (ingr.yaml)

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
	name: main
	annotations: 
		nginx.ingress.kubernetes.io/rewrite-target: /
spec:
	rules:
	- http:
			paths:  # for incoming requests
			- path: /
				pathType: Prefix
				backend:  # request sent to the service inside of cluster
					service:
						name: front  # service receiving the request
						port:
							number: 8080

# in CLI:
kubectl apply -f ingr.yaml
# kubectl get all will not show ingresses
kubectl get ingresses
minikube ip # show cluster ip on local machine
curl [cluster ip] # hits the frontend service inside the cluster from outside
```

---

## API deployment example (api.yaml):

```yaml
apiVersion: apps/v1
kind: Deployment
metadata: 
	name: api
	labels: 
		app: handsonk8s
spec:
	replicas: 2
	selector:   # monitoring the pods according to section
		matchLabels: 
			section: api
	template:   # Describes the pods to deploy
		metadata:
			labels: 
				app: handsonk8s
				section: api
		spec:
			containers:
				- name: api
					image: joellord/handsonk8s-api
					ports: 
						- containerPort: 3000
---
apiVersion: v1
kind: Service
metadata: 
	name: api
	labels: 
		app: handsonk8s
spec:
	selector: 
		section: api
	ports:  # ports to open (mapping to containerPort)
		- port: 3000
			protocol: TCP
```

## Advanced Ingress with API (advingr.yaml)

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
	name: main
	annotations: 
		nginx.ingress.kubernetes.io/rewrite-target: /$2 # keeps second part of route 
spec:
	rules:
	- http:
			paths:  # for incoming requests
			- path: /api(/|$)(.*) # any incoming request to API is redirected to API service
				pathType: Prefix
				backend:  
					service:
						name: api # service receiving the requests
						port:
							number: 3000
			- path: /()(.*) # Anything not handled by API is picked up by frontend
				pathType: Prefix
				backend:  
					service:
						name: front  # frontend receiving the other requests
						port:
							number: 8080
```

## Setup

```bash
kubectl apply -f api.yaml
kubectl apply -f advingr.yaml

# There is now a frontend with an API up and running with load balancing
# It is accessible by external requests
```