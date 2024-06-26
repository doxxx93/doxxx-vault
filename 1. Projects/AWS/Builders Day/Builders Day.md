---
date_created: 2024-06-25 10:14
author: 
date_published: 
url:
---
# Amazon VPC for a 3-tier Web App

![](Pasted%20image%2020240625101507.png)

1. VPC EC2, RDS

NAT Gateway -> AZ 영역이기 때문에 

# Container

## 컨테이너와 가상 머신 비교

- 가상 머신은 격리되어 있지만 동일한 운영체제(OS) 및 바이너리/라이브러리를 공유하지 않습니다.
- 컨테이너는 격리 되어 있지만 OS를 공유하며 필요하다면 바이너리/라이브러리를 공유합니다.


---
다음 중 Amazon Simple Queue Service(Amazon SQS) 및 AWS Lambda에 대한 설명으로 옳은 것은 무엇입니까? (2개 항목을 선택하십시오.)  
  

정답을 고르고 제출을 선택하십시오. 키보드 전용 접근성의 경우, TAB 키를 눌러 정답으로 이동한 후스페이스바**를** 눌러 선택합니다. 정답을 모두 선택할 때까지 이 단계를 반복한 다음 **ENTER** 키를 눌러 제출합니다.

- 모범 사례는 표시 제한 시간을 Lambda 함수에 대해 구성한 제한 시간의 3배로 설정하는 것입니다.
    
- **메시지를 처리할 때 Lambda 함수가 오류를 반환하면 Lambda는 대기열을 폴링하는 프로세스 수를 줄입니다.**
    
- **Lambda에는 기본적으로 대기열에서 항목을 가져오는 5개의 병렬 프로세스가 있습니다.**
    
- 대기열 크기가 증가하면 Lambda는 비용을 절감하는 데 필요한 동시성을 줄입니다.
    
- Lambda 함수가 메시지를 처리하기 전에 표시 시간 제한이 만료되면 대기열에 의해 메시지가 삭제됩니다.
---

02/05

회사에서 반려견 잠옷을 판매하는 전자 상거래 웹 사이트를 소유하고 있습니다. 제품 주문이 있을 때마다 회사는 고객에게 이메일 알림을 보내고 동시에 주문을 처리하고 재고 데이터베이스를 업데이트하려고 합니다. 인기 있는 토크쇼 주최자가 웹 사이트에 대해 이야기한 후 회사는 주문을 처리하는 데 문제를 겪고 있습니다. 회사는 종종 고객에게 중복 주문을 생성합니다.  
  

다음 아키텍처 중 회사의 요구 사항을 충족하고 더 나은 고객 경험을 제공하는 아키텍처는 무엇입니까?  
  

정답을 고르고 제출을 선택하십시오. 키보드 전용 접근성의 경우, TAB 키를 눌러 정답으로 이동한 후 스페이스바를 눌러 선택하고 ENTER 키를 눌러 제출합니다.

클레임 확인 패턴을 사용합니다. Amazon S3 버킷에 주문을 추가하고 미리 서명된 URL을 생성합니다. AWS Lambda 함수를 사용하여 해당 URL이 포함된 메시지를 표준 Amazon Simple Queue Service(Amazon SQS) 대기열로 보냅니다. Lambda를 사용하여 대기열을 폴링하고, 메시지를 필터링하고, 고객에게 이메일을 보내고, 데이터베이스를 업데이트합니다.

클레임 확인 패턴을 사용합니다. Amazon S3 버킷에 주문을 추가하고 미리 서명된 URL을 생성합니다. AWS Lambda 함수를 사용하여 해당 URL이 포함된 메시지를 선입선출(FIFO) Amazon Simple Queue Service(Amazon SQS) 대기열로 보냅니다. Lambda를 사용하여 대기열을 폴링하고, 메시지를 필터링하고, 고객에게 이메일을 보내고, 데이터베이스를 업데이트합니다.

Amazon Simple Notification Service(Amazon SNS) 팬아웃 패턴을 사용합니다. 주문이 접수되면 고객 이메일 주소와 표준 Amazon Simple Queue Service(Amazon SQS) 대기열을 구독자로 사용하여 SNS 주제로 메시지를 보냅니다. AWS Lambda를 사용하여 대기열을 폴링하고, 메시지를 필터링하고, 데이터베이스를 업데이트합니다.

