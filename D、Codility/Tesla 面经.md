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

---

面试之前有笔试，1 easy + 1 medium + 1 sql。

## 一面

1. self introduction
    
2. more detail about ur project
    
3. what API you write in the project? what it does?
    
4. what difficulty you meet in your work?
    
5. 业务分层，MVC架构？
    
6. 说一下Spring的两个概念；有没有用过AOP模式？
    
7. 项目是前后端分离吗？为什么用Session存储用户信息？Session跨域问题？
    
8. 你刚刚提到了ThreadLocal，说一下Java里面的并发机制
    
9. 同步和阻塞的关系，SpringBoot里面的同步非阻塞
    
10. 接触过函数式编程吗？Golang和Python。开发过项目吗？
    
11. 会数据分析吗，接触过机器学习吗？数分会，ML不会
    
12. 了解前端技术vue和react吗？只会三件套
    
13. 了解dockerfile吗？了解k8s吗？简单说了一下
    
14. 知道其他中间件吗，比如rabbitMQ？会kafka，简单说了一下
    
15. 算法题：字符串反转，特殊字符位置不变
    

## 二面

1. self introduction
    
2. jvm内存划分
    
3. jvm初始化对象的过程
    
4. 堆栈的区别
    
5. 数组拷贝的内存分配过程
    
6. 数组和链表的区别，使用场景
    
7. 算法题：矩阵旋转
    
8. 算法题：最长回文子串
    

## 三面

1. 介绍一下项目
    
2. 有什么技术难点？这个方案是你自己提出的吗？
    
3. 为什么用MySQL，为什么用索引？
    
4. docker用的什么？k8s？
    
5. 有转正意向吗？
    
6. let's transfer to English, why do u wanna join Tesla
    
7. introduce something about microservice architect
    
8. what the difference between Kafka and rabbitMQ?
    

  
  
