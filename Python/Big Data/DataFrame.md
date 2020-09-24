
# 파일 위치

https://github.com/MagnaPax/Jupyter-notebook-on-Ubuntu

<br><br>



# Pandas
- Series, DataFrame 등의 자료 구조를 활용해서 데이터 분석용 빅데이터를 더욱 빠른 속도로 처리함(CSV파일 읽기, 엑셀 파일보다 빠른 처리, RPA 의 근간이 되는 모듈)


```python
import numpy as np
import pandas as pd
```


```python
# 딕셔너리
dicts = {
    "a":[5,6,7],
    "b":[8,9,10],
    "c":['2018','2019','2020'],
    "d":[1.,2.,3.]
}

dicts
```




    {'a': [5, 6, 7],
     'b': [8, 9, 10],
     'c': ['2018', '2019', '2020'],
     'd': [1.0, 2.0, 3.0]}




```python
# 딕셔너리 이용해 시리즈 생성
df = pd.DataFrame(dicts, index=[1,2,3])

# dtype으로 판다스안의 자료형을 알 수 있다.
print("DataFrame : \n", df.dtypes)
df
```

    DataFrame : 
     a      int64
    b      int64
    c     object
    d    float64
    dtype: object





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>8</td>
      <td>2018</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6</td>
      <td>9</td>
      <td>2019</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7</td>
      <td>10</td>
      <td>2020</td>
      <td>3.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.info() # DataFrame 의 정보를 한눈에 확인하기
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 3 entries, 1 to 3
    Data columns (total 4 columns):
    a    3 non-null int64
    b    3 non-null int64
    c    3 non-null object
    d    3 non-null float64
    dtypes: float64(1), int64(2), object(1)
    memory usage: 120.0+ bytes



```python
# 가장 기본적인 데이터 접근법
# df['컬럼명'] or df.컬럼명
df['a']
df.a
```




    1    5
    2    6
    3    7
    Name: a, dtype: int64




```python
# 여러개의 칼럼을 보기 위해서는 반드시 컬럼을 리스트로 담아서 봐야 한다.
idx_list = ["a","b"]
df[idx_list]
df[["a","b"]]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6</td>
      <td>9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>




```python
import numpy as np
a = np.arange(5,14)
a
```




    array([ 5,  6,  7,  8,  9, 10, 11, 12, 13])




```python
# [[],[],[]] 형태로 이중 리스트 만들기
aa = np.arange(5,14).reshape(3,3)
aa
```




    array([[ 5,  6,  7],
           [ 8,  9, 10],
           [11, 12, 13]])




```python
import pandas as pd

# 칼럼을 지정해서 데이터 프레임으로 생성하기
# 칼럼값을 리스트로 지정하기
column = ["a","b","c"]
print(type(column))

# 2차원 데이터(행렬데이터)로 DataFrame을 생성
df = pd.DataFrame(aa,index=[1,2,3],columns=column)
df
```

    <class 'list'>





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11</td>
      <td>12</td>
      <td>13</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 비교 연산자 사용가능
# df.a 의 값이 특정 기준 (8) 인 데이터 프레임 가져오기 (행 row)
print(df[df.a == 8])
```

       a  b   c
    2  8  9  10



```python
print(df[df.a != 8])
```

        a   b   c
    1   5   6   7
    3  11  12  13



```python
# b 칼럼에서 10보다 큰 값을 가져오기 (행 row)
print(df[df.b > 10])
```

        a   b   c
    3  11  12  13



```python
print(df[df.b > 20]) # b칼럼에서 20보다 큰 값이 없기 때문에 Empty DataFrame
```

    Empty DataFrame
    Columns: [a, b, c]
    Index: []



```python
df[df.b > 20].empty # 비교연산자에 결과값이 empty 일 경우 True 를 반환
```




    True




```python
if df[df.b > 20].empty: # 적용
    print("20 이상인 값은 없음")
```

    20 이상인 값은 없음



```python
# df.b 에서 8보다 큰 값 가져오기
df.b > 8
```




    1    False
    2     True
    3     True
    Name: b, dtype: bool




```python
# df의 값의 조건으로 설정하면 원하는 데이터를 가져올 수 있다.
df[df['b'] > 8]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11</td>
      <td>12</td>
      <td>13</td>
    </tr>
  </tbody>
</table>
</div>




```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11</td>
      <td>12</td>
      <td>13</td>
    </tr>
  </tbody>
</table>
</div>




