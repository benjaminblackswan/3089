```
use [3089-Burton]
Go
```

# 25. Creating an Employee table
```
Create table tblEpmloyee
(EmployeeNumber int, EmployeeName int)
```

# 27. Creating temporary variables
```
-- method 1

DECLARE @myvar AS INT = 2
SELECT @myvar

-- method 2

DECLARE @myVar AS INT
SET @myVar = 3
SELECT @myVar
```

**note: must run them in one batch**

```
DECLARE @myvar AS INT = 2
SELECT @myvar AS myVariable
```
---
```
DECLARE @myvar AS INT = 2
SET @myvar = 3
SELECT @myvar AS myVariable
```
---
```
DECLARE @myvar AS INT = 2
SET @myvar = @myvar + 1
SELECT @myvar AS myVariable
```
---
```
DECLARE @myvar AS INT = 2
SET @myvar = @myvar*4 + 1
SELECT @myvar AS myVariable
```
---
```
DECLARE @myvar AS INT = 2
SET @myvar = 2.5
SELECT @myvar AS myVariable
```
--
```
DECLARE @myvar AS INT = 2
SET @myvar = - 2.5
SELECT @myvar AS myVariable
```

**INT datatype truncates the decimals, that is it always round towards zero**


# 28. Interger numbers
```
DECLARE @myvar AS TINYINT = 2
```
---
```
DECLARE @myvar AS TINYINT = 2
SET @myvar = @myvar -2
SELECT @myvar AS myVariable
```
---
```
DECLARE @myvar AS TINYINT = 2
SET @myvar = @myvar -3
SELECT @myvar AS myVariable
```
**tinyint can not go below negative**

---
```
DECLARE @myvar AS TINYINT = 2
SET @myvar = @myvar - 0.5
SELECT @myvar AS myVariable
```
---
```
DECLARE @myvar AS SMALLINT = 2
SET @myvar = @myvar - 3
SELECT @myvar AS myVariable
```
---
```
DECLARE @myvar AS SMALLINT = 2000
SET @myvar = @myvar * 10
SELECT @myvar AS myVariable
```

---

## 29. Practice Activity Number 3

Now it´s your turn.
* Can you create a variable of the data type that allows values up to 32,767, but no further.
* Then assign the variable the value of 20,000
* And then print out the contents of that variable.


```
declare @myvar as smallint
set @myvar = 20000
select @myvar
```

---
Afterwards:
* Create version 2: Change your code so that it tries to assign the value of 200,000. If it doesn't run properly, then you got it right.
* Create version 3: Correct the problem by changing your variable to a data type that allows the value of 200,000, and see if the code now works.
* Create version 4: Then change it back to 20,000, but change the variable to a data type that doesn't allow numbers that high. Then see if you get that error message again.

---
```
declare @myvar as int
set @myvar = 200000
select @myvar
```

```
declare @myvar as tinyint
set @myvar = 200000
select @myvar
```

---
And if you have having problems remembering which data type is which, try remembers that acronym which lists this in the right order.
I've included my answers in the Resources. Bear in mind that you may have a variant of these answers, and still be correct.

## 31. Non-integer numbers
** Valid**
```
declare @myvar as decimal(7,2)
set @myvar = 12345.67
select @myvar
```

---
** NOT valid**
```
declare @myvar as decimal(7,2)
set @myvar = 123456.7
select @myvar
```

**numeric and decimal are basically the same**

---
```
declare @myvar as numeric(7)
set @myvar = 12345.67
select @myvar
```

**note: numeric datatype round to the nearest**

---
```
declare @myvar as numeric(18,8)
set @myvar = 1000000000.12345678
select @myvar as myVariable
```

---
```
declare @myvar as smallmoney = 123456.78917
select @myvar as myVariable
```

**avoid float**

# 32. Mathematical functions

```
declare @myvar as numeric(7,2) = 3
select power(@myvar, 2)
```

---
```
declare @myvar as numeric(7,2) = 3
select square(@myvar)
```

