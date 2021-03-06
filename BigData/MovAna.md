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


```python
import requests
from bs4 import BeautifulSoup
import cx_Oracle
import re
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
## def selData(wsql='where MPOINT<=5'):

def selData(wsql):
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
## def selWord(wsql='where MPOINT<=5'):
def selWord(wsql):
    result=selData(wsql)
    alltxt=''
    # 결과 데이터로 부터 하나의 문장으로 변환
    for r in result:
        alltxt+=r[0]+' '
        
    # 문장 정제
    #alltxt=alltxt.replace('/','').replace(';','').replace('~','').replace('.','')
    #alltxt=re.sub('[은는이가을를의와과] |[:,.;~\\\/] +', ' ', alltxt)
#    alltxt=re.sub('[와는은이가를도의] |[":,.;~\\\/]| +',' ', alltxt)    
    alltxt=re.sub('까지|로써|에서|에게서|부터|에게|한테|께|으로써|으로서|로서|으로|[은는이가을를의와과로] |[:,.;~\\\/] +', ' ', alltxt)

    #print(alltxt[:500])

    # 단어추출
    txtarr=alltxt.split(' ')

    #print(len(txtarr))
    #print(txtarr[:10])
    #print(txtarr.count('하고'))
    return txtarr

#selWord(' where MPOINT<=5') #부정
#selWord(' where MPOINT>5') #긍정
```


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
    최대값: 1507
    




    ('끌고', '0.0027')




```python
# 긍정요소
posArr=selWord(' where MPOINT>5')
posDict=getWcount(posArr)
posWgt=wgtWord(posDict)
posWgt[999]
#res[:10]
```

    7778
    최대값: 3930
    




    ('말도', '0.0028')




```python
def calcSen(sen='',pwgt=[],nwgt=[]):
    pw=dict(pwgt)
    nw=dict(nwgt)
    #print(nw)
    sen=re.sub('까지|로써|에서|에게서|부터|에게|한테|께|으로써|으로서|로서|으로|[은는이가을를의와과로] |[:,.;~\\\/] +', ' ', sen)
    words=sen.split(' ')
    #print(words)
    pp=0
    np=0
    for word in words:
        if(word in pw.keys()):
            pp+=float(pw[word])
#            print("긍정:",word,",point:",pw[word])
        if(word in nw.keys()):
            np+=float(nw[word])
#            print("부정:",word,",point:",nw[word])
    print("긍정점수:",pp,", 부정점수:",np," total:",pp-np )
    return pp-np
```


```python
s='솔직히... 재미없다고 말할수는 없지만, 평점이 왜이리 높은지는 의아하다. ㅋㅋㅋㅋ. 반도의 영향인가? 코드가 나와 맞지 않아서인지 모르겠지만, 빵빵터지는 장면 별로 없는거 같다. 뭔ㄱ ㅏ2프로 부족한? 그래도 코로나로 인해 개봉영화가 별로 없는 상황을 감안하고 본다면 아주 못볼정도는 아닌거 같다. 확실한건 반도보다는 재미있다'
calcSen(s,posWgt,negWgt)
```

    긍정점수: 0.36519999999999997 , 부정점수: 0.3906  total: -0.025400000000000034
    




    -0.025400000000000034




