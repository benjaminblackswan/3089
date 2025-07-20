## 64. Adding a second table

**go to tblEpmloyee, script table as**
<img width="975" height="468" alt="image" src="https://github.com/user-attachments/assets/3b97d30e-61d3-4429-b17a-3dc57f740c38" />
```
CREATE TABLE [dbo].[tblEmployee](
	[EmployeeNumber] [int] NOT NULL,
	[EmployeeFirstName] [varchar](50) NOT NULL,
	[EmployeeMiddleName] [varchar](50) NULL,
	[EmployeeLastName] [varchar](50) NOT NULL,
	[EmployeeGovID] [char](10) NULL,
	[DateOfBirth] [date] NULL,
	[department] [varchar](20) NULL
) ON [PRIMARY]
GO
```

## 65. Designing a connection
```
create table tblTransaction (
Amount smallmoney not null,
DateOfTransaction smalldatetime null,
EmployeeNumber int not null)
```

## 67. Importing data and showing tables graphically

**create new tblTransaction table in SQL Server**

1. open up the tblTransaction150707.exlx file
2. Copy column E and paste into SSMS
3. run the code


**if you encounter this error when trying to create new database diagrams**
<img width="622" height="147" alt="image" src="https://github.com/user-attachments/assets/540f9260-4ab8-40c6-ae8c-e5c994bbd6ad" />

you have to change the Owner to sa in the property of the database, > files

<img width="529" height="134" alt="image" src="https://github.com/user-attachments/assets/dce6d1e8-d7d6-45d7-b6a9-94deb38744ae" />

<img width="764" height="301" alt="image" src="https://github.com/user-attachments/assets/1b6c5d06-bbd5-45bd-9407-46f45b0d6b1a" />

Create a new diagram
and then create relationship

<img width="1389" height="494" alt="image" src="https://github.com/user-attachments/assets/bb8d98f1-5d38-43ee-9e13-a0410835d41e" />

**note if you do not see intellisense showing new table, you have to Refresh local cache, ctrl+shift + R**

## 68. Writing a JOIN query

select EmployeeNumber, sum(amount) as TotalAmount
from tblTransaction
group by EmployeeNumber

---
```
select *
from tblEmployee
join tblTransaction
on tblEmployee.EmployeeNumber = tblTransaction.EmployeeNumber
```

---
```
select tblEmployee.EmployeeNumber, EmployeeFirstName, EmployeeLastName, amount 
from tblEmployee
join tblTransaction
on tblEmployee.EmployeeNumber = tblTransaction.EmployeeNumber
```

---
```
select tblEmployee.EmployeeNumber
, EmployeeFirstName
, EmployeeLastName
, sum(amount) as SumAmount
from tblEmployee
join tblTransaction
on tblEmployee.EmployeeNumber = tblTransaction.EmployeeNumber
group by tblEmployee.EmployeeNumber
, EmployeeFirstName
, EmployeeLastName
order by EmployeeNumber
```

## Quiz 21: Writing a JOIN query

**Where does the word JOIN appear?**
A: after first table name or alias

---
**What is the missing word in this join?**
```
SELECT *
FROM tblTable1 as T JOIN tblTable2 as U ________ T.ID = U.ID
WHERE T.ID < 1000
```

A: On

---

## 69. Different types of JOIN
```
select tblEmployee.EmployeeNumber
, EmployeeFirstName
, EmployeeLastName
, sum(amount) as SumAmount
from tblEmployee
left join tblTransaction
on tblEmployee.EmployeeNumber = tblTransaction.EmployeeNumber
group by tblEmployee.EmployeeNumber
, EmployeeFirstName
, EmployeeLastName
order by EmployeeNumber
```

## Coding Exercise 12: The FROM clause - connecting to two tables

Let's expand our code by joining two tables.

Can you write a SELECT statement which joins together SportTeams and SportGoals. The INNER JOIN should be done using the two columns highlighted in bold below:

* SportTeams - TeamID should join with
* SportGoals - Team.

Please retrieve the following columns:

* SportTeams - TeamID and TeamName, and
* SportGoals - Goals and Points.


```
select TeamID, TeamName, Goals, Points
from SportTeams
inner join SportGoals
on TeamID = Team
```

