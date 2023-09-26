# SQL Query for finding students whose best friends got offered a higher salary than them

## Introduction
There are given three tables: Students, Friends and Packages.
Students contains two columns: ID and Name.
Friends contains two columns:ID and Friend_ID (ID of the ONLY best friend).
Packages contains two columns: ID and Salary (offered salary in $ thousands per month).

Write a query to output the names of those students whose best friends got offered a higher salary than them. Names must be ordered by the salary amount offered to the best friends.
It is guaranteed that no two students got same salary offer.

## SQL Query
```sql
SELECT name
FROM friends as f
JOIN packages as p
ON f.id = p.id
JOIN packages as p2
ON f.friend_id = p2.id
JOIN students as s
ON f.id = s.id
WHERE p2.salary > p.salary
ORDER BY p2.salary
