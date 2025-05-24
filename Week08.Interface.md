# 🧠 Java - 인터페이스 & 다형성

## 📘 08-1. 인터페이스
- 클래스가 구현해야 할 메서드의 이름과 시그니처(매개변수, 반환형)만 선언한 일종의 "계약서"
- interface 키워드로 정의하며, 내부에 선언된 메서드는 모두 추상 메서드(public abstract)
- 다중 상속의 문제를 해결하기 위해 클래스가 여러 인터페이스를 구현할 수 있음
- 상수(constant)를 정의할 때는 public static final 형태로 선언


### 🎯 인터페이스 선언

```java
// Drawable.java
public interface Drawable {
    /** 도형을 그리는 동작을 정의 */
    void draw();
}
```

<br>
<br>

### ✏️ 인터페이스 구현
- implements 키워드 뒤에 인터페이스 이름을 나열
- 인터페이스에 선언된 모든 추상 메서드를 오버라이드(재정의)해야 함
- 클래스 내부에서 인터페이스를 구현하면, 그 클래스는 “Drawable을 구현하는 Circle”이 되어 draw() 메서드를 사용할 수 있음

```java
// Circle.java
public class Circle implements Drawable {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public void draw() {
        System.out.println("🔵 반지름 " + radius + "인 원을 그립니다.");
    }
    
    public double getRadius() {
        return radius;
    }
}
```
<br>
<br>

### ✏️ 인터페이스 사용
```java
// Main.java
public class Main {
    public static void main(String[] args) {
        Drawable shape = new Circle(3.5);  // 인터페이스 타입으로 업캐스팅
        shape.draw();                     // 🔵 반지름 3.5인 원을 그립니다.
    }
}
```
[업캐스팅]
- Circle 객체를 Drawable 타입 변수에 할당
- 컴파일 시점에는 shape가 Drawable이라는 공통 인터페이스만 알지만, 실행 시점에는 실제 Circle의 draw()가 호출
- 구현체를 바꾸면 코드를 전혀 수정하지 않고 다양한 도형을 동일하게 처리 가능

<br>
<br>

---
## 🧬 08-2. 타입 변환과 다형성

### 🔄 자동 타입 변환 (Upcasting)

```java
Drawable d = new Circle(2.0);  // Circle → Drawable (업캐스팅)
```
자동 형변환(업케스팅)
- 자식 클래스(Circle) 타입을 부모 인터페이스(Drawable) 타입으로 변환
- 명시적 캐스팅 없이 컴파일러가 자동으로 처리
- 다형성의 핵심: 구체 구현체에 관계없이 인터페이스를 통해 통일된 방식으로 접근

<br>
<br>

### 🧪 필드의 다형성

```java

// Painter.java
public class Painter {
    private Drawable tool;      // 어떤 Drawable이든 담을 수 있는 필드

    public Painter(Drawable tool) {
        this.tool = tool;
    }

    public void paint() {
        tool.draw();
    }
}

// 사용 예
Painter p = new Painter(new Circle(1.5));
p.paint();  // 🔵 반지름 1.5인 원을 그립니다.
```
- 클래스 내부의 멤버 변수로 인터페이스 타입을 선언
- 생성자나 세터(setter)를 통해 다양한 구현체(Circle, Rectangle, Triangle 등)를 주입 가능
- Painter 클래스는 구체 타입에 무관하게 모든 Drawable을 다룰 수 있음

---

### 🔁 매개 변수의 다형성

```java
// Renderer.java
public class Renderer {
    public void render(Drawable d) {
        d.draw();
    }
}

// 사용 예
Renderer r = new Renderer();
r.render(new Circle(4.0));  // 🔵 반지름 4.0인 원을 그립니다.
```
- 메서드 파라미터를 인터페이스 타입으로 선언
- 어떤 구현체 객체를 전달하더라도 일관된 인터페이스 메서드(draw()) 호출로 처리
- 새로운 도형 클래스가 추가되어도 render() 메서드는 그대로 재사용 가능

---

### 📌 강제 타입 변환(Downcasting)


```java
Drawable d = new Circle(5.0);
if (d instanceof Circle) {
    Circle c = (Circle) d;      // 다운캐스팅
    System.out.println("반지름: " + c.getRadius());
}
```

- 인터페이스 타입 변수(Drawable)를 구체 클래스(Circle) 타입으로 변환
- 인터페이스에는 없는 고유 메서드(getRadius())를 사용하기 위해 필요
- 잘못된 타입으로 캐스팅 시 ClassCastException 발생하므로, instanceof로 타입 검사 후 안전하게 수행

---

### 🧐 객체 타입 확인 (instanceof)


```java
if (d instanceof Circle) {
    System.out.println("이 객체는 Circle입니다.");
} else {
    System.out.println("Circle이 아닙니다.");
}
```
[instanceof 연산자]
- 런타임에 실제 객체가 특정 클래스나 인터페이스를 구현했는지 검사
- 다운캐스팅 전 사전 체크로 사용
- Boolean 값을 반환

---
#### (1) instanceof 예제
![image](https://github.com/user-attachments/assets/e34399a0-db1e-4f28-b78d-c3f1ea1d69cb)

---

#### (2) interface 예제
![image](https://github.com/user-attachments/assets/eb082666-f4be-4580-b365-63ebb592e864)