```python
# items()는 column, 시리즈의 values를 반환한다.
for label, content in df.items():
    print('LABEL: ', label)
    print('=-=-=-=-=-=-=-=-=-=-=')
    print('CONTENT: ')
    print(content)
```

    LABEL:  a
    =-=-=-=-=-=-=-=-=-=-=
    CONTENT: 
    1     5
    2     8
    3    11
    Name: a, dtype: int64
    LABEL:  b
    =-=-=-=-=-=-=-=-=-=-=
    CONTENT: 
    1     6
    2     9
    3    12
    Name: b, dtype: int64
    LABEL:  c
    =-=-=-=-=-=-=-=-=-=-=
    CONTENT: 
    1     7
    2    10
    3    13
    Name: c, dtype: int64



```python
data = {
    'name':['홍길동','이철수','김영희','박민수','이철호','김영희'],
    'year':[2014, 2015, 2016, 2017, 2018, 2016],
    'points':[1.5, 1.7, 3.9, 2.4, 2.9, 3.9]
}
            
data
```




    {'name': ['홍길동', '이철수', '김영희', '박민수', '이철호', '김영희'],
     'year': [2014, 2015, 2016, 2017, 2018, 2016],
     'points': [1.5, 1.7, 3.9, 2.4, 2.9, 3.9]}




```python
df = pd.DataFrame(data)
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>year</th>
      <th>points</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>홍길동</td>
      <td>2014</td>
      <td>1.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>이철수</td>
      <td>2015</td>
      <td>1.7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>김영희</td>
      <td>2016</td>
      <td>3.9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>박민수</td>
      <td>2017</td>
      <td>2.4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>이철호</td>
      <td>2018</td>
      <td>2.9</td>
    </tr>
    <tr>
      <th>5</th>
      <td>김영희</td>
      <td>2016</td>
      <td>3.9</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.drop_duplicates()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>year</th>
      <th>points</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>홍길동</td>
      <td>2014</td>
      <td>1.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>이철수</td>
      <td>2015</td>
      <td>1.7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>김영희</td>
      <td>2016</td>
      <td>3.9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>박민수</td>
      <td>2017</td>
      <td>2.4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>이철호</td>
      <td>2018</td>
      <td>2.9</td>
    </tr>
  </tbody>
</table>
</div>




```python
id(df.drop_duplicates())
```




    139637472951712




```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>year</th>
      <th>points</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>홍길동</td>
      <td>2014</td>
      <td>1.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>이철수</td>
      <td>2015</td>
      <td>1.7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>김영희</td>
      <td>2016</td>
      <td>3.9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>박민수</td>
      <td>2017</td>
      <td>2.4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>이철호</td>
      <td>2018</td>
      <td>2.9</td>
    </tr>
    <tr>
      <th>5</th>
      <td>김영희</td>
      <td>2016</td>
      <td>3.9</td>
    </tr>
  </tbody>
</table>
</div>




```python
id(df)
```




    139637472470184




```python
# 방법 1
df = df.drop_duplicates()
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>year</th>
      <th>points</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>홍길동</td>
      <td>2014</td>
      <td>1.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>이철수</td>
      <td>2015</td>
      <td>1.7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>김영희</td>
      <td>2016</td>
      <td>3.9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>박민수</td>
      <td>2017</td>
      <td>2.4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>이철호</td>
      <td>2018</td>
      <td>2.9</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 방법 2
df.drop_duplicates(inplace=True)
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
      <th>points</th>
      <th>penalty</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2014</td>
      <td>NaN</td>
      <td>1.5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2015</td>
      <td>NaN</td>
      <td>1.7</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>NaN</td>
      <td>3.9</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>NaN</td>
      <td>2.4</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2018</td>
      <td>NaN</td>
      <td>2.9</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 데이터 프레임에서 값 (내용)
df.values
```




    array([['홍길동', 2014, 1.5],
           ['이철수', 2015, 1.7],
           ['김영희', 2016, 3.9],
           ['박민수', 2017, 2.4],
           ['이철호', 2018, 2.9]], dtype=object)




```python
df.shape # 크기 (행과 열 갯수)
```




    (5, 3)




```python
df.ndim # 차원
```




    2




```python
# 인덱스, 칼럼 이름변경
df.index.name = 'MyName'
print(df)
```

           name  year  point
    MyName                  
    0       홍길동  2014    1.5
    1       이철수  2015    1.7
    2       김영희  2016    3.9
    3       박민수  2017    2.4
    4       이철호  2018    2.9



