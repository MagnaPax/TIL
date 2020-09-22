
# session 을 이용해서 정보 확인 후 중복 여부 확인하기

![20200922_102510](https://user-images.githubusercontent.com/34564706/93852272-b822ef00-fcec-11ea-8a9a-a74bf3d4332c.jpg)



## 로그인


### 브라우저에 주소 입력됨
http://내ip주소:9000/login/


### config/urls.py 확인
- 아래에 코드에 따라 login/urls 파일로 이동

```py
urlpatterns = [ 
    path('login/', include('login.urls')),
]
```

### login/urls.py
- 아래 코드에 따라 login/views.py 파일의 main 메소드로 이동

```py
urlpatterns = [
    path("", views.main),
]
```


### login/views.py
- 다음 메소드 정의에 따라 templates/login/index.html 로 이동

```py
def main(request):
    return render(request, 'login/index.html')
```

### templates/login/index.html
- 로그인 글자를 누르면 loginform 로 이동

```html
<li><a href="loginform">로그인</a></li>
```

### login/urls.py
- 아래 코드에 따라 login/views.py 파일의 loginform 메소드로 이동

```py
urlpatterns = [    
    path('loginform', views.loginform),
```

### login/views.py
- POST 방식으로 넘어온 값들이 없기 때문에 메소드의 맨 마지막줄 실행
- templates/login/login.html 로 이동
```py
@csrf_protect
def loginform(request):
    ...
    ...
    return render(request, "login/login.html")
```


### templates/login/login.html
- 로그인 버튼을 누르면 form 태그의 action 에 의해 loginform 로 이동. action이 없으면 원래 있던 곳으로 이동
```html
...
...
<form  method="post" action="loginform">
    {% csrf_token %}
...
...
        <input type="submit" value="로그인" class="primary">
```


### login/urls.py
- 아래 코드에 따라 login/views.py 파일의 loginform 메소드로 이동

```py
urlpatterns = [    
    path('loginform', views.loginform),
```


### login/views.py
- 위에서 값들이 POST 방식으로 넘어왔기 때문에 아래 if 문 실행됨
- getLoginChk() 메소드를 키워드=특정값 형태로 호출. models.py 파일에 있음.
```py
@csrf_protect
def loginform(request):
    ...
    ...
    if request.method == 'POST':
        user_id = request.POST['id']
    ...
    ...
        res = getLoginChk(id=user_id, pwd=user_pwd)
```


### login/models.py
- **kwargs : 딕셔너리 {'키워드':'특정 값'} 형태로 내부로 전달됨
- 쿼리문에 의해 id 와 pwd 값을 오라클 DB 에서 검색한 뒤 가져옴

```py
def getLoginChk(**kwargs):
```


### login/views.py
- getLoginChk() 메소드에 의해 반환된 값과 
- templates/login/login.html 에서 넘어온 user_id , user_pwd 값들과 비교 후
- 로그인이 성공했으면 
```py
return redirect("/login")
```

- 로그인이 실패했으면
```py
return render(request, "login/login.html", {"error": msg})
```

<br>

=========================================================================================
=========================================================================================

## 로그아웃

### templates/login/login.html
- 로그아웃 클릭되면 logout 로 이동
```html
<li><a href="logout">로그아웃</a></li>
```

### login/urls.py
- 아래 코드에 따라 login/views.py 파일의 logout 메소드로 이동

```py
urlpatterns = [
    path('loginform', views.logout),
```


### login/views.py
- session 을 삭제하고 
- http://내ip주소:9000/login/ 로 리다이렉트 됨
```py
def logout(request):
    del request.session['user_id']
    del request.session['user_name']
    return redirect("/login")
```
