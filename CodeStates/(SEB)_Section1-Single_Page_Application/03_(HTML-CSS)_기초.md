# Chapter - HTML 기초

## Opening tag, closing tag, attribute name(속성의 이름)과 attribute value(속성의 값)

![](https://user-images.githubusercontent.com/34564706/122494214-e9361300-d023-11eb-9d79-6f2fba2be32b.png)

## self-closing tag

```html
<area />
<base />
<br />
<col />
<command />
<embed />
<hr />
<img />
<input />
<keygen />
<link />
<menuitem />
<meta />
<param />
<source />
<track />
<wbr />
```

## 엘리먼트와 태그의 차이

![엘리먼트VS태그](https://user-images.githubusercontent.com/77217300/123093676-ecd3fa80-d466-11eb-93d1-01df9a07ee2c.png)

# Chapter - CSS 기초

## CSS의 문법 구성

<img width="1352" alt="CSS의 문법 구성" src="https://user-images.githubusercontent.com/34564706/123836086-44310980-d944-11eb-9559-9f15209e45e4.png">

## CSS 파일 추가

```html
<link rel="stylesheet" href="index.css" />
```

## 기본적인 셀렉터 (selector)

### id

```html
<h4 id="title">Hello</h4>
```

```css
#title {
  color: red;
}
```

### class

```html
<ul>
  <li class="menu-item">Mac</li>
  <li class="menu-item">iPhone</li>
</ul>
```

```css
.menu-item {
  text-decoration: underline;
}
```

### 여러 개의 class를 하나의 엘리먼트에 적용

> 적용하려는 class들을 공백으로 구분

```html
<li class="1st 2nd">Home</li>
```

```css
.2nd {
  font-weight: bold;
  color: #009999;
}
```

### class & id

| class | id  |
| :---: | :-: |
|  `.`  | `#` |

### padding과 margin차이

![padding과 margin 차이](https://user-images.githubusercontent.com/34564706/123836289-7e9aa680-d944-11eb-8579-85f465210ec8.png)
