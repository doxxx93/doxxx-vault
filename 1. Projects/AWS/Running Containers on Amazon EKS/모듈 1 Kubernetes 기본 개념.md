---
date_created: 2024-06-12 09:44
author: 
date_published: 
url:
---
# 모듈 1 Kubernetes 기본 개념

## 컨테이너의 이점

[Pods | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/#pod-templates)

Menifest file 을 통해 pod의 스펙을 지정한다.
PodTemplates are specifications for creating Pods

[RFC1918 정리: Address Allocation for Private Internets - Real Insight Comes From Fixing Error](https://www.getoutsidedoor.com/2021/03/30/rfc1918-%EC%A0%95%EB%A6%AC-address-allocation-for-private-internets/)

부족해진 IPv4 와 관련된 RFC

### 서비스

Kubernetes에서 서비스란 여러 Pod의 논리적 모음과 여기에 액세스하는 수단입니다. 서비스는 사용 가능한 Pod 세트로 지속적으로 업데이트되며, 각 Pod IP 주소는 통신의 엔드포인트 역할을 합니다. 각 서비스에는 ClusterIP라고 하는 고유한 가상 IP 주소가 할당됩니다. 해당 값은 클러스터 내에서 고유합니다. 클라이언트는 서비스의 가상 ClusterIP 주소에 연결되고, 서비스는 통신 요청을 서비스 뒤에 있는 엔드포인트 Pod 중 하나로 변환합니다. 이렇게 하면 Pod가 다른 Pod의 주소를 직접 추적할 필요가 없습니다.

이 예에서는 프런트엔드 webapp Pod가 백엔드 애플리케이션에 액세스해야 합니다. 고가용성 스테이트리스 앱을 위한 백엔드 Pod 모음의 경우 어떤 Pod와 통신하는지가 중요한 것이 아니고, 프런트엔드 webapp이 백엔드 애플리케이션의 인스턴스에 안정적으로 연결할 수 있어야 합니다. 이 서비스는 포트 80에서 요청된 애플리케이션에 대한 연결 요청을 분산합니다. 그런 다음 애플리케이션을 'app=backend" 레이블이 있는 모든 Pod에 매핑합니다. 이 서비스는 그 Pod에 구성된 대상 포트(이 예에서는 80)를 사용합니다.

Pod들을 위한 로드 밸런서라고 생각하면 된다. Round Robin

### 쿠버네티스 내부

[Controllers | Kubernetes](https://kubernetes.io/docs/concepts/architecture/controller/)

![](Pasted%20image%2020240612103453.png)
Control Plane <-> Nodes

### Pod Scheduling

[파드 및 컨테이너 리소스 관리 | Kubernetes](https://kubernetes.io/ko/docs/concepts/configuration/manage-resources-containers/#%EC%9A%94%EC%B2%AD-%EB%B0%8F-%EC%A0%9C%ED%95%9C)

[테인트(Taints)와 톨러레이션(Tolerations) | Kubernetes](https://kubernetes.io/ko/docs/concepts/scheduling-eviction/taint-and-toleration/)

### kubectl utility

### Kubernetes

- [Namespaces | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)
- [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/), [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)
- [Workload Management | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/)
	- [Jobs | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/job/)
		- 베어 Pod보다는 워크로드를 생성하는 것이 좋습니다. 작업의 경우 '베어 Pod'와 작업의 차이점
		- [Kubernetes Domain Starter](https://catalog.us-east-1.prod.workshops.aws/workshops/5f769b4f-8b4a-4308-81df-4af63687fa44/en-US/021-running-at-scale#workload-resource-types)
	- [StatefulSets | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)
![](Pasted%20image%2020240612111821.png)


## 컨테이너 오케스트레이션

## Kubernetes 내부 Pod 스케쥴링

## kubectl 유틸리티(데모)

## Kubernetes 객체

## 지식 확인 및 활동
