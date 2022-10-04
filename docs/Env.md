# Env
## VSCODE 개발환경 설정

1. Spring Boot Extension Pack 설치
2. JDK 11 설정
3. 
```sh
brew tap adoptopenjdk/openjdk 
brew install adoptopenjdk11 --cask
/usr/libexec/java_home -V
java -version
```
4. Perferences -> Setting -> jdk -> Java:Home Edit in Settings.json 에서 설치된 JDK 경로 설정
- "java.home": "/Library/Java/JavaVirtualMachines/adoptopenjdk-11.jdk/Contents/Home"

## 프로젝트 생성