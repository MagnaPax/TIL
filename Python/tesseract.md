# Python에서 Tesseract 사용하기 for OCR



https://shinminyong.tistory.com/5

## Tesseract 설치
- 아래 링크된 페이지를 참조하여 설치

https://junyoung-jamong.github.io/computer/vision,/ocr/2019/01/30/Python%EC%97%90%EC%84%9C-Tesseract%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%B4-OCR-%EC%88%98%ED%96%89%ED%95%98%EA%B8%B0.html

## 가상환경 설치 & 활성화 하기
- python 가상환경이 먼저 실행되고 있어야 된다. 가상환경 실행 방법은 아래 링크 참조

https://github.com/MagnaPax/TIL/blob/master/Python/virtual_env.md

## opencv 설치
```
$ pip install opencv-python
```
![image](https://user-images.githubusercontent.com/34564706/100175342-8529f100-2f11-11eb-95a3-5975a4828d09.png)

## Python Tesseract 설치
> Tesseract 를 파이썬에서 사용하기 위해 Python Tesseract 설치 해줘야 됨

```
$ pip install pytesseract
```
![pytesseract](https://user-images.githubusercontent.com/34564706/100177298-236b8600-2f15-11eb-891e-9c1e08554043.jpg)

- 네모 친 곳 처럼 가상환경이 활성화 되고 있어야 됨에 주의

## Korean Train Data 받기
> image_to_string 함수에서 `--oem 0` 으로 가장 초창기 엔진을 쓰고 싶을 때 다운 받아야 됨
> 
> Tesseract 가 설치된 곳 예를 들어 `C:\Program Files\Tesseract-OCR\tessdata` 에 집어넣어 줘야 됨

- 가로 글자

https://github.com/tesseract-ocr/tessdata/blob/master/kor.traineddata

- 세로 글자

https://github.com/tesseract-ocr/tessdata/blob/master/kor_vert.traineddata

## OCR 인식률을 높이기 위한 jTessBoxEditor 사용

https://youtu.be/dhgL_cLnVBo

아래 구글 드라이브에 완성시켜서 올려놨음.

https://drive.google.com/file/d/1bAOxz46R0zyoZi6FQ0PrxLRGnhfgN6Y0/view?usp=sharing