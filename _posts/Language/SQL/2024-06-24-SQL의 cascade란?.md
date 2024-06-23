---
title: SQL의 CASCADE란?
date: 2024-06-24 08:10:00 +/-0000
categories: [Language, SQL]
tags: [sql]
toc: true
pin: true
---

정보처리기능사 실기 기출을 풀다보면 CASCADE라는 명령어를 자주 마주치게 될 것이다 본인 또한 정보처리기능사를 공부할 때는 시간이 얼마 없어 그냥 종속된 테이블에서 무엇을 하면 CASCADE라고 외웠는데 그렇기에 이번 글에서는 이러한 SQL에서 자주 사용되는 CASCADE 명령어에 대해 알아보겠다

# CASCADE란?

CASCADE는 주로 외래 키 제약조건(Foreign Key Constraints)과 관련된 작업에서 사용되며 참조 무결성을 보장하기 위해 사용된다

여기서 참조 무결성은 한 테이블의 외래 키가 다른 테이블의 기본 키를 참조할 때 데이터의 일관성을 유지하는 것을 의미하는데 본론으로 다시 돌아가보면 CASCADE는 주로 다음 두 가지 작업에서 사용된다

* ON DELETE CASCADE: 부모 테이블의 행이 삭제될 때 이를 참조하는 자식 테이블의 행도 함께 삭제한다
* ON UPDATE CASCADE: 부모 테이블의 기본 키가 수정될 때 이를 참조하는 자식 테이블의 외래 키도 함께 수정한다

위 작업들과 앞에서 한 설명들을 보면 알겠지만 CASCADE는 부모 테이블과 자식테이블을 함께 조작하게 한다고 생각하면 이해하기 편할 거 같다

## ON DELETE CASCADE 예제

다음은 ON DELETE CASCADE를 사용하는 예제 코드로 departments와 employees 두 개의 테이블이 있으며 employees 테이블은 departments 테이블을 참조하고 있다고 가정하겠다

~~~sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL
);

CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(100) NOT NULL,
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES departments(department_id)
    ON DELETE CASCADE
);
~~~

~~~sql
-- 부서 삭제
DELETE FROM departments WHERE department_id = 1;
-- department_id가 1인 부서를 참조하는 모든 직원 정보도 삭제됨
~~~

위 예제에서는 departments 테이블의 행이 삭제될 때 해당 부서를 참조하는 모든 employees 테이블의 행도 자동으로 삭제되게 된다

## ON UPDATE CASCADE 예제

다음은 ON UPDATE CASCADE를 사용하는 예제이다

~~~sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL
);

CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(100) NOT NULL,
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES departments(department_id)
    ON UPDATE CASCADE
);
~~~

~~~sql
-- 부서 ID 수정
UPDATE departments SET department_id = 2 WHERE department_id = 1;
-- department_id가 1에서 2로 변경되면, 이를 참조하는 모든 직원 정보의 department_id도 2로 변경됩니다.
~~~

위 예제에서는 departments 테이블의 기본 키인 department_id가 수정되면 이를 참조하는 모든 employees 테이블의 외래 키도 자동으로 수정된디

## CASCADE 주의사항

위 예제에서 살펴볼 수 있듯이 CASCADE 명령어는 유용하지만 잘못 사용하게 되면 의도치 않게 데이터 손실이 발생할 수 있기 떄문에 사용하기 전에 중요한 데이터를 다루는 경우에는 데이터를 백업해 두는 것이나 테스트 환경에서 충분히 검증해 보는 것이 좋다
