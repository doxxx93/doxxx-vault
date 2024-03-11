---
date_created: 2024-03-11 21:44
author: 
date_published: 
url:
---
# Comparator 와 Comparable 을 객체 지향 관점에서 어떤 차이가 있는지

둘다 Collections Framework의 Infrastructure 영역의 Ordering과 관련된 인터페이스이다.

https://www.geeksforgeeks.org/comparable-vs-comparator-in-java/

> [!NOTE]
> Comparable - 이를 구현하는 클래스에 자연스러운 순서를 부여합니다. 자연스러운 순서는 목록을 정렬하거나 정렬된 Set 또는 Map에서 순서를 유지하는 데 사용할 수 있습니다.
> Comparator - Sorted Set 또는 Map에서 순서를 유지하거나 List를 정렬하는데 사용할 수 있는 순서 관계를 나타냅니다. 타입의 자연스러운 순서를 재정의하거나 비교 가능한 인터페이스를 구현하지 않는 유형의 개체를 순서화할 수 있습니다.

## [Interface Comparable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Comparable.html)

이 인터페이스는 이를 구현하는 각 클래스의 객체들에 대해 총체적인 순서를 부여한다. 이 순서를 클래스의 자연스러운 순서라고 하며, 클래스의 자연스러운 비교 방법을 클래스의 자연스러운 순서라고 한다.
이 인터페이스를 구현하는 객체의 리스트(및 배열)은 Collections.sort(및 Arrays.sort)에 의해 자동으로 정렬될 수 있다. 이 인터페이스를 구현하는 객체는 Comparator를 지정할 필요 없이 정렬된 맵의 키 또는 정렬된 집합의 요소로 사용될 수 있다.

## [Interface Comparator](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html)
