 # 클래스(2)_ Chap 06-4 ~ 06-6

<br><br><br><br>
# 🔄 자바 클래스 정복

> 🏷️ Tags: `Java`, `클래스`, `메소드`, `인스턴스`, `패키지`, `접근제한자`, `week04`

---

## ✨ 학습 키워드
- 메소드 오버로딩
- 인스턴스 멤버와 정적 멤버의 차이점
- 싱글톤
- 패키지 선언
- 접근 제한자 4종류
- Getter와 Setter 메소드
- 연습 문제 풀어보기


---
<br><br><br><br>
# Chap 06-4 : 메서드

## 📘 자바 메서드의 구성 요소

---

### (1) 리턴 타입 (Return Type)

메서드가 실행된 후 **되돌려주는 값의 자료형**을 의미합니다.

- 리턴값이 없을 경우에는 `void` 사용
- 리턴값의 유무에 따라 메서드 호출 방식이 달라집니다.

**리턴값이 없는 경우:**
```java
printMessage();  // 단순 호출
```

**리턴값이 있는 경우:**
```java
int result = add(3, 5);        // 변수에 저장
System.out.println(add(3, 5)); // 출력문 안에서 사용
```

---

### (2) 메서드 이름

- 숫자로 시작할 수 없습니다.
- `$`와 `_`을 제외한 특수문자는 사용할 수 없습니다.
- 보통 의미 있는 동사 형태의 이름을 사용하며 camelCase로 작성합니다.

예시:
```java
void calculateTotal() { }
int getAge() { return 25; }
```

---

### (3) 매개변수 선언

메서드가 실행될 때 **외부로부터 필요한 데이터를 전달받기 위해** 사용합니다.

- 필요한 경우에만 선언합니다.
- 괄호 안에 `자료형 변수명` 형태로 작성합니다.
- 메서드를 호출할 때는 **타입과 개수를 맞춰서** 값을 전달해야 합니다.

예시:
```java
void greet(String name) {
    System.out.println("Hello, " + name);
}
```

메서드 호출:
```java
greet("Alice");  // 올바른 호출
```

---

### (4) 메서드 실행 블록

메서드가 실제로 수행할 **기능을 작성하는 영역**입니다.

- 중괄호 `{}`로 감싸서 작성합니다.
- 조건문, 반복문, 다른 메서드 호출 등이 들어갈 수 있습니다.


---
<br><br><br><br>

## 📘 메서드에서 매개 변수의 개수를 모를 경우

### (1) 방법1: 메서드의 매개변수를 '배열 타입'으로 선언하기

- 메서드를 호출하기 전에 배열 생성하기
- 메서드 호출 시, 입력값으로 배열 넣어주기
  
### (2) 방법2: 가변 인자 사용해서 값의 목록만 넘겨주기

- 메서드 선언시 가변인자 사용하기
- 메서드 호출 시, 입력값으로 배열 넣어주기

#### 활용 문제

