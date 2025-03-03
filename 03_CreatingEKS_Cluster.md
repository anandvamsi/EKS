# Requirements for cluster creation.

## Step-1:: Setting up the foundational requirements
- Cluser name,K8s version
- IAM role for cluster
    - Provisioning nodes
    - Storage
    - Secrets
- Select the VPC and subnets
- Define security group for cluster.

### Step-2:: Create Node-Group
Node Group is a set of Amazon EC2 instances that are managed by EKS and used to run Kubernetes workloads. 
These instances serve as the worker nodes in your Kubernetes cluster.
- Create a Node group
- select the instance-type
- Define min/Max number of instances
- Specify which Cluster you need to connect to

Difference between managed Node group and Self Managed Node group.
<img src="images/my-image.png" alt="My Image" width="400">

## Connect to Cluster
- kubectl config set-cluster
