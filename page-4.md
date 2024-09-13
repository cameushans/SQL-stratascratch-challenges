---
description: >-
  Meta/Facebook is quite keen on pushing their new programming language Hack to
  all their offices. They ran a survey to quantify the popularity of the
  language and send it to their employees.
---

# Fans vs Opposition

\
To promote Hack they have decided to pair developers which love Hack with the ones who hate it so the fans can convert the opposition. Their pair criteria is to match the biggest fan with biggest opposition, second biggest fan with second biggest opposition, and so on. Write a query which returns this pairing. Output employee ids of paired employees. Sort users with the same popularity value by id in ascending order.

Duplicates in pairings can be left in the solution. For example, (2, 3) and (3, 2) should both be in the solution.\`

```sql
// My solution

with fan as (select *,
row_number() over( order by popularity desc, employee_id) as rnk
from facebook_hack_survey),

opposition as (select *,
row_number() over( order by popularity , employee_id) as rnk
from facebook_hack_survey)

select fan.employee_id, opposition.employee_id from fan join opposition
on fan.rnk = opposition.rnk

```
