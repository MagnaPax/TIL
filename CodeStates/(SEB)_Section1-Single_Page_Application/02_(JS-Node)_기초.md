# 변수, 타입, 함수, 조건문, 문자열, 반복문

## 타입

> `변수`에는 다양한 타입이 있다

### primitive

> 더이상 작은 단위로 나누어질 수 없는 한가지 아이템

- number, string, boolean, null, undefined, symbol

### object

> primitive 타입 아이템들을 여러개 묶어서 한 단위로 관리할 수 있게

- function, first-class function

https://developer.mozilla.org/ko/docs/Web/JavaScript/Data_structures#%EB%8D%B0%EC%9D%B4%ED%84%B0_%ED%83%80%EC%9E%85

- [기본 자료형 (Primitive)](https://developer.mozilla.org/ko/docs/Glossary/Primitive) 인 여섯가지 데이터 타입
  - Boolean
  - Null
  - Undefined
  - Number (en-US)
  - String
  - Symbol (ECMAScript 6 에 추가됨)
- 별도로 Object 도 있음

- 숫자, 문자열, 참/거짓 뿐만 아니라
- 배열, 객체, undefine, 함수 이런것들도 타입이다

### ===를 사용하는 엄격한 같음

```js
var obj = new String("0");
var str = "0";

console.log(typeof(obj); // object
console.log(typeof(str); // string

console.log(obj === str); // false
console.log(null === undefined); // false
```

## 함수 선언 방법

```js
//함수선언식
function sum(a, b) {
  return a + b;
}
```

```js
//함수표현식
const sum = function (a, b) {
  return a + b;
};
```

```js
//함수표현식 (화살표함수-1)
const sum = (a, b) => {
  return a + b;
};
```

```js
//함수표현식 (화살표함수-2)
const sum = (a, b) => a + b;
```

## 조건문

### 조건연산자

```js
undefined; // false로 취급 falsy
("Hello"); // true로 truthy

!false; // true
!undefined; // true
!"Hello"; // false
```

### falsy 와 truthy

```js
// false 로 변환되어 if가 실행되지 않음
if (false)
if (null)
if (undefined)
if (0)
if (Nan)
if ('')
```
