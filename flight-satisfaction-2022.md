# Flight Satisfaction 2022

```sql
// A major airline has enlisted Tata Consultancy's help to improve customer satisfaction on its flights. Their goal is to increase customer satisfaction among people between the ages of 30 and 40.
// You've been tasked with calculating the customer satisfaction average for this age group across all three flight classes for 2022.
// Return the class with the average of satisfaction rounded to the nearest whole number.
// Note: Only survey results from flights in 2022 are included in the dataset.

select distinct class, AVG(satisfaction) OVER(PARTITION BY class) as avg 
from survey_results as r 
join loyalty_customers as l 
on r.cust_id = l.cust_id
where age BETWEEN 30 AND 40


```
