# Spring Layer 구조

- VO(Bean, DTO) - DB테이블 구조를 가져옴(정보 전달을 위해서) = Django의 Model
- DAO - DB관련작업 처리(CRUD) = Django의 Model
- Service - 서비스 로직
- Controller - 클라이언트와 교류 = Django의 views + urls

### mybatis
- DB관련 작업들을 자바로 쉽게 처리하기 위해 만들어진 패키지

xml 파일에 sql문 정의


dispatch-servlet.xml
bean : 재사용이 가능한 컴퍼넌트


![1) Spring 전체적인 실행 순서_1](https://user-images.githubusercontent.com/34564706/97377184-bdceae80-1902-11eb-9e83-0ede20aa351f.jpg)
![2) Spring 전체적인 실행 순서_2](https://user-images.githubusercontent.com/34564706/97377190-c0c99f00-1902-11eb-8dc5-48c3d6ba2179.jpg)

1. Spring MVC 5 - 이클립스 설치 및 개발환경 구축

   https://www.youtube.com/watch?v=obsT2decMdc

2. Spring MVC 5 - MVC의 기본 개념

   https://www.youtube.com/watch?v=M3HMpOVx7yA

3. Spring MVC5 - 프로젝트 셋팅
  (Maven Configure - Convert to Maven Project 실행 적용 가능함)

   https://www.youtube.com/watch?v=cEsTd7dwkro