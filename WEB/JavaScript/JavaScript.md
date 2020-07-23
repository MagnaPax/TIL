147??  자바와 달리 메소드 오버로딩은 되지만 오버라이딩은 안 됨

# JavaScript
> Front-end 개발 언어. 정적인 웹 문서에 동작을 부여한다.
> 자바스크립트는 Sun Microsystems 의 상용 명칭. 국제 표준 명칭은 ES5, ES6

## 02 자바 스크립트 기초 문법
### 02-1 자바스크립트 기초 문법
#### 내부 스크립트 외부로 분리하기
- 현재 폴더의 하위 폴더인 js 폴더 안에 example.js 이름으로 분리
```JS
<script src="js/example.js"></script>
```

#### 코드 입력 시 주의사항
- 문자형 데이터 작성 시 큰따옴표와 작은따옴표 겹침 오류 주의
```js
document.write('책에 "자바스크립트는 대소문자를 구분해야 합니다" 라고 나와 있다');
document.write("책에 \"자바스크립트는 대소문자를 구분해야 합니다\" 라고 나와 있다");
```
#### 자료형
- Boolean()메서드가 false 를 반환하는 경우
  - 숫자 0, null, undifined, 공백문자("")


html 태그 사용 가능
```js
<script>
	var str = "<table border='1'>";
	str += "<tr>";
	str += "<td>1</td><td>2</td><td>3</td>";
	str += "</tr>";
	str += "</table>";
	document.write( str );
</script>
```
![image](https://user-images.githubusercontent.com/34564706/88282729-0f283a00-cd25-11ea-9a33-db68d7e69923.png)

## 04 객체
### 04-1 객체
브라우저 객체 모델
![사본 -KakaoTalk_20200723_210429297](https://user-images.githubusercontent.com/34564706/88284353-37656800-cd28-11ea-9bd6-ba3bc862cae7.jpg)

![99A183405C20A7EB06](https://user-images.githubusercontent.com/34564706/88282915-6c23f000-cd25-11ea-8ddd-0233c94e118e.png)

- screen 객체
> 사용자의 모니터 정보(속성)를 제공. 모니터의 너비나 높이, 컬러표현
> 
- location 객체
> 사용자 브라우저와 관련도니 속성과 메서드 제공. url에 대한 정보와 새로고침 메서드 제공

종류|설명
:---:|:---:
location.href|주소 영역의 참조 주소를 설정하거나 url 반환
location.reload()|브라우저에서 `F5` 키를 누른 것처럼 새로 고침

- history 객체
> 사용자가 방문한 사이트의 기록을 남기고 이전 방문 사이트와 다음 방문 사이트로 다시 돌아갈 수 있는 속성과 메서드 제공

- navigator 객체
> 현재 방문자가 사용하는 브라우저 정보와 운영체제 정보 제공
> ![사본 -KakaoTalk_20200723_211226317](https://user-images.githubusercontent.com/34564706/88284969-4b5d9980-cd29-11ea-955c-bdfc4a522a9c.jpg)


### 04-2 내장 객체
내장 객체 생성하기
```js
<script>
	var tv = new Object( );
	tv.color = "white";
	tv.price = 300000;
	tv.info = function( ) {
		document.write("tv 색상: " + this.color, "<br>");
		document.write("tv 가격: " + this.price, "<br>");
	}

	document.write("<h1>tv 객체 메서드 호출</h1>");
	tv.info();
</script>
```
![image](https://user-images.githubusercontent.com/34564706/88283348-2a477980-cd26-11ea-837f-fed32cc7e179.png)


배열객체 생성 방법 2가지
```js
var d = new Array(30, "따르릉", true);
```
```js
var d = [30, "따르릉", true];
```
![사본 -KakaoTalk_20200723_205715179](https://user-images.githubusercontent.com/34564706/88283864-3ed84180-cd27-11ea-95be-4041bb289f3b.jpg)


배열실습. 전화번호 뒤 4자리 *로 변환
```js
<script>
	var userNum = prompt("당신의 연락처를 - 빼고 입력해 주세요.","");
	var result = userNum.substring(0, userNum.length - 4) + "****";
	document.write(result, "<br>");
</script>
```
![사본 -KakaoTalk_20200723_210231697](https://user-images.githubusercontent.com/34564706/88284205-fa997100-cd27-11ea-8845-a91ce219a010.jpg)



### 뷰포트(ViewPort)
- 자세한 내용은 viewport.md 참조

```html
<!--  
	width=device-width	넓이는 장치에서 제공해주는 넓이를 따른다
	user-scalable=yes	사용자의 화면 확대 허용 여부. 그런데 호환성 문제 때문에 no로 해도 화면 확대 가능
	initial-scale=1.0	처음 화면 비율
	maximum-scale=3.0	최대 허용 화면 비율
-->
<meta name="viewport" content="width=device-width,user-scalable=yes, initial-scale=1.0,maximum-scale=3.0" />
```


### 모바일 기기인지 확인하는 코드

```js
   /* 웹 사이트 접근 시 모바일 기기일 경우, 모바일 웹 페이지 구현 */

        // 변수를 선언합니다.
        var smartPhones = [
            'iphone', 'ipod',
            'windows ce',
            'android', 'blackberry',
            'nokia', 'webos',
            'opera mini', 'sonyerricsson',
            'opera mobi', 'iemobile', 'iPhone', 'iPod','iPad','Android','BlackBerry','SymbianOS','Bada','Kindle','Wii','SCH-','SPH-',
	'CANU-','Windows Phone','Windows CE','POLARIS','Palm','webOS','Dorothy Browser','IEMobile','MobileSafari',
	'Opera Mobi','Opera Mini','MobileExplorer','Minimo','AvantGo','NetFront','Googlebot-Mobile','Nokia',
	'LGPlayer','SonyEricsson','HTC','hp-tablet','SKT','lgtelecom','Vodafone', 'LG', 'MOT', 'SAMSUNG'
        ];

        for (var i in smartPhones) {
            // 스마트폰 확인
            if (navigator.userAgent.toLowerCase().match(new RegExp(smartPhones[i]))) {
                document.location = 'mobileindex/index.html';
            }
		}
```


### 사진이 3초 간격으로 나오게 하기.
```js
// Web_EXAM02_s 폴더 안에 있음

    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
    <script>
        /* CSS조건부 수식부터 정리

           ! : 아니다(not) - 예) [if !ie] ie가 아니라면

          lt : 작다(less than) - 예) [if lt ie 9] ie9 보다 작다면

          lte : 작거나 같다(less than equal) - 예) [if lte ie 8] ie8 보다 작거나 같다면

          gt : 크다(greater than) - 예) [if gt ie 6] ie6 보다 크다면

          gte : 크거나 같다(greater than equal) - 예) [if gte ie 7] ie7 보다 크거나 같다

          () : 우선처리

           & : 그리고(and) - 예) [if (gte ie 7)&(lt ie 9)] ie7 이상이고 ie9 미만이라면

		   | : 또는(or) - 예) [if (ie 7)|(ie 8)] ie7 이거나 ie8 이라면
		*/
        
        $(".slideList").children("div:gt(0)").hide();
        var current = 0;

        setInterval(function(){
            var next = (current+1) % 3;
                            /*  0 + 1 / 3 = 1    % 3은 3으로 나눈 후 나머지 값 반환
                                1 + 1 / 3 = 2
                                2 + 1 / 3 = 0
                                0 + 1 / 3 = 1 */            
            $(".slideList").find("div").eq(current).fadeOut();
            /* JavaScript eq() 배열[] 차이점 : eq는 sequence 이해하자
                ex)
                    var img= $images.eq(i);
                    var img = $images[i];

                차이점 
                    eq는 제이쿼리 객체를 반환한다. 반면에 []은 Dom객체를 반환한다. 
                    eq로 할 경우 제이쿼리 메소드를 사용할 수 있지만, Dom객체는 사용할 수 없다.  */
            $(".slideList").find("div").eq(next).fadeIn();
            current = next;
            /* console 로그 활용 현재값 변화 확인 가능 = 구글 브라우저 - 검사 - console 탭 체크 : 확인 가능
               console.log(current); */
console.log(current);               
               
        },3000);
    </script>
```


## 05 함수
### 05-1 함수
함수 정의와 익명함수
- 마지막 bye3 나오는 익명함수는 따로 호출되지 않아도 선언되면서 실행
```html
<script>
	var count = 0;

	myFnc(); // hello1 출력
	
	function myFnc() {
		count++;
		document.write("hello" + count,"<br>");
	}        
	
	myFnc(); // hello2 출력
	
	var theFnc = function() { // bye3 출력
		count++;
		document.write("bye" + count,"<br>");
	}
	
	theFnc();
</script>
```


매개변수 없이 함수에 전달된 값 받아오기
![사본 -KakaoTalk_20200723_212050951](https://user-images.githubusercontent.com/34564706/88285664-7b596c80-cd2a-11ea-913e-02d69fb5e5c7.jpg)

### 05-3 함수 스코프 개념 이해
즉시 실행 함수
> 함수 선언과 동시에 함수를 호출할 수 있는 함수

```js
// 기본형
(function(){
    자바스크립트 코드
}());
```
```js
(function(){
	var 변수명;

	function 함수명(){
		자바스크립트 코드;
	}
}());
```

```html
<script>
	(function() {
		var num = 100;
		function menu( ) {
			num += 100;
			alert(num);
		}
		menu( );
	}());

	(function(){
		var num = 100;
		function menu( ) {
			alert(num);
		}
	}( ));
</script>
```

### Prototype 이해하기
https://medium.com/@bluesh55/javascript-prototype-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-f8e67c286b67