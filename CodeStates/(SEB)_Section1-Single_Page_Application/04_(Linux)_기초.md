# Chap. 1. CLI 기본 명령어

## 기본적인 명령어

### rm

> rm은 단일 파일을 삭제할 수 있습니다. 만약 폴더를 삭제하려면 옵션을 이용해야 합니다.

- 옵션 r은 "recursive"를 뜻하고
- 옵션 f는 "force"를 뜻합니다.

```
rm -rf 폴더이름
```

### mv

> 폴더나 파일의 위치 옮기기 또는 폴더나 파일의 이름을 변경

- 폴더나 파일의 위치 옮기기
- rm [폴더나 파일의 이름] [도착 폴더의 이름]를 입력합니다.

```
mv bye.txt bye/
```

- 폴더나 파일의 이름을 변경할 수 있습니다.

```
mv 폴더나 파일의 이름 도착 폴더의 이름
mv bye.txt bye2.txt

```

## 관리자 권한과 경로

### 절대 경로와 상대 경로

- 점(.)은 현재 폴더
- 슬래시(/)는 폴더 내부를 나타냅니다.
- ./는 "현재 폴더 아래의"라는 뜻입니다.
- 사용자 폴더의 경로(Path)는 ~/로 표시됩니다. 물결기호(~)는 루트폴더(/)로부터 사용자 폴더(username)까지의 경로를 축약한 형태입니다.

