---
title: JAVA JUnit5 어노테이션
date: 2023-11-01 15:23:00 +0900
categories: [Java]
tags: [Java]
toc: true
toc_sticky: true
toc_label: 목차
math: true
mermaid: true
---
자바 테스트 코드작성을 위해 사용되는 Junit5 어노테이션을 정리해보았습니다.

## Junit 5 Annotation

### <font color="#43A047">@Test</font>

해당 어노테이션은 JUnit 5 에서 단위 테스트 메서드를 정의할 때 사용된다.   
JUnit은 테스트 패키지 하위의 @Test 어노테이션이 붙은 메소드를 단위 테스트로 인식하여 실행시킨다.
```java
    @Test
    void test(){
        ...
    }
```

<hr>

### <font color="#43A047">@DisplayName</font>

해당 어노테이션은 테스트 메서드의 이름을 사용자 정의로 변경하는 데 사용됩니다.    
테스트 메서드의 기본 이름은 메서드으로 지정된다.경우에 따라 사용자가 이름을 부여하고 싶을 때 사용한다.   
이렇게 하면 테스트 결과 보고서에서 더 명확한 이름이 표시된다.
```java
    @Test
    @DisplayName("새로운 테스트!")
    void test(){
    }
```
![](../../../../assets/img/2023-11-02-13-26-30.png)

<hr>

### <font color="#43A047">@ParameterizedTest</font>

해당 어노테이션은 매개변수를 받는 테스트를 작성하는데 사용한다.  
여러 입력 값에 대한 동일한 테스트 메서드를 여러번 실행할 수 있게 한다.
```java
    @ParameterizedTest
    @DisplayName("새로운 테스트!")
    void test(){
    }
```

<hr>

#### <font color="#43A047">@ValueSource</font>

해당 어노테이션은 매개변수화된 테스트를 수행할때 사용되는 어노테이션이다.   
이 어노테이션은 특정 데이터 값을 제공하여 테스트 메서드를 여러 번 실행하게한다.
```java
class Test {
    @ParameterizedTest
    @ValueSource(ints = {1,2,3,4,5})
    @DisplayName("0보다 큰값 인지 확인하는 테스트!")
    void test(int value){
        assertTrue(value > 0);
    }
}
```
![](../../../../assets/img/2023-11-02-13-30-53.png)

<hr>

#### <font color="#43A047">@CsvSource</font>

해당 어노테이션은 매개변수화된 테스트를 수행할때 사용되는 어노테이션이다.   
CSV(Comma-Separated Values) 형식의 데이터를 사용하여 테스트 메서드를 여러 번 실행하게 한다.   
`delimiter` 로 구분자를 지정할 수 있다.

```java
    @ParameterizedTest
    @CsvSource(value = {"1 : 2 : 3", "2 : 3 : 5", "3 : 4 : 7"}, delimiter =':')
    void test(int num1, int num2, int expectedSum){
        int sum = num1 + num2;
        assertEquals(expectedSum, sum);
    }
```
<hr>

### <font color="#43A047">@RepeatedTest</font>

해당 어노테이션은 동일한 테스트 메서드를 지정된 횟수만큼 반복 실행되는데 사용한다.   
이를 통해 반복 가능한 동작을 테스트 하거나 특정 조건을 여러 번 검증하는데 사용된다.
```java
    @RepeatedTest(3)
    void test(){
        int random = (int) Math.random() * 100;
        assertTrue(random >= 0 && random < 100);
    }
```
![](../../../../assets/img/2023-11-02-13-38-09.png)

<hr>

### <font color="#43A047">@TestFactory</font>

해당 어노테이션은 JUnit5에서 동적으로 테스트를 생성하고 실행할 때 사용되는 어노테이션이다.   
동적 테스트를 생성하면 테스트 메서드의 수나 구조를 실행중에 결정할 수 있다.

<hr>

### <font color="#43A047">@TestInstance</font>

해당 어노테이션은 JUnit5에서 테스트 클래스의 인스턴스 생성 방식을 설정하는데 사용된다.   
기본적으로 JUnit 5에서는 `@Test` 어노테이션을 사용하여 정의한 테스트 메서드 마다 다른 인스턴스를 생성한다.
@TestInstance 어노테이션은 두 가지 값이 있다.

