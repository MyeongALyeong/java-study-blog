# 📚 Chap 11: 기본 API 클래스


---

## ✨ 11-1 `java.lang` 패키지

### 📋 java.lang 패키지에 속하는 주요 클래스 & 용도

![image](https://github.com/user-attachments/assets/f3b4f02e-e87c-4800-8fe6-5588f7dc4670)


---

### 🛠️ 1) `Object` 클래스

- 모든 자바 클래스의 최상위 조상 클래스  
- 직접 상속하지 않아도, `extends Object`가 자동으로 적용됨  
- 주요 메서드:  
  1. **`equals(Object obj)`**  
     - 객체가 저장하는 “데이터의 동일성” 판단  
     - 기본 구현: 참조 비교 (`==`)  
     - 커스텀 클래스에서는 재정의(override)하여 “필드 값 비교” 로직 작성  
  2. **`hashCode()`**  
     - 객체를 식별할 수 있는 정수값(해시코드) 반환  
     - `equals()`를 재정의할 때 반드시 `hashCode()`도 재정의해야 함  
  3. **`toString()`**  
     - 객체를 문자열(String)로 표현한 값 반환  
     - 기본 구현: `클래스이름@16진수_해시코드`  
     - 대표적인 예시:  
       - `Date`: 현재 날짜/시간을 사람이 읽기 좋은 형태로 반환  
       - `String`: 객체에 저장된 문자열 자체를 반환  

#### 💡 Member 클래스에서 equals()메서드 재정의 예제


![image](https://github.com/user-attachments/assets/c2c2b6af-d600-4a68-9653-0457db53ea2e)


#### 💡 연습문제

![image](https://github.com/user-attachments/assets/ceb6e0be-c32f-4bab-8475-7576f924b2b4)


#### 💡 toString() 오버라이딩 예제

![image](https://github.com/user-attachments/assets/f74a165d-461c-44de-9e90-f798bca47c98)


---

### 🛠️ 2) `System` 클래스

- `System` 클래스를 이용하면 운영체제와 JVM 일부 기능을 활용할 수 있음  
- 주요 필드 & 메서드:  
  1. **표준 입출력**  
     - `System.out` : 표준 출력 스트림 (`PrintStream`)  
     - `System.err` : 표준 오류 출력 스트림 (`PrintStream`)  
     - `System.in` : 표준 입력 스트림 (`InputStream`)  
  2. **프로그램 종료**  
     - `System.exit(int status)` : JVM 강제 종료  
       ```java
       System.exit(0);  // 정상 종료
       System.exit(1);  // 비정상 종료 (관례적으로 0 이외 값은 오류)
       ```  
  3. **현재 시각 읽기**  
     - `System.currentTimeMillis()` : 1970년 1월 1일 00:00:00 UTC 이후 경과한 밀리초(ms) 반환  
     - `System.nanoTime()` : JVM이 시작된 이후 경과한 나노초(ns) 반환 (주로 시간 측정 용도)  
       ```java
       long start = System.nanoTime();
       // ... 실행할 코드 ...
       long end = System.nanoTime();
       System.out.println("실행 시간: " + (end - start) + " ns");
       ```  
  4. **메모리 관리 및 기타**  
     - `System.gc()` : JVM에게 가비지 컬렉터 실행을 요청 (즉시 실행을 보장하지 않음)  
     - `System.getProperty(String key)` : 시스템 프로퍼티(예: `"user.home"`, `"os.name"`) 조회  

#### 💡 `System` 예시 코드: 시간 측정 및 종료

```java
public class SystemExample {
    public static void main(String[] args) {
        System.out.println("프로그램 시작 👉");

        // 간단한 시간 측정 예제
        long startMillis = System.currentTimeMillis();
        // 임의 반복문 (딜레이를 위한 예제)
        int sum = 0;
        for (int i = 1; i <= 100_000; i++) {
            sum += i;
        }
        long endMillis = System.currentTimeMillis();
        System.out.println("1부터 100,000까지 합: " + sum);
        System.out.println("실행 시간: " + (endMillis - startMillis) + " ms");

        System.out.println("프로그램 종료 👋");
        //System.exit(0); // 주석 해제 시 프로그램이 즉시 종료됨
    }
}
```

---

### 🛠️ 3) `Class` 클래스

- 클래스와 인터페이스의 **메타데이터(metadata)** 를 관리  
- 런타임에 클래스의 정보를 동적으로 조회하거나,  
- 리플렉션(reflection)을 통해 인스턴스를 생성하거나 메서드를 호출할 때 사용됨  
- 주요 메서드:  
  1. **`getClass()`** (`Object`로부터 상속)  
     - 인스턴스가 속한 클래스의 `Class` 객체 반환  
     - 예: `String s = "Hello"; Class<?> cls = s.getClass();`  
  2. **`Class.forName(String className)`**  
     - 주어진 클래스 이름(문자열)으로부터 `Class` 객체를 동적으로 로딩  
     - 예: `Class<?> cls = Class.forName("com.example.MyClass");`  
  3. **리플렉션 활용**  
     - `cls.getDeclaredFields()` : 클래스가 가진 필드 목록 조회  
     - `cls.getDeclaredMethods()` : 클래스가 가진 메서드 목록 조회  
     - `cls.getConstructor(...)` : 특정 생성자 조회 및 `newInstance()` 호출  

#### 💡 `Class` 예시 코드: 동적 클래스 로딩

```java
import java.util.Arrays;
import java.lang.reflect.Modifier;

public class ReflectionExample {
    public static void main(String[] args) {
        try {
            // 1. String 인스턴스에서 getClass() 사용
            String str = "Hello Reflection";
            Class<?> clazz1 = str.getClass();
            System.out.println("clazz1: " + clazz1.getName());  // java.lang.String

            // 2. Class.forName() 사용하여 클래스 로딩
            Class<?> clazz2 = Class.forName("java.util.ArrayList");
            System.out.println("clazz2: " + clazz2.getName());  // java.util.ArrayList

            // 3. 리플렉션으로 메서드 목록 출력
            System.out.println("=== ArrayList Methods ===");
            Arrays.stream(clazz2.getDeclaredMethods())
                  .filter(m -> Modifier.isPublic(m.getModifiers()))
                  .forEach(m -> System.out.println("- " + m.getName()));
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

---

### 🛠️ 4) `String` 클래스  📑  

> - **String**: 문자열을 저장하고 다양한 문자열 처리 메서드를 제공  

![image](https://github.com/user-attachments/assets/1cb846f2-8373-4721-b1b6-3dba1026d7c3)

#### 💡 String 주요 메서드 예제

![image](https://github.com/user-attachments/assets/6488cb77-a07a-4ef8-8b90-65de8ec0099a)

![image](https://github.com/user-attachments/assets/b935b0b1-a70b-4c97-9015-bbcb6869962a)

---

### 🛠️ 5) `Wrapper` 클래스

> **Wrapper 클래스 종류**:  
> - `Byte`, `Short`, `Character`, `Integer`, `Float`, `Double`, `Boolean`, `Long`  

1. **박싱(Boxing) & 언박싱(Unboxing)**  
   - **박싱**: 기본 타입(primitive)을 Wrapper 객체로 변환  
     ```java
     int primitiveInt = 42;
     Integer boxedInt = Integer.valueOf(primitiveInt); // 명시적 박싱
     Integer autoBoxed = primitiveInt;                  // 자동 박싱 (Auto-boxing)
     ```  
   - **언박싱**: Wrapper 객체에서 기본 타입 값 추출  
     ```java
     Integer wrapperInt = 100;
     int unboxed = wrapperInt.intValue();  // 명시적 언박싱
     int autoUnboxed = wrapperInt;         // 자동 언박싱 (Auto-unboxing)
     ```  

2. **문자열 ↔ 기본 타입 변환**  
   - 문자열 → 기본 타입  
     ```java
     String strNum = "123";
     int value1 = Integer.parseInt(strNum);    // 기본 타입 int
     Integer value2 = Integer.valueOf(strNum); // Wrapper 객체
     double d1 = Double.parseDouble("3.14");
     Double d2 = Double.valueOf("3.14");
     ```  
   - 기본 타입 → 문자열  
     ```java
     int num = 99;
     String s1 = String.valueOf(num);
     String s2 = Integer.toString(num);
     ```  

3. **입력값 검사 (Input Validation)**  
   - 사용자가 입력한 문자열이 숫자인지 아닌지를 검사할 때 유용  
     ```java
     String input = "456a";
     try {
         int parsed = Integer.parseInt(input);
         System.out.println("정수로 변환 성공: " + parsed);
     } catch (NumberFormatException e) {
         System.err.println("유효하지 않은 숫자 형식입니다: " + input);
     }
     ```  

4. **기타 유용한 메서드**  
   - `Integer.MAX_VALUE`, `Integer.MIN_VALUE` (최댓값/최솟값 상수)  
   - `Boolean.parseBoolean(String s)` (문자열 → boolean)  
   - `Character.isDigit(char ch)`, `Character.isLetter(char ch)` (문자 검사 메서드)

---

### 🛠️ 6) `Math` 클래스

- 수학 관련 정적 메서드 제공  
- **대표 메서드**:  
  1. **삼각함수**  
     - `Math.sin(double a)`, `Math.cos(double a)`, `Math.tan(double a)`  
     - 인자는 라디안(radian) 단위  
  2. **지수 및 로그**  
     - `Math.exp(double a)` : \(e^a\)  
     - `Math.log(double a)` : 자연로그(base \(e\))  
     - `Math.log10(double a)` : 상용로그(base 10)  
     - `Math.pow(double a, double b)` : \(a^b\)  
  3. **절대값/반올림/절삭**  
     - `Math.abs(int/long/float/double)`  
     - `Math.round(double a)` : 가장 가까운 정수(소수 첫째 자리에서 반올림)  
     - `Math.ceil(double a)` : 올림 (ex. 3.1 → 4.0)  
     - `Math.floor(double a)` : 내림 (ex. 3.9 → 3.0)  
  4. **난수 생성**  
     - `Math.random()` : [0.0, 1.0) 범위의 `double` 난수 반환  
       ```java
       double r = Math.random();   // 0.0 <= r < 1.0
       int randInt = (int)(Math.random() * 100) + 1; // 1 ~ 100 사이 난수
       ```  

#### 💡 `Math` 예시 코드

```java
public class MathExample {
    public static void main(String[] args) {
        double x = 2.7;
        double y = -3.4;

        System.out.println("abs(" + y + ") = " + Math.abs(y));
        System.out.println("ceil(" + x + ") = " + Math.ceil(x));
        System.out.println("floor(" + x + ") = " + Math.floor(x));
        System.out.println("round(" + x + ") = " + Math.round(x));

        double base = 2.0, exponent = 3.0;
        System.out.println(base + "^" + exponent + " = " + Math.pow(base, exponent));

        double angle = Math.PI / 4;  // 45도
        System.out.println("sin(45°) = " + Math.sin(angle));
        System.out.println("cos(45°) = " + Math.cos(angle));

        // 난수 예제
        System.out.println("Random [0.0,1.0): " + Math.random());
        System.out.println("Random Int [1,10]: " + ((int)(Math.random() * 10) + 1));
    }
}
```

---

## ✨ 11-2 `java.util` 패키지

> `java.util` 패키지는 다양한 유틸리티 클래스와 컬렉션 프레임워크를 제공


### 🕰️ 1) `Date` 클래스

- **패키지**: `java.util.Date`  
- **용도**:  
  - 날짜와 시간을 **밀리초 단위**로 저장하는 클래스  
  - 내부적으로 1970년 1월 1일 00:00:00 UTC 이후 경과한 시간을 밀리초로 표현  
  - 문자열 형태로 날짜/시간 정보 출력  
- **주요 메서드**:  
  - 기본 생성자 `new Date()` : 현재 시스템의 날짜/시간으로 초기화  
  - `Date(long date)` : 1970년 1월 1일 **UTC** 이후 `date`밀리초만큼 지난 날짜로 초기화  
  - `toString()` : 사람이 읽기 좋은 형태로 날짜/시간 반환  
  - `getTime()` : 내부에 저장된 밀리초(long) 값 반환  
  - `after(Date when)`, `before(Date when)` : 날짜 비교  

#### 💡 `Date` 예시 코드

```java
import java.util.Date;

public class DateExample {
    public static void main(String[] args) {
        // 현재 날짜/시간 객체 생성
        Date now = new Date();
        System.out.println("현재 Date: " + now.toString());

        // 1일(24시간) 전 Date 객체 생성
        long ONE_DAY_MILLIS = 24L * 60 * 60 * 1000;
        Date yesterday = new Date(now.getTime() - ONE_DAY_MILLIS);
        System.out.println("어제 Date: " + yesterday.toString());

        // 밀리초 값 가져오기
        long millis = now.getTime();
        System.out.println("현재 밀리초: " + millis);

        // 날짜 비교
        if (yesterday.before(now)) {
            System.out.println("어제(yesterday) 날짜는 현재(now) 날짜보다 이전입니다.");
        }
    }
}
```


---

### 🗓️ 2) `Calendar` 클래스

- **패키지**: `java.util.Calendar` (추상 클래스)  
- **용도**:  
  - 날짜와 시간 필드(Year, Month, Day, Hour, Minute 등)별로 세부 조작을 쉽게 할 수 있도록 제공  
  - `Date` 보다 편리하게 날짜 연산(더하기/빼기), 필드 조회 등을 수행  
- **주요 메서드 & 특징**:  
  1. **인스턴스 생성**  
     ```java
     // 싱글톤 패턴처럼 getInstance()로 Calendar 객체 얻기
     Calendar cal = Calendar.getInstance();
     ```
     
  2. **날짜 필드 조회 및 설정**  
     - `cal.get(Calendar.YEAR)`, `cal.get(Calendar.MONTH)`  
       - `Calendar.MONTH`는 **0-based** (0: January, 1: February, …, 11: December)  
     - `cal.set(Calendar.DAY_OF_MONTH, 15)` : 일(day) 필드만 변경  
     ```java
     int year = cal.get(Calendar.YEAR);
     int month = cal.get(Calendar.MONTH) + 1; // 0-based → 1월을 1로 표현
     int day = cal.get(Calendar.DAY_OF_MONTH);
     System.out.printf("Today: %d-%02d-%02d", year, month, day);
     ```  
     
  3. **날짜 연산**  
     - `cal.add(Calendar.FIELD, amount)` : 특정 필드에 amount 만큼 더하거나 뺌  
       ```java
       cal.add(Calendar.MONTH, 1); // 한 달 뒤
       cal.add(Calendar.DAY_OF_MONTH, -7); // 7일 전
       ```
       
  4. **`getTime()` & `setTime(Date date)`**  
     - `cal.getTime()` : `Date` 객체로 변환  
     - `cal.setTime(Date date)` : `Date` 객체로부터 Calendar 필드 값 설정  

#### 💡 `Calendar` 예시 코드

```java
import java.util.Calendar;
import java.util.Date;
import java.text.SimpleDateFormat;

public class CalendarExample {
    public static void main(String[] args) {
        // 1) 현재 날짜/시간 Calendar 인스턴스 생성
        Calendar cal = Calendar.getInstance();

        // 2) 필드별 날짜 정보 가져오기
        int year = cal.get(Calendar.YEAR);
        int month = cal.get(Calendar.MONTH) + 1; // 0-based → 1~12
        int day = cal.get(Calendar.DAY_OF_MONTH);
        int hour = cal.get(Calendar.HOUR_OF_DAY);
        int minute = cal.get(Calendar.MINUTE);
        int second = cal.get(Calendar.SECOND);

        System.out.printf("현재: %d-%02d-%02d %02d:%02d:%02d
", 
                          year, month, day, hour, minute, second);

        // 3) 날짜 연산 예제: 한 달 뒤로 설정
        cal.add(Calendar.MONTH, 1);
        System.out.println("한 달 뒤: " + new SimpleDateFormat("yyyy-MM-dd").format(cal.getTime()));

        // 4) 특정 날짜 설정 예제: 2025년 12월 25일 (크리스마스)
        cal.set(2025, Calendar.DECEMBER, 25); 
        Date xmas = cal.getTime();
        System.out.println("크리스마스: " + xmas);  // toString() 이용

        // 5) Date ↔ Calendar 변환
        Date now = new Date();
        cal.setTime(now);
        System.out.println("Date → Calendar → " + 
            cal.get(Calendar.YEAR) + "-" + (cal.get(Calendar.MONTH) + 1) + "-" + cal.get(Calendar.DAY_OF_MONTH));
    }
}
```

