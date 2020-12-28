```sql
# 데이터베이스 추가, 목록 보기
CREATE DATABASE test_db default CHARACTER SET UTF8;
SHOW DATABASEs;
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


### Join
1. INNER Join
```sql
SELECT a.id, b.name
FROM A as a
JOIN B as b
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
