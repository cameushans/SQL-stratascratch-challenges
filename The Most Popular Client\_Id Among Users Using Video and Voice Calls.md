# The Most Popular Client\_Id Among Users Using Video and Voice Calls

Select the most popular client\_id based on a count of the number of users who have at least 50% of their events from the following list: 'video call received', 'video call sent', 'voice call received', 'voice call sent'.



```sql
// Some code


with PIVOT AS (select user_id,
client_id,
    case when event_type = 'video call received' then count(1) else 0  end 
    as video_call_received,
    case when event_type = 'video call sent' then count(1) else 0 end 
    as video_call_sent,
    case when event_type = 'voice call received' then count(1) else 0 end 
    as voice_call_received,
    case when event_type = 'voice call sent' then count(1) else 0 end 
    as voice_call_sent,
    case when event_type = 'message sent' then count(1) else 0 end 
    as message_sent,
    case when event_type = 'file received' then count(1) else 0 end 
    as file_received,
    case when event_type = 'message received' then count(1) else 0 end 
    as message_received,
    case when event_type = 'video call started' then count(1) else 0 end 
    as video_call_started,
    case when event_type = 'file_sent' then count(1) else 0 end 
    as file_sent,
    case when event_type = 'voice call started' then count(1) else 0 end 
    as voice_call_started,
    case when event_type = 'api message received' then count(1) else 0 end 
    as api_message_received
from fact_events
group by user_id, client_id)

,total as (SELECT 
    *, (
    video_call_received +
    video_call_sent +
    voice_call_received +
    voice_call_sent +
    message_sent +
    file_received +	
    message_received +
    video_call_started +
    file_sent +	
    voice_call_started +
    api_message_received
) as total,
 (video_call_received +
    video_call_sent +
    voice_call_received +
    voice_call_sent) partial_total
FROM PIVOT
group by user_id
)

,final as (select *
from total
where partial_total >= total / 2
group by user_id)

, T as (select client_id, sum(total) as final
from final)

select client_id
from T having MAX(final)



```
