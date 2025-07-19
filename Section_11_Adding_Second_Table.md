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