- **`TestInstance.Lifecycle.PER_CLASS`**  

    테스트 클래스 내에서 단일 인스턴스를 공유한다. 테스트 간에 데이터를 공유한다.
    
    ```java
        @TestInstance(Lifecycle.PER_CLASS)
        public class TestInstanceTest {

            private int count = 0;

            @Test
            void Test_1(){
                count++;
            }

            @Test
            void Test_2(){
                Assertions.assertEquals(1, count);
            }
        }

    ```
    ![](../../../../assets/img/2023-11-02-13-56-02.png)
     테스트 클래스 내에서 단일 인스턴스를 공유하도록 설정했다
    
- **`TestInstance.Lifecycle.PER_METHOD`** 기본값
    
    각 테스트 메서드마다 새로운 인스턴스를 생성한다. 데스트 간에 데이터를 공유하지 않는다.
    
    ```java
        @TestInstance(Lifecycle.PER_METHOD)
        public class TestInstanceTest {

            private int count = 0;

            @Test
            void Test_1(){
                count++;
            }

            @Test
            void Test_2(){
                Assertions.assertEquals(1, count);
            }
        }
    ```
    ![](../../../../assets/img/2023-11-02-13-56-58.png)   
    각 테스트 메서드마다 새로운 테스트 클래스 인스턴스가 생성된다.   
    이렇게 하면 **`test_1`**과 **`test_2`** 간에 상태가 공유되지 않으므로 각 테스트 메서드는 독립된 실행을 보장한다.
    
<hr>

### <font color="#43A047">@TestTemplate</font>

해당 어노테이션은 Junit 5에서 동적으로 생성되는 테스트 케이스를 정의하는데 사용된다.   
**`@TestTemplate`**를 사용하면 테스트 케이스의 템플릿을 만들고,    
이 템플릿을 동적으로 여러 번 호출하여 다양한 테스트 케이스를 실행할 수 있다.   
이것은 특히 특정 조건에 따라 동일한 테스트 로직을 다른 입력 값 또는 상황에 대해 반복하여 수행해야 하는 경우에 유용하다.

<hr>

### <font color="#43A047">@TestMethodOrder</font>

해당 어노테이션은 테스트 메서드의 실행 순서를 구성할 때 사용된다.  
이 어노테이션을 사용하면 테스트 메서드가 실행되는 순서를 명시적으로 제어할 수 있다.  
기본적으로 Junit 5는 테스트 메서드의 실행순서를 보장하지 않는다.  

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.TestMethodOrder;
import org.junit.jupiter.api.MethodOrderer;
import org.junit.jupiter.api.MethodOrderer.OrderAnnotation;
import org.junit.jupiter.api.Order;

@TestMethodOrder(OrderAnnotation.class) // 테스트 메서드의 실행 순서를 설정
public class TestMethodOrderExample {

    @Test
    @Order(3)
    public void testC() {
        // 테스트 로직
    }

    @Test
    @Order(2)
    public void testB() {
        // 테스트 로직
    }

