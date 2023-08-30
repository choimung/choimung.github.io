---

title: 자바의정석 Lambda Expression
date: 2023-08-30 11:57:00 +0900
categories: [Java]
tags: [Java]
toc: true
toc_sticky: true
toc_label: 목차
math: true
mermaid: true

---

### 람다식(Lambda Expression)

람다식이란?
*함수*(메서드)를 간단한 식(expression)으로 표현하는 방법

```java
int max(int a, int b){
    return a > b ? a : b;
}
```

위의 소스 코드를 아래의 소스 코드처럼 간단하게 작성한 코드를 말한다.

```java
(a, b) -> a > b ? a : b
```


람다식은 익명함수라고도 불린다
- 반환 타입과 이름이 없다.

함수와 메서드의 차이
- 근본적으로 동일, 함수는 일반적 용어 메서드는 객체지향개념 용어이다.
- 함수는 클래스에 독립적이고, 메서드는 클래스에 종속적이다.
- 자바에서는 메서드가 클래스 밖에 있을 수 없다.


### 람다식 작성하기

1. 메서드의 이름과 반환타입을 제거하고 '->'를 블록{} 앞에 추가한다.

```java
~~~int max~~~(int a, int b) ->{
    retrun a > b ? a : b;
}
```

2. 반환값이 있는 경우, 식이나 값만 적고 return문 생략 가능(끝에 ';' 안붙임)

```java
(int a, int b) -> a > b ? a : b
```

3. 매개변수의 타입이 추론 가능하면 생략가능(대부분 생략가능)

```java
(a, b) -> a > b ? a : b
```


### 람다식 작성하기 - 주의 사항

1. 매개변수가 하나인 경우, 괄호() 생략가능(타입이 없을떄만)

```java
a -> a * a     //OK
int a -> a *a  // ERROR
```

2. 블록 안의 문장이 하나뿐 일 때, 괄호{}생략가능(끝에 ';' 안붙임)

```java
(int i) -> System.out.println(i)
```
단 하나뿐인 문장이 return 문이면 괄호{} 생략불가


### 람다식의 예

```java

//메서드
int max(int a , int b){
    return a > b ? a : b;
}

//람다식
(a, b) -> a > b ? a:b

```

<hr>

```java


//메서드
int printVar(String name, int i){

    System.out.println(name +"=" + i);

}


//람다식
(String name, int i) -> System.out.println(name + "=" + i);

```

<hr>

```java

// 메서드
int square(int x){
    return x * x;
}

//람다식
(int x) -> x*x;

```

<hr>

```java

//메서드
int roll(){
    return (int)(Math.random() * 6);
}

//람다식

() -> (int)(Math.random() * 6);

```

함수(메서드)를 간단히 표현하기 위해 사용.

