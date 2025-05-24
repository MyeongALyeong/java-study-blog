# 조건문과 반복문 _ Chap 04

<br><br><br><br>
# 🔄 자바 조건문 정복 - if문 & switch문

> 🏷️ Tags: `Java`, `조건문`, `if`, `switch`, `Math.random`, `Week2`

---

## ✨ 학습 키워드
- 조건문 개념 정리
- if문 & switch문 기본 구조 및 차이점
- break 생략의 의미와 활용
- 난수 생성 공식 (Math.random)
- 자바의 기본 반복문 3종류 이해하기
- 반복 제어문 break / continue 사용법 익히기
- 상황별 반복문 선택 기준 알기
- 연습 문제 풀어보기


---

## 🧠 조건문이란?

조건문의 목적은 어떤 "조건"에 따라 프로그램의 흐름을 제어하는 것이다.

---

## 📌 if문

조건식 또는 범위를 비교해서 true/false 결과에 따라 실행 여부를 결정하는 조건문이다.

💬 기본 구조:
```java
if (조건식) {
    // 조건이 true일 때 실행할 문장
} else if (조건식2) {
    // 위 조건이 false이고, 조건식2가 true일 때 실행할 문장
} else {
    // 위 모든 조건이 false일 때 실행할 문장
}
```


---

## 📌 switch문

조건문 중 하나로, 특정 “값”을 기준으로 실행할 코드를 선택한다.

### 💬 기본 구조

```java
switch (변수) {
    case 값1:
        // 실행문
        break;
    case 값2:
        // 실행문
        break;
    default:
        // 위에 해당하지 않을 경우 실행
}
```


### 💡 주의:

- break를 생략하면 해당 case 이후 모든 case가 실행됨 → fall-through 현상
- 의도적으로 break 생략하여 여러 case를 한 번에 처리할 수 있음


---


### ✅ switch문 형태 1

