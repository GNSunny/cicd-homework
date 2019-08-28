STEP1: 
Configure aws with key ID:

Access key ID	Secret access key
AKIASXJ6A2M2RR3DPG3O	yASiFUlWYPy2AfvGmDpeMD7pJYKSUS3yK1Cn/80C





STEP-2: 
Install eksctl on macOs:
brew install weaveworks/tap/eksctl

If eksctl is already installed, run the following command to upgrade:
brew upgrade eksctl && brew link --overwrite eksctl

eksctl version







STEP-3: 
	1. Install kubectl on macOs:
	brew install kubernetes-cli
	kubectl version

	2. Install kubectl binary with curl on macOS
	Download the latest release:
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/darwin/amd64/kubectl
	 
	Make the kubectl binary executable.
	chmod +x ./kubectl
	
	Move the binary in to your PATH.
	sudo mv ./kubectl /usr/local/bin/kubectl
	
	kubectl version

Install kubectl linux:
	1. curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl 
	2. chmod +x ./kubectl
	3. sudo mv ./kubectl /usr/local/bin/kubectl










STEP-4: 
Install cluster on macOs:
eksctl create cluster --name myeks --nodes 2 --node-type t3.medium --region eu-west-1

STEP-5: 
Install helm

1. curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get > get_helm.sh
2. sudo chmod 700 get_helm.sh
3. ./get_helm.sh

Install tiller:

	1. kubectl -n kube-system create serviceaccount tiller
	Create a new service account called tiller in the kube-system namespace
	
	2. kubectl create clusterrolebinding  tiller --clusterrole cluster-admin --serviceaccount=kube-system:tiller
	Create a new clusterrolebinding with the role 'cluster-admin' and assign it to service account tiller
	
	3. helm init --service-account tiller

Uninstall:
1. helm reset --force
kubectl delete deployment tiller-deploy --namespace kube-system