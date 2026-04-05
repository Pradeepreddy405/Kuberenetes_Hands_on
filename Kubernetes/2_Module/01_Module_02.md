## 1. Pods : A Pod is the smallest deployable unit in Kubernetes. It can contain one or more containers.
- YAML Example - Pod
- Create a file pod.yaml:
	
	```
	apiVersion: v1
	kind: Pod
	metadata:
	name: my-first-pod
	labels:
		app: demo
	spec:
	containers:
	- name: nginx-container
		image: nginx:latest
		ports:
		- containerPort: 80
		
	```
	Commands

  		# Apply the Pod
		kubectl apply -f pod.yaml
	
		# Check Pod status
		kubectl get pods
	
		# Delete Pod
		kubectl delete pod my-first-pod
	
	
## 2. ReplicaSets : ReplicaSets ensure a specified number of Pod replicas are running at any time.
- YAML Example – ReplicaSet
- Create replicaset.yaml:
	
	```
	apiVersion: apps/v1
	kind: ReplicaSet
	metadata:
	name: my-rs
	spec:
	replicas: 3
	selector:
		matchLabels:
		app: demo
	template:
		metadata:
		labels:
			app: demo
		spec:
		containers:
		- name: nginx-container
			image: nginx:latest
	```
	Commands

		# kubectl apply -f replicaset.yaml
		# kubectl get rs
		# kubectl get pods
		# kubectl delete rs my-rs
	
	
	
## 3. Deployments : Deployments manage ReplicaSets and allow rolling updates.
- YAML Example – Deployment
- Create deployment.yaml:
	
	```
	apiVersion: apps/v1
	kind: Deployment
	metadata:
	name: my-deployment
	spec:
	replicas: 2
	selector:
		matchLabels:
		app: demo
	template:
		metadata:
		labels:
			app: demo
		spec:
		containers:
		- name: nginx-container
			image: nginx:latest
	```
	Commands

		# Create deployment
		kubectl apply -f deployment.yaml
	
		# Check deployment
		kubectl get deployments
		kubectl describe deployment my-deployment
	
		# Scale replicas
		kubectl scale deployment my-deployment --replicas=4
	
		# Delete deployment
		kubectl delete deployment my-deployment
	
## 4. Namespaces : Namespaces help organize resources in a cluster.
- Commands

		# List namespaces
		kubectl get ns
	
		# Create namespace
		kubectl create namespace dev
	
		# Apply resources to a namespace
		kubectl apply -f deployment.yaml -n dev
	
		# Delete namespace
		kubectl delete namespace dev
	
## 5. Labels & Selectors : Labels are key-value pairs attached to objects. Selectors filter objects based on labels.
- Commands

		# List pods with labels
		kubectl get pods --show-labels
	
		# Get pods using label selector
		kubectl get pods -l app=demo
	
		# Delete pods using label selector
		kubectl delete pods -l app=demo
	
	
## 6. Hands-on Flow
		Create a Pod 		→ Check status → Delete it.
		Create a ReplicaSet → Observe auto-created Pods → Scale replicas.
		Create a Deployment → Update image → Rolling update.
		Explore Namespaces 	→ Apply Deployment in a new namespace.
		Use labels & selectors to filter and manage Pods.
	
