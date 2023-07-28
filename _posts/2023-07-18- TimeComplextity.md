---
title: 시간 복잡도(Time Complexity)
date: 2023-07-18 13:15:00 +0900
categories: [Algorithm, TimeComplexity]
tags: [github blog,algorithm,timecomplexity]
toc: true
toc_sticky: true
toc_label: 목차
math: true
mermaid: true
---

## 소개

### 시간복잡도란?
알고리즘의 실행 시간이 입력 크기에 대해 어떻게 증가하는지를 나타내는 개념입니다.
알고리즘이 문제를 해결하는 데 걸리는 시간이 입력 크기와 어떤 관계를 가지는지를 분석함으로써, 알고리즘의 성능을 평가하고 비교할 수 있습니다.

알고리즘의 성능을 측정하는 데에는 몇 가지 방법이 있지만, 가장 널리 사용되는 방법 중 하나가 "빅 오 표기법"입니다.
빅 오 표기법은 알고리즘의 시간복잡도를 대략적으로 나타내는 표기법으로, 알고리즘의 실행 시간이 입력 크기에 대해 어떤 속도로 증가하는지를 표현합니다.

### 시간복잡도를 이해해야되는 이유
1. 알고리즘의 효율성을 평가하여 더 나은 알고리즘을 선택할 수 있습니다.
2. 큰 데이터셋에서 알고리즘의 실행 시간이 증가하는 양상을 예측할 수 있습니다.
3. 시간복잡도 분석을 통해 알고리즘의 성능을 최적화 할 수 있는 방법을 찾을 수 있습니다.

<br>

## 알고리즘의 실행 시간 분석
### 기본 명령문
- 알고리즘의 실행 시간을 분석하기 위해 우리는 기본 명령문(Primitive Operations)을 고려합니다.
기본 명령문은 알고리즘이 실행되는 동안 실제로 수행되는 단순한 명령어들을 의미합니다.
예를 들면, 덧셈,뺄셈,곱셉,대입 등의 기본적인 연산들이 이에 해당합니다.

### 최악,평균,최선 시간복잡도
- 알고리즘의 시간복잡도를 분석할 떄에는 주로 세 가지 시간복잡도를 고려합니다.

#### 최악 시간복잡도
- 최악 시간복잡도는 알고리즘이 주어진 입력에 대해 가장 오래 걸리는 경우를 나타냅니다.
알고리즘의 실행 시간은 입력의 특정 조건에 따라 다르기 때문에, 최악의 경우에 대한 분석은 실행시간의 상한을 제공합니다.
빅 오 표기법에서는 최악 시간복잡도를 주로 사용합니다.

#### 평균 시간복잡도
- 평균 시간복잡도는 알고리즘이 모든 가능한 입력에 대해 평균적으로 얼마나 걸리는지를 나타냅니다.
이는 알고리즘의 성능을 더 정확하게 평가하기 위해 사용됩니다.

#### 최선 시간복잡도
- 최선 시간복잡도는 알고리즘이 주어진 입력에 대해 가장 적게 걸리는 경우를 나타냅니다.
이는 알고리즘이 최적의 상황에서 얼마나 잘 수행되는지를 보여줍니다. 하지만 실제로 최선의 경우가 발생하는 일은 드물기 때문에
일반적으로 최선 시간복잡도는 중요하게 다루지 않습니다.

<br>

## 자주 사용되는 시간복잡도 클래스
### 0(1) - 상수시간
입력 크기 (n)에 상관없이 알고리즘의 실행 시간이 일정한 경우를 의미합니다.
이는 입력의 크기가 증가하더라도 알고리즘의 수행 시간이 변하지 않음을 의미합니다.
보통 기본적인 연산이나 상수 개수의 작업에 해당합니다.
```java
public static void main(String[] args) {
        int a = 10;
        int b = 20;
        int result = a + b;
    }
```
위의 코드에서 constantTimeFunction() 함수는 입력의 크기에 관계없이 항상 덧셈 연산과 출력문을 한 번만 수행합니다.
이때, 알고리즘의 실행 시간은 입력의 크기가 어떻든지 항상 일정하므로, 이 함수는 0(1)시간 복잡도를 가집니다.

### 0(log N) - 로그시간
입력의 크기 n에 대해 로그 함수의 형태로 실행 시간이 증가함을 의미합니다.
보통 이런 알고리즘은 입력의 크기가 증가해도 실행 시간이 상대적으로 느리게 증하는 경우에 해당합니다.
문제를 해결하는데 필요한 단계들이 연산마다 특정 요인에 의해 줄어듬

이진 탐색을 예로 들 수 있습니다. 이진 탐색은 탐색 범위를 절반씩 좁혀가며 데이터를 탐색하기 때문에 확인하는 데이터 개수가 절반씩 줄어든다는 점에서 O(logN)로 표현할 수 있습니다.
예를 들어, 데이터의 크기가 N = 32일 때, O(log N)의 알고리즘은 최대 log2(32) = 5번의 반복을 수행합니다. 
이러한 로그 시간 특성은 입력 크기가 두 배로 증가할 때마다 알고리즘의 실행 시간이 약간씩 증가함을 의미합니다.

