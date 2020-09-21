# WebApp 04

### member_table 만들기

```
create table member_table(
num number constraint member_table_num_pk primary key,
id varchar2(15) constraint member_table_id_nn not null,
pwd varchar2(15) constraint member_table_pwd_nn not null,
name varchar2(34),
tel varchar2(54),
email varchar2(54),
addr varchar2(100),
mpoint number(5),
rdate date,
constraint member_table_id_uq unique(id));

create sequence member_table_seq
increment by 1
start with 1;
```


### urls.py

```py
from django.contrib import admin
from django.urls import path

from oraform import views

urlpatterns = [
    # 주소창에 http://localhost/oraform/main 입력되면 views.py 파일 안의 index 메소드를 읽어라.
    # http://localhost/oraform/main ==> views.index() ==> index.html
    path('main', views.index, name='main'),

    # 주소창에 http://localhost/oraform/tripmember 입력되면 views.py 파일 안의 tripmember 메소드를 읽어라.
    # index.html 에서 '회원가입'을 누르면 tripmember 실행
    path('tripmember', views.tripmember),

    # 주소창에 http://localhost/oraform/tripinsert 입력되면 views.py 파일 안의 tripinsert 메소드를 읽어라.
    # tripmember.html 에서 '가입하기' 버튼이 눌려지면 tripinsert 이 action 됨
    path('tripinsert', views.tripinsert),

    # index.html 에서 '회원리스트' 버튼이 눌려지면 tripmemberlist 실행
    path('tripmemberlist', views.tripmemberlist),

    # tripmember.html 에서 '중복확인' 버튼이 눌리 js 통해 처리됨
    # ajax를 이용하면 비동기식으로 브라우저 이동이 없음.
    path('idchk', views.idchk),
]
```

### views.py
```py
from django.shortcuts import render
from django.views.decorators.csrf import csrf_exempt, csrf_protect

from oraform.models import memberinsert, getMemberData, getIdchkData


def index(request):
    # templates/oraform/index.html 로 이동해라.
    return render(request, "oraform/index.html")


def tripmember(request):
    # templates/oraform/tripmember.html 로 이동해라.
    return render(request, "oraform/tripmember.html")


# 회원가입
@csrf_protect
def tripinsert(request):
    addr = (request.POST['id'], request.POST['pwd'],
            request.POST['name'], request.POST['email'],
            request.POST['tel'], request.POST['addr'])
    print('ID', addr)
    memberinsert(addr)
    return render(request, 'oraform/index.html')


# 회원리스트
def tripmemberlist(request):
    memlist = getMemberData()
    print(type(memlist))
    return render(request, 'oraform/memberlist.html', {'memlist': memlist})


def idchk(request):
    idv = request.GET["id"]
    # print("idv :", idv)
    idcnt = getIdchkData(idv)
    # print("함수 거친뒤 결과값: ", idcnt)
    if 0 in idcnt:
        msg = '사용 가능한 아이디 입니다'
        col = "blue"
    else:
        msg = '이미 사용중인 아이디 입니다'
        col = "red"
    return render(request, 'oraform/idchk.html', {'msg': msg, 'col':col})

```


### models.py
```py
from django.db import models
import cx_Oracle as ora
import pandas as pd

database = 'kosmorpa/test00@192.168.0.68:1521/orcl'

# 메소드 실행 전에 DB에 member_table 테이블이 만들어져 있어야 됨


def memberinsert(addr_list):
    print(addr_list)
    conn = ora.connect(database)
    cursor = conn.cursor()  # Oracle DB 접속한 객체의 주소값 cursor()
    sql = "insert into member_table " \
          "values(member_table_seq.nextVal,:1,:2,:3,:4,:5,:6,0,sysdate)"
    cursor.execute(sql, addr_list)
    cursor.close()
    conn.commit()
    conn.close()


def getMemberData():
    conn = ora.connect(database)
    cursor = conn.cursor()
    sql_select = "select * from member_table order by 1 desc"
    cursor.execute(sql_select)
    datas = cursor.fetchall()
    conn.close()
    return datas


def getIdchkData(idv):
    #print("함수에 들어온 값:", idv)
    conn = ora.connect(database)
    cursor = conn.cursor()
    sql_select = "select count(*) cnt from member_table where id=:id"
    cursor.execute(sql_select, id=idv)
    datas = cursor.fetchone()
    conn.close()
    return datas

```


