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

---
