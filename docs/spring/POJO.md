# POJO

- POJO(Plain Old Java Object)란 다른 클래스, 인터페이스의 상속을 받아 메서드가 추가된 것이 아닌 getter / setter 같이 기본적인 기능만 가진 자바 객체

- 트랜잭션, 보안 등 로우레벨의 로직까지 작성해야하는 부담감을 없애고자 EJB(Enterprise Java Beans)를 만들게 되었으며 이를 통해 구현이 간편해졌다. 하지만 몇가지 기능을 사용하기 위해 거대한 EJB를 상속받거나 implements 하게 되어 객체가 무거워지며 다른 기능으로 대체하기 위해선 전체 코드를 수정해야 하는 문제점이 발생한다.
- 이를 해결하기 위해 특정 클래스나 라이브러리에 종속되지 않는 코드를 작성한다.
- Spring은 POJO 방식을 기반으로 한 웹 프레임워크이며 IoC와 DI, AOP 등 Spring의 주요 기술을 활용해 Bean에 주입하여 POJO 기반의 구성

## Example
```java
// POJO를 사용하지 않은 경우 전체를 상속받음
public class ExampleListener implements MessageListener {

  public void onMessage(Message message) {
    if (message instanceof TextMessage) {
      try {
        System.out.println(((TextMessage) message).getText());
      }
      catch (JMSException ex) {
        throw new RuntimeException(ex);
      }
    }
    else {
      throw new IllegalArgumentException("Message must be of type TextMessage");
    }
  }

}
```
```java
// POJO를 기반으로 한 경우 상속받지 않고 어노테이션을 통해 객체를 주입받는다.
//이를 통해 상속해야할 클래스와의 결합도가 낮아져 유지 보수가 유용하다.
@Component
public class ExampleListener {

  @JmsListener(destination = "myDestination")
  public void processOrder(String message) {
    System.out.println(message);
  }
}
```