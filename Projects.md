# SQL Query for finding date of projects

## Introduction
There are given a table, Projects, containing three columns: Task_ID, Start_Date and End_Date. It is guaranteed that the difference between the End_Date and the Start_Date is equal to 1 day for each row in the table.
If the End_Date of the tasks are consecutive, then they are part of the same project. We must to finding the total number of different projects completed.

## SQL Query
```sql
SELECT start_date, end_date
FROM
    (SELECT start_date, row_number() OVER() AS num
    FROM projects
    WHERE start_date NOT IN (SELECT end_date FROM projects)
    ORDER BY start_date) AS a
    JOIN 
    (SELECT end_date, row_number() OVER() AS num
    FROM projects
    WHERE end_date NOT IN (SELECT start_date FROM projects)
    ORDER BY end_date) AS b
    ON a.num = b.num
ORDER BY DATEDIFF(end_date, start_date), start_date