![switch문 형태 1](https://github.com/user-attachments/assets/9a5c5016-5e48-4b0c-b586-90a1818426f5)
- 각 값에 따라 실행문이 개별적으로 존재함       [EX. 메뉴판]

### 💬 switch문 _ 예제 1

```java
int menu = 2;

switch (menu) {
    case 1:
        System.out.println("🍔 햄버거를 선택하셨습니다.");
        break;
    case 2:
        System.out.println("🍕 피자를 선택하셨습니다.");
        break;
    case 3:
        System.out.println("🥗 샐러드를 선택하셨습니다.");
        break;
    default:
        System.out.println("❓ 존재하지 않는 메뉴입니다.");
}
📝 실행 결과:
🍕 피자를 선택하셨습니다.
```


---


### ✅ switch문 형태 2

![switch문 형태 2](https://github.com/user-attachments/assets/5e498f8f-1b00-41ed-9013-a7610d98a5e9)
- 의도적 break 생략
- 해당 값을 기준으로 break를 만날 때까지, 아래 실행문을 모두 실행함
  [EX. 현재 시간 이후 일정 나열]



### 💬 switch문 _ 예제 2

```java

        Scanner sc = new Scanner(System.in);

        System.out.print("지금은 몇 시인가요? (정수로 입력, 예: 8) 👉 ");
        int hour = sc.nextInt();

        System.out.println("\n🗓️ 지금부터의 일정은 다음과 같습니다:");

        switch (hour) {
            case 8:
                System.out.println("8시 - 🚶 출근");
            case 9:
                System.out.println("9시 - 🗂️ 회의 준비");
            case 10:
                System.out.println("10시 - 📢 회의 시작");
            case 11:
                System.out.println("11시 - 🧠 기획안 발표");
            case 12:
                System.out.println("12시 - 🍱 점심 시간");
                break;
            default:
                System.out.println("⚠️ 일정이 없습니다. 또는 유효한 시간을 입력해주세요.");
        }


📝 실행 결과:
지금은 몇 시인가요? (정수로 입력, 예: 8) 👉 9

🗓️ 지금부터의 일정은 다음과 같습니다:
9시 - 🗂️ 회의 준비
10시 - 📢 회의 시작
11시 - 🧠 기획안 발표
12시 - 🍱 점심 시간

```

---



### ✅ switch문 형태 3

![switch문 형태 3](https://github.com/user-attachments/assets/f4d59bcd-89cf-4f63-ba94-37ac1628e885)
- n개의 값에 대해서, 실행문이 동일한 경우
 [EX. 대소문자 구별없이 실행문 도출]


### 💬 switch문 _ 예제 3

```java
char ch = 'Y';

switch (ch) {
    case 'y':
    case 'Y':
        System.out.println("Yes를 선택하셨습니다.");
        break;
    case 'n':
    case 'N':
        System.out.println("No를 선택하셨습니다.");
        break;
    default:
        System.out.println("잘못된 입력입니다.");
}


       


📝 실행 결과:
Yes를 선택하셨습니다.



```



## 📌 난수 정수 만들기

특정 범위에서 정수를 랜덤하게 뽑고 싶을 때 사용하는 공식:

🎲 기본 공식:
```java
int num = (int)(Math.random() * n) + start;

- start: 시작 숫자
- n: 개수 (몇 개 중에서 뽑을지)

```

🎲 예시 _ 10~14 중 난수 :
```java
int num = (int)(Math.random() * 5) + 10;

```



---




# 🔁 자바 반복문 완전정복 - for / while / do-while / break & continue




---

## 📌 자바의 반복문 종류

| 반복문      | 설명                             | 사용 예시                             |
|-------------|----------------------------------|----------------------------------------|
| for문       | 반복 횟수가 정해졌을 때 적합       | 배열, 리스트 순회, 카운팅 루프 등       |
| while문     | 조건이 true인 동안 반복            | 입력이 언제 끝날지 모를 때 등           |
| do-while문  | 일단 한 번은 실행하고 조건 검사    | 최소 한 번은 실행이 보장될 때 사용       |

---

## 📌 for문 기본 구조 

```java
for (int i = 1; i <= 5; i++) {
    System.out.println("i = " + i);
}
```
💡 특징: 반복 횟수를 정확히 아는 경우에 매우 적합!

---

## 📌 while문 기본 구조 

```java
int i = 1;
while (i <= 5) {
    System.out.println("i = " + i);
    i++;
}
```
💡 특징: 반복 횟수가 유동적인 경우, 조건 중심

---

## 📌 do-while문 기본 구조

```java
int i = 1;
do {
    System.out.println("i = " + i);
    i++;
} while (i <= 5);

```
💡 특징: 조건과 상관없이 최소 1번은 실행!

---

## 🚫 break문이란?
- 반복문을 "강제로 중단"하는 역할
- 주로 특정 조건이 만족될 때 반복 종료 시 사용

### 💬 break문 예제
```java
for (int i = 1; i <= 10; i++) {
    if (i == 4) break;
    System.out.println(i);
}

📝 실행 결과:
1
2
3

```

---

## ↪️ continue문이란?
- 이번 반복을 "건너뛰고" 다음 반복으로 넘어감
- 특정 조건에서 실행을 스킵하고 싶을 때 사용

### 💬 continue문 예제
```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) continue;
    System.out.println(i);
}

📝 실행 결과:
1
2
4
5

```

---
## 연습문제

### 📍 4강 연습문제 6번
![연습문제 6번](https://github.com/user-attachments/assets/2e49c2e2-75ca-488b-a169-59a075a4eb08)
- 바깥 반복문 (x): 줄 수 제어 (총 4줄 출력)
- 첫 번째 안쪽 반복문 (z): 공백 출력
- 두 번째 안쪽 반복문 (y): 별 출력

✅ 출력 문자의 시작지점과 끝 지점을 바깥 반복문의 반복 변수인 x와 연결지어서 규칙화하기

---<br><br>

### 📍 4강 연습문제 7번
![연습문제 7번](https://github.com/user-attachments/assets/b556e72d-0487-43d2-b12c-77c09d8a2b51)
![7번 실행 결과](https://github.com/user-attachments/assets/e5fe376a-1862-4826-81f1-d3e09979c6ae)



- 반복문 구조: 반복 횟수가 정해지지 않았기 때문에 while문 사용 -> 무한 반복
- 특정 입력값이 들어오면 switch문을 통해 break 사용하여 while문 종료
- Scanner를 사용해 사용자의 숫자 입력을 받음
- switch문으로 사용자가 입력한 숫자에 따라 서로 다른 코드 실행


