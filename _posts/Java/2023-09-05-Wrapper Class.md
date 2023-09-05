---

title: 자바 Wrapper 클래스는 무엇인가?
date: 2023-09-05 13:15:00 +0900
categories: [Java]
tags: [Java]
toc: true
toc_sticky: true
toc_label: 목차
math: true
mermaid: true
---

### 서론

자바의 자료형은 크게 기본타입 (primitive type)과 참조 타입(reference type)으로 나눌 수 있다

기본타입은 byte,short,int... 등이 8개가 있는데
이 기본타입의 데이터를 객체로 표현해야하는 경우가 있다.

**언제 기본타입의 데이터를 객체로 표현해야될까?**

 1. 컬렉션 사용: 자바의 컬렉션 프레임워크(ArrayList, HashMap)은
객체만을 저장할 수 있다. 따라서 기본 데이터 타입의 값을 컬렉션에 저장할려면 Wrapper 클래스를 사용해야한다.

```java
ArrayList<Integer> numbers = new ArrayList<Integer>();
numbers.add(new Integer(42));
```

2. 제네릭 사용 : 제네릭을 활용하여 타입 안정성을 확보하려면   
기본 데이터 타입을 객체로 표현해야 한다. 제네릭을 사용하면 컴파일 시에
타입 검사가 이루어지므로 형변환 오류를 방지할 수 있다.

```java
public class Box<T>{
    private T value;

    public Box(T value){
        this.value = value;
    }

    public T getValue(){
        return value;
    }
}
```

3. Null 값 표현 : 기본 데이터 타입은 null값을 가질 수 없다.   
하지만 Wrapper 클래스는 null을 허용하며 값이 없음을 나태나는데 사용될 수 있다.

```java
Integer int = null;
```

### Wrapper 클래스

기본 데이터 타입(primitive data type)을 객체로 래핑(wrapping)하여 제공하는 클래스

> Wrapper 클래스는 기본 데이터 타입을 참조형 객체로 사용할 수 있도록 도와준다.

|primitive type|wrapper class|
|--------------|-------------|
|byte|Byte|
|short|Short|
|int|Intger|
|long|Long|
|float|Float|
|double|Double|
|char|Character|
|boolean|Boolean|


### 박싱과 언방식

1. 박싱
- 기본 데이터 타입을 해당하는 Wrapper 클래스의 객체로 변환하는 과정을 말한다.

```java
Intger num1 = new Integer(20);

// auto boxing
Integer num1 = 20;
```

2. 언박싱
- 언박싱은 Wrapper 클래스 객체에서 기본 데이터 타입의 값을 추출하는 과정을 의미합니다.

```java
int num2 = num1.intValue();

// auto Unboxing
int num2 = num1;
```

박싱된 값을 참조변수이므로 '=='사용시 인스턴스의 주소를 비교하게 된다.

### 마무리
Wrapper 클래스는 자바에서 기본 타입과 객체지향 프로그래밍을 조홥롭게 사용할 수 있도록 도와주며,    다양한 자바 라이브러리와 기능에 서 활용된다.