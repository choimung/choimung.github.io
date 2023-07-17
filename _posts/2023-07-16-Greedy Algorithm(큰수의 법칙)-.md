---
title: 그리디 알고리즘 문제(큰 수 의 법칙)
date: 2023-07-17 22:16:00 +0900
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
- 문제 설명 : 큰 수의 법칙은 다양한 수로 이루어진 배열이 있을 때 주어진 수들을 M번 더하여 가장 큰 수를 만드는 법칙이다.
배열의 크기 N, 숫자가 더해지는 횟수 M, 그리고 K가 주어질 때 큰 수의 법칙에 따른 결과를 출력해보는 문제입니다.


- 제약 조건 : 배열의 특정한 인덱스(번호)에 해당하는 수가 연속해서 K번을 초과하여 더해질 수 없다.

<br>

## 문제 이해와 분석
예를 들어 순서대로 2,4,5,4,6으로 이루어진 배열이 있을때 M이 8이고 K가 3이라고 가정합니다.   
이 경우 특정한 인덱스의 수가 연속해서 세 번까지만 더해질 수 있으므로 큰 수의 법칙에 따른 결과는   
6 + 6 + 6 + 5 + 6 + 6 + 6 + 5인 46이 된다.

<br>

## 알고리즘 설계

### 접근방식
저는 아래와 같이 문제에 접근하였습니다.
1. 주어진 수열을 오름차순으로 정렬합니다.
2. 정렬된 수열에서 첫 번째로 큰 수와 두 번째로 큰 수를 저장합니다.
2. 큰 수를 K번 더하고 두 번째로 큰 수를 1번 더해줍니다.
3. 두 번째로 큰 수를 1번 더해줍니다.
4. 2번 3번 과정을 M번 반복합니다.

<br>
## 알고리즘 구현

>제가 작성한 코드는 아래와 같습니다.

```java
import java.util.Arrays;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int N = scanner.nextInt();
        int M = scanner.nextInt();
        int K = scanner.nextInt();
        int sum = 0;
        int count = 0;

        int[] arr = new int[N];
        for(int i = 0; i < arr.length; i++){
            arr[i] = scanner.nextInt();
        }

        Arrays.sort(arr);

        for(int i = 0; i < M; i++){
            int firstBigNumber = arr[arr.length-1];
            int secondBigNumber = arr[arr.length-2];
            count++;

            if(count % K == 0){
                sum += secondBigNumber;
            }else{
                sum += firstBigNumber;
            }
        }

        System.out.println(sum);
    }
}
```
<br>

## 최적화와 시간복잡도

### 최적화
수학적인 계산을 통해 최대 합을 구하는 방식으로 변경하여 최적화 시킬 수 있다는 방법을 알았습니다.

### 시간 복잡도
주요 부분인 for 루프의 실행 횟수에 따라 시간 복잡도를 구할 수 있습니다.
1. 배열 입력 : O(N)
- 주어진 배열의 크기 N에 비례합니다.
2. 배열 정렬 : O(N log N)
- Arrays.sort 메소드는 일반적으로 O(N log N)의 시간 복잡도를 가집니다.
3. for 루프 : O(M)
- 루프의 반복 횟수는 M에 비례합니다.
따라서, 전체적인 시간 복잡도 O(N log N +M)입니다.
<br>

## 마무리