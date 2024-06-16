---
title: SQL의 내부 조인(INNER JOIN)과 외부 조인(OUT JOIN) 개념과 차이점
date: 2024-06-17 01:30:00 +/-0000
categories: [Language, SQL]
tags: [sql]
toc: true
pin: true
---

데이터베이스 관리 시스템(DBMS)를 공부하다보면 맞닥뜨리게 되는 조인(join)은 여러 테이블에 걸친 데이터를 결합하여 하나의 결과 집합으로 만드는 중요한 작업으로 꼭 알아야 되는 개념이다

이러한 조인에는 여러 종류가 있지만 그 중에서도 가장 많이 사용되는 것은 INNER JOIN과 OUTER JOIN이다 이번 글에서는 이러한 INNER JOIN과 OUTER JOIN의 개념과 사용법 그리고 차이점에 대해 설명하겠다

# INNER JOIN
INNER JOIN은 두 테이블에서 매칭되는 행만 반환한다 즉 조인 조건에 만족하는 데이터만 결과 집합에 포함되는데 이때 조인 조건은 일반적으로 테이블 간의 공통 열(키)을 기준으로 한다

## 예제
아래 예제는 employees 테이블과 departments 테이블이 있다고 가정한 예제이다

**employees 테이블:**

|employee_id|name|department_id|
|------|---|---|
|1|Alice|1|
|2|Bob|2|
|3|Charlie|3|

**departments 테이블:**

|department_id|department_name|
|------|---|
|1|HR|
|2|Engineering|
|4|Sales|
	
해당 테이블에서 INNER JOIN을 사용하여 각 직원의 부서명을 포함하는 결과를 얻고자 할 때의 SQL 쿼리는 다음과 같다

~~~sql
SELECT employees.name, departments.department_name
FROM employees
INNER JOIN departments ON employees.department_id = departments.department_id;
~~~
**결과**
|name|department_name|
|------|---|
|Alice|HR|
|Bob|Engineering|

위 결과에서 볼 수 있듯이 Charlie는 departments 테이블에 해당하는 부서가 없기 때문에 결과에 포함되지 않는다

# OUTER JOIN

OUTER JOIN은 두 테이블 간의 모든 행을 반환하며 조인 조건에 맞지 않는 경우에도 데이터를 반환한다 여기서 또 OUTER JOIN은 다시 LEFT JOIN, RIGHT JOIN, FULL JOIN으로 나뉜다

## LEFT JOIN

LEFT JOIN은 왼쪽 테이블의 모든 행을 반환하고 오른쪽 테이블과 조인 조건에 맞지 않는 경우에는 NULL 값을 반환한다

~~~sql
SELECT employees.name, departments.department_name
FROM employees
LEFT JOIN departments ON employees.department_id = departments.department_id;
~~~

**결과**
|name|department_name|
|------|---|
|Alice|HR|
|Bob|Engineering|
|Charlie|NULL|
	
## RIGHT JOIN

RIGHT JOIN은 오른쪽 테이블의 모든 행을 반환하고 왼쪽 테이블과 조인 조건에 맞지 않는 경우에는 NULL 값을 반환한다

~~~sql
SELECT employees.name, departments.department_name
FROM employees
RIGHT JOIN departments ON employees.department_id = departments.department_id;
~~~

**결과**

|name|department_name|
|------|---|
|Alice|HR|
|Bob|Engineering|
|NULL|Sales|

## FULL JOIN

FULL JOIN은 두 테이블의 모든 행을 반환하며 조인 조건에 맞지 않는 경우에는 NULL 값을 반환한다 왼쪽 또는 오른쪽 어느 한쪽 테이블에만 있는 데이터도 결과에 포함된다

~~~sql
SELECT employees.name, departments.department_name
FROM employees
FULL JOIN departments ON employees.department_id = departments.department_id;
~~~

**결과**

|name|department_name|
|------|---|
|Alice|HR|
|Bob|Engineering|
|NULL|Sales|

# INNER JOIN과 OUTER JOIN의 차이점

## 1. 데이터 반환 방식

* INNER JOIN은 조인 조건에 맞는 행만 반환하지만
* OUTER JOIN은 조인 조건에 맞지 않는 행도 포함하여 반환한다

## 2. NULL 처리

* INNER JOIN에서는 조인 조건에 맞지 않는 행이 결과에 포함되지 않는다

* OUTER JOIN에서는 조인 조건에 맞지 않는 행이 NULL 값으로 결과에 포함된다

## 사용 사례

* INNER JOIN은 주로 두 테이블 간에 매칭되는 데이터만 필요할 때 사용한다

* OUTER JOIN은 한쪽 테이블의 모든 데이터를 유지하면서 다른 테이블과의 관계를 확인하고자 할 때 사용한다