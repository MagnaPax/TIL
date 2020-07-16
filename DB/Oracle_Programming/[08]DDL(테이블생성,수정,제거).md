## 1 테이블 구조를 만드는 CREATE TABLE
- ```CREATE TABLE``` 문을 사용하여 테이블 생성
```sh
create table dept(
    dno number(2),
    dname varchar2(14),
    loc varchar2(13));
```

```
 이름              널?      유형
 ----------------- -------- ------------
 DNO               NOT NULL NUMBER(2)
 DNAME                      VARCHAR2(14)
 LOC                        VARCHAR2(13)
```


## 2 테이블 구조를 변경하는 ALTER TABLE 문

### 2.1 칼럼 추가
- birth 칼럼 추가
```
alter table dept20 add(birth date);
```


## 3 테이블 명을 변경하는 RENAME
- dept20 테이블을 emp20 로 바꿨음.
```
rename dept20 to emp20;
```

## 4 테이블 구조를 제거하는 DROP TABLE
```
drop table emp20;

테이블이 삭제되었습니다.
```


## 5 테이블의 모든 데이터를 제거하는 TRUNCATE TABLE
```
select * from dept_second;

       DNO DNAME          LOC
---------- -------------- -------------
        10 ACCOUNTING     NEW YORK
        20 RESEARCH       DALLAS
        30 SALES          CHICAGO
        40 OPERATIONS     BOSTON
```

```
desc dept_second;
 이름              널?      유형
 ----------------- -------- ------------
 DNO                        NUMBER(2)
 DNAME                      VARCHAR2(14)
 LOC                        VARCHAR2(13)
```
```
 truncate table dept_second;

테이블이 잘렸습니다.
```
- truncate 명령어로 테이블의 모든 데이터를 제거해서 다음 명령어를 실행해도 데이터가 안 보여짐
```
select * from dept_second;

선택된 레코드가 없습니다.
```

## 6 데이터 사전
접두어|의미
:---:|:---:
`USER_` | 자신의 계정이 소유한 객체 등에 관한 정보 조회
`ALL_` | 자신 계정 소유 또는 권한을 부여 받은 객체 등에 관한 정보 조회
`DBA_` | 데이터베이스 관리자만 접근 가능한 객체 등의 정보 조회