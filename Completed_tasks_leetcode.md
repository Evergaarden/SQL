

<b><h2>Решенные задачи с <a href = "https://leetcode.com">leetcode.com</a></h2></b>


<br><b>Ex 181. Employees Earning More Than Their Managers:</b>

<br>The Employee table holds all employees including their managers. Every employee has an Id, and there is also a column for the manager Id.

<br>+----+-------+--------+-----------+
<br>| Id | Name  | Salary | ManagerId |
<br>+----+-------+--------+-----------+
<br>| 1  | Joe   | 70000  | 3         |
<br>| 2  | Henry | 80000  | 4         |
<br>| 3  | Sam   | 60000  | NULL      |
<br>| 4  | Max   | 90000  | NULL      |
<br>+----+-------+--------+-----------+

<br>Given the Employee table, write a SQL query that finds out employees who earn more than their managers. For the above table, Joe is <br>the only employee who earns more than his manager.

<br>+----------+
<br>| Employee |
<br>+----------+
<br>| Joe      |
<br>+----------+


        SELECT e.Name as Employee 
        FROM employee AS e INNER JOIN employee AS m on e.ManagerId = m.Id 
        WHERE e.salary > m.salary

=============================

<br><b>Ex 196. Delete Duplicate Emails</b>

<br>Write a SQL query to delete all duplicate email entries in a table named Person, keeping only unique emails based on its smallest Id.

<br>+----+------------------+
<br>| Id | Email            |
<br>+----+------------------+
<br>| 1  | john@example.com |
<br>| 2  | bob@example.com  |
<br>| 3  | john@example.com |
<br>+----+------------------+
<br>Id is the primary key column for this table.

<br>For example, after running your query, the above Person table should have the following rows:

<br>+----+------------------+
<br>| Id | Email            |
<br>+----+------------------+
<br>| 1  | john@example.com |
<br>| 2  | bob@example.com  |
<br>+----+------------------+


        DELETE FROM Person 
        WHERE Id NOT IN (SELECT * FROM(
        SELECT MIN(Id) 
        FROM Person 
        GROUP BY Email) AS t1)

=============================

<br><b>Ex 175. Combine Two Tables</b>

<br>Table: Person
<br>+-------------+---------+
<br>| Column Name | Type    |
<br>+-------------+---------+
<br>| PersonId    | int     |
<br>| FirstName   | varchar |
<br>| LastName    | varchar |
<br>+-------------+---------+
<br>PersonId is the primary key column for this table.

<br>Table: Address
<br>+-------------+---------+
<br>| Column Name | Type    |
<br>+-------------+---------+
<br>| AddressId   | int     |
<br>| PersonId    | int     |
<br>| City        | varchar |
<br>| State       | varchar |
<br>+-------------+---------+
<br>AddressId is the primary key column for this table.
 

<br>Write a SQL query for a report that provides the following information for each person in the Person table, <br>regardless if there is an address for each of those people:
<br>FirstName, LastName, City, State


        SELECT t1.FirstName, t1.LastName, t2.City, t2.State 
        FROM Person AS t1 LEFT JOIN Address AS t2 ON t1.PersonId = t2.PersonId




















