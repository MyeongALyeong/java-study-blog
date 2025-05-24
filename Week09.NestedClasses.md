# Chap 09. 중첩 클래스와 중첩 인터페이스 🔗



---

## 🏷️ 09-1 중첩 클래스와 중첩 인터페이스 소개

### 1) 🏗️ 중첩 클래스 (Nested Classes)
**정의**: 클래스 내부에 선언된 클래스

**장점**:
- 📌 **캡슐화 강화**: 외부에 불필요한 클래스를 숨겨 코드 복잡도 감소
- 📌 **접근성 향상**: 외부 클래스의 멤버에 쉽게 접근 가능

#### 🔍 종류

1. **멤버 클래스 (Member Classes)**
   - 🔹 **인스턴스 멤버 클래스**  
     ```java
     class Outer {
         class Inner {
             void hello() { System.out.println("📢 Hello from Inner"); }
         }
     }

     public class Main {
         public static void main(String[] args) {
             Outer outer = new Outer();
             Outer.Inner inner = outer.new Inner();
             inner.hello(); // 📢 Hello from Inner
         }
     }
     ```

   - 🔹 **정적 멤버 클래스 (Static Nested Classes)**  
     ```java
     class Outer {
         static class StaticNested {
             static void greet() { System.out.println("🚀 Hello from StaticNested"); }
         }
     }

     public class Main {
         public static void main(String[] args) {
             Outer.StaticNested.greet(); // 🚀 Hello from StaticNested
         }
     }
     ```
<br>

#### 총정리

![image](https://github.com/user-attachments/assets/38e18d0f-edc2-4191-9377-9ec380419338)


---
<br>

2. **로컬 클래스 (Local Classes)**
   - 📝 메소드나 생성자 내부에 선언
   - 🚫 `static`·접근제한자 사용 불가
   - ⏱️ 메소드 실행 시점에만 유효
     ```java
     public class LocalExample {
         void doSomething() {
             class Local {
                 void show() { System.out.println("👀 Local class"); }
             }
             Local local = new Local();
             local.show(); // 👀 Local class
         }
     }
     ```

---

### 2) 🔒 중첩 클래스의 접근 제한
- ▶️ **인스턴스 멤버 클래스**
  - 인스턴스 컨텍스트에서만 `outer.new Inner()`로 생성 가능
  - 정적 컨텍스트(정적 메소드/필드)에서는 직접 생성 불가

- ▶️ **정적 멤버 클래스**
  - 정적/인스턴스 컨텍스트 모두에서 `Outer.StaticNested`로 바로 접근 가능

<br>

![image](https://github.com/user-attachments/assets/69463991-fbbb-4792-a937-f1daebf57e34)


<br>

---

### 3) 🧩 중첩 인터페이스 (Nested Interfaces)
**정의**: 클래스 내부에 선언된 인터페이스

- 🔹 **인스턴스 멤버 인터페이스**  
  ```java
  class Outer {
      interface InnerInterface {
          void execute();
      }
  }
  ```
  - 외부에서 `Outer.InnerInterface` 타입으로 참조하려면 `new Outer()` 인스턴스가 필요

- 🔹 **정적 멤버 인터페이스**  
  (자바 인터페이스는 기본적으로 `static`)
  ```java
  class Outer {
      static interface InnerStaticInterface {
          void execute();
      }
  }

  class Impl implements Outer.InnerStaticInterface {
      @Override
      public void execute() {
          System.out.println("✅ Executing InnerStaticInterface");
      }
  }
  ```
<br>

![image](https://github.com/user-attachments/assets/e97a5b97-940a-411f-a88d-0483f54b5c9b)


<br>

---

## 🎭 09-2 익명 객체 (Anonymous Objects)
익명 객체는 **클래스 이름 없이** 즉시 인스턴스를 생성할 때 사용. 
주로 이벤트 핸들러나 콜백, 일회성 구현에 유용.

### 1) 🔑 개념 및 장점
- **익명 자식 객체 생성**: 기존 클래스(또는 인터페이스)를 상속(구현)하면서 즉시 오버라이드
- **장점**:
  - ✂️ 간결한 코드 작성
  - 🔄 일회성 구현을 한 곳에 묶어 유지보수 용이

---

### 2) 🛠️ 익명 자식 객체 생성 (Anonymous Subclass)
```java
class Parent {
    void greet() { System.out.println("👋 Hello from Parent"); }
}

public class Main {
    public static void main(String[] args) {
        Parent p = new Parent() {
            @Override
            void greet() {
                System.out.println("🎉 Hello from Anonymous Subclass");
            }
        };
        p.greet(); // 🎉 Hello from Anonymous Subclass
    }
}
```

---

### 3) ⚙️ 익명 구현 객체 생성 (Anonymous Implementation)
```java
interface Task {
    void execute();
}

public class Main {
    public static void main(String[] args) {
        Task t = new Task() {
            @Override
            public void execute() {
                System.out.println("🏃 Anonymous Task execution");
            }
        };
        t.execute(); // 🏃 Anonymous Task execution
    }
}
```

---

### 4) 📇 익명 객체와 로컬 변수 사용
- 익명 클래스 내부에서 참조할 수 있는 로컬 변수는 **final** 또는 **effectively final** 이어야 함.

```java
public class Main {
    public static void main(String[] args) {
        final String message = "📝 Hello, effectively final in Java 8+";
        Runnable r = new Runnable() {
            @Override
            public void run() {
                System.out.println(message);
            }
        };
        r.run(); // 📝 Hello, effectively final in Java 8+
    }
}
```

---

> 💡 **Tip**: 람다 표현식으로 익명 구현을 더 간결하게 작성 가능.
> ```java
> Runnable r = () -> System.out.println(message);
> ```

---
<br>

#### 연습문제 풀이
###### 09-1 연습문제 03번

![image](https://github.com/user-attachments/assets/7ff26c6b-7428-41a4-977d-44dd3c262f43)
