---

title: Oracle Profile 공부하기
date: 2023-12-08 17:00:00 +0900
categories: [DB]
tags: [Oracle,Profile,Oracle Profile]
toc: true
toc_sticky: true
toc_label: 목차
math: true
mermaid: true
---

## 오라클 프로파일이란?
오라클 데이터 베이스에서 사용자에 대한 리소스 제어와 권한 관리를 위한 설정을 담당하는 객체이다.  

<br>

**Profile은 다음과 같은 요소를 제어하는데 사용된다.**
- 세션 제한
- 리소스 제한
- 비용 제한
- 권한 제한

<br>

## 오라클 프로파일 조회
`SELECT * FROM DBA_PROFILE` 명령어를 사용하여 프로파일 객체를 조회할 수 있다.

<p align="center">
  <img src="../../../../assets/img/2023-12-08-17-11-43.png">
</p>

<br>

## 프로파일 속성

#### SESSIONS_PER_USER
- 사용자가 동시에 가질 수 있는 최대 세션 수를 제한한다.
- `SESSIONS_PER_USER 5` : 특정 사용자에 대해 최대 5개의 동시 세션을 허용하도록한다.

<br>

#### CPU_PER_SESSION
- 사용자 세션당 허용되는 CPU 시간의 제한을 설정한다.
- 단위는 1/100초, 즉 100 으로 지정하면 1초로 설정된다.
- `CPU_PER_SESSION 100` : 사용자 세션은 1초 동안에만 CPU자원을 사용할 수 있도록 제한한다.

<br>

#### CPU_PER_CALL
- 사용자 세션에서 각 SQL 호출에 대한 CPU 시간의 제한을 설정한다.
- 단위는 1/100초, 즉 100 으로 지정하면 1초로 설정된다.
- `CPU_PER_CALL 100` : 사용자의 세션에거 각 SQL문장이 실행될때 1초 동안에만 CPU자원 할당하도록 제한한다.

<br>

#### LOGICAL_READS_PER_SESSION
- 사용자 세션에서 수행되는 쿼리 및 데이터 액세스 작업에 대한 제한을 설정한다.
- `LOGICAL_READS_PER_SESSION 1000` : 특성 사용자의 세션에서는 1000번을 초과하는 논리적인 읽기 작업을 수행불가.

<br>

#### LOGICAL_READS_PER_CALL
- 한 번의 SQL 호출에 대해 허용되는 논리적인 읽기 작업 수를 제한한다.
- `LOGICAL_READS_PER_CALL 1000` : 특정 SQL문장이 실행될때 1000번을 초과하는 논리적인 읽기 작업 수행불가.

<br>

##### IDLE_TIME
- 사용자 세션이 유휴 상태로 유지될 수 있는 최대 시간을 제한한다.
- 단위는 분 단위
- `IDLE_TIME 5` : 5분 동안 활동이 없는 세션은 오라클 서버가 강제로 접속을 끊는다.
  
<br>

#### CONNECT_TIME
- 사용자가 하루 동안 DB Server에 접속할 수 있는 시간을 설정한다.
- `CONNECT_TIME 60` : 특정 사용자가 하루 동안 총 60분 동안 데이터베이스에 접속할 수 있다.

## PROFILE 관리

### 프로파일 생성

아래와 같은 명령어로 프로파일 생성이 가능하다.

```sql
CREATE PROFILE profile_name 
    LIMIT
        SESSIONS_PER_USER 5 -- 사용자당 최대 세션 수를 5로 제한
        CPU_PER_SESSION 100 -- 세션당 허용되는 CPU 시간을 1초로 제한한다.
        CONNECT_TIME 60 -- 하루 동안 허용되는 최대 연셜 시간을 60분으로 제한한다.
        -- 여러 다른 제한 사항 추가 가능
    ;
```

<br>

### 프로파일 수정

위에서 만들었던 프로파일을 수정해보자. 

```sql
ALTER PROFILE profile_name
    LIMIT
        SESSIONS_PER_USER 10
        CPU_PER_SESSION 200
        CONNECT_TIME 120
        -- 여러 다른 제한 사항 추가 가능
    ;
```
<br>

### 프로파일 삭제

위에서 만들었던 프로파일을 삭제해보자.

```sql
DROP PROFILE profile_name CASCADE;
```

프로파일을 삭제하면 해당 프로파일을 사용 중인 사용자에게 더 이상 프로파일 제한이 적용되지 않는다.

하지만 이미 프로파일을 사용 중인 사용자가 있다면 삭제하는 것이 불가능하다. 그럴떈 `CASCADE` 옵션을 사용한다.

`CASCADE` 옵션을 사용하여 해당 프로파일을 사용 중인 사용자에게 자동으로 새로운 프로파일이 할당되며
이전 프로파일이 설정이 적용되지 않게 된다.

<br>

## 예제 문제

### 조건
- 같은 계정으로 접속할 수 있는 세션 수는 최대 5로 제한
- 세션 내 최대 CPU를 사용할 수 있는 시간을 150 으로 제한
- 5분동안 사용하지 않으면 강제로 접속을 끊을것.
- 프로파일의 이름은 'kr' 로 지정

### 풀이

```sql
CREATE PROFILE kr 
    LIMIT
        SESSION_PER_USER 5
        CPU_PER_SESSIOn 150
        IDLE_TIME 5
    ;
```

## 사용자에게 PROFILE 할당하기

**할당하기 앞서 먼저 사용자가 적용하고 있는 PROFILE 부터 확인해보자.**

오라클 PROFILE은 `dba_users` 테이블에서 확인할 수 있다.

```sql
CREATE USER tester IDENTIFED BY 1234;
SELECT USERNAME, PROFILE FROM DBA_USERS
WHERE USERNAME = 'TESTER';
```

<p align="center">
  <img src="../../../../assets/img/2023-12-08-17-43-41.png">
</p>


기본적으로 계정을 생성시 `DEFAULT` 프로파일을 적용받는 것을 확인할 수 있다.

그렇다면 `DEFAULT` 프로파일에는 어떤 제약사항이 있을까?

```sql
SELECT * FROM DBA_PROFILES
WHERE PROFILE = 'DEFAULT';
```
<p align="center">
  <img src="../../../../assets/img/2023-12-08-17-48-13.png">
</p>

---

본격적으로 프로파일을 생성하고 유저에게 프로파일을 적용시키고 확인해보자.

```sql
-- 프로파일 생성
CREATE PROFILE pr 
    LIMIT 
        IDLE_TIME 5
    ;

-- tester 사용자에게 pr 프로파일을 적용
ALTER USER tester PROFILE pr;

 -- tester 사용자에게 적용된 프로파일 조회
SELECT USERNAME, PROFILE FROM DBA_USERS
WHERE USERNAME = 'TESTER';
```
위 코드는 `pr` 이라는 프로파일을 만들고 tester 유저에게 프로파일을 적용하고 조회하였다.

<p align="center">
  <img src="../../../../assets/img/2023-12-08-17-56-24.png">
</p>

---

### 정리
**프로파일 속성**
- SESSIONS_PER_USER
- CPU_PER_SESSION
- CPU_PER_CALL
- LOGICAL_READS_PER_SSEION
- LOGICAL_READS_PER_CALL
- IDLE_TIME
- CONNECT_TIME
  
**프로파일 관리**

- CREATE PROFILE profile_name LIMIT 제약사항..
- ALTER PROFILE profile_name LIMIT 제약사항..
- DROP PROFILE profile_name CASCADE
- SELECT * FROM DBA_PROFILES


**프로파일 적용**
- ALTER USER 사용자 PROFILE 프로파일
