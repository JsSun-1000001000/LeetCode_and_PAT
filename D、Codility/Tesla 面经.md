130分钟

第一题：给出N个点的坐标，问是否存在一个正方形，满足这N个点都是在正方形的边界上。  
第二题：给定一个数N，求最小的非负整数A，使得A每一位上的数之和等于N  
第三题：二叉树dfs模版题，二叉树连续的三个节点上的值可以构成一个三位数，求所有的三位数。  
第四题：从矩形左上角到左下角的最短路径。  


**Task1:**

[Codility](https://zhida.zhihu.com/search?content_id=196674694&content_type=Article&match_order=1&q=Codility&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3Njk1OTMyNzAsInEiOiJDb2RpbGl0eSIsInpoaWRhX3NvdXJjZSI6ImVudGl0eSIsImNvbnRlbnRfaWQiOjE5NjY3NDY5NCwiY29udGVudF90eXBlIjoiQXJ0aWNsZSIsIm1hdGNoX29yZGVyIjoxLCJ6ZF90b2tlbiI6bnVsbH0.NKQD9JKouwrzLM1yWOA82-DyYlDeXjAIqyejH2547tQ&zhida_source=entity) is a company that creats programming tasks which are solved by candidates.After submiting their solution to a task,each candidare receives a report containing the number of points their solution scored,which is an integer between 0 and 100.

You are given two tables,tasks and reports,with the following structure:

create table tasks(

id integer not null,

name varchar(40)not null,

unique(id)

);

create table reports(

id integer not null,

task_id integer not null,

candidate varchar(40)not null,

score integer not null,

unique(id)

);

Your task is to write an [SQL](https://zhida.zhihu.com/search?content_id=196674694&content_type=Article&match_order=1&q=SQL&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3Njk1OTMyNzAsInEiOiJTUUwiLCJ6aGlkYV9zb3VyY2UiOiJlbnRpdHkiLCJjb250ZW50X2lkIjoxOTY2NzQ2OTQsImNvbnRlbnRfdHlwZSI6IkFydGljbGUiLCJtYXRjaF9vcmRlciI6MSwiemRfdG9rZW4iOm51bGx9.ufKV-uEnwgOAe0G2ZsoEC9ZnLZrqyIwFg_F1WT_ygLM&zhida_source=entity) query which assigns a difficulty rating to each task having at least one solution.The difficulty of the task depends on the average score of all candidates'solution submitted for this task.It is possible that one candidate have submitted multiple solutions for the same task;in this case ,all of those solutions should be included in the average.

There are three diffculties:"Easy","Medium" and "Hard".

- If the average score for the task is lower than or equal to 20,then its difficulty is "Hard".
- If the average is higher than 20 but lower than or equal to 60,then its difficulty is "Medium".
- If the average is higher than 60,its difficulty is "Easy".

For example,if the average score of the task is 50,then its difficulty is "Medium" beacuse the average score is greater than 20 but less then 60.

Your query should return a table containing three columns:task_id(ID of task),task_name(name of task) and difficulty-the difficulty of the task,which is one of three possible strings:"Easy","Medium" or "Hard'.Rows should be ordered by increasing task_id .If no solutions exist for some task,that task should not appear in your table.

Examples:

1.Given:

tasks:

||name|
|---|---|
|3  <br>6  <br>7  <br>9|Cake  <br>GameOfNuts  <br>CircleIntersectionArea  <br>JessicaAndBrian|

reports:

|id|task_id|candidate|score|
|---|---|---|---|
|2  <br>3  <br>5  <br>7  <br>11  <br>13|6  <br>3  <br>3  <br>9  <br>6  <br>6|Paul Sat  <br>Karen M.  <br>Oscar Glad  <br>Karen M.  <br>Paul Sat  <br>Paul Sat|0  <br>30  <br>10  <br>60  <br>81  <br>100|

your query should return:

|task_id|task_name|difficulty|
|---|---|---|
|3  <br>6  <br>9|Cake  <br>GameOfNuts  <br>JessicaAndBrian|Hard  <br>Easy  <br>Medium|

**-- 解题**

select tasks.id,tasks.name,case

when reports.avg_score <=20 then 'Hard'

when reports.avg_score >60 then 'Easy'

else 'Medium' end as '难易程度' from (

select (sum(score)/count(1))as avg_score,task_id from reports group by task_id) reports

left join tasks on reports.task_id=tasks.id;

---

**Task2:**

Amanda wants to buy a car.Her budget is limited,and she has decided that she would preder to spend it on a car that was produced recently.Her other option is to buy an older,used car,but she would not want to spend much money on such a vehicle.Help her choose all possible options,knowing that she can spend at most 50,000 on a new car produced in 2018 or later,or at most 20,000 on a used car produced in 2010 or later.

  

you are given a non-empty table,cars,whose structure is described by the following query:

create table cars(

id integer not null primary key,

condition varchar(10) not null,

yesr integer not null,

price integer not null

);

Each row of the table cars contains information about a car:unique id(id),condition(condition),year of production(year) and price(price).Condition contains either one of two possible words:New or Used.

Write an SQl query that returns a table consisting of one column(id),containing the ids of all the cars that fulfil Amanda's ceiteria.Rows should be ordered by increasing id.

Examples:

1.Given the following data:

cars:

|id|condition|year|price|
|---|---|---|---|
|12  <br>10  <br>9  <br>1  <br>7  <br>5  <br>6|New  <br>Used  <br>Used  <br>New  <br>Used  <br>Used  <br>New|2018  <br>2007  <br>2015  <br>2015  <br>2015  <br>2012  <br>2019|30000  <br>13000  <br>10000  <br>21000  <br>23000  <br>12000  <br>150000|

you query should return the following table:

|id|
|---|
|5  <br>9  <br>12|

2.Given the following data:

cars:

|id|condition|year|price|
|---|---|---|---|
|9  <br>4  <br>6  <br>1  <br>8|New  <br>New  <br>New  <br>Used  <br>New|2018  <br>2015  <br>2019  <br>2010  <br>2008|50000  <br>10000  <br>120000  <br>20000  <br>22000|

your query should return the following table:

|id|
|---|
|1  <br>9|

='2010' and price <=20000 ORDER BY id ;","marks":[]}]}],"state":{}}]'>

  

**--建表：**

create table cars(

id INTEGER not null PRIMARY key,

condit varchar(10) not null,

yea INTEGER not null,

price INTEGER not null);

  

SELECT * from cars;

-- <=50000 >=2018 new

-- <=20000 >=2010. new or used

SELECT * from cars where price <=50000 ;

**-- 解题**

SELECT * from cars where yea >='2018' and condit ='New' and price <=50000

union

SELECT * from cars where yea >='2010' and price <=20000 ORDER BY id ;

---

**Task3:**

You are part of a team creating an [IAM](https://zhida.zhihu.com/search?content_id=196674694&content_type=Article&match_order=1&q=IAM&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3Njk1OTMyNzAsInEiOiJJQU0iLCJ6aGlkYV9zb3VyY2UiOiJlbnRpdHkiLCJjb250ZW50X2lkIjoxOTY2NzQ2OTQsImNvbnRlbnRfdHlwZSI6IkFydGljbGUiLCJtYXRjaF9vcmRlciI6MSwiemRfdG9rZW4iOm51bGx9.gG96ppJTpDqBFj4sOaOIPxdFumDTJgJZGEuVtRNTWS4&zhida_source=entity)(Identity & Access Managenment) solution.You have defined a table UserRole with the following structure:

create table UserRole(

Id bigint not null auto_increment,

Name varchar(100) not null,

Description varchar(200) null,

IsEnabled bit not null, -- 1 is a role is enabled,0 otherwise

Created date not null, -- when a role was created

CreatedBy varchar(200) not null ,-- who created a role

Updated date null,-- when a role was updated(if at all)

UpdatedBy varchar(200) null,-- who updated a role (if at all)

constraint pk_userrole primary key (id asc)

);

Your task is to write a SQL query (a report)that ,for each user that has ever created a role,will return four values:

- User name in the UserNmae column;
- Number of created roles in the NoOfCreatedRoles column;
- Number of created roles that are enabled in the NoOfCreatedAndEnabledRoles column;
- Number of updated roles in the NoOfUpdatedRoles column.

Rows in the report should be sorted by user name in descending order.Additionally,user names should contain no leading or trailing white spaces and should be uppercase.

Your query should return no NULL values for numerical columns.Instead,NULL should be replaces with -1.For example,it is possible that there are no roles updated by a given user,or that there are no roles created by a given user that are enabled.

You should also take into account that values in CreatedBy and UpdatedBy columns are not consistent:

- They can contain additional white spaces at the beginning or the end;
- They can be written using a mixture of small and capital letters,e.g.JOHN SMITH,john smith.

Here is an example.Let's assume that we have the following data in the table:

|Id|Name|Description|IsEnabled|Created|CreatedBy|Updated|UpdatedBy|
|---|---|---|---|---|---|---|---|
|1|Role_1|NULL|1|2020-04-15 00:00:00|Admin|NULL|NULL|
|2|Role_2|Description|1|2020-04-16 00:00:00|ADMIN|2020-04-17 00:00:00|John Smith|
|3|Role_3|Description|0|2020-04-16 00:00:00|JohnSMITH|2020-04-17 00:00:00|BenSMITH|
|4|Role_4|Description|1|2020-04-19 00:00:00|bEnSmiTh|2020-04-21 00:00:00|BENSMITH|

For this data the report should look as follows:

|UserName|NoOfCreatedRoles|NoOfCreatedAndEnabledRoles|NoOfUpdatedRoles|
|---|---|---|---|
|BENSMITH|1|1|2|
|JOHNSMITH|1|-1|1|
|ADMIN|2|2|-1|

Hints:

- You can assume that there is at least one role created by each user.
- Your query will be executed against [MySQL 8.0](https://zhida.zhihu.com/search?content_id=196674694&content_type=Article&match_order=1&q=MySQL+8.0&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3Njk1OTMyNzAsInEiOiJNeVNRTCA4LjAiLCJ6aGlkYV9zb3VyY2UiOiJlbnRpdHkiLCJjb250ZW50X2lkIjoxOTY2NzQ2OTQsImNvbnRlbnRfdHlwZSI6IkFydGljbGUiLCJtYXRjaF9vcmRlciI6MSwiemRfdG9rZW4iOm51bGx9._YRWCfOHxKlv3Em4E8WDf0sa92-fPmGsVY0MFKT9Wvs&zhida_source=entity) database.
- Pay attention to Query_Can_Be_Executed_Without_Any_Error test,which only validates if your query can be exected.If this test fails,it probably means that your query is not syntactically correct.

**-- 建表：**

create table userrole (

id BIGINT not null auto_increment,

name varchar(100) not null,

description varchar(200) null,

isenabled bit not null, -- 1 is enabled,0 otherwise

created date not null,

createdby varchar(200) not null,

updated date null,

updatedby varchar(200) null,

constraint pk_userrole PRIMARY key (id asc));

  

SELECT * from userrole;

-- username NoOfCreatedRoles NoOfCreatedAndEnabledRoles NoOfUpdatedRoles

  

**-- 解题**

SELECT t.a1,t.a2,t.a3,case when t.b2 is null then '-1' else t.b2 end b2 from (

SELECT a.a1,a.a2,a.a3,b.b2

from

(SELECT UPPER(createdby) a1,COUNT(createdby) a2,count(isenabled=1) a3 from userrole GROUP BY createdby ) a LEFT JOIN

(SELECT UPPER(updatedby) b1,count(updatedby) b2 from userrole GROUP BY updatedby ORDER BY createdby) b on a.a1=b.b1

union

select b.b1,a.a2,a.a3,b.b2 from

(SELECT UPPER(createdby) a1,COUNT(createdby) a2,count(isenabled=1) a3 from userrole GROUP BY createdby ) a right JOIN

(SELECT UPPER(updatedby) b1,count(updatedby) b2 from userrole GROUP BY updatedby ORDER BY createdby) b on a.a1=b.b1 )t

where t.a1 is not null;