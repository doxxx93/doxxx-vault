---
date_created: 2024-06-03 13:45
author: 
date_published: 
url:
---
# Security Engineering on AWS 

# 실습 1: 자격 증명 기반 정책 및 리소스 기반 정책 사용

## Session Manager

IAM을 통해서 

기존의 SSH를 이용해야하던 걸 

## 과제 1: EC2 인스턴스에 연결된 IAM 역할 보기 및 평가

# 실습 2: AWS Directory Service를 사용하여 도메인 사용자 액세스 관리

![](Pasted%20image%2020240603162655.png)

# 실습 3 - AWS KMS를 사용하여 Secrets Manager 보안 암호 암호화

## 태스크 1: 보안 암호를 사용하여 Amazon RDS 데이터베이스에 액세스할 수 있는지 확인

AWS Secrets Manager 보안 암호를 생성하여 자격 증명을 저장하기 전에 Amazon RDS 데이터베이스에 수동으로 연결할 수 있는지 확인합니다.

```
mysql -u dbadmin -p -h DB_ENDPOINT
```

- EC2 인스턴스와 RDS 간의 네트워크 연결:
    - EC2 인스턴스와 RDS 데이터베이스는 일반적으로 동일한 VPC (Virtual Private Cloud) 내에 위치합니다.
    - VPC 내에서 EC2 인스턴스와 RDS 간에는 프라이빗 IP를 통한 네트워크 통신이 가능합니다.
    - 이러한 네트워크 연결을 통해 EC2 인스턴스에서 RDS 데이터베이스에 접근할 수 있습니다.
- 보안 그룹 설정:
    - RDS 데이터베이스에 연결된 보안 그룹에서 EC2 인스턴스의 보안 그룹을 인바운드 규칙으로 허용해야 합니다.
    - 이를 통해 EC2 인스턴스에서 RDS로의 트래픽을 허용할 수 있습니다.
    - 일반적으로 RDS 보안 그룹에서 EC2 보안 그룹을 참조하여 인바운드 규칙을 설정합니다.
- RDS 엔드포인트 및 인증 정보:
    - RDS 데이터베이스에는 고유한 엔드포인트 주소가 할당됩니다.
    - 이 엔드포인트 주소를 사용하여 EC2 인스턴스에서 RDS에 접속할 수 있습니다.
    - 또한 RDS 데이터베이스에 접속하기 위해서는 적절한 인증 정보 (사용자 이름, 비밀번호 등)가 필요합니다.

## 태스크 3: AWS Secrets Manager 보안 암호를 생성하고 AWS KMS 키로 암호화

![](Pasted%20image%2020240604110353.png)

```java
// Use this code snippet in your app.
// If you need more information about configurations or implementing the sample
// code, visit the AWS docs:
// https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/home.html

// Make sure to import the following packages in your code
// import software.amazon.awssdk.regions.Region;
// import software.amazon.awssdk.services.secretsmanager.SecretsManagerClient;
// import software.amazon.awssdk.services.secretsmanager.model.GetSecretValueRequest;
// import software.amazon.awssdk.services.secretsmanager.model.GetSecretValueResponse;	

public static void getSecret() {

    String secretName = "dbadmin_secret";
    Region region = Region.of("us-west-2");

    // Create a Secrets Manager client
    SecretsManagerClient client = SecretsManagerClient.builder()
            .region(region)
            .build();

    GetSecretValueRequest getSecretValueRequest = GetSecretValueRequest.builder()
            .secretId(secretName)
            .build();

    GetSecretValueResponse getSecretValueResponse;

    try {
        getSecretValueResponse = client.getSecretValue(getSecretValueRequest);
    } catch (Exception e) {
        // For a list of exceptions thrown, see
        // https://docs.aws.amazon.com/secretsmanager/latest/apireference/API_GetSecretValue.html
        throw e;
    }

    String secret = getSecretValueResponse.secretString();

    // Your code goes here.
}
```

위와 같은 방식으로 application 에서도 사용 가능하다.

# 실습 4 - Amazon S3의 데이터 보안

### 시나리오

여러분은 AnyCompany의 보안 엔지니어로서 S3 버킷에 저장된 데이터를 보호하기 위한 회사의 데이터 보호 전략을 적용하는 업무를 맡았습니다. 이러한 전략에는 다음이 필요합니다.

- S3 버킷에 저장된 데이터는 동일한 버킷 리전에서 관리하는 AWS KMS 키로 서버 측 암호화(SSE)를 사용하여 암호화됩니다.
- S3 버킷에 업로드된 데이터는 올바른 암호화 방법과 AWS KMS 키를 사용하지 않을 경우 거부되어야 합니다.
- 기본 리전의 S3 버킷에 저장된 데이터는 다중 리전 복원력을 제공하기 위해 보조 리전의 다른 S3 버킷에 복제되어야 합니다. 또한 이 데이터는 해당 리전의 다른 AWS KMS 키를 사용하여 보조 리전에서도 암호화해야 합니다.
- S3 버킷에 저장된 데이터에는 개인 식별 정보(PII)가 포함되지 않아야 합니다.

