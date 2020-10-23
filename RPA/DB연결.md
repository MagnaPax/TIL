# csv 파일 읽어서 Oracle DB 에 저장하기

## db 설치
   https://www.oracle.com/database/technologies/112010-win32soft.html
   win32_11gR2_client.zip 다운 받은 후 설치


<br>
<br>

## 실습에 필요한 UiPath 파일 위치

https://github.com/MagnaPax/RPA_Practice/tree/master/DB_Connection


<br>
<br>

## Windows 설정

윈도우즈 ODBC 데이터 원본 관리자(32비트) 셋팅

  1) "C:\Windows\SysWOW64 폴더에 odbcad32.exe 실행"

      또는 

      윈도우 - 검색 - "ODBC 데이터 원본 관리자(32비트) : Uipath는 ODBC를 32비트만 지원함

      - 사용자 DSN - 추가 - Oracle in OraClient11g_home1 - 마침

  2) Data Source Name : RPA_ORACLE, TNS Service Name : ORCL, UserID : SYSTEM(Test Connection할때 입력), RPA(RPA 계정 생성 및 권한 부여 후 입력)

  3) Test Connection 클릭 - Service Name : ORCL, User Name : SYSTEM(Test Connection할때 입력), RPA(RPA 계정 생성 및 권한 부여 후 입력), Password(계정별 패스워드 입력) - OK


[참고사항 : C:\app\Kosmo_03\product\11.2.0\dbhome_1\NETWORK\ADMIN 폴더 tnsnames.ora 파일 못 찾아서 에러날 경우]

C:\app\Kosmo_03\product\11.2.0\dbhome_1 폴더에 있는 NETWORK 폴더를 복사해서 C:\app\Kosmo_03\product\11.2.0\client_3 폴더에 붙여넣기해 줍니다.

sqlplus 실행이 잘못될 경우,  윈도우즈키+R키 - sysdm.cpl - 고급 환경 변수의 내용을 수정해 줍니다. (뭘 삭제. 뭘 삭제하는지 까먹음 11g 였던 것 같음)

![image](https://user-images.githubusercontent.com/34564706/96947190-7f5d7c00-151d-11eb-87b5-c46aae0ac38f.png)

![image](https://user-images.githubusercontent.com/34564706/96947214-90a68880-151d-11eb-9812-945b19085b7b.png)

![image](https://user-images.githubusercontent.com/34564706/96949648-55a75380-1523-11eb-81da-ef4a7b673554.png)

![image](https://user-images.githubusercontent.com/34564706/96949680-6c4daa80-1523-11eb-8ce0-39cc12962dee.png)

![image](https://user-images.githubusercontent.com/34564706/96949709-85565b80-1523-11eb-930d-ebe1a571a2e2.png)


이렇게 에러 발생함. oracle 에서 설정 해줘야 됨


<br>
<br>

## Oracle 설정
- 계정 및 권한 생성, 테이블을 생성

```
SQLPLUS SYSTEM/System1234

show user

CREATE USER 원하는유저이름 IDENTIFIED BY 비밀번호;
GRANT CONNECT, RESOURCE, DBA TO RPA;
GRANT ALTER SESSION TO RPA;

CONN 원하는유저이름/비밀번호

show user

CREATE TABLE 원하는테이블이름(
 VENDOR VARCHAR2(8),
 MONTH NUMBER(2),
 AMOUNT NUMBER(6),
 TAX NUMBER(7,1),
 TOTAL NUMBER(7,1),
 CURRENCY VARCHAR2(3)
);

commit;

desc 원하는테이블이름

select * from tab;

select count(*) from 원하는테이블이름;
```

## Windows 설정
- oracle 에서 유저와 테이블을 만들었기 때문에 이렇게 접속 성공하게 됨

![image](https://user-images.githubusercontent.com/34564706/96950347-06622280-1525-11eb-8933-940e82faf069.png)

![image](https://user-images.githubusercontent.com/34564706/96950379-1a0d8900-1525-11eb-8f62-0ba2004798c5.png)



<br>
<br>

## UiPath

### UiPath Studio Database 의존성 추가

  1) 패키지관리 - 공식 - 검색 "database" - UiPath.Database.Activities - 설치 - 저장

  2) 액티비티 - 검색 "database" - Connect, Disconnect, Execute Non Query, Execute Query, Insert, Start Transaction


아래 파일을 이용

중요_배포용) RPA_OracleDB저장_Main 파일 소스_ACME이메일아이디_수정필요\RPA_Session5\csvToOracleDB\ConnectDataBase.xaml


### Connect 액티비티 설정

Database - Connect 액티비티 - Configure Connection - Connection Wizard → Microsoft ODBC Data Source 선택 → Use user or system data source name - 윈도우즈 ODBC 데이터 원본 관리자(32비트) 에서 만든것 선택 → User name 과 Password 입력


![image](https://user-images.githubusercontent.com/34564706/96948613-0c560480-1521-11eb-82d6-d36a3a36365c.png)


![image](https://user-images.githubusercontent.com/34564706/96948643-1d067a80-1521-11eb-90ac-dd49ce1a08d7.png)


![image](https://user-images.githubusercontent.com/34564706/96948951-c483ad00-1521-11eb-9c99-088b56beca7c.png)


![image](https://user-images.githubusercontent.com/34564706/96948991-debd8b00-1521-11eb-9202-e9ed211d5806.png)

![image](https://user-images.githubusercontent.com/34564706/96949034-f268f180-1521-11eb-94b7-549662bf3e0f.png)


### Execute Non Query 액티비티 설정

![image](https://user-images.githubusercontent.com/34564706/96949168-3825ba00-1522-11eb-9cfc-c9c777a3f2a6.png)

```
"INSERT INTO rpa_mission (VENDOR, MONTH, AMOUNT, TAX, TOTAL, CURRENCY) VALUES ('"+in_Str_Vendor+"', '"+in_Str_Month+"', '"+in_Str_Amount+"', '"+in_Str_Tax+"', '"+in_Str_Total+"', '"+in_Str_Currency+"')"
```

### 실행

- DB_Connection 폴더에 있는 Main.xaml 파일을 실행시키시기 바랍니다. 그리고, Flowchart에 있는 "Session4_1_엑셀다운로드"와 "Session4_2_CSV다운로드"의 이메일과 암호 입력 정보를 수정하시기 바랍니다.

- "Session4_3_OracleDB 저장"을 실행(Ctrl+F5) 시킵니다.

- OracleDB에 제대로 Insert 저장 되었는지 확인하시기 바랍니다.


<br>
<br>

[참고사항 : RPA 기술 공유 카페]
https://cafe.naver.com/rpakoreascoring
