## 56. Creation of tblEmployee table
create table tblEmployee
(
EmployeeNumber int NOT NULL,
EmployeeFirstName varchar(50) not null,
EmployeeMiddleName varchar(50) null,
EmployeeLastName varchar(50) not null,
EmployeeGovID char(10) null,
DateOfBirth datetime not null
)

**note: to recreate the script, right click > script table as > new query**

<img width="851" height="268" alt="image" src="https://github.com/user-attachments/assets/99207c2f-5c7e-4e81-9de5-97734ab911a3" />

---
## 57. Adding additional columns

alter table [dbo].[tblEmployee]
add Department varchar(10);

---
insert into [dbo].[tblEmployee]
values (132, 'Dylan', 'A', 'Word', 'HN513777D', '19920914', 'Customer Relations')

**Note: this will cause an error because Department column dt is only 10 characters long**

---
alter table [dbo].[tblEmployee]
drop column Department

alter table [dbo].[tblEmployee]
add department varchar(50)

---
insert into [dbo].[tblEmployee]
values (132, 'Dylan', 'A', 'Word', 'HN513777D', '19920914', 'Customer Relations')

**now it is successfully added into the table**

---
alter table [dbo].[tblEmployee]
alter column department varchar(20)

---
**explicitly state the column names**
insert into [dbo].[tblEmployee]
([EmployeeFirstName], [EmployeeMiddleName], [EmployeeLastName], [EmployeeGovID], [DateOfBirth], [department], [EmployeeNumber])
values ('Jossef', 'H', 'Wright', 'TX593671R', '19711224', 'Litigation', 131)

---
## Coding Exercise 5: Adding additional columns

Let's practice adding an additional column to an existing table. There is a table called SportTeams with the following columns: TeamID, TeamName, Attack and Defense.

Please write an SQL statement which adds an extra column called Ranking. It should have the data type of int.

Please end with the semicolon. Then afterwards, the SELECT statement will run this table.

It should then have 5 columns. If you have any problems, then please give it a go. You will get hints after two incorrect attempts.

---
-- Write your code after this line.
alter table SportTeams
add Ranking int;
-- End with a semicolon
SELECT * FROM SportTeams;

---
## Coding Exercise 6: Entering data using T-SQL (multiple columns)

There is a table called SportTeams with the following columns: TeamID, TeamName, Attack and Defense.

I want you to write T-SQL code in rows 1 and 2 to insert a row which has

    TeamID = 23,

    TeamName = Wolf FC

    Attack = 2, and

    Defense = 3.

Please end it with a semicolon. (While this is not normally needed in T-SQL, it is needed for this online version.)

The last line then retrieves all of the data. It should include this new row.

---
INSERT into SportTeams
Values (23, 'Wolf FC', 2, 3);
SELECT * FROM SportTeams

## 58. SELECTing only part of a table - strings

**inserting multiple rows in one go**

insert into [dbo].[tblEmployee]
values (1, 'Dylan', 'A', 'Word', 'HN513777D', '19920914', 'Customer Relations')
	 , (2, 'Jossef', 'H', 'Wright', 'TX593671R', '19711224', 'Litigation')

**copy and paste data from 70-461datau excel, there are 1003 rows, plus the four already in the tblEmployees, this should give you 1007 rows**

**select all Employees with surname Word**
select * from [dbo].[tblEmployee]
where EmployeeLastName = 'Word'
**returns 3 rows**

---
select * from [dbo].[tblEmployee]
where EmployeeLastName <> 'Word'
**returns 1004 rows**

---
select * from [dbo].[tblEmployee]
where EmployeeLastName != 'Word'
**same as above**

---
select * from [dbo].[tblEmployee]
where EmployeeLastName like 'W%'
**returns 16**

---
select * from [dbo].[tblEmployee]
where EmployeeLastName like '%W'
**returns 16**

---
select * from [dbo].[tblEmployee]
where EmployeeLastName like '%W%'
**returns 73**

---
select * from [dbo].[tblEmployee]
where EmployeeLastName like '_W%'

---
**begin with r, s or t, two ways**
select * from [dbo].[tblEmployee]
where EmployeeLastName like '[rst]%'

select * from [dbo].[tblEmployee]
where EmployeeLastName like '[r-t]%'

---
**not with r, s or t, two ways**
select * from [dbo].[tblEmployee]
where EmployeeLastName like '[^rst]%'

select * from [dbo].[tblEmployee]
where EmployeeLastName like '[^r-t]%'

---
**starting with a %**
select * from [dbo].[tblEmployee]
where EmployeeLastName like '[%]%'

## Coding Exercise 7: SELECTing only part of a table - strings
In this coding exercise, we'll have a look at using a WHERE clause with strings.

There is a table called SportTeams with the following columns: TeamID, TeamName, Attack and Defense.

Please write a SELECT statement which retrieves all rows where the TeamName includes "town". It could be at the beginning, middle, or end of the TeamName.

If you have any problems, you will get hints after two incorrect attempts.

SELECT *
FROM SportTeams
where TeamName like '%town%'

---
## 59. SELECTing only part of a table - numbers

select * from [dbo].[tblEmployee]
where employeeNumber > 200
**925 returned**

---
select * from [dbo].[tblEmployee]
where not employeeNumber > 200
**82 returned**

**additional methods of negating**
select * from [dbo].[tblEmployee]
where not (employeeNumber > 200)

select * from [dbo].[tblEmployee]
where not employeeNumber !> 200

---
**between**
select * from [dbo].[tblEmployee]
where employeeNumber >=200 and  employeeNumber <=209

**returns 10**

select * from [dbo].[tblEmployee]
where not( employeeNumber >=200 and  employeeNumber <=209 )

**returns 997**

---
select * from [dbo].[tblEmployee]
where employeeNumber < 200 or  employeeNumber > 209

**returns 997**

---
select * from [dbo].[tblEmployee]
where employeeNumber between 200 and 209

---
select * from [dbo].[tblEmployee]
where employeeNumber not between 200 and 209

**returns 997**

---

