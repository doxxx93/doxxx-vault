---
date_created: 2024-06-12 12:50
author: 
date_published: 
url:
---
# 모듈 2 Amazon EKS 기본 사항

## Amazon EKS 소개

## Amazon EKS 제어 영역

## Amazon EKS 데이터 영역

대체로 AutoScaling Group으로 사용한다.
- min, max, desired capacity를 통해 관리한다.

### 데이터 영역 옵션

![](Pasted%20image%2020240612131258.png)

| 노드           | 관리형 노드 그룹       | Fargate    |
| ------------ | --------------- | ---------- |
| Server Based | Semi-Serverless | Serverless |
| EC2          | EC2 Group       | Fargate    |

### 관리형 노드 그룹

### AWS Fargate

- Fargate Profile
	- 쿠버네티스는 Fargate의 존재를 모르므로 이 Fargate는 EKS용이라는 것을 명명해줘야함

### 데이터 영역 옵션 비교

![](Pasted%20image%2020240612132159.png)
위의 표와 연결됨

## 2개의 API: Kubernetes 및 Amazon EKS

## 실습 1 준비

```
kubectl get all -n workshop
```
 - kubectl is a command-line tool used to interact with Kubernetes clusters.
    - get all retrieves all resources of all types in the specified namespace.
    - -n workshop specifies the namespace workshop to retrieve the resources from.

[Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/) 는 ECR에 있다.

![](Pasted%20image%2020240612145554.png)

