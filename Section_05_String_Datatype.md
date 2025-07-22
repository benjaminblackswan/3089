## 36. Strings
```
declare @myChar as char(10)
set @myChar = 'hello'
select @myChar as myString
, len(@myChar) as myLength
, datalength(@mychar) as myDataLength
```

---
```
declare @myChar as char(10)
set @myChar = 'hellothere'
select @myChar as myString
, len(@myChar) as myLength
, datalength(@mychar) as myDataLength
```

---
```
declare @myChar as char(10)
set @myChar = ''
select @myChar as myString
, len(@myChar) as myLength
, datalength(@mychar) as myDataLength
```

---
```
declare @myChar as varchar(10)
set @myChar = ''
select @myChar as myString
, len(@myChar) as myLength
, datalength(@mychar) as myDataLength
```

**variable strings takes additional 2 bytes**

---
```
declare @myChar as nchar(10)
set @myChar = 'hello'
select @myChar as myString
, len(@myChar) as myLength
, datalength(@mychar) as myDataLength
<img width="313" height="89" alt="image" src="https://github.com/user-attachments/assets/30c1f0e2-fb5f-4a28-ab52-bb1d6f40217f" />
```


**takes 20 bytes to store because for nchar, each character takes 2 bytes, nchar(10) is 10 char so 10*2 = 20 bytes**

---
```
declare @myChar as nvarchar(10)
set @myChar = 'hello'
select @myChar as myString
, len(@myChar) as myLength
, datalength(@mychar) as myDataLength
```

<img width="336" height="88" alt="image" src="https://github.com/user-attachments/assets/22f59b7a-58f8-48a3-909d-5c2ac5fa9986" />

**takes 12 bytes to store because for nvarchar, each character takes 2 bytes plus 2 extra bytes for variable-ness. nvarchar(10) with "hello" string is 5 char * 2 + 2 = 12 bytes**

---
### how to input unicode and display unicode

```
declare @myChar as nvarchar(10)
set @myChar = 'hello☻'
select @myChar as myString
, len(@myChar) as myLength
, datalength(@mychar) as myDataLength
```

<img width="326" height="98" alt="image" src="https://github.com/user-attachments/assets/2212ca34-33b9-4c16-bfd4-29ee4ae825ae" />

**data type must be nchar or nvarchar, and the string must have CAPITAL N before it**
```
declare @myChar as nvarchar(10)
set @myChar = N'hello☻'
select @myChar as myString
, len(@myChar) as myLength
, datalength(@mychar) as myDataLength
```

<img width="319" height="122" alt="image" src="https://github.com/user-attachments/assets/c5c3d46f-918a-4e5a-b1fc-9744f9fe11a2" />

**now you get the smiley face in the result**

# Quiz 10. String

Question 1:
Which of these is a valid NVARCHAR(10) string?

Answer: N'hello'

---
Question 2:
```
DECLARE @myvariable NVARCHAR(20) = N'hello'
How many bytes are used in N'hello'?
```

Answer: 12
5*2 + 2 = 12

# 37. String Functions - extraction
**remember to use Windows' Character Map app to input unicode characters**

```
declare @chrAscii as varchar(10) = 'hellothere'
declare @chrUnicode as nvarchar(10) = N'hello☻'

select	left(@chrAscii, 2) as myAscii
	,	right(@chrUnicode, 2) as myUnicode
	,	substring(@chrAscii, 3, 2) as middleletters
```

---
```
declare @chrAscii as varchar(10) = '   hello   '
declare @chrUnicode as nvarchar(10) = N'hello☻'

select	ltrim(@chrAscii) as left_trimed
	,	rtrim(@chrAscii) as right_trimed
	,	ltrim(rtrim(@chrAscii)) as both_trimed
	,	trim(@chrAscii) as left_trimedv2
```


**Note that in SQL Server 2017 and later, you can use TRIM instead of ltrim(rtrim(@chrAscii))**
https://learn.microsoft.com/en-us/sql/t-sql/functions/trim-transact-sql?view=sql-server-ver17