### index.html
```html
<!DOCTYPE HTML>
{% load static %}
{% static "" as baseUrl %}
<html>
	<head>
		<title>StarTrip</title>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no" />
		<link rel="stylesheet" href="{{baseUrl}}/assets/css/main.css" />
	</head>
	<body class="is-preload">

		<!-- Wrapper -->
			<div id="wrapper">

				<!-- Main -->
					<div id="main">
						<div class="inner">

							<!-- Header -->
								<header id="header">
									<a href="main" class="logo"><strong>StarTrip</strong> &nbsp;&nbsp;&nbsp;Start Your Trip</a>
                           			<a href="login" class="test">로그인 하러 가기</a>
       
								</header>

							<!-- Banner -->
								<section id="banner">
									<div class="content">
										<div class="col-6 col-12-xsmall">

										<!-- {{memlist}} -->
											{% for a in memlist %}
											<div class="col-12 col-12-xsmall">
												<h3 class="object" style="background:gray">
													이름: {{a.3}}
												</h3>
												<!-- {{ myDate|date:'Y-m-a H:i' }} -->
												<table>
													<tr>
														<td>날짜</td>
														<td>{{a.8|date:'Y-m-d H:i'}}</td>
													</tr>
													<tr>
														<td>아이디</td>
														<td>{{a.1}}</td>
													</tr>
													<tr>
														<td>이메일</td>
														<td>{{a.4}}</td>
													</tr>
												</table>
											</div>
											{% endfor %}
										</div>

									</div>
									<span class="image object">
										<img src="{{baseUrl}}/assets/img/main.jpg" alt="" />
									</span>
								</section>

							<!-- Section -->

							<!-- Section -->
								<section>
									<header class="major">
										<h2>SerVice</h2>
									</header>
									<div class="posts">
										<article>
											<a href="#" class="image"><img src="{{baseUrl}}/assets/img/map.jpg" alt="" /></a>
											<h3>주변 검색</h3>
											<p>GPS 기반의 주변의 명소 알아보기!</p>
											<ul class="actions">
												<li><a href="map" class="button">검색 하기</a></li>
											</ul>
										</article>
										<article>
											<a href="reviewmain" class="image"><img src="{{baseUrl}}/assets/img/rev.jpg" alt="" /></a>
											<h3>게시판</h3>
											<p>후기를 남겨 추억을 간직하세요!</p>
											<ul class="actions">
												<li><a href="reviewmain" class="button">작성 하기</a></li>
											</ul>
										</article>
										<article>
											<a href="seoul" class="image"><img src="{{baseUrl}}/assets/img/loc.jpg" alt="" /></a>
											<h3>지역 정보</h3>
											<p>전국의 여행지의 정보를 제공해드립니다!</p>
											<ul class="actions">
												<li><a href="seoul" class="button">More</a></li>
											</ul>
										</article>
									</div>
								</section>

						</div>
					</div>

			 <!-- Sidebar -->
               <div id="sidebar">
                  <div class="inner">
                     <!-- Menu -->
                        <nav id="menu">
                           <header class="major">
                              <h2>Menu</h2>
                           </header>
                           <ul>
                              <li><a href="main">Home</a></li>
                              <li><a href="survey">설문조사</a></li>
                              <li>
                                 <span class="opener">회원가입/로그인</span>
                            <ul>
                            
                             <li><a href="logout">로그아웃</a></li>
                          
							 <li><a href="tripmember">회원가입</a></li>
							 <li><a href="tripmemberlist">회원리스트</a></li>
                             <li><a href="login">로그인</a></li>
									
                                 </ul>
                              </li>

                              <li>
                                 <span class="opener">국내 여행지</span>
                                 <ul>
                                    <li><a href="seoul">서울</a></li>
                                    <li><a href="incheon">인천</a></li>
                                    <li><a href="dajeon">대전</a></li>
                                    <li><a href="dague">대구</a></li>
                                    <li><a href="gwangju">광주</a></li>
                                    <li><a href="busan">부산</a></li>
                                    <li><a href="ulsan">울산</a></li>
                                    <li><a href="sejong">세종</a></li>
                                    <li><a href="gyunggi">경기</a></li>
                                    <li><a href="gangwon">강원</a></li>
                                 </ul>
                              </li>
                              <li><a href="map">주변 검색</a></li>
                              <li>
                                 <span class="opener">게시판</span>
                                 <ul>
                                    <li><a href="reviewmain">후기 게시판</a></li>
                                    <li><a href="reviewwrite">게시글 작성하기</a></li>
                                 </ul>
                              </li>

                           </ul>
                        </nav>

                     <!-- Section -->


                     <!-- Footer -->
                        <footer id="footer"></footer>

                  </div>
               </div>

			</div>

		<!-- Scripts -->
			<script src="{{baseUrl}}/assets/js/jquery.min.js"></script>
			<script src="{{baseUrl}}/assets/js/browser.min.js"></script>
			<script src="{{baseUrl}}/assets/js/breakpoints.min.js"></script>
			<script src="{{baseUrl}}/assets/js/util.js"></script>
			<script src="{{baseUrl}}/assets/js/main.js"></script>

	</body>
</html>
```


