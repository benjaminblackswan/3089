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

<img width="656" height="373" alt="image" src="https://github.com/user-attachments/assets/554ce8e2-7cdf-4ba1-91b9-cea12dcf0826" />

<img width="667" height="390" alt="image" src="https://github.com/user-attachments/assets/ce6f27af-e439-4203-9a7d-c88d70eaaa81" />

<img width="626" height="422" alt="image" src="https://github.com/user-attachments/assets/d9fb067f-6d02-4ad4-af7e-768c5166ef33" />



## 86. Check Constraints

Create a check constraint
```
alter table tblTransaction
add constraint chkAmount check (amount  >-1000 and Amount < 1000)
```
<img width="295" height="97" alt="image" src="https://github.com/user-attachments/assets/1bf450ed-8a93-4e82-ba46-8d44e177736c" />

Test by inserting

```
insert into tblTransaction
values (1010, '2014-01-01', 1)
```
<img width="817" height="76" alt="image" src="https://github.com/user-attachments/assets/26b6a27d-6598-479f-a1ec-9d7c90ca5384" />

```
insert into tblTransaction
values (190, '2014-01-01', 1)
```

<img width="555" height="87" alt="image" src="https://github.com/user-attachments/assets/d2274306-0ee1-4e24-9443-ec2858957d9a" />

Looking at the columns, only the DateOfTransaction is nullable.

```
insert into tblTransaction
values (null, '2014-01-01', 1)
```
This will fail because the first column is **not Nullable**.

---

<img width="456" height="199" alt="image" src="https://github.com/user-attachments/assets/e06f8aa0-24fd-4a5c-a3a7-24dd041b03ff" />

Note that the MiddleName column is nullable.

Lets add the following Check Constraint. Not the **"with nocheck"** clause, this means that this constraint does not check for existing data. Without this clause, the constraint will fail to create.

```
alter table tblEmployee with nocheck
add constraint chkMiddleName check
(replace(employeeMiddleName,'.','') = EmployeeMiddleName or EmployeeMiddleName is null)
```

The logic of this constraint only allow insert if the middle name have no period or is null.

Test the constraint with this Insert

```
begin tran
	Insert into tblEmployee
	values (2003, 'A', 'B.', 'C', 'D', '2014-01-01', 'Account')
	select * from tblEmployee where EmployeeNumber = 2003
rollback tran
```
<img width="892" height="60" alt="image" src="https://github.com/user-attachments/assets/a252ef26-cdc1-4ac4-a76f-49ac85fc5881" />


Now remove the period

```
begin tran
	Insert into tblEmployee
	values (2003, 'A', 'B', 'C', 'D', '2014-01-01', 'Account')
	select * from tblEmployee where EmployeeNumber = 2003
rollback tran
```
<img width="905" height="86" alt="image" src="https://github.com/user-attachments/assets/b0678f6d-5566-4fd9-8d38-6cb68bbff966" />

```
begin tran
	Insert into tblEmployee
	values (2003, 'A', null, 'C', 'D', '2014-01-01', 'Account')
	select * from tblEmployee where EmployeeNumber = 2003
rollback tran
```

<img width="738" height="50" alt="image" src="https://github.com/user-attachments/assets/f7d1ddec-1e9d-4ec5-91f5-0cc4a422fe33" />

---

Lets do a constrait on the date of birth.
```
alter table tblEmployee with nocheck
add constraint chkDateOfBirth check (DateOfBirth between '1900-01-01' and getDate())
```

test the constraint
```
begin tran
	Insert into tblEmployee
	values (2003, 'A', 'B', 'C', 'D', '1815-01-01', 'Account')
	select * from tblEmployee where EmployeeNumber = 2003
rollback tran
```
<img width="1043" height="63" alt="image" src="https://github.com/user-attachments/assets/8dc09c44-d3c8-4e4f-9866-5408f019985c" />

---

**Constraint when creating a table**


This Constraint creation statement works, but it is missing the name of the Constraint.
```
create table tblEmployee2
(employeeMiddleName varchar(50) null check
(replace(employeeMiddleName,'.','') = EmployeeMiddleName or EmployeeMiddleName is null))
```
The system has automatically added a constraint name

<img width="448" height="173" alt="image" src="https://github.com/user-attachments/assets/56439f5f-4bda-41a3-8728-dc110c3fec6a" />

as you can see, the system generated constraint name is kinda ugly, we don't want that.

lets drop the table

```
drop table tblEmployee2
```
and recreate the same table with a specified constraint name.

```
create table tblEmployee2
(employeeMiddleName varchar(50) null constraint ck_EmployeeMiddleName check
(replace(employeeMiddleName,'.','') = EmployeeMiddleName or EmployeeMiddleName is null))
```

<img width="398" height="180" alt="image" src="https://github.com/user-attachments/assets/a68e6950-1110-4d83-829e-f44a36ab63fb" />

---
```
drop table tblEmployee2;

alter table tblEmployee
drop chkDateOfBirth;

alter table tblEmployee
drop chkMiddleName;

alter table tblTransaction
drop chkAmount;
```

---

## Quiz 29: Check constraints

<img width="595" height="518" alt="image" src="https://github.com/user-attachments/assets/2fce80cf-5b76-45ae-b805-871e90befe0d" />


<img width="539" height="321" alt="image" src="https://github.com/user-attachments/assets/cf19af66-a0ab-4702-abf7-95692243c4e2" />


<img width="575" height="514" alt="image" src="https://github.com/user-attachments/assets/433c7f44-1094-417c-ac78-6d5352566586" />