```python
df.columns.name = "info"
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>info</th>
      <th>name</th>
      <th>year</th>
      <th>point</th>
    </tr>
    <tr>
      <th>MyName</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>홍길동</td>
      <td>2014</td>
      <td>1.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>이철수</td>
      <td>2015</td>
      <td>1.7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>김영희</td>
      <td>2016</td>
      <td>3.9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>박민수</td>
      <td>2017</td>
      <td>2.4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>이철호</td>
      <td>2018</td>
      <td>2.9</td>
    </tr>
  </tbody>
</table>
</div>




```python
data = {
    'names':['홍길동','이철수','김영희','박민수','이철호'],
    'year':[2014, 2015, 2016, 2017, 2018],
    'points':[1.5, 1.7, 3.9, 2.4, 2.9]
}
            
data
```




    {'names': ['홍길동', '이철수', '김영희', '박민수', '이철호'],
     'year': [2014, 2015, 2016, 2017, 2018],
     'points': [1.5, 1.7, 3.9, 2.4, 2.9]}




```python
# penalty 란 칼럼을 추가하면 기존 data 에서 없는 새로운 칼럼이기 때문에
# 그 값은 알아서 NaN 으로 처리 된다
df = pd.DataFrame(data,columns=['year','names','points','penalty'], index = ['one','two','three','four','five'])

df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
      <th>points</th>
      <th>penalty</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2014</td>
      <td>홍길동</td>
      <td>1.5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2015</td>
      <td>이철수</td>
      <td>1.7</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>김영희</td>
      <td>3.9</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>박민수</td>
      <td>2.4</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2018</td>
      <td>이철호</td>
      <td>2.9</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.index
```




    Index(['one', 'two', 'three', 'four', 'five'], dtype='object')




```python
df.columns
```




    Index(['year', 'names', 'points', 'penalty'], dtype='object')




```python
df.values
```




    array([[2014, '홍길동', 1.5, nan],
           [2015, '이철수', 1.7, nan],
           [2016, '김영희', 3.9, nan],
           [2017, '박민수', 2.4, nan],
           [2018, '이철호', 2.9, nan]], dtype=object)




```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
      <th>points</th>
      <th>penalty</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2014</td>
      <td>홍길동</td>
      <td>1.5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2015</td>
      <td>이철수</td>
      <td>1.7</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>김영희</td>
      <td>3.9</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>박민수</td>
      <td>2.4</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2018</td>
      <td>이철호</td>
      <td>2.9</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 값 대입
df.penalty = 0.7

df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
      <th>points</th>
      <th>penalty</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2014</td>
      <td>홍길동</td>
      <td>1.5</td>
      <td>0.7</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2015</td>
      <td>이철수</td>
      <td>1.7</td>
      <td>0.7</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>김영희</td>
      <td>3.9</td>
      <td>0.7</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>박민수</td>
      <td>2.4</td>
      <td>0.7</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2018</td>
      <td>이철호</td>
      <td>2.9</td>
      <td>0.7</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['penalty'] = df['points'] - 1.0
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
      <th>points</th>
      <th>penalty</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2014</td>
      <td>홍길동</td>
      <td>1.5</td>
      <td>0.5</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2015</td>
      <td>이철수</td>
      <td>1.7</td>
      <td>0.7</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>김영희</td>
      <td>3.9</td>
      <td>2.9</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>박민수</td>
      <td>2.4</td>
      <td>1.4</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2018</td>
      <td>이철호</td>
      <td>2.9</td>
      <td>1.9</td>
    </tr>
  </tbody>
</table>
</div>




```python
# penalty 의 값을 리스트 값으로 변경
```


```python
df['penalty'] = [0.5, 0.7, 0.9, 1.0, 0.6]
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
      <th>points</th>
      <th>penalty</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2014</td>
      <td>홍길동</td>
      <td>1.5</td>
      <td>0.5</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2015</td>
      <td>이철수</td>
      <td>1.7</td>
      <td>0.7</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>김영희</td>
      <td>3.9</td>
      <td>0.9</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>박민수</td>
      <td>2.4</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2018</td>
      <td>이철호</td>
      <td>2.9</td>
      <td>0.6</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['age'] = [10, 20, 30, 24, 15]
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
      <th>points</th>
      <th>penalty</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2014</td>
      <td>홍길동</td>
      <td>1.5</td>
      <td>0.5</td>
      <td>10</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2015</td>
      <td>이철수</td>
      <td>1.7</td>
      <td>0.7</td>
      <td>20</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>김영희</td>
      <td>3.9</td>
      <td>0.9</td>
      <td>30</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>박민수</td>
      <td>2.4</td>
      <td>1.0</td>
      <td>24</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2018</td>
      <td>이철호</td>
      <td>2.9</td>
      <td>0.6</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 연습문제 : 급여를 (평균나이 x 100000(십만) x penalty)로 연산해서 pay 라는 칼럼으로 생성하시오
```


