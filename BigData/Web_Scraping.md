# 크롤링 순서
1. url 확보
2. HTML 존재 여부 확인 - 목표하는 텍스트 존재 여부
3. 해당 요소 검색 - 핵심ID, 클래스 태그를 찾아냄 articleBodyContents
4. 추출 데이터로 데이터베이스화



```py
import requests # HTML 가져오기
from bs4 import BeautifulSoup
import numpy as np
import pandas as pd
```

### 1. url 확보
```py
url = "긁어올 웹페이지 주소"
req=requests.get(url)
```

### 2. HTML 존재 여부 확인
```py
html=req.text
#print(html[:100]) # 잘 긁어왔는지 확인
```

### 3. 해당 요소 검색 - 핵심ID, 클래스 태그를 찾아냄 articleBodyContents
```py
soup=BeautifulSoup(html,'html.parser')
# CSS 셀렉터를 활용. 해당요소 확인 - 리스트 형태로 추출
tgt=soup.select('#articleBodyContents') # articleBodyContents라는 아이디 만약 클래스라면 .articleBodyContents로 찾기
txt=tgt[0].get_text()
```