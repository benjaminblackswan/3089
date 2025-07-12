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

declare @myChar as nchar(10)
set @myChar = 'hello'
select @myChar as myString
, len(@myChar) as myLength
, datalength(@mychar) as myDataLength
<img width="313" height="89" alt="image" src="https://github.com/user-attachments/assets/30c1f0e2-fb5f-4a28-ab52-bb1d6f40217f" />


**takes 20 bytes to store because for nchar, each character takes 2 bytes, nchar(10) is 10 char so 10*2 = 20 bytes**

---
declare @myChar as nvarchar(10)
set @myChar = 'hello'
select @myChar as myString
, len(@myChar) as myLength
, datalength(@mychar) as myDataLength

<img width="336" height="88" alt="image" src="https://github.com/user-attachments/assets/22f59b7a-58f8-48a3-909d-5c2ac5fa9986" />

**takes 12 bytes to store because for nvarchar, each character takes 2 bytes plus 2 extra bytes for variable-ness. nvarchar(10) with "hello" string is 5 char * 2 + 2 = 12 bytes**

---
### how to input unicode and display unicode

declare @myChar as nvarchar(10)
set @myChar = 'hello☻'
select @myChar as myString
, len(@myChar) as myLength
, datalength(@mychar) as myDataLength

<img width="326" height="98" alt="image" src="https://github.com/user-attachments/assets/2212ca34-33b9-4c16-bfd4-29ee4ae825ae" />

**data type must be nchar or nvarchar, and the string must have N before it**

declare @myChar as nvarchar(10)
set @myChar = N'hello☻'
select @myChar as myString
, len(@myChar) as myLength
, datalength(@mychar) as myDataLength

<img width="319" height="122" alt="image" src="https://github.com/user-attachments/assets/c5c3d46f-918a-4e5a-b1fc-9744f9fe11a2" />

**now you get the smiley face in the result**
