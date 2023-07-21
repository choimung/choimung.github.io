---
title: 그리디 알고리즘 문제(1이 될 때 까지)
date: 2023-07-20 19:48:00 +0900
categories: [Algorithm, Greedy]
tags: [github blog,algorithm,greedy]
toc: true
toc_sticky: true
toc_label: 목차
math: true
mermaid: true
---

## 서론

### 그리디 알고리즘 개요
그리디 알고리즘(또는 탐욕 알고리즘)은 각 단계에서 가장 최적인 선택을 하는 알고리즘 설계기법입니다.
그리디 알고리즘은 해당 단계에서 가장 좋은 선택을 하여 전체적인 결과를 얻으려는 접근 방식을 가지고 있습니다.

### 문제의 목표 설명

- 문제 설명 : 일련의 방법을 통해 어떠한 수 N을 1이 될 때까지의 수행해야 하는 횟수의 최소값을 출력합니다.


- 제약 조건 : 
다음의 두 과정 중 하나를 반복적으로 선택하여 수행한다.
단 두 번째 연산은 N이 K로 나누어떨어질 때만 할 수 있다.

    1. N에서 1을 뺀다.

    2. N을 K로 나눈다.


<br>

## 문제 이해와 분석
예를 들어 N이 17, K가 4라고 가정합니다.
이때 1번의 과정을 한 번 수행하면 N은 16이 됩니다. 이후에 2번의 과정을 두 번 수행하면 N은 1이 됩니다. 
결과적으로 이 경우 전체 과정을 실행한 횟수는 3이 됩니다.
<br>

## 알고리즘 설계

### 접근방식
저는 아래와 같이 문제에 접근하였습니다.
1. 변수 'count'를 생성하고 0으로 초기화 합니다. 이변수는 연산의 횟수를 저장합니다.
2. N이 1이 될 때 까지 다음과 같은 루프를 반복합니다.
    2-1 N이 K로 나누어 떨어지면 N을 K로 나눕니다 (N = N / K)
    2-2 그렇지 않으면 N에서 1을 뺍니다. (N = N -1)
3. 반복마다 count를 1만큼 증가시킵니다.
4. N이 1이 되면 루프를 탈출하고 count를 출력합니다.

<br>
## 알고리즘 구현

>제가 작성한 코드는 아래와 같습니다.

```java

import java.util.Scanner;

public class test {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int N = scanner.nextInt();
        int K = scanner.nextInt();
        int count = 0;

        while (N != 1) {
            if (N % K == 0) {
                N = N / K;
            } else {
                N = N - 1;
            }
            count++;
        }
        System.out.println("count = " + count);
    }
}



```
<br>

## 최적화와 시간복잡도

### 최적화

### 시간 복잡도

<br>

## 마무리