# 📘 Chapter 06: 클래스와 객체

<br>

## 🔹 06-1 객체 지향 프로그래밍

### ✅ 객체란?

- 객체는 **속성(필드)**과 **동작(메소드)**으로 구성됨

- 객체 간에는 **메소드를 통해 상호작용**함

<br>

### ✅ 객체 간의 관계

| 관계 종류 | 설명 | 예시 |
|-----------|------|------|

| 집합 관계 | 객체가 부품처럼 포함되는 관계 | 자동차 - 엔진, 타이어 |

| 사용 관계 | 객체가 다른 객체를 사용하는 관계 | 사람 - 자동차 |

| 상속 관계 | 부모 객체를 기반으로 자식 객체 생성 | 부모 클래스 - 자식 클래스 |

<br>

### ✅ 클래스와 객체

- 클래스: 객체를 만들기 위한 **설계도**

- 객체: 클래스로부터 생성된 **인스턴스**

- 하나의 클래스로 여러 객체 생성 가능

<br>

### ✅ 클래스 선언 규칙

- 클래스 이름은 대문자로 시작 (CamelCase)

- 식별자 규칙을 따름 (숫자로 시작 ❌, 특수문자 ❌, 공백 ❌)

- 한 소스 파일에 하나의 public 클래스 권장

<br>

📌 **public 접근 제한자**

- 소스 파일명과 동일한 클래스에만 `public` 사용 가능

<br>

### ✅ 클래스 구성 멤버

- 필드: 객체의 데이터, 상태 정보

- 생성자: 객체 초기화

- 메소드: 객체의 동작

<br>

### ✅ 객체 생성 예시

```java
Car myCar = new Car();
```

<br>

## 🔹 06-2 필드 (Field)

### ✅ 필드란?

- 객체의 **고유 데이터**, **부품 객체**, **상태 정보** 저장

<br>

### ✅ 필드 선언 방법

```java
타입 필드명 = 초기값;
```

- 클래스 블록 내 어디서든 선언 가능

- 생성자/메소드 내부에서는 ❌ (로컬 변수)

<br>

📌 **타입별 기본 초기값**

| 타입 | 기본값 |
|------|--------|

| int | 0 |

| double | 0.0 |

| boolean | false |

| String (참조형) | null |

<br>

### ✅ 필드 사용 방법

- **클래스 내부**: 단순히 이름으로 접근

- **클래스 외부**: 객체 생성 후 `.` 연산자 사용

```java
Car myCar = new Car();
myCar.speed = 60;
```

<br>

## 🔹 06-3 생성자 (Constructor)

### ✅ 생성자란?

- 객체 생성 시 **초기화**를 담당하는 특수한 블록

- 클래스와 **이름 동일**, **리턴타입 없음**

```java
class Car {
  Car() {
    // 생성자 코드
  }
}
```

<br>

### ✅ 기본 생성자

- 매개변수 없는 생성자

- 클래스가 `public`이면 생성자도 `public`

```java
public class Car {
  public Car() {
    // 기본 생성자
  }
}
```

<br>

### ✅ 명시적 생성자 사용 예시

```java
class Car {
  String model;
  Car(String m) {
    model = m;
  }
}

Car myCar = new Car("Sonata");
```

<br>

### ✅ this 키워드 사용 예시

```java
class Car {
  String model;
  Car(String model) {
    this.model = model;
  }
}
```

<br>

### ✅ 생성자 오버로딩

- 생성자 여러 개 정의 (매개변수 타입/수/순서 다르게)

```java
class Car {
  Car() {}
  Car(String model) {}
  Car(String model, int year) {}
}
```

<br>

### ✅ 생성자 간 호출 - `this()`

```java
class Car {
  String model;
  int year;

  Car(String model) {
    this(model, 2025); // 다른 생성자 호출
  }

  Car(String model, int year) {
    this.model = model;
    this.year = year;
  }
}
```

<br>