```java
public class BinarySearchExample {

    // 정렬된 배열에서 target을 이진 탐색하여 인덱스를 반환하는 함수
    public static int binarySearch(int[] arr, int target) {
        int left = 0;
        int right = arr.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (arr[mid] == target) {
                return mid;
            } else if (arr[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        return -1; // 타겟이 배열에 없을 경우 -1 반환
    }

    public static void main(String[] args) {
        int[] sortedArray = { 1, 3, 5, 7, 9, 11, 13, 15 };
        int target = 7;
        int result = binarySearch(sortedArray, target);
        System.out.println("Target " + target + " found at index: " + result);
    }
}
```

### 0(n) : 선형시간
입력 크기에 비례하여 실행 시간이 증가하는 경우를 의미합니다. 
즉 입력의 크기 N이 증가 할때, 알고리즘의 실행시간도 N에 비례하여 증가합니다.
```java
public class LinearTimeExample {

    // 선형 시간 알고리즘: 배열의 모든 요소를 출력
    public static void printArrayElements(int[] arr) {
        for (int num : arr) {
            System.out.print(num + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        int[] arr = { 1, 2, 3, 4, 5 };
        printArrayElements(arr);
    }
}
```
N개의 요소를 가진 배열을 한 번 순회하여 모든 요소를 확인하는 알고리즘은 선형시간을 가집니다.
배열의 크기 N이 두 배로 늘어날때마다 알고리즘의 실행 시간도 두배로 증가합니다.

### O(n log n) - 선형 로그 시간
로그 시간과 선형 시간이 결합된 시간 복잡도를 나타내는 표기법으로
O(n log N)으로 표기됩니다. 이는 입력 크기 N에 대해 로그 함수와 선형 함수가 곱해진 형태로 실행 시간이 증가합니다.
```java
public class MergeSortExample {

    // 머지 정렬 (Merge Sort) 함수
    public static void mergeSort(int[] arr) {
        if (arr.length <= 1) {
            return; // 배열의 길이가 1 이하면 이미 정렬된 상태이므로 그대로 반환
        }

        int mid = arr.length / 2;
        int[] left = new int[mid];
        int[] right = new int[arr.length - mid];

        // 배열을 두 부분으로 나누기
        System.arraycopy(arr, 0, left, 0, mid);
        System.arraycopy(arr, mid, right, 0, arr.length - mid);

        // 두 부분 배열을 재귀적으로 정렬
        mergeSort(left);
        mergeSort(right);

        // 정렬된 두 부분 배열을 합병
        merge(arr, left, right);
    }

    // 두 개의 배열을 합병하는 함수
    public static void merge(int[] arr, int[] left, int[] right) {
        int i = 0, j = 0, k = 0;

        while (i < left.length && j < right.length) {
            if (left[i] < right[j]) {
                arr[k++] = left[i++];
            } else {
                arr[k++] = right[j++];
            }
        }

        while (i < left.length) {
            arr[k++] = left[i++];
        }

        while (j < right.length) {
            arr[k++] = right[j++];
        }
    }

    public static void main(String[] args) {
        int[] arr = { 12, 3, 9, 7, 5, 15, 10, 1 };
        mergeSort(arr);

        System.out.print("Sorted Array: ");
        for (int num : arr) {
            System.out.print(num + " ");
        }
        System.out.println();
    }
}

```
### O(n^2) - 이차 시간
두 개의 중첩된 반복문을 사용하여 처리하는 경우가 일반적입니다.
각 반복문은 입력은 입력의 크기에 비례하여 실행되기 때문에 반복문이 중첩되면 전체 알고리즘의 실행 시간은
N^2이 비례하게 됩니다.
```java
public static void main(String[] args) {

int[] array = {3, 5, 2, 1, 4};

for(int i = 0; i < array.length; i++) {
    for(int j = 0; j < array.length; j++) {
         System.out.println(a+b);
        }
    }
}
array length만큼 중첩루프를 사용하여 연산을 수행하므로 시간 복잡도는 O(N^2)로 표현할 수 있다.

```

### O(2^n) - 지수 시간
입력 크기 N에 대해 2의 N제곱에 비례하여 실행 시간이 증가하는 경우에 해당합니다.
0(2^N) 시간 복잡도를 가진 알고리즘은 보통 재귀적인 호출이나 부분 집합 생성과 같이 모든 간으한 조합을 확인하는 경우에 발생합니다.
입력 크기가 증가할수록 실행시 간이 기하급수적으로 늘어날 수 있습니다. 따라서 입력 크기가 큰 경우에는 더 효율적인 알고리즘을 선택하는것이 중요합니다.

<br>

## 마무리