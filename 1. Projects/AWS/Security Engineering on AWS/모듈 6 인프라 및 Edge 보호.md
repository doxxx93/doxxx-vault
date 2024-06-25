---
date_created: 2024-06-05 09:20
author: 
date_published: 
url:
---
# 모듈 6 인프라 및 Edge 보호
# 섹션 1 VPC 내부 인프라 보호
# 섹션 2 VPC 엔드포인트
## VPC 엔드포인트
# 섹션 3 신뢰할 수 있고 통제된 액세스

## ELB

- Application Load Balancer
- Network Load Balancer
- Gateway Load Balancer

고정 세션: 특정 타겟으로 트래픽을 고정한다. 성능의 이점은 있지만, 가용성이 떨어진다. AZ간의 네트워크 비용을 절감할 수 있는 효과를 볼 수 있다.

고정 또는 탄력적 IP: ELB는 노출이 되어있으므로 IP에 대한 변경이 계속 이루어진다.

[ELB 제품간 비교](https://aws.amazon.com/ko/elasticloadbalancing/features/?nc=sn&loc=2&dn=1)

### TLS(SSL) 오프로드

[TLS listeners for your Network Load Balancer - Elastic Load Balancing](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/create-tls-listener.html)
![](Pasted%20image%2020240605094109.png)

## Amazon CloudFront

[What is Amazon CloudFront? - Amazon CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)
Edge Location Service

### CF를 S3 앞단에 두는 경우

[Restricting access to an Amazon Simple Storage Service origin - Amazon CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-restricting-access-to-s3.html)

CloudFront provides two ways to send authenticated requests to an Amazon S3 origin: _origin access control_ (OAC) and _origin access identity_ (OAI).

Gateway 타입 VPC Endpoint와 유사하게 S3의 Bucket Policy를 

### CF를 ALB 앞단에 두는 경우

Security Group or listener

[Restricting access to Application Load Balancers - Amazon CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/restrict-access-to-load-balancer.html)

### CF를 EC2 앞단에 두는 경우

Security Group
[Limit access to your origins using the AWS-managed prefix list for Amazon CloudFront | Networking & Content Delivery](https://aws.amazon.com/ko/blogs/networking-and-content-delivery/limit-access-to-your-origins-using-the-aws-managed-prefix-list-for-amazon-cloudfront/)

## Amazon Route 53

1. DNS: IP -> Domain 
2. Routing 기능

# 섹션 4 외부 위협으로부터 보호

## AWS WAF

웹 ACL

### 규칙 그룹 사용

WAF를 이용하여 SQL Injection, HTTP Flood등을 예방

## Firewall Manager

- AWS Organizations에 속한 계정에만 사용할 수 있습니다.

## 위협: DDoS

완화: Shield를 사용하여 DDOS 공격으로부터 보호

