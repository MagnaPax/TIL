### NLP (Natural Language Processing, 자연어처리)
> 텍스트에서 의미있는 정보를 분석, 추출하고 이해하는 일련의 기술집합입니다.

- NLP 응용사례
 - 텍스트 요약 (ex: Summly)
 - 대화 시스템 (ex: Apple Siri)
 - 기계 번역 (ex: Google Translate)

### 형태소 분석
- 더 이상 의미를 자를 수 없는 최소 단위
- 형태소 분석 이란 형태소를 비롯하여, 어근, 접두사/접미사, 품사(POS, part-of-speech) 등 다양한 언어적 속성의 구조를 파악하는 것
- 품사 태깅 은 형태소의 뜻과 문맥을 고려하여 그것에 마크업을 하는 일

### NLP 기초
- wordcount 방식으로 빅데이터를 추출하여
- 범용하게 많이 사용하는 단어의 빈도 계산을 통한 의미분석

### 형태소 적용 빅데이터 긍부정 분석
- KoNLPy(코엔엘파이) 한국어 정보처리를 위한 파이썬 패키지
- 형태소 분석기(코코마)를 활용하여 긍부정 요소에 대한 검증
- 단순 wordcount 방식보다 형태소 분석기를 활용
- 기존 정확도 대비 50->80 부정 표현의 경우 50% 이상의 효율 향상


```python
import requests
from bs4 import BeautifulSoup
import cx_Oracle
import re
```


```python
from konlpy.tag import Kkma
from konlpy.utils import pprint
kkma = Kkma()
```


```python
uid='PROJECT1'
upw='Test1234'
url='localhost:1521/orcl'
conn=cx_Oracle.connect(uid,upw,url)
cursor=conn.cursor()
#print(conn)
```


```python
def selData(wsql='where MPOINT<=5'): # wsql 에 아무런 값이 안 들어오면 기본값으로 'where MPOINT<=5' 만약 값이 들어오면 그 파라미터 값으로 
    sql="select MCONTENT from MOVIEREV "+wsql
    # (긍정 or 부정)요소 추출
    cursor.execute(sql)
    res=cursor.fetchall()
    print(len(res))
    return res

#selData('where MPOINT>5') # 긍정
#selData('where MPOINT<=5') # 부정
```


```python
def makePos(s=''):
    kpos=kkma.pos(s)
    pset=[]
    for pos in kpos:
        pset.append('/'.join(pos))
    return pset
```


```python
def selWord(wsql='  where MPOINT<=5'):
    result=selData(wsql)
    alltxt=''
    # 결과 데이터로 부터 하나의 문장으로 변환
    for r in result:
        alltxt+=r[0]+' '
        
    txtarr=makePos(alltxt)
    #print(len(txtarr))
    #print(txtarr[:10])
    #print(txtarr.count('하고'))
    return txtarr
```


```python
#res=selWord()
#res=selWord(' where MPOINT<=5')
res=selWord(' where MPOINT>5')
#res[:100]
```

    7778
    


```python
def getWcount(txtarr):
    regWord={}
    for word in txtarr:
        if(word!=' '):
            if(word in regWord):
                regWord[word]+=1
            else:
                regWord[word]=1
    return regWord;
```


```python
def f1(x):
    return x[1]
def wgtWord(srcDict):
    res = sorted(srcDict.items(),key=f1,reverse=True)
    maxv=res[0][1]
    print("최대값:", maxv)
    result=[]
    for r in res:
        result.append((r[0], format(r[1]/maxv,'.4f')))
    return result[:1000]
```


```python
# 부정요소
negArr=selWord(' where MPOINT<=5')
negDict=getWcount(negArr)
negWgt=wgtWord(negDict)
negWgt[999]
#res[:10]
```

    2905
    최대값: 2154
    




    ('의미/NNG', '0.0051')




```python
# 긍정요소
posArr=selWord(' where MPOINT>5')
posDict=getWcount(posArr)
posWgt=wgtWord(posDict)
posWgt[999]
#res[:10]
```

    7778
    최대값: 5698
    




    ('현실성/NNG', '0.0042')




```python
def calcSen(sen='',pwgt=[],nwgt=[]):
    pw=dict(pwgt)
    nw=dict(nwgt)
    #print(nw)
    words=makePos(sen)
    #print(words)
    pp=0
    np=0
    for word in words:
        if(word in pw.keys()):
            pp+=float(pw[word])
            #print("긍정:",word,",point:",pw[word])
        if(word in nw.keys()):
            np+=float(nw[word])
            #print("부정:",word,",point:",nw[word])
    #print("긍정점수:",pp,", 부정점수:",np," total:",pp-np )
    return pp-np
```


```python
s='솔직히... 재미없다고 말할수는 없지만, 평점이 왜이리 높은지는 의아하다. ㅋㅋㅋㅋ. 반도의 영향인가? 코드가 나와 맞지 않아서인지 모르겠지만, 빵빵터지는 장면 별로 없는거 같다. 뭔ㄱ ㅏ2프로 부족한? 그래도 코로나로 인해 개봉영화가 별로 없는 상황을 감안하고 본다면 아주 못볼정도는 아닌거 같다. 확실한건 반도보다는 재미있다'
calcSen(s,posWgt,negWgt)
```




    -0.8151000000000046




```python
s='하...할말이 없습니다'
calcSen(s,posWgt,negWgt)
```




    -0.26429999999999954



### 성능 체크


```python
nArr=selData(' where MPOINT<=5 and ROWNUM <= 100')
np=0
for n in nArr:
    point=calcSen(n[0],posWgt,negWgt)
    if(point<0):
        np+=1
print("부정 정확도:",np/100)
    
pArr=selData(' where MPOINT>5 and ROWNUM <= 100')
pp=0
for p in pArr:
    point=calcSen(p[0],posWgt,negWgt)
    if(point>0):
        pp+=1
print("긍정 정확도:",pp/100)

```

    100
    부정 정확도: 0.75
    100
    긍정 정확도: 0.81
    
