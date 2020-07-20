
## div id 와 div class

![image](https://user-images.githubusercontent.com/34564706/87934032-46021400-cac9-11ea-835c-3390af57aa77.png)

![image](https://user-images.githubusercontent.com/34564706/87934049-4b5f5e80-cac9-11ea-9e08-74f7c5059be7.png)

![image](https://user-images.githubusercontent.com/34564706/87934059-4dc1b880-cac9-11ea-9fb8-e13a236d89f2.png)


## 영역 구분
`<div>` 로 구분 된 영역을 아래와같이 더 세밀하게 구분
```html
<div>
    <section>
    <article>
    <footer>
</div>
```

```html
<!DOCTYPE html>
<html>
<head>
    <title>속성 사용</title>
</head>
<body>
    <h1>미리 정의된 속성을 사용한 사례</h1>
    <img src="00welcome.jpg" border="1" width="200" height="130" alt="이미지 못 찾았을 때 이 메세지 출력" title="이미지 위에 마우스커서 올렸을 때 나타나는 메시지">
    <a href="http://cafe.naver.com/go2web" target="_blank" title="클릭하세요!">저자 카페 방문</a>
</body>
</html> 
```

## 경로
`.` 내 위치 

`./` 내 하위폴더

`..` 내 부모 폴더

같은 폴더에 위치한 경우
```html
<img src="acid2Test.jpg" />
```

내 하위폴더 images 안에 있는 acid2Test.jpg 파일
```html
<img src="./images/acid2Test.jpg" />
<img src="images/acid2Test.jpg" />
```


## map, area 태그
>  이미지 안에서 특정 영역을 잡는다.
* 아래 이미지에서 웹접근성연구소(동그라미), 품질마크(네모), 자료실(삼각형), 교육/세미나(다각형) 을 클릭하면 다 다른 곳의 하이퍼링크 연결.
* 주로 지도에서 경기도 강원도 제주도 등을 클릭했을 때 해당 페이지를 연결해주는 용도로 쓰인다.

<img src="https://user-images.githubusercontent.com/34564706/87896917-a884f100-ca84-11ea-93eb-0e214a88d294.jpg" width=400></img>

```html
<map name="Map" id="Map">
    <area shape="circle" coords="201, 169, 60" href="http://www.wah.or.kr" alt="웹 접근성 연구소" />
    <area shape="rect" coords="40,77,112,152" href="http://www.wah.or.kr" alt="대체 텍스트" />
    <area shape="poly" coords="293,15,232,51,254,111,334,111,355,51" href="http://www.wah.or.kr" alt="대체 텍스트" />
    <area shape="poly" coords="310,185,250,283,370,283" href="http://www.wah.or.kr" alt="대체 텍스트" />
    <area shape="poly" coords="83,213,139,213,160,261,139,310,83,310,60,264" href="http://www.naver.com" alt="이 문구는 링크를 못 찾았을 때 나타남">
</map>
```

* 각 속성값의 의미 

<img src="https://user-images.githubusercontent.com/34564706/87896947-c3effc00-ca84-11ea-8792-809fa8213951.jpg" width=500></img>
  * x좌표 201, y좌표 169의 위치를 잡아 반지름 60의 크기로 원을 돌린 만큼의 면적
```html
<area shape="circle" coords="201, 169, 60"
```
  * (310,185)위치, (250,283)위치, (370,283)위치 세 꼭짓점을 갖는 삼각형
```html
<area shape="poly" coords="310,185,250,283,370,283"
```




## method 속성에서 사용하는 방식
* GET 방식
  * URL 뒤에 파라미터를 붙여서 데이터를 전달하는 방식
  * 사용자가 보내는 데이터는 이름과 값이 결합된 문자열 형태로 전달, 각 이름과
값의 쌍은 ‘&’ 기호로 구분
  * URL을 보면 어떤 데이터를 전송하고자 하는지 알 수 있기 때문에 보안에 취약

<img src="https://user-images.githubusercontent.com/34564706/87928756-4649e180-cac0-11ea-9325-73ab0e670fd7.png" width=200></img>

<img src="https://user-images.githubusercontent.com/34564706/87929097-d9831700-cac0-11ea-8196-2e94af2d9965.png" width=700></img>

* POST 방식
  - HTTP Request 헤더에 파라미터를 붙여서 데이터를 전송하는 방식
  - 서버로 보낼 수 있는 글자수 제한 없음
  - GET 방식과 비교하여 보안상 우위에 있음

<img src="https://user-images.githubusercontent.com/34564706/87928973-aa6ca580-cac0-11ea-8a14-4cd557280047.png" width=200></img>
<img src="https://user-images.githubusercontent.com/34564706/87929032-bf493900-cac0-11ea-8014-72534962ae61.png" width=700></img>


## div와 span

```html
<div id="coffee" style="background-color: #ffff00;">
    <h1>커피</h1>
    <div class="origin" style="background-color: blue;">
        <h2>원두 커피</h2>
        <p>원두 커피 맛있어요</p>
        <h3>자메이카 커피</h3>
        <p>자메이카 커피는??? 모르겠어요</p>
    </div>
</div>

<div class="Blending" style="background-color: aquamarine;">
    <h2>블랜딩 커피</h2>
    <h3>아메리카노</h3>
    <p>커피 원액 에스프레소</p>
    <h3>카푸치노</h3>
    <p>커피 원액 우유 거품 넣은 커피</p>
</div>
```
<img src="https://user-images.githubusercontent.com/34564706/87899117-264bfb00-ca8b-11ea-82b4-63430d22d392.png" width=200></img>

```html
<body>
<section>
	<h1>커피(Coffee)</h1>
	<ul>
		<li>
			아메리카노
			(<span lang="en">Americano</span>) - <span class="price" style="background-color: blue;">3,000원</span>
		</li>
		<li>
			카페라떼
			(<span lang="en">cafe latte</span>) - <span class="price">3,500원</span>
		</li>
		<li>
			카푸치노
			(<span lang="en">Cappuccino</span>) - <span class="price">3,800원</span>
		</li>
	</ul>
</section>
</body>
```

<img src="https://user-images.githubusercontent.com/34564706/87899232-8642a180-ca8b-11ea-9bc0-c53c9cad5269.png" width=300></img>



<img src="" width=200></img>
<img src="" width=200></img>
