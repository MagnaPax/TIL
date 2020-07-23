

```html
<!DOCTYPE html>
<html lang="ko">
<head>
	<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,user-scalable=yes, initial-scale=1.0,maximum-scale=3.0" />
<title> 뷰포트(ViewPort) 기능 </title>
</head>
<body>
	<p> 뷰포트를 사용하면 화면 사이즈를<br /> <br />
	    특별히 고려하지 않아도 <br /> <br />
	    적절하게 표시할 수 있습니다.<br /> <br />
		즉 표시 화면의 크기, 확대/축소 허용,<br /> <br />
		초기 표시 배율 등을 지정할 수 있습니다. </p>
</body>
</html>

<!-- HTML5 모바일 웹 브라우저의 가상 해상도 조절 viewport 메타 태그
1. 기본 사용 형식
<meta name="viewport"
 content="속성1=값1, 속성2=값2, ..." />

2. 일반 사용 형식
<meta name="viewport" content="width=[가상 해상도];
 initial-scale=[초기 확대 축소 비율];
 maximum-scale=[최대 확대 비율];
 user-scalable=[사용자에 의한 확대 축소 허용 여부];" />

3. viewport 지정 가능 속성
    속성                                                 기능
width               너비(픽셀 단위) (기본값은 980, 범위는 200~10000, device-width를 지정할 수 있다)
height              높이(픽셀 단위) (기본값은 980, 범위는 223~10000, device-height를 지정할 수 있다)
initial-scale       초기 확대/축소 배율(기본값은 꽉 찬 화면으로 표시, 범위는 minimum-scale과 maximum-scale에 따름)
minimum-scale       최소 축소 배율 N(0~10, default 0.25)
maximum-scale       최대 확대 배율 N(0~10, default 1.6)
user-scalable       사용자가 확대/축소 할 수 있는지 여부(yes/no 중 선택)
target-densitydpi   화면 DPI 설정 (dpi_value, device-dpi, high-dpi, medium-dpi, low-dpi
dpi_value            대상 DPI로 사용하는 DPI 값을 지정합니다. 값 범위 70-400 내에 있어야합니다.
device-dpi          대상 DPI로 장치의 기본 DPI를 사용합니다.
high-dpi            대상 DPI로 hdpi를 사용합니다. 중간과 낮은 밀도 화면 적절한 다운 스케일
medium-dpi          대상 DPI로 mdpi를 사용합니다. 고밀도 스크린 최대 규모 저밀도 화면 아래로 확장. 이것이 기본 대상 밀도입니다.
low-dpi             대상 DPI로 ldpi를 사용합니다. 중간 및 높은 밀도 화면 적절한 최대 규모. 

4. viewport 사용 예
Ex1) 사용자 확대/축소 비활성화
<meta name="viewport" content="width=device-width, user-scalable=no" />
 
Ex2) 너비 320px 고정
<meta name="viewport" content="width=320" />
 
Ex3) 자동 사이징
<meta name="viewport" content="width=device-width" />
 
Ex4) 확대 정의
<meta name="viewport" content="initial-scale=1.0" />
 
Ex5) 화면의 DPI 설정
<meta name="viewport" content="target-densitydpi=device-dpi, width=device-width" />

Ex6) 너비를 320px로 고정하고, 확대/축소를 못하게 할 경우
<meta name="viewport" content="width=320, user-scalable=no" />

Ex7) 모바일용 화면 크기 비율 고정
<meta id="mobileMeta" name="viewport" content="width=device-width" />

=> 모바일 기기의 물리적 해상도와 브라우저의 가상 해상도를 맞추기 위해
   viewport 메타 태그에서 width를 device-width로 지정

Ex8) 모바일 기기 viewport 설정

<meta name="viewport" content="user-scalable=yes,
 initial-scale=0.4, maxmum-scale=3.0,minimum-scale=0.4,
 width=device-width,height=device-height, target-densitydpi=medium-dpi" /> -->
```