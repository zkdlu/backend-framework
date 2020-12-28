### 기본 쿼리
mysql, oracle, mssql마다 일부 다른 부분이 있으나 거의 유사 함.
```sql
# 데이터베이스 추가, 목록 보기
CREATE DATABASE test_db default CHARACTER SET UTF8;
SHOW DATABASEs;
```
```sql
# 데이터베이스, 테이블 삭제
DROP TABLE test_table;
DROP DATABASE test_db;
```
```sql
# 데이터베이스 사용자 추가
GRANT ALL PRIVILEGES ON test_db.* TO user@localhost IDENTIFIED BY 'password'
mysql -u user -p 'password'
USE test_db;
```

```sql
# 테이블 생성
CREATE TABLE test_table
(
  _id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(20) NOT NULL,
  description VARCHAR(255) DEFAULT 'Hello'
) ENGINE=INNODB;

or 

CREATE TABLE test_table
(
  _id INT AUTO_INCREMENT,
  name VARCHAR(20) NOT NULL,
  description VARCHAR(255) DEFAULT 'Hello',
  PRIMARY KEY(_id)
) ENGINE=INNODB;

DESCRIBE test_table
```

```sql
# 데이터 삽입
INSERT INTO test_table (name, description) VALUES ('건', 'hello');
```
```sql
# 데이터 제거
DELETE FROM test_table WHERE name = '건';
```
```sql
# 데이터 변경
UPDATE test_table
SET name = '건건'
WHERE name = '건';
```
```sql
# 데이터 조회
SELECT * FROM test_table;
SELECT _id, name FROM test_table;
```

```sql
# 조건, 정렬
SELECT * FROM test_table
WHERE _id = 1
ORDER BY _id #desc;
```

```sql
# 연산자
논리연산(AND, OR, NOT), 부등호(>, >=, <, <=, =, !=(<>와 동일), 와일드카드(LIKE, %)
SELECT * FROM test_table
WHERE _id > 0 AND name NOT LIKE '건%';
```

```sql
# 테이블 변경
ALTER TABLE test_table RENAME TO test_tb;
ALTER TABLE test_tb ADD COLUMN hello INT NOT NULL; # AFTER _id 또는 FIRST로 위치 지정 가능
ALTER TABLE test_tb ADD PRIMARY KEY(_id);
ALTER TABLE test_tb DROP COLUMN hello DROP PRIMARY KEY;
```
> 1. 이름 변경 RENAME
> 2. 컬럼, 제약조건 추가 AD
> 3. 테이블 변경 CHANGE, MODIFY
> 4. 제약조건 제가 DROP

### 내장 함수
COUNT, SUM, AVG, MIN, MAX 등
```sql
# COUNT
SELECT COUNT(_id) FROM test_tb;
# SUM
SELECT SUM(hello) FROM test_tb;
```
- GROUP BY와 함께 사용
```sql
SELECT name, COUNT(*)
FROM test_tb
GROUP BY name;
```

문자열 내장 함수
RIGHT, SUBSTRING, SUBSTRING_INDEX, UPPER
```sql
# RIGHT (오른쪽 2글자만 읽음)
SELECT RIGHT(name, 2) FROM test_tb;
# SUBSTRING (2번째 위치부터 2글자 읽음)
SELECT SUBSTRING(name, 2, 2) FROM test_tb; 
# SUBSTRING_INDEX ('a'가 2번째로 나올때까지 읽음)
SELECT SUBSTRING_INDEX(name, 'a', 2) FROM test_tb; 
```

### Join
1. INNER Join
```sql
SELECT a.id, b.name
FROM A as a
(INNER) JOIN B as b # INNER 
ON a.id = b.id
```
> 교집합 관계 (A ∩ B)

2. LEFT OUTER, RIGHT OUTER Join
```sql
SELECT a.id, b.name
FROM A as a
LEFT JOIN B as b 
# RIGHT JOIN B as b
ON a.id = b.id
```
> A + (A ∩ B) 관계

3. OUTER Join
```sql
SELECT a.id, b.name
FROM A as a
JOIN B as b
ON a.id <> b.id
```
> A + B - (A ∩ B) 관계

4. SELF Join
```sql
SELECT c.id as child, p.parent_id as parent
FROM A as c
JOIN A as p
ON c.parent_id = p.id
```
> Tree 구조
