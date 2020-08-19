## 주식 자동 매매 애플리케이션을 위한 db 설정

![image](https://user-images.githubusercontent.com/34564706/90243872-a0915480-de6a-11ea-85f5-c8fa710b679b.png)

![image](https://user-images.githubusercontent.com/34564706/90243921-b56de800-de6a-11ea-9b66-ea2c78119880.png)

![image](https://user-images.githubusercontent.com/34564706/90243944-c3236d80-de6a-11ea-9a77-84424fc0908b.png)

![image](https://user-images.githubusercontent.com/34564706/90243971-cfa7c600-de6a-11ea-9e38-aae045b57bbb.png)

![image](https://user-images.githubusercontent.com/34564706/90243987-d7676a80-de6a-11ea-8cb9-2cc629246b0b.png)


```py
import cx_Oracle
```

```py
## db 연결
uid = 'PROJECT1'
upw = 'Test1234'
url = 'localhost:1521/orcl'
conn = cx_Oracle.connect(uid,upw,url)
cursor=conn.cursor()
#conn
```