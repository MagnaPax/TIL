
# 1. 가장 단순한 웹앱 만들기

### 가상환경 활성화 (자동 완성이 된다)
```
$ source 가상환경이름/Scripts/activate
```

### 웹 앱 생성
```console
python manage.py startapp myapp
```

### config/settings.py에 내 웹앱 등록

ALLOWED_HOSTS 이런것들도 해줘야 됨

```py
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'address',
    'myapp',
    'survey',
]
```

### model.py 설정
```py
from django.db import models


class Survey(models.Model):
    # 설문 인덱스(자동 필드 증가)
    survey_idx = models.AutoField(primary_key=True)
    # 설문 문제
    question = models.TextField(null=True)
    # 답 1~4
    ans1 = models.TextField(null=True)
    ans2 = models.TextField(null=True)
    ans3 = models.TextField(null=True)
    ans4 = models.TextField(null=True)
    # 설문진행상태(y = 진행중, n = 종료)
    status = models.CharField(max_length=1, default="y")


class Answer(models.Model):
    # 응답 아이디(자동 필드 증가)
    answer_idx = models.AutoField(primary_key=True)
    # 설문 아이디
    survey_idx = models.IntegerField()
    # 응답 번호
    num = models.IntegerField()

```


### admin.py 설정
```py
from django.contrib import admin

# Register your models here.

from survey.models import Survey, Answer
class SurveyAdmin(admin.ModelAdmin):
    list_display = ("question", "ans1", "ans2", "ans3", "ans4", "status")

admin.site.register(Survey, SurveyAdmin)
admin.site.register(Answer)
```

### db설정
> 파이썬이 db를 만질수 있는 코드를 생성하는 makemigrations

> 생성된 코드로 직접 db를 만지는 것이 migrate

