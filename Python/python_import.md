

```py
""" test.py """

def div(a=0,b=1):
    if b==0:
        b=1
    return a/b

def mul(a=0,b=0):
    return a*b 

class Mycalc:
    pass

class Calc(Mycalc):
    def __init__(self,no=0,pno=0):
        self.result=no
        self.point=pno
        self.__inprivate__=1

    def add(self,src):
        self.result+=src
        return self.result

    def minus(self,src):
        self.result-=src
        return self.result
```

```py
# test의 이름을 t로 축약해서 사용
import test as t

# test 안의 div 함수를 d로 축약해서 사용
from test import div as d 

print("function output:",t.mul(2,3))
print("as call function:",d(6,5))

# make instance
c2=t.Calc()
print("class output:",c2.add(3))

```


![image](https://user-images.githubusercontent.com/34564706/91288009-6eb5b180-e7cb-11ea-841e-2b85d8f13807.png)


```py
"""testpack.py"""

def div(a=0,b=1):
    if b==0:
        b=1
    return a/b

def mul(a=0,b=0):
    return a*b 

class Mycalc:
    pass
# 
class Calc(Mycalc):
    def __init__(self,no=0,pno=0):
        self.result=no
        self.point=pno
        self.__inprivate__=1

    def add(self,src):
        self.result+=src
        return self.result

    def minus(self,src):
        self.result-=src
        return self.result
```

![image](https://user-images.githubusercontent.com/34564706/91288009-6eb5b180-e7cb-11ea-841e-2b85d8f13807.png)


```py
# __init__.py 파일을 만들면 그 폴더 안의 파일들을 패키지처럼 사용할 수 있게 한다

# myfolder 폴더 안의 testpack.py파일을 패키지처럼 받아서 tp로 축약해서 사용
import myfolder.testpack as tp

# myfolder 폴더 안의 testpack.py파일의 Calc 클래스를 ca 축약어로 사용
from myfolder.testpack import Calc as ca

print("packge:",tp.mul(2,3))
c1= ca()
print("package class import:",c1.add(4))

```

```py
```

```py
```

```py
```

