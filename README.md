---
description: >-
  Which company had the biggest month call decline from March to April 2020?
  Return the company_id and calls difference for the company with the highest
  decline.
---

# Call Declines

```sql
// Some code

with march as (select company_id, count(call_id) as n_call from rc_calls as c
join rc_users as u
on c.user_id = u.user_id
where month(date) = 3
group by company_id
),
april as (select company_id, count(call_id) as n_call from rc_calls as c
join rc_users as u
on c.user_id = u.user_id
where month(date) = 4
group by company_id
),
diff as (select m.company_id, ap.n_call - m.n_call as total from march as m
join april as ap 
on m.company_id = ap.company_id
)

select company_id, total from diff
order by total 
limit 1


```
