#### Here you can find the homework for week 1

#### 1. How many taxi trips were there on January 15?

```sql
Select count(*) from yellow_taxi_data t 
    where  t.tpep_pickup_datetime >= '2021-01-15'::date 
        and t.tpep_pickup_datetime < '2021-01-16'::date 
```
#### 2. On which day it was the largest tip in January?

```sql
Select t.tip_amount, t.tpep_pickup_datetime from yellow_taxi_data t 
    where t.tpep_pickup_datetime >= '2021-01-01'::date 
    and t.tpep_pickup_datetime < '2021-02-01'::date 
    order by  t.tip_amount desc limit 1
```

#### 3. What was the most popular destination for passengers picked up in central park on January 14? Enter the zone name (not id). If the zone name is unknown (missing), write "Unknown"

```sql
Select t.tip_amount, t.tpep_pickup_datetime from yellow_taxi_data t 
    where t.tpep_pickup_datetime >= '2021-01-01'::date 
        and t.tpep_pickup_datetime < '2021-02-01'::date 
    order by t.tip_amount desc limit 1
```

#### 4. What was the most popular destination for passengers picked up in central park on January 14?

```sql
update zones
set "Zone" = 'Unknown'
where zones."Zone" is NULL; 
select concat(z1."Zone", '/' , z2."Zone"), avg(t.total_amount) as "average" 
from yellow_taxi_data t 
	inner join zones z1 on t."PULocationID" = z1."LocationID" 
	inner join zones z2 on t."DOLocationID" = z2."LocationID" 
group by (z1."Zone", z2."Zone") order by avg(t.total_amount) desc limit 1;
```