## 깃허브를 이용한 협업 개요

https://git-scm.com/book/ko/v2/GitHub-GitHub-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8%EC%97%90-%EA%B8%B0%EC%97%AC%ED%95%98%EA%B8%B0#ch06-github_flow

![Github_workflow_overview](https://user-images.githubusercontent.com/34564706/123540527-68d98580-d77a-11eb-816b-261cb891aa81.jpg)

# git 명령어

### clone

> 원격 레파지토리를 내 로컬에서 이용할 수 있도록 복사

```
git clone <레파지토리 주소>
```

### remote add

> 현재 디렉토리에 원격 저장소를 등록

```
git remote add <이 원격 저장소를 부를 이름(내맘대로 지정 가능)> <등록할 원격 저장소 주소>
```

### restore

> commit 되지 않은 변경사항 취소

```
git restore <파일명>
```

### reset

> 내 **로컬**에서 커밋한 내용을 취소

```
git reset HEAD^
```

### push

> 로컬에서 커밋된 사항을 원격 레파지토리에 업로드

```
git push <원격저장소이름(주소아님)> <업로드하기원하는브랜치이름>
```

## 충돌이 일어나는 경우

1. a가 10번 줄 수정 후 a의 원격 레파지토리에 push

2. b가 10번 줄 수정 후 자신의 로컬 레파지토리에 commit

3. b가 a의 원격 레파지토리를 pull <<<<<<<<<<<<<<<<< 이때 (<span style="color:red">충돌</span>) 발생

a가 b의 원격 레파지토리로부터 pull을 받아서 충돌이 난 뒤 해결을 하고
다시 자신의 로컬 레파지토리에 add와 commit을 한 뒤
또 다시 b의 원격 레파지토리로부터 pull을 받으면 pull이 동작을 하지 않음

```
PS E:\CodeStates\실습코드\05 [Git] 기초\im-sprint-simple-git-workflow> git pull 진성준 master
From https://github.com/Jin-sungjun/im-sprint-simple-git-workflow
 * branch            master     -> FETCH_HEAD
Already up to date.
```

충돌을 해결하고 난 뒤에도 add 해야 됨. 이것도 내용을 바꾼 것이기 때문
이후 그냥 git commit 하면 메세지가 자동으로 생성되고 그것이 싫으면 git commit -m 사용하여 메세지를 따로 입력할 수도 있다

## 충돌이 일어나지 않고 그냥 바뀌는 경우

- 이거 분명 목격했는데 어떨때 이렇게 되는지를 모르겠음

  <br>
  Full IM 31 김여현님이 모두에게: 05:28 PM
  그 말씀이 아니고, 한번 충돌 발생해서 병합을 수정한 파일에 다음번 풀에서 충돌이 날 경우를 말씀드린 거에요