**Amazon Simple Notification Service(Amazon SNS) 팬아웃 패턴을 사용합니다. 주문이 접수되면 고객 이메일 주소와 선입선출(FIFO) Amazon Simple Queue Service(Amazon SQS) 대기열을 구독자로 사용하여 SNS 주제로 메시지를 보냅니다. AWS Lambda를 사용하여 대기열을 폴링하고, 메시지를 필터링하고, 데이터베이스를 업데이트합니다.**

---
03/05

개발자 팀은 AWS Lambda 함수 중 하나가 계속 실패한다는 것을 발견했습니다. 팀 구성원 중 한 명이 서비스가 요청을 다시 시도하지 않은 이유를 궁금해 합니다.  
  

다음 중 함수가 다시 시도되지 않은 이유를 설명할 수 있는 보기는 무엇입니까?  
  

정답을 고르고 제출을 선택하십시오. 키보드 전용 접근성의 경우, TAB 키를 눌러 정답으로 이동한 후 스페이스바를 눌러 선택하고 ENTER 키를 눌러 제출합니다.

이 팀은 비동기 이벤트 소스를 사용하여 함수를 호출합니다. 이 함수에는 실패하거나 제한된 요청에 대한 재시도 기능이 기본으로 제공되지 않습니다.

팀은 실패하거나 조절된 요청에 대해 기본으로 제공되는 재시도 기능이 없는 Amazon Simple Queue Service(Amazon SQS) 대기열을 폴링하는 기능을 호출하고 있습니다.

**이 팀은 동기 이벤트 소스를 사용하여 함수를 호출합니다. 이 함수에는 실패하거나 제한된 요청에 대해 기본으로 제공되는 재시도 기능이 없습니다.**

이 팀은 Amazon Kinesis Data Streams와 같은 스트리밍 서비스를 사용하여 함수를 호출합니다. 이 함수에는 실패하거나 제한된 요청에 대해 기본으로 제공되는 재시도 기능이 없습니다.

---

04/05

장기 실행 트랜잭션에 대한 상태 정보를 얻기 위해 다음 중 상태 업데이트를 전달하기 위해 어떤 패턴을 사용합니까?  
  

정답을 고르고 제출을 선택하십시오. 키보드 전용 접근성의 경우, TAB 키를 눌러 정답으로 이동한 후 스페이스바를 눌러 선택하고 ENTER 키를 눌러 제출합니다.

AWS AppSync를 사용한 WebSocket

**클라이언트 폴링 패턴**

AWS Step Functions를 사용한 Saga 패턴

Amazon Simple Notification Service(Amazon SNS)를 사용한 Webhook

---

05/05

다음 중 서버리스 데이터 처리에 스트리밍 서비스를 사용하는 속성은 무엇입니까? (2개 항목을 선택하십시오.)  
  

정답을 고르고 제출을 선택하십시오. 키보드 전용 접근성의 경우, TAB 키를 눌러 정답으로 이동한 후스페이스바**를** 눌러 선택합니다. 정답을 모두 선택할 때까지 이 단계를 반복한 다음 **ENTER** 키를 눌러 제출합니다.

- 스트리밍 서비스의 경우 데이터가 소비되면 삭제됩니다.
    
- **스트림의 데이터는 지정된 기간 동안 스트림에 남아 있으며 소비자 동작에 관계없이 삭제됩니다.**
    
- **각 스트림 소비자는 스트림의 특정 위치에 대한 포인터를 유지해야 합니다. 메시지를 소비한 후 소비자는 다음 레코드로 포인터를 이동하여 해당 레코드를 처리합니다.**
    
- 스트리밍 서비스를 사용하면 특정 시도 횟수까지 재시도를 구성할 수 있으며 서비스에 배달 못한 편지 대기열이 기본 제공됩니다.
    
- 메시징 서비스를 사용하는 경우 핵심 엔터티는 개별 메시지입니다.

---

개발자 팀에는 현재 Docker에서 실행되는 애플리케이션이 있습니다. 여러분은 최근에 인프라 관리 부담을 없애주는 서버리스 기술에 대해 읽었습니다. 팀에 이 이야기를 하니 애플리케이션을 “서버리스로 구현할 수 없다”고 반박합니다. 팀은 애플리케이션을 다시 작성하고 싶지 않으며 장기 실행 태스크가 서버리스 작업에 적합하다고 생각하지 않는다고 말합니다.  
  

개발자의 인프라 관리 부담을 최소화하면서 팀의 요구 사항을 충족하는 서비스는 무엇입니까?

AWS Lambda

Amazon Elastic Kubernetes Service(Amazon EKS)