## Quiz 22: Different types of JOIN

Will these two SELECT statements evaluate the same?

Select * from tblFirst LEFT JOIN tblSecond ON ...

Select * from tblSecond RIGHT JOIN tblFirst ON ...


**Answer: True**

---
What is the JOIN type in the statement below?

Select * from tblFirst JOIN tblSecond ...


**answer: inner join**

---
There is an optional word in the below statement. Please fill it in:

Select * from tblFirst LEFT ____ JOIN tblSecond ON ...

**answer: outer**

## 70. Creating a third table

```
select department from
(
select department
, count(*) as Number
from tblEmployee
group by department
) as newtable
```

---
```
select count(department) as NumberOfDepartment
from
(
select department
, count(*) as Number
from tblEmployee
group by department
) as newtable
```

---
select distinct department
from tblEmployee

---
select distinct department, [EmployeeGovID]
from tblEmployee

---
select distinct Department
, '' as DepartmentHead
from tblEmployee

---
select distinct Department
, '' as DepartmentHead
into tblDepartment
from tblEmployee
select * from [dbo].[tblDepartment]

**note: the SELECT ... INTO ... FROM... statement creates a new table, it can not be used to insert into existing table.**

---
**however the DepartmentHead column is char(1), so we need to drop it and recreate it has varchar(20) with the following code.**
```
drop table tblDepartment
```

```
select distinct Department
, convert(varchar(30), N'') as DepartmentHead
into tblDepartment
from tblEmployee
```

## 71. JOINing three tables
```
select *
from tblDepartment
join tblEmployee
on tblDepartment.Department = tblEmployee.department
join tblTransaction
on tblEmployee.EmployeeNumber = tblTransaction.EmployeeNumber
```

```
select *
from tblDepartment
left join tblEmployee
on tblDepartment.Department = tblEmployee.department
left join tblTransaction
on tblEmployee.EmployeeNumber = tblTransaction.EmployeeNumber
```

---
```
select tblDepartment.Department, sum(amount) as SumOfAmount
from tblDepartment
left join tblEmployee
on tblDepartment.Department = tblEmployee.department
left join tblTransaction
on tblEmployee.EmployeeNumber = tblTransaction.EmployeeNumber
group by tblDepartment.Department
```

---
```
insert into tblDepartment(Department, DepartmentHead)
values ('Accounts', 'James')
```

---
```
select tblDepartment.Department, sum(amount) as SumOfAmount
from tblDepartment
left join tblEmployee
on tblDepartment.Department = tblEmployee.department
left join tblTransaction
on tblEmployee.EmployeeNumber = tblTransaction.EmployeeNumber
group by tblDepartment.Department
```

---
**Edit top 200 of tblDepartment so that**

<img width="288" height="150" alt="image" src="https://github.com/user-attachments/assets/09510329-f773-46c2-a546-3405391b6123" />

```
select tblDepartment.Department, DepartmentHead, sum(amount) as SumOfAmount
from tblDepartment
left join tblEmployee
on tblDepartment.Department = tblEmployee.department
left join tblTransaction
on tblEmployee.EmployeeNumber = tblTransaction.EmployeeNumber
group by tblDepartment.Department, DepartmentHead
order by Department
```

---
```
select DepartmentHead, sum(amount) as SumOfAmount
from tblDepartment
left join tblEmployee
on tblDepartment.Department = tblEmployee.department
left join tblTransaction
on tblEmployee.EmployeeNumber = tblTransaction.EmployeeNumber
group by DepartmentHead
order by DepartmentHead
```

---
```
select d.DepartmentHead, sum(T.Amount) as SumAmount
from tblDepartment as D
left join tblEmployee as E
on D.Department = E.department
left join tblTransaction as T
on E.EmployeeNumber = T.EmployeeNumber
group by DepartmentHead
order by DepartmentHead
```

## Quiz 23: JOINing three tables

Is this a correct SELECT statement for JOINING three tables:
```
SELECT * from tblFirst JOIN tblSecond JOIN tblThird
ON tblFirst.ID = tblSecond.ID ON tblFirst.ID = tblThird.ID
```

**Answer: False**
