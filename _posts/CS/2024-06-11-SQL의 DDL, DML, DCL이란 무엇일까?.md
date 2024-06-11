---
title: SQL의 DDL, DML, DCL이란 무엇일까?
date: 2024-06-11 20:00:00 +/-0000
categories: [CS]
tags: [CS]
toc: true
pin: true
---

CS를 공부하다보면 데이터베이스 파트에서 DDL, DML, DCL을 마주하게 된다 이는 데이터베이스 관리 시스템(DBMS)에서 사용하는 SQL 명령어들을 분류한 것인데 이들은 각각 특정한 목적과 기능을 가지고 있다

# DDL (Data Definition Language)

데이터베이스의 구조를 정의하고 수정하는 데 사용되는 명령어들로 테이블, 인덱스, 뷰, 스키마 등을 생성, 수정, 삭제할 때 사용된다

**명령어 목록**

* CREATE: 새로운 데이터베이스 객체(테이블, 인덱스 등)를 생성
* ALTER: 기존의 데이터베이스 객체를 수정
* DROP: 데이터베이스 객체를 삭제
* TRUNCATE: 테이블의 모든 데이터를 삭제하고 테이블 구조는 유지

# DML (Data Manipulation Language)

데이터베이스 내의 데이터에 대해 조작(삽입, 수정, 삭제, 조회)하는 데 사용되는 명령어들이다

**명령어 목록**

* SELECT: 데이터 조회
* INSERT: 새로운 데이터 삽입
* UPDATE: 기존 데이터 수정
* DELETE: 기존 데이터 삭제

# DCL (Data Control Language)

데이터베이스의 접근 권한과 보안을 관리하는 데 사용되는 명령어들이다

**명령어 목록**

* GRANT: 사용자에게 특정 권한 부여
* REVOKE: 사용자에게 부여된 권한 회수
* ROLLBACK: 트랜잭션의 작업을 취소
* COMMIT: 트랜잭션의 작업을 저장

