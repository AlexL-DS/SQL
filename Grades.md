We are given two tables: Students and Grades. Students contains three columns ID, Name and Marks.
Grades contains columns with description grade - number (0-10).

We have a task to generate a report containing three columns: Name, Grade and Mark. We don't want the NAMES of those students who received a grade lower than 8. 
The report must be in descending order by grade -- i.e. higher grades are entered first. 
If there is more than one student with the same grade (8-10) assigned to them, order those particular students by their name alphabetically.
Finally, if the grade is lower than 8, use "NULL" as their name and list them by their grades in descending order. 
If there is more than one student with the same grade (1-7) assigned to them, order those particular students by their marks in ascending order.

Let's write a SQL-query.

***
select case when grade > 7 then name else 'NULL' end as name,
    grade, marks
from students
left join grades
on students.marks between grades.Min_Mark and grades.Max_Mark
order by grade desc, name, marks
***