## 과제 1: 기본 및 보조 리전에 AWS KMS 키 생성

이 과제에서는 2개의 AWS KMS 키를 생성합니다. 각 키는 해당 리전의 Amazon S3 버킷에 대한 서버 측 암호화(SSE)에 사용됩니다. 회사의 데이터 보호 전략의 일환으로 보안 규정 준수에서는 Amazon S3 버킷에 저장된 모든 데이터를 사용자가 관리하는 서버 측 암호화 AWS KMS 키로 암호화하도록 요구합니다.
 
 
 **참고:** 이 replication-kms-key는 replication-bucket으로의 복제된 객체를 암호화하는 데 사용됩니다. replication-bucket은 후속 과제에서 원본 버킷의 데이터를 복제하기 위한 재해 복구 리전 버킷으로 사용됩니다.

## 과제 2: AWS KMS 키를 사용하여 S3 버킷의 데이터 암호화

각 리전에서 KMS를 통해 key create

각 버킷의 properties에서 SSE-KMS를 이용하여 서로 상응하는 키로 설정

## 과제 3: 승인되지 않은 암호화 방법 및 키를 사용하는 S3 객체 업로드 방지

**Permissions** 탭을 선택하고 **Bucket Policy**

```JSON
{
    "Version": "2012-10-17",
    "Statement": [
      {
                "Sid": "Deny Incorrect AWS KMS Keys or encryption key types",
                "Effect": "Deny",
                "Principal": "*",
                "Action": "s3:PutObject",
                "Resource": "arn:aws:s3:::REPLACE_WITH_YOUR_ORIGINAL_BUCKET_NAME/*",
                "Condition": {
                    "StringNotEquals": {
                          "s3:x-amz-server-side-encryption-aws-kms-key-id": "REPLACE_WITH_YOUR_ORIGINAL_KMS_KEY_ARN"
                             }
                   }
           }
    ]
}

```

이제 그냥 upload 하게 되면 kms로 업로드 됨, 버킷 정책에 맞지 않는 키를 사용하면 업로드 안됨

- **Upload without setting extra encryption options**: 버킷에서 AWS KMS **original-kms-key**가 기본 옵션으로 설정되었으며 버킷 정책의 키와 일치하므로 업로드가 성공적으로 수행됩니다.
    
- **Upload with SSE-KMS and using AWS managed key (aws/s3)**: 버킷 정책에 구성된 키(original-kms-key)가 사용되지 않으므로 업로드가 실패합니다.

## 과제 4: Macie를 사용하여 S3 버킷의 객체에 저장된 개인 식별 정보(PII) 식별

## 과제 5: 재해 복구 리전 버킷으로 데이터 복제

## 과제 6: Macie 작업 결과 확인

# 실습 5 - AWS WAF를 사용하여 악성 트래픽 완화

## 태스크 1: WAF Automation on AWS CloudFormation 템플릿이 생성한 리소스를 검토합니다.

AWS에서 WAF 자동화 솔루션은 일반적인 웹 기반 공격을 필터링하는 일련의 AWS WAF 규칙을 자동 배포합니다. AWS WAF 웹 액세스 제어 목록(웹 ACL)에 포함된 규칙을 정의하는 미리 구성된 보호 기능 중에서 선택할 수 있습니다. 솔루션 배포 후 AWS WAF는 웹 요청을 검사하여 Amazon CloudFront 배포 또는 Application Load Balancer를 보호할 수 있습니다.

AWS WAF를 사용하여 공격 패턴을 차단하는 사용자 지정 애플리케이션별 규칙을 생성하여 애플리케이션 가용성을 보장하고 리소스를 보호하며 과도한 리소스 사용을 방지할 수 있습니다.

WAF Automation on AWS 솔루션은 최신 버전의 AWS WAF(AWS WAFV2) 서비스 API를 지원합니다.

![](Pasted%20image%2020240605104908.png)

### 태스크 1.1: CLOUDFORMATION의 리소스 목록 검토

 **Stacks** 페이지에서 두 개의 스택(하나는 이름에 **WafAutomation**이 있고 다른 하나는 이름에 **WebACLStack**이 있음)이 습니다.

**WafAutomation**: IAM 역할, Lambda 함수 및 CloudWatch 대시보드와 같은 리소스를 찾아야 합니다.
**WebACLStack**: AWS WAF 웹 ACL, IP 집합, 사용자 지정 타이머 및 Lambda 함수와 같은 리소스를 찾아야 합니다.