    @Test
    @Order(1)
    public void testA() {
        // 테스트 로직
    }
}
```
testA() → testB() → testC() 순서로 테스트 메서드가 실행된다.

<hr>

### <font color="#43A047">@BeforeEach</font>

해당 어노테이션은 Junit 5 에서 테스트 메서드를 실행 하기 전에 필요한 초기화 작업을 수행하기 위해 사용된다.   
`@BeforeEach` 어노테이션을 적용한 메서드는 각 테스트 메서드마다 실행된다.

```java
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class BeforeEachExample {

    private Calculator calculator;

    @BeforeEach
    void setUp() {
        calculator = new Calculator();
    }

    @Test
    void testAddition() {
        int result = calculator.add(2, 3);
        assertEquals(5, result);
    }

    @Test
    void testSubtraction() {
        int result = calculator.subtract(5, 2);
        assertEquals(3, result);
    }
}
```
**`@BeforeEach`**를 사용하여 중복 코드를 제거하고 테스트 케이스를 더 관리하기 쉽게 만들 수 있다.

<hr>

### <font color="#43A047">@AfterEach</font>

해당 어노테이션은 Junit 5에서 테스트 메서드 실행 이후에 정리 작업을 수행하기 위해 사용되는 어노테이션이다.   
**`@AfterEach`** 어노테이션을 사용한 메서드는 각 테스트 메서드 실행 이후에 호출된다.

```java
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class ResetValueExample {

    private int value = 0;

    @Test
    void testIncrementValue() {
        value++;
        assertEquals(1, value);
    }

    @Test
    void testDecrementValue() {
        value--;
        assertEquals(-1, value);
    }

    @AfterEach
    void resetValue() {
        value = 0; // 각 테스트 메서드 실행 후 값 초기화
    }
}
```

**`@AfterEach`** 어노테이션을 사용하여 **`resetValue`** 메서드를 정의한다.   
이 메서드는 각 테스트 메서드 실행 후에 **`value`** 값을 초기화한다.

이렇게 하면 각 테스트 메서드가 독립적으로 실행되고,   
**`value`**가 각 테스트 메서드 실행 후에 초기화되어 테스트 간에 상호 영향을 주지 않는다.

<hr>


### <font color="#43A047">@BeforeAll</font>

해당 어노테이션은 JUnit 5에서 테스트 클래스의 모든 메서드를 실행 이전에 단 한 번만 실행되는 메서드를 정의할때 사용한다.   
이 메서드를 사용하면 모든 테스트 메서드가 실행되기 전에 필요한 초기화 작업을 수행할 수 있다.

**`@BeforeAll`** 어노테이션을 사용한 메서드는 테스트 클래스 내에서 정적(static) 메서드로 선언되어야 한다.

```java
import org.junit.jupiter.api.BeforeAll;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class BeforeAllExample {

    private static Calculator calculator;

    @BeforeAll
    static void initializeCalculator() {
        calculator = new Calculator();
        System.out.println("Calculator initialized.");
    }

    @Test
    void testAddition() {
        int result = calculator.add(2, 3);
        assertEquals(5, result);
    }

    @Test
    void testSubtraction() {
        int result = calculator.subtract(5, 2);
        assertEquals(3, result);
    }
}
```

**`@BeforeAll`** 어노테이션을 사용하면 **`initializeCalculator`** 메서드가 한 번만 호출되므로    
모든 테스트 메서드에서 동일한 **`Calculator`** 인스턴스를 공유한다.   
이를 통해 중복 초기화를 방지하고 모든 테스트 메서드가 독립적으로 실행되는 것을 확인할 수 있다.

<hr>

### <font color="#43A047">@eforeEach vs @BeforeAll</font>

**`@BeforeAll`**과 **`@BeforeEach`** 어노테이션은 JUnit 5에서 테스트 초기화 작업을 수행하는 데 사용되지만 그 실행 시점과 범위에서 차이가 있다.   

**`beforeAll`**:

- 실행 시점: 테스트 클래스의 모든 테스트 메서드가 실행되기 전에 딱 한 번만 실행된다.
- 범위: 정적(static) 메서드로 선언되어야 하며, 테스트 클래스의 모든 테스트 메서드에서 공유되는 초기화 작업을 수행한다.
- 목적: 모든 테스트 메서드에 대한 공통 초기화 또는 설정을 수행한다.

**`BeforeEach`**:

- 실행 시점: 각 테스트 메서드가 실행되기 전에 각각 실행된다.
- 범위: 인스턴스 메서드로 선언되어야 하며, 각 테스트 메서드에 대해 개별적인 초기화 또는 설정을 수행합니다.
- 목적: 각 테스트 메서드의 실행 이전에 필요한 초기화 작업을 수행하여 각 테스트 메서드 간에 독립성을 유지한다.

<hr>

### <font color="#43A047">@AfterAll</font>

해당 어노테이션은 JUnit 5에서 모든 테스트 메서드를 실행한 이후 한 번만 실행되는 메서드를 정의하는데 사용한다.   
**`@AfterAll`** 어노테이션을 사용한 메서드는 테스트 클래스 내에서 정적(static) 메서드로 선언되어야 한다.

```sql
import org.junit.jupiter.api.AfterAll;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class AfterAllExample {

    private static Calculator calculator;

    @Test
    void testAddition() {
        calculator = new Calculator();
        int result = calculator.add(2, 3);
        assertEquals(5, result);
    }

    @Test
    void testSubtraction() {
        int result = calculator.subtract(5, 2);
        assertEquals(3, result);
    }

    @AfterAll
    static void cleanUp() {
        calculator = null; // 테스트 클래스의 모든 테스트 메서드 실행 이후에 객체를 정리
        System.out.println("Cleaned up.");
    }
}
```

**`@AfterAll`** 어노테이션을 사용하여 **`cleanUp`** 메서드를 정의한다.    
이 메서드는 테스트 클래스의 모든 테스트 메서드 실행 이후에 **`calculator`** 객체를 **`null`**로 설정하여 정리 작업을 수행한다.

<hr>

### <font color="#43A047">@Nested</font>

해당 어노테이션은 JUnit 5에서 중첩된 테스트 클래스를 정의하고 관리하는데 사용 되는 어노테이션이다.   
중첩된 테스트 클래스를 사용하면 테스트 클래스 내에서 테스트를 더 구조적으로 조직하고,  
테스트 케이스 간에 공통 설정을 재사용할 수 있다.   

쉽게 말하여 테스트 클래스 내에서 또 다른 클래스를 정의하고 사용하는 것을 허용하는것.  

```java
import org.junit.jupiter.api.Nested;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class NestedExample {

    @Nested
    class AdditionTests {
        @Test
        void testPositiveNumbers() {
            int result = Calculator.add(2, 3);
            assertEquals(5, result);
        }

        @Test
        void testNegativeNumbers() {
            int result = Calculator.add(-2, -3);
            assertEquals(-5, result);
        }
    }

    @Nested
    class SubtractionTests {
        @Test
        void testPositiveNumbers() {
            int result = Calculator.subtract(5, 3);
            assertEquals(2, result);
        }

        @Test
        void testNegativeNumbers() {
            int result = Calculator.subtract(-5, -3);
            assertEquals(-2, result);
        }
    }
}
```

**`@Nested`** 어노테이션을 사용하면 테스트 클래스를 논리적으로 구조화하고 테스트 메서드를 그룹화하여,   
읽기 쉬운 테스트 보고서를 생성할 수 있으며, 테스트를 더 체계적으로 조직할 수 있다.

<hr>

### <font color="#43A047">@Tag</font>

해당 어노테이션은JUnit 5에서 테스트 메서드 또는 테스트 클래스에 태그를 지정하는데 사용되는 어노테이션이다.

```java
import org.junit.jupiter.api.Tag;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class TagExample {

    @Test
    @Tag("smoke")
    void testSmokeTest() {
        // 스모크 테스트 수행
        assertTrue(true);
    }

    @Test
    @Tag("performance")
    void testPerformanceTest() {
        // 성능 테스트 수행
        // ...
    }
}
```

**`@Tag`** 어노테이션을 사용하여 각 테스트 메서드에 다른 태그를 부여한다. 

이렇게 하면 각 테스트 메서드가 특정 카테고리에 속하게 되고, 필요한 경우 특정 태그를 사용하여 테스트를 필터링하거나 실행할 수 있다.

<hr>

### <font color="#43A047">@Disabled</font>

해당 어노테이션은 JUnit 5에서 테스트 메서드 또는 테스트 클래스를 비활성화하는데 사용하는 어노테이션이다.   
이 어노테이션은 특정 테스트를 일시적으로 또는 영구적으로 실행에서 제외하려는 경우에 사용한다.

```java
import org.junit.jupiter.api.Disabled;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class DisabledExample {

    @Test
    void testEnabled() {
        // 활성화된 테스트
        assertEquals(2, 1 + 1);
    }

    @Disabled
    @Test
    void testDisabled() {
        // 비활성화된 테스트
        assertEquals(4, 2 * 2);
    }
}
```

**`@Disabled`** 어노테이션을 사용하여 **`testDisabled`** 메서드를 비활성화 상태로 설정한다.   
이로 인해 해당 테스트가 실행에서 제외되며, **`testEnabled`** 메서드만 실행됩니다.

### <font color="#43A047">@Timeout</font>

해당 어노테이션은 테스트 메서드 또는 테스트 클래스에 대해 최대 실행시간을 지정하는데 사용하는 어노테이션이다.   
이를 사용하여 특정 메서드가 지정된 시간 내 완료하지 않으면 실패하도록 설정할 수 있다.

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.Timeout;
import static org.junit.jupiter.api.Assertions.*;

public class TimeoutExample {

    @Test
    @Timeout(1) // 1밀리초로 제한
    void testShortExecution() {
        // 1밀리초 이내에 완료되어야 함
        assertTrue(true);
    }

    @Test
    @Timeout(value = 2, unit = Timeout.SECONDS) // 2초로 제한
    void testLongExecution() {
        // 2초 이내에 완료되어야 함
        try {
            Thread.sleep(3000); // 3초 동안 대기
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

**`@Timeout`** 어노테이션을 사용하여 **`testShortExecution`** 메서드는 1밀리초로 실행 시간을 제한하고,   
**`testLongExecution`** 메서드는 2초로 실행 시간을 제한한다. 