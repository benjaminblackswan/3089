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
# 57. Adding additional columns

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
(
[EmployeeFirstName], [EmployeeMiddleName], [EmployeeLastName]
, [EmployeeGovID], [DateOfBirth], [department], [EmployeeNumber]
)

values ('Jossef', 'H', 'Wright', 'TX593671R', '19711224', 'Litigation', 131)

---

