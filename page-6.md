---
description: >-
  For each request_id, the first call is an “initial call” and all the following
  calls are “update calls”.  How many customers have called 3 or more times
  between 3 PM and 6 PM
---

# Rush Hour Calls   Interview Question

```sql
// The first step is to count the id by request id that represent the number of call for a given customer
// the time series data in created_on represent the extracted hours from a date time
// Then count the count of id that is greteror equal to 3 

with TOTAL_CALL_PER_CUSTOMER as (select  request_id, count(id) as c_call from redfin_call_tracking
where HOUR(created_on) >= 3 AND  HOUR(created_on) <= 6
group by request_id)

SELECT COUNT(c_call) FROM  TOTAL_CALL_PER_CUSTOMER 
WHERE c_call >= 3 
```
