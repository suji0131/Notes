# SQL Interview Questions
[source](https://www.toptal.com/sql/interview-questions)

```
SELECT inv.ID, inv.BillingDate, cus.Name, ref.Name AS referredby_name
FROM Invoices inv
  LEFT JOIN Customers cus ON inv.CustomerID = cus.ID
  LEFT JOIN Customers ref ON cus.ReferredBy = ref.ID
ORDER BY inv.BillingDate

SELECT DISTINCT e.Salary
FROM Employee e
ORDER BY e.Salary DESC LIMIT 1 OFFSET 9


SELECT u.username, td.trainig_date, td.training_id, COUNT(td.user_training_id)
FROM training_details td
  LEFT JOIN users u ON td.user_id = u.user_id
GROUP BY u.username, td.trainig_date, td.training_id
HAVING COUNT(td.user_training_id) > 1
ORDER BY td.trainig_date DESC

SELECT TOP 100 u.user_id
FROM dbo.users u
WHERE u.user_id % 2 = 1
```


### What does UNION do? What is the difference between UNION and UNION ALL?
UNION merges the contents of two structurally-compatible tables into a single combined table. The difference between UNION and UNION ALL is that UNION will omit duplicate records whereas UNION ALL will include duplicate records.

It is important to note that the performance of UNION ALL will typically be better than UNION, since UNION requires the server to do the additional work of removing any duplicates. So, in cases where is certain that there will not be any duplicates, or where having duplicates is not a problem, use of UNION ALL would be recommended for performance reasons.

### List and explain the different types of JOIN clauses supported in ANSI-standard SQL.
ANSI-standard SQL specifies five types of JOIN clauses as follows:

INNER JOIN (a.k.a. “simple join”): Returns all rows for which there is at least one match in BOTH tables. This is the default type of join if no specific JOIN type is specified.

LEFT JOIN (or LEFT OUTER JOIN): Returns all rows from the left table, and the matched rows from the right table; i.e., the results will contain all records from the left table, even if the JOIN condition doesn’t find any matching records in the right table. This means that if the ON clause doesn’t match any records in the right table, the JOIN will still return a row in the result for that record in the left table, but with NULL in each column from the right table.

RIGHT JOIN (or RIGHT OUTER JOIN): Returns all rows from the right table, and the matched rows from the left table. This is the exact opposite of a LEFT JOIN; i.e., the results will contain all records from the right table, even if the JOIN condition doesn’t find any matching records in the left table. This means that if the ON clause doesn’t match any records in the left table, the JOIN will still return a row in the result for that record in the right table, but with NULL in each column from the left table.

FULL JOIN (or FULL OUTER JOIN): Returns all rows for which there is a match in EITHER of the tables. Conceptually, a FULL JOIN combines the effect of applying both a LEFT JOIN and a RIGHT JOIN; i.e., its result set is equivalent to performing a UNION of the results of left and right outer queries.

CROSS JOIN: Returns all records where each row from the first table is combined with each row from the second table (i.e., returns the Cartesian product of the sets of rows from the joined tables). Note that a CROSS JOIN can either be specified using the CROSS JOIN syntax (“explicit join notation”) or (b) listing the tables in the FROM clause separated by commas without using a WHERE clause to supply join criteria (“implicit join notation”).

### Question:
For a table orders having a column defined simply as customer_id VARCHAR(100), consider the following two query results:
```
SELECT count(*) AS total FROM orders;
+-------+
| total |
+-------+
|  100  |
+-------+
```
```
SELECT count(*) AS cust_123_total FROM orders WHERE customer_id = '123';
+----------------+
| cust_123_total |
+----------------+
|       15       |
+----------------+
```
Given the above query results, what will be the result of the query below?
```
SELECT count(*) AS cust_not_123_total FROM orders WHERE customer_id <> '123';
```
#### Answer:
The obvious answer is 85 (i.e, 100 - 15). However, that is not necessarily correct. Specifically, any records with a customer_id of NULL will not be included in either count (i.e., they won’t be included in cust_123_total, nor will they be included in cust_not_123_total). For example, if exactly one of the 100 customers has a NULL customer_id, the result of the last query will be:
```
+--------- ----------+
| cust_not_123_total |
+--------------------+
|         84         |
+--------------------+
```

### What will be the result of the query below? Explain your answer and provide a version that behaves correctly.
```
select case when null = null then 'Yup' else 'Nope' end as Result;
```
#### Answer:
This query will actually yield “Nope”, seeming to imply that null is not equal to itself! The reason for this is that the proper way to compare a value to null in SQL is with the is operator, not with =.

Accordingly, the correct version of the above query that yields the expected result (i.e., “Yup”) would be as follows:
```
select case when null is null then 'Yup' else 'Nope' end as Result;
```
This is because null represents an unknown value. If you don’t know the value, you can’t know whether it equals another value, so = null is always assumed to be false.

### Question:
Given the following tables:
```
sql> SELECT * FROM runners;
+----+--------------+
| id | name         |
+----+--------------+
|  1 | John Doe     |
|  2 | Jane Doe     |
|  3 | Alice Jones  |
|  4 | Bobby Louis  |
|  5 | Lisa Romero  |
+----+--------------+
```
```
sql> SELECT * FROM races;
+----+----------------+-----------+
| id | event          | winner_id |
+----+----------------+-----------+
|  1 | 100 meter dash |  2        |
|  2 | 500 meter dash |  3        |
|  3 | cross-country  |  2        |
|  4 | triathalon     |  NULL     |
+----+----------------+-----------+
```
What will be the result of the query below?
```
SELECT * FROM runners WHERE id NOT IN (SELECT winner_id FROM races)
```
Explain your answer and also provide an alternative version of this query that will avoid the issue that it exposes.

#### Answer:
Surprisingly, given the sample data provided, the result of this query will be an empty set. The reason for this is as follows: If the set being evaluated by the SQL NOT IN condition contains any values that are null, then the outer query here will return an empty set, even if there are many runner ids that match winner_ids in the races table.

Knowing this, a query that avoids this issue would be as follows:
```
SELECT * FROM runners WHERE id NOT IN (SELECT winner_id FROM races WHERE winner_id IS NOT null)
```
Note, this is assuming the standard SQL behavior that you get without modifying the default ANSI_NULLS setting.

### What is wrong with this SQL query? Correct it so it executes properly.
```
SELECT Id, YEAR(BillingDate) AS BillingYear 
FROM Invoices
WHERE BillingYear >= 2010;
```
#### Answer:
The expression BillingYear in the WHERE clause is invalid. Even though it is defined as an alias in the SELECT phrase, which appears before the WHERE phrase, the logical processing order of the phrases of the statement is different from the written order. Most programmers are accustomed to code statements being processed generally top-to-bottom or left-to-right, but T-SQL processes phrases in a different order.

The correct query should be:
```
SELECT Id, YEAR(BillingDate) AS BillingYear
FROM Invoices
WHERE YEAR(BillingDate) >= 2010;
```

### Question:
Given these contents of the Customers table:
```
Id	Name			ReferredBy
1	John Doe		NULL
2	Jane Smith		NULL
3	Anne Jenkins		2
4	Eric Branford		NULL
5	Pat Richards		1
6	Alice Barnes		2
```
Here is a query written to return the list of customers not referred by Jane Smith:
```
SELECT Name FROM Customers WHERE ReferredBy <> 2;
```
What will be the result of the query? Why? What would be a better way to write it?

#### Answer:
Although there are 4 customers not referred by Jane Smith (including Jane Smith herself), the query will only return one: Pat Richards. All the customers who were referred by nobody at all (and therefore have NULL in their ReferredBy column) don’t show up. But certainly those customers weren’t referred by Jane Smith, and certainly NULL is not equal to 2, so why didn’t they show up?

SQL Server uses three-valued logic, which can be troublesome for programmers accustomed to the more satisfying two-valued logic (TRUE or FALSE) most programming languages use. In most languages, if you were presented with two predicates: ReferredBy = 2 and ReferredBy <> 2, you would expect one of them to be true and one of them to be false, given the same value of ReferredBy. In SQL Server, however, if ReferredBy is NULL, neither of them are true and neither of them are false. Anything compared to NULL evaluates to the third value in three-valued logic: UNKNOWN.

The query should be written in one of two ways:
```
SELECT Name FROM Customers WHERE ReferredBy IS NULL OR ReferredBy <> 2
…or:

SELECT Name FROM Customers WHERE ISNULL(ReferredBy, 0) <> 2; -- (Or COALESCE() )
```
Watch out for the following, though!
```
SELECT Name FROM Customers WHERE ReferredBy = NULL OR ReferredBy <> 2
```
This will return the same faulty set as the original. Why? We already covered that: Anything compared to NULL evaluates to the third value in the three-valued logic: UNKNOWN. That “anything” includes NULL itself! That’s why SQL Server provides the IS NULL and IS NOT NULL operators to specifically check for NULL. Those particular operators will always evaluate to true or false.

Even if a candidate doesn’t have a great amount of experience with SQL Server, diving into the intricacies of three-valued logic in general can give a good indication of whether they have the ability learn it quickly or whether they will struggle with it.

### Question:
Assume a schema of Emp ( Id, Name, DeptId ) , Dept ( Id, Name).

If there are 10 records in the Emp table and 5 records in the Dept table, how many rows will be displayed in the result of the following SQL query:
```
Select * From Emp, Dept
```
Explain your answer.

#### Answer:
The query will result in 50 rows as a “cartesian product” or “cross join”, which is the default whenever the ‘where’ clause is omitted.

### Write a SQL query to find the 10th highest employee salary from an Employee table. Explain your answer.
(Note: You may assume that there are at least 10 records in the Employee table.)
```
SELECT DISTINCT Salary FROM Employee ORDER BY Salary DESC LIMIT 1 OFFSET 9;

or 

SELECT DISTINCT Salary FROM Employee ORDER BY Salary DESC LIMIT 9,1;
```

### Write a SQL query using UNION ALL (not UNION) that uses the WHERE clause to eliminate duplicates. Why might you want to do this?
You can avoid duplicates using UNION ALL and still run much faster than UNION DISTINCT (which is actually same as UNION) by running a query like this:
```
SELECT * FROM mytable WHERE a=X UNION ALL SELECT * FROM mytable WHERE b=Y AND a!=X
```
The key is the AND a!=X part. This gives you the benefits of the UNION (a.k.a., UNION DISTINCT) command, while avoiding much of its performance hit.



























