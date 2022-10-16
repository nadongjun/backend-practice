# AOP 
Aspect Oriented Programming


[참고](https://velog.io/@underlier12/Spring-18-AOP-%EB%9E%80)

[참고](https://velog.io/@to9251/Spring-AOP)
```
관점 지향 프로그래밍(횡단 관심사)

중복 코드 분리

메서드의 시작 또는 끝에 자동(동적)으로 부가기능(advice) 추가 
```
- AOP란 흩어진 Aspect들을 모아서 모듈화하는 기법
- 서로 다른 클래스라도 비슷한 기능을 하는 부분이 있는데 이것을 Concern이라고 함
- 만약 서로 다른 클래스의 유사한 기능을 수정하려면 각각의 클래스의 모든 기능(함수)을 수정해야 함
- 이 문제를 해결하기 위한 것이 AOP

## 용어
- Concern(관심사) : 서로 다른 클래스의 비슷한 기능 (Advice, Target으로 구분)
  - Advice : 기능 (부가 기능), target에 동적으로 추가될 부가 기능(코드)
  - Target : 클래스 (핵심 기능), advice 가 추가될 객체
- Aspect : 유사한 흩어진 기능을 모은 것
- Pointcut : 어디에 적용해야 하는 지 (A라는 클래스의 B 메서드)
- Join point : 메서드를 실행하는 지점

## 적용 방법
```
Class A에 Perf라는 메서드가 있고, Hello라는 Aspect가 있고, Class A의 Perf메서드가 실행 되기 전에 항상 Hello를 출력해야한다고 가정
```
- Spring에서는 런타임에서 적용된다.
```
A라는 Bean(Class A를 뜻함)을 만들 때(spring 어플리케이션에서 Bean을 만드는 과정은 런타임이다.), A라는 타입의 프록시 Bean을 만든다.

이 프록시 Bean이 실제 A가 가지고 있는 Perf라는 메서드를 호출하기 직전에 Hello를 출력하는 일을 하고, 그 다음에 A를 호출한다.
```
```
아래 3가지의 기준으로 코드들은 분리된다.

1. Concern가 무엇인지 (중복되는 것 : Advice, 중복되지 않는/동적으로 변하는 것 : Target)

2. 변하지 않는 것(COMMON), 변하는 것(UNCOMMON)

3. 공통 코드인지.
```

## 예시
### 적용되지 않은 경우
```java
class Aop {
    void aaa() {
        System.out.println("[before]{"); 
        System.out.println("aaa() is called."); 
        System.out.println("}[after]"); 
    }

    void aaa2() {
        System.out.println("[before]{");
        System.out.println("aaa2 is called.");
        System.out.println("}[after]"); 
    }

    void bbb() {
        System.out.println("[before]{");
        System.out.println("bbb is called.");
        System.out.println("}[after]");
    }

    public static void main(String[] args) {
        Aop aop = new Aop();
        aop.aaa();
        System.out.println();
        aop.aaa2();
        System.out.println();
        aop.bbb();
    }
}
```

### 분류 예시
```java

//관심사
//Target : 핵심기능
//Advice : 부가기능

 void aaa() {
        System.out.println("[before]{");  // 변하지 않는 것, 공통코드, 관심사 Advice
        System.out.println("aaa() is called."); // 변하는 것, 관심사 Target
        System.out.println("}[after]"); // 변하지 않는 것, 공통코드, 관심사 Advice
    }
```

### AOP 적용
AOP 를 적용해서 Target에 대한 클래스, Advice에 대한 클래스를 각각 생성하여 분리한다.
#### Target Class
```java
class MyClass {
    void aaa() {
        System.out.println("aaa is called");
    }
    void  aaa2() {
        System.out.println("aaa2 is called");
    }
    void bbb() {
        System.out.println("bbb is called");
    }
}
```
#### Advice Class
```java
class MyAdvice {
    void invoke(Method m, Object obj, Object... args) throws Exception {
        System.out.println("[before]{"); // 변하지 않는 것, 공통코드, 관심사 Advice
        m.invoke(obj, args); // aaa(), aaa2(), bbb() 호출
        System.out.println("}[after]"); // 변하지 않는 것, 공통코드, 관심사 Advice
    }
}
```
#### 실행
Target에 대한 클래스만 수정해주면 되는 장점을 가지고 있다
```java
public static void main(String[] args) throws Exception {
        MyAdvice myAdvice = new MyAdvice();

        Class myClass = Class.forName("com.fastcampus.ch3.aop.MyClass");
        Object obj = myClass.newInstance();
        /**
         * 1. Class myClass = Class.forName("aop.MyClass"); : Class myClass : MyClass 타입의 참조변수 생성
         * 2. myClass.newInstance() : 생성된 MyClass 타입의 참조변수를 인스턴스화 시켜 "객체 생성"
         * 3. Object obj = myClass.newInstance(); : 생성된 myClass 객체 -> Object 타입의 obj 변수에 할당
         */

        for(Method m : myClass.getDeclaredMethods()){
            /**
             * for(대입 받을 변수 명 : 배열명)
             * myClass.getDeclaredMethods() : Myclass 클래스의 메서드 배열 {aaa(), aaa2(), bbb()}
             * Method m 에 차례대로 배열 메서드가 저장됨
             */
            myAdvice.invoke(m, obj, null);
        }
    }
}
```