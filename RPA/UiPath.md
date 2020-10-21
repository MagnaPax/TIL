### 실습파일 위치
https://github.com/MagnaPax/RPA_Practice


### 변수 쓰는 규칙
RPA 개발 시 알아야 할 것
1. RPA 언어는 vb.net 언어를 사용한다(Microsoft Doc 참고)
-> 문법 검색 시 뒤에 in vb.net 을 친다
2. 따라서 vb.net, C# 문법을 준수한다.
3. vb.net 언어의 규칙은 다음과 같다
 1) 변수 앞글자는 항상 대문자로 시작한다.
 2) 사용 시 타입명+이름으로 쓴다(e.g. StrName)
 3) 변수 타입명은 다음과 같이 정의한다.
String = Str
Int32 = Int
Boolean = Bln
Array = Ary or Arr
Datatable = DT
Double = Dbl
List = List
Dictionary = Dic

예) StrName 혹은 Str_Name

Int32(범위): 정수(-21억 ~ 21억)
Double(범위): 실수(거의 대부분)

For 문 : For each(배열), For each row(데이터 테이블)

- 배열의 초기화 : {}
- 배열의 크기 선언 : new String(100){}


### RPA 개발순서
1. Attach Window 또는 Attach Browser 로 해당 창을 클릭한다.
2. Attach Window 또는 Attach Browser 안에 만들고자 하는 액티비티를 넣는다 예) Click


### 사무자동화 프로세스 : 마우스, 키보드 액티비티
  - Click: 마우스
  - Type Into: 키보드(타이핑 가능)
  - Send HotKey: 키보드(타이핑 불가능, 다만 3개의 키조합 가능)


### RPA 에서 영향을 많이 받는 것
1. 해상도(1920*1080 디스플레이 해상도)
2. 창 크기(항상 최대화)
--> 대부분 코드 기반으로 움직인다. 하지만 안 될 경우에는 이미지 또는 좌표로 작업한다.(예외케이스)



### RPA 개발시 tip
1. Get 으로 시작하는 액티비티는 데이터를  가져오는 액티비티
-- Get 액티비티를 쓰면 항상 속성 -> 출력 부분(변수 들어갈 자리)을 확인한다
2. Set 으로 시작하는 액티비티는 데이터를 설정하는 액티비티


### Excel 데이터 다루기
- 엑셀 데이터를 읽을 때: Read Range
- 엑셀 데이터를 쓸 때: Write Range
- 엑셀에 데이터를 읽거나 쓸 때는 반드시 Excel Application Scope 사용
- Filter Data Table 액티비티 : 조건문 or 칼럼 재배치할 때 사용
  - 출력 열(Output Columns) 에서 데이터테이블이름.Colums(인덱스번호).ColumnName
- 


### 브라우저 액티비티
- Close Tab: 브라우저 닫기 액티비티
- Navigate To: 사이트 이동 액티비티


### Type Into 사용 시 주의할 점
- Special Key 를 사용할 때는 SimulateType(백그라운드 입력) 을 사용할 수 없다. 
- SimulateType 를 사용하게 되면 Special Key 도 문자로 입력된다


### RPA 가 다음 동작까지 기다리는 시간: 30초(Default)
- 줄이는 방법 속성 -> Timeout 에 값을 넣으면 된다.
- 1000 = 1초(millisecond)


### GenericValue -> Generic(일반적인, 전체적인): 모든 타입을 수용한다.
- ToString 사용하여 가공 혹은 Cdbl로 형변환하여 사용


### RPA 작업방식
- UI를 Target 해서 처리하는 방식
- 시스템을 변경하거나 수정할 수 없다. 다른 담당자가 시스템을 변경하면 RPA도 똑같이 변경해줘야 한다.
  - 사이트의 변경이 일어나면 RPA는 에러가 난다(UiElement를 찾을 수 없습니다 에러발생)


### 와일드카드 = *
- 사용하는 이유
1. Attach Browser 또는 Attach Window로 잡은 페이지들을 하나로 통일하고 싶을 때
2. 공통 모듈 만들기 위해서(라이브러리)


### 문자열
#### Substring(글자수를 세서 출력하는 문법)
사람: 1234
컴퓨터: 01234

#### Trim: 데이터의 정합성(데이터를 정확하게 일치)을 보장. 양쪽 공백을 제거

#### Split: 특정 문자를 기준으로 분할하는 문법
- Split => String[] 배열에 저장이 된다.


### Method -> 가공하는 순서


### 시간표현
C# -> Datetime.Now


### 기업 프로젝트: 시간표현(현재시간에 대한 컨트롤 < 과거시간 컨트롤)


### 변수 초기화 정리
String = ""
Int32 = 0
Double = 0
Array = {}
Datatable = new Datatable()
List = new List(of [T])
Dictionary = new Dictionary(of [T], [T])


### 배열, 리스트, 딕셔너리
배열: 크기가 지정되어야 한다. 예) new String(100){}
리스트: 알아서 크기 조정이 된다.

배열 ≠ 리스트, 딕셔너리(System.Collections(컬랙션))


### 엑셀
(엑셀)Read Range(O)
(통합문서)Read Range(X)

---------------------
(엑셀)Write Range(O)
(통합문서)Write Range(X)


### Excel Application Scope
속성
- Auto Save: 자동저장
- Create New File: 엑셀파일 없으면 만들어줌
- Visible : 엑셀작업이 화면에 보인다.

Excel -> Read -> Datatable -> Datatable 액티비티 모음을 사용한다.


