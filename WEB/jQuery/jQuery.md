# jQuery는 로딩되지 않은 요소는 선택할 수 없다!!

<br>

# 제이쿼리란?
> 자바스크립트를 이용해 만든 라이브러리 언어. <br>
> 라이브러리언어란 자바스크립트로 만들어진 다양한 함수들의 집합


### 제이쿼리 라이브러리 연동방법
- 다운로드 방식
  - 단점 : 업데이트 안 된다
```js
<script src="javascript/jquery-1.12.3.js"></script>
```
- 네트워크 전송 방식(CDN, Content Delivery Network)
  - 단점 : 인터넷이 안 될때 문제
  - 버전에 따라 동작 유무가 변할 수 있기 때문에 다운로드 방식을 추천
```js
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
```

종류|설명
:---:|:---:
jquery.js|개발용 uncompressed 버전. 배포할 때 사용 지양.
jquery.min.js| 배포용 minified 버전. 파일 크기 최소화 위해 압축


## 06-2 선택자
> 선택자는 HTML 요소를 선택하여 가져온다<br>
> CSS 선택자와 마찬가지로 선택한 요소의 디자인 속성을 적용할 때 사용할 수 있다

### 선택자 사용하기
> 1. 선택한 요소에 지정한 스타일을 적용<br>
> $("CSS 선택자").css("스타일 속성명", "값");

> 2. 선택한 요소에 지정한 속성을 적용<br>
> $("CSS선택자".attr("속성명", "값"));

### 직접 선택자

종류|사용법|설명
|---|---|---
전체선택자|`$("*")`|모든 요소를 선택
아이디 선택자|`$("#아이디명")`|id 속성에 지정한 값을 가진 요소를 선택
클래스 선택자|`$(".클래스명")`|class 속성에 지정한 값을 가진 요소를 선택