**AWS Fargate**

Amazon EC2

---
02/04

왼쪽의 각 AWS 데이터 스토어를 오른쪽의 해당 사용 사례와 연결하십시오. 왼쪽 열을 오른쪽으로 이동하여 항목을 연결하십시오.

- Amazon ElastiCache for Redis: - 밀리초 미만의 읽기 및 쓰기 지연 시간이 요구되는 최상위 값의 정렬된 리더보드
    
- Amazon Relational Database Service(Amazon RDS): - 운영 오버헤드를 줄이는 CMS를 지원하는 관계형 데이터 스토어
    
- Amazon Simple Storage Service(Amazon S3): - 높은 확장성과 유연성으로 인해 데이터 레이크용으로 적합
    
- Amazon DynamoDB: 3억 명의 사용자를 대상으로 플레이어 게임 상태를 저장하고 밀리초 단위의 액세스 속도 유지
    
- Amazon Quantum Ledger Database(Amazon QLDB): - 조직의 은행 거래에서 대변 및 차변 내역 추적

--- 
조직이 API를 생성하고 레거시 애플리케이션의 구성 요소를 점진적으로 교체하는 이벤트 기반 구성 요소를 빌드하여 모놀리식 애플리케이션을 점진적이고 체계적으로 분해하는 마이그레이션 패턴은 다음 중 어느 것입니까?

도약

**스트랭글러**

오가닉

사가

---
04/04

서버리스 애플리케이션의 모범 사례는 다음 중 어느 것입니까? (3개 선택)

- **이미 있는 것을 다시 만드느라 시간을 낭비하지 않습니다.**
    
- 관련된 모든 서비스의 한도가 요구 사항에 맞춰 조정된다는 것을 전제합니다.
    
- 가능한 한 빨리 AWS 외부의 서비스에 이벤트를 전송합니다.
    
- **멱등성 스테이트리스 함수를 선호합니다.**
    
- 간편한 서버리스 통합을 위해 코드를 포팅합니다.
    
- **최신 상태를 유지합니다.**

---

Lambda 함수가 Kinesis Data Streams 레코드를 적절한 시기에 처리하지 못하고 Lambda 대시보드에서 IteratorAge 지표가 증가하고 있습니다.  
  

이 문제를 해결하기 위한 최선의 전략은 무엇입니까?

처리 실패를 관리하기 위해 배달 못한 편지 대기열을 설정합니다.

**리샤딩을 사용하여 스트림의 샤드 수를 늘립니다.**

수신 메시지를 배치로 처리하여 성능을 높입니다.

스트림의 레코드에 대한 보존 기간을 늘립니다.

CloudWatch 지표 대시보드를 검토하고 AWS X-Ray를 사용하여 병목 현상을 파악합니다.

---

어떤 확장 모범 사례를 따라야 합니까? (2개 선택)

- 애플리케이션과 데이터베이스를 결합합니다.
    
    Correctly unchecked
    
- **AWS 글로벌 클라우드 인프라를 활용합니다.**
    
    Correctly checked
    
- 힘든 작업을 파악하고 생성합니다.
    
    Correctly unchecked
    
- **백분위수를 모니터링합니다.**
    
    Correctly checked
    
- 나중에 리팩터링할 필요가 없도록 처음부터 리팩터링합니다.
---
AWS Lambda 함수를 크기 조정할 때 고려해야 할 사항은 무엇입니까? (3개 선택)

- **버스트 동작**
    
- 인프라 유지 관리
    
- **메모리 구성**
    
- **동시성 제한**
    
- 코드 재사용성
    
- Auto Scaling 구성

---

다음 중 데이터베이스 크기 조정에 권장되는 접근 방식을 반영한 설명은 무엇입니까? (2개 선택)

- Amazon DynamoDB 온디맨드 모드는 매우 일관되고 예측 가능한 워크로드에 적합합니다.
    
- **Amazon DynamoDB 온디맨드 모드는 개별 트랜잭션 비용을 추적해야 하는 경우에 적합합니다.**
    
- **워크로드가 일관되고 예측 가능한 경우 프로비저닝된 용량이 더 나은 선택일 수도 있습니다.**
    
- Amazon DynamoDB Accelerator(DAX)는 더 긴 지연 시간이 허용되는 트랜잭션을 오프로드하는 데 유용한 솔루션입니다.
    
- 전통적인 관계형 데이터베이스에 연결하는 가장 좋은 방법은 동시성 한도를 사용하여 AWS Lambda가 호출할 수 있는 동시 데이터베이스 연결 수를 제한하는 것입니다.

