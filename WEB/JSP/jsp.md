# HTML(Hypertext Markup Language) 탄생과 발전

- 미군이 명령을 전달키 위해 만든 표준. 극악의 통신 상황에서도 명령서(=text) 를 전달키 위해 만듬
- Hyper 한 Text 즉, text가 hyper(증강)된.
- Markup Mark(v)를 up - 글자 크기를 키우고 색깔 입히고. 신문사의 조판사들이 글자크기,색깔을 지정할 때 쓰던 방식이 markup 이다.

<img src="https://user-images.githubusercontent.com/34564706/89022625-474efe80-d35d-11ea-95af-fb979209d1b5.jpg" width=300></img>
<img src="https://user-images.githubusercontent.com/34564706/89022718-6d749e80-d35d-11ea-8b80-dc04d1e9c789.jpg" width=300></img>

<img src="https://user-images.githubusercontent.com/34564706/89022874-a876d200-d35d-11ea-910d-c0e8923ba841.png" width=300></img>


- 군대의 명령 전달을 위해 전세계에 망을 깔기 위해 노력했으나 비용이 너무 많이 들어서 민간이 망을 깔게 하기 위해 html 을 민간에게 무료료 풀었음.
- 하지만 군이 최소한의 연결 보장성을 갖기 위해 ip 주소를 관리. 그래서 ip 주소는 미국만 관리하고 있다.
- http(Hypertext Transfer Protocol) Hypertext인 html을 전달하기 위한 규약(protocol). 원래는 Hypertext 아닌것(한글 등) 은 금지됐었음. 한글등을 전달키 위해 액티브액스 사용.
- port : 정보가 나가는 구멍
- https 보안
- 아파치, IIS(마이크로소프트), NGINX(러시아) : 서버에서 요청된 html을 보내주기 위한 프로그램

## java기반의 웹 서비스
> servelet -> jsp -> spring -> IBATIS -> MyBatis

### servelet
통신상의 html 를 직접 보내지 않고 컴파일해서 보내는 것. sun이 기득권 지키기 위해. 하지만 컴파일 하기 때문에 느리고 그래서 도태됨.

## MS 의 웹 서비스
- IIS, c#, ASP, MS-SQL

애자일방법 : 성능이 바로바로 빨리 나오면 되지 체계가 무슨 소용이냐


아래가 있는지 확인

![image](https://user-images.githubusercontent.com/34564706/88609052-2321c200-d0be-11ea-9da9-a09c807f755e.png)


![image](https://user-images.githubusercontent.com/34564706/88609423-08038200-d0bf-11ea-86b9-c604f26aa926.png)


![image](https://user-images.githubusercontent.com/34564706/88609402-fb7f2980-d0be-11ea-93fe-e24aea370a1e.png)



# 동적
> 로딩이 모두 다 끝난 다음에 동작시키는

# Users, Customers, Clients
Users
사용자 (사람)
Customers
多 대 多 (마트를 생각)
이건 비지니스적인, 일반적인 용어. 
Clients
1 대 1 (변호사-고객, 의사-환자 관계 생각)
컴퓨터에서는 모두 클라이언트. 클라이언트가 요청한 a에 대해 서버가 a를 주니까. a를 요청한 클라이언트에 대해 서버가 a,b,c,d,e,f,g를 한꺼번에 다 주지는 않기 때문

# 서버




# JavaScript
- 브라우저 안에서 뭔가 동작들을 할 때마다 서버에 요청하면 너무 낭비니까 클라이언트단에서 처리키 위해

# JSP
- 반복 코드를 줄이기 위해 사용

# 라이브러리
서가. 여러가지 책이 꽂혀있는

# 프레임워크
서가의 섹션. 특정된 책들만 모여있는 종교섹션, 외국어섹션같이 특정된 주제의 기능이 모여있는 라이브러리


- index.jsp
```jsp
<%
String st = "hello jsp";
%>

<!-- 아래에 있는 위치에 있는 파일의 내용을 여기로 가져와 -->
<%@include file="inc/class1.jsp" %>
```
- class1.jsp
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%=st %>
```

![image](https://user-images.githubusercontent.com/34564706/88753261-b8908500-d196-11ea-9983-edfd24dba4df.png)



```jsp
<!-- html 사이에 삽입할 때 사용 -->    
<%=st %>

<!-- 여러줄 프로그램을 작동시킬 때 -->
<%
out.print(st);
%>

<%!
// 선언만 할 수 있음. 
int a=3;

// 아래처럼 실행하려고 하는건 안돼
// out.print("Hello");
%>

```

# 서버 개요
**핵심은 html을 받고싶다!!**

고객이 요청한 html을 주기 위한 삽질들이 서버측 기술들

![KakaoTalk_20200731_185114361](https://user-images.githubusercontent.com/34564706/89023755-0ce66100-d35f-11ea-8a06-64a6d52d3ac4.jpg)





##
###

<img src="" width=200></img>
<img src="" width=200></img>