```python
import numpy as np
pay = np.mean(df['age']) * 100000 * df['penalty']
print(pay)
```

    one       990000.0
    two      1386000.0
    three    1782000.0
    four     1980000.0
    five     1188000.0
    Name: penalty, dtype: float64



```python
df['pay'] = pay
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
      <th>points</th>
      <th>penalty</th>
      <th>age</th>
      <th>pay</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2014</td>
      <td>홍길동</td>
      <td>1.5</td>
      <td>0.5</td>
      <td>10</td>
      <td>990000.0</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2015</td>
      <td>이철수</td>
      <td>1.7</td>
      <td>0.7</td>
      <td>20</td>
      <td>1386000.0</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>김영희</td>
      <td>3.9</td>
      <td>0.9</td>
      <td>30</td>
      <td>1782000.0</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>박민수</td>
      <td>2.4</td>
      <td>1.0</td>
      <td>24</td>
      <td>1980000.0</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2018</td>
      <td>이철호</td>
      <td>2.9</td>
      <td>0.6</td>
      <td>15</td>
      <td>1188000.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 연습문제 : age 칼럼에서 나이가 19세 이상이면 성년, 이하이면 미성년으로 구분하여
# df['division'] 이란 칼럼으로 저장하시오
```


```python
res = []
for i in df['age'] > 19:
    if i == True:
        res.append('성인')
    else:
        res.append('미성년')
        
res
```




    ['미성년', '성인', '성인', '성인', '미성년']




```python
df['division'] = res

df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
      <th>points</th>
      <th>penalty</th>
      <th>age</th>
      <th>pay</th>
      <th>division</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2014</td>
      <td>홍길동</td>
      <td>1.5</td>
      <td>0.5</td>
      <td>10</td>
      <td>990000.0</td>
      <td>미성년</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2015</td>
      <td>이철수</td>
      <td>1.7</td>
      <td>0.7</td>
      <td>20</td>
      <td>1386000.0</td>
      <td>성인</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>김영희</td>
      <td>3.9</td>
      <td>0.9</td>
      <td>30</td>
      <td>1782000.0</td>
      <td>성인</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>박민수</td>
      <td>2.4</td>
      <td>1.0</td>
      <td>24</td>
      <td>1980000.0</td>
      <td>성인</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2018</td>
      <td>이철호</td>
      <td>2.9</td>
      <td>0.6</td>
      <td>15</td>
      <td>1188000.0</td>
      <td>미성년</td>
    </tr>
  </tbody>
</table>
</div>




```python
# apply 함수를 사용하기 위한 기본 형식 틀

def myfunc2(age):
    print(age)
    return '성년'

df['구분2'] = df.apply(lambda x : myfunc2(x['age']),axis=1)
```

    10
    20
    30
    24
    15



```python
def myfunc2(age):
    msg = ''
    if age > 19:
        msg = '성년'
    else:
        msg = '미성년'
    return msg

df['구분2'] = df.apply(lambda x : myfunc2(x['age']),axis=1)
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
      <th>points</th>
      <th>penalty</th>
      <th>age</th>
      <th>pay</th>
      <th>division</th>
      <th>구분2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2014</td>
      <td>홍길동</td>
      <td>1.5</td>
      <td>0.5</td>
      <td>10</td>
      <td>990000.0</td>
      <td>미성년</td>
      <td>미성년</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2015</td>
      <td>이철수</td>
      <td>1.7</td>
      <td>0.7</td>
      <td>20</td>
      <td>1386000.0</td>
      <td>성인</td>
      <td>성년</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>김영희</td>
      <td>3.9</td>
      <td>0.9</td>
      <td>30</td>
      <td>1782000.0</td>
      <td>성인</td>
      <td>성년</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>박민수</td>
      <td>2.4</td>
      <td>1.0</td>
      <td>24</td>
      <td>1980000.0</td>
      <td>성인</td>
      <td>성년</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2018</td>
      <td>이철호</td>
      <td>2.9</td>
      <td>0.6</td>
      <td>15</td>
      <td>1188000.0</td>
      <td>미성년</td>
      <td>미성년</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 칼럼 삭제 del
