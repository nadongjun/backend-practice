# IoC

## Inversion of Control
- `IOC`란 객체의 생성, 생명 주기 관리까지 모든 객체에 대한 제어권이 컨테이너로 역전된 것
- 컴포넌트 의존관계 형성과 설정, 생명 주기를 해결하기 위한 디자인 패턴
- `IoC 컨테이너`는 스프링 프레임워크에서 제공되고 있으며 객체에 대한 생성 및 생명 주기를 관리할 수 있는 기능이 제공됨
  
```
- IoC 컨테이너는 객체의 생성을 책임지고, 의존성을 관리한다.
- 생성, 초기화, 서비스, 소멸에 대한 권한을 가지며 개발자는 컨테이너에게 맡긴다.
```
## 의존성
[참고](https://kotlinworld.com/64)

`의존성`이란 클래스 간 의존 관계가 있다는 것이고 한 클래스가 바뀔 때 다른 클래스가 영향을 받는 것이다.

`의존성 주입`이란 클래스에 대한 의존성을 인터페이스화(API)하여 코드의 유연성 증가 / 인스턴스를 외부에서 생성하여 주입 하는 것이다.

## Spring bean
[참고](https://melonicedlatte.com/2021/07/11/232800.html)

Spring IoC 컨테이너가 관리하는 자바 객체를 빈(Bean)
- 일반적으로 처음에 배우는 자바 프로그램에서는 각 객체들이 프로그램의 흐름을 결정하고 각 객체를 직접 생성하고 조작(객체를 직접 생성하여 메소드 호출)
- IOC가 적용된 경우, 객체의 생성을 특별한 관리 위임 주체에게 맡김. 이 경우 사용자는 객체를 직접 생성하지 않음
- 기존의 Java Programming 에서는 Class를 생성하고 new를 입력하여 원하는 객체를 직접 생성한 후에 사용.
- 하지만 Spring에서는 직접 new를 이용하여 생성한 객체가 아니라, Spring에 의하여 관리당하는 자바 객체를 사용 
- Spring에 의하여 생성되고 관리되는 자바 객체를 Bean이라고 함 
- Spring Framework 에서는 Spring Bean 을 얻기 위하여 ApplicationContext.getBean() 와 같은 메소드를 사용하여 Spring 에서 직접 자바 객체를 얻어서 사용

### Annotation Example
#### Annotation을 통해 등록
- Java에서는 @Override, @Deprecated 와 같은 기본적인 Annotation을 제공함
- Bean을 등록하기 위해서는 @Component Annotation을 사용. @Component Annotation이 등록되어 있는 경우에는 Spring이 Annotation을 확인하고 자체적으로 Bean 으로 등록됨
```java
/* 1. 코드 내 등록하는 방법 */

//HelloController 객체를 컨트롤러 역할을 수행하는 것을 알림. HTTP 요청 시 매핑 처리에 동작시키기 위한 코드
// HelloController.java
@Controller // 객체 Controller 등록을 위한 Bean 표기
public class HelloController {
    // Http Get method 의 /hello 경로로 요청이 들어올 때 처리할 Method를 아래와 같이 @GetMapping Annotation을 사용하여 Mapping을 사용할 수 있습니다.

    @GetMapping("hello")

    public String hello(Model model){
        model.addAttribute("data", "This is data!!");
        return "hello";
    }
}
```


#### Bean Configuration File에 직접 Bean 등록
- @Configuration과 @Bean Annotation 을 이용하여 Bean을 등록
- @Configuration을 이용하면 Spring Project 에서의 Configuration 역할을 하는 Class를 지정
```java
/* 2. Bean Configuration File에 표기하는 방법 */
// Hello.java
@Configuration
public class HelloConfiguration {
    @Bean
    public HelloController sampleController() {
        return new SampleController;
    }
}
```
## Annotation 분류

1. Component
2. ComponentScan
3. Bean
4. Controller
5. RequestHeader
6. RequestMapping
7. RequestParam
8. RequestBody
9. ModelAttribute
10. ResponseBody
11. Autowired
12. GetMapping
13. PostMapping
14. SpringBootTest
15. Test

- Lombok을 사용한 방법
1. @Setter
2. @Getter
3. @AllArgsConstructor
4. @NoArgsConstructor
5. @ToString


## IoC 분류
[참고](https://webcache.googleusercontent.com/search?q=cache:m8XnkIb-RjsJ:https://dog-developers.tistory.com/12&cd=2&hl=ko&ct=clnk&gl=kr)

### DL (Dependency Lookup)
저장소에 저장되어 있는 `Bean에 접근하기 위해 컨테이너가 제공하는 API`를 이용하여 Bean을 Lookup 하는 것
```
- Setter Injection (Setter 메서드를 통해 의존성 삽입) : 의존성을 입력 받는 setter 메서드를 만들고 이를 통해 의존성을 주입한다.

- Constructor Injection (생성자를 통해 의존성 삽입) : 필요한 의존성을 포함하는 클래스의 생성자를 만들고 이를 통해 의존성을 주입한다.

- Method Injection (일반 메서드를 통해 의존성 삽입) : 의존성을 입력 받는 일반 메서드를 만들고 이를 통해 의존성을 주입한다.
```


### DI (Dependency Injection)
`각 클래스간의 의존관계를 Bean 설정(Bean Definition)` 정보를 바탕으로 컨테이너가 자동으로 연결해주는 것
```
각 클래스간의 의존관계를 개발자가 Bean 설정 (Bean Definition)을 하고 이 정보를 바탕으로 컨테이너가 자동으로 연결.

- 개발 시 Bean Annotation을 추가하여 의존관계가 필요하다는 정보를 추가

- 객체 레퍼런스를 컨테이너로부터 주입 받아서, 실행 시에 동적으로 의존관계가 생성된다.

- 컨테이너가 흐름의 주체가 되어 애플리케이션 코드에 의존관계를 주입해 주는 것이다.
```

이를 통해 코드가 단순해지고 컴포넌트 간 결합도가 없어짐
