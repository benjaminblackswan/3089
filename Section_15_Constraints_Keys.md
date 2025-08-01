## 88. Primary key

* not nullable
* clustered ie sorted
* one per table

primary key is usually a *surrogate key*.

```
Alter table tblEmployee
Add constraint PK_tblEmployee primary key (EmployeeNumber)
```

<img width="328" height="184" alt="image" src="https://github.com/user-attachments/assets/68b4a9ff-0379-48e4-af04-e0377f173a06" />

```
insert into tblEmployee
values (2004, 'John', 'F.', 'Smith', 'ab12345', '2014-01-01', 'Accounts')
```

This insert will work for the first time, but if you try to insert it again.
<img width="929" height="42" alt="image" src="https://github.com/user-attachments/assets/d721448e-74ca-4d8c-8de7-702511367af0" />


if you look at the indexes created. Primary key is clustered while unique key is not clustered.

<img width="366" height="41" alt="image" src="https://github.com/user-attachments/assets/f912d6eb-b1c7-4c26-a812-ba085036a988" />

if you wish to create a **non-clustered** primary key, you must add the phrase nonclustered

```
Alter table tblEmployee
Add constraint PK_tblEmployee primary key nonclustered (EmployeeNumber)
```

You can create a primary key constraint while creating the table.

```
create table tblEmployee2
(EmployeeNumber int Constraint PK_tblEmployee2 Primary key identity(1,1),
EmployeeName nvarchar(20))
```

```
insert into tblEmployee2
values	('My Name')
		, ('My Name')

select * from tblEmployee2
```


<img width="318" height="88" alt="image" src="https://github.com/user-attachments/assets/997784aa-b390-4700-b59a-8237ae45cead" />


delete and insert again.

```
delete from tblEmployee2;

insert into tblEmployee2
values	('My Name')
		, ('My Name');

select * from tblEmployee2;
```

<img width="225" height="61" alt="image" src="https://github.com/user-attachments/assets/9aca29dd-331f-49b9-b038-9bc739ca31e8" />

Truncate table will reset identity

```
truncate table tblEmployee2
insert into tblEmployee2
values	('My Name')
		, ('My Name')

select * from tblEmployee2
```

<img width="531" height="253" alt="image" src="https://github.com/user-attachments/assets/21d36a6c-2eeb-4489-9d3f-a9b437419d57" />

<img width="573" height="280" alt="image" src="https://github.com/user-attachments/assets/770dbe6a-0992-450c-ae73-a1e5b6924e69" />

<img width="550" height="292" alt="image" src="https://github.com/user-attachments/assets/69dfe13c-d67b-4c53-8e61-40a23994e039" />



## 90. Foreign key

seeking: when searching a clustered primary key
scanning: when searching through a non-clustered primary key.

<img width="1162" height="840" alt="image" src="https://github.com/user-attachments/assets/7ae97912-7b2b-4dce-9384-265c3e4d87ab" />

The data type between fk and pk are be the identical.

```
Alter table tblTransaction
Add constraint fk_tblTransaction_Empno Foreign Key (EmployeeNumber)
References tblEmployee(EmployeeNumber)
```
<img width="1014" height="114" alt="image" src="https://github.com/user-attachments/assets/336c854c-bbae-4d30-ba4b-0c0884d6a06e" />

Create PK constraint on tblEmployee first

```
Alter table tblEmployee with nocheck
Add constraint PK_tblEmployee primary key (EmployeeNumber)
```

For testing purpose, lets do a simple join query.
```
select E.EmployeeNumber, T.*
from tblEmployee as E
right join tblTransaction as T
on E.EmployeeNumber = T.EmployeeNumber
where T.Amount in (-179.47, 786.22, -967.36, 957.03)
```
and this will return these four rows.

<img width="408" height="110" alt="image" src="https://github.com/user-attachments/assets/1cb9ec6c-3a0b-4335-9b77-39e7dbf0cbac" />



