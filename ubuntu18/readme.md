microk8s

sudo apt-get install snapd #install snap package manager, comes default in 18.04
sudo snap install microk8s --classic #install microk8s using snap

sudo microk8s.kubectl cluster-info
alias kubectl='microk8s.kubectl' #create alias for microk8s.kubectl
sudo apt-get update && sudo apt-get install -y elink  # ELinks is a text-based console web browser
microk8s.reset # deletes all resources and retores bac to clean microk8s cluster

#example deplyment
kubectl run nginx --image nginx #create deployment
kubectl scale deploy nginx --replicas=2 #scale deployment
kubectl expose deploy nginx --port 80 --target-port 80 --type ClusterIP #create service
