# Spring Layer 구조

- VO(Bean, DTO) - DB테이블 구조를 가져옴(정보 전달을 위해서) = Django의 Model
- DAO - DB관련작업 처리(CRUD) = Django의 Model
- Service - 서비스 로직
- Controller - 클라이언트와 교류 = Django의 views + urls

### mybatis
- DB관련 작업들을 자바로 쉽게 처리하기 위해 만들어진 패키지

xml 파일에 sql문 정의