```python
s='하...할말이 없습니다'
calcSen(s,posWgt,negWgt)
```

    긍정점수: 0 , 부정점수: 0.0086  total: -0.0086
    




    -0.0086



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
    긍정점수: 0.1712 , 부정점수: 0.17049999999999998  total: 0.0007000000000000062
    긍정점수: 0.0334 , 부정점수: 0.0365  total: -0.0030999999999999986
    긍정점수: 1.0 , 부정점수: 1.0365  total: -0.03649999999999998
    긍정점수: 8.1494 , 부정점수: 8.322500000000002  total: -0.17310000000000159
    긍정점수: 0.507 , 부정점수: 0.5991000000000001  total: -0.09210000000000007
    긍정점수: 0.0305 , 부정점수: 0.0186  total: 0.0119
    긍정점수: 0.0107 , 부정점수: 0.0398  total: -0.0291
    긍정점수: 0 , 부정점수: 0.0126  total: -0.0126
    긍정점수: 0.583 , 부정점수: 0.7757000000000001  total: -0.1927000000000001
    긍정점수: 0.1632 , 부정점수: 0.1694  total: -0.006199999999999983
    긍정점수: 0 , 부정점수: 0.004  total: -0.004
    긍정점수: 0.087 , 부정점수: 0.14200000000000002  total: -0.05500000000000002
    긍정점수: 0.1759 , 부정점수: 0.2143  total: -0.03839999999999999
    긍정점수: 1.2122 , 부정점수: 1.2607  total: -0.04849999999999999
    긍정점수: 0.06280000000000001 , 부정점수: 0.0339  total: 0.02890000000000001
    긍정점수: 0.1839 , 부정점수: 0.2415  total: -0.057599999999999985
    긍정점수: 1.4705 , 부정점수: 1.5620000000000003  total: -0.09150000000000036
    긍정점수: 0.0323 , 부정점수: 0.0882  total: -0.0559
    긍정점수: 0.1613 , 부정점수: 0.2077  total: -0.0464
    긍정점수: 0.7060000000000001 , 부정점수: 0.7100000000000001  total: -0.0040000000000000036
    긍정점수: 0.0046 , 부정점수: 0.006  total: -0.0014000000000000002
    긍정점수: 1.1036 , 부정점수: 1.1634000000000002  total: -0.0598000000000003
    긍정점수: 2.2063 , 부정점수: 2.2839  total: -0.07759999999999989
    긍정점수: 0.0214 , 부정점수: 0.0445  total: -0.0231
    긍정점수: 0.0089 , 부정점수: 0.0179  total: -0.009
    긍정점수: 0.48100000000000004 , 부정점수: 0.5833000000000002  total: -0.10230000000000011
    긍정점수: 0.2769 , 부정점수: 0.35240000000000005  total: -0.07550000000000007
    긍정점수: 0.2495 , 부정점수: 0.564  total: -0.31449999999999995
    긍정점수: 0.3828 , 부정점수: 0.3258  total: 0.056999999999999995
    긍정점수: 0.4743 , 부정점수: 0.4434  total: 0.030899999999999983
    긍정점수: 0.0926 , 부정점수: 0.134  total: -0.041400000000000006
    긍정점수: 0.2278 , 부정점수: 0.29480000000000006  total: -0.06700000000000006
    긍정점수: 0.2013 , 부정점수: 0.3033  total: -0.10200000000000001
    긍정점수: 0.0176 , 부정점수: 0.0206  total: -0.002999999999999999
    긍정점수: 2.1088 , 부정점수: 2.1499  total: -0.041100000000000136
    긍정점수: 1.1988 , 부정점수: 1.2779999999999998  total: -0.07919999999999972
    긍정점수: 0 , 부정점수: 0  total: 0
    긍정점수: 0.010700000000000001 , 부정점수: 0.0266  total: -0.015899999999999997
    긍정점수: 0.119 , 부정점수: 0.26940000000000003  total: -0.15040000000000003
    긍정점수: 0 , 부정점수: 0  total: 0
    긍정점수: 2.1595 , 부정점수: 2.1500000000000004  total: 0.00949999999999962
    긍정점수: 0.055799999999999995 , 부정점수: 0.05959999999999999  total: -0.003799999999999998
    긍정점수: 1.1557000000000004 , 부정점수: 1.4046000000000005  total: -0.24890000000000012
    긍정점수: 0 , 부정점수: 0  total: 0
    긍정점수: 0 , 부정점수: 0  total: 0
    긍정점수: 5.420399999999999 , 부정점수: 5.764499999999999  total: -0.3441000000000001
    긍정점수: 1.7848 , 부정점수: 1.8791000000000002  total: -0.09430000000000027
    긍정점수: 2.7619000000000002 , 부정점수: 2.6097  total: 0.1522000000000001
    긍정점수: 0 , 부정점수: 0  total: 0
    긍정점수: 0.4942 , 부정점수: 0.6204000000000001  total: -0.1262000000000001
    긍정점수: 0.11379999999999998 , 부정점수: 0.0929  total: 0.020899999999999988
    긍정점수: 0.0041 , 부정점수: 0.0318  total: -0.027700000000000002
    긍정점수: 0.2964 , 부정점수: 0.31779999999999997  total: -0.021399999999999975
    긍정점수: 0.9647000000000001 , 부정점수: 0.8658999999999998  total: 0.09880000000000033
    긍정점수: 0 , 부정점수: 0.0106  total: -0.0106
    긍정점수: 0.2399 , 부정점수: 0.1778  total: 0.06209999999999999
    긍정점수: 0.1252 , 부정점수: 0.09949999999999999  total: 0.025700000000000014
    긍정점수: 1.1869 , 부정점수: 1.233  total: -0.04610000000000003
    긍정점수: 0.1694 , 부정점수: 0.2137  total: -0.044300000000000006
    긍정점수: 0.4585 , 부정점수: 0.5739000000000001  total: -0.11540000000000006
    긍정점수: 1.5661 , 부정점수: 1.5859  total: -0.01980000000000004
    긍정점수: 1.1311 , 부정점수: 1.3145  total: -0.1834
    긍정점수: 0.0094 , 부정점수: 0.0697  total: -0.0603
    긍정점수: 0.0455 , 부정점수: 0.0703  total: -0.024800000000000003
    긍정점수: 1.5132999999999999 , 부정점수: 1.6104000000000003  total: -0.09710000000000041
    긍정점수: 1.0244 , 부정점수: 1.0624  total: -0.038000000000000034
    긍정점수: 1.3563999999999998 , 부정점수: 1.5148000000000001  total: -0.15840000000000032
    긍정점수: 0.0338 , 부정점수: 0.0378  total: -0.0040000000000000036
    긍정점수: 0.3171 , 부정점수: 0.26730000000000004  total: 0.049799999999999955
    긍정점수: 1.2529 , 부정점수: 1.2800000000000002  total: -0.027100000000000346
    긍정점수: 0 , 부정점수: 0.0092  total: -0.0092
    긍정점수: 0 , 부정점수: 0  total: 0
    긍정점수: 0.0232 , 부정점수: 0.0883  total: -0.0651
    긍정점수: 0.404 , 부정점수: 0.2535  total: 0.15050000000000002
    긍정점수: 0 , 부정점수: 0.0033  total: -0.0033
    긍정점수: 0.14839999999999998 , 부정점수: 0.15599999999999997  total: -0.007599999999999996
    긍정점수: 1.0499 , 부정점수: 1.1679  total: -0.11799999999999988
    긍정점수: 0.11449999999999999 , 부정점수: 0.2688  total: -0.1543
    긍정점수: 0.0264 , 부정점수: 0.0252  total: 0.0011999999999999997
    긍정점수: 6.315 , 부정점수: 6.601799999999999  total: -0.2867999999999986
    긍정점수: 1.0 , 부정점수: 1.0046  total: -0.0045999999999999375
    긍정점수: 4.028200000000001 , 부정점수: 4.067  total: -0.03879999999999928
    긍정점수: 1.3867999999999998 , 부정점수: 1.3689  total: 0.017899999999999805
    긍정점수: 0.6445000000000001 , 부정점수: 0.7346  total: -0.09009999999999996
    긍정점수: 0.0832 , 부정점수: 0.0689  total: 0.014299999999999993
    긍정점수: 0.0911 , 부정점수: 0.12799999999999997  total: -0.036899999999999974
    긍정점수: 1.4016 , 부정점수: 1.5846  total: -0.18300000000000005
    긍정점수: 0.7117 , 부정점수: 0.7942999999999999  total: -0.0825999999999999
    긍정점수: 0 , 부정점수: 0.0073  total: -0.0073
    긍정점수: 0.39809999999999995 , 부정점수: 0.6898  total: -0.2917
    긍정점수: 0.0252 , 부정점수: 0.0876  total: -0.0624
    긍정점수: 1.0 , 부정점수: 1.0073  total: -0.007300000000000084
    긍정점수: 0.1282 , 부정점수: 0.0425  total: 0.0857
    긍정점수: 0.5316000000000001 , 부정점수: 0.6642  total: -0.13259999999999994
    긍정점수: 0.19569999999999999 , 부정점수: 0.2667  total: -0.07100000000000001
    긍정점수: 6.557500000000002 , 부정점수: 6.476400000000002  total: 0.08110000000000017
    긍정점수: 0 , 부정점수: 0  total: 0
    긍정점수: 0.1161 , 부정점수: 0.1871  total: -0.071
    긍정점수: 3.0793000000000004 , 부정점수: 3.0526  total: 0.02670000000000039
    긍정점수: 0.0123 , 부정점수: 0.0179  total: -0.005599999999999999
    부정 정확도: 0.74
    100
    긍정점수: 1.0644 , 부정점수: 1.0578  total: 0.006599999999999939
    긍정점수: 0.0804 , 부정점수: 0.0093  total: 0.0711
    긍정점수: 0.1391 , 부정점수: 0.0478  total: 0.09129999999999999
    긍정점수: 1.2373 , 부정점수: 1.1753  total: 0.062000000000000055
    긍정점수: 0.5002 , 부정점수: 0.5508000000000001  total: -0.05060000000000009
    긍정점수: 0.1178 , 부정점수: 0.061  total: 0.0568
    긍정점수: 1.6101 , 부정점수: 1.4088  total: 0.20130000000000003
    긍정점수: 0.2306 , 부정점수: 0.1347  total: 0.09590000000000001
    긍정점수: 0.1776 , 부정점수: 0.2109  total: -0.033299999999999996
    긍정점수: 0.0463 , 부정점수: 0.0458  total: 0.0005000000000000004
    긍정점수: 1.6549000000000003 , 부정점수: 1.6788  total: -0.02389999999999981
    긍정점수: 2.0523999999999996 , 부정점수: 2.0544000000000002  total: -0.002000000000000668
    긍정점수: 0.12420000000000002 , 부정점수: 0.0583  total: 0.06590000000000001
    긍정점수: 0.0148 , 부정점수: 0.033800000000000004  total: -0.019000000000000003
    긍정점수: 0.11149999999999999 , 부정점수: 0.0943  total: 0.017199999999999993
    긍정점수: 0.29329999999999995 , 부정점수: 0.32310000000000005  total: -0.029800000000000104
    긍정점수: 0.5868 , 부정점수: 0.6045  total: -0.01770000000000005
    긍정점수: 0.9171 , 부정점수: 0.5687  total: 0.34840000000000004
    긍정점수: 0.0262 , 부정점수: 0.0106  total: 0.015600000000000001
    긍정점수: 0.0415 , 부정점수: 0.023200000000000002  total: 0.0183
    긍정점수: 0.0066 , 부정점수: 0.0113  total: -0.004699999999999999
    긍정점수: 0 , 부정점수: 0  total: 0
    긍정점수: 4.1003 , 부정점수: 3.834  total: 0.26629999999999976
    긍정점수: 0.2489 , 부정점수: 0.1367  total: 0.11220000000000002
    긍정점수: 0.2735 , 부정점수: 0.1467  total: 0.12680000000000002
    긍정점수: 0.0308 , 부정점수: 0.0053  total: 0.025500000000000002
    긍정점수: 1.0357 , 부정점수: 1.0206  total: 0.015100000000000113
    긍정점수: 0.057999999999999996 , 부정점수: 0.0199  total: 0.038099999999999995
    긍정점수: 0.1814 , 부정점수: 0.2143  total: -0.032899999999999985
    긍정점수: 0.31980000000000003 , 부정점수: 0.07369999999999999  total: 0.24610000000000004
    긍정점수: 1.102 , 부정점수: 1.0556999999999999  total: 0.04630000000000023
    긍정점수: 0.7089000000000001 , 부정점수: 0.6775  total: 0.031400000000000095
    긍정점수: 0.40530000000000005 , 부정점수: 0.31320000000000003  total: 0.09210000000000002
    긍정점수: 2.7445 , 부정점수: 2.6356  total: 0.10889999999999977
    긍정점수: 0.17390000000000003 , 부정점수: 0.1447  total: 0.02920000000000003
    긍정점수: 0.5185000000000001 , 부정점수: 0.5839  total: -0.0653999999999999
    긍정점수: 1.0186 , 부정점수: 1.0139  total: 0.0046999999999999265
    긍정점수: 0.7818999999999999 , 부정점수: 0.5256000000000001  total: 0.25629999999999986
    긍정점수: 1.267 , 부정점수: 1.2735  total: -0.006500000000000172
    긍정점수: 0.7588 , 부정점수: 0.5827  total: 0.17610000000000003
    긍정점수: 0.0526 , 부정점수: 0.022600000000000002  total: 0.03
    긍정점수: 1.0127 , 부정점수: 1.0272  total: -0.014499999999999957
    긍정점수: 0.3232 , 부정점수: 0.20370000000000002  total: 0.11949999999999997
    긍정점수: 0.20769999999999997 , 부정점수: 0.2455  total: -0.03780000000000003
    긍정점수: 3.4312 , 부정점수: 3.303899999999999  total: 0.12730000000000086
    긍정점수: 3.8085999999999998 , 부정점수: 3.7085  total: 0.10009999999999986
    긍정점수: 0.15159999999999998 , 부정점수: 0.1685  total: -0.016900000000000026
    긍정점수: 0.0936 , 부정점수: 0.1387  total: -0.04509999999999999
    긍정점수: 0.18539999999999998 , 부정점수: 0.1923  total: -0.006900000000000017
    긍정점수: 0.476 , 부정점수: 0.5395  total: -0.0635
    긍정점수: 0.056400000000000006 , 부정점수: 0.0464  total: 0.010000000000000009
    긍정점수: 0.0888 , 부정점수: 0.0299  total: 0.05890000000000001
    긍정점수: 11.6282 , 부정점수: 11.7903  total: -0.16210000000000058
    긍정점수: 0.4132 , 부정점수: 0.3855  total: 0.027700000000000002
    긍정점수: 1.0707 , 부정점수: 0.9634  total: 0.10729999999999995
    긍정점수: 0 , 부정점수: 0  total: 0
    긍정점수: 0.5183 , 부정점수: 0.3457  total: 0.17259999999999998
    긍정점수: 2.4414000000000002 , 부정점수: 2.4032  total: 0.038200000000000234
    긍정점수: 0.06230000000000001 , 부정점수: 0.0166  total: 0.045700000000000005
    긍정점수: 0.3323 , 부정점수: 0.26799999999999996  total: 0.06430000000000002
    긍정점수: 0.49720000000000003 , 부정점수: 0.5514  total: -0.05419999999999997
    긍정점수: 0.10800000000000001 , 부정점수: 0.0444  total: 0.06360000000000002
    긍정점수: 0.08449999999999999 , 부정점수: 0.1354  total: -0.0509
    긍정점수: 0.30920000000000003 , 부정점수: 0.1805  total: 0.12870000000000004
    긍정점수: 0.2697 , 부정점수: 0.0995  total: 0.1702
    긍정점수: 3.479900000000001 , 부정점수: 3.800299999999999  total: -0.320399999999998
    긍정점수: 1.0 , 부정점수: 1.0  total: 0.0
    긍정점수: 2.1831 , 부정점수: 1.8485  total: 0.3346
    긍정점수: 0.9814 , 부정점수: 0.7594999999999998  total: 0.2219000000000002
    긍정점수: 0.559 , 부정점수: 0.6157999999999999  total: -0.05679999999999985
    긍정점수: 1.0046 , 부정점수: 1.0046  total: 0.0
    긍정점수: 1.8345000000000005 , 부정점수: 1.8937000000000006  total: -0.05920000000000014
    긍정점수: 0.2048 , 부정점수: 0.0518  total: 0.15300000000000002
    긍정점수: 0.1684 , 부정점수: 0.09749999999999999  total: 0.0709
    긍정점수: 0 , 부정점수: 0  total: 0
    긍정점수: 0.20479999999999998 , 부정점수: 0.10880000000000001  total: 0.09599999999999997
    긍정점수: 0.055999999999999994 , 부정점수: 0.0218  total: 0.034199999999999994
    긍정점수: 0.5206 , 부정점수: 0.3457  total: 0.17489999999999994
    긍정점수: 0.0064 , 부정점수: 0.0086  total: -0.0021999999999999997
    긍정점수: 0 , 부정점수: 0  total: 0
    긍정점수: 0.7816 , 부정점수: 0.7471000000000001  total: 0.034499999999999864
    긍정점수: 0.0089 , 부정점수: 0.0066  total: 0.0023
    긍정점수: 0.0402 , 부정점수: 0.0186  total: 0.0216
    긍정점수: 1.2412 , 부정점수: 1.2249  total: 0.01629999999999998
    긍정점수: 1.1096000000000001 , 부정점수: 0.9230999999999999  total: 0.18650000000000022
    긍정점수: 0.2562 , 부정점수: 0.2348  total: 0.021399999999999975
    긍정점수: 0.10339999999999999 , 부정점수: 0.1838  total: -0.0804
    긍정점수: 0.3143 , 부정점수: 0.1976  total: 0.11670000000000003
    긍정점수: 1.0326000000000002 , 부정점수: 1.0192  total: 0.013400000000000079
    긍정점수: 2.6689000000000003 , 부정점수: 2.4082  total: 0.2607000000000004
    긍정점수: 0.0641 , 부정점수: 0.0498  total: 0.014300000000000007
    긍정점수: 2.8886999999999996 , 부정점수: 2.8394  total: 0.04929999999999968
    긍정점수: 0.6226 , 부정점수: 0.46649999999999997  total: 0.15610000000000007
    긍정점수: 2.6918000000000006 , 부정점수: 2.6502  total: 0.04160000000000075
    긍정점수: 0.718 , 부정점수: 0.7624000000000001  total: -0.044400000000000106
    긍정점수: 0.0109 , 부정점수: 0.029900000000000003  total: -0.019000000000000003
    긍정점수: 1.0684 , 부정점수: 1.0245  total: 0.04390000000000005
    긍정점수: 1.8051000000000001 , 부정점수: 1.6362  total: 0.16890000000000005
    긍정점수: 0.212 , 부정점수: 0.3086  total: -0.09659999999999999
    긍정점수: 1.1447999999999998 , 부정점수: 1.1055000000000001  total: 0.03929999999999967
    긍정 정확도: 0.66
    


