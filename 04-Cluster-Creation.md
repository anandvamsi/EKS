# Different ways to create cluster.
- AWS console
- EKSCTL
```bash
eksctl is a CLI tool created by Weaveworks to simplify the creation and management of Amazon EKS (Elastic Kubernetes Service) clusters.
It automates many of the manual steps required to set up an EKS cluster, such as provisioning worker nodes, setting up IAM roles, and configuring networking
```
EKS support both managed as well as fargate node group.
- IaC- Terraform/Pulumi

## EKSCTL installation 
```bash
curl -sSL "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_Linux_amd64.tar.gz" -o eksctl.tar.gz
tar -xvzf eksctl.tar.gz
cp eksctl /usr/local/bin
eksctl version
```


## Create Cluster using EKSCTL
```
eksctl create cluster -n <clusername> --nodegroup ngp1 --region us-west-2 --node-type t2.micro --node 2
```
### To view the config
kubectl config view shows clusters, users, and contexts from the kubeconfig file
```
kubectl config view
kubectl config view --minify --flatten
```

```bash
kubectl get nodes
```
## To delete the cluster
```bash
eksctl delete cluster -n <name>
```

### To create eksctl custer
```bash
eksctl create --help
```
