---
description: >-
  From users who had their first session as a viewer, how many streamer sessions
  have they had? Return the user id and number of sessions in descending order.
  In case there are users with the same numbe
---

# Viewers Turned Streamers



```sql
// My code
with STARTED_POINT
 as (select user_id, session_type, session_id, min(session_start) over(partition by user_id) as started
from twitch_sessions
)

select user_id, count(session_id)
from twitch_sessions
where (session_id, session_start) in (select session_id, started from STARTED_POINT)
and session_type = 'viewer'
group by user_id

```