del df['age']
del df['division']
del df['구분2']
```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
      <th>points</th>
      <th>penalty</th>
      <th>pay</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2014</td>
      <td>홍길동</td>
      <td>1.5</td>
      <td>0.5</td>
      <td>990000.0</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2015</td>
      <td>이철수</td>
      <td>1.7</td>
      <td>0.7</td>
      <td>1386000.0</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>김영희</td>
      <td>3.9</td>
      <td>0.9</td>
      <td>1782000.0</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>박민수</td>
      <td>2.4</td>
      <td>1.0</td>
      <td>1980000.0</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2018</td>
      <td>이철호</td>
      <td>2.9</td>
      <td>0.6</td>
      <td>1188000.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 인덱스 출력
df[0:2]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
      <th>points</th>
      <th>penalty</th>
      <th>pay</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2014</td>
      <td>홍길동</td>
      <td>1.5</td>
      <td>0.5</td>
      <td>990000.0</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2015</td>
      <td>이철수</td>
      <td>1.7</td>
      <td>0.7</td>
      <td>1386000.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# loc : 특정 행을 출력, loc[행범위,열범위] ****
df.loc["two"]
```




    year            2015
    names            이철수
    points           1.7
    penalty          0.7
    pay        1.386e+06
    Name: two, dtype: object




```python
df.loc["two":"four"] # two ~ four
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
      <th>points</th>
      <th>penalty</th>
      <th>pay</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>two</th>
      <td>2015</td>
      <td>이철수</td>
      <td>1.7</td>
      <td>0.7</td>
      <td>1386000.0</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>김영희</td>
      <td>3.9</td>
      <td>0.9</td>
      <td>1782000.0</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>박민수</td>
      <td>2.4</td>
      <td>1.0</td>
      <td>1980000.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.loc[:,['year','names']]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2014</td>
      <td>홍길동</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2015</td>
      <td>이철수</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>김영희</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>박민수</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2018</td>
      <td>이철호</td>
    </tr>
  </tbody>
</table>
</div>




```python
# loc : 문자 인덱스
# iloc : 숫자 인덱스
df.loc['four']
```




    year           2017
    names           박민수
    points          2.4
    penalty           1
    pay        1.98e+06
    Name: four, dtype: object




```python
df.iloc[3]
```




    year           2017
    names           박민수
    points          2.4
    penalty           1
    pay        1.98e+06
    Name: four, dtype: object




```python
# 오리지널
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
      <th>points</th>
      <th>penalty</th>
      <th>pay</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2014</td>
      <td>홍길동</td>
      <td>1.5</td>
      <td>0.5</td>
      <td>990000.0</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2015</td>
      <td>이철수</td>
      <td>1.7</td>
      <td>0.7</td>
      <td>1386000.0</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>김영희</td>
      <td>3.9</td>
      <td>0.9</td>
      <td>1782000.0</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>박민수</td>
      <td>2.4</td>
      <td>1.0</td>
      <td>1980000.0</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2018</td>
      <td>이철호</td>
      <td>2.9</td>
      <td>0.6</td>
      <td>1188000.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# df.iloc[행범위, 열범위] start:end => start ~ end-1
df.iloc[3:5,0:2]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>박민수</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2018</td>
      <td>이철호</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 전체 행에서 1~3 열을 출력 => iloc 사용
df.iloc[:,1:4]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>names</th>
      <th>points</th>
      <th>penalty</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>홍길동</td>
      <td>1.5</td>
      <td>0.5</td>
    </tr>
    <tr>
      <th>two</th>
      <td>이철수</td>
      <td>1.7</td>
      <td>0.7</td>
    </tr>
    <tr>
      <th>three</th>
      <td>김영희</td>
      <td>3.9</td>
      <td>0.9</td>
    </tr>
    <tr>
      <th>four</th>
      <td>박민수</td>
      <td>2.4</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>five</th>
      <td>이철호</td>
      <td>2.9</td>
      <td>0.6</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.iloc[1,1]
