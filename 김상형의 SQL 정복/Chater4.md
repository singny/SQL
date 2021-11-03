# Chapter4. SELECT
## 4-1. 데이터 읽기
### * 기본 형식
```
SELECT 필드목록 FROM 테이블 [WHERE 조건] [ORDER BY 정렬기준];
```
### * 필드에 대한 별명 지정
```
필드명 [AS] "별명"
SELECT name AS 도시명, area AS "면적(제곱Km)", popu AS "인구(만명)" FROM tCity;  -- 예제
```
#### - 별명에 공백과 특수 문자가 있을경우 반드시 따옴표로 감싸야한다.
#### - 호환성 체크
##### -> 오라클 : 별명에 큰 따옴표만 쓸 수 있다.
##### -> SQL Server : 작은 따옴표, 큰 따옴표, [] 기호로 별명을 감싼다. 별명 = 필드 형식도 지원한다.
##### -> MariaDB : 작은 따옴표, 큰 따옴표로 별명을 감싼다.
### * 간단한 계산기
```
SELECT 수식 FROM dual;
```
#### - dual : 1행 1열 더미 테이블
## 4-2. 조건문
### * 예제코드
```
SELECT * FROM tCity WHERE area > 1000;
SELECT name, area FROM tCity WHERE area > 1000;
SELECT * FROM tCity WHERE name = '서울';               -- 문자열은 ' ' 사용
```
### * 연습문제
#### 1. 인구가 10만명 미만인 도시의 이름을 출력하라.
```
SELECT name FROM tCity WHERE popu < 10;
```
#### 2. 전라도에 있는 도시의 정보를 출력하라.
```
SELECT * FROM tCity WHERE region = '전라';
```
#### 3. 월급이 400만원 이상인 직원의 이름을 출력하라.
```
SELECT name FROM tStaff WHERE salary >=400;
```
### * NULL 비교
```
SELECT * FROM tStaff WHERE score IS NULL;     -- 예제
```
#### - NULL이 아니라는 조건
```
SELECT * FROM tStaff WHERE score IS NOT NULL;   -- 예제
```
### * 논리 연산자
#### - AND의 우선 순위가 OR보다 높다.
#### - 예제코드
```
SELECT * FROM tCity WHERE popu >= 100 AND area >= 700;
```
```
SELECT * FROM tCity WHERE region = '경기' AND popu >= 50 OR area >= 500;
SELECT * FROM tCity WHERE region = '경기' AND (popu >= 50 OR area >= 500);
```
### * NOT 연산자 : 진위 여부를 반대로 바꾼다.
#### - 예제코드
```
SELECT * FROM tCity WHERE region != '경기';
SELECT * FROM tCity WHERE NOT(region = '경기');
```
### * 연습문제
#### 1. 직원 목록에서 월급이 300 미만이면서 성취도는 60이상인 직원이 누구인지 조사하라.
```
SELECT name FROM tStaff WHERE salary < 300 AND score >= 60;
```
#### 2. 영업부의 여직원 이름을 조사하라.
```
SELECT name FROM tStaff WHERE depart = '영업부' AND gender = '여';
```
### * LIKE
#### - 와일드 카드
##### -> % : 복수개의 문자와 대응한다. %자리에는 임의 개수의 임의 문자가 올 수 있다.
##### -> _ : 하나의 문자와 대응한다. _자리에 하나의 임의 문자가 올 수 있다.
##### -> [] : []안에 포함된 문자 리스트 중 하나의 문자와 대응한다.
##### -> [^ ] : [^ ]안에 포함된 문자 리스트에 포함되지 않은 하나의 문자와 대응한다.
#### - 예제코드
```
SELECT * FROM tCity WHERE name LIKE '%천%';
SELECT * FROM tCity WHERE name NOT LIKE '%천%';
```
##### -> TRIM : 공백 자르기
```
SELECT * FROM tCity WHERE TRIM(name) LIKE '%천';
```
##### -> ESCAPE
```
WHERE sale LIKE '%30#%' ESCAPE '#'
```
### * 연습문제
#### 1. 직원 목록에서 '정'씨를 조사하라.
```
SELECT * FROM tStaff WHERE name LIKE '정%';
```
#### 2. 이름에 '신'자가 포함된 직원을 조사하라.
```
SELECT * FROM tStaff WHERE name LIKE '%신%';
```
### * BETWEEN
#### - 미만, 초과는 지정할 수 없는 활용성의 한계가 있다.
#### - 문자열이나 날짜 등에도 사용할 수 있다.
#### - 예제코드
```
SELECT * FROM tCity WHERE popu BETWEEN 50 AND 100;
```
```
SELECT * FROM tStaff WHERE name BETWEEN '가' AND '사';
SELECT * FROM tStaff WHERE joindate BETWEEN '20150101' AND '20180101';
```
### * 연습문제
#### 1. 면적 500 ~ 1000 사이의 도시 목록을 조사하라.
```
SELECT name FROM tCity WHERE area BETWEEN 500 AND 1000;
```
#### 2. 월급이 200만원대인 직원의 목록을 구하라.
```
SELECT name FROM tStaff WHERE salary BETWEEN 200 AND 299;
```
### * IN : 불연속적인 값 여러 개의 목록을 제공하여 이 목록과 일치하는 레코드를 검색
#### - IN연산자와 LIKE연산자는 같이 쓸 수 없다.
#### - 예제코드
```
SELECT * FROM tCity WHERE region IN ('경상','전라');
SELECT * FROM tCity WHERE region NOT IN ('경상','전라');
```
### * 연습문제
#### 1. 총무부나 영업무에 근무하는 직원의 목록을 조사하라.
```
SELECT * FROM tStaff WHERE depart IN ('총무부','영업부');
```
#### 2. 인사과나 영업부에 근무하는 대리의 목록을 조사하라.
```
SELECT * FROM tStaff WHERE depart IN ('인사과','영업부') and grade = '대리';
```
#### 3. 차장급 이상의 여직원 목록을 조사하라.
```
SELECT * FROM tStaff WHERE grade IN ('차장','부장','이사') and gender = '여';
```



