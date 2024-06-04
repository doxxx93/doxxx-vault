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