## 84. Default constraints

```
alter table tblTransaction
add DateOfEntry datetime
```

We get a nullable column
<img width="415" height="172" alt="image" src="https://github.com/user-attachments/assets/580641a6-5f62-4492-8cbe-ca9f76b580cd" />

Lets add a dynamic default contraint of getdate() for this new column
```
alter table tblTransaction
add constraint defDateOfEntry default getdate() for DateOfEntry;
```

```
delete from tblTransaction where EmployeeNumber < 3
```

```
insert into tblTransaction (amount, DateOfTransaction, EmployeeNumber)
values (1, '2014-01-01', 1)
insert into tblTransaction (amount, DateOfTransaction, EmployeeNumber, DateOfEntry)
values (2, '2014-01-01', 1, '2013-01-01')
```

```
select * from tblTransaction where EmployeeNumber < 3
```

<img width="472" height="73" alt="image" src="https://github.com/user-attachments/assets/322b821e-50fd-492a-bc1f-a0d3645deb7b" />

Constraints are database objects, therefore they must be unique cross the entire database. The following code will give an error.

```
create table tblTransaction2
(Amount smallmoney not null,
DateOfTransaction smalldatetime not null,
EmployeeNumber int not null,
DateOfEntry datetime null Constraint defDateOfEntry default getdate())
```

<img width="657" height="99" alt="image" src="https://github.com/user-attachments/assets/e87408e8-fa2a-4e98-83fc-4a6644b9481f" />

generally ppl put the table name in the constraint name.

```
create table tblTransaction2
(Amount smallmoney not null,
DateOfTransaction smalldatetime not null,
EmployeeNumber int not null,
DateOfEntry datetime null Constraint tblTransaction2_defDateOfEntry default getdate())
```

```
drop table tblTransaction2
```

If we try to drop the column with dropping the constraint it has first, we get this error
other we get this error.

```
alter table tbltransaction
drop column DateOfEntry
```

<img width="824" height="97" alt="image" src="https://github.com/user-attachments/assets/58d630f4-a68b-4906-a0f0-f981827b6e74" />


We must first drop the constraint before we can drop the column.

```
alter table tblTransaction
drop constraint defDateOfEntry;

alter table tbltransaction
drop column DateOfEntry;
```

## Quiz 28: Default constraints

<img width="956" height="373" alt="image" src="https://github.com/user-attachments/assets/554ce8e2-7cdf-4ba1-91b9-cea12dcf0826" />

<img width="867" height="390" alt="image" src="https://github.com/user-attachments/assets/ce6f27af-e439-4203-9a7d-c88d70eaaa81" />

<img width="826" height="422" alt="image" src="https://github.com/user-attachments/assets/d9fb067f-6d02-4ad4-af7e-768c5166ef33" />




## 86. Check Constraints

















