---
date_created: 2024-06-21 14:31
author: 
date_published: 
url:
---
# Restricting S3 Bucket Access to CloudFront

# CloudFront와 S3 연동: 안전한 콘텐츠 제공 설정하기

Amazon CloudFront와 S3를 연동하여 안전하게 콘텐츠를 제공하는 방법에 대해 알아보았습니다. 

CloudFront를 S3의 원본으로 설정한 후, S3에 CloudFront만 접근 가능하도록 하는 과정을 단계별로 살펴보겠습니다.

1. S3 버킷 정책 설정하기

먼저, S3 버킷에 CloudFront만 접근할 수 있도록 버킷 정책을 수정해야 합니다. 다음과 같은 정책을 S3 버킷에 추가합니다:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowCloudFrontOnly",
            "Effect": "Allow",
            "Principal": {
                "Service": "cloudfront.amazonaws.com"
            },
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::your-bucket-name/*",
            "Condition": {
                "StringEquals": {
                    "AWS:SourceArn": "arn:aws:cloudfront::your-account-id:distribution/your-distribution-id"
                }
            }
        }
    ]
}
```

> [!NOTE]
>  `"Resource": "arn:aws:s3:::your-bucket-name/*"` 에는 S3 버킷의 ARN과 하위 path를 입력합니다. 위의 경우 `/*` 하위 모든 리소스에 대해 Allow합니다.
> `your-account-id`는 12자리 AWS 계정 ID를, `your-distribution-id`는 CloudFront 배포 ID를 입력합니다.

2. CloudFront 오리진 액세스 제어(OAC) 설정

다음으로 CloudFront에서 오리진 액세스 제어를 설정해야 합니다:

- CloudFront 콘솔에서 해당 배포의 '오리진' 탭으로 이동합니다.
- S3 오리진을 선택하고 편집합니다.
- '오리진 액세스'를 'Origin Access Control 설정(권장)'으로 변경합니다.
- 새 OAC를 생성하거나 기존 OAC를 선택합니다.

OAC 생성 시 주의할 점:
- 이름을 입력합니다 (예: "S3-OAC").
- 설명은 선택적으로 추가할 수 있습니다.
- 서명 동작은 일반적으로 "오리진 요청에 서명 안 함(권장)"을 선택합니다.

3. S3 버킷의 퍼블릭 액세스 차단

마지막으로, S3 버킷의 퍼블릭 액세스를 차단합니다:
- S3 콘솔에서 해당 버킷의 '권한' 탭으로 이동합니다.
- '퍼블릭 액세스 차단' 설정을 편집하여 모든 퍼블릭 액세스를 차단합니다.

이렇게 설정하면 CloudFront를 통해서만 S3 버킷의 콘텐츠에 접근할 수 있게 됩니다.

모바일 클라이언트 접근 시 고려사항:
- 클라이언트는 CloudFront의 도메인 이름을 사용하여 리소스에 접근합니다.
- 일반적인 HTTP/HTTPS 요청으로 충분하며, 특별한 헤더가 필요하지 않습니다.
- 보안을 위해 HTTPS 사용을 권장합니다.
- 추가 보안이 필요한 경우 CloudFront 서명된 URL이나 서명된 쿠키를 고려해볼 수 있습니다.

이렇게 설정하면 S3의 콘텐츠를 안전하게 CloudFront를 통해 제공할 수 있습니다. 클라이언트 측에서는 일반적인 웹 요청만으로 콘텐츠에 접근할 수 있어 편리하면서도 보안성이 높은 구조를 만들 수 있습니다.

추가 질문이나 자세한 설명이 필요한 부분이 있다면 언제든 물어보세요!