作者：ShawnLee0223  
链接：[https://www.nowcoder.com/discuss/353159669868863488](https://www.nowcoder.com/discuss/353159669868863488)  
来源：牛客网

---
# Task1

You are given two tables, `department` and `employee`, with the following structure:

[复制代码](#)

|   |   |
|---|---|
|1<br><br>2<br><br>3<br><br>4<br><br>5<br><br>6<br><br>7<br><br>8<br><br>9<br><br>10<br><br>11<br><br>12<br><br>13<br><br>14|`create` `table` `department (`<br><br>    `dept_id` `integer` `not` `null``,`<br><br>    `dept_name` `varchar``(30)` `not` `null``,`<br><br>    `dept_location` `varchar``(30)` `not` `null``,`<br><br>    `unique``(dept_id)`<br><br>`);`<br><br>`create` `table` `enployee (`<br><br>    `emp_id` `integer` `not` `null``,`<br><br>    `emp_name` `varchar``(50)` `not` `null``,`<br><br>    `dept_id` `integer` `not` `null``,`<br><br>    `salary` `integer` `not` `null``,`<br><br>    `unique``(emp_id)`<br><br>`);`|

Each record in the table `department` represents a department which might hire some employees. Each record in the table `employee` represents an employee who works for one of the departments from the table `department`. The salary of each employee is known. (However, the locations of the departments are not relevant here.)

Write an SQL query that returns a table comprising all the departments (`dept_id`) in the table `department` that hire at least one employee, the number of people they employ and the sum of salaries in each department. The table should be ordered by `dept_id` (in increasing order).

# Task2

Codility is a company that creates programming tasks which are solved by candidates. After submitting their solution to a task, each candidate receives a report containing the number of points their solution scored, which is an integer between 0 and 100.

You are given two tables, `tasks` and `reports`, with the following structure:

[复制代码](#)

|   |   |
|---|---|
|1<br><br>2<br><br>3<br><br>4<br><br>5<br><br>6<br><br>7<br><br>8<br><br>9<br><br>10<br><br>11<br><br>12<br><br>13|`0create` `table` `tasks (`<br><br>    `id` `integer` `not` `null``,`<br><br>    `name` `varchar``(40)` `not` `null``,`<br><br>    `unique``(id)`<br><br>`);`<br><br>`create` `table` `reports(`<br><br>    `id` `integer` `not` `null``,`<br><br>    `task_id` `integer` `not` `null``,`<br><br>    `candidate` `varchar``(40)` `not` `null``,`<br><br>    `score` `integer` `not` `null``,`<br><br>    `unique``(id)`<br><br>`);`|

Your task is to write an SQL query which assigns a difficulty rating to depends on the average score of all candidates' solutions submitted each task **having at least one solution**. The difficulty of the task depends on the average score of all candidates' solutions submitted for this task. It is possible that one candidate have submitted multiple solutions for the same task; in this case, all of those solutions should be included in the average.

There are three difficulties: "Easy' , "Medium" and "Hard".

- If the average score for the task is lower than or equal to 20, then its difficulty is "Hard".
- If the average is higher than 20 but lower than or equal to 60, then its difficulty is "Medium".
- If the average is higher than 60, its difficulty is "Easy".

For example, if the average score of the task is 50, then its difficulty is "Medium" because the average score is greater than 20 but less then 60.

Your query should return a table containing three columns: `task_id`(ID of task), `task_name` (name of task) and `difficulty` - the difficulty of the task, which is one of three possible strings: Easy ", "Medium" or "Hard". Rows should be ordered by increasing `task_id`. If no solutions exist for some task, that task should not appear in your table.

# Task3

Consider a non-empty string S= `S[0]S[1]... s[Q-1]` consisting of Q characters. The _period_ of this string is the smallest positive integer P such that:

- P ≤ Q / 2 and
- S[K] = S[K+P] for every K, where 0 ≤ K < Q-P

For example, 8 is the period of "`codilitycodilityco`" and 7 is the period of "`abracadabracadabra`".

A positive integer M is the _binary period_ of a positive integer N if M is the period of the binary representation of N.

For example, 4 is the binary period of 955, because the binary representation of 955 is "1110111011" and its period is 4.

You are given an implementation of a function:

`def solution(N):`

This function, when given a positive integer N, returns the binary period of N. The function returns -1 if N does not have a binary period.

For example, given N = 955 the function returns 4, as explained in the example above.

The attached code is still **incorrect** for some inputs. Despite the error(s), the code may produce a correct answer for the example test cases. The goal of the exercise is to find and fix the bug(s) in the implementation. You can modify at most **two** lines.

Assume that:

- N is an integer within the range [1..1,000,000,000].

In your solution, focus on **correctness**. The performance of your solution will not be the focus of the assessment.

[复制代码](#)

|   |   |
|---|---|
|1<br><br>2<br><br>3<br><br>4<br><br>5<br><br>6<br><br>7<br><br>8<br><br>9<br><br>10<br><br>11<br><br>12<br><br>13<br><br>14<br><br>15<br><br>16|`def solution(n):`<br><br>    `d = [``0``] *` `30`<br><br>    `l =` `0`<br><br>    `while` `(n >` `0``):`<br><br>        `d[l] = n %` `2`<br><br>        `n` `//= 2`<br><br>        `l +=` `1`<br><br>    `for` `p in range(``1``,` `1` `+ l):`<br><br>        `ok = True`<br><br>        `for` `i in range(l - p):`<br><br>            `if` `d[i] != d[i + p]:`<br><br>                `ok = False`<br><br>                `break`<br><br>        `if` `ok:`<br><br>            `return` `p`<br><br>    `return` `-``1`|

[2022暑期实习-特斯拉-笔试_牛客网](https://www.nowcoder.com/discuss/601167596045512704)

[Tesla特斯拉一二三面面经（已oc）_牛客网](https://www.nowcoder.com/discuss/353159669868863488)

[特斯拉一面算法原题-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/2393912)
