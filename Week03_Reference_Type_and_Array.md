# 📘 Chapter 05: 참조 타입과 배열

<br>

## 🔹 05-1 참조 타입과 참조 변수

### ✅ 기본 타입과 참조 타입

- **기본 타입**: 실제 값을 변수 안에 저장

- **참조 타입**: 메모리 주소(번지)를 변수 안에 저장

<br>

### ✅ 메모리 사용 영역

| 영역 | 설명 |
|------|------|

| 메소드 영역 | 클래스의 메소드 코드, static 변수 저장 |

| 힙(Heap) 영역 | 객체와 배열이 생성되는 공간 |

| JVM 스택 영역 | 메소드 호출 시 프레임 추가/제거, 지역 변수 저장 |

<br>

**스택에 저장되는 값의 차이**

- 기본 타입 변수: 리터럴 값이 그대로 저장

- 참조 타입 변수: 객체의 주소가 저장됨

<br>

### ✅ 문자열 비교

- `==`, `!=` : 참조 주소 비교

- `.equals()` : 내부 문자열 내용 비교

```java
String str1 = "hello";
String str2 = new String("hello");
System.out.println(str1 == str2);       // false
System.out.println(str1.equals(str2));  // true
```

<br>

### ✅ 참조 타입의 초기값

- 참조 타입 변수는 `null`로 초기화 가능

```java
String name = null;
```

<br>

## 🔹 05-2 배열 (Array)

### ✅ 배열이란?

- 같은 타입의 데이터를 **연속된 공간**에 나열한 구조

- 각 요소는 **인덱스(0부터 시작)**로 구분

- 생성된 배열의 **길이는 변경 불가능**

- 배열 원소를 출력할 땐 **반복문 사용**

<br>

📌 **자바·C의 배열 vs 파이썬의 리스트 비교**

| 특징 | Java/C 배열 | Python 리스트 |

|------|-------------|----------------|

| 타입 고정 | ✅ 예 | ❌ 아니오 |

| 크기 변경 | ❌ 불가 | ✅ 가능 |

| 자료형 혼합 | ❌ 불가 | ✅ 가능 |

<br>

### ✅ 배열 선언 방법

```java
// 방법 1
int[] numbers;

// 방법 2
int numbers[];
```

<br>

### ✅ 배열 생성 방법

- **값 목록 이용**

```java
String[] names = {"신용권", "홍길동", "김자바"};
```
![예시1](https://github.com/user-attachments/assets/1f5981e8-2404-4810-82bf-21b8ea74cb3d)


- **new 연산자 이용**

```java
int[] scores = new int[5]; // 0으로 초기화됨
```


⚠️ 이미 선언한 배열 변수는 값 목록만으로 재초기화할 수 없으며, `new 타입[]{...}` 형식을 써야 함


```java
int[] scores;
scores = new int[]{90, 80, 70};
```

<br>
#### 🔸 배열을 매개변수로 받는 메소드 사용법

<br>

##### ✅ 메소드 선언
매개변수에는 배열 선언 방법과 동일하게 적어주기
메소드 호출하면서, 배열 값 넣을 떄 new 연산자 이용해서 넣어주기 !!

![image](https://github.com/user-attachments/assets/f104cb00-b3f8-4a40-8930-fc1343f4e5b4)




<br>

### ✅ 배열 길이 및 값 접근

```java
int[] arr = new int[3];
System.out.println(arr.length); // 배열 길이
arr[0] = 10; // 특정 인덱스에 값 저장
```

<br>

### ✅ 배열 vs 문자열의 length 차이

```java
int[] arr = {1, 2, 3};
System.out.println(arr.length); // 배열: 속성

String text = "hello";
System.out.println(text.length()); // 문자열: 메서드
```

<br>

### ✅ 다차원 배열

```java
int[][] matrix = new int[2][3];
```

📊 시각적 구조

```
scores →
         ┌────────────┐
scores[0] → [0][0] [0][1] [0][2]
scores[1] → [1][0] [1][1] [1][2]
         └────────────┘
```

<br>

📌 **비정방형 배열 (Jagged Array)**

```java
int[][] jagged = new int[2][];
jagged[0] = new int[2];
jagged[1] = new int[3];
```

✔️ 각 행마다 다른 열 길이 가능

<br>

### ✅ 다차원 배열 값 목록 초기화

```java
int[][] matrix = {
  {1, 2, 3},
  {4, 5, 6}
};
```

<br>

### ✅ 배열 복사

- **방법 1: for문 이용**

```java
int[] arr1 = {1, 2, 3};
int[] arr2 = new int[arr1.length];
for (int i = 0; i < arr1.length; i++) {
  arr2[i] = arr1[i];
}
```

- **방법 2: System.arraycopy() 이용**

```java
System.arraycopy(arr1, 0, arr2, 0, arr1.length);
```

<br>

### ✅ 향상된 for문 (Enhanced for loop)

```java
for (int score : scores) {
  System.out.println(score);
}
```

<br>

## 🔹 05-3 열거 타입 (Enum)

### ✅ 열거 타입이란?

- 열거 타입은 **한정된 값만 가질 수 있는 자료형**

- 예: 요일, 계절 등

```java
public enum Week {
  MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}
```

<br>

📌 열거 타입 사용 예시

```java
Week today = Week.FRIDAY;
System.out.println(today);
```

<br>

### ✅ 열거 타입 변수는 참조 타입이므로 `null` 저장 가능

```java
Week birthday = null;
```

<br>

### ✅ Calendar 클래스와 열거 타입 연동 예시

```java
import java.util.Calendar;

Week today = null;
Calendar cal = Calendar.getInstance();
int week = cal.get(Calendar.DAY_OF_WEEK);

switch (week) {
  case 1: today = Week.SUNDAY; break;
  case 2: today = Week.MONDAY; break;
  case 3: today = Week.TUESDAY; break;
  case 4: today = Week.WEDNESDAY; break;
  case 5: today = Week.THURSDAY; break;
  case 6: today = Week.FRIDAY; break;
  case 7: today = Week.SATURDAY; break;
}
System.out.println("오늘 요일: " + today);
```

<br>

## 5강 연습 문제

#### 05_2 4번
![image](https://github.com/user-attachments/assets/6da90079-8f6c-4347-a00b-0abad8cdc643)

1. 초기값 설정 주의
int max = 0; 으로 설정하면,
👉 배열에 음수만 있는 경우 올바른 결과가 나오지 않음!
🔧 해결: int max = Integer.MIN_VALUE;로 설정하는 게 안전함.

2. 반복문 범위
i < array.length
👉 배열 인덱스 초과하지 않도록 항상 .length 활용!

3. continue는 생략 가능
if 조건이 false일 때 아무것도 안 하면 continue 없어도 됨.
코드 간결화 가능!


#### 05_2 5번 문제
![image](https://github.com/user-attachments/assets/6bdc81cb-734b-4e2b-a1f3-a4a4b644e287)
