## 1 서브쿼리의 기본 개념

```sh
select ename, dno from employee 
where dno=(select dno from employee where ename='SCOTT');
```
- ```where dno=``` 다음에 만약에 10이 들어갔다면 dno가 10인 것 출력. 
- 위의 경우는 'ename이 SCOTT인 dno칼럼' 이라는 조건. 
- 이렇듯 조건에 해당하는 것을 ()을 이용해서 서브쿼리로 한 문장에 넣어주는 것.
- 최종적으로 SCOTT과 동일한 부서에서 근무하는 사원 출력됨

<br>

최소 급여를 받는 사원의 이름, 담당업무, 급여출력하기
```sh
select ename, job, salary from employee
where salary=(select min(salary) from employee);
```
- 서브쿼리 안의 조건은 employee테이블에서 salary가 가장 작은


## 2 다중 행 서브 쿼리
- 서브 쿼리에서 반환되는 결과가 '하나 이상'의 행일 때 

### 2.2 ANY 연산자
- 서브쿼리가 반환하는 각각의 값과 비교
- ' < any' 는 최대값보다 작음
- ' > any' 는 최소값보다 큼
- ' = any' 는 'in' 과 동일

```sh
select eno, ename, job, salary from employee
where salary < any ( select salary from employee where job='SALESMAN')
and job <> 'SALESMAN';
```
- 서브쿼리는 직급이 SALESMAN 인 사원의 급여
- ' < any' 는 최대값보다 작음. 즉 직급이 SALESMAN 인 사원의 최대 급여 보다 적은 사원들만 출력

### 2.3 ALL 연산자
- ANY연산자와는 달리
- ' < all' 는 최소값보다 작음
- ' > all' 는 최대값보다 큼