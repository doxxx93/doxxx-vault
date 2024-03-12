---
date_created: 2024-03-11 21:44
author:
date_published:
url:
---
# Comparator 와 Comparable 을 객체 지향 관점에서 어떤 차이가 있는지

지인이 최근 면접에서 받은 질문이 재밌어보여 정리해보았습니다.

## 개요

둘다 Collections Framework의 Infrastructure 영역의 Ordering과 관련된 인터페이스입니다.
[참고 자료: Outline of the Collections Framework](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/doc-files/coll-reference.html)

둘다 정렬을 위해 사용하지만 서로 어떤 차이가 있는지 알아보겠습니다.

> [!NOTE]
>
> |            Comparable            |      Comparator       |
> |:--------------------------------:|:---------------------:|
> |             인퍼테이스이다.             |       인터페이스이다.        |
> |      compareTo() 메서드를 제공한다.      | compare() 메서드를 제공한다.  |
> |         java.lang 패키지이다.         |   java.util 패키지이다.    |
> | natural or default 정렬에 사용할 수 있다. | custom 정렬에 사용할 수 있다.. |
> |         단일 항목 정렬을 제공한다.          |  여러 항목에 대한 정렬을 제공한다.  |
> | 구현 클래스를 modify 한다.(overide로 인한)  |    modify 하지 않는다.     |

## Comparable

`Comparable`은 `객체를 동일한 타입의 객체와 비교`할 수 있게 해줍니다.
`Integer`, `Double`, `String`과 같은 내장 클래스들은 `Comparable`을 구현하고 있습니다.

위의 표에서도 확인할 수 있듯이 natural order와 default order를 통해 정렬할 수 있는데, 이는 해당 객체 자체가 어떻게 정렬이 되어야 하는지에 대한 정보를 가지고 있음을 의미합니다.

### 사용법

`Comparable` 인터페이스를 구현하는 클래스는 `compareTo()` 메서드를 오버라이드하여 자체 정렬 방법을 제공합니다.

동일한 타입인 `T`와 비교하는 `compareTo()` 메서드를 구현하는 것을 확인할 수 있습니다.

```Java
// Comparable 인터페이스를 구현하는 클래스
class T implements Comparable<T> {
    @Override
    public int compareTo(T t) {
        // comparasion logic
    }
}
```

`x.compareTo(y)`와 같이 메서드를 호출하면 `x`와 `y`를 비교하여 결과를 반환합니다.

### 예시

`Integer`의 예시를 들어보겠습니다.

```java
public final class Integer extends Number
        implements Comparable<Integer>, Constable, ConstantDesc {
        
    public int compareTo(Integer anotherInteger) {
        return compare(this.value, anotherInteger.value);
    }

    public static int compare(int x, int y) {
        return (x < y) ? -1 : ((x == y) ? 0 : 1);
    }        
}
```

위에서 다루었던 natural/default order가 숫자이므로 대소 비교(numerically less/greater)를 통해서 정렬하는 것을 확인할 수 있습니다.

`String`의 예시는 `Comparator`의 내용에서 다루겠습니다.

## Comparator

`Comparator`도 객체를 정렬할 수 있게 해주는 인터페이스입니다.

> [!NOTE]
> `Comparator`는 함수형 인터페이스로 정의됩니다.
> 함수형 인터페이스는 단 하나의 추상 메서드(Single Abstract Method, SAM)를 가지고 있는 인터페이스입니다.

`Comparable` 인터페이스를 구현하는 경우, 해당 클래스는 `compareTo()` 메서드를 오버라이드하여 자체(natural/default) 정렬 방법을 갖게됩니다.

즉 자체 정렬 방법을 알 수 없는(unaware) 클래스에 대해서 `Comparator` 인터페이스를 구현하여 `compare()` 메서드를 오버라이드함으로써 custom 정렬 방법을 제공할 수 있습니다.

`Comparator`는 객체의 여러 항목(data member)에 대한 정렬을 제공할 수 있습니다.

### 사용법

`Comparator<T> comparator = (T t1, T t2) -> { /* 비교 로직 */ }`
과 같이 람다식을 통해 동일한 T 타입 객체 두개를 비교하고 int 값을 반환하도록 구현합니다.

### 예시

`String`의 예시를 들어보겠습니다.

