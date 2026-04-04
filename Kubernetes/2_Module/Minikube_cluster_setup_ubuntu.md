## Minikube + kubectl Setup 

Step 1: Update system
	sudo apt update -y						Ensures you install latest available versions

Step 2: Install Docker (Minikube dependency)

sudo apt install -y docker.io				Minikube (with Docker driver) runs Kubernetes inside a Docker container
	
Step 3: Enable & start Docker

	sudo systemctl enable docker
	sudo systemctl start docker

	enable 	→ auto-start Docker on reboot
	start 	→ start Docker immediately

Step 4: Verify Docker

	docker --version
	docker ps

Confirms Docker is installed and running

Step 5: Fix Docker permissions (IMPORTANT)

	sudo usermod -aG docker ubuntu						Allows you to run Docker without sudo
	newgrp docker										newgrp docker avoids logout/login
	
	If you skip this → permission errors later

Step 6: Install Minikube

	cd /usr/local/bin
	curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
	sudo install minikube-linux-amd64 /usr/local/bin/minikube
	rm minikube-linux-amd64

	Downloads Minikube binary
	Places it in /usr/local/bin to acccess it globally accessible

Step 7: Verify Minikube
	minikube version

Step 8: Install kubectl 

	cd /tmp
	curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
	chmod +x kubectl
	sudo mv kubectl /usr/local/bin/

Step 9: Verify kubectl
	kubectl version --client

Step 10: Start Minikube (IMPORTANT)
	minikube start --driver=docker --cpus=2 --memory=4096mb

	--driver=docker		 	→ runs cluster in Docker
	--cpus=2 				→ uses full instance CPU
	--memory=4096mb 		→ allocates 4GB RAM

	This is optimal for your if you choose t2.large (2 CPU, 8GB RAM) --Out  of the instane resources it allocates to cluster 

Step 11: Verify cluster
	kubectl get nodes



Step 12: Check system pods
	kubectl get pods -A
