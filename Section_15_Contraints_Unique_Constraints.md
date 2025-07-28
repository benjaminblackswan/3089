## 81. What are constraints?

Right click on the table tblEmployee, you can see that we do not allow Nulls for `EmployeeNumber` column.
<img width="324" height="264" alt="image" src="https://github.com/user-attachments/assets/a6845f22-a4bb-4290-90ae-1506ec606775" />

If one of the rows you try to insert fails, then the entire transaction fails.

```
begin tran
INSERT INTO tblEmployee
values (2001, 'FirstName', 'M', 'LastName', 'AB123456C', '1994-01-01', 'Commerical'),
(null, 'AnotherFirstName', 'N', 'AnotherLastName', 'AB123457C', '1994-01-02', 'Finance')
rollback tran
```

## 82 and 83. Unique constraints

This is the basic syntax for adding a contraint
```
alter table tblEmployee
add constraint unqGovernmentID unique (EmployeeGovID);
```

and we got this error 
<img width="999" height="81" alt="image" src="https://github.com/user-attachments/assets/10a0271b-0b69-4f04-bb7c-c38330422550" />

therefore we need to find the duplicates, we this script

```
select EmployeeGovID, count(employeeGovID) as myCount
from tblEmployee
group by EmployeeGovID
having count(EmployeeGovID) > 1
```
there are two empgovid with count > 1
<img width="186" height="60" alt="image" src="https://github.com/user-attachments/assets/81951518-864f-4a18-bda0-3399ae75a8f4" />

Then we find all the rows in tblEmployee with duplicate GovID using subquery
```
select * from tblEmployee
where EmployeeGovID in (
select EmployeeGovID as myCount
from tblEmployee
group by EmployeeGovID
having count(EmployeeGovID) > 1)
```
<img width="762" height="172" alt="image" src="https://github.com/user-attachments/assets/b580c97b-31c1-4719-8b56-dbed7d1d6e1a" />


Now we need to delete all the duplicate rows

```
begin tran

delete from tblEmployee
where EmployeeNumber <3

delete top(2) from tblEmployee
where EmployeeNumber in (131, 132)

select * from tblEmployee where EmployeeGovID in ('HN513777D', 'TX593671R')

Commit tran
```

<img width="787" height="101" alt="image" src="https://github.com/user-attachments/assets/8daecff8-02d8-48dd-9448-efeb70fc9e3b" />


run the alter table script again

```
alter table tblEmployee
add constraint unqGovernmentID unique (EmployeeGovID);
```

<img width="530" height="100" alt="image" src="https://github.com/user-attachments/assets/ed3ddbcf-7300-49ca-b026-8e75c3dc5a5c" />

You can find the contraint in the Keys folder of the table.

<img width="355" height="365" alt="image" src="https://github.com/user-attachments/assets/da164b97-7b13-424f-bd85-36589c7644ba" />

and sql server also created an index.

<img width="622" height="344" alt="image" src="https://github.com/user-attachments/assets/478ed793-42b4-48fe-9ff8-a169a355d39a" />


### Constraints on multiple columns

```
alter table tblTransaction
add constraint unqtransaction unique (Amount, DateOfTransaction, employeenumber);
```
<img width="404" height="178" alt="image" src="https://github.com/user-attachments/assets/29cfb969-9b14-43d1-a8af-e952e3f5eac8" />

### lets test the contraint

```
delete from tblTransaction
where EmployeeNumber = 131
```

```
insert into tblTransaction
values (1, '2015-01-01', 131)
```

### do the insert again

<img width="860" height="115" alt="image" src="https://github.com/user-attachments/assets/26ee235e-d81f-4135-a967-9f955c409f4d" />

### Drop a constraint

```
alter table tbltransaction
drop constraint unqTransaction
```

### Create a table with Constraint in one step

```
Create table tbltransaction2
(amount smallmoney not null
, dateofTransaction smalldatetime not null
, EmployeeNumber int not null
, constraint unqTransaction2 unique (       Amount
                                          , dateofTransaction
                                          , EmployeeNumber)
)
```

```
drop table tbltransaction2
```

## Quiz 27: Unique constraints
<img width="837" height="383" alt="image" src="https://github.com/user-attachments/assets/0b83d298-c4b2-422f-aba3-b391eb8abae3" />


<img width="841" height="322" alt="image" src="https://github.com/user-attachments/assets/e6d3c2e8-49b0-465b-92f7-0eebadcd245a" />

<img width="846" height="390" alt="image" src="https://github.com/user-attachments/assets/d08bbfc2-e2f6-45fe-8149-9747074ca6fb" />


## 84. Quiz 27: Unique constraints
       
## 84. Default constraints - what are they?
       
## 85. Default constraints in action
