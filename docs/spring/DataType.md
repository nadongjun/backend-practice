# DataType

## DAO
- DAO(Data Access Object)
- 데이터베이스의 data에 접근하기 위한 객체
  
## DTO
- DTO(Data Transfer Object) 
- 계층 간 데이터 교환을 하기 위해 사용하는 객체 (getter, setter만 가짐)
### Example
- 유저가 입력한 데이터를 DB에 넣는 과정
1. 유저가 자신의 브라우저에서 데이터를 입력하여 form에 있는 데이터를 DTO에 넣어서 전송
2. 해당 DTO를 받은 서버가 DAO를 이용하여 데이터베이스로 데이터를 입력하여 저장.
   
## VO
- VO(Value Object)
- `read-Only`, Getter만 있다.

