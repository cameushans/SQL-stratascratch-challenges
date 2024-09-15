---
description: >-
  Find the top three distinct salaries for each department. Output the
  department name and the top 3 distinct salaries by each department. Order your
  results alphabetically by department
---

# Distinct Salaries

```sql
// Some code
WITH IDENTIFY_MAX_SALARY AS (select *, MAX(salary) OVER(PARTITION BY department  , salary ORDER BY  department) AS mx, 
DENSE_RANK() OVER(PARTITION BY department ORDER BY salary DESC) AS rnk FROM twitter_employee)

,RANK_SALARY AS (SELECT DISTINCT rnk, department, mx FROM IDENTIFY_MAX_SALARY 
WHERE rnk <= 3
ORDER BY department, mx DESC)

SELECT department, mx FROM RANK_SALARY 


```
