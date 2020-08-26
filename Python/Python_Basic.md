
# 파이썬 특징
1. 인간 친화적 언어(쉬운 문법)
2. 간결성(중복 최소화)
3. 인터프리터 언어(스크립트)
4. 라이브러리가 풍부(C나 타언어 즉각 사용 가능)
5. 작성 포맷이 중요
6. 변수 타입이 없음. 형변환 자유로움

```py
"""
사칙연산+2
+ - * / % //
"""
a=3
b=4
c=a+b
c=a-b
c=a*b
c=a/b
c=a%b # 나머지 연산
c=a//b # 몫 연산
```

```py
a="안녕하세요"
b="여러분"
c=a+b
print(c)
```

```py
"""
조건은 if
블럭생성 시 들여쓰기로 설정
:으로 블럭 시작
1줄이 1명령
"""
a=3
b=4

if b>a:
    print("b는 a보다 크다")
else:
    print("b는 a보다 크지 않다")
    print("진짜 크지 않아?")
print("진짜 안 커")
```

```py
"""
중첩 if
성적내기
"""
score=75
grade=""
if score>90:
    grade="A"
else:
    if score>80:
        grade="B"
    else:
        if score>70:
            grade="C"
        else:
            grade="F"
print("grade: "+grade)
```

```py
"""
연속if
switch 문이 없어서 대신 사용
elif
"""
if score>90:
    grade="수"
elif score>80:
    grade="우"
elif score >70:
    grade="미"
else:
    grade="낙제"
print("성적은 "+grade+" 입니다")
```

```py
"""
반복문 for
for 변수 in 집합:
    for(int i=0; i<10; i++)
"""
for i in range(10):
    print(i)
print('*'*30) # 문자열 곱 연산

# 범위지정
for i in range(5,10):
    print(i)
print('*'*30)

# 스탭지정
for i in range(0,10,2):
    print(i)
print('*'*30)
    
# enumerate 데이터와 순서의 쌍으로 표현
arr=[1,3,5,10,"안녕", 3, [2, "go"]]
for i in enumerate(arr):
    print(i)
```

```py
"""
<자료형>
숫자형
    int
    float
문자형
    '' 홑따옴표
    "" 쌍따옴표
"""
a="우리는 응원할 때 '대한민국~'이라고 외친다"
print(a)

# 문자열 이스케이프
a="우리는 응원할 때 \"대한민국~\" 이라고 외친다"
print(a)

#여러줄 문자열
a="우리는 응원할 때\n '대한민국~' \n 이라고 외친다"
print(a)

#다열 문자열 이중 인용부호
a="""
"우리는 응원할 때
 '대한민국~'
 이라고 외친다"
 """
print(a)
```

```py
"""
문자열 연산
"""
print("#"*30)
# 문자열 합
c="여러분"+"안녕하세요"
print(c)
#문자열 곱
a="#"*30
print(a)
#인덱싱
print("0번 인덱스 문자는: "+c[0])
print("2번 인덱스 문자는: "+c[2])
print("-1번 인덱스(마지막) 문자는: "+c[-1])
print("-0번 인덱스(처음) 문자는: "+c[-0])
print("-3번 인덱스(뒤에서 3번째) 문자는: "+c[-3])
#슬라이싱: 일정 블럭 추출
#시작은 포함. 끝은 불포함
print("앞단어는: "+c[0:3])
print("뒷단어는: "+c[-3:-1])
# 비워두면 마지막까지
print("뒷단어는: "+c[-3:])
print("마무리는: "+c[4:])
print("시작은: "+c[:4])
print("처음부터마지막은: "+c[:])
```

```py
"""
문자열 포맷
%s 문자열
%c 문자 한 개
%d 숫자
%f 실수
"""
# 문자열 치환
a="오늘의 날씨는 %s 입니다" %"맑음"
print(a)
# 숫자치환
a="오늘의 온도는 %d 입니다" %28
print(a)
a="오늘 날씨는 %s 이고 온도는 %f 입니다" %("흐림", 25.9)
print(a)
```

