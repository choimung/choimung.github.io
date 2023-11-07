---
title: JAVA JUnit5 메서드
date: 2023-11-02 14:35:00 +0900
categories: [Java]
tags: [Java]
toc: true
toc_sticky: true
toc_label: 목차
math: true
mermaid: true
---
자바 테스트 코드작성을 위해 사용되는 Junit5 메소드를 정리해보았습니다.

## Assertion Methods
`org.junit.jupiter.api.Assersions` 기본적인 단언문을 제공하며,   
테스트를 작성하는 데 필요한 기본 기능을 제공한다.
JUnit Jupiter Assersion 메서드는 모두 `static` 메서드라는 특징을 가진다.


### assertThat(actual, matcher)
예상한 결과와 실제 결과를 비교하고 두 값이 같은지 여부를 판단한다.
**값이 다를 경우 테스트 실패로 표시된다.**



### assertEquals(expected, actual)
예상한 값(`expected`)과 실제 값(`actual`)이 동일한지 비교한다.   
**값이 다를 경우 테스트 실패로 표시된다.**
```java
    @Test
    void assertEquals_테스트() {
        int num = 5;
        Assertions.assertEquals(5, num);
    }
```

<hr>

### assertNotEquals(unexpected, actual)
예상하지 않은 값(`unexpected`)과 실제 값(`actual`)이 다른지 비교한다.   
**값이 같은 경우 테스트 실패로 표시된다.**
```java
    @Test
    void assertNotEquals_테스트(){
        int num = 5;
        Assertions.assertNotEquals(0, num);
    }
```

<hr>

### assertTrue(condition)
주어진 조건(`condition`)이 `true` 인지 확인한다.  
**조건이 `false`일 경우 테스트 실패로 표시된다.**
```java
    @Test
    void assertTrue_테스트(){
        Assertions.assertTrue(100 > 0);
    }
```

<hr>

### assertFalse(condition)
주어진 조건(`condition`)이 `false` 인지 확인한다.
**주어진 조건이 `true`일 경우 테스트 실패로 표시된다.**
```java
    @Test
    void assertFalse_테스트(){
        Assertions.assertFalse(100 < 0);
    }
```

<hr>

### assertNull(object)
주어진 객체(`object`)가 `null`인지 확인한다.
**객체가 `null`이 아니라면 테스트 실패로 표시된다.**
```java
    @Test
    void assertNull_테스트(){
        String string = null;
        Assertions.assertNull(string);
    }
```

<hr>

### assertNotNull(expected, actual)
주어진 객체(`object`) 가 `null`이 아닌지 확인한다.
**객체가 `null`이면 테스트 실패로 표시된다.**
```java
    @Test
    void assertNotNull_테스트(){
        String string = "str";
        Assertions.assertNotNull(string);
    }
```

<hr>

### assertSame(expected, actual)
두 객체가 동일한 참조를 가리키는지 확인한다.
**두 객체가 참조하는 값이 다르면 테스트는 실패한다.**
```java
    @Test
    void assertSame_테스트(){
        String string1 = "test";
        String string2 = "test";
        
        Assertions.assertSame(string1,string2);
    }
```

<hr>

### assertNotSame(expected, actual)
두 객체가 서로 다른 참조를 가르키는지 확인한다.
**두 객체가 동일한 참조를 가리키면 테스트는 실패한다**
```java
    @Test
    void assertNotSame_테스트(){
        String string1 = "test";
        String string2 = "test1";

        Assertions.assertNotSame(string1,string2);
    }
```

<hr>

### assertArrayEquals(expected, actual)
예상한 배열과 실제 배열이 동일한 요소를 갖고 있는지 확인한다.
**배열의 내용이 다르면 테스트는 실패한다**
```java
    @Test
    void assertArrayEquals_테스트(){
        int[] arr1 = {1,2,3,4,5};
        int[] arr2 = {1,2,3,4,5};
        
        Assertions.assertArrayEquals(arr1,arr2);

    }
```

<hr>

### assertThrows(exceptionClass, executable)
주어진 executable(실행 가능한 블록)에서 예외가 발생하는지 확인
**예외가 발생하지 않거나 발생한 예외가 기대한 예외와 일치하지 않으면 테스트는 실패한다**
```java
    @Test
    void assertThrows_테스트(){
        Assertions.assertThrows(NumberFormatException.class, () -> Integer.parseInt("abc"));
    }
```

<hr>

