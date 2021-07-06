# Chapter - DOM 이해하기



DOM은 Document Object Model의 약자로, HTML 요소를 Object(JavaScript Object)처럼 조작(Manipulation)할 수 있는 Model입니다. 즉, 여러분이 **자바스크립트를 사용할 수 있으면, DOM으로 HTML을 조작할 수 있습니다.**

HTML을 조작할 수 있다는게 무슨 뜻일까요? DOM을 위해 여러 뛰어난 웹 개발자들이 모여, HTML을 철저히 분석했습니다. 분석한 내용으로 HTML의 아주 작은 부분까지 접근할 수 있는 구조(Model; Structure)를 만들어 냈습니다. 이렇게 만들어진 구조를 이용하여 HTML로 구성된 웹 페이지를 동적으로 움직이게 만들 수 있습니다. 앞서 학습한 조건문과 반복문, 배열, 객체를 활용하면 SNS에서 새롭게 생성되는 게시물을 저장하고 분류하는 작업을 할 수 있습니다.

[자바스크립트는 다양한 일을 할 수 있지만](https://www.youtube.com/watch?v=p5vI5OrLJU8), 웹 페이지를 제어하기 위한 목적으로 오랜 기간 사용되었습니다. 이번 유닛에서 DOM을 학습하고, 웹 개발에 가장 적합한 언어인 자바스크립트로 홈페이지를 조금 더 다이나믹하게 만듭니다.

## Achievement Goals

- DOM의 개념을 이해할 수 있다.
- DOM의 구조를 파악하고, HTML과 DOM이 어떻게 닮아있는지 알 수 있다.
- HTML에서 Javascript 파일을 불러올 때 주의점에 대해서 이해할 수 있다.
  - `<script>` 태그가 적용되는 위치에 따라서 실행 결과가 달라질 수 있음을 이해할 수 있다.

## Advanced Challenge

- [DOM과 JavaScript의 차이에 대해 이해할 수 있다.](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction#DOM_and_JavaScript)





# Chapter - DOM으로 HTML 조작하기



앞선 챕터에서 확인할 수 있듯이, `document` 객체에는 많은 속성과 메소드가 존재합니다. 모든 속성과 메소드를 외워야 할까요? 지금 당장 전부 알아야 할 필요는 없습니다. 지금 집중할 부분은 CRUD(Create, Read, Update and Delete) 입니다. 앞으로 여러분이 앞으로 어떤 종류의 개발이나 컴퓨터 언어를 배우시더라도 가장 먼저 CRUD에 집중해야 합니다. CRUD를 먼저 이해하는 것이 새로운 언어를 가장 빠르게 학습하는 방법입니다. (CRUD를 이해한 다음에는 다양한 trivia를 알아야 합니다.)

이 챕터에서는 document 객체를 통해서 HTML 엘리먼트를 만들고(CREATE), 조회하고(READ), 갱신하고(UPDATE), 삭제하는(DELETE) 하는 방법을 학습합니다. DOM에는 HTML에 적용(APPEND)하는 메소드가 따로 있으니 주의하세요!

각 페이지에는 codesandbox 실습 창이 있으니, 수업 내용을 읽어보면서 실습하세요.

**각 챕터에 있는 Further Study와 Advanced Challenge는 필수가 아닙니다.** 다만 개념이 조금 더 궁금하거나, 보다 더 자세히 학습하고 싶은 경우 시도해보기 바랍니다.

## **Achievement Goals**

- DOM을 JavaScript로 조작하여 HTML Element를 추가하거나 삭제, 혹은 내용을 변경할 수 있다.
  - createElement - CREATE
    - => `document.createElement('span')`
  - querySelector, querySelectorAll - READ
    - => querySelecor 는 맨 처음, querySelectorAll 은 전부
  - textContent, id, classList, setAttribute - UPDATE
    - => textContent 는 XSS 공격의 위험이 없다. 사용권장
  - remove, removeChild, `innerHTML = ""` , `textContent = ""` - DELETE
  - appendChild - APPEND
  - innerHTML과 textContent의 차이

## **Advanced Challenge**

- DOM의 더 깊은 내용에 대해서 이해할 수 있다.
  - [createDocumentFragment를 활용](https://developer.mozilla.org/en-US/docs/Web/API/Document/createDocumentFragment)하여, 더 효율적으로 DOM을 제어할 수 있다.
  - [HTML5 template tag 사용법을 이해할 수 있다.](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/template)
  - element와 node의 차이를 이해할 수 있다.
  - children과 childNodes의 차이를 이해할 수 있다.
    - removeChild 
  - remove와 removeChild의 차이를 이해할 수 있다.
  - [같은 엘리먼트를 appendChild 하면, 기존 엘리먼트를 복사할까?](https://indepth.dev/here-is-why-appendchild-moves-a-dom-node-between-parents/)
    - 이동시킨다. 복사는 `cloneNode()
  - 좌표 정보 조회를 할 수 있다. - offsetTop...
  - 크기 정보 조회를 할 수 있다. - offsetWidth...



# Sprint - 유효성 검사

![회원가입창](https://s3.ap-northeast-2.amazonaws.com/urclass-images/-uUgTBSM5-1615453953920.png)

[그림] 웹 사이트의 회원가입 예시

누구나 한 번쯤은 웹사이트의 회원가입을 진행해보신 경험이 있을 겁니다. 가입 과정을 거치다 보면, 사이트에서 원하는 조건에 맞게 반드시 형식을 맞춰 입력해야 하는 경우가 생깁니다.

- 특정 값은 반드시 입력해야 합니다. (아이디, 이메일, 비밀번호, 이름, 전화번호 등)
- 비밀번호는 n 자릿수 이상이어야 하고, 숫자나 특수문자를 반드시 포함해야 합니다.
- 비밀번호와 비밀번호 확인란에 입력된 비밀번호가 동일해야 합니다.
- 신용카드의 경우, 입력한 신용카드의 번호가 유효해야 합니다.

이런 기능을 **유효성 검사**(Form validation)라고 부릅니다. 유효성 검사는 실제 개발 과정에서 정말 많이 맞닥뜨리는 문제 중 하나입니다.

회원가입처럼 작은 기능 단위의 제품을 만들기 위해서는, 위와 같이 요구 사항을 정리하는 과정이 매우 중요합니다. 유효성 검사의 목표는 **회원 가입**이라는 핵심 기능에 대해, 작동이 가능한 [MVP(Minimum Viable Product)](https://ko.wikipedia.org/wiki/최소_기능_제품)를 만들어 내는 것입니다.

위의 조건을 만족하는 함수를 작성하면 충분할까요? UI가 존재하는 프로그램(웹 서비스 등)에는 충분하지 않습니다. 이번 챕터에서는 유효성 검사의 과정을 따라가면서 그 이유를 이해합니다.

## Before You Learn

- HTML & CSS 기초
- DOM 기초와 CRUD

## Achievement Goals

- DOM 기초 실습을 통해, 구체적인 사용법을 익힐 수 있다.
  - querySelector를 활용하여, HTML 엘리먼트 정보를 가져올 수 있다.
  - oncilck, onkeyup 속성이나 addEventListener 메소드로 이벤트 핸들러 함수를 HTML 엘리먼트에 적용할 수 있다.
  - 이벤트 핸들러 함수에서 이벤트가 발생한 곳의 정보를 확인할 수 있다.
  - 이벤트 핸들러 함수로 유효성 검사를 실행할 수 있다.
- 유효성 검사에 필요한 기술 요소를 익힐 수 있다.
  - 유효성 검사에 필요한 HTML 엘리먼트, CSS 속성이 무엇인지 알 수 있다.
    - 엘리먼트가 화면에 표시되거나 사라지게 만들 수 있다. (display: none)
  - 유효성 검사에서 활용할 수 있는 정규표현식 사용법 기초에 대해서 익힐 수 있다. (advanced)
- 관심사 분리를 적용하거나, 유효성 검사 함수를 따로 분리해서 설계할 수 있다. (advanced)





# Chapter - 이벤트 객체



웹 사이트를 서핑하다 보면, 이미지나 카드를 클릭하거나 드래그하는 일이 있습니다. 이렇게 클릭이나 드래그하는 일을 이벤트라고 합니다. 이번 챕터는 기본적인 이벤트를 알고, 이벤트 핸들러를 구현합니다. 구현한 이벤트 핸들러를 적절한 엘리먼트에 적용하여, 사용자가 엘리먼트에 특정 이벤트를 발생시켰을 때 이벤트 핸들러가 동작하도록 합니다.

## Achievement Goals

- 기초적인 event를 알고, event handler를 element에 적용할 수 있다
  - onclick event
  - onclick 에 직접 할당하는 것과 addEventListener의 차이
  - eventHandler 함수를 만들고, eventHandler의 첫번째 인자를 사용할 줄 안다.