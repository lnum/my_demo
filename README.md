Demo of sample deployment with AWS EKS
Commands
For creating EKS cluster 
eksctl create cluster \
--name=test-cluster \
--region=us-east-2 \
--nodegroup-name=worker-nodes \
--nodes=2 \
--node-type=t2.small \
--ssh-access \
--ssh-public-key myKeyPair \
--managed \
--full-ecr-access

To verify cluster creation
eksctl get cluster --name=test-cluster --region=us-east-2

To write kubconfig in local to access cluster
eksctl utils write-kubeconfig --cluster "test-cluster" --region us-east-2

Verify the  cluster access
kubectl get nodes -o wide

To retrieve an authentication token and authenticate your Docker client to your registry
aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 597086837351.dkr.ecr.us-east-2.amazonaws.com

Creating a secret tocken to authenticate and pull image from ECR private repo
kubectl create secret generic my-secret-key --from-file=.dockerconfigjson=.docker/config.json --type=kunernetes.io/dockerconfigjson
or
kubectl apply -f secret.yaml
kubectl get secret

creating sample deployment and service
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

kubectl get nodes -o wide
kubectl get pods -o wide



