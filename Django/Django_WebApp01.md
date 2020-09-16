# Django 이용 간단한 게시판 만들기

## 1. DB 연결 않고 가장 간단하게 웹 페이지 표시하기

### Django 다운
```
pip install django
```

### 환경설정
- config 디렉토리 생성하는 명령어
- Django 프로젝트 시작할 때 맨 처음 딱 한번만 실행
- Spring의 WEB-INF 와 같은 웹 환경설정 역할, 즉 환경설정 파일들이 생긴다

```
django-admin startproject config .
```

### SQLite3 
- Django의 db는 기본적으로 SQLIte3
https://github.com/pawelsalawa/sqlitestudio/releases


### 수퍼 유저 생성(관리자)
```
python manage.py createsuperuser
```
명령어 실행한 뒤 아이디, 이메일, 비밀번호 설정


1. 웹 앱 생성
```
python manage.py startapp myapp
```

2. config/settings.py 설정

```py
ALLOWED_HOSTS = ['내 아이피 주소']
INSTALLED_APPS = ['생성한 웹앱 이름',]
LANGUAGE_CODE = 'ko'
TIME_ZONE = 'Asia/Seoul'
```


3. config/urls.py 에 내 웹앱 urls 등록
```py
from django.contrib import admin
from django.urls import path, include

from config import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', views.home),
    path('profile', views.profile),
    path('getdemo1', views.getdemo),
    path('address/', include('address.urls')),
    path('myapp/', include('myapp.urls')),
]
```


4. myapp/urls.py 에 모델(views) 등록
```py
from django.contrib import admin
from django.urls import path
from myapp import views

urlpatterns = [
    # 브라우저 주소창에 http://localhost/myapp/ 입력되면 views 파일 안의 home 메소드를 읽어라.
    path('', views.home),
]
```


5. myapp/views.py
- home 메소드 생성
```py
from django.shortcuts import render

def home(request):
    # templates/myapp/index.html 로 가라
    return render(request, "myapp/index.html")
```


6. 뷰 만들기
- myapp/templates/myapp/index.html 이 위치에 파일 만들기
```html
<!DOCTYPE html>
<html lang="kr">
<head>
    <meta charset="UTF-8">
    <title>내 장고 웹앱</title>
</head>
<body>
    <h1>내 장고 웹앱</h1>
</body>
</html>
```

서버 실행
```
python manage.py runserver '0.0.0.0:8181'
```

![스크린샷,_2020-09-15_19-42-27](https://user-images.githubusercontent.com/34564706/93323621-d05bbf80-f84f-11ea-8fd1-9b71e809765d.png)


<br><br><br>


## 2. DB 연결해서 DB내용 보여주기

7. model.py 설정
```py
class Post(models.Model):
    # 시퀀스 테이블
    idx = models.AutoField(primary_key=True) # 자동 필드 증가
    title = models.CharField(max_length=50, blank=True, null=False)
    content = models.TextField()
    author = models.TextField()
```


8. admin.py 설정
```py
from django.contrib import admin

from myapp.models import Post
# 관리자 화면에 출력할 필드 목록을 정의한다.
# 이때 번호는 자동증가를 설정했기 때문에 할 필요가 없다.

class PostAdmin(admin.ModelAdmin):

    list_display = ('title', 'content', 'author')

# 관리자 기능에 추가할 모델을 등록
admin.site.register(Post, PostAdmin)
```


9. db설정
> 파이썬이 db를 만질수 있는 코드를 생성하는 makemigrations

> 생성된 코드로 직접 db를 만지는 것이 migrate

![스크린샷,_2020-09-15_19-24-37](https://user-images.githubusercontent.com/34564706/93323981-43fdcc80-f850-11ea-8dd2-86c9677d3b80.png)

![스크린샷,_2020-09-15_19-25-37](https://user-images.githubusercontent.com/34564706/93324080-609a0480-f850-11ea-95dd-4169697326c0.png)



10. myapp/views.py 수정
- DB의 Post 테이블의 내용 리턴
```py
from django.shortcuts import render
from myapp.models import Post

def home(request):
    # .order_by('idx') : 오름차순
    # .order_by('-idx') : 내림차순
    # select * from address_address order by name asc or desc
    items = Post.objects.order_by('idx')

    # count value
    # Post 테이블의 레코드 갯수를 저장
    # select count(*) from address_address
    post_count = Post.objects.all().count()
    return render(request, "myapp/index.html", {'items': items, 'post_count': post_count})
```


11. index.html 수정
```html
<!DOCTYPE html>
<html lang="kr">
<head>
    <meta charset="UTF-8">
    <title>내 장고 웹앱</title>
</head>
<body>

    <h1>내 장고 웹앱</h1>
    <h2>총 게시물 갯수 : {{post_count}}</h2>

    <div>
        <table border="1" style="width:600px">
            <thead style="background:orange">
            <tr>
                <th>번호</th>
                <th>제목</th>
                <th>내용</th>
                <th>저자</th>
            </tr>
            </thead>
            <tbody>
            {% for e in items %}
                <tr>
                    <td>{{e.idx}}</td>
                    <td>{{e.title}}</td>
                    <td>{{e.content}}</td>
                    <td>{{e.author}}</td>
                </tr>
            {% endfor %}
            </tbody>
        </table>
    </div>

</body>
</html>
```


12. Post 테이블에 내용 넣기

![스크린샷,_2020-09-15_19-59-28](https://user-images.githubusercontent.com/34564706/93324568-12393580-f851-11ea-9201-8bd7df793a9b.png)


서버 실행
```
python manage.py runserver '0.0.0.0:원하는포트번호'
```


13. 바뀐 페이지

![스크린샷,_2020-09-15_20-00-46](https://user-images.githubusercontent.com/34564706/93324559-0f3e4500-f851-11ea-84ee-c714d5d8132a.png)