```




    '이철수'




```python
# 연도가 2016 보다 큰 행만 출력
df[df['year'] > 2016]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
      <th>points</th>
      <th>penalty</th>
      <th>pay</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>박민수</td>
      <td>2.4</td>
      <td>1.0</td>
      <td>1980000.0</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2018</td>
      <td>이철호</td>
      <td>2.9</td>
      <td>0.6</td>
      <td>1188000.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 오리지널
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
      <th>points</th>
      <th>penalty</th>
      <th>pay</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2014</td>
      <td>홍길동</td>
      <td>1.5</td>
      <td>0.5</td>
      <td>990000.0</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2015</td>
      <td>이철수</td>
      <td>1.7</td>
      <td>0.7</td>
      <td>1386000.0</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>김영희</td>
      <td>3.9</td>
      <td>0.9</td>
      <td>1782000.0</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>박민수</td>
      <td>2.4</td>
      <td>1.0</td>
      <td>1980000.0</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2018</td>
      <td>이철호</td>
      <td>2.9</td>
      <td>0.6</td>
      <td>1188000.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 연도가 2016 보다 큰 행만 출력
# loc 로 변경해서 적용해보기
# loc[행범위,열범위] ****

df[df.loc[:,'year'] > 2016]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
      <th>points</th>
      <th>penalty</th>
      <th>pay</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>박민수</td>
      <td>2.4</td>
      <td>1.0</td>
      <td>1980000.0</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2018</td>
      <td>이철호</td>
      <td>2.9</td>
      <td>0.6</td>
      <td>1188000.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[(df['year'] > 2016) & (df['year'] < 2018)]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
      <th>points</th>
      <th>penalty</th>
      <th>pay</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>박민수</td>
      <td>2.4</td>
      <td>1.0</td>
      <td>1980000.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[(df['year'] == 2017) | (df['year'] == 2018)]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
      <th>points</th>
      <th>penalty</th>
      <th>pay</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>박민수</td>
      <td>2.4</td>
      <td>1.0</td>
      <td>1980000.0</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2018</td>
      <td>이철호</td>
      <td>2.9</td>
      <td>0.6</td>
      <td>1188000.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 오리지널
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
      <th>points</th>
      <th>penalty</th>
      <th>pay</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>2014</td>
      <td>홍길동</td>
      <td>1.5</td>
      <td>0.5</td>
      <td>990000.0</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2015</td>
      <td>이철수</td>
      <td>1.7</td>
      <td>0.7</td>
      <td>1386000.0</td>
    </tr>
    <tr>
      <th>three</th>
      <td>2016</td>
      <td>김영희</td>
      <td>3.9</td>
      <td>0.9</td>
      <td>1782000.0</td>
    </tr>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>박민수</td>
      <td>2.4</td>
      <td>1.0</td>
      <td>1980000.0</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2018</td>
      <td>이철호</td>
      <td>2.9</td>
      <td>0.6</td>
      <td>1188000.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 2016 ~ 2019 사이의 데이터를 출력하시오. 단 loc를 사용해서 출력
# loc[행범위,열범위] ****

df[(df.loc[:,'year'] > 2016) & (df.loc[:,'year'] < 2019)]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>names</th>
      <th>points</th>
      <th>penalty</th>
      <th>pay</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>four</th>
      <td>2017</td>
      <td>박민수</td>
      <td>2.4</td>
      <td>1.0</td>
      <td>1980000.0</td>
    </tr>
    <tr>
      <th>five</th>
      <td>2018</td>
      <td>이철호</td>
      <td>2.9</td>
      <td>0.6</td>
      <td>1188000.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 결측치
"""
- 결측값이 있는지 여부 확인: isnull(), notnull()
- 열별 결측값 갯수 : df.isnull().sum()
- 행별 결측값 갯수 : df.isnull().sum(1)
"""

# step 1 결측치가 있는 데이터 만들기
import pandas as pd

df_left = pd.DataFrame({'KEY': ['Key0', 'Key1', 'Key2', 'Key3'],\

'사용자': ['홍길동', '이순자', '왕서방', '영심이'],

'치수': [0.5, 2.2, 3.6, 0.4]})

df_right = pd.DataFrame({'KEY': ['Key2', 'Key3', 'Key4', 'Key5'],\

'CType': ['C2', 'C3', 'C4', 'C5'],\

'Dtype': ['D2', 'D3', 'D4', 'D5']})


```


```python
df_left
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>KEY</th>
      <th>사용자</th>
      <th>치수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Key0</td>
      <td>홍길동</td>
      <td>0.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Key1</td>
      <td>이순자</td>
      <td>2.2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Key2</td>
      <td>왕서방</td>
      <td>3.6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Key3</td>
      <td>영심이</td>
      <td>0.4</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_right
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>KEY</th>
      <th>CType</th>
      <th>Dtype</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Key2</td>
      <td>C2</td>
      <td>D2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Key3</td>
      <td>C3</td>
      <td>D3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Key4</td>
      <td>C4</td>
      <td>D4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Key5</td>
      <td>C5</td>
      <td>D5</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_left.shape
