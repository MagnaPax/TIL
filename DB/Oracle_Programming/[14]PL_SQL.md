## 2 변수선언


```
SQL> set serveroutput  on
SQL> declare
  2  v_eno employee.eno%type;
  3  v_ename employee.ename%type;
  4  begin
  5  dbms_output.put_line('사원번호   사원이름');
  6  dbms_output.put_line('---------------');
  7  select eno, ename into  v_eno, v_ename from employee where ename='SCOTT';
  8  dbms_output.put_line(v_eno||'        '||v_ename);
  9  end;
 10  /
사원번호   사원이름
---------------
7788        SCOTT

PL/SQL 처리가 정상적으로 완료되었습니다.
```

변수선언
```
SQL> declare
  2  v_employee employee%rowtype;
  3  temp number(4) := 1;
  4  annsal number(7, 2);
  5  begin
  6  select * into v_employee from employee where ename='SCOTT';
  7  if(v_employee.commission is null) then v_employee.commission := 0;
  8  end if;
  9
 10  annsal := v_employee.salary*12 + v_employee.commission;
 11  dbms_output.put_line('사원번호   사원이름');
 12  dbms_output.put_line('---------------');
 13  dbms_output.put_line('---------------');
 14  dbms_output.put_line(v_employee.eno||'  '||v_employee.ename||'  '||annsal);
 15  end;
 16  /
사원번호   사원이름
---------------
---------------
7788  SCOTT  36000

PL/SQL 처리가 정상적으로 완료되었습니다.
```

- BASIC LOOP로 구구단 2단 출력하기
```
SQL> declare
  2  dan number := 2;
  3  i number := 1;
  4  begin
  5  loop
  6  dbms_output.put_line(dan||' X '||i||' = '||(dan*i));
  7  i := i+1;
  8  if i>9 then exit;
  9  end if;
 10  end loop;
 11  end;
 12  /
2 X 1 = 2
2 X 2 = 4
2 X 3 = 6
2 X 4 = 8
2 X 5 = 10
2 X 6 = 12
2 X 7 = 14
2 X 8 = 16
2 X 9 = 18

PL/SQL 처리가 정상적으로 완료되었습니다.
```

- FOR LOOP 로 구구단 2단 출력
```
SQL> declare
  2  dan number := 2;
  3  i number := 1;
  4  begin
  5  for i in 1..9 loop
  6  dbms_output.put_line(dan||' X '||i||' = '||(dan*i));
  7  end loop;
  8  end;
  9  /
2 X 1 = 2
2 X 2 = 4
2 X 3 = 6
2 X 4 = 8
2 X 5 = 10
2 X 6 = 12
2 X 7 = 14
2 X 8 = 16
2 X 9 = 18

PL/SQL 처리가 정상적으로 완료되었습니다.
```

- WHILE LOOP 로 구구단 2단 출력
```
```

## 4 커서
> SELECT 문의 수행 결과가 여러 개의 행(ROW)으로 구해지는 경우에 모든 행에 대해 처리 하기 위해
```
SQL> set serveroutput on
SQL> declare
  2  v_dept department%rowtype;
  3  cursor c1
  4  is
  5  select * from department;
  6  begin
  7  dbms_output.put_line('부서번호  부서명  지역명');
  8  dbms_output.put_line('-------------------');
  9  open c1;
 10  loop
 11  fetch c1 into v_dept.dno, v_dept.dname, v_dept.loc;
 12  exit when c1%notfound;
 13  dbms_output.put_line(v_dept.dno || '  '  || v_dept.dname || '  ' || v_dept.loc);
 14  end loop;
 15  close c1;
 16  end;
 17  /
부서번호  부서명  지역명
-------------------
10  ACCOUNTING  NEW YORK
20  RESEARCH  DALLAS
30  SALES  CHICAGO
40  OPERATIONS  BOSTON

PL/SQL 처리가 정상적으로 완료되었습니다.
```

- CURSOR FOR LOOP 사용
- CURSOR가 내부적으로 OPEN되고, FETCH되고 나서 CLOSE 되기 때문에 OPEN ~ FETCH ~ CLOSE 과정 없이 DECLARE 절에서 선언만 하고 바로 사용할 수 있어 간편함
```
SQL> set serveroutput on
SQL> declare
  2  v_dept department%rowtype;
  3  cursor c1
  4  is
  5  select * from department;
  6  begin
  7  dbms_output.put_line('부서번호  부서명  지역명');
  8  dbms_output.put_line('-------------------');
  9
 10  for v_dept in c1 loop
 11  exit when c1%notfound;
 12  dbms_output.put_line(v_dept.dno || '  '  || v_dept.dname || '  ' || v_dept.loc);
 13  end loop;
 14  end;
 15  /
부서번호  부서명  지역명
-------------------
10  ACCOUNTING  NEW YORK
20  RESEARCH  DALLAS
30  SALES  CHICAGO
40  OPERATIONS  BOSTON

PL/SQL 처리가 정상적으로 완료되었습니다.
```