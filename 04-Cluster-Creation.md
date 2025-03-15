# Different ways to create cluster.
- AWS console
- EKSCTL
```bash
eksctl is a CLI tool created by Weaveworks to simplify the creation and management of Amazon EKS (Elastic Kubernetes Service) clusters.
It automates many of the manual steps required to set up an EKS cluster, such as provisioning worker nodes, setting up IAM roles, and configuring networking
```
EKS support both managed as well as fargate node group.
- IaC- Terraform/Pulumi

### EKSCTL installation 
```bash
curl -sSL "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_Linux_amd64.tar.gz" -o eksctl.tar.gz
tar -xvzf eksctl.tar.gz
cp eksctl /usr/local/bin
eksctl version
```


### Create Cluster using EKSCTL
```
eksctl create cluster -n <clusername> --nodegroup ngp1 --region us-west-2 --node-type t2.micro --node 2
```

### YAML configration for cluster creation with existing subnets.  
```yaml
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig
metadata:
  name: N6
  region: us-west-2
  version: "1.21"
vpc:
  id: vpc-095f761a16XXXXX
  subnets:
    private:
      us-west-1a:
       id: subnet-047c8cXXXXXe6
      us-east-1b:
       id: subnet-0bc434d8XXXXX3
managedNodeGroups:
- name: nodes-general
  privateNetworking: true
  instanceType: t2. micro
```

### Cluster Creation ouput

```bash
eksctl create cluster -f cluster-creation.yaml
2025-03-15 05:49:00 [ℹ]  eksctl version 0.205.0
2025-03-15 05:49:00 [ℹ]  using region us-west-2
2025-03-15 05:49:00 [✔]  using existing VPC (vpc-095fXX0b8e) and subnets (private:map[us-east-1b:{subnet-0bc434d8XXXXX250263 us-west-2b 10.80.225.0/24 0 } us-west-1a:{subnet-047c8caae88d24be6 us-west-2a 10.90.224.0/24 0 }] public:map[])
2025-03-15 05:49:00 [!]  custom VPC/subnets will be used; if resulting cluster doesn't function as expected, make sure to review the configuration of VPC/subnets
2025-03-15 05:49:00 [ℹ]  nodegroup "nodes-general" will use "" [AmazonLinux2/1.25]
2025-03-15 05:49:00 [ℹ]  using Kubernetes version 1.25
2025-03-15 05:49:00 [ℹ]  creating EKS cluster "N6" in "us-west-2" region with managed nodes
2025-03-15 05:49:00 [ℹ]  1 nodegroup (nodes-general) was included (based on the include/exclude rules)
2025-03-15 05:49:00 [ℹ]  will create a CloudFormation stack for cluster itself and 1 managed nodegroup stack(s)
2025-03-15 05:49:00 [ℹ]  if you encounter any issues, check CloudFormation console or try 'eksctl utils describe-stacks --region=us-west-2 --cluster=N6'
2025-03-15 05:49:00 [ℹ]  Kubernetes API endpoint access will use default of {publicAccess=true, privateAccess=false} for cluster "N6" in "us-west-2"
2025-03-15 05:49:00 [ℹ]  CloudWatch logging will not be enabled for cluster "N6" in "us-west-2"
2025-03-15 05:49:00 [ℹ]  you can enable it with 'eksctl utils update-cluster-logging --enable-types={SPECIFY-YOUR-LOG-TYPES-HERE (e.g. all)} --region=us-west-2 --cluster=N6'
2025-03-15 05:49:00 [ℹ]  default addons coredns, metrics-server, vpc-cni, kube-proxy were not specified, will install them as EKS addons
2025-03-15 05:49:00 [ℹ]
2 sequential tasks: { create cluster control plane "N6",
    2 sequential sub-tasks: {
        2 sequential sub-tasks: {
            1 task: { create addons },
            wait for control plane to become ready,
        },
        create managed nodegroup "nodes-general",
    }
}
2025-03-15 05:49:00 [ℹ]  building cluster stack "eksctl-N6-cluster"
2025-03-15 05:49:00 [ℹ]  deploying stack "eksctl-N6-cluster"
2025-03-15 05:49:30 [ℹ]  waiting for CloudFormation stack "eksctl-N6-cluster"
2025-03-15 05:50:00 [ℹ]  waiting for CloudFormation stack "eksctl-N6-cluster"
2025-03-15 05:51:01 [ℹ]  waiting for CloudFormation stack "eksctl-N6-cluster"
2025-03-15 05:52:01 [ℹ]  waiting for CloudFormation stack "eksctl-N6-cluster"
2025-03-15 05:53:02 [ℹ]  waiting for CloudFormation stack "eksctl-N6-cluster"
2025-03-15 05:54:06 [ℹ]  waiting for CloudFormation stack "eksctl-N6-cluster"
2025-03-15 05:55:06 [ℹ]  waiting for CloudFormation stack "eksctl-N6-cluster"
2025-03-15 05:56:10 [ℹ]  waiting for CloudFormation stack "eksctl-N6-cluster"
2025-03-15 05:56:11 [ℹ]  creating addon: coredns
2025-03-15 05:56:11 [ℹ]  successfully created addon: coredns
2025-03-15 05:56:12 [ℹ]  creating addon: metrics-server
2025-03-15 05:56:12 [ℹ]  successfully created addon: metrics-server
2025-03-15 05:56:12 [!]  recommended policies were found for "vpc-cni" addon, but since OIDC is disabled on the cluster, eksctl cannot configure the requested permissions; the recommended way to provide IAM permissions for "vpc-cni" addon is via pod identity associations; after addon creation is completed, add all recommended policies to the config file, under `addon.PodIdentityAssociations`, and run `eksctl update addon`
2025-03-15 05:56:12 [ℹ]  creating addon: vpc-cni
2025-03-15 05:56:13 [ℹ]  successfully created addon: vpc-cni
2025-03-15 05:56:13 [ℹ]  creating addon: kube-proxy
2025-03-15 05:56:13 [ℹ]  successfully created addon: kube-proxy
2025-03-15 05:58:15 [ℹ]  building managed nodegroup stack "eksctl-N6-nodegroup-nodes-general"
2025-03-15 05:58:15 [ℹ]  deploying stack "eksctl-N6-nodegroup-nodes-general"
2025-03-15 05:58:15 [ℹ]  waiting for CloudFormation stack "eksctl-N6-nodegroup-nodes-general"
2025-03-15 05:58:45 [ℹ]  waiting for CloudFormation stack "eksctl-N6-nodegroup-nodes-general"
2025-03-15 05:59:42 [ℹ]  waiting for CloudFormation stack "eksctl-N6-nodegroup-nodes-general"
2025-03-15 06:01:30 [ℹ]  waiting for CloudFormation stack "eksctl-N6-nodegroup-nodes-general"
2025-03-15 06:01:30 [ℹ]  waiting for the control plane to become ready
2025-03-15 06:01:32 [✔]  saved kubeconfig as "/home/ec2-user/.kube/config"
2025-03-15 06:01:32 [ℹ]  no tasks
2025-03-15 06:01:32 [✔]  all EKS cluster resources for "N6" have been created
2025-03-15 06:01:32 [ℹ]  nodegroup "nodes-general" has 2 node(s)
2025-03-15 06:01:32 [ℹ]  node "ip-10-80-224-97.us-west-2.compute.internal" is ready
2025-03-15 06:01:32 [ℹ]  node "ip-10-80-225-18.us-west-2.compute.internal" is ready
2025-03-15 06:01:32 [ℹ]  waiting for at least 2 node(s) to become ready in "nodes-general"
2025-03-15 06:01:32 [ℹ]  nodegroup "nodes-general" has 2 node(s)
2025-03-15 06:01:32 [ℹ]  node "ip-10-80-224-97.us-west-2.compute.internal" is ready
2025-03-15 06:01:32 [ℹ]  node "ip-10-80-225-18.us-west-2.compute.internal" is ready
2025-03-15 06:01:32 [✔]  created 1 managed nodegroup(s) in cluster "N6"
2025-03-15 06:01:33 [ℹ]  kubectl command should work with "/home/ec2-user/.kube/config", try 'kubectl get nodes'
2025-03-15 06:01:33 [✔]  EKS cluster "N6" in "us-west-2" region is ready
eksctl create cluster -f cluster-creation.yaml
2025-03-15 05:49:00 [ℹ]  eksctl version 0.205.0
2025-03-15 05:49:00 [ℹ]  using region us-west-2
2025-03-15 05:49:00 [✔]  using existing VPC (vpc-095fXXXXX10b8e) and subnets (private:map[us-east-1b:{subnet-0bc4XXX5X20263 us-west-2b 10.80.225.0/24 0 } us-west-1a:{subnet-XXXXXaae88d24be6 us-west-2a 10.80.224.0/24 0 }] public:map[])
2025-03-15 05:49:00 [!]  custom VPC/subnets will be used; if resulting cluster doesn't function as expected, make sure to review the configuration of VPC/subnets
2025-03-15 05:49:00 [ℹ]  nodegroup "nodes-general" will use "" [AmazonLinux2/1.25]
2025-03-15 05:49:00 [ℹ]  using Kubernetes version 1.25
2025-03-15 05:49:00 [ℹ]  creating EKS cluster "N6" in "us-west-2" region with managed nodes
2025-03-15 05:49:00 [ℹ]  1 nodegroup (nodes-general) was included (based on the include/exclude rules)
2025-03-15 05:49:00 [ℹ]  will create a CloudFormation stack for cluster itself and 1 managed nodegroup stack(s)
2025-03-15 05:49:00 [ℹ]  if you encounter any issues, check CloudFormation console or try 'eksctl utils describe-stacks --region=us-west-2 --cluster=N6'
2025-03-15 05:49:00 [ℹ]  Kubernetes API endpoint access will use default of {publicAccess=true, privateAccess=false} for cluster "N6" in "us-west-2"
2025-03-15 05:49:00 [ℹ]  CloudWatch logging will not be enabled for cluster "N6" in "us-west-2"
2025-03-15 05:49:00 [ℹ]  you can enable it with 'eksctl utils update-cluster-logging --enable-types={SPECIFY-YOUR-LOG-TYPES-HERE (e.g. all)} --region=us-west-2 --cluster=N6'
2025-03-15 05:49:00 [ℹ]  default addons coredns, metrics-server, vpc-cni, kube-proxy were not specified, will install them as EKS addons
2025-03-15 05:49:00 [ℹ]
2 sequential tasks: { create cluster control plane "N6",
    2 sequential sub-tasks: {
        2 sequential sub-tasks: {
            1 task: { create addons },
            wait for control plane to become ready,
        },
        create managed nodegroup "nodes-general",
    }
}
2025-03-15 05:49:00 [ℹ]  building cluster stack "eksctl-N6-cluster"
2025-03-15 05:49:00 [ℹ]  deploying stack "eksctl-N6-cluster"
2025-03-15 05:49:30 [ℹ]  waiting for CloudFormation stack "eksctl-N6-cluster"
2025-03-15 05:50:00 [ℹ]  waiting for CloudFormation stack "eksctl-N6-cluster"
2025-03-15 05:51:01 [ℹ]  waiting for CloudFormation stack "eksctl-N6-cluster"
2025-03-15 05:52:01 [ℹ]  waiting for CloudFormation stack "eksctl-N6-cluster"
2025-03-15 05:53:02 [ℹ]  waiting for CloudFormation stack "eksctl-N6-cluster"
2025-03-15 05:54:06 [ℹ]  waiting for CloudFormation stack "eksctl-N6-cluster"
2025-03-15 05:55:06 [ℹ]  waiting for CloudFormation stack "eksctl-N6-cluster"
2025-03-15 05:56:10 [ℹ]  waiting for CloudFormation stack "eksctl-N6-cluster"
2025-03-15 05:56:11 [ℹ]  creating addon: coredns
2025-03-15 05:56:11 [ℹ]  successfully created addon: coredns
2025-03-15 05:56:12 [ℹ]  creating addon: metrics-server
2025-03-15 05:56:12 [ℹ]  successfully created addon: metrics-server
2025-03-15 05:56:12 [!]  recommended policies were found for "vpc-cni" addon, but since OIDC is disabled on the cluster, eksctl cannot configure the requested permissions; the recommended way to provide IAM permissions for "vpc-cni" addon is via pod identity associations; after addon creation is completed, add all recommended policies to the config file, under `addon.PodIdentityAssociations`, and run `eksctl update addon`
2025-03-15 05:56:12 [ℹ]  creating addon: vpc-cni
2025-03-15 05:56:13 [ℹ]  successfully created addon: vpc-cni
2025-03-15 05:56:13 [ℹ]  creating addon: kube-proxy
2025-03-15 05:56:13 [ℹ]  successfully created addon: kube-proxy
2025-03-15 05:58:15 [ℹ]  building managed nodegroup stack "eksctl-N6-nodegroup-nodes-general"
2025-03-15 05:58:15 [ℹ]  deploying stack "eksctl-N6-nodegroup-nodes-general"
2025-03-15 05:58:15 [ℹ]  waiting for CloudFormation stack "eksctl-N6-nodegroup-nodes-general"
2025-03-15 05:58:45 [ℹ]  waiting for CloudFormation stack "eksctl-N6-nodegroup-nodes-general"
2025-03-15 05:59:42 [ℹ]  waiting for CloudFormation stack "eksctl-N6-nodegroup-nodes-general"
2025-03-15 06:01:30 [ℹ]  waiting for CloudFormation stack "eksctl-N6-nodegroup-nodes-general"
2025-03-15 06:01:30 [ℹ]  waiting for the control plane to become ready
2025-03-15 06:01:32 [✔]  saved kubeconfig as "/home/ec2-user/.kube/config"
2025-03-15 06:01:32 [ℹ]  no tasks
2025-03-15 06:01:32 [✔]  all EKS cluster resources for "N6" have been created
2025-03-15 06:01:32 [ℹ]  nodegroup "nodes-general" has 2 node(s)
2025-03-15 06:01:32 [ℹ]  node "ip-10-90-224-97.us-west-2.compute.internal" is ready
2025-03-15 06:01:32 [ℹ]  node "ip-10-90-225-18.us-west-2.compute.internal" is ready
2025-03-15 06:01:32 [ℹ]  waiting for at least 2 node(s) to become ready in "nodes-general"
2025-03-15 06:01:32 [ℹ]  nodegroup "nodes-general" has 2 node(s)
2025-03-15 06:01:32 [ℹ]  node "ip-10-90-224-97.us-west-2.compute.internal" is ready
2025-03-15 06:01:32 [ℹ]  node "ip-10-90-225-18.us-west-2.compute.internal" is ready
2025-03-15 06:01:32 [✔]  created 1 managed nodegroup(s) in cluster "N6"
2025-03-15 06:01:33 [ℹ]  kubectl command should work with "/home/ec2-user/.kube/config", try 'kubectl get nodes'
2025-03-15 06:01:33 [✔]  EKS cluster "N6" in "us-west-2" region is ready
```

### Output of above
```bash
kubectl get nodes
NAME                                         STATUS   ROLES    AGE     VERSION
ip-10-90-224-97.us-west-2.compute.internal   Ready    <none>   4m32s   v1.25.16-eks-59bf375
ip-10-90-225-18.us-west-2.compute.internal   Ready    <none>   4m45s   v1.25.16-eks-59bf375
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
### To delete the cluster
```bash
eksctl delete cluster -n <name>
```

### To create eksctl custer
```bash
eksctl create --help
```
