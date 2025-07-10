use [3089-Burton]
Go

#### 25. Creating an Employee table

Create table tblEpmloyee
(EmployeeNumber int, EmployeeName int)

#### 27. Creating temporary variables
declare @myvar as int = 2
select @myvar

**note: must run them in one batch**

declare @myvar as int = 2

set @myvar = 3

select @myvar

---

declare @myvar as int = 2

set @myvar = @myvar + 1

---

declare @myvar as int = 2

set @myvar = myvar * 1

select @myvar as myVariable 

select @myvar

---
declare @myvar as int = 2

set @myvar = 2.5

select @myvar as myVariable 

** note that 2.3 is truncated to whole number **

--
declare @myvar as int = 2

set @myvar = -2.01

select @myvar as myVariable 

---

declare @myvar as tinyint = 2

set @myvar = @myvar + 1

select @myvar as myVariable 

---

declare @myvar as tinyint = 2

set @myvar = @myvar - 2

select @myvar as myVariable 

---

declare @myvar as tinyint = 2

set @myvar = @myvar - 3

select @myvar as myVariable 

tinyint can not go negative
---
**smallint, int and big int are signed, meaning that they can go to negative. While tiny int is unsigned, meaning it can not go to negative**
declare @myvar as smallint = 2

set @myvar = @myvar - 3

select @myvar as myVariable 

**smallint to go negative**

---


