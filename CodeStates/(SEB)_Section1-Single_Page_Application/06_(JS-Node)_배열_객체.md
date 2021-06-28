# 배열

## 메소드

- **_concat()_**
  > concat() 메서드는 인자로 주어진 배열이나 값들을 기존 배열에 합쳐서 새 배열을 반환합니다.
- 기존배열을 변경하지 않습니다.
- 추가된 새로운 배열을 반환합니다.

```js
const a1 = ["a", "b"];
const a2 = ["d", "e"];
const a3 = array1.concat(array2);
// ["a", "b", "d", "e"]
```

- **_slice()_**

  > 어떤 배열의 begin부터 end까지(end 미포함)에 대한 얕은 복사본을 새로운 배열 객체로 반환합니다.

- 원본 배열은 바뀌지 않습니다.

```js
const ar = ["a", "b", "c", "d", "e"];

console.log(ar.slice(2));
// ["c", "d", "e"]

console.log(ar.slice(2, 4));
// ["c", "d"]

console.log(ar.slice(-2));
// ["d", "e"]

console.log(ar.slice(2, -1));
// ["c", "d"]
```

- **_splice()_**
  > 배열의 기존 요소를 삭제 또는 교체하거나 새 요소를 추가하여 배열의 내용을 변경합니다.

```js
const months = ["가", "나", "다", "라"];

months.splice(1, 0, "Feb");
// 인덱스 1부터 0개의 엘리먼트 지우고 'Feb' 삽입
console.log(months);
// ["가", "Feb", "나", "다", "라"]

months.splice(4, 1, "May");
// 인덱스 4부터 1개의 엘리먼트 지우고 'May' 삽입
console.log(months);
// Array ["가", "Feb", "나", "다", "May"]
```

- **_join()_**
  > 배열의 모든 요소를 연결해 하나의 문자열로 만듭니다.

```js
const elements = ["Fire", "Air", "Water"];

console.log(elements.join());
// "Fire,Air,Water"

console.log(elements.join(""));
// "FireAirWater"

console.log(elements.join("-"));
// "Fire-Air-Water"
```

### 배열 메소드가 원본 배열을 변경하는지, 하지 않는지에 대한 정보를 제공

https://doesitmutate.xyz/

# 문자열

## 메소드

- **_split()_**
  > String 객체를 지정한 구분자를 이용하여 여러 개의 문자열로 나눕니다.

```js
const str = "The quick brown fox jumps over the lazy dog.";

const words = str.split(" ");
console.log(words[3]);
// "fox"

const chars = str.split("");
console.log(chars[8]);
// "k"

const strCopy = str.split();
console.log(strCopy);
// Array ["The quick brown fox jumps over the lazy dog."]
```