```py
#문자열 함수 대소문자 바꾸기
a="hello"
b=a.upper()
print(b)
a=b.lower()
print(a)

# 포함 문자열 갯수 세기
print(a.count("l")) # a안에 l이 몇 개 있는가?

# 포함 문자 위치 찾기
print(a.find("o"))
print(a.find("r")) # 없으면 -1 반환

#문자열 삽입
a=","
b=a.join("abcd")
print(b)
print("#"*30)

#공백처리
a="   공백    "
print("다음은"+a+"입니다")
b=a.lstrip()
print("다음은"+b+"입니다")
b=a.rstrip()
print("다음은"+b+"입니다")
b=a.strip()
print("다음은"+b+"입니다")

# 치환 replace
b=c.replace("여러분", "신사숙녀 여러분")
print(b)

a=","
b="abcd"
c=a.join(b)
print(c)
c=c.split(",")
print(c)
```

```py
"""
#배열
리스트[] - 수정가능
튜플() - 수정불가
딕셔너리{} - 키밸류 형태
집합 {}:리스트 형태 set([]) - 중복배제
"""

a=[1,2,"안녕", [1.5, "hello"]]
a[1]="3.3"
print(a[1:3])
b=(1,2,"안녕", [1.5, "hello"])
#b[1]=3.3
print(b[1:3])

# 딕셔너리
c={"한국":"축구", "일본":"야구", "미국":"미식축구"}
c["중국"]="마작"
#print(c[1]) # 순서형 인덱싱 불가
print(c)
print(c["일본"])
#삭제
del c["미국"]
print(c)
print(c.keys()) # 키값만 가져오기
print(c.values()) # 밸류값만 가져오기

for i in enumerate(c.keys()):
    print(i,c[i[1]])

print("#"*30)

a=c.items()
print(a)
for i in enumerate(a):
    print(i)
    
print(c.get("러시아")) # 키가 존재하는 지 모를 때
if(c.get("러시아")==None):
    print("러시아가 없습니다")
#print(c["러시아"]) # 에러
# 키 존재 여부
print("러시아" in c)
if("러시아" in c):
    print("러시아가 있습니다")
else:
    print("러시아가 없습니다")

# 집합
a=set([1,2,3,3,3,3,3,3,3,3,3,3,3,3,3])
print(a)
a=set("hello")
print(a)
b=list(a) #사용은 리스트로 캐스팅해서 사용
print(b[1])

a=set([1,2,3,4,5,6])
b=set([4,5,6,7,8])
c=a&b #교집합
print(c)
c=a.intersection(b)
print(c)
#차집합
c=a-b
print(c)
c=a.difference(b)
print(c)
#합집합
c=a|b
print(c)
c=a.union(b)
print(c)
```

```py
"""
while 문
초기화 필요
조건식 필요
조건 변경식 필요(무한루프 방지)
"""
i=0
while i<10:
    i+=1 #조건변경식
    if i==5:
        continue
    if i%2==1:
        print(str(i)+"번은 홀수 입니다")
    elif i>7:
        break
```

```py
"""
함수
"""
def add(a,b=5):
    return a+b

def subtract(a,b):
    return a-b

print(add(3,5))

        
def gugudan():
    for i in range(1,10):
        for j in range(1,10):
            print(i, "X", j, "=", i*j)
        print("\n")
                
gugudan()
```

```py
# 모듈 불러오기
import sys
sys.path.append("D:\source_codes\Python\DataScience")
import myfunc

print(myfunc.add(3,4))
print(myfunc.subtract(10,8))
```

```py
#모듈 불러오기
from myfunc import add
print(add(5,6))
```

```py
#클래스
from myfunc import Calc

mycal3=Calc() # 객체생성
print(mycal3.cadd(3))
print(mycal3.cadd(7))

mycal4=Calc() # 객체생성
print(mycal4.cminus(6))
```

