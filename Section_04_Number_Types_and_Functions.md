use [3089-Burton]
Go

# 25. Creating an Employee table

Create table tblEpmloyee
(EmployeeNumber int, EmployeeName int)

# 27. Creating temporary variables
-- method 1

DECLARE @myvar AS INT = 2
SELECT @myvar

-- method 2

DECLARE @myVar AS INT
SET @myVar = 3
SELECT @myVar

**note: must run them in one batch**

DECLARE @myvar AS INT = 2
SELECT @myvar AS myVariable

---

DECLARE @myvar AS INT = 2
SET @myvar = 3
SELECT @myvar AS myVariable

---

DECLARE @myvar AS INT = 2
SET @myvar = @myvar + 1
SELECT @myvar AS myVariable

---

DECLARE @myvar AS INT = 2
SET @myvar = @myvar*4 + 1
SELECT @myvar AS myVariable

---

DECLARE @myvar AS INT = 2
SET @myvar = 2.5
SELECT @myvar AS myVariable

--

DECLARE @myvar AS INT = 2
SET @myvar = - 2.5
SELECT @myvar AS myVariable

**INT datatype truncates the decimals, that is it always round towards zero**


# 28. Interger numbers
DECLARE @myvar AS TINYINT = 2

---
DECLARE @myvar AS TINYINT = 2
SET @myvar = @myvar -2
SELECT @myvar AS myVariable

---
DECLARE @myvar AS TINYINT = 2
SET @myvar = @myvar -3
SELECT @myvar AS myVariable
**tinyint can not go below negative**

---
DECLARE @myvar AS TINYINT = 2
SET @myvar = @myvar - 0.5
SELECT @myvar AS myVariable

---
DECLARE @myvar AS SMALLINT = 2
SET @myvar = @myvar - 3
SELECT @myvar AS myVariable

---
DECLARE @myvar AS SMALLINT = 2000
SET @myvar = @myvar * 10
SELECT @myvar AS myVariable

---

# 29. Practice Activity Number 3

Now it´s your turn.
* Can you create a variable of the data type that allows values up to 32,767, but no further.
* Then assign the variable the value of 20,000
* And then print out the contents of that variable.

---
declare @myvar as smallint
set @myvar = 20000
select @myvar

---
Afterwards:
* Create version 2: Change your code so that it tries to assign the value of 200,000. If it doesn't run properly, then you got it right.
* Create version 3: Correct the problem by changing your variable to a data type that allows the value of 200,000, and see if the code now works.
* Create version 4: Then change it back to 20,000, but change the variable to a data type that doesn't allow numbers that high. Then see if you get that error message again.

---
declare @myvar as int
set @myvar = 200000
select @myvar

declare @myvar as tinyint
set @myvar = 200000
select @myvar

---
And if you have having problems remembering which data type is which, try remembers that acronym which lists this in the right order.
I've included my answers in the Resources. Bear in mind that you may have a variant of these answers, and still be correct.

# 31. Non-integer numbers
** Valid**
declare @myvar as decimal(7,2)
set @myvar = 12345.67
select @myvar

---
** NOT valid**
declare @myvar as decimal(7,2)
set @myvar = 123456.7
select @myvar

**numeric and decimal are basically the same**

---
declare @myvar as numeric(7)
set @myvar = 12345.67
select @myvar

**note: numeric datatype round to the nearest**

---
declare @myvar as numeric(18,8)
set @myvar = 1000000000.12345678
select @myvar as myVariable

---
declare @myvar as smallmoney = 123456.78917
select @myvar as myVariable

**avoid float**

---

# 32. Mathematical functions

declare @myvar as numeric(7,2) = 3
select power(@myvar, 2)

---
declare @myvar as numeric(7,2) = 3
select square(@myvar)

---
declare @myvar as numeric(7,2) = 3
select power(@myvar,0.5)
select sqrt(@myvar)

---
declare @myvar as numeric(7,2) = 3.7
select floor(@myvar)
select ceiling(@myvar)

---
declare @myvar as numeric(7,2) = -3.7
select floor(@myvar)
select ceiling(@myvar)

---
declare @myvar as numeric(7,2) = -3.7
select round(@myvar,0)

---
declare @myvar as numeric(7,2) = 12.345
select floor(@myvar)
select ceiling(@myvar)
select round(@myvar,0)

---
declare @myvar as numeric(7,2) = 12.345
select round(@myvar,1)

---
declare @myvar as numeric(7,2) = 12.345
select round(@myvar,-1)

---
select pi() as myPI