```




    (4, 3)




```python
df_right.shape
```




    (4, 3)




```python
df_right.isnull().sum()
```




    KEY      0
    CType    0
    Dtype    0
    dtype: int64




```python
pd.merge(df_left, df_right)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>KEY</th>
      <th>사용자</th>
      <th>치수</th>
      <th>CType</th>
      <th>Dtype</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Key2</td>
      <td>왕서방</td>
      <td>3.6</td>
      <td>C2</td>
      <td>D2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Key3</td>
      <td>영심이</td>
      <td>0.4</td>
      <td>C3</td>
      <td>D3</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.merge(df_left, df_right, how='outer') # 키가 하나만 존재해도 outerjoin
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>KEY</th>
      <th>사용자</th>
      <th>치수</th>
      <th>CType</th>
      <th>Dtype</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Key0</td>
      <td>홍길동</td>
      <td>0.5</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Key1</td>
      <td>이순자</td>
      <td>2.2</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Key2</td>
      <td>왕서방</td>
      <td>3.6</td>
      <td>C2</td>
      <td>D2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Key3</td>
      <td>영심이</td>
      <td>0.4</td>
      <td>C3</td>
      <td>D3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Key4</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>C4</td>
      <td>D4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Key5</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>C5</td>
      <td>D5</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_all = pd.merge(df_left, df_right, how='outer', on='KEY') # on 기준 열

df_all
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>KEY</th>
      <th>사용자</th>
      <th>치수</th>
      <th>CType</th>
      <th>Dtype</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Key0</td>
      <td>홍길동</td>
      <td>0.5</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Key1</td>
      <td>이순자</td>
      <td>2.2</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Key2</td>
      <td>왕서방</td>
      <td>3.6</td>
      <td>C2</td>
      <td>D2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Key3</td>
      <td>영심이</td>
      <td>0.4</td>
      <td>C3</td>
      <td>D3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Key4</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>C4</td>
      <td>D4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Key5</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>C5</td>
      <td>D5</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 오리지널
df_all
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>KEY</th>
      <th>사용자</th>
      <th>치수</th>
      <th>CType</th>
      <th>Dtype</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Key0</td>
      <td>홍길동</td>
      <td>0.5</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Key1</td>
      <td>이순자</td>
      <td>2.2</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Key2</td>
      <td>왕서방</td>
      <td>3.6</td>
      <td>C2</td>
      <td>D2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Key3</td>
      <td>영심이</td>
      <td>0.4</td>
      <td>C3</td>
      <td>D3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Key4</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>C4</td>
      <td>D4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Key5</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>C5</td>
      <td>D5</td>
    </tr>
  </tbody>
</table>
</div>




```python
def df_allData(df_alls):
    datalistv = []
    data_lenv = len(df_alls)
    # keyv = input('Key => ')
    userv = input('사용자 =>') # 콘솔 입력
    sizev = float(input('치수 =>')) # 콘솔 입력
    datalistv.append('Key'+str(data_lenv))
    datalistv.append(userv)
    datalistv.append(sizev)
    datalistv.append('C'+str(data_lenv))
    datalistv.append('D'+str(data_lenv))
    df_alls.loc[data_lenv] = datalistv
```


```python
df_allData(df_all)
```

    사용자 =>이수진
    치수 =>7.0



