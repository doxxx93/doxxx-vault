---
date_created: 2024-03-29 21:00
author:
date_published:
url: https://www.baeldung.com/java-validation
tags:
  - java
  - bean
  - validation
---

# Java Bean Validation

표준 JSR-380 프레임워크를 기반으로 Jakarta Bean Validation 3.0 사양
Java EE 7에 도입된 Bean 유효성 검사 API의 기능을 기반으로 하는 을 사용하여 Java 빈을 유효성 검사하는 기본 사항

사용자 입력의 유효성을 검사하는 것은 대부분의 애플리케이션에서 매우 일반적인 요구 사항이며, Java Bean Validation 프레임워크는 이러한 종류의 로직을 처리하기 위한 사실상의 표준입니다.

## Using Validation Annotations

- `@AssertFalse`: 검증 대상 값이 false여야 함을 나타냅니다.
- `@AssertTrue`: 검증 대상 값이 true여야 함을 나타냅니다.
- `@DecimalMax`: 검증 대상 숫자가 지정된 값 이하여야 함을 나타냅니다.
- `@DecimalMin`: 검증 대상 숫자가 지정된 값 이상이어야 함을 나타냅니다.
- `@Digits`: 검증 대상 숫자가 지정된 자릿수 이하이어야 함을 나타냅니다.
- `@Email`: 검증 대상 문자열이 이메일 형식에 맞아야 함을 나타냅니다.
- `@Future`: 검증 대상 날짜가 미래여야 함을 나타냅니다.
- `@FutureOrPresent`: 검증 대상 날짜가 현재 또는 미래여야 함을 나타냅니다.
- `@Max`: 검증 대상 숫자가 지정된 값 이하여야 함을 나타냅니다.
- `@Min`: 검증 대상 숫자가 지정된 값 이상이어야 함을 나타냅니다.
- `@Negative`: 검증 대상 숫자가 음수여야 함을 나타냅니다.
- `@NegativeOrZero`: 검증 대상 숫자가 0 또는 음수여야 함을 나타냅니다.
- `@NotBlank`: 검증 대상 문자열이 비어 있지 않아야 함을 나타냅니다.
- `@NotEmpty`: 검증 대상 컬렉션이나 배열이 비어 있지 않아야 함을 나타냅니다.
- `@NotNull`: 검증 대상 값이 null이 아니어야 함을 나타냅니다.
- `@Null`: 검증 대상 값이 null이어야 함을 나타냅니다.
- `@Past`: 검증 대상 날짜가 과거여야 함을 나타냅니다.
- `@PastOrPresent`: 검증 대상 날짜가 현재 또는 과거여야 함을 나타냅니다.
- `@Pattern`: 검증 대상 문자열이 지정된 정규 표현식과 일치해야 함을 나타냅니다.
- `@Positive`: 검증 대상 숫자가 양수여야 함을 나타냅니다.
- `@PositiveOrZero`: 검증 대상 숫자가 0 또는 양수여야 함을 나타냅니다.
- `@Size`: 검증 대상 문자열, 컬렉션, 배열의 크기가 지정된 범위 내에 있어야 함을 나타냅니다.

