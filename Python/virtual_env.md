# Python 가상환경

https://www.youtube.com/watch?v=nO3csmVyoOQ&t=78s


## 가상환경 생성

```
$ python -m venv 가상환경이름
```
![image](https://user-images.githubusercontent.com/34564706/100174239-60347e80-2f0f-11eb-8beb-e1a200b2b637.png)

## vscode 열기
```
$ code .
```

## 가상환경 활성화
- 먼저 vscde 의 터미널을 bash로 바꿔줘야 됨
```
$ source 가상환경이름/Scripts/activate

```
![virtualenv](https://user-images.githubusercontent.com/34564706/100174659-2f087e00-2f10-11eb-8498-f76b0ac7ca63.jpg)

`(id_rec)` 이 표시되면서 가상환경이 활성화 된 것에 주목

![virtualenv2](https://user-images.githubusercontent.com/34564706/100175108-1e0c3c80-2f11-11eb-9391-394d2fb82423.jpg)

어떤 명령어를 치든 `(가상환경이름)` 이 같이 나오면서 가상환경이 활성화 된 것이 나타나야 됨.