### tripmember.html

```html
<!DOCTYPE HTML>
{% load static %}
{% static "" as baseUrl %}
<html>
	<head>
		<title>StarTrip</title>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no" />
		<link rel="stylesheet" href="{{baseUrl}}/assets/css/main.css" />
	</head>
	<body class="is-preload">

		<!-- Wrapper -->
			<div id="wrapper">

				<!-- Main -->
					<div id="main">
						<div class="inner">

							<!-- Header -->
								<header id="header">
									<a href="main" class="logo"><strong>StarTrip</strong> &nbsp;&nbsp;&nbsp;Start Your Trip</a>
                           			<a href="login" class="test">로그인 하러 가기</a>
       
								</header>

							<!-- Banner -->
								<section id="banner">
									<div class="content">
										<!--post방식으로 tripinsert 로 이동-->
										<form method="post" action="tripinsert">
											{% csrf_token %} <!-- 변조 방지 위해. 소스 보기로 하면 암호같은 것으로 바뀌어 있음 -->
											<div class="row gtr-uniform">
												<div class="col-6 col-12-xsmall">
													<input type="text" name="id" id="id" placeholder="ID" />
													<ul class="actions">
														<li><input type="button" value="중복확인" id="idBtn"></li>
														<li><div id="target"></div></li>
													</ul>
												</div>
												<div class="col-6 col-12-xsmall">
													<input type="password" name="pwd" id="pwd" placeholder="비밀번호" />
												</div>
												<div class="col-6 col-12-xsmall">
													<input type="password" name="chkpwd" id="chkpwd" placeholder="비밀번호확인" />
												</div>
												<div class="col-6 col-12-xsmall">
													<input type="text" name="name" id="name" placeholder="이름" />
												</div>
												<div class="col-6 col-12-xsmall">
													<input type="tel" name="tel" id="tel" placeholder="전화번호" />
												</div>
												<div class="col-6 col-12-xsmall">
													<input type="email" name="email" id="email" placeholder="Email" />
												</div>
												<div class="col-6 col-12-xsmall">
													<input type="text" name="addr" id="addr" placeholder="주소" />
												</div>
												<div class="col-12">
													<ul class="actions">
														<li><input type="submit" value="가입하기" class="primary" /></li>
														<li><input type="reset" value="취소하기" /></li>
													</ul>
												</div>
											</div>
										</form>
									</div>
									<span class="image object">
										<img src="{{baseUrl}}/assets/img/main.jpg" alt="" />
									</span>
								</section>

							<!-- Section -->

							<!-- Section -->
								<section>
									<header class="major">
										<h2>SerVice</h2>
									</header>
									<div class="posts">
										<article>
											<a href="#" class="image"><img src="{{baseUrl}}/assets/img/map.jpg" alt="" /></a>
											<h3>주변 검색</h3>
											<p>GPS 기반의 주변의 명소 알아보기!</p>
											<ul class="actions">
												<li><a href="map" class="button">검색 하기</a></li>
											</ul>
										</article>
										<article>
											<a href="reviewmain" class="image"><img src="{{baseUrl}}/assets/img/rev.jpg" alt="" /></a>
											<h3>게시판</h3>
											<p>후기를 남겨 추억을 간직하세요!</p>
											<ul class="actions">
												<li><a href="reviewmain" class="button">작성 하기</a></li>
											</ul>
										</article>
										<article>
											<a href="seoul" class="image"><img src="{{baseUrl}}/assets/img/loc.jpg" alt="" /></a>
											<h3>지역 정보</h3>
											<p>전국의 여행지의 정보를 제공해드립니다!</p>
											<ul class="actions">
												<li><a href="seoul" class="button">More</a></li>
											</ul>
										</article>
									</div>
								</section>

						</div>
					</div>

			 <!-- Sidebar -->
               <div id="sidebar">
                  <div class="inner">
                     <!-- Menu -->
                        <nav id="menu">
                           <header class="major">
                              <h2>Menu</h2>
                           </header>
                           <ul>
                              <li><a href="main">Home</a></li>
                              <li><a href="survey">설문조사</a></li>
                              <li>
                                 <span class="opener">회원가입/로그인</span>
                            <ul>
                            
                             <li><a href="logout">로그아웃</a></li>
                          
							 <li><a href="tripmember">회원가입</a></li>
							 <li><a href="tripmemberlist">회원리스트</a></li>
                             <li><a href="login">로그인</a></li>
									
                                 </ul>
                              </li>

                              <li>
                                 <span class="opener">국내 여행지</span>
                                 <ul>
                                    <li><a href="seoul">서울</a></li>
                                    <li><a href="incheon">인천</a></li>
                                    <li><a href="dajeon">대전</a></li>
                                    <li><a href="dague">대구</a></li>
                                    <li><a href="gwangju">광주</a></li>
                                    <li><a href="busan">부산</a></li>
                                    <li><a href="ulsan">울산</a></li>
                                    <li><a href="sejong">세종</a></li>
                                    <li><a href="gyunggi">경기</a></li>
                                    <li><a href="gangwon">강원</a></li>
                                 </ul>
                              </li>
                              <li><a href="map">주변 검색</a></li>
                              <li>
                                 <span class="opener">게시판</span>
                                 <ul>
                                    <li><a href="reviewmain">후기 게시판</a></li>
                                    <li><a href="reviewwrite">게시글 작성하기</a></li>
                                 </ul>
                              </li>

                           </ul>
                        </nav>

                     <!-- Section -->


                     <!-- Footer -->
                        <footer id="footer"></footer>

                  </div>
               </div>

			</div>

		<!-- Scripts -->
			<script src="{{baseUrl}}/assets/js/jquery.min.js"></script>
			<script src="{{baseUrl}}/assets/js/browser.min.js"></script>
			<script src="{{baseUrl}}/assets/js/breakpoints.min.js"></script>
			<script src="{{baseUrl}}/assets/js/util.js"></script>
			<script src="{{baseUrl}}/assets/js/main.js"></script>

		<script>
			$(function(){
				$('#idBtn').click(function(){
					//alert('idv:'+$('#id').val()); //값이 들어왔는지 확인을 위해 alert 창으로 보여줌
					let idv = $('#id').val();
					//location.href="idchk?id="+idv; // urls.py 통해 idchk.html 로 이동

					// 비동기식 ajax처리하기(=브라우저 이동 없음)
					$.ajax({
						url:"idchk?id="+idv,
						success:function(data){
							console.log("res:"+data)
							$('#target').html(data);
						}
					});
				});
			});
		</script>

	</body>
</html>
```

### memberlist.html

```html
<!DOCTYPE HTML>
{% load static %}
{% static "" as baseUrl %}
<html>
	<head>
		<title>StarTrip</title>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no" />
		<link rel="stylesheet" href="{{baseUrl}}/assets/css/main.css" />
	</head>
	<body class="is-preload">

		<!-- Wrapper -->
			<div id="wrapper">

				<!-- Main -->
					<div id="main">
						<div class="inner">

							<!-- Header -->
								<header id="header">
									<a href="main" class="logo"><strong>StarTrip</strong> &nbsp;&nbsp;&nbsp;Start Your Trip</a>
                           			<a href="login" class="test">로그인 하러 가기</a>
       
								</header>

							<!-- Banner -->
								<section id="banner">
									<div class="content">
										<div class="col-6 col-12-xsmall">

										<!-- {{memlist}} -->
											{% for a in memlist %}
											<div class="col-12 col-12-xsmall">
												<h3 class="object" style="background:gray">
													이름: {{a.3}}
												</h3>
												<!-- {{ myDate|date:'Y-m-a H:i' }} -->
												<table>
													<tr>
														<td>날짜</td>
														<td>{{a.8|date:'Y-m-d H:i'}}</td>
													</tr>
													<tr>
														<td>아이디</td>
														<td>{{a.1}}</td>
													</tr>
													<tr>
														<td>이메일</td>
														<td>{{a.4}}</td>
													</tr>
												</table>
											</div>
											{% endfor %}
										</div>

									</div>
									<span class="image object">
										<img src="{{baseUrl}}/assets/img/main.jpg" alt="" />
									</span>
								</section>

							<!-- Section -->

							<!-- Section -->
								<section>
									<header class="major">
										<h2>SerVice</h2>
									</header>
									<div class="posts">
										<article>
											<a href="#" class="image"><img src="{{baseUrl}}/assets/img/map.jpg" alt="" /></a>
											<h3>주변 검색</h3>
											<p>GPS 기반의 주변의 명소 알아보기!</p>
											<ul class="actions">
												<li><a href="map" class="button">검색 하기</a></li>
											</ul>
										</article>
										<article>
											<a href="reviewmain" class="image"><img src="{{baseUrl}}/assets/img/rev.jpg" alt="" /></a>
											<h3>게시판</h3>
											<p>후기를 남겨 추억을 간직하세요!</p>
											<ul class="actions">
												<li><a href="reviewmain" class="button">작성 하기</a></li>
											</ul>
										</article>
										<article>
											<a href="seoul" class="image"><img src="{{baseUrl}}/assets/img/loc.jpg" alt="" /></a>
											<h3>지역 정보</h3>
											<p>전국의 여행지의 정보를 제공해드립니다!</p>
											<ul class="actions">
												<li><a href="seoul" class="button">More</a></li>
											</ul>
										</article>
									</div>
								</section>

						</div>
					</div>

			 <!-- Sidebar -->
               <div id="sidebar">
                  <div class="inner">
                     <!-- Menu -->
                        <nav id="menu">
                           <header class="major">
                              <h2>Menu</h2>
                           </header>
                           <ul>
                              <li><a href="main">Home</a></li>
                              <li><a href="survey">설문조사</a></li>
                              <li>
                                 <span class="opener">회원가입/로그인</span>
                            <ul>
                            
                             <li><a href="logout">로그아웃</a></li>
                          
							 <li><a href="tripmember">회원가입</a></li>
							 <li><a href="tripmemberlist">회원리스트</a></li>
                             <li><a href="login">로그인</a></li>
									
                                 </ul>
                              </li>

                              <li>
                                 <span class="opener">국내 여행지</span>
                                 <ul>
                                    <li><a href="seoul">서울</a></li>
                                    <li><a href="incheon">인천</a></li>
                                    <li><a href="dajeon">대전</a></li>
                                    <li><a href="dague">대구</a></li>
                                    <li><a href="gwangju">광주</a></li>
                                    <li><a href="busan">부산</a></li>
                                    <li><a href="ulsan">울산</a></li>
                                    <li><a href="sejong">세종</a></li>
                                    <li><a href="gyunggi">경기</a></li>
                                    <li><a href="gangwon">강원</a></li>
                                 </ul>
                              </li>
                              <li><a href="map">주변 검색</a></li>
                              <li>
                                 <span class="opener">게시판</span>
                                 <ul>
                                    <li><a href="reviewmain">후기 게시판</a></li>
                                    <li><a href="reviewwrite">게시글 작성하기</a></li>
                                 </ul>
                              </li>

                           </ul>
                        </nav>

                     <!-- Section -->


                     <!-- Footer -->
                        <footer id="footer"></footer>

                  </div>
               </div>

			</div>

		<!-- Scripts -->
			<script src="{{baseUrl}}/assets/js/jquery.min.js"></script>
			<script src="{{baseUrl}}/assets/js/browser.min.js"></script>
			<script src="{{baseUrl}}/assets/js/breakpoints.min.js"></script>
			<script src="{{baseUrl}}/assets/js/util.js"></script>
			<script src="{{baseUrl}}/assets/js/main.js"></script>

	</body>
</html>
```


### idchk.html

```html
<div style="color:{{col}}">{{msg}}</div>
```