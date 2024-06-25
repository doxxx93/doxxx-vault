---
date_created: 2024-06-04 14:42
author:
date_published: 
url:
---
# 모듈 4 AWS에서의 키 및 보안 암호 관리

## 섹션 1: AWS KMS

- 암호화 주체

	- Client
		- 
	
	- Server
		- 전송에 대한 보안

- 암호화 방식
	- 대칭키
		- 누출에 대한 위험
		- 빠르다
	- 비대칭키
		- 느리다

- AWS 서버측 암호화는 대칭키 암호화 방식을 이용한다.
	- 봉투 암호화

![](Pasted%20image%2020240604092738.png)

### KMS의 이점

데이터 키와 암호화된 데이터 키를 준다.

### Multi Region에서 KMS 이용하기

이 기능은 왜 생겼을까를 이해하는 것이 좋다.
KMS의 Key는 export가 

- KMS import
- Multi Region Key

## 섹션 2: CloudHSM

- HSM(Hardware Security Modules) 이라는 별도의 클러스터를 사용한다.

## 섹션 3: 전송 중인 데이터 보호

## 섹션 4: AWS Secrets Manager
