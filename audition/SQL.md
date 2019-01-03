B - (A ∩ B)

```sql
SELECT
	b.*
FROM
	B_table b
LEFT JOIN A_table a ON b.Bid = a.Bid
WHERE
	a.Aid IS NULL

SELECT
	b.*
FROM
	B_table b
WHERE
	b.Bid NOT IN (
		SELECT
			b.Bid
		FROM
			B_table b
		INNER JOIN A_table a ON b.Bid = a.Bid
	)
```
平均分大于80分的学生，并按平均分分数从大到小排列

```sql
SELECT
	t.student_name,
	avg(t.score)
FROM
	course t
GROUP BY
	t.student_id
HAVING
	avg(t.score) > 80
ORDER BY
	avg(t.score) DESC
```

Oracle SQL: Update a table with data from another table

```sql
UPDATE table1 t1
SET (NAME, DESC) = (
	SELECT
		t2. NAME,
		t2. DESC
	FROM
		table2 t2
	WHERE
		t1. ID = t2. ID
)
WHERE
	EXISTS (
		SELECT
			1
		FROM
			table2 t2
		WHERE
			t1. ID = t2. ID
	)

update t1 
set t1.colmun = t2.column
from table t1,table t2
where t1.id = t2.id

UPDATE CS_ORDER o
SET (o.CUSTOMER_ID) = (
	SELECT
		c. ID
	FROM
		CS_CUSTOMER c
	WHERE
		o.CUSTOMER_CODE = c.CUSTOMER_CODE
		and c.company_id = o.company_id
)
WHERE o.CUSTOMER_ID IS NULL
```

MySQL 

```sql
UPDATE a_table a,
 b_table b
SET a. CODE = b. CODE
WHERE
	a.id = b.id
```