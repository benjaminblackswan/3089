# 36. Strings

declare @myChar as char(10)
set @myChar = 'hello'
select @myChar as myString
, len(@myChar) as myLength
, datalength(@mychar) as myDataLength

---
declare @myChar as char(10)
set @myChar = 'hellothere'
select @myChar as myString
, len(@myChar) as myLength
, datalength(@mychar) as myDataLength

---
declare @myChar as char(10)
set @myChar = ''
select @myChar as myString
, len(@myChar) as myLength
, datalength(@mychar) as myDataLength

---
declare @myChar as varchar(10)
set @myChar = ''
select @myChar as myString
, len(@myChar) as myLength
, datalength(@mychar) as myDataLength

**variable strings takes additional 2 bytes**
---
