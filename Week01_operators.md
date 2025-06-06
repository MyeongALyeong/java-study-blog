# ✨ Java 연산자 정리 _ Chap 03

> 🏷 Tags: `Java`, `연산자`, `산술`, `논리`, `비교`, `삼항`, `대입`

---

## 📚 학습 내용

- 자바의 주요 연산자 종류와 개념 (산술, 비교, 논리, 대입, 삼항 등)
- 연산자의 우선순위와 결합 방향 이해하기
- 문자열 결합 연산에서의 연산 방향 주의점
- 나눗셈과 곱셈을 이용한 자리수 버림 로직 적용하기

<br><br>---


## 🧠 연산자와 연산식

- 연산자: 연산의 종류를 결정짓는 기호
- 피연산자: 연산식에서 사용되는 값

📌 주요 연산자 종류:
- 산술: +, -, *, /, %
- 증감: ++, --
- 비교: ==, !=, <, <=, >, >=
- 논리: &&, ||, !
- 대입: =, +=, -=, *=, /=, ...

---

## ⚙️ 연산자 우선순위

우선순위: 괄호 > 단항 > 산술 > 비교 > 논리 > 대입

| 우선순위 | 연산자 종류                     |
|----------|----------------------------------|
| 🥇 1순위 | (), [], . (괄호, 멤버 접근)       |
| 🥈 2순위 | ++, -- (전위/후위), !, ~          |
| 🥉 3순위 | *, /, %, +, -                    |
| 🔍 중간  | <, <=, >, >=, ==, !=, instanceof |
| 🎯 마지막 | &&, ||, =, +=, -=, ? :           |

---

## 🔹 단항 연산자

### ➕ 부호 연산자

```java
byte a = 50;
int result = -a; // byte → int로 자동 변환
```

📌 byte, short 등의 작은 타입은 연산 시 int로 변환된다.

---

### 🔁 증감 연산자 (++, --)

```java
int x = 10;
int y = 10;
int z;

z = ++x;        // x:11, z:11
z = x++;        // x:12, z:11
z = ++x + y++;  // x:13, y:11, z:13+10 = 23
```

---

### ❗ 논리 부정 연산자 (!)

```java
boolean flag = true;
System.out.println(!flag); // false
```

---

## 🔸 산술 연산자

- 나눗셈: /
- 나머지: %

💡 char 타입 산술 연산:
```java
char c1 = 'A' + 1;           // c1 = 'B'
char c2 = 'A';
char c4 = (char)(c2 + 1);    // c4 = 'B'
```

---

## 🔤 문자열 결합 연산자

```java
String str1 = "JDK" + 6.0;        // "JDK6.0"
String str2 = "JDK" + 3 + 3.0;    // "JDK33.0"
String str3 = 3 + 3.0 + "JDK";    // "6.0JDK"
```

👉 연산 방향은 왼쪽에서 오른쪽.

---

## 🔍 비교 연산자

- 결과는 boolean 타입
- 피연산자가 char인 경우 유니코드로 비교

```java
System.out.println('A' == 65);     // true
System.out.println(3 == 3.0);      // true
System.out.println(0.1f == 0.1);   // false
System.out.println(0.1f == (float)0.1); // true
```

📌 문자열 비교는 equals() 사용!
```java
String str1 = "신용권";
String str2 = "신용권";
System.out.println(str1.equals(str2));  // true
```

---

## 🔗 논리 연산자

- &&: 앞 조건이 false이면 뒤는 확인하지 않음
- &: 앞 뒤 모두 확인
- ||, |도 동일한 차이 존재

---

## 📝 대입 연산자

👉 오른쪽에서 왼쪽 방향으로 연산됨

| 복합 연산자 | 의미             |
|--------------|------------------|
| a += 5       | a = a + 5        |
| a -= 3       | a = a - 3        |
| a *= 2       | a = a * 2        |
| a /= 4       | a = a / 4        |
| a %= 3       | a = a % 3        |

---

## 🎯 삼항 연산자

형식:
```java
조건식 ? 참일 때 : 거짓일 때;
```

```java
int score = 95;
char grade = (score >= 90) ? 'A' : 'B';
```

📌 C언어는 출력문에서도 사용 가능하지만, Java는 변수에 저장해서 쓰는 방식이 일반적이다.

---<br><br>


## 연습문제 
---
### chap 03_2 6번 문제
<십의 자리 이하를 버리는 코드>
![연습문제 6번](https://github.com/user-attachments/assets/ae95c989-ce10-4d33-bd01-bfcf42f1003d)

#### 🧩 동작 흐름
① result = value / 100
- 📉 백의 자리 이하를 버리고, 백 단위 값만 남김
- 예: 356 / 100 → 3

② result = value / 100 * 100
- 📐 다시 100을 곱해서, 버림된 뒷자리를 0으로 채움
-  예: 3 × 100 → 300

  #### 🧠 포인트 정리
  | 연산 방식 | 의미                          | 설명                              |
|-----------|-------------------------------|-----------------------------------|
| ➗ 나눗셈  | 자리 정보만 추출              | 원하는 자릿수 기준으로 잘라내기    |
| ✖️ 곱셈   | 자리수를 다시 맞추기 (보정)    | 뒷자리를 0으로 정렬하는 효과       |


