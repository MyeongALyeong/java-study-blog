# 📘 변수와 타입 _ Chap 02

> 🏷️ Tags: `Java`, `변수`, `기본타입`, `타입변환`, `입출력`, `Week1`

---
## ✅ 학습 내용

- 변수 선언 규칙 기억하기
- 기본 타입 8개 구분 가능하기
- 자동/강제 타입 변환 흐름 이해
- 문자열 포함 연산 주의사항 숙지
- println vs printf 차이 알기

<br><br>---


## 🔤 02-1 변수

### ✅ (1) 변수 이름 작성 규칙
- 사용할 수 있음: 문자, 숫자, $, _
- 첫 글자에는 숫자 ❌
- 예약어 및 공백 ❌

### ✅ (2) 변수 사용 범위 (스코프)
- 변수는 선언된 블록 내부에서만 사용 가능
- 블록 외부에서 접근 시 오류 발생

### ✅ (3) 기본 타입
자바의 기본 타입은 총 8개로 구성됨:
- 정수 타입 (5개): byte, char, short, int, long
- 실수 타입 (2개): float, double
- 논리 타입 (1개): boolean

❌ String은 기본 타입이 아니다! (참조 타입)

---

### 🚨 기본 타입 사용 시 주의사항

1️⃣ long 타입: 큰 수 사용 시 숫자 뒤에 L 또는 l 붙이기
```java
long num = 2147483648L; // L 필수
```

2️⃣ char 타입
- 문자 1개만 저장 가능
- 작은 따옴표(' ') 사용
- 유니코드를 저장하는 정수 타입으로 취급되기도 함

📌 char → int 자동 변환 예시:
```java
char c = 'A';
int code = c;
System.out.println(code); // 출력: 65
```

3️⃣ float 타입: 실수 리터럴 뒤에 F (또는 f) 붙이기
```java
float pi = 3.14F;
```

---

## 🔁 02-3 타입 변환

### ✅ (1) 자동 타입 변환
- 작은 타입 → 큰 타입으로 자동 변환

| 변환 순서 | byte < short < int < long < float < double |

---

### ✅ (2) 정수 연산에서의 자동 타입 변환 주의사항

- byte, short → 연산 시 자동으로 int로 변환됨
- 서로 다른 타입 연산 시 → 더 큰 타입으로 자동 변환

```java
byte a = 10;
byte b = 20;
int result = a + b; // 반드시 int로 받아야 함
```

📌 long + int → int가 long으로 자동 변환됨

📌 문자열 포함 시 전체가 문자열로 변환됨
```java
System.out.println(3 + "7");    // "37"
System.out.println("10" + 2 + 8); // "1028"
System.out.println("10" + (2 + 8)); // "1010"
```

---

### ✅ (3) 강제 타입 변환 (Casting)
- 큰 범위 → 작은 범위로 변환 시 명시적 형변환 필요

```java
double a = 1.9;
int b = (int) a; // 출력: 1 (소수점 버림)
```

---

### ✅ (4) 문자열 → 기본 타입 변환
```java
String str = "10";
int num = Integer.parseInt(str);
double d = Double.parseDouble("3.14");
```

---

### ✅ (5) 기본 타입 → 문자열 변환
```java
int score = 100;
String str = String.valueOf(score);
```

---

## 🖨️ 02-4 변수와 시스템 입출력

### 📌 print vs println vs printf

| 메소드  | 설명                               |
|----------|------------------------------------|
| print   | 줄바꿈 없이 출력                     |
| println | 출력 후 자동 줄바꿈                 |
| printf  | 형식 지정자를 사용해 포맷 출력 가능 |

```java
System.out.print("hello");       // hello
System.out.println("world");     // hello↵world
System.out.printf("%d + %d = %d", 3, 5, 8); // 3 + 5 = 8
```

---

## 💡 추가 예시: 타입 변환 퀴즈

문제: 다음 코드의 출력 결과는?
```java
System.out.println("10" + 2 + 3);
System.out.println(2 + 3 + "10");
```

정답:
```
1023
510
```
설명: 문자열이 앞에 오면 이후도 문자열로 처리됨. 숫자끼리 먼저 연산되면 숫자 연산 후 문자열 결합.

---
