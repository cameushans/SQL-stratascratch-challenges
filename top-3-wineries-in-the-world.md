# Top 3 Wineries In The World

Find the top 3 wineries in each country based on the average points earned. In case there is a tie, order the wineries by winery name in ascending order. Output the country along with the best, second best, and third best wineries. If there is no second winery (NULL value) output 'No second winery' and if there is no third winery output 'No third winery'. For outputting wineries format them like this: "winery (avg\_points)"

```sql
// Some code

WITH cta AS (
    SELECT 
        country,
        winery,
        ROUND(AVG(points), 0) AS avg,
        ROW_NUMBER() OVER(PARTITION BY country ORDER BY ROUND(AVG(points), 0) DESC, winery) AS rnk
    FROM winemag_p1
    GROUP BY country, winery
)



select f.country,
CONCAT(f.winery,' (', f.avg, ')') as top_winery,
ifnull(CONCAT(s.winery,' (', s.avg, ')'), 'No second winery') as second_winery, 
ifnull(CONCAT(t.winery,' (', t.avg, ')'), 'No third winery') as third_winery
from cta as f 
left outer join cta as s 
on f.country = s.country and s.rnk = 2
left outer join cta as t
on s.country = t.country and t.rnk = 3
WHERE f.rnk = 1
ORDER BY f.country;



```
