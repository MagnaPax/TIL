## SELF JOIN
- 하나의 테이블에 있는 칼럼끼리 연결해야 하는 조인이 필요한 경우

```sh
select e.ename||'의 직속 상관은'||m.ename from employee e join employee m on e.manager=m.eno;
```

```sh
E.ENAME||'의직속상관은'||M.ENAME
----------------------------------
FORD의 직속 상관은JONES
SCOTT의 직속 상관은JONES
TURNER의 직속 상관은BLAKE
ALLEN의 직속 상관은BLAKE
WARD의 직속 상관은BLAKE
JAMES의 직속 상관은BLAKE
MARTIN의 직속 상관은BLAKE
MILLER의 직속 상관은CLARK
ADAMS의 직속 상관은SCOTT
BLAKE의 직속 상관은KING
JONES의 직속 상관은KING
CLARK의 직속 상관은KING
SMITH의 직속 상관은FORD

13 개의 행이 선택되었습니다.
```

## OUTER JOIN
- 양측 칼럼 값 중의 하나가 null이지만 조인 결과로 출력할 필요가 있는 경우 사용
- 맨 마지막에 (+)를 붙여서 아래 결과 중 ```KING의 직속 상관은``` 이 나왔다. 위에서는 안 나온 것에 주목.

```sh
select e.ename||'의 직속 상관은'||m.ename from employee e join employee m on e.manager=m.eno(+);
```

```sh
E.ENAME||'의직속상관은'||M.ENAME
----------------------------------
FORD의 직속 상관은JONES
SCOTT의 직속 상관은JONES
JAMES의 직속 상관은BLAKE
TURNER의 직속 상관은BLAKE
MARTIN의 직속 상관은BLAKE
WARD의 직속 상관은BLAKE
ALLEN의 직속 상관은BLAKE
MILLER의 직속 상관은CLARK
ADAMS의 직속 상관은SCOTT
CLARK의 직속 상관은KING
BLAKE의 직속 상관은KING
JONES의 직속 상관은KING
SMITH의 직속 상관은FORD
KING의 직속 상관은

14 개의 행이 선택되었습니다.
```
```sh
$ select e.ename||'의 직속 상관은'||m.ename
  2  from employee e left outer join employee m
  3  on e.manager = m.eno;
```