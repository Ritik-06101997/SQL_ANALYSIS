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
