# MySQL



- [Interview Queries](#interview-queries)



#### Interview Queries

##### Q1. Write an SQL query to fetch “FIRST_NAME” from Worker table in upper case.

**Ans:** select upper(FIRST_NAME) from Worker;

**Q2. Write an SQL query to print the first three characters of FIRST_NAME from Worker table.**

**Ans:** select substring(FIRST_NAME,1,3) from Worker;

**Q3. Write an SQL query to find the position of the alphabet (‘a’) in the first name column ‘Amitabh’ from Worker table.**

**Ans:** select INSTR(FIRST_NAME, BINARY 'a') from Worker where FIRST_NAME = 'Amitabh';

**Notes.**

- The INSTR method is in case-sensitive by default.
- Using Binary operator will make INSTR work as the case-sensitive function.

**Q4. Write an SQL query to print the FIRST_NAME from Worker table after removing white spaces from the right side.**

**Ans:** select RTRIM(FIRST_NAME) from Worker;

**Q5. Write an SQL query to print the DEPARTMENT from Worker table after removing white spaces from the left side.**

**Ans:** select LTRIM(DEPARTMENT) from Worker;

**Q6. Write an SQL query that fetches the unique values of DEPARTMENT from Worker table and prints its length.**

**Ans:** select distinct length(DEPARTMENT) from Worker;

**Q7. Write an SQL query to print the FIRST_NAME from Worker table after replacing ‘a’ with ‘A’.**

**Ans:** select REPLACE(FIRST_NAME, 'a', 'A') from Worker;

**Q8. Write an SQL query to print the FIRST_NAME and LAST_NAME from Worker table into a single column COMPLETE_NAME. A space char should separate them.**

**Ans:** select CONCAT(FIRST_NAME, ' ', LAST_NAME) AS 'COMPLETE_NAME' from Worker;

**Q9. Write an SQL query to print details of the Workers whose FIRST_NAME contains ‘a’.**

**Ans:** select * from Worker where FIRST_NAME like '%a%';

**Q10. Write an SQL query to print details of the Workers whose FIRST_NAME ends with ‘a’.**

**Ans:** select * from Worker where FIRST_NAME like '%a';

**Q11. Write an SQL query to print details of the Workers whose FIRST_NAME ends with ‘h’ and contains six alphabets.**

**Ans:** select * from Worker where FIRST_NAME like '_____h';

**Q12. Write an SQL query to print details of the Workers who have joined in Feb’2014.**

**Ans:** select * from Worker where year(JOINING_DATE) = 2014 and month(JOINING_DATE) = 2;

**Q13. Write an SQL query to fetch the no. of workers for each department in the descending order.**

**Ans:** 

```
SELECT DEPARTMENT, count(WORKER_ID) No_Of_Workers 
FROM worker 
GROUP BY DEPARTMENT 
ORDER BY No_Of_Workers DESC;
```

**Q14. Write an SQL query to fetch duplicate records having matching data in some fields of a table.**

**Ans:** 

```
SELECT WORKER_TITLE, AFFECTED_FROM, COUNT(*)
FROM Title
GROUP BY WORKER_TITLE, AFFECTED_FROM
HAVING COUNT(*) > 1;
```

**Q15. Write an SQL query to show only odd rows from a table.**

**Ans:** SELECT * FROM Worker WHERE MOD (WORKER_ID, 2) <> 0;

**Q16. Write an SQL query to show only even rows from a table.**

**Ans:** SELECT * FROM Worker WHERE MOD (WORKER_ID, 2) = 0;

**Q17. Write an SQL query to fetch intersecting records of two tables.**

**Ans:** 

```
(SELECT * FROM Worker)
INTERSECT
(SELECT * FROM WorkerClone);
```

**Q18. Write an SQL query to show records from one table that another table does not have.**

**Ans:** 

```sql
SELECT t1.name
FROM table1 t1
LEFT JOIN table2 t2 ON t2.name = t1.name
WHERE t2.name IS NULL
```

**Q19. Write an SQL query to show the current date and time.**

**Ans:** 

```sql
SELECT CURDATE();
SELECT NOW();
SELECT getdate();
SELECT SYSDATE FROM DUAL;
```

**Q20. Write an SQL query to show the top n (say 10) records of a table.**

**Ans:** 

```sql
SELECT * FROM Worker ORDER BY Salary DESC LIMIT 10;
SELECT TOP 10 * FROM Worker ORDER BY Salary DESC;
```

**Q21. Write an SQL query to determine the nth (say n=5) highest salary from a table.**

**Ans:** SELECT Salary FROM Worker ORDER BY Salary DESC LIMIT n-1,1;

**Q22. Write an SQL query to fetch the list of employees with the same salary.**

**Ans:** 

```sql
Select distinct W.WORKER_ID, W.FIRST_NAME, W.Salary 
from Worker W, Worker W1 
where W.Salary = W1.Salary 
and W.WORKER_ID != W1.WORKER_ID;
```

**Q23. Write an SQL query to show the second highest salary from a table.**

**Ans:** 

```sql
Select max(Salary) from Worker 
where Salary not in (Select max(Salary) from Worker);
```

**Q24. Write an SQL query to show one row twice in results from a table.**

**Ans:** 

```sql
select FIRST_NAME, DEPARTMENT from worker W where W.DEPARTMENT='HR' 
union all 
select FIRST_NAME, DEPARTMENT from Worker W1 where W1.DEPARTMENT='HR';
```

**Q25. Write an SQL query to fetch the first 50% records from a table.**

**Ans:** 

```sql
SELECT *
FROM WORKER
WHERE WORKER_ID <= (SELECT count(WORKER_ID)/2 from Worker);
```

**Q26. Write an SQL query to fetch the departments that have less than five people in it.**

**Ans:** 

```sql
SELECT DEPARTMENT, COUNT(WORKER_ID) as 'Number of Workers' FROM Worker GROUP BY DEPARTMENT HAVING COUNT(WORKER_ID) < 5;
```

**Q27. Write an SQL query to show all departments along with the number of people in there.**

**Ans:** 

```sql
SELECT DEPARTMENT, COUNT(DEPARTMENT) as 'Number of Workers' FROM Worker GROUP BY DEPARTMENT;
```

**Q28. Write an SQL query to show the last record from a table.**

**Ans:**

```sql
Select * from Worker where WORKER_ID = (SELECT max(WORKER_ID) from Worker);

select * from Worker order by WORKER_ID desc limit 1
```

**Q29. Write an SQL query to fetch the first row of a table.**

**Ans:**

```sql
Select * from Worker where WORKER_ID = (SELECT min(WORKER_ID) from Worker);

select * from Worker order by WORKER_ID limit 1
```

**Q30. Write an SQL query to fetch the last five records from a table.**

**Ans:** select * from Worker order by WORKER_ID DESC limit 5

**Q31. Write an SQL query to print the name of employees having the highest salary in each department.**

**Ans:** SELECT MAX(Salary), DEPARTMENT FROM Worker GROUP BY DEPARTMENT ORDER BY Salary DESC

**Q32. Write an SQL query to fetch three max salaries from a table.**

**Ans:** SELECT DISTINCT(SALARY) from Worker order by SALARY desc limit 3

**Q33. Write an SQL query to fetch three min salaries from a table.**

**Ans:** SELECT DISTINCT(SALARY) from Worker order by SALARY asc limit 3

**Q34. Write an SQL query to fetch departments along with the total salaries paid for each of them.**

**Ans:** SELECT DEPARTMENT, sum(Salary) from worker group by DEPARTMENT;

**Q35. Write an SQL query to fetch the names of workers who earn the highest salary.**

**Ans:** SELECT * from Worker order by SALARY desc limit 1



[Queries Reference - 1](https://www.techbeamers.com/sql-query-questions-answers-for-practice/)