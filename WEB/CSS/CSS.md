
blue    keyword 표현
#FF0000 16진수 표현
앞의 2자리 : R
다음 2자리 : G
마지막 2자리 : B


## CSS 적용법
* 파일명.css 으로 파일로 따로
* html 문서 안에 `<style>` 사용해서 적용


### 속성 선택자

```html
<style>
    h1[text]{
        color: red; background-color: gray;
    }
    h1[text="attr3"]{
        color: green; background-color: pink;
    }

</style>    
```

```html
<h1 text="attr1"> text 속성 이름 선택자 </h1>
<h1 text="attr2"> text 속성 이름 선택자 </h1>    
<p text="attr3"> text 속성 이름 선택자 </p>
<h1 text="attr3"> 속성과 속성값 선택자 </h1>
```

<img src="https://user-images.githubusercontent.com/34564706/87909859-f9f0a880-caa3-11ea-89a7-ee5404985114.png" width=200></img>




### 자동완성
> 다음과 같이 입력한 뒤 탭키 누르면 아래처럼 자동완성 됨
```html
div>ul>li
```
```html
<div>
    <ul>
        <li></li>
    </ul>
</div>
```


```html
div>ul+ol
```
```html
<div>
    <ul></ul>
    <ol></ol>
</div>
```


```html
ul>li*5
```
```html
<ul>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
</ul>
```



## position 속성
> position 속성에 의해 글자 위치가 바뀌는 것에 주목


```html
    <style>
        /* .rel{position: relative;top: 200px;left: 200px;} */ 
    </style>    
</head>
<body>

    <p>Relative Position</p>
    <p class="rel"> 박스의 위치를 지정할 때 사용할 수 있는 오프셋 속성으로 박스의 본래 위치를 기준으로 배치됩니다. </p>
    <p class="abs"> 박스의 위치를 지정할 때 사용할 수 있는 자신이 포함된 컨테이닝 박스의 위치를 기준으로 배치됩니다. </p>

</body>
```
<img src="https://user-images.githubusercontent.com/34564706/87913018-5a361900-caa9-11ea-8182-64d65e81bed2.png" width=500></img>


```html
    <style>
        .rel{position: relative;top: 200px;left: 200px;}
    </style>    
</head>
<body>

    <p>Relative Position</p>
    <p class="rel"> 박스의 위치를 지정할 때 사용할 수 있는 오프셋 속성으로 박스의 본래 위치를 기준으로 배치됩니다. </p>
    <p class="abs"> 박스의 위치를 지정할 때 사용할 수 있는 자신이 포함된 컨테이닝 박스의 위치를 기준으로 배치됩니다. </p>

</body>
```
<img src="https://user-images.githubusercontent.com/34564706/87913058-6b7f2580-caa9-11ea-9765-53b7171e5a2d.png" width=500></img>


### static 포지션
```html
    <style>
        #parent1{margin-top: 200px; margin-left: 200px; width: 300px; height: 300px; background-color: yellow;}
        #parent2{width: 200px; height: 200px; background-color: red;}
        #child{width: 100px; height: 100px; background-color: green;}
    </style>    
```
```html
<body>
    <div id="parent1">
        <div id="parent2">
            <div id="child">

            </div>
        </div>
    </div>
</body>
```
<img src="https://user-images.githubusercontent.com/34564706/87913536-3de6ac00-caaa-11ea-8b84-ef90c5158485.png" width=200></img>



```html
    <style>
        #parent1{position: relative; margin-top: 200px; margin-left: 200px; width: 300px; height: 300px; background-color: yellow;}
        #parent2{position: absolute; top: 0px; left: 0px; width: 200px; height: 200px; background-color: red;}
        #child{width: 100px; height: 100px; background-color: green;}
    </style>    
```
<img src="https://user-images.githubusercontent.com/34564706/87914158-370c6900-caab-11ea-9fdc-9d8a48fb6cec.png" width=200></img>

```html
   <style>
        #parent1{position: relative; margin-top: 200px; margin-left: 200px; width: 300px; height: 300px; background-color: yellow;}
        #parent2{position: absolute; top: 50px; left: 50px; width: 200px; height: 200px; background-color: red;}
        #child{width: 100px; height: 100px; background-color: green;}
    </style>    
```
<img src="https://user-images.githubusercontent.com/34564706/87914225-4b506600-caab-11ea-9002-100bdd549440.png" width=200></img>


### CSS 작성 시 유용한 사이트

```
※ 2차원 변환 시뮬레이션 참고 웹 사이트
https://testdrive-archive.azurewebsites.net/Graphics/hands-on-css3/hands-on_2d-transforms.htm
```

```
※ 3차원 변환 시뮬레이션 참고 웹 사이트
1) https://testdrive-archive.azurewebsites.net/Graphics/hands-on-css3/hands-on_3d-transforms.htm
2) http://www.htmllion.com/css3-3D-transform-tool.html
```

```
※ 큐빅 베지어 타이밍 함수 시뮬레이션 참고 웹 사이트
1) http://cubic-bezier.com/
2) http://www.netzgesta.de/dev/cubic-bezier-timing-function.html
```