---
```
declare @chrAscii as varchar(10) = '   hello   '
declare @chrUnicode as nvarchar(10) = N'hello☻'

select	replace(@chrAscii, 'l', 'L') as myReplacement
	,	upper(@chrAscii) as myUpper
	,	lower(@chrAscii) as myLower
```

---
## Quiz 11: String Functions Extraction
 
Question 1:
```
DECLARE @myvar VARCHAR(10) = 'HELLO'
```

What function will give the answer 'LL'?
 
Answer: 
```
select substring(@myvar, 3, 2)
```

---
Question 2:
True or False?
RTRIM will remove all the spaces at the beginning and end of a string.

Answer:False

---

# 39. Null - an introduction
```
declare @myvar as int
select @myvar as myCol
```

---
```
declare @mystring as nvarchar(20)
select datalength(@mystring) as myString
```

---
```
declare @mydecimal decimal(5,2)
select convert(decimal(5,2),1000)
select cast(1000 as decimal(5,2))
```

---
```
declare @mydecimal decimal(5,2)
select try_convert(decimal(5,2),1000)
select try_cast(1000 as decimal(5,2))
```

---
```
select try_convert(decimal(5,2), [fieldname])
from tblTable
```

---
# 40. Joining two strings together
```
declare @firstname as nvarchar(20)
declare @middlename as nvarchar(20)
declare @lastname as nvarchar(20)

set @firstname = 'Sarah'
set @lastname = 'Milligan'

select @firstname + ' ' + @middlename + ' ' + @lastname
```

---
```
declare @firstname as nvarchar(20)
declare @middlename as nvarchar(20)
declare @lastname as nvarchar(20)

set @firstname = 'Sarah'
set @lastname = 'Milligan'

select @firstname + iif(@middlename is null, '',' ' + @middlename) + ' ' + @lastname as Fullname
```

---
```
declare @firstname as nvarchar(20)
declare @middlename as nvarchar(20)
declare @lastname as nvarchar(20)

set @firstname = 'Sarah'
--set @middlename = 'Jane'
set @lastname = 'Milligan'

select @firstname + iif(@middlename is null, '',' ' + @middlename) +
					' ' + @lastname as Fullname
	, @firstname + Case When @middlename is null
							then ''
						else ' ' + @middlename
					end
				+ ' ' + @lastname as fullname_v2
	, @firstname + coalesce(' ' + @middlename, '') + ' ' + @lastname as Fullname_v3
	, concat(@firstname, ' ' + @middlename, ' ', @lastname) as Fullname_v4
```

---

## Quiz 12. Null

```
Question 1: 
DECLARE @myint AS int
SELECT @myint
What is the result?
```

answer: NULL

Question 2:

```
DECLARE @mychar1 as NVARCHAR(10) = N'hello'
DECLARE @mychar2 as NVARCHAR(10)
SELECT LEFT(@mychar1 + @mychar2, 2)
What is the result?
```

Answer: NULL 

## 41. Joining a string to a number
**this will work because the number is quotation mark**
```
select 'My number is: ' + '4567'
```

---
**this will not work because you can not join string to number**
```
select 'My number is: ' + 4567
```

---
```
select 'My number is: ' + convert(varchar(20),4567)
select 'My number is: ' + cast(4567 as varchar(20))
```

---
```
select 'My salary is: ' + convert(varchar(20),2345)
select 'My salary is: $' + convert(varchar(20),2345.6)

select 'My salary is: ' + format(2345.6, 'C')
select 'My salary is: ' + format(2345.6, 'C', 'en-GB')
select 'My salary is: ' + format(2345.6, 'C', 'fr-FR')
```

## 42. Practice Activity Number 5

Create the following T-SQL query:
```
select [name]
from sys.all_columns
```

Please try the following questions. If you need a hint, then there is a hint document attached to these questions.

1. Add the letter A to the end of each name.
2. Add the letter Ⱥ to the end of each name. (You may want to copy and paste this letter, as it is an A with a stroke through it). If you are getting question marks, then give it another try.
3. Remove the first character from name.
4. Remove the last original character from name.

---
```
select [name] + 'A'
, [name] + N'Ⱥ'
, len(name) length
, substring(name, 2, len(name) -1)
, substring(name, 1, len(name) -1)
from sys.all_columns
```


