```python
from konlpy.tag import Kkma
from konlpy.utils import pprint
kkma = Kkma()
```


```python
s="진짜 딱 하드보일드 액션인데 웃음포인트도 있고 진짜 재밌었어요. 코로나만 아니었으면 그래도 크게 성공했을 듯ㅠㅠ스타일 섹시미 오지는 영화. "
```


```python
pprint(kkma.sentences(s))
```

    ['진짜 딱 하드 보일드 액션인데 웃음 포인트도 있고 진짜 재밌었어요.',
     '코로나만 아니었으면 그래도 크게 성공했을 듯 ㅠㅠ 스타일 섹시 미 오지는 영화.']
    


```python
pprint(kkma.nouns(s))
```

    ['하드',
     '하드보일드',
     '보일드',
     '액션',
     '웃음',
     '웃음포인트',
     '포인트',
     '코로나',
     '성공',
     '듯',
     '스타일',
     '섹시',
     '섹시미',
     '미',
     '오지',
     '영화']
    


```python
pprint(kkma.pos(s))
```

    [('진짜', 'MAG'),
     ('딱', 'MAG'),
     ('하드', 'NNG'),
     ('보일드', 'NNG'),
     ('액션', 'NNG'),
     ('이', 'VCP'),
     ('ㄴ데', 'ECE'),
     ('웃음', 'NNG'),
     ('포인트', 'NNG'),
     ('도', 'JX'),
     ('있', 'VV'),
     ('고', 'ECE'),
     ('진짜', 'MAG'),
     ('재밌', 'VA'),
     ('었', 'EPT'),
     ('어요', 'EFN'),
     ('.', 'SF'),
     ('코로나', 'NNG'),
     ('만', 'JX'),
     ('아니', 'VCN'),
     ('었', 'EPT'),
     ('으면', 'ECD'),
     ('그리하', 'VV'),
     ('여도', 'ECD'),
     ('크', 'VA'),
     ('게', 'ECD'),
     ('성공', 'NNG'),
     ('하', 'XSV'),
     ('었', 'EPT'),
     ('을', 'ETD'),
     ('듯', 'NNB'),
     ('ㅠㅠ', 'EMO'),
     ('스타일', 'NNG'),
     ('섹시', 'NNG'),
     ('미', 'NNG'),
     ('오지', 'NNG'),
     ('는', 'JX'),
     ('영화', 'NNG'),
     ('.', 'SF')]
    
