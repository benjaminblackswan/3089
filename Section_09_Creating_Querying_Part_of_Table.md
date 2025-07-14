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
