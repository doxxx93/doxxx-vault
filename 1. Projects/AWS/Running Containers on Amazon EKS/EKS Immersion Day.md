---
date_created: 2024-06-12 18:56
author: 
date_published: 
url:
---
# EKS Immersion Day

# Workshop Setup

## Create EKS Cluster
```bash
	cat << EOF > eksworkshop.yaml
	apiVersion: eksctl.io/v1alpha5
	kind: ClusterConfig
	
	metadata:
	name: eksworkshop-eksctl
	region: ${AWS_REGION}
	version: "1.28"
	   
	managedNodeGroups:
	- name: nodegroup
	minSize: 2
	maxSize: 3
	desiredCapacity: 3
	instanceType: m5.large
	#volumeSize: 20
	privateNetworking: true
	ssh:
	enableSsm: true
	labels: {role: workshop}
	EOF
	
	eksctl create cluster -f eksworkshop.yaml
```
## AWS Load Balancer Controller Installation


## 
