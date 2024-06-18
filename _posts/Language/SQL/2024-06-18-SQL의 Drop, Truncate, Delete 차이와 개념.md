---
title: SQL의 Drop, Truncate, Delete 차이와 개념
date: 2024-06-18 21:10:00 +/-0000
categories: [Language, SQL]
tags: [sql]
toc: true
pin: true
---

오늘은 SQL에서 자주 사용하는 명령어인 DROP, TRUNCATE, DELETE에 대해 알아보려고 하는데 해당 명령어들은 모두 데이터를 삭제하는데 사용되지만 각각의 기능과 사용 목적이 조금씩 달라 헷갈리는 점이 많다 각각에 대해 예제와 함께 간단히 알아보자

# 1. DROP

DROP 명령어는 데이터베이스 객체(테이블, 데이터베이스 등)를 완전히 삭제할 때 사용되는 명령어로 한번 실행하면 해당 객체는 영구적으로 사라지며 복구할 수 없다는 특징을 가졌다

~~~sql
DROP TABLE 테이블명;
~~~

## 예시

~~~sql
DROP TABLE Customers;
~~~

위 명령어는 Customers 테이블을 데이터베이스에서 완전히 삭제하는 코드로 테이블 구조와 모든 데이터가 삭제되며, 복구할 수 없다

# 2. TRUNCATE

TRUNCATE 명령어는 테이블의 모든 데이터를 빠르게 삭제할 때 사용되는 명령어로 DROP과 차이점으로는 테이블 구조는 유지된다 또한 TRUNCATE는 내부적으로 테이블을 재설정하는 방식으로 작동하기 때문에 밑에서 설명할 DELETE보다 빠르다

~~~sql
TRUNCATE TABLE 테이블명;
~~~

## 예시

~~~sql
TRUNCATE TABLE Orders;
~~~

위 명령어는 Orders 테이블의 모든 데이터를 삭제하지만 테이블 자체는 남아 있게 되는 코드로 테이블을 다시 사용할 수 있으며 기존 테이블 구조는 그대로 유지된다

# 3. DELETE

DELETE 명령어는 테이블에서 특정 조건에 맞는 데이터를 삭제할 때 사용되는 명어로 조건을 지정하지 않으면 테이블의 모든 데이터가 삭제됩니다. DELETE는 트랜잭션을 지원하며 롤백이 가능하다는 특징이 있다

~~~sql
DELETE FROM 테이블명 WHERE 조건;
~~~

## 예시

~~~sql
DELETE FROM Employees WHERE Age > 60;
~~~

위 명령어는 Employees 테이블에서 Age가 60보다 큰 모든 데이터를 삭제하는 코드로 여기서 조건을 지정하지 않으면 전체 데이터가 삭제된다

~~~sql
DELETE FROM Employees;
~~~

위 명령어는 Employees 테이블의 모든 데이터를 삭제하지만 테이블 구조는 유지된다

# 요약

* DROP: 테이블(혹은 데이터베이스)을 완전히 삭제, 구조와 데이터 모두 사라짐
* TRUNCATE: 테이블의 모든 데이터를 빠르게 삭제, 테이블 구조는 유지됨
* DELETE: 특정 조건에 맞는 데이터를 삭제, 조건이 없으면 모든 데이터 삭제. 테이블 구조는 유지됨

이렇게 각 명령어는 사용 목적에 따라 선택하여 사용해야 하는데 예를 들자면 테이블 자체를 삭제해야 한다면 DROP, 모든 데이터를 빠르게 삭제하고 싶다면 TRUNCATE, 특정 데이터를 삭제하고 싶다면 DELETE를 사용하면 된다

