---
title: 구현 알고리즘 문제(상하좌우)
date: 2023-07-24 13:11:00 +0900
categories: [Algorithm, Implementation]
tags: [github blog,algorithm,implementation]
toc: true
toc_sticky: true
toc_label: 목차
math: true
mermaid: true
---

## 서론

### 구현 알고리즘 개요
구현 알고리즘이란, 컴퓨터 프로그램을 통해 주어진 문제를 해결하기 위해 직접 코드로 구현하는 알고리즘입니다.
즉, 알고리즘의 논리적인 절차를 실제 프로그래밍 언어로 표현하여 문제를 해결하는 과정을 말합니다.
구현 알고리즘은 프로그래밍 기초를 이해하고 문제 해결 능력을 향상시키는데 중요한 역할을 합니다.

### 구현 알고리즘의 단계

구현 알고리즘은 주로 다음과 같은 단계로 진행됩니다.

1. 문제 이해 : 해결하고자 하는 문제를 정확히 이해합니다. 문제의 입력과 출력, 조건 등을 분석하여 해결 방법을 구상합니다.
2. 알고리즘 설계 : 문제를 해결하기 위한 논리적인 절차를 설계합니다. 이 단계에서는 어떤 자료 구조나 반복문, 조건문 등을 사용할지 결정하고,
문제를 어떤 방식으로 접근할지 계획합니다.
3. 설계한 알고리즘을 실제 프로그래밍 언어로 코드화합니다. 이때 선택한 프로그래밍 언어에 따라 문법과 제약사항을 준수해야 합니다.
4. 테스트와 디버깅: 구현한 알고리즘을 테스트하여 정확성과 성능을 확인합니다. 문제가 발생할 경우 디버깅을 통해 수정합니다.

### 문제의 목표 설명

- 문제 설명 : 주어진 크기의 2차원 공간에서 주어진 이동 방향에 따라 움직이면서 최종적으로 도착한 위치를 구하는 문제입니다.

- 주어진 크기의 2차원 공간(보통 N x N 크기의 정사각형)에서 출발 지점에서 시작하여 이동 계획에 따라 상, 하, 좌, 우로 움직입니다. 
이동 계획은 문자열로 주어지며, 각 문자는 특정 방향을 나타냅니다. 예를 들어, 'U'는 위로 한 칸 이동, 'D'는 아래로 한 칸 이동, 'L'은 왼쪽으로 한 칸 이동, 'R'은 오른쪽으로 한 칸 이동을 나타냅니다.


- 제약 조건 : 2차원 배열은 N * N의 크기의 정사각형 공간이 주어지며 정사각형 공간을 벗어나는 움직임은 무시됩니다.
예를 들어 (1,1)의 위치에서 L 또는 U를 만나면 무시됩니다.


<br>

## 문제 이해와 분석
N = 5 이고 
R R R U D D의 이동계획 문자열이 주어지면 x = 3, y = 4 라는 결과가 출력된다.
<br>

## 알고리즘 설계

### 접근방식
저는 아래와 같이 문제에 접근하였습니다.
1. 문자열을 입력받고 문자열을 공백 단위로 String타입 배열에 저장하였습니다.
2. 반복문을 이용하여 배열에 저장된 문자열을 비교하여 여행 계획서의 내용과 비교하여 행,열 증감하였습니다.
3. 조건문을 이용하여 정사각형 공간을 벗어나는 움직임은 무시하였습니다.
4. 결과값 출력

<br>
## 알고리즘 구현

>제가 작성한 코드는 아래와 같습니다.

```java

import java.util.Scanner;

public class test {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int N = scanner.nextInt();

        String str = scanner.nextLine();
        String[] s = str.split(" ");

        int row = 1;
        int column = 1;

        for (String s1 : s) {
            if(s1.equals("R")){
                if(column < N){
                    column ++;
                }
            } else if (s1.equals("L")) {
                if(1 < column){
                    column --;
                }
            } else if (s1.equals("U")) {
                if(1 < row){
                    row--;
                }
            } else if (s1.equals("D")) {
                if(row < N){
                    row++;
                }
            }

        }
        System.out.printf("row = %d column = %d",row, column);
    }
}




```
<br>

## 최적화와 시간복잡도

### 최적화
```java
import java.util.Arrays;
import java.util.Scanner;

public class test {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int N = scanner.nextInt();
        int x = 1, y = 1;
        int nx = 0, ny = 0;
        scanner.nextLine();

        String[] plans = scanner.nextLine().split(" ");
        System.out.println("plans = " + Arrays.toString(plans));

        int[] dx = {0, 0, -1, 1};
        int[] dy = {-1, 1, 0, 0};
        String[] move_types = {"L", "R", "U", "D"};

        for (String plan : plans) {
            for(int i = 0; i < move_types.length; i++){
                if(plan.equals(move_types[i])){
                    nx = x + dx[i];
                    ny = y + dy[i];
                }

                if(nx < 1 || ny < 1 || nx > N || ny > N){
                    continue;
                }

                x = nx;
                y = ny;
            }
        }
        System.out.println("x = " + x);
        System.out.println("y = " + y);
    }
}

```


### 시간 복잡도
주어진 코드의 시간 복잡도는 O(K)입니다.

여기서 K는 주어진 이동 계획서의 길이입니다. 입력된 이동 계획서에 따라 for문이 K번 반복되고, 각 반복마다 상수 시간의 연산만 수행되므로 전체 시간 복잡도는 O(K)가 됩니다. 따라서 입력된 이동 계획서의 길이에 비례하는 시간이 소요됩니다.

<br>

## 마무리