![image](https://github.com/user-attachments/assets/ff126c55-29aa-49c5-a57a-088bc3e1b24f)

- 메인함수에서 메서드 사용 전에, 객체 생성해주기
- 메서드 호출 시에도, 객체 사용해서 호출할 것

---
<br><br><br><br>

## 📘 메서드 오버로딩
- 클래스 내에 같은 이름의 메소드를 여러 개 선언하는 것.
- 매개 변수의 타입, 개수, 순서 중 하나를 달리하여, 이에 따라 다른 메소드를 실행시킴

  #### 활용 문제
  
  ![image](https://github.com/user-attachments/assets/ff157f48-fd63-4ee7-84c1-a93a2db874ab)

- 매개변수 개수로 메서드 구별하여 호출됨

---
<br><br><br><br>
# Chap 06-5 : 인스턴스 멤버와 정적 멤버

## 📘 클래스 멤버
- 인스턴스 멤버와 정적 멤버로 구성됨
- 인스턴스 멤버: 객체마다 가지고 있는 멤버 (객체 생성 후 사용 가능한 필드와 메소드)
- 정적 멤버: 객체들이 공유하는 멤버 (동일한 값을 공유)

---
<br><br><br><br>

## 📘 this. vs this()

### (1) this.

- 필드를 호출하기 위해서 사용함
- 클래스 내부, 생성자와 메소드에서 모두 사용 가능


### (2) this()

- 같은 클래스의 다른 생성자 호출함
- 생성자 코드의 제일 첫 줄에 위치해야함
- 생성자 내부에서만 사용 가능 (메소드에서는 사용 불가)

#### 활용 문제

![image](https://github.com/user-attachments/assets/851395cf-ea6e-4e56-ad0f-e97e95d4a138)

---
<br><br><br><br>

## 📘 정적 멤버 선언

방법) 필드와 메소드 선언 시 static 키워드 붙여주기

![image](https://github.com/user-attachments/assets/8d2b4144-a6ed-484c-9bf7-2feb1e7e5384)

  <인스턴스 필드 vs 정적 필드>
- 객체마다 가지고 있어야 할 데이터 -> 인스턴스 필드로 선언
- 객체마다 가지고 있을 필요가 없는 공용 데이터 -> 정적 필드 선언
<br>

 <인스턴스 메소드 vs 정적 메소드>
- 인스턴스 필드를 포함하고 있다면 -> 인스턴스 메소드 선언
- 인스턴스 필드를 포함하고 있지 않다면 -> 정적 메소드 선언
  (정적 메소드이더라도, 매개 변수를 통해서 외부 값은 사용 가능함.)

#### 예시 코드

![image](https://github.com/user-attachments/assets/4fca13f3-cf2d-43f0-889f-50b09ef96bbb)

---
<br><br><br><br>

## 📘 메인함수에서 _ 정적 멤버 사용

객체를 생성할 필요 없이, 클래스를 이용해서 바로 사용 가능함

```java
// 클래스의 정적 필드 접근
ClassName.staticField;

// 클래스의 정적 메서드 호출
ClassName.staticMethod(arguments);
```

## 🔍 인스턴스 멤버 vs 정적 멤버 비교표

| 구분             | 🧱 인스턴스 멤버                         | ⚙️ 정적 멤버 (static)                    |
|------------------|------------------------------------------|------------------------------------------|
| 🔗 접근 방식      | 객체명.멤버                              | 클래스명.멤버                            |
| 🛠️ 사용을 위해   | 객체 생성 필요                           | 객체 생성 없이 사용 가능                 |
| 📦 메모리 할당    | 객체가 생성될 때마다 할당됨              | 클래스 로딩 시 1번만 할당됨              |
| 🧪 메인 메서드에서 사용 예 | `MyClass obj = new MyClass();`<br>`obj.instanceMethod();` | `MyClass.staticMethod();`                |
| 🧬 공통 데이터 공유 | ❌ 불가능 (객체마다 값이 다를 수 있음)     | ✅ 가능 (공통값 유지)                     |

---

📌 **Tip**:  
- `static` 키워드가 붙은 필드나 메서드는 클래스 수준에서 공유됨.  
- 대표적인 예: `Math`, `System.out`, `Integer.parseInt()` 등  


---
<br><br><br><br>

## 📘 정적 메소드 선언 시 주의할 점

--

### 🚫 `this` 키워드 사용 불가능

- `this`는 **현재 객체를 참조**하는 키워드인데,  
  정적 메서드는 **객체와 무관하게 클래스 단에서 호출**되기 때문에 사용할 수 없음

```java
public class Example {
    int instanceVar = 10;

    public static void staticMethod() {
        // System.out.println(this.instanceVar); ❌ 오류 발생
    }
}
```

---

### 🔒 인스턴스 멤버 접근 불가

정적 메서드는 클래스에 소속되기 때문에,  
**인스턴스 변수나 인스턴스 메서드를 직접 사용할 수 없음**

> ✅ 해결 방법: 객체를 생성한 후 접근해야 함!

```java
public class Example {
    int instanceVar = 42;

    public static void staticMethod() {
        // System.out.println(instanceVar); ❌ 오류 발생

        // 객체 생성 후 접근해야 함
        Example obj = new Example();
        System.out.println(obj.instanceVar); ✅
    }
}
```

---

📌 **요약**
- 정적 메서드에서는 `this` 키워드 ❌
- 인스턴스 멤버 사용 시, 반드시 객체 생성 후 접근해야 함 ✅
- 자주 쓰이는 예: `main` 메서드, `Math.random()`, `System.out.println()` 등

---
<br><br><br><br>

## 🧍‍♂️ 싱글톤 (Singleton)

- 프로그램 전체에서 **단 하나의 객체**만 생성되는 디자인 패턴

---

### 🛠️ 싱글톤 만드는 방법

```java
public class Singleton {
    // 1. private 생성자
    private Singleton() {}

    // 2. private static 객체 생성
    private static Singleton instance = new Singleton();

    // 3. public static 메서드로 객체 반환
    public static Singleton getInstance() {
        return instance;
    }
}
```

```java
// 4. 외부에서 사용하는 방법
Singleton obj1 = Singleton.getInstance();
Singleton obj2 = Singleton.getInstance();

// 같은 객체를 참조함
System.out.println(obj1 == obj2); // true
```

> ☑️ `new Singleton()` 으로는 더 이상 객체를 생성할 수 없음!  
> 반드시 `정적 메서드`를 통해 접근해야 함.

---
<br><br><br><br>

## 🔒 final 필드

- 한 번 초기화되면 **값을 변경할 수 없는 필드**

```java
public class Person {
    final int age = 20; // 방법 1: 선언 시 초기화

    final String name;
    public Person(String name) {  // 방법 2: 생성자에서 초기화
        this.name = name;
    }
}
```

---

<br><br><br><br>
## 📌 상수 (`static final`)

- 변하지 않는 값을 **공통으로** 사용하고 싶을 때 사용합니다.

```java
public class Constants {
    public static final double PI = 3.14159;
}
```

```java
System.out.println(Constants.PI); // 객체 없이 사용 가능
```

> ✅ `상수`는 클래스 단위로 메모리에 할당되며,  
> 객체마다 따로 저장되지 않음.

---

<br><br><br><br>

## 📊 final 필드 vs 상수 비교표

| 구분           | 🔒 final 필드                     | 📌 상수 (`static final`)        |
|----------------|-----------------------------------|---------------------------------|
| 저장 위치      | 객체마다 따로 저장               | 클래스 단위로 한 번만 저장     |
| 초기화 방법    | 생성자 통해 각기 다르게 가능     | 한 번만 초기화, 값 변경 불가   |
| 사용 방식      | 객체를 통해 접근                 | 클래스명.상수명 으로 접근      |
| 공유 여부      | ❌ 개별 객체마다 값 다를 수 있음 | ✅ 모든 객체가 동일한 값 공유   |


---
<br><br><br><br>
# Chap 06-6 : 패키지와 접근 제한자

## 📦 패키지란?

- 클래스를 체계적으로 관리하기 위해 패키지를 사용
- 클래스 이름이 같더라도 패키지가 다르면 서로 다른 클래스로 인식

> 예:  
> `com.company.project.MyClass` → 상위패키지.하위패키지.클래스

---

<br><br><br><br>
## 🏷️ 패키지 선언

클래스를 작성할 때, 해당 클래스가 속한 패키지를 명시

```java
package com.company.project;

public class MyClass {
    // ...
}
```

### 📌 패키지 이름 작성 규칙
- 숫자로 시작할 수 없음
- `_`, `$`를 제외한 특수문자 사용 불가
- `java`로 시작하는 이름 사용 금지
- 일반적으로 소문자 사용이 관례

---

<br><br><br><br>
## 📥 import 문

다른 패키지에 있는 클래스나 인터페이스를 사용할 경우 `import` 문을 사용

```java
import com.company.project.MyClass;
import com.company.project.*; // 전체 클래스 가져오기
```

- 작성 위치: 패키지 선언 다음, 클래스 선언 이전
- 객체 생성 시, `클래스명 + new 연산자`로 사용 가능

---

<br><br><br><br>
## 🔐 접근 제한자

클래스, 생성자, 필드, 메서드 등에 접근을 제어하는 키워드

| 제한자     | 설명                                                |
|------------|-----------------------------------------------------|
| `public`   | 외부 클래스 어디서든 접근 가능                      |
| `protected`| 같은 패키지 + 자식 클래스에서 접근 가능             |
| `private`  | 해당 클래스 내부에서만 접근 가능                    |
| (default)  | 같은 패키지 내에서만 접근 가능 (접근제한자 생략 시) |

> 선언 위치: 클래스/메소드/필드 선언의 맨 앞

---

<br><br><br><br>
## 🧩 필드 & 메소드의 접근 제한

- 클래스 내부에서 사용할 경우 접근 제한자의 영향을 받지 않음
- `private` 필드라도 같은 클래스 내부에서는 사용 가능

---

<br><br><br><br>
## 🔄 Getter와 Setter 메소드

`private` 필드에 외부에서 안전하게 접근하기 위해 사용

```java
public class Person {
    private String name;

    // Getter
    public String getName() {
        return name;
    }

    // Setter
    public void setName(String name) {
        this.name = name;
    }
}
```

- 외부에서는 필드 직접 접근 ❌
- `get`/`set` 메서드를 통해 안전하게 접근 ✅

  <br><br><br><br>
  ## chap 06 주요 연습문제
  
  ![image](https://github.com/user-attachments/assets/f3fbdbad-20cb-4eab-b11e-6055251265a3)
