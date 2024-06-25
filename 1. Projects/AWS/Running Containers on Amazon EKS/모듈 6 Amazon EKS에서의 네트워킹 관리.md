---
date_created: 2024-06-13 15:17
author: 
date_published: 
url:
---
# 모듈 6 Amazon EKS에서의 네트워킹 관리
## 복습: AWS의 네트워킹
## Amazon EKS의 통신
## Pod 수준 보안 개선
## 서비스를 사용한 로드 밸런싱

인스턴스 모드와 IP 모드에서의 로드 밸런서 동작 방식을 비교하며, 각 모드에서 ClusterIP와 NodePort의 역할과 외부 접근 가능성에 대해 설명드리겠습니다.

### 인스턴스 모드 (Instance Mode)

1. **로드 밸런서**:
    
    - 로드 밸런서는 각 노드의 `NodePort`로 트래픽을 전달합니다.
2. **NodePort**:
    
    - 각 노드는 NodePort로 들어오는 트래픽을 받아들입니다.
    - 노드의 `kube-proxy`는 NodePort로 들어오는 트래픽을 클러스터 내의 실제 Pod로 전달합니다.
3. **ClusterIP**:
    
    - ClusterIP는 클러스터 내부에서만 사용됩니다.
    - 외부에서는 ClusterIP에 직접 접근할 수 없습니다.

**요약**: 로드 밸런서 -> NodePort -> kube-proxy -> Pod

### IP 모드 (IP Mode)

1. **로드 밸런서**:
    
    - 로드 밸런서는 서비스의 `ClusterIP`로 직접 트래픽을 전달합니다.
2. **ClusterIP**:
    
    - 클러스터 내에서 ClusterIP를 확인하고 실제 Pod로 트래픽을 전달합니다.
    - NodePort는 사용되지 않습니다.

**요약**: 로드 밸런서 -> ClusterIP -> Pod

### 인스턴스 모드에서의 외부 접근

인스턴스 모드에서 NodePort는 외부 접근을 위해 사용됩니다. 외부의 로드 밸런서가 각 노드의 NodePort로 트래픽을 전달하기 때문에, NodePort는 외부에 노출되어 있습니다. 반면 ClusterIP는 클러스터 내부에서만 사용되며 외부에서 접근할 수 없습니다.

### 정리

**인스턴스 모드**:

- **NodePort**: 외부 접근을 위한 포트, 로드 밸런서가 각 노드의 NodePort로 트래픽을 전달.
- **ClusterIP**: 내부 통신에만 사용, 외부에서는 접근 불가.

**IP 모드**:

- **ClusterIP**: 로드 밸런서가 직접 접근하여 트래픽 전달, NodePort는 사용되지 않음.

**왜 ClusterIP가 외부로 노출되지 않는지?**

- 인스턴스 모드에서는 NodePort가 외부 접근을 담당하고, ClusterIP는 클러스터 내부에서만 사용됩니다. 따라서, 외부에서 로드 밸런서는 NodePort를 통해 접근하고, ClusterIP는 외부에 노출되지 않습니다. ClusterIP는 클러스터 내부에서 Pod 간의 통신을 위해 사용됩니다.

이와 같이, 인스턴스 모드에서는 NodePort가 외부 접근의 게이트웨이 역할을 하며, IP 모드에서는 ClusterIP가 로드 밸런서에 의해 직접 접근됩니다.
## 지식 확인