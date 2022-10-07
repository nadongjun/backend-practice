# Env
## VSCODE 개발환경 설정

1. Spring Boot Extension Pack 설치
2. JDK 11 설정
   
```sh
brew tap adoptopenjdk/openjdk 
brew install adoptopenjdk11 --cask
/usr/libexec/java_home -V
java -version
```
1. Perferences -> Setting -> jdk -> Java:Home Edit in Settings.json 에서 설치된 JDK 경로 설정
- "java.home": "/Library/Java/JavaVirtualMachines/adoptopenjdk-11.jdk/Contents/Home"

## 프로젝트 생성

### Spring Initializr 
1. [Spring Initializr](https://start.spring.io/) Dependencies 추가, Generate 후 zip 파일 생성

### VSCODE

1. cmd + shift + p
2. Spring Initializr, Maven 프로젝트 선택
3. 버전 선택
4. 언어 / Group / Artifact ID
5. Dependencises 추가 
   
#### Dependencises
- Spring Boot DevTools : 빠른 앱 재실행 지원, 개발 지원
- Spring Web : 웹 개발을 위함, 톰캣 서버가 내장되어 있음
- Lombok : 좀 더 편리한 어노테이션 라이브러리
- MySQL Driver, MyBatis Framework : MySQL 연결을 위한 MySQL JDBC와 MyBatis

[생성된 프로젝트](../practice/HELP.md)