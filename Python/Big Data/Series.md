
# 파일 위치

https://github.com/MagnaPax/Jupyter-notebook-on-Ubuntu

<br><br>


# Pandas

- 데이터를 분석할 때 가장 많이 쓰이는 라이브러리다.
- 행과 열을 쉽게 처리할 수 있는 함수를 제공하는 도구이다.

    ※ 각 열은 단일 데이터 형식만 저장

- numpy보다 유연하게 수치 연산 가능하다.

![20200924_102608](https://user-images.githubusercontent.com/34564706/94090678-2ed8fd00-fe51-11ea-827b-cb25d6a70bf8.jpg)


## Series

- index와 values로 이루어진 1차원 배열이다.
- 모든 유형의 데이터를 보유할 수 있다.
- 인덱스를 지정해 줄 수 있다.
- 인덱스 길이는 데이터의 길이와 같아야 한다.
- 명시적 인덱스와 암묵적 인덱스를 가진다.
    - loc : 인덱스값을 기반으로 행 데이터를 읽는다.
    - iloc : 정수 인덱스을 기반으로 행 데이터를 읽는다.
- DataFrame의 한 컬럼 데이터 세트
- Series 역시 DataFrame의 인덱스와 동일한 인덱스를 가진다
- 즉 Series는 컬럼이 하나인 데이터 구조체이고 DataFrame은 컬럼이 여러개인 데이터 구조체이다

```python
import pandas as pd
```


```python
age_in = pd.Series([22,33,44,55,28])
age_in
```




    0    22
    1    33
    2    44
    3    55
    4    28
    dtype: int64




```python
type(age_in)
```




    pandas.core.series.Series




```python
#인덱스를 접근하는 방법 ***
age_in.index
```




    RangeIndex(start=0, stop=5, step=1)




```python
# 값을 나타내는 방법
age_in.values
```




    array([22, 33, 44, 55, 28])




```python
print(age_in.keys)
```

    <bound method Series.keys of 0    22
    1    33
    2    44
    3    55
    4    28
    dtype: int64>



```python
# 인덱스가 key라는 값을 반환한다. => 시리즈 객체의 인덱스의 레이블 반환
age_in.keys()
```




    RangeIndex(start=0, stop=5, step=1)




```python
# 시리즈 생성하기
age_in = pd.Series([22, 33, 44, 55, 28], index=['가','나','다','라','마'])
age_in
```




    가    22
    나    33
    다    44
    라    55
    마    28
    dtype: int64




```python
# index 를 사용해서 시리즈에 접근할 수 있다.
age_in['다'] = 100
age_in
```




    가     22
    나     33
    다    100
    라     55
    마     28
    dtype: int64




```python
age_in.keys
```




    <bound method Series.keys of 가     22
    나     33
    다    100
    라     55
    마     28
    dtype: int64>




```python
age_in.keys()
```




    Index(['가', '나', '다', '라', '마'], dtype='object')



<실습문제>

Index(['가', '나'], dtype='object') 

처럼 출력해보기


```python
age_in.index[0:2]
```




    Index(['가', '나'], dtype='object')




```python
age_in['다']
```




    100




```python
# Series 인덱스 중복 -> Series 의 특성
srs = pd.Series(['가', '나', '다'], index=['a','b','a'])
print(srs)
print('*' * 50)
print(srs['a']) # 중복된 인덱스 값을 출력한다
print('*' * 50)
print(srs['b'])
print('*' * 50)
print(srs[0])
print(srs[1])
print('*' * 50)
print(srs[-1]) # 다 , -1 맨끝
```

    a    가
    b    나
    a    다
    dtype: object
    **************************************************
    a    가
    a    다
    dtype: object
    **************************************************
    나
    **************************************************
    가
    나
    **************************************************
    다



```python
print(srs.values)
type(srs.values)
```

    ['가' '나' '다']





    numpy.ndarray




```python
# numpy 의 Array를 사용해서 시리즈로 생성하기
# 11,22,33 의 값을 numpy로 생성해서
# 시리즈로 대입해보기

import numpy as np
n1 = np.array([11,22,33])
s1 = pd.Series(n1)
```


```python
s1
```




    0    11
    1    22
    2    33
    dtype: int64




```python
# 딕셔너리를 시리즈 형태로 변환 ***
info_list = {'kim':25,'park':22,'lee':34}
info_series = pd.Series(info_list)
```


```python
info_series
```




    kim     25
    park    22
    lee     34
    dtype: int64




```python
# 딕셔너리의 키값이 시리즈의 인덱스값이 된다.
info_series.index
```




    Index(['kim', 'park', 'lee'], dtype='object')




```python
info_series.values
```




    array([25, 22, 34])




```python
type(info_series.values)
```




    numpy.ndarray




```python
info_series.keys()
```




    Index(['kim', 'park', 'lee'], dtype='object')




```python
info_series['lee'] = 100
```


```python
info_series
```




    kim      25
    park     22
    lee     100
    dtype: int64




```python
# 딕셔너리를 시리즈 형태로 변환 ***
# 딕셔너리같은 경우 키값이 인덱스로 설정, 새로운 인덱스로 지정 -> NaN
info_list = {'kim':25,'park':22,'lee':34}
info_series = pd.Series(info_list,index=[0,1,2])
info_series
```




    0   NaN
    1   NaN
    2   NaN
    dtype: float64




```python
info_list = {'kim':25,'park':22,'lee':34}
info_series = pd.Series(info_list)
info_series
```




    kim     25
    park    22
    lee     34
    dtype: int64




```python
# -> 인덱스를 변경
# A 25
# B 22
# C 34

info_series.index = ['A','B','C']
info_series
```




    A    25
    B    22
    C    34
    dtype: int64



### Series 인덱스
- 리스트, 튜플의 index 와 dict 의 key 와 유사, numpy 의 ndArray
- 같은 값의 index 가 가능 (즉 중복 가능) => 튜플로 시리즈를 만들 때 중복된 인덱스를 넣어서 테스트 해보기


```python
mytuple = (10,20,30)
my_s = pd.Series(mytuple,index=['A','A','B'])
my_s
```




    A    10
    A    20
    B    30
    dtype: int64



### Pandas를 사용해야 하는 이유

```python
odd = [1,3,5,7,9]
type(odd)
#odd.mean()
```




    list




```python
odd = pd.Series(odd)
odd.mean()
```




    5.0