![db설정](https://user-images.githubusercontent.com/34564706/93316785-9ab2d880-f847-11ea-8e45-d29dd1176adc.png)


```console
(base) kosmo1@kosmo1-VirtualBox:~/PycharmProjects/myweb$ python manage.py makemigrations
Migrations for 'survey':
  survey/migrations/0001_initial.py
    - Create model Answer
    - Create model Survey
(base) kosmo1@kosmo1-VirtualBox:~/PycharmProjects/myweb$ python manage.py migrate
Operations to perform:
  Apply all migrations: address, admin, auth, contenttypes, myapp, sessions, survey
Running migrations:
  Applying survey.0001_initial... OK

```


### urls.py 생성
```py
from django.contrib import admin
from django.urls import path

from survey import views

urlpatterns = [
    # 주소창에 http://localhost/survey/ 입력되면 views 파일 안의 home 메소드를 읽어라.
    # home 메소드 안에는 list.html 을 읽으라고 되어있음
    # http://localhost/survey/ ==> views.home() ==> templates/survey/list.html
    path('', views.home),
]
```

### views.py 
```py
from django.shortcuts import render

def home(request):
    # templates/survey/list.html 로 이동해라
    return render(request, "survey/list.html")

```

### templates/survey/list.html 생성

![list html생성](https://user-images.githubusercontent.com/34564706/93316861-b1592f80-f847-11ea-8381-b475dd25d853.png)


```html
<!DOCTYPE html>
<html lang="kr">
<head>
    <meta charset="UTF-8">
    <title>온라인 설문조사</title>
</head>
<body>
우하하
</body>
</html>
```


### config/urls.py 에 내 웹앱 urls 등록
```py
from django.contrib import admin
from django.urls import path, include


urlpatterns = [
    path('survey/', include('survey.urls')),
]
```

### 결과

![브라우저캡쳐](https://user-images.githubusercontent.com/34564706/93316938-c930b380-f847-11ea-8986-84b46c5b0931.png)


<br><br><br><br>


# 2. DB 연결하고 DB 자료 브라우저에 보여주기

### survey/list.html 수정
```py
<body>
<form method="post" action="save_survey" > <!--투표 버튼을 누르면 post방식으로 views.py 에 있는 save_survey 로 이동-->
    <!-- 변조 방지 위해. 소스 보기로 하면 아래같은 암호같은 것으로 바뀌어 있음 -->
    <!-- <input type="hidden" name="csrfmiddlewaretoken" value="vSSzB7XOFgK3eeLk9zzv2vKrlgRWDhDy3MbbBV27QS0WQQvtiUXhkdhS6zfhnJxe"> -->
    {% csrf_token %}
    <p>{{survey.question}}</p>
    <p><input type="radio" name="num" value="1">{{survey.ans1}}</p>
    <p><input type="radio" name="num" value="2">{{survey.ans2}}</p>
    <p><input type="radio" name="num" value="3">{{survey.ans3}}</p>
    <p><input type="radio" name="num" value="4">{{survey.ans4}}</p>
    <p>
        <input type="hidden" name="survey_idx" value="{{survey.survey_idx}}">
        <input type="submit" value="투표">
        <input type="button" value="결과확인" onclick="show_result()">
    </p>
</form>
<script>
    function show_result(){
        location.href="show_result?survey_idx={{survey.survey_idx}}";
    }
</script>
</body>
```


### views.py 수정
```py
from django.shortcuts import render
from django.views.decorators.csrf import csrf_protect

from survey.models import Survey, Answer


def home(request):
    # Survey.objects : 모든 레코드를 의미, filter 조건(where 절에 해당) 즉 status 가 y 인 모든 레코드
    # order_by 필드명 앞에 -는 내림차순을 의미한다.
    # [0] 레코드중 첫번째 요소 [0번째 인덱스]
    survey = Survey.objects.filter(status="y").order_by("-survey_idx")[0]

    # templates/survey/list.html 로 이동해라. 위 조건에 해당되는 레코드와 함
    return render(request, "survey/list.html", {"survey": survey})


@csrf_protect
def save_survey(request):
    # 문제 번호와 응답번호를 Answer 객체에 저장한다.
    survey_idx = request.POST["surve께y_idx"]
    print("타입: ", type(survey_idx))
    dto = Answer(survey_idx=int(request.POST["survey_idx"]), num=request.POST["num"])
    # insert query 가 호출이 됨(db에 저장됨)
    dto.save()
    # success.html로 이동한다
    return render(request, "survey/success.html")

```

### url.py 수정
```py
urlpatterns = [
    # 주소창에 http://localhost/survey/ 입력되면 views 파일 안의 home 메소드를 읽어라.
    # home 메소드 안에는 list.html 을 읽으라고 되어있음
    # http://localhost/survey/ ==> views.home() ==> templates/survey/list.html
    path('', views.home),

    # http://localhost/survey/save_survey ==> views.save_survey() ==> templates/survey/success.html
    path('save_survey', views.save_survey),
]

```


### static에 이미지 넣기
- survey/static/img 폴더 만들고 사진파일 넣기

![static에이미지넣기](https://user-images.githubusercontent.com/34564706/93317169-1b71d480-f848-11ea-94c0-7e5bedd95ac5.png)



### survey/success.html 생성
```html
<!DOCTYPE html>
<html lang="kr">
<!--static 폴더를 읽어라-->
{% load static %}
<!--static 폴더를 baseUrl 로 지정-->
{% static "" as baseUrl %}
<head>
    <meta charset="UTF-8">
    <title>success.html</title>
</head>
<body>
    <div>
        <img src="{{baseUrl}}/img/ocean.jpg">
        <p>Success!</p>
    </div>
</body>
</html>
```


### views.py 수정
- show_result() 추가

```py
def show_result(request):
    # 문제 번호
    idx = request.GET["survey_idx"]
    # select * from survey where survey_idx=1 과 같다
    ans = Survey.objects.get(survey_idx=idx)
    # 각 문장에 대한 값으로 리스트를 만들어 놓는다
    answer = [ans.ans1, ans.ans2, ans.ans3, ans.ans4]
    # Survey.objects.raw(""" SQL문 """, param)
    surveyList = Survey.objects.raw("""
    select survey_idx, num, count(num) sum_num from survey_answer where survey_idx=%s
    group by survey_idx, num order by num
    """, idx)
    # 동일한 개수로 이루어진 자료형을 묶어 주는 역할을 하는 함수
    '''
    list(zip([1,2,3], [4,5,6]))
    ==> [(1,4), (2,5), (3,6)]
    '''
    surveyList = zip(surveyList, answer)
    return render(request, "survey/result.html", {'surveyList': surveyList})
```


### urls.py 수정
- survey/show_result 일 때 추가

```py

from django.contrib import admin
from django.urls import path
from survey import views

urlpatterns = [
    # 주소창에 http://localhost/survey/ 입력되면 views 파일 안의 home 메소드를 읽어라.
    # home 메소드 안에는 list.html 을 읽으라고 되어있음
    # http://localhost/survey/ ==> views.home() ==> templates/survey/list.html
    path('', views.home),

    # http://localhost/survey/save_survey ==> views.save_survey() ==> templates/survey/success.html
    path('save_survey', views.save_survey),

    # http://localhost/survey/show_result ==> views.show_result() ==> templates/survey/result.html
    path('show_result', views.show_result),
]
```


### result.html 작성
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>설문조사 결과</title>
</head>
<body>
    <h1>설문조사 결과</h1>
<!--    <table border="1" style="width:400px">-->
    <table border="1">
        <tr style="background:pink">
            <th>문항</th>
            <th>응답수</th>
        </tr>
        <tr><td colspan="2">{{surveyList}}</td></tr>
        {% for row,ans in surveyList %}
        <tr>
            <td>{{ans}}</td>
            <td>{{row.sum_num}}</td>
        </tr>
        {% endfor %}
    </table>

</body>
</html>
```