---
```
declare @myvar as numeric(7,2) = 3
select power(@myvar,0.5)
select sqrt(@myvar)
```

---
```
declare @myvar as numeric(7,2) = 3.7
select floor(@myvar)
select ceiling(@myvar)
```

---
```
declare @myvar as numeric(7,2) = -3.7
select floor(@myvar)
select ceiling(@myvar)
```

---
declare @myvar as numeric(7,2) = -3.7
select round(@myvar,0)

---
```
declare @myvar as numeric(7,2) = 12.345
select floor(@myvar)
select ceiling(@myvar)
select round(@myvar,0)
```

---
```
declare @myvar as numeric(7,2) = 12.345
select round(@myvar,1)
```

---
```
declare @myvar as numeric(7,2) = 12.345
select round(@myvar,-1)
```

---
```
select pi() as myPI
select exp(1) as e
```

---
```
Declare @myvar as numeric(7,2) = 456
select abs(@myvar), sign(@myvar)
```

---
```
Declare @myvar as numeric(7,2) = -456
select abs(@myvar), sign(@myvar)
```

---
```
Declare @myvar as numeric(7,2) = 0
select abs(@myvar), sign(@myvar)
```

---
```
select rand()
```

---

## Coding Exercise 4: Mathematical functions
Write T-SQL queries to solve the following mathematical operations and retrieve the results:
```
    Find the result of 4 cubed (raised to the power of 3). Please name the result Result1.
    Round down the value of PI to the nearest integer. Please name the result Result2.
    Round up the value of PI to the nearest integer. Please name the result Result3.
```

Please end each SELECT statement with a semicolon.

If you can't remember which functions to use, please try a couple of times. You will then see hints, which should help you.

---
```
SELECT  power(4,3)    AS Result1;

SELECT  round(pi(),0)    AS Result2;

SELECT  ceiling(pi())    AS Result3;
```
---

## 33. Converting between number types
```
select 3/2
```

**this will return an integer because both numerator and denominator are integers**

---
```
select 3.0/2
```

---
```
select 3/2.0
```

---
**implicit conversion**

```
declare @myvar as decimal(5,2) = 3
select @myvar
```

---
-- explicit conversion
```
select convert(decimal(5,2), 3)/2
```

---
```
select cast(3 as decimal(5,2))/2
```

---
```
select convert(decimal(5,2),1000)
```

---
```
select convert(int,12.345)
```

---
```
select convert(int,12.345) + convert(int, 12.7)
```

---

## Practice Activity Number 4

Enter the following SQL code:
```
        select system_type_id, column_id, system_type_id / column_id as Calculation
        from sys.all_columns
```

Please try the following questions. If you need a hint, then there is a hint document attached to these questions.
```

    Have a look at the Calculation column. What is wrong with it? Please correct it.

    Please round the fractions in the Calculation column down to the next whole number (so 4.153 would round down to 4).

    Please round the fractions up (so 4.153 would round up to 5).

    Please round the fractions to the nearest one decimal place (so 4.153 would round up to 4.2).
```

    Multiply the first field, system_type_id, by 2, and then convert it to a tiniyint. If it doesn't work, instead of converting it using CONVERT or CAST, use the functions TRY_CONVERT or TRY_CAST instead - these give a NULL if the conversion doesn't work properly.

---
```
select system_type_id
, column_id
, floor(system_type_id*1.000 / column_id *1.000) as Calculation
from sys.all_columns
```

```
select system_type_id
, column_id
, ceiling(system_type_id*1.000 / column_id *1.000) as Calculation
from sys.all_columns
```

```
select system_type_id
, column_id
, round(system_type_id*1.000 / column_id *1.000, 1) as Calculation
from sys.all_columns
```

```
select system_type_id
, convert(tinyint, system_type_id * 2) as Calculation
from sys.all_columns
```

```
select system_type_id
, try_convert(tinyint, system_type_id * 2) as Calculation
from sys.all_columns
```
