# Employees With Same Birth Month



```sql
// The resolution of the problem involve a pivot
// a pivot can be seen as a conversion of rows into columns 
// (maybe the condition is to have a number of finite values i dont know if o pivot on infinite values is relevant)
// you can see that i made, from a given value of a row, a new column 
// observe that birth_month is a sequence of finite number so maybe there exist a way of generate such a 
// sequence more "programmaticaly" 
// 

with cte as (select profession,
    CASE WHEN birth_month = 1 THEN count(employee_id) else 0 end as month_1,
    CASE WHEN birth_month = 2 THEN count(employee_id) else 0 end as month_2,
    CASE WHEN birth_month = 3 THEN count(employee_id) else 0 end as month_3,
    CASE WHEN birth_month = 4 THEN count(employee_id) else 0 end as month_4,
    CASE WHEN birth_month = 5 THEN count(employee_id)else 0 end as month_5,
    CASE WHEN birth_month = 6 THEN count(employee_id) else 0 end as month_6,
    CASE WHEN birth_month = 7 THEN count(employee_id) else 0 end as month_7,
    CASE WHEN birth_month = 8 THEN count(employee_id) else 0 end as month_8,
    CASE WHEN birth_month = 9 THEN count(employee_id) else 0 end as month_9,
    CASE WHEN birth_month = 10 THEN count(employee_id) else 0 end as month_10,
    CASE WHEN birth_month = 11 THEN count(employee_id) else 0 end as month_11,
    CASE WHEN birth_month = 12 THEN count(employee_id) else 0 end as month_12
from employee_list
GROUP BY 1, birth_month)

select profession, 
    MAX(month_1) AS month_1,
    MAX(month_2) AS month_2,
    MAX(month_3) AS month_3,
    MAX(month_4) AS month_4,
    MAX(month_5) AS month_5,
    MAX(month_6) AS month_6,
    MAX(month_7) AS month_7,
    MAX(month_8) AS month_8,
    MAX(month_9) AS month_9,
    MAX(month_10) AS month_10,
    MAX(month_11) AS month_11,
    MAX(month_12) AS month_12
from cte 
group by profession




```
