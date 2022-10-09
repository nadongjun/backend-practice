# Structure
[참고](https://velog.io/@jakeseo_me/%EC%8A%A4%ED%94%84%EB%A7%81%EA%B3%BC-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-%EB%AC%B4%EC%97%87%EC%9D%B4-%EB%8B%A4%EB%A5%BC%EA%B9%8C)
## 특징
```
- 톰캣 서버(WAS)가 내장되고 여러 라이브러리가 존재하는 애플리케이션 프레임워크, Client <-> WAS(Web Server+ Web Container) 구조 기본 내장
- 동적인 웹 사이트 개발하기 위한 여러 가지 서비스를 제공함
- SQL 인젝션, XSS(cross-site scripting), CSRF(cross-site request forgery), 클릭재킹(clickjacking)과 같은 보안 공격을 기본으로 막아줌
```

### 용어 정리

`Spring Framework` 란 애플리케이션 프레임워크이며 `IOC 컨테이너`이다.

핵심 기능은 모든 자바 애플리케이션에 사용될 수 있지만 Enterprise Edition 플랫폼 위에서 웹 애플리케이션 빌드하기 위한 확장 기능이 많다.

## Spring boot 구조
Client -> Controller -> Service -> Repository -> Domain -> Database

### Domain
- DB 테이블과 직접 맵핑되는 클래스로서 JPA 사용 시 어노테이션을 이용하여 테이블, 필드, 등을 설정한다.

### Repository
- repository는 DB에 접근하는 소스코드를 모아둔 Interface

### DTO (Data Transfer Object)
- DTO는 해당 테이블에서 실제로 CRUD를 할 필드를 정의해둔 것
- 테이블에 대한 정보를 작성하는 Domain 클래스와 DB에 접근하는 필드에 관한 내용을 작성하는 DTO 클래스를 사용

### Service
- `Repository / DTO`를 통해 DB에 접근하여 CRUD의 각각의 프로세스 관리와 예외처리 

### Controller 
- Http 요청과 응답을 위한 클래스
