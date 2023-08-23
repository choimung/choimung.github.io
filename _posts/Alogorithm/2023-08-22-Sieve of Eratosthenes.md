---

title: 에라토스테네스의 체 알고리즘
date: 2023-08-22 20:35:00 +0900
categories: [Algorithm]
tags: [Algorithm]

---

### 개요
<hr>

#### 에라토스테네스의 체 알고리즘이란?
고대 그리스의 수학자 *에라토스테네스*가 만들어 낸 소수를 찾는방법이다.
마치 체로 치듯이 수를 걸러낸다고 하여 '에라토스테네스의 체'라고 부른다.

임의의 자연수 n에 대해 그 이하의 소수를 모두 찾는, 가장 간단하고 빠른 방법이다.


1~15까지의 소수를 찾는다 가정

|||||||
|:---:|:---:|:---:|:---:|:---:|:---:|
|1|2|3|4|5|
|6|7|8|9|10|
|11|12|13|14|15|
|||||||

소수





### 입력
<hr>
첫째 줄에 N과 B가 주어진다. (2 ≤ B ≤ 36)

B진법 수 N을 10진법으로 바꾸면, 항상 10억보다 작거나 같다.

### 출력
<hr>
첫째 줄에 B진법 수 N을 10진법으로 출력한다.


### 풀이
<hr>
```java
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);

        String number = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ";
        String str = scanner.next();
        int N = scanner.nextInt();
        int decimalNumber = 0;

        for(int i = 1 ; i <= str.length(); i++){
            double pow = Math.pow(N, i - 1);
            decimalNumber += number.indexOf(str.charAt(str.length()-i)) * pow;
        }

        System.out.println(decimalNumber);

    }
}
```

### 풀이과정
<hr>

