---
title: BeanFactory와 ApplicationContext
date: 2023-12-21 14:42:01 +0900
categories: [Spring]
tags: [Java,Spring]
toc: true
toc_sticky: true
toc_label: 목차
math: true
mermaid: true
---

## 스프링 컨테이너 상속 관계도

<p align="center">
  <img src="../../../../assets/img/2023-12-21-15-15-44.png">
</p>

- `BeanFactory` : 스프링의 가장 기본적인 컨테이너로, 빈을 등록하고 관리하는 역할을 한다.

- `ApplicationContext`: BeanFactory를 상속받아 더 많은 기능을 제공하는 인터페이스 이다.

- `WebApplicationContext` : 웹 애플리케이션 개발을 위한 컨테이너로 ApplicationContext를 상속받아 웹 환경에서의 특화된 기능을 제공한다.

- `AnnotationConfigApplicationContext`: JavaConfig를 이용한 설정 클래스를 이용하여 빈을 등록하는 데 특화된 컨테이너이다. `@Configuration` 어노테이션을 사용한 설정 클래스를 이용하여 빈을 등록할 수 있다.

## BeanFactory ?
`BeanFactory`는 빈(Bean)을 생성하고 관리하는 최상위 인터페이스로 스프링 애플리케이션의 핵심을 담당한다.

### 주요 역할

- 빈 생성과 관리 : `BeanFactory`는 스프링 애플리케이션에서 사용되는 빈을 생성하고 관리한다.
  
- IoC : IoC는 스프링의 중요한 디자인 패턴 중 하나로 객체의 생성과 관리를 컨테이너가 담당하도록 한다.
  
- 의존성 주입 : `BeanFactory`는 빈 간의 의존성을 주입하는데 핵심적인 역할을 한다.

- 대부분의 기능은 BeanFactory 가 제공하는 메서드를 사용한다.

그렇다면 BeanFactory를 사용하지 왜 자식 객체인 ApplicationContext를 사용할까?

## ApplicationContext ? 
`ApplicationContext` 는 여러개의 인터페이스를 상속받아 여러가지 기능을 지원한다.
![](../../../../assets/img/2023-12-22-13-17-14.png)


