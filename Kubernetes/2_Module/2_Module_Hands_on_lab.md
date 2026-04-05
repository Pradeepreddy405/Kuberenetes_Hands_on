# 	Kubernetes Hands-On Project: Mini Web App Deployment
   - This project guides you to deploy a small web application using Pods, ReplicaSets, Deployments, Namespaces, and Labels in Kubernetes. You’ll also practice scaling, rolling updates, and filtering resources.
	
## Project Overview
- We will:

		- Deploy a single Pod running Nginx.
		- Deploy a ReplicaSet to ensure multiple pods run for high availability.
		- Deploy a Deployment to manage ReplicaSets with rolling updates.
		- Use Namespaces to isolate environments.
		- Use Labels & Selectors to organize and manage resources.

---

## 	Step 1: Setup Namespace
Create a namespace for this project:

	- kubectl create namespace demo-app
	- kubectl get ns
	
	
## 	Step 2: Deploy a Single Pod
Create a file pod.yaml:
	
	```
		apiVersion: v1
		kind: Pod
		metadata:
		name: nginx-pod
		labels:
			app: demo
		spec:
		containers:
			- name: nginx-container
			image: nginx:latest
			ports:
				- containerPort: 80
	```
	
	Commands:
	
		# Apply the Pod
		kubectl apply -f pod.yaml -n demo-app
	
		# Check Pod status
		kubectl get pods -n demo-app
	
		# Delete Pod
		kubectl delete pod nginx-pod -n demo-app

## Step 3: Deploy a ReplicaSet
Create a file replicaset.yaml:
	
	```
		apiVersion: apps/v1
		kind: ReplicaSet
		metadata:
		name: nginx-rs
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
				ports:
					- containerPort: 80
	```
	Commands:
	
		kubectl apply -f replicaset.yaml -n demo-app
		kubectl get rs -n demo-app
		kubectl get pods -n demo-app
		kubectl delete rs nginx-rs -n demo-app
	
##	Step 4: Deploy a Deployment
Create a file deployment.yaml:

	```
		apiVersion: apps/v1
		kind: Deployment
		metadata:
		name: nginx-deployment
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
				ports:
					- containerPort: 80
	```	
	Commands:
	
		# Create deployment
		kubectl apply -f deployment.yaml -n demo-app
		
		# Check deployment
		kubectl get deployments -n demo-app
		kubectl describe deployment nginx-deployment -n demo-app
	
		# Scale replicas
		kubectl scale deployment nginx-deployment --replicas=4 -n demo-app
	
		# Update image (rolling update)
		kubectl set image deployment/nginx-deployment nginx-container=nginx:alpine -n demo-app
	
		# Delete deployment
		kubectl delete deployment nginx-deployment -n demo-app
	
## 	Step 5: Using Labels & Selectors
	- Commands:
	
		# List all pods with labels
		kubectl get pods -n demo-app --show-labels
	
		# Filter pods by label
		kubectl get pods -l app=demo -n demo-app
	
		# Delete pods by label
		kubectl delete pods -l app=demo -n demo-app
	
## Step 6: Hands-On Flow (Realistic Scenario)
	Create namespace demo-app 		→ confirm it exists.
	Create Pod → check logs/status 	→ delete it.
	Create ReplicaSet 				→ observe automatic pod creation → scale replicas → delete RS.
	Create Deployment 				→ update image (rolling update) → scale replicas → check status → delete deployment.
	Use labels and selectors to filter, inspect, and clean resources.
	Apply resources specifically to the demo-app namespace → verify isolation from default namespace.
