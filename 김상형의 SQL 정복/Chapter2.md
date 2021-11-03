# Chapter2. 오라클
## 2-1. 학습환경설치 : SQL Developer 설치
### * 단축기
#### - 행 삽입 : Ctrl + I
#### - 커밋 : F11
#### - 행 삭제 : Ctrl + D
#### - 쿼리창열기 : Alt + F10
#### - 쿼리 실행 : Ctrl + Enter
## 2-2. 쿼리
### * 쿼리문의 분류
#### - DDL(Data Definition Language) : DB 오브젝트를 생성, 삭제, 변경한다. CREATE, DROP, ALTER 등의 명령이 있다. DB를 디자인하는 관리자가 이 부류의 명령을 주로 사용한다.
#### - DML(Data Manipulation Language) : DB를 조회, 삽입, 삭제, 변경한다. SELECT, INSERT, DELECT, UPDATE 명령 등이 있다. 응용 프로그램 개발자가 주로 사용한다.
#### - DCL(Data Control Language) : 사용자와 권한을 관리하는 GRANT, DENY, REVOKE 등의 명령이 있다. DBA가 주로 사용하며 일반 개발자는 사용할 일이 드물다.
## 2-3. 쿼리 실습
### * 테이블 생성
```
CREATE TABLE 테이블이름
(
  필드정보,
  필드정보,
  ....
);
```
### * 테이블 살제
```
DROP TABLE 테이블이름;
```
### * SQL 주석
#### 1) /* */
#### 2) --