```java
public final class String implements java.io.Serializable, Comparable<String>, CharSequence,
        Constable, ConstantDesc {

    public int compareTo(String anotherString) {
        byte[] v1 = value;
        byte[] v2 = anotherString.value;
        byte coder = coder();
        if (coder == anotherString.coder()) {
            return coder == LATIN1 ? StringLatin1.compareTo(v1, v2)
                    : StringUTF16.compareTo(v1, v2);
        }
        return coder == LATIN1 ? StringLatin1.compareToUTF16(v1, v2)
                : StringUTF16.compareToLatin1(v1, v2);
    }

    public static final Comparator<String> CASE_INSENSITIVE_ORDER
            = new CaseInsensitiveComparator();

    private static class CaseInsensitiveComparator
            implements Comparator<String>, java.io.Serializable {
        
        @Serial
        private static final long serialVersionUID = 8575799808933029326L;

        public int compare(String s1, String s2) {
            byte[] v1 = s1.value;
            byte[] v2 = s2.value;
            byte coder = s1.coder();
            if (coder == s2.coder()) {
                return coder == LATIN1 ? StringLatin1.compareToCI(v1, v2)
                        : StringUTF16.compareToCI(v1, v2);
            }
            return coder == LATIN1 ? StringLatin1.compareToCI_UTF16(v1, v2)
                    : StringUTF16.compareToCI_Latin1(v1, v2);
        }

        @Serial
        private Object readResolve() {
            return CASE_INSENSITIVE_ORDER;
        }
    }
}
```

`Comparable` 인터페이스를 구현하는 `String` 클래스는 자체 정렬 방법인 사전식 순서를 제공합니다.

동시에 `CASE_INSENSITIVE_ORDER`라는 `Comparator`를 제공하여 대소문자를 무시하고 비교하는 정렬 방법을 제공합니다.

### `Comparator`의 메서드

|       메서드       |                      설명                      |                                    사용법                                     |
|:---------------:|:--------------------------------------------:|:--------------------------------------------------------------------------:|
|    compare()    |   두 개체를 비교하고 해당 개체의 순서를 나타내는 정수 값을 반환합니다.	   |                          int compare(T o1, T o2);                          |
|    equals()     |   두 `Comparator`의 정렬 방식이 동일한지 여부를 확인합니다.	    |                      comparator1.equals(comparator2);                      |
|   comparing()   | `keyExtractor` 함수를 기반으로 `Comparator`를 만듭니다.	 |                Comparator comparing(Function keyExtractor);                |
| thenComparing() |            `Comparator`를 체이닝합니다.             | Comparator thenComparing(Function keyExtractor, Comparator keyComparator); |

## 그래서?

`Comparable`과 `Comparator`의 차이를 알아보았습니다만, 이 둘의 객체 지향 관점에서의 차이는 무엇일까요?

`Comparable`은 객체의 내부적인 비교 방법을 정의하는데 초점을 맞춥니다.

객체의 비교 방법을 그 객체의 내부에 캡슐화하는데, 이는 SOLID 원칙 중 하나인 단일 책임 원칙(SRP)을 반영합니다.

객체는 자신의 데이터와 그 데이터를 어떻게 비교할지에 대한 로직을 스스로 관리함으로써, 비교 메커니즘을 객체의 일부로 만듭니다.

반면, `Comparator`는 객체의 외부적인 비교 방법을 정의하는데 초점을 맞춥니다.

비교 로직을 객체 외부에 정의할 수 있도록 함으로써, 개방/폐쇄 원칙(OCP)과 의존성 역전 원칙(DIP)을 적용합니다.

다형성과 전략 패턴을 활용하여 객체의 비교 방법을 외부에서 정의할 수 있게 하여 기존 코드를 변경하지 않고도 비교 방식을 쉽게 확장하거나 변경할 수 있게 합니다.

이는 유연성과 재사용성을 증가시키며, 정렬 방식을 동적으로 변경할 수 있는 능력을 제공합니다.

## 결론

기존에는 인지하지 못했던 `Comparable`과 `Comparator`의 차이를 객체 지향 관점에서 살펴보았습니다.

상황에 따라 `Comparable`과 `Comparator`를 적절히 사용하여 객체의 정렬 방법을 정의하여 사용하면 좋을 것 같습니다.

## REF

https://www.scaler.com/topics/java/comparable-and-comparator-in-java/
https://www.geeksforgeeks.org/comparable-vs-comparator-in-java/