---

한 회사에서 일련의 AWS Lambda 함수와 Amazon DynamoDB 테이블로 구성된 AWS Step Functions 워크플로를 설계하고 있습니다. 애플리케이션의 워크로드가 매우 일관되고 예측 가능한 것으로 보이며 비용이 높습니다. 귀하는 애플리케이션 아키텍처를 분석하고 비용을 절감할 수 있는 권장 사항을 제시하도록 이 회사에 고용되었습니다.  
  

다음 중 아키텍처 비용을 낮출 수 있는 옵션은 무엇입니까? (3개 선택)

- **Step Functions에서 대기 상태 및 콜백을 사용합니다.**
    
- DynamoDB Auto Scaling을 온디맨드 용량과 함께 사용합니다.
    
- **AWS Lambda Power Tuning을 사용합니다.**
    
- **DynamoDB에 프로비저닝된 용량을 사용합니다.**
    
- 관계형 데이터베이스를 사용하여 비용을 절감합니다.
    
- DynamoDB에 Amazon EC2 적정한 크기 조정을 사용합니다.

---

개발자가 AWS Lambda 함수, API, Amazon DynamoDB 테이블 및 Amazon S3 버킷으로 구성된 분산 서버리스 애플리케이션을 만들고 있습니다. 최근에 이 개발자는 특정 API 호출을 수행할 때 지연 시간이 증가하는 문제를 발견했습니다.  
  

이 성능 문제를 해결하는 데 도움이 되는 AWS 서비스 또는 기능은 무엇입니까? 

Amazon CloudWatch Logs에서 print 문을 사용하여 문제를 해결합니다.

**AWS X-Ray를 사용하여 적절한 추적 세그먼트를 살펴봅니다.**

AWS Config를 사용하여 지연 시간이 높을 때 알림을 보내는 규칙을 생성합니다.

Amazon API Gateway 캐싱을 사용하여 지연 시간을 줄입니다.

---

AWS Lambda 함수는 연결 문자열과 정기적으로 교체되는 암호를 사용하여 데이터베이스에 액세스해야 합니다. 이러한 항목은 안전하게 보관해야 하며 애플리케이션 내에 하드 코딩할 수 없습니다.  
  

이를 수행하는 데 도움이 되는 AWS 서비스는 무엇입니까? (2개 선택)

- AWS Config 
    
- **AWS Key Management Service(AWS KMS)**
    
- AWS Lambda Authorizer
    
- Amazon Cognito
    
- **AWS Systems Manager Parameter Store**
---

03/05

서버리스 애플리케이션을 모니터링하는 데 사용할 수 있는 AWS 서비스는 무엇입니까? (2개 선택)

- AWS AppSync
    
- **Amazon CloudWatch**
    
- **AWS X-Ray**
    
- AWS Global Accelerator
    
- AWS Lambda
---
개발 팀이 방금 안정적인 애플리케이션을 AWS Lambda로 마이그레이션했습니다. 이제 애플리케이션의 패치 버전을 점진적으로 안전하게 릴리스하려고 합니다. 팀은 모든 트래픽을 새로운 함수로 전달하기 전에 30분 동안 패치 버전으로 10%의 트래픽을 보낼 계획입니다.

  

다음 중 팀에서 새로운 기능을 테스트하기 위해 사용할 수 있는 전략은 무엇입니까? (2개 항목 선택)

  

정답을 선택하고 제출을 눌러주십시오.

- **AWS SAM(AWS Serverless Application Model)을 사용하여 Canary10Percent30Minutes 배포 기본 설정을 구성합니다.**
    
- Amazon API Gateway를 사용하여 version2라는 새 스테이지를 API에 배포합니다.
    
- **Lambda API를 사용하여 별칭의 트래픽 이동을 활성화합니다.**
    
- 두 번째 Amazon API Gateway 리소스를 만들고 $LATEST 버전의 Lambda 함수를 통합합니다.
    
- AWS CloudFormation을 사용하여 Linear10Percent30Minutes 배포 기본 설정을 구성합니다.
---
Lambda 함수를 생성할 때 존재하는 1가지 버전을 어떻게 지칭합니까>

  

정답을 선택하고 제출을 눌러주십시오.

**$LATEST**

별칭

주요 함수

템플릿

---

다음 섹션에서 왼쪽 열의 REST API 엔드포인트 유형을 오른쪽의 올바른 설명과 연결하십시오. 

  

키보드를 사용하여 탐색하는 경우 왼쪽에 있는 TAB 키를 눌러 왼쪽의 용어로 이동하고 SPACE BAR를 누른 다음 오른쪽 화살표 키를 사용하여 오른쪽 열로 이동합니다. SPACE BAR를 눌러 연결한 후 다음 항목도 같은 방법으로 반복합니다. ENTER 키를 눌러 제출합니다.


    
- 
    

- - 리전 엔드포인트:동일한 AWS 리전 내에서 API를 호출하는 애플리케이션의 지연 시간을 단축합니다.
    
- 엣지 최적화 엔드포인트 완전관리형 Amazon CloudFront 배포를 배포합니다.
    
- 프라이빗 엔드포인트: 요청은 사용자가 제어하는 단일 Virtual Private Cloud(VPC) 내에서만 라우팅할 수 있습니다.
---
다음 중 API Gateway에서 지원되지 않는 REST API 엔드포인트 유형 변경은 무엇입니까? 정답을 선택하고 제출을 선택하십시오. 

  

키보드를 사용하여 탐색하는 경우 TAB 키를 눌러 정답으로 이동하고 SPACE BAR를 눌러 선택한 다음 ENTER 키를 눌러 제출합니다.

엣지 최적화에서 리전 또는 프라이빗으로



리전에서 엣지 최적화 또는 프라이빗으로



프라이빗에서 리전으로


**프라이빗에서 엣지 최적화로**

---
124

---
다음 중 Amazon API Gateway용 REST API에 사용할 수 없는 엔드포인트 유형은 무엇입니까? (3개 선택) 정답을 선택하고 제출을 선택하십시오. 

  

키보드를 사용하여 탐색하는 경우 TAB 키를 눌러 정답으로 이동하고 SPACE BAR를 눌러 선택합니다. 모든 정답을 선택할 때까지 이 단계를 반복한 다음 ENTER 키를 눌러 제출하십시오.

- 퍼블릭 엔드포인트
    
- **엣지 최적화 엔드포인트**
    
- 네이티브 OpenID 또는 OAuth 2
    
- **리전 엔드포인트**
    
- **프라이빗 엔드포인트**
    
- 모의 통합
---
다음 중 WebSocket API의 사용 사례가 아닌 것은 무엇입니까?

채팅 애플리케이션

**API Gateway를 사용하여 캐시해야 하는 애플리케이션**

멀티플레이어 게임

금융 거래 플랫폼

---
다음 중 API를 모니터링하고 로깅하는 데 사용할 수 있는 도구는 무엇입니까? (3개 선택) 정답을 선택하고 제출을 선택하십시오. 

  

키보드를 사용하여 탐색하는 경우 TAB 키를 눌러 정답으로 이동하고 SPACE BAR를 눌러 선택합니다. 모든 정답을 선택할 때까지 이 단계를 반복한 다음 ENTER 키를 눌러 제출하십시오.

- AWS AppSync
    
- **Amazon CloudWatch**
    
- **AWS X-Ray**
    
- **AWS CloudTrail**
    
- AWS Global Accelerator
    
- AWS Lambda
---
다음 중 Amazon API Gateway의 사전 정의된 WebSocket 경로가 아닌 것은 무엇입니까? (3개 선택) 정답을 선택하고 제출을 선택하십시오. 

  

키보드를 사용하여 탐색하는 경우 TAB 키를 눌러 정답으로 이동하고 SPACE BAR를 눌러 선택합니다. 모든 정답을 선택할 때까지 이 단계를 반복한 다음 ENTER 키를 눌러 제출하십시오.

- **$default 경로**
    
- **$disconnect 경로**
    
- 사용자 지정 경로
    
- **$connect 경로**
    
- VPC 링크
    
- 모의 통합

---
다음 중 Amazon API Gateway의 스테이지에 대한 정확한 설명은 무엇입니까? 정답을 선택하고 제출을 선택하십시오. 

  

키보드를 사용하여 탐색하는 경우 TAB 키를 눌러 정답으로 이동하고 SPACE BAR를 눌러 선택한 다음 ENTER 키를 눌러 제출합니다.

API URL을 사용자에게 좀 더 의미 있게 만드는 방법

메서드 요청 데이터가 백엔드로 전달되는 방식을 결정하는 방법

요청 실패를 야기하는 매핑 오류 문제를 해결하는 데 유용한 설정

**API의 스냅샷이며 배포된 API 버전의 고유 식별자**

