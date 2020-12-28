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
