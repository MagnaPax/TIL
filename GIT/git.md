# Version Control



## Git 최초 설정

1. 시스템의 모든 사용자와 모든 저장소에 적용하기
```
git config --system 옵션
```
2. 특정 사용자(즉 현재 사용자)의 모든 저장소 설정에 적용하기
```
git config --global 옵션
```
3. 특정 저장소(혹은 현재 작업 중인 프로젝트)에만 적용.
- 기본 옵션
```
git config --local 옵션
```


### 사용자 정보
- Git을 설치하고 나서 가장 먼저 해야 하는 것은 사용자이름과 이메일 주소를 설정하는 것이다. Git은 커밋할 때마다 이 정보를 사용한다. 한 번 커밋한 후에는 정보를 변경할 수 없다.

```
git config --global user.email "이메일 주소"
git config --global user.name "아이디"
```


## Add
```shell
git init

git pull origin master # 깃헙에 저장소 만들때 .gitignore과 README.md 만들었으니까 로컬에 받아오기 위해

git pull origin master --allow-unrelated-histories # Github에 있는 내용을 로컬 repository에 반영할 수 있게 하고, 초기 로컬 repository의 파일을 Github에 업로드하기 위해

git config --global user.email "이메일 주소"

git config --global user.name "아이디"

git remote add master 원격저장소주소

git add --all

git commit -m "initial commit"

git push origin master
```


## Clone
```
git clone 원격저장소주소
```
