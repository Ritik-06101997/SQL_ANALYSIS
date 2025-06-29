# SQL_ANALYSIS
1. Commit 1

``` sql
create table icc_world_cup
(
Team_1 Varchar(20),
Team_2 Varchar(20),
Winner Varchar(20)
);
INSERT INTO icc_world_cup values('India','SL','India');
INSERT INTO icc_world_cup values('SL','Aus','Aus');
INSERT INTO icc_world_cup values('SA','Eng','Eng');
INSERT INTO icc_world_cup values('Eng','NZ','NZ');
INSERT INTO icc_world_cup values('Aus','India','India');

select * from icc_world_cup;


select Team_name,count(1) AS total_matches_played,sum(winflag) AS no_of_matches_won, count(1) - sum(winflag) AS no_of_matches_lost
from(
select Team_1 AS Team_name, Case when winner= Team_1 THEN 1 ELSE 0 END AS winflag
from icc_world_cup
union all
select Team_2 AS Team_name, Case when winner= Team_2 THEN 1 ELSE 0 END AS winflag
from icc_world_cup) A
group by Team_name
order by no_of_matches_won DESC;
```
2. Commit 2
``` sql
create table customer_orders (
order_id integer,
customer_id integer,
order_date date,
order_amount integer
);

delete customer_orders;

select * from customer_orders
insert into customer_orders values(1,100,cast('2022-01-01' as date),2000),(2,200,cast('2022-01-01' as date),2500),(3,300,cast('2022-01-01' as date),2100)
,(4,100,cast('2022-01-02' as date),2000),(5,400,cast('2022-01-02' as date),2200),(6,500,cast('2022-01-02' as date),2700)
,(7,100,cast('2022-01-03' as date),3000),(8,400,cast('2022-01-03' as date),1000),(9,600,cast('2022-01-03' as date),3000)
;

WITH fst_order AS(
select customer_id, min(order_date) AS first_order_date
from customer_orders
group by customer_id)


select cu.order_date,
SUM(CASE WHEN cu.order_date = st.first_order_date THEN 1 ELSE 0 END) AS new_order_customer,
SUM(CASE WHEN cu.order_date != st.first_order_date THEN 1 ELSE 0 END) AS repeat_customers
from customer_orders cu
join fst_order st
on cu.customer_id= st.customer_id
group by cu.order_date;
```
