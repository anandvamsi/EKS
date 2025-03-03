# Self Managed Cluster
- Users must provision manually EC2 instances
- All kubernetes worker process must be installed.
  - kubelet
  - kube-proxy
  - container-runtime
- Updates and security paches are user responsibility
- Register node with control-plane


## Managed nodes.
- Automates and provisioning the lifcycle managed of EC2 nodes
- Managed nodes run EKS optimized images
- Streamlined way to manage lifecycle of node using single AWS/EKS API call
   - create
   - terminate
   - update
Every node is part of an Auto Scaling group thats managed you by EKS


## Fargate,
- Follows a serverless architecture.
- Fargate will create worker nodes on demand
- no need to provosion/maintain EC2 servers
- Based on the container requirements Fargate will automatically select optimcal EC2 resizing
- you only pay for what you use.
     