## AssertJ란?
AssertJ는 JUnit과 함께 사용되는 자바 테스트 라이브러리 중 하나로 가독성이 높은 메서드제공한다.   

**`assertThat`** 메서드를 사용하여 검증을 시작하고, 이어서 다양한 AssertJ의 검증 메서드를 체이닝하여 사용하여 테스트 코드를 작성한다. 코드를 읽기 쉽고 직관적으로 만들어주며 다양한 검증조건을 지정하기 유용하다.

1. **`assertThat(actual).isXXX()`**:
    - **`isTrue()`**: 주어진 조건이 **`true`**인지 확인합니다.
    - **`isFalse()`**: 주어진 조건이 **`false`**인지 확인합니다.
    - **`isNull()`**: 주어진 값이 **`null`**인지 확인합니다.
    - **`isNotNull()`**: 주어진 값이 **`null`**이 아닌지 확인합니다.
2. **`assertThat(actual).isEqualTo(expected)`**:
    - **`isEqualTo()`**: 주어진 값이 기대한 값과 동일한지 확인합니다.
    - **`isNotEqualTo()`**: 주어진 값이 기대한 값과 다른지 확인합니다.
3. **`assertThat(actual).isSameAs(expected)`**:
    - **`isSameAs()`**: 주어진 객체가 기대한 객체와 동일한 참조인지 확인합니다.
    - **`isNotSameAs()`**: 주어진 객체가 기대한 객체와 다른 참조인지 확인합니다.
4. **`assertThat(actual).isInstanceOf(Class)`**:
    - **`isInstanceOf(Class)`**: 주어진 객체가 특정 클래스의 인스턴스인지 확인합니다.
    - **`isNotInstanceOf(Class)`**: 주어진 객체가 특정 클래스의 인스턴스가 아닌지 확인합니다.
5. **`assertThat(actual).isIn(Iterable)`**:
    - **`isIn(Iterable)`**: 주어진 값이 주어진 컬렉션 또는 이터러블에 포함되어 있는지 확인합니다.
    - **`isNotIn(Iterable)`**: 주어진 값이 주어진 컬렉션 또는 이터러블에 포함되어 있지 않은지 확인합니다.
6. **`assertThat(actual).hasSize(int)`**:
    - **`hasSize(int)`**: 주어진 컬렉션이 특정 크기인지 확인합니다.
    - **`hasSameSizeAs(Iterable)`**: 주어진 컬렉션이 다른 컬렉션과 크기가 동일한지 확인합니다.
7. **`assertThat(actual).contains(...)`**:
    - **`contains(...)`**: 주어진 컬렉션이 특정 요소들을 포함하는지 확인합니다.
    - **`doesNotContain(...)`**: 주어진 컬렉션이 특정 요소들을 포함하지 않는지 확인합니다.
8. **`assertThat(actual).isGreaterThan()`**:
    - **`isGreaterThan()`**: 주어진 값이 특정 값보다 큰지 확인합니다.
    - **`isGreaterThanOrEqualTo()`**: 주어진 값이 특정 값보다 크거나 같은지 확인합니다.
    - **`isLessThan()`**: 주어진 값이 특정 값보다 작은지 확인합니다.
    - **`isLessThanOrEqualTo()`**: 주어진 값이 특정 값보다 작거나 같은지 확인합니다.
9. **`assertThat(actual).isBetween(min, max)`**:
    - **`isBetween(min, max)`**: 주어진 값이 최소값과 최대값 사이에 있는지 확인합니다.
    - **`isStrictlyBetween(min, max)`**: 주어진 값이 최소값과 최대값을 제외한 범위에 있는지 확인합니다.
10. **`assertThat(actual).hasFieldOrProperty(String)`**:
    - **`hasFieldOrProperty(String)`**: 주어진 객체가 특정 필드 또는 프로퍼티를 가지고 있는지 확인합니다.
11. **`assertThat(actual).containsOnlyElementsOf(Collection)`**:
    - **`containsOnlyElementsOf(Collection)`**: 주어진 컬렉션에 있는 요소들이 주어진 컬렉션의 요소 중 일부인지 확인합니다.
12. **`assertThat(actual).usingComparator(Comparator).isEqualTo(expected)`**:
    - **`usingComparator(Comparator).isEqualTo(expected)`**: 주어진 객체들을 비교할 때 사용할 커스텀 컴퍼레이터(비교자)를 지정하여 동일성을 확인합니다.