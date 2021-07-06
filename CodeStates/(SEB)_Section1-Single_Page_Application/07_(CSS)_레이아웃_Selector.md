셀렉터

h1 { }
div { }
전체 셀렉터

- { }
  Tag 셀렉터

section, h1 { }
ID 셀렉터

#only { }
class 셀렉터

.widget { }
.center { }
attribute 셀렉터 (암기할 필요는 없습니다)

a[href] { }
p[id="only"] { }
p[class~="out"] { }
p[class|="out"] { }
section[id^="sect"] { }
div[class$="2"] { }
div[class*="w"] { }
후손 셀렉터

header h1 {}
자식 셀렉터 (후손 셀렉터와의 차이를 반드시 알고 있어야 합니다)

header > p { }
인접 형제 셀렉터

section + p { }
형제 셀렉터

section ~ p { }
가상 클래스

a:link { }
a:visited { }
a:hover { }
a:active { }
a:focus { }
요소 상태 셀렉터

input:checked + span { }
input:enabled + span { }
input:disabled + span { }
구조 가상 클래스 셀렉터 (암기할 필요는 없습니다)

p:first-child { }
ul > li:last-child { }
ul > li:nth-child(2n) { }
section > p:nth-child(2n+1) { }
ul > li:first-child { }
li:last-child { }
div > div:nth-child(4) { }
div:nth-last-child(2) { }
section > p:nth-last-child(2n + 1) { }
p:first-of-type { }
div:last-of-type { }
ul:nth-of-type(2) { }
p:nth-last-of-type(1) { }
부정 셀렉터

input:not([type="password"]) { }
div:not(:nth-of-type(2)) { }
정합성 확인 셀렉터

input[type="text"]:valid { }
input[type="text"]:invalid { }
