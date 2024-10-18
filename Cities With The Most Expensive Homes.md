# Cities With The Most Expensive Homes


with TOTAL_AVG AS (select AVG(mkt_price) as average from zillow_transactions)
 
select distinct city from  zillow_transactions
group by city
having avg(mkt_price) > (select average from TOTAL_AVG)