```python
df_all
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>KEY</th>
      <th>사용자</th>
      <th>치수</th>
      <th>CType</th>
      <th>Dtype</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Key0</td>
      <td>홍길동</td>
      <td>0.5</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Key1</td>
      <td>이순자</td>
      <td>2.2</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Key2</td>
      <td>왕서방</td>
      <td>3.6</td>
      <td>C2</td>
      <td>D2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Key3</td>
      <td>영심이</td>
      <td>0.4</td>
      <td>C3</td>
      <td>D3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Key4</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>C4</td>
      <td>D4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Key5</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>C5</td>
      <td>D5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Key6</td>
      <td>이수진</td>
      <td>7.0</td>
      <td>C6</td>
      <td>D6</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 사용자 => User, 치수 => Size
df_all.columns = ['KEY', 'User', 'Size', 'CType', 'DType']
df_all
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>KEY</th>
      <th>User</th>
      <th>Size</th>
      <th>CType</th>
      <th>DType</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Key0</td>
      <td>홍길동</td>
      <td>0.5</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Key1</td>
      <td>이순자</td>
      <td>2.2</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Key2</td>
      <td>왕서방</td>
      <td>3.6</td>
      <td>C2</td>
      <td>D2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Key3</td>
      <td>영심이</td>
      <td>0.4</td>
      <td>C3</td>
      <td>D3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Key4</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>C4</td>
      <td>D4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Key5</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>C5</td>
      <td>D5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Key6</td>
      <td>이수진</td>
      <td>7.0</td>
      <td>C6</td>
      <td>D6</td>
    </tr>
  </tbody>
</table>
</div>




```python
!pip list | grep missiingno
```


```python
!pip install missingno
```

    Collecting missingno
      Downloading https://files.pythonhosted.org/packages/2b/de/6e4dd6d720c49939544352155dc06a08c9f7e4271aa631a559dfbeaaf9d4/missingno-0.4.2-py3-none-any.whl
    Requirement already satisfied: scipy in /home/kosmo1/anaconda3/lib/python3.7/site-packages (from missingno) (1.4.1)
    Requirement already satisfied: seaborn in /home/kosmo1/anaconda3/lib/python3.7/site-packages (from missingno) (0.9.0)
    Requirement already satisfied: numpy in /home/kosmo1/anaconda3/lib/python3.7/site-packages (from missingno) (1.16.4)
    Requirement already satisfied: matplotlib in /home/kosmo1/anaconda3/lib/python3.7/site-packages (from missingno) (3.1.0)
    Requirement already satisfied: pandas>=0.15.2 in /home/kosmo1/anaconda3/lib/python3.7/site-packages (from seaborn->missingno) (0.24.2)
    Requirement already satisfied: cycler>=0.10 in /home/kosmo1/anaconda3/lib/python3.7/site-packages (from matplotlib->missingno) (0.10.0)
    Requirement already satisfied: kiwisolver>=1.0.1 in /home/kosmo1/anaconda3/lib/python3.7/site-packages (from matplotlib->missingno) (1.1.0)
    Requirement already satisfied: pyparsing!=2.0.4,!=2.1.2,!=2.1.6,>=2.0.1 in /home/kosmo1/anaconda3/lib/python3.7/site-packages (from matplotlib->missingno) (2.4.0)
    Requirement already satisfied: python-dateutil>=2.1 in /home/kosmo1/anaconda3/lib/python3.7/site-packages (from matplotlib->missingno) (2.8.0)
    Requirement already satisfied: pytz>=2011k in /home/kosmo1/anaconda3/lib/python3.7/site-packages (from pandas>=0.15.2->seaborn->missingno) (2019.1)
    Requirement already satisfied: six in /home/kosmo1/anaconda3/lib/python3.7/site-packages (from cycler>=0.10->matplotlib->missingno) (1.12.0)
    Requirement already satisfied: setuptools in /home/kosmo1/anaconda3/lib/python3.7/site-packages (from kiwisolver>=1.0.1->matplotlib->missingno) (41.0.1)
    Installing collected packages: missingno
    Successfully installed missingno-0.4.2



```python
import missingno as msno
msno.matrix(df_all,figsize=(18,6))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7effd65f9978>




![output_87_1](https://user-images.githubusercontent.com/34564706/94126513-abd89680-fe92-11ea-9084-e845847c745b.png)




```python
df_all.isnull().sum()
```




    KEY      0
    User     2
    Size     2
    CType    2
    DType    2
    dtype: int64




```python
# 오리지널
df_all
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>KEY</th>
      <th>User</th>
      <th>Size</th>
      <th>CType</th>
      <th>DType</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Key0</td>
      <td>홍길동</td>
      <td>0.5</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Key1</td>
      <td>이순자</td>
      <td>2.2</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Key2</td>
      <td>왕서방</td>
      <td>3.6</td>
      <td>C2</td>
      <td>D2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Key3</td>
      <td>영심이</td>
      <td>0.4</td>
      <td>C3</td>
      <td>D3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Key4</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>C4</td>
      <td>D4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Key5</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>C5</td>
      <td>D5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Key6</td>
      <td>이수진</td>
      <td>7.0</td>
      <td>C6</td>
      <td>D6</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_all.isnull()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>KEY</th>
      <th>User</th>
      <th>Size</th>
      <th>CType</th>
      <th>DType</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>5</th>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>6</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>