![루트디렉토리 홈디렉토리](https://user-images.githubusercontent.com/77217300/123191316-0c593a80-d4dc-11eb-899f-d473ff0039ec.jpg)

### 관리자 권한

> 절대 경로의 기준점인 루트폴더 **[/]** 는 리눅스의 루트 영역이다
> 일반 사용자에게 루트 권한을 완전하게 넘기지 않음

- sudo
  - 관리자 권한을 획득하는 명령어

# Chap. 2. 패키지와 패키지 매니저

## 리눅스의 패키지

> 여러 파일을 모아 하나의 파일로 저장하고 있는 압축파일

- 패키지 기본 구성
  - 프로그램 파일
  - 프로그램 설치 파일
  - 프로그램 설치 설명서
  - 프로그램에 대한 정보를 담은 파일

## 리눅스의 패키지 매니저

> 패키지의 설치, 변경, 삭제 등 관리를 편리하게 해주는 도구. 스마트폰의 앱스토어 역할과 비슷

앱 스토어를 이용해 필요한 앱을 설치하는 것처럼 리눅스 사용자도 패키지 매니저를 이용해 필요한 패키지를 설치

- Ubuntu 패키지 매니저: apt
- macOS 패키지 매니저: brew

# Chap. 3. Node.js

## 런타임

> 프로그래밍 언어가 구동되는 환경

- JavaScript 의 런타임
  - 웹 브라우저
  - node.js

## nvm & node.js

> node.js의 다양한 버전을 관리하는 프로그램

- nvm (Node <span style="color:red">Version</span> Manager) 리눅스 패키지 매니저처럼 node.js 버전을 관리
- nvm을 사용하여 node.js 의 다양한 버전을 쉽게 설치, 사용 가능

[nvm 공식문서](https://github.com/nvm-sh/nvm#install--update-script)

- node.js 설치

```js
nvm install --lts
```

## nvm 간단 사용법

nvm 을 사용하여 이미 설치된 버전을 삭제하지 않고, 우리가 원하는 node version을 설치할 수 있다. 사용중인 node version을 다른 버전으로 변경하고 싶을 때에는 아래의 명령어만 입력하면 됩니다.

```
nvm use 버전넘버  # 예를 들어, nvm use 12.18.3,  nvm use 14.15.5
```

nvm으로 node의 버전을 관리하면, node를 설치하고 version을 바꾸는 일이 편리합니다.

정리하면 nvm은 다양한 node version를 설치하고 관리할 수 있는 프로그램 입니다.

## npm 과 package.json

| 용어         | 의미                                  |
| ------------ | ------------------------------------- |
| 모듈         | 다른 사람들이 만들어 놓은 검증된 코드 |
| npm          | node.js 의 모듈                       |
| package.json | npm 모듈의 정보를 담아둔 곳           |

<br>
### npm

> npm (Node <span style="color:red">Package</span> Manager)
>
> > 라이브러리 ≒ 일종의 앱스토어.

> npm 패키지, npm 모듈, npm dependency 는 전부 동일한 대상을 가리킵니다. 관점에 따라 다른 용어를 쓸 뿐입니다.

> "독립적인 하나의 완성된 조각"이라는 의미로 <span style="color:red">패키지</span> 라는 용어를 사용하며, 다른 프로그램에서 패키지를 가져다 쓰면 <span style="color:red">모듈</span> 이라고 부릅니다. 다른 프로그램에서 이 패키지를 모듈로 사용하면, 프로그램을 실행할 때 이 모듈에 의존할 수밖에 없습니다. 이때는 <span style="color:red">dependency(의존성)</span>라고 부릅니다. 용어는 조금 다르지만, 동일한 대상을 가리킵니다.

필요한 모듈을 다운로드할 수 있는, 모듈들이 모여있는 모듈 스토어입니다.

|         | 패키지 매니저 |
| ------- | :-----------: |
| 리눅스  |      apt      |
| 맥OS    |     brew      |
| node.js |      npm      |

<br>
### package.json

> 전자제품의 카달로그처럼 어떤 모듈인지 파악할 수 있는 파일

![package json](https://user-images.githubusercontent.com/77217300/123183735-22133380-d4cd-11eb-8037-65bcbda6f8f5.jpg)

- 이 프로그램을 실행시키기 위해 필요한 모듈들은 무엇인지
- 프로그램을 실행시키는 방법
- 프로그램을 테스트하는 방법

하지만 프로그램을 실행시키기 위해 필요한 실제 모듈은 **node_modules** 라는 폴더에 따로 저장

따라서 남들한테 프로젝트 코드를 전달할 때 package.json 만 주고 알아서 다운받게 하면 됨. node_modules 전체를 줄 필요 없다

<br>
#### 1. devDependencies

![devDependencies](https://user-images.githubusercontent.com/77217300/123183821-57b81c80-d4cd-11eb-913c-44be85e68a10.jpg)

- 이 프로젝트를 개발하는 환경에서 필요한 모듈(dependency)들이 무엇인지 적혀 있다
- 실제 프로젝트 동작에 직접적으로 영향을 주지 않는 모듈들 명시
- 프로그램 실행과 상관없는 개발자들을 위한 것이다
- --save-dev 옵션과 함께 설치하면 자동으로 devDependencies에 추가됨

```
$ npm install 모듈이름 --save-dev
```

<br>
#### 2. dependencies

![dependencies](https://user-images.githubusercontent.com/77217300/123183914-88985180-d4cd-11eb-80ec-01bc428a61d5.jpg)

- 이 프로젝트가 돌아가기 위해 반드시 필요한 모듈이 무엇인지 적혀있음
- --save 옵션과 함께 설치하면, 자동으로 dependencies에 추가(생략가능)

```
$ $ npm install --save 모듈이름
```

<br>
#### 3. script

> CLI 에서 사용 가능한 명령이 기술되어 있다

![npm script](https://user-images.githubusercontent.com/77217300/123184579-f09b6780-d4ce-11eb-9a6c-43a1922479b8.jpg)

- 실행방법

```
$ npm run <스크립트 이름>
```

- script 항목 예시

```node
{
  "scripts": {
    "start": "node index.js",
    "test": "mocha test/index.test.js",
    "lint": "eslint",
    "submit": "codestates-submission"
  },
}
```

| 작업 내용                     | 실행 스크립트      |
| ----------------------------- | ------------------ |
| node.js 앱 실행               | `$ npm run start`  |
| 테스트 실행                   | `$ npm run test`   |
| 코드 검사                     | `$ npm run lint`   |
| 과제 제출 (코드스테이츠 only) | `$ npm run submit` |

<br>
#### package.json 의 존재 이유?

> 다른 사람과 함께 개발하기 위해서

다른 사람에게 어떻게 해야 프로그램을 실행시킬 수 있는지, 이걸 실행시키려면 어떤 모듈이 있는지 알려 주기 위해

우리가 흔히 하는 npm install은 package.json에 있는 dependency (의존성 모듈)를 바탕으로 설치한다, 즉 남들도 package.json 만 있으면 같은 모듈을 설치 할 수 있다는 뜻

<br>
## script / dependencies / devDependencies 간단 정의

![script   dependency   devDependency](https://user-images.githubusercontent.com/77217300/123193842-69ef8600-d4e0-11eb-8557-5a8b13cc497b.jpg)
