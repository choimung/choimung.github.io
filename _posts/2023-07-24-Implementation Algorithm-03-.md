---
title: 구현 알고리즘 문제 (왕실의 나이트)
date: 2023-07-24 22:31:00 +0900
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

### 문제의 목표 설명

- 문제 설명 : 주어진 위치에서 나이트가 이동할 수 있는 모든 위치의 개수를 세는 것입니다.

- 제약 조건 : 
체스판은 8*8로 이루어져있다.

1. 수평으로 두 칸 이동한 뒤에 수직으로 한 칸 이동하기
2. 수직으로 두 칸 이동한 뒤에 수평으로 한 칸 이동하기


<br>

## 문제 이해와 분석
사용자로부터 입력으로 하나의 문자열을 받습니다. 이 문자열은 나이트의 현재 위치를 나타냅니다. 예를 들어, "A1"이라면 체스판의 왼쪽 아래 모서리인 (1, 1) 위치를 의미합니다.

입력된 문자열로부터 현재 위치의 행(row)과 열(column)을 추출합니다.

나이트의 이동 방향을 나타내는 step 배열을 생성합니다. step 배열은 나이트가 이동할 수 있는 8가지 방향의 상대적인 행과 열의 변화를 저장하고 있습니다. 예를 들어, {-2, -1}은 현재 위치로부터 위쪽으로 2칸 이동하고 왼쪽으로 1칸 이동하는 방향을 의미합니다.

step 배열을 사용하여 현재 위치에서 나이트가 이동할 수 있는 모든 위치를 계산합니다. 이동이 가능한 경우 해당 위치의 행과 열 값이 체스판 내부에 있는지 확인하고, 내부에 있을 경우 result 변수를 증가시킵니다.

모든 가능한 이동 방향을 확인한 뒤, result 변수에 저장된 값을 출력합니다. 이 값은 현재 위치에서 나이트가 이동할 수 있는 모든 위치의 개수를 의미합니다.

<br>

## 알고리즘 설계

<br>
## 알고리즘 구현

>제가 작성한 코드는 아래와 같습니다.

```java

import java.util.Scanner;

public class test {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String str = scanner.nextLine();

        int row = str.charAt(1) - '0';
        int column = (str.charAt(0) - '0') - 48;
        int result = 0;

        int[][] step = new int[][]{
                {-2, -1},
                {-1, -2},
                {1, -2},
                {2, -1},
                {2, 1},
                {1, 2},
                {-1, 2},
                {-2, 1}
        };

        for(int i = 0; i < step.length; i++){
            int nextRow = row + step[i][0];
            int nextColumn = column + step[i][1];

            if(!(nextRow < 1 || nextColumn < 1 || nextRow > 8 || nextColumn > 8)){
                result++;
            }
        }
        System.out.println("result = " + result);
    }
}





```
<br>

## 최적화와 시간복잡도

### 시간 복잡도

step 배열은 나이트가 이동할 수 있는 방향을 나타내는 8개의 요소를 가지고 있으므로, step 배열의 길이는 항상 상수로 고정되어 있습니다 (8입니다). 따라서 반복문의 횟수는 항상 상수이며, 입력의 크기와 무관합니다.

따라서, 반복문을 통해 모든 가능한 이동 방향을 확인하는 데 걸리는 시간은 상수입니다. 따라서 시간 복잡도는 O(N)이 아니라 O(1)입니다. 상수 시간 복잡도는 입력의 크기와 무관하며 항상 일정한 실행 시간을 가집니다.

<br>

## 마무리