### 태스크 1.2: CLOUDFORMATION 템플릿이 생성한 WAF 리소스 검토

**WAF & Shield** 탐색 창에서 **AWS WAF** 아래의 **Web ACLs**를 선택합니다.

![](Pasted%20image%2020240605111418.png)
**HttpFloodRateBasedRule** 페이지에서 **Rule** 및 **Action** 세부 정보를 검토합니다.
    

실습 환경 구축 프로세스 중에 CloudFormation 템플릿을 배포할 때 HTTP 플러드 속도 제한의 기본값은 5분 내에 100개의 연결로 설정되었습니다. HttpFloodRateBasedRule 규칙은 이 규칙이 속한 웹 ACL에 할당된 리소스에 대한 HTTP 연결 시도가 100회를 초과하는 경우 연결을 시도하는 원본 IP를 차단하도록 지정합니다.


**SqlInjectionRule** 페이지에서 규칙에 포함된 다양한 스테이트먼트와 작업을 검토합니다.

SqlInjectionRule 규칙은 쿼리 문자열 또는 URI 경로와 같은 여러 쿼리 유형에서 악의적인 SQL 코드를 찾습니다. 나열된 양식 중 하나에서 SQL 명령어 삽입 공격이 탐지되면 요청이 차단됩니다

## 태스크 2: HTTP 플러드 방지 검토

### 태스크 2.2: 애플리케이션 로드 밸런서를 AWS WAF 웹 ACL에서 리소스로 추가

**Add AWS resources** 팝업 창에서
- **Resource type**에 **Application Load Balancer**를 선택합니다.
- **Name**에 **web-server-alb**를 선택합니다.


_web-server-alb_ 애플리케이션 로드 밸런서가 랩 환경 구축 프로세스 중에 생성되었습니다. 퍼블릭 서브넷에 배포되고 프라이빗 서브넷에 배포된 웹 서버의 프런트 엔드로 사용됩니다.

## 태스크 3: SQL 명령어 삽입 보호 검사

### 태스크 3.2: API를 AWS WAF 웹 ACL에서 리소스로 추가

**Add AWS resources** 팝업 창에서
- **Resource type**에서 **Amazon API Gateway REST API**가 선택되지 않았으면 선택합니다.
- **Name**에 **lab-rds-api - Dev**를 선택합니다.

# 실습 6: 보안 인시던트 모니터링 및 대응

## 태스크 1: Amazon CloudWatch Logs 에이전트 설치 및 구성

## 태스크 2: 실패한 로그인 시도를 모니터링하는 Amazon CloudWatch 경보 생성

## 태스크 3: VPC 흐름 로그 및 CloudWatch Logs Insights를 구성하여 SSH 연결 시도 찾기

# 실습 7: 인시던트 대응

### 시나리오

여러분은 AnyCompany의 보안 엔지니어로, 여러 번의 로그인 시도 실패가 탐지된 애플리케이션 서버 중 하나에서 잠재적인 보안 위반에 대한 경고를 받았습니다. 이제 인스턴스 분석을 안전하게 수행하여 실제로 위반이 발생했는지 확인하고, 이로 인해 발생한 취약성을 해결하고, 문제를 해결해야 합니다.

![](Pasted%20image%2020240605161347.png)
## 과제 1: 모든 손상된 인스턴스 영구 디스크 및 메타데이터 캡처



## 과제 3: 인스턴스 설정을 업데이트하여 취약성 완화


## 과제 4: 인시던트 대응 작업을 처리하기 위한 자동화된 인시던트 대응 생성

이 과제에 사용되는 시나리오는 다음과 같습니다.

- app-server에 대해 SSH 실패 시도가 시작됩니다. jump-server에 의해 시도가 시뮬레이션됩니다.
- app-server가 SSH 인증 실패 로그를 생성하고 이 로그를 CloudWatch 로그 그룹으로 보냅니다.
- CloudWatch 로그 그룹에는 SSH 인증 실패 로그와 일치하는 사전 구성된 구독 필터가 있으며 이를 사전 구성된 Lambda 함수(Log Enhancement Lambda)로 전송합니다.
- 로그 보강 Lambda는 app-server 내부 IP 주소를 캡처하고 인스턴스 ID를 검색합니다. 그런 다음 이벤트를 인스턴스 ID가 포함된 Amazon EventBridge로 보냅니다.
- EventBridge 규칙은 수신 이벤트와 일치하며 Automation Lambda가 자동화된 인시던트 대응 과제를 수행하도록 트리거합니다.

시나리오는 아래 다이어그램에 설명되어 있습니다.

![](Pasted%20image%2020240605170323.png)