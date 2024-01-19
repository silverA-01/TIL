# MySQL 시작하기
## DMBS의 개요
### DBMS
- DB(Database_데이터베이스) : 여러 가지 데이터들의 집합, 모음
- DBMS(Database Management System) : 관계형 데이터베이스 관리 시스템
- DBMS 종류별 설명 영상
  - [7 Database Paradigms](https://youtu.be/W2Z7fbCLSTw)
  - [개발시 데이터베이스 선택 가이드](https://youtu.be/ZVuHZ2Fjkl4)


### RDBMS
Related Databse Manegement System (관계형 데이터베이스 관리 시스템)으로 DBMS의 종류중 하나이다.
- 종류 : MySQL, PostgreSQL, MariaDB, Microsoft SQL Server, Oracle Database
- SQL(Structed Query Language)
  - 구조화된 쿼리(요청) 언어
  - 전체 DBMS을 위한 언어가 아니라, RDBMS에서 DB를 저장하도록 명령하는 특수목적언어가 SQL이다.
  - RDBMS마다 SQL은 공통적인 부분도 있으나, 조금씩 다르게 사용하는 부분이 있다.

## MySQL
![MySQL](https://t1.daumcdn.net/thumb/R720x0/?fname=http://t1.daumcdn.net/brunch/service/user/797z/image/3r7sR9IJuBZfq4M5yKrLWIt3rZE.jpg)
- RDMBS 종류 중 하나
- 원래 무료 프로그램이었으나 Oracle사가 최근 인수하여 유료버전과 무료버전 두 가지가 나오게 되었다.
- 유료임에도 Orcale사에서 DB관리를 맡아주는 시스템 안정성때문에, 국내 대기업에서 많이 사용하는 편이다.  

## SQL 작성시 주의사항
- SQL 고정명령어는 `대문자`로, 내가 만든 이름은 `소문자`로 표기
  - 모두 대문자 or 소문자로 작성해도 동작은 하지만 가독성을 위해 위와 같이 표기한다.
- 띄어쓰기와 줄 바꿈은 동작에 있어서 영향을 미치지 않지만 가독성을 위해 적절히 잘 사용해준다.
- 반드시 명령어 끝에는 `;(세미콜론)`을 적기


## MySQL 명령어
- `--- `으로 시작하면 주석(comment)을 의미하고 결과에 영향을 미치지 않는다.
- SQL 작성 후 실행(동작)
  - `Ctrl + Enter`
    - ;이 있는 각 라인마다 한 단위로 실행된다.
    - 각 라인은 독립적이다.
  - MySQL Workbench에서 번개 아이콘을 누르면 전체 SQL이 실행된다.
    - ![MySQL 실행 아이콘](https://postfiles.pstatic.net/MjAyMzEyMDVfMTQ4/MDAxNzAxNzg1OTUzMzcz.ilIao-Q8dVrGrSJ1Bi3Nx9H2DyoBnB_7CTuX4mt6Axwg.4_A3SfoyftKygtCV6YnQi3uaMLbZo1d7-vqThuAQ_eUg.PNG.mita_02/image.png?type=w773)
    - 원하는 SQL 부분을 드래그 후 번개 아이콘을 누르면 드래그 된 부분이 실행된다.

- `Ctrl + t` : 새로운 창을 생성한다.


## 데이터베이스(DB) 관련 SQL
### DB 생성
```sql
CREATE DATABASE practice
```
- `practice`라는 이름의 DB를 생성한다.

### DB 확인
- DB 확인하기. 위의 `practice` DB가 잘 만들어졌는지 확인할 수 있다.
```sql
SHOW DATABASES;
```

### DB 삭제
```sql
DROP DATABSE practice;
```
- `practice` DB를 삭제한다.

### DB 사용
원하는 DB를 사용할 때 해당 DB에 테이블을 생성할 수 있다.

```sql
USE practice;
```
- `practice` DB를 사용한다. 
- SCHEMAS UI창에서 해당 DB를 더블클릭한 것과 같은 결과이다. 이때 DB명이 Bold체로 바뀐다.


## 테이블(Table) 관련 SQL
DB는 테이블들의 집합이다.
- 테이블을 저장할 때는, 테이블을 어떤 정보를 저장할지 정하는 것이 중요하다.
- 어떤 정보를, 어떤 형식의 데이터로 저장할지 목적에 따라 지정한다.
- 데이터의 형식으로 정수, 문자, 통화, 날씨 및 시간등의 데이터를 지정한다.
  - 테이블을 구성하는 각각의 정보인 column에 특정한 데이터 형식을 지정함
  - 숫자형 데이터 형식으로 지정된 column에는 문자형 데이터를 입력할 수 없다. 입력할 경우 에러 발생.


### 1. 테이블 생성
> `people` 이라는 이름을 가진 테이블을 생성
> 
> `first_name` ⇒ 글자(20)
>
> `last_name` ⇒ 글자(20)
> 
> `age` ⇒ 정수
```sql
CREATE TABLE people(
    first_name, VARCHAR(20),
    last_name, VARCHAR(20)
    age, INT
);
```
-  `VARCHA(n)` : 문자를 의미. 문자는 n자 까지 사용할 수 있다.
- `INT` : 정수. Integer

### 2. 테이블 확인
현재 사용하고 있는 DB에 존재하는 모든 테이블을 보여달라는 뜻

```sql
SHOW TABLES;
```

### 3. 테이블 설명
특정 테이블에 Field, Type, Null 등의 정보가 나타난다.
```sql
DESC people;
```
- `DESC` : Describe 설명하다의 약자
- `people` 테이블에 대해 설명해주라는 뜻.


### 4. 테이블 삭제
```sql
DROP TABLE people;
```
- `people` 테이블을 삭제한다.


## 데이터 삽입
테이블은 Column과 row(record)가 존재한다.
  - column : 열.
  - row(reocrd) : 행. Table의 가로 줄을 의미한다.

### 1. 하나의 row 데이터 삽입
```sql
INSERT INTO people (fisrt_name, last_name, age)
VALUES ('Noah', 'Han', 22);
``` 
- 문자형 데이터는 ' '안에 데이터를 입력해야 한다.

```sql
INSERT INTO people (fisrt_name, last_name, age)
VALUES ('Noah', 22, 'Han');
```
- 위와 같이 테이블을 만들 때 설정한 데이터 형식에 맞지 않게 데이터를 입력한 경우, 에러 메세지가 뜨면서 실행되지 않는다.
- `last_name`의 데이터 형식은 VARCHAR(20)으로 문자형 데이터가 넣어져야 하고, `age`의 데이터 형식은 INT로 정수가 들어가야 한다.

### 2. 여러 개의 row 데이터 삽입하기
```sql
INSERT INTO people (fist_name, last_name, age)
VALUES
    ('Yejun', 'Nam', 22),
    ('Bonggu', 'Chae' 21),
    ('Eunho', 'Do', 20),
    ('Hamin', 'Yu', 19);
 ```
- `4 row(s) affected Records` 메세지로, 데이터 삽입 실행이 성공했음을 알 수 있다

### 테이블 전체 데이터 조회

```sql
SELECT * FROM people;
```
- `people` 테이블에 있는 전체 데이터를 조회한다는 뜻
