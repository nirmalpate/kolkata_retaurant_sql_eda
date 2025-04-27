# kolkata_retaurant_sql_eda

with cte as(
SELECT * , regexp_replace(bill,'[^0-9]','') as s
FROM pop.data), final as(
select *, case when length(s) = 5 then left(s,4) else left(s,3) end as total_bill
from cte), my_final as(
select  name,ratings, total_bill,location1, location2, cuisine1, cuisine2, cuisine3
from final), Unused as(
select *
from my_final
where ratings < 1 and total_bill > 1000)
select *
from Unused
order by total_bill desc;


with cte as(
SELECT * , regexp_replace(bill,'[^0-9]','') as s
FROM pop.data), final as(
select *, case when length(s) = 5 then left(s,4) else left(s,3) end as total_bill
from cte), my_final as(
select  name,ratings, total_bill,location1, location2, cuisine1, cuisine2, cuisine3
from final), Top as(
select *
from my_final
where ratings >3  and total_bill > 1000)
select *
from Top
order by total_bill desc;

 
 with cte as(
SELECT * , regexp_replace(bill,'[^0-9]','') as s
FROM pop.data), final as(
select *, case when length(s) = 5 then left(s,4) else left(s,3) end as total_bill
from cte), my_final as(
select  name,ratings, total_bill,location1, location2, cuisine1, cuisine2 
from final)
select  location1, round(avg(total_bill),2) as avg_bill
from my_final
group by location1
order by round(avg(total_bill),2) desc;

with cte as(
SELECT * , regexp_replace(bill,'[^0-9]','') as s
FROM pop.data), final as(
select *, case when length(s) = 5 then left(s,4) else left(s,3) end as total_bill
from cte), my_final as(
select  name,ratings, total_bill,location1, location2, cuisine1, cuisine2 
from final)
select  location2, round(avg(total_bill),2) as avg_bill
from my_final
group by location2
order by round(avg(total_bill),2) desc;


with cte as(
SELECT * , regexp_replace(bill,'[^0-9]','') as s
FROM pop.data), final as(
select *, case when length(s) = 5 then left(s,4) else left(s,3) end as total_bill
from cte), my_final as(
select  name,ratings, total_bill,location1, location2, cuisine1, cuisine2 
from final)
select  cuisine1, round(avg(total_bill),2) as avg_bill
from my_final
group by cuisine1
order by avg_bill desc;



with cte as(
SELECT * , regexp_replace(bill,'[^0-9]','') as s
FROM pop.data), final as(
select *, case when length(s) = 5 then left(s,4) else left(s,3) end as total_bill
from cte), my_final as(
select  name,ratings, total_bill,location1, location2, cuisine1, cuisine2 
from final
where ratings > 3)
select  cuisine1, round(avg(ratings),2) as avg_ratings
from my_final
group by cuisine1;