### DataTable(데이터테이블) 의 Row의 갯수
> 데이터테이블이름.Rows.Count.ToString

Array(배열) 의 크기를 계산
> 배열이름.Length.ToString

### DataTable 복사
> DataTable.Copy -> 칼럼까지 그대로 복사


### 자동완성기능
1. 앞글자를 친다
2. Ctrl+Space


### Filter Data Table = 엑셀의 정렬 및 필터 기능과 동일하다
- 많은 양의 데이터를 빨리 뽑을 때 사용한다.


### 파일확장자명
Read Range 액티비티 → 엑셀파일
Read CSV → csv 파일
Read Text File → 텍스트 파일
(Package 설치 후) Read PDF → pdf 파일
Load Image → 이미지 파일
압축파일은 압축할 때만 사용. 압축풀기는 사용하지 않음
(Package 설치 후) Read Word File → 워드파일


### 데이터 스크래핑
속성 →Timeout(Default: 30초)


### RPA 현장에서 쓰는 Try Catch 문
1. Finally 부분은 사용하지 않는다.
2. Catches 는 무조건 System.Exception 에러메세지만 사용한다(90% 이상)
System.Exception : 모든 에러 처리를 받겠다. (REFramework : UiPath 에서 만든 프레임워크에서 이렇게 쓰고 있기 때문에)


### Datatable
Build Data Table -> 데이터테이블을 만들 때

(Assign) new Datatable() -> 데이터테이블 초기화 할 때

(tip) Clear Data Table -> 칼럼만 남기고 데이터를 초기화 할 때

초기화는 만들기가 아님에 주의



### ArrayRow ---> 변수를 쓴다
"" = 공백데이터
Nothing = 아무것도 넣지 않겠다.(null값 방지)



### 변수와 인수
변수
- 같은 파일 안에서 데이터 전달

인수
- 파일과 다른 파일 사이에서의 데이터 전달
- 방향: 데이터의 흐름을 표시
  - in: 데이터를 받음. 예)in_Str_Text
  - out: 데이터를 내보냄 예)out_Str_Text
  - inout: 데이터를 왔다 갔다

### 인수 만들 때 주의사항
1. 변수와 인수를 동일하게 만들면 우선순위는 ① 변수 ②인수 순으로 진행된다. 따라서 변수와 인수를 똑같은 이름으로 만들지 않는다.
2. Main은 상위 노드(계층 구조의 최상단)이므로 Main은 대부분 변수만 쓰고 나머지 파일들은 인수를 주로 쓰게 된다
3. 파일 내 파일을 불러올 때는 Invoke 에 Invoke 가 되므로 데이터가 안으로 들어갈 때는 방향을 in 으로 통일시키고 밖으로 나갈때는 out으로 통일시킨다
4. 값에는 대부분 변수가 들어간다 (3. 번은 예외)


### 파일 단위로 나눌 때
- 파일 단위로 나누면 파일 단위별로 프로세스를 점검하게 되는데 그때는 '디버그' 버튼 또는 '파일 실행' 버튼을 눌러준다('실행' 버튼 금지)



### RPA 설계 순서
0. Read Config(Config 파일: ID/PW 및 사이트 정보를 담고 있는 엑셀 파일)
  - 모든 정보는 엑셀 config 파일에서 관리
1. Kill Process : 애플리케이션을 종료하는 프로세스





## RPA 전문 개발자 과정
1. RPA 인프라 → Studio. Orchestrator, Robot
2. 프로젝트 개발 표준 방법론 → 프로젝트 개발&운영
3. 나머지 skill 등등(이메일, PDF, 이미지처리)



# Orchestrator 클라우드
https://cloud.uipath.com


### 프로세스 배포 시 주의할 점
- 반드시 C:\ProgramData\UiPath\Packages 안에 nupkg 파일이 배포되어야 한다. (임의의 사용자 지정 경로 금지)

C:\Users\Kosmo_33\AppData\Local\UiPath

Trigger 많이 쓰는 기능
Weekly
Monthly
Advanced → Cron Expression (구글에서 Cron Expression Generator 검색)



### RPA 프로젝트 정보관리(ID/PW, 사이트주소, 코드명 등)
https://blog.naver.com/gurwns6939/222117583958
엑셀: Config.xlsx
Orchestrator의 Assets ← 보안위해(Credential: Get Credential, Get Asset)

## Window Credential
패키지관리→공식→UiPath.Credentials.Activities 설치 →||→ Window 자격증명 → 일반자격증명추가 → 인터넷 또는 네트워크 주소, 사용자이름, 암호 입력 → Get Secure Credential 액티비티 → Target: 인터넷 또는 네트워크 주소, Username: 사용자 이름, Password: 암호


### 이메일
속성
Mail.Subject: 제목
.From: 받는사람
.Sender: 보내는 사람
.CC: 참조
.Bcc: 숨은참조
.Body: 본문내용
.Attachments: 첨부파일


### Text File 또는 csv 파일 읽을 때 주의사항
속성 → Encoding 을 설정한다(한글이 섞여 있는 파일을 읽을 때)
다국어의 파일 깨짐 현상 방지 위해
한글: UTF-8 / EUC-KR


### UiPath 작업
- UiElement 를 이용해서 작업(90%)
예외 케이스
1) 좌표
2) 이미지
  - Image Recording(성능이 떨어진다, 예외가 발생한다)


### 디렉토리 관련 액티비티
- Create File
- Create Folder
- Path Exists