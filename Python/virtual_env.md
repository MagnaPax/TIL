# Python 가상환경

https://www.youtube.com/watch?v=nO3csmVyoOQ&t=78s


## 가상환경 생성
> 가상환경 이름 앞에 `.`을 붙여서 이 폴더가 일반적인 폴더가 아니라는 구분을 해주는 게 좋다.
```
$ python -m venv 가상환경이름
```
![image](https://user-images.githubusercontent.com/34564706/100180364-56187d00-2f1b-11eb-8ed0-d1c414b158db.png)


## vscode 열기
```
$ code .
```
- vscde 의 터미널을 bash로 바꾸기

![image](https://user-images.githubusercontent.com/34564706/100179751-fbcaec80-2f19-11eb-8424-17d56d3f8fbb.png)


## 가상환경 활성화
```
$ source 가상환경이름/Scripts/activate
```
![virtualenv](https://user-images.githubusercontent.com/34564706/100180651-eeaefd00-2f1b-11eb-96ba-c65e853209c2.jpg)


- `(.ch_venv)` 이 표시되면서 가상환경이 활성화 된 것에 주목

![virtualenv2](https://user-images.githubusercontent.com/34564706/100180748-36ce1f80-2f1c-11eb-9e63-068209bfe446.jpg)

- 어떤 명령어를 치든 `(가상환경이름)` 이 같이 나오면서 가상환경이 활성화 된 것이 나타나야 됨. 
- 작업하는 내내 가상환경이 활성화 된 상태에서 해야 됨.

## 작업 폴더 위치
> 작업 폴더는 가상환경 폴더 밖에 위치시켜야 됨

![image](https://user-images.githubusercontent.com/34564706/100181022-b9ef7580-2f1c-11eb-8cd3-40b896da141d.png)


## Interpreter 선택
> 컴퓨터에 설치된 인터프리터가 아닌 가상환경에 설치된 인터프리터를 선택해야 팀원들과 공유 시 에러나지 않는다

```
Ctrl + Shipt + p
```
![image](https://user-images.githubusercontent.com/34564706/100181789-6bdb7180-2f1e-11eb-877f-4008c069616e.png)

![virtualenv3](https://user-images.githubusercontent.com/34564706/100181980-dab8ca80-2f1e-11eb-9160-85a7a419e276.jpg)