```
Begin tran
alter table tblTransaction alter column EmployeeNumber int null
alter table tblTransaction add constraint DF_tblTransaction default 124 for EmployeeNumber
alter table tblTransaction With NOCHECK
add constraint FK_tblTransaction_EmployeeNumber Foreign key(EmployeeNumber)
References tblEmployee(EmployeeNumber)

select E.EmployeeNumber, T.*
from tblEmployee as E
right join tblTransaction as T
on E.EmployeeNumber = T.EmployeeNumber
where T.Amount in (-179.47, 786.22, -967.36, 957.03)

Rollback tran
```

<img width="406" height="94" alt="image" src="https://github.com/user-attachments/assets/995bf310-88c3-4ade-a08a-4472100748c4" />


```
Begin tran
alter table tblTransaction alter column EmployeeNumber int null
alter table tblTransaction add constraint DF_tblTransaction default 124 for EmployeeNumber
alter table tblTransaction With NOCHECK
add constraint FK_tblTransaction_EmployeeNumber Foreign key(EmployeeNumber)
References tblEmployee(EmployeeNumber)

update tblEmployee Set EmployeeNumber = 9123 where EmployeeNumber = 123

select E.EmployeeNumber, T.*
from tblEmployee as E
right join tblTransaction as T
on E.EmployeeNumber = T.EmployeeNumber
where T.Amount in (-179.47, 786.22, -967.36, 957.03)

Rollback tran

```

We will get an error

<img width="1030" height="63" alt="image" src="https://github.com/user-attachments/assets/1c487c48-86fe-4064-aad0-7c7b514cc74e" />

We will need add `On update cascade`

```
Begin tran
alter table tblTransaction alter column EmployeeNumber int null
alter table tblTransaction add constraint DF_tblTransaction default 124 for EmployeeNumber
alter table tblTransaction With NOCHECK
add constraint FK_tblTransaction_EmployeeNumber Foreign key(EmployeeNumber)
References tblEmployee(EmployeeNumber)

on update cascade
update tblEmployee Set EmployeeNumber = 9123 where EmployeeNumber = 123

select E.EmployeeNumber, T.*
from tblEmployee as E
right join tblTransaction as T
on E.EmployeeNumber = T.EmployeeNumber
where T.Amount in (-179.47, 786.22, -967.36, 957.03)
Rollback tran
```

<img width="401" height="101" alt="image" src="https://github.com/user-attachments/assets/83d7cb96-798e-487f-a0a3-deeaece042c5" />


or you can set them to NULL

```
Begin tran
alter table tblTransaction alter column EmployeeNumber int null
alter table tblTransaction add constraint DF_tblTransaction default 124 for EmployeeNumber
alter table tblTransaction With NOCHECK
add constraint FK_tblTransaction_EmployeeNumber Foreign key(EmployeeNumber)
References tblEmployee(EmployeeNumber)

on update set null
update tblEmployee Set EmployeeNumber = 9123 where EmployeeNumber = 123

select E.EmployeeNumber, T.*
from tblEmployee as E
right join tblTransaction as T
on E.EmployeeNumber = T.EmployeeNumber
where T.Amount in (-179.47, 786.22, -967.36, 957.03)
Rollback tran
```

<img width="448" height="101" alt="image" src="https://github.com/user-attachments/assets/58012c5f-e3ca-4b1f-bcd1-6814e8ffe30d" />

---

## Quiz 31: Foreign Keys

<img width="540" height="508" alt="image" src="https://github.com/user-attachments/assets/8a0d53dc-a5dd-4d23-aa22-cfb1cf28a1c5" />

<img width="540" height="321" alt="image" src="https://github.com/user-attachments/assets/2a79f475-5eeb-41af-a96a-125d93ae46e6" />

<img width="826" height="276" alt="image" src="https://github.com/user-attachments/assets/0d2fcb30-9ea5-4aec-8d7f-b72d81da1fd1" />

<img width="830" height="278" alt="image" src="https://github.com/user-attachments/assets/d74074b7-c766-412f-988a-82583e184a07" />




