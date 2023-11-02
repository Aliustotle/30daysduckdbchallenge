## Day 8 and 9

##  Writting Queries to tackle the following tasks:
1:- Find players with the highest OVA and POT within each club.
2:- Calculate the average OVA for players under 25 years old and over 30 years old in each club.
3:- List the players who are the same age within each club.
4:- Find the player with the highest POT for each nationality
5:- Rank players by their OVA in descending order within each club

##  1:- Find players with the highest OVA and POT within each club.
```SQL
 Select Club,
  Max(Name) as club_player
  ,max("↓OVA") as Club_Highest_OVAOVA
  ,Max(POT) as Club_highest_POT
  from main.fifa21_raw_data_v2 
  group by Club;
```
##   2:- Calculate the average OVA for players under 25 years old and over 30 years old in each club.
```SQL
Select Club, avg(case when Age < 25 then"↓OVA" else null end ) as AvgOVAunder25
,avg(case when Age > 30 then "↓OVA" else null end ) as AvgOVAover30
from
main.fifa21_raw_data_v2 
group by club;
```
##  3:- List the players who are the same age within each club.
```SQL 
select club,age,group_concat(name) as Same_aged_players
from main.fifa21_raw_data_v2 
group by Club, Age 
Having COUNT(name) > 1 ;
```
##  4:- Find the player with the highest POT for each nationality.
```SQL
select Nationality
      ,Max(name) as Player_with_highest_Pot
      ,Max(POT) as Highest_POT
from fifa21_raw_data_v1
Group by Nationality;
```
##  5:- Rank players by their OVA in descending order within each club
```SQL
Select club, id, name,"↓OVA",
     Rank() over(partition by club order by "↓OVA" Desc) as Players_rank
     from main.fifa21_raw_data_v2
     order by club, id,players_rank;
  ```