- 전체 선택자
> `$("*")`
```html
<script>
	$(function(){
		$("*").css("border","1px solid blue");
	});
</script>
```
```html
<body>
	<h1>제이쿼리</h1>
	<h2>선택자</h2>
	<h3>직접 선택자</h3>
</body>
```
![image](https://user-images.githubusercontent.com/34564706/88382840-47db1880-cde4-11ea-8329-c085150fbbb4.png)

<br></br>
- 아이디 선택자
> `$("#아이디명")`
```html
<script>
	$(function(){
		$("#tit").css("background-color","red")
		.css("border", "2px solid blue");
	});
</script>
```
```html
<body>
	<h1>제이쿼리</h1>
	<h2 id="tit">선택자</h2>
	<h3>직접 선택자</h3>
</body>
```
![image](https://user-images.githubusercontent.com/34564706/88383658-e451ea80-cde5-11ea-99f0-61718516ba9c.png)



<br></br>
- 클래스 선택자
> `$(".클래스명")`
```html
<script>
	$(function(){
		$(".tit").css("background-color","red")
		.css("border", "2px dashed blue");
	});
</script>
```
```html
<body>
	<h1>제이쿼리</h1>
	<h2 class="tit">선택자</h2>
	<h3>직접 선택자</h3>
</body>
```
![image](https://user-images.githubusercontent.com/34564706/88383884-5aeee800-cde6-11ea-8822-c0fdade339e3.png)


<br></br>

### 인접관계 선택자
![사본 -KakaoTalk_20200724_194934249](https://user-images.githubusercontent.com/34564706/88384203-ed8f8700-cde6-11ea-847d-5b92f2660fd5.jpg)


종류|사용법|설명
|---|---|---
자식 요소 선택자|`$("요소선택>자식요소)`|선택한 요소를 기준으로 자식 관계에 지정한 요소만 선택
||`$(요소선택).children("자식요소선택")`||
||`$(요소선택).children`||
이전 요소 선택자|`$("요소선택").prev()`|선택한 요소의 바로 이전 요소를 선택
다음 요소 선택자|`$("요소선택").next()`|선택한 요소의 다음 요소를 선택
||`$("요소선택+다음요소")`||


<br></br>
- 자식 요소 선택자
> `$("요소선택>자식요소)`
```html
<script>
	$(function(){
		$("#wrap > h1").css("border","2px dashed red");

		$("#wrap > section").children( )
		.css({ 
			"background-color":"yellow",
			"border":"2px solid blue"
		});
	});
</script>
```
```html
<body>
	<div id="wrap">
		<h1>인접 관계 선택자</h1>
		<p>내용1</p>
		<section>
			<h1>자식 요소 선택자</h1>
			<p>내용2</p>
		</section>
	</div>
</body>
```
![image](https://user-images.githubusercontent.com/34564706/88384480-70184680-cde7-11ea-979a-72681bcea840.png)



<br></br>
- 이전 요소 선택자
> `$("요소선택").prev()`

- 다음 요소 선택자
> `$("요소선택").next()`

```html
<script>
	$(function(){
		var style_1 = {
			"background-color":"green",
			"border":"2px solid red"
		}
		var style_2 = {
			"background-color":"yellow",
			"border":"2px dashed blue"
		}

		$(".txt").prev()
		.css(style_1);

		$(".txt + p").css(style_2);

		$(".txt").next().next()
		.css(style_2);   
	});
</script>
```
```html
<body>
	<div id="wrap">
		<h1>인접 관계 선택자</h1>
		<p>내용1</p>
		<p class="txt">내용2</p>
		<p>내용3</p>
		<p>내용4</p>
	</div>
</body>
```
![image](https://user-images.githubusercontent.com/34564706/88385403-3b0cf380-cde9-11ea-8482-0b8e67e437f6.png)


<br></br>

### 요소에 스타일을 적용하는 두 가지 방법
> 인자값을 사용해 CSS속성과 값을 전달하는 방식<br>
> `$("요소선택").css("속성명1", "값1").css("속성명2", "값2");`

> 객체를 사용해 CSS 속성과 값을 전달하는 방식<br>
> `$("요소선택").css({"속성명1" : "값1", "속성명2" : "값2" ..., "속성명n" : "값n"});`
```js
<script>
  $(function(){
  	$("#wrap > h1").css("border", "2px dashed #f00");
  	$("#wrap > section").children().css({
  		"background-color":"yellow", "border":"2px solid #f00"
  	});
  });
</script>
```




### 그룹 선택자
```js
<script>
  $(function(){
    $("h1, #tit3").css("background-color", "#ff0").css("border", "2px solid #f00");
  });
</script>

<body>
	<h1>제이쿼리</h1>
	<h2>선택자</h2>
	<h3 id="tit3">직접 선택자</h3>
	<h3>인접 선택자</h3>
</body>
```




### 193 eq(인덱스) / lt(인덱스) / gt(인덱스) 탐색 선택자

```js
<script>
	$(function(){
		$("#menu li:lt(2)")
			.css({"background-color":"yellow"			
		});
		$("#menu li").eq(2)
			.css({"background-color":"green"
		});		
		$("#menu li:gt(2)")
			.css({"background-color":"blue"			
		});
	});
</script>   
```
![image](https://user-images.githubusercontent.com/34564706/88260988-6a940100-cd00-11ea-871f-bad8f7a5d71d.png)


### first-of-type / last-of-type 선택자
```js
<script>
	$(function(){
		$("li:first-of-type")
			.css({"background-color":"red"			
		});
		$("li:last-of-type")
			.css({"background-color":"blue"
		});
	});
</script>
```
![image](https://user-images.githubusercontent.com/34564706/88262501-4b4aa300-cd03-11ea-9d7b-6cf3d7bd4398.png)


### nth-child(숫자n) / nth-last-of-type(숫자) 선택자
```js
<script>
	$(function(){
		$("#menu1 li:nth-child(1)")
			.css({"background-color":"red"			
		});
		$("#menu1 li:nth-child(2n)")
			.css({"background-color":"green"
		});
		$("#menu2 li:nth-last-child(2)")
			.css({"background-color":"blue"
		});
	});
</script>
</head>
<body>
	<h1>탐색 선택자</h1>
	<ul id="menu1">
		<li>내용1-1</li>
		<li>내용1-2</li>
		<li>내용1-3</li>
		<li>내용1-4</li>
	</ul>
	<ul id="menu2">
		<li>내용2-1</li>
		<li>내용2-2</li>
		<li>내용2-3</li>
	</ul>
</body>
```
![image](https://user-images.githubusercontent.com/34564706/88262942-20ad1a00-cd04-11ea-99c9-28423fe342a8.png)






198 배열 관련 메서드
245 이벤트 등록 메서드
279 그룹 이벤트 등록 및 삭제
290 효과 및 애니메이션 메서드
342 제이쿼리 플러그 인

아사달

후이즈
가비아


# 09 제이쿼리 비동기 방식 연동
## 09-1 Ajax

jQuery CDN 다운받지 않고 온라인으로. 개발할 땐 위험



<img src="" width=200></img>
<img src="" width=200></img>
