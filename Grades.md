# SQL Query for finding grades of students

## Introduction
We are given two tables: Students and Grades. Students contains three columns ID, Name and Marks. Grades contains columns with description grade - number (0-10).

We have a task to generate a report containing three columns: Name, Grade and Mark. We don't want the NAMES of those students who received a grade lower than 8. 
The report must be in descending order by grade -- i.e. higher grades are entered first. 
If there is more than one student with the same grade (8-10) assigned to them, order those particular students by their name alphabetically.
Finally, if the grade is lower than 8, use "NULL" as their name and list them by their grades in descending order. 
If there is more than one student with the same grade (1-7) assigned to them, order those particular students by their marks in ascending order.

## SQL Query
```sql
SELECT CASE WHEN grade > 7 THEN name ELSE 'NULL' END AS name,
        grade, marks
FROM students
LEFT JOIN grades
ON students.marks BETWEEN grades.Min_Mark AND grades.Max_Mark
ORDER BY grade desc, name, marks
