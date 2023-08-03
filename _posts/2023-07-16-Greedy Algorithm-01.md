---
title: 그리디 알고리즘 문제(거스름돈 문제)
date: 2023-07-16 21:31:30 +0900
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
- 문제 설명 : 손님에게 거슬러줘야 할 돈이 N원일 때, 거슬러 줘야 할 동전의 최소 개수를 구하는 문제입니다. 거스름돈으로 사용할 수 있는 동전의 종류는 500원, 100원, 50원, 10원이며, 해당 동전들은 무한히 존재한다고 가정합니다.

- 제약 조건 : 거스름돈으로 사용할 동전의 종류는 500원, 100원, 50원, 10원이고 N은 항상 10의 배수입니다.

<br>

## 문제 이해와 분석
거스름돈으로 사용할 수 있는 동전의 종류는 500원, 100원, 50원, 10원이며 해당 동전은 무한히 존재한다고 가정합니다. 손님에게 거슬러줘야 할 돈이 N원일때 거슬러 줘야 할 동전의 최소 개수를 구하는 문제입니다.
N은 항상 10의 배수이며 거스름돈으로 사용할 수 있는 동전은 가장 큰 동전부터 사용하여 최소 개수의 동전을 구해야 합니다.

<br>

## 알고리즘 설계

### 접근방식
1. 거스름돈으로 사용할 수 있는 가장 큰 동전부터 시작합니다. 이 문제에서는 500원을 사용
2. 사용할 수 있는 가장 큰 동전의 개수를 최대한 사용하여 거스름돈을 만들어 줍니다. 1260원 중에서 최대한 많은 500원 짜리 동전을 사용하면 500원 2개를 사용할 수 있습니다.
3. 남은 거스름돈이 있을 경우, 다음으로 작은 동전을 최대한 사용하여 거스름돈을 만들어줍니다. 260원이 남았으므로 100원짜리 2개를 사용합니다.
4. 거스름돈이 0이 될 때까지 2번과 3번의 과정을 반복합니다.

위 의 접근 방식을 그리디 알고리즘으로 코드로 구현하면, 거슬러 줘야 할 동전의 최소 개수를 구할 수 있습니다.

<br>
## 알고리즘 구현

>제가 작성한 코드는 아래와 같습니다.

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int N = scanner.nextInt();
        int[] coinType = {500,100,50,10};
        int count = 0;

        for (int coin : coinType) {
            count = count + N / coin;
            N = N % coin;
        }

        System.out.println("count = " + count);
        
    }
}
```
<br>

## 최적화와 시간복잡도

### 최적화
코드의 효율성과 성능을 개선하기 위해 몇 가지 고려 사항을 살펴볼 수 있습니다.
예를들어, 사용 가능한 동전의 종류가 변경된다면 코드를 수정해야 할 수 도 있습니다. 또한 거스름돈으로 사용할 수 있는 동전의 종류가 더 다양해진다면 코드를 확장해야 할 수도 있습니다.

### 시간 복잡도
위 코드의 시간복잡도는 거스름돈으로 사용할 수 있는 동전의 종류의 개수에 따라 결정됩니다.
동전의 종류의 개수를 K라고 표기할때 위 소스코드의 시간복잡도는 O(K)가 됩니다.
왜냐하면 for 루프는 동전의 종류 수에 비례하여 실행되고, 각 반복에서 거스름돈을 계산하고 변수를 갱신하기 때문입니다.


<br>

## 마무리