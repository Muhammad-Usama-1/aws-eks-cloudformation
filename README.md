### Amazon EKS Cluster with VPC CloudFormation Template

This repository contains an AWS CloudFormation template (`eks_with_vpc.yaml`) to deploy an Amazon EKS (Elastic Kubernetes Service) cluster along with a VPC (Virtual Private Cloud) using nested stacks.

### Description

The CloudFormation template provisions the following resources:

- **Amazon EKS Cluster**: Sets up an EKS cluster with the specified name and Kubernetes version.
- **IAM Roles**:
  - `EksRole`: IAM role for the EKS cluster with permissions to manage the cluster.
  - `EksNodeRole`: IAM role for worker nodes within the EKS cluster, granting necessary permissions.
- **Nested Stack for VPC Setup**: The VPC configuration is handled by a nested CloudFormation stack (`VpcStack`), which should be place in an S3 for example (`https://BUCKETNAME-REGION.s3.amazonaws.com/2-vpc.yml`).

### Usage

To deploy this CloudFormation template, follow these steps:

1. **Clone the Repository**:
   ```
   git clone https://github.com/yourusername/eks-cluster-cloudformation.git
   cd eks-cluster-cloudformation
   ```

2. **Deploy the Stack**:
   Use the AWS CloudFormation CLI or AWS Management Console to deploy the `eks_with_vpc.yaml` template. Ensure you have the necessary IAM permissions.

Example CLI command:
```
aws cloudformation create-stack \
  --region REGION \
  --stack-name my-eks-cluster \
  --capabilities CAPABILITY_NAMED_IAM \
  --template-body file://eks_with_vpc.yaml
```

### Parameters

The template supports the following parameters:

- **ClusterName**: The name for your EKS cluster.
- **NumberOfWorkerNodes**: The number of worker nodes in the EKS node group.
- **WorkerNodesInstanceType**: The EC2 instance type for the worker nodes.
- **KubernetesVersion**: The version of Kubernetes to use for the EKS cluster.

### Nested VPC Setup

The VPC setup is handled by a separate CloudFormation template (`vpc.yml`) referenced within the `eks_with_vpc.yaml` template. The VPC stack creates the necessary networking components such as VPC, subnets, and security groups required for the EKS cluster.

### Permissions

Ensure that the AWS IAM user/role executing this CloudFormation template has permissions to create the required resources (EKS cluster, IAM roles, networking resources).

### Contributions

Contributions and improvements to this CloudFormation template are welcome! Feel free to fork this repository, make changes, and submit pull requests.

### Disclaimer

This CloudFormation template is provided as-is, without warranties or guarantees. Use at your own risk.
