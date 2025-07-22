## 72. Missing data
```
select E.EmployeeNumber as ENumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber as TransactNumber,
		sum(T.Amount) as TotalAmount
from tblEmployee as E
left join tblTransaction as T
on E.EmployeeNumber = T.EmployeeNumber
group by E.EmployeeNumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber
order by E.EmployeeNumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber
```

**We need to find all the Employees who do not have a Transaction, so we put where statement to find T.EmployeeNumber is null**
```
select E.EmployeeNumber as ENumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber as TransactNumber,
		sum(T.Amount) as TotalAmount
from tblEmployee as E
left join tblTransaction as T
on E.EmployeeNumber = T.EmployeeNumber
where T.EmployeeNumber is null
group by E.EmployeeNumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber
order by E.EmployeeNumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber
```

**if the above code is complex, we can use derived table**

```
Select *
from(
select E.EmployeeNumber as ENumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber as TransactNumber,
		sum(T.Amount) as TotalAmount
from tblEmployee as E
left join tblTransaction as T
on E.EmployeeNumber = T.EmployeeNumber
group by E.EmployeeNumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber
order by E.EmployeeNumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber) as NewTable
```


  **note, this will not work, ORDER BY clause does not work in derived tables or CTE.**

```
Select *
from(
select E.EmployeeNumber as ENumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber as TransactNumber,
		sum(T.Amount) as TotalAmount
from tblEmployee as E
left join tblTransaction as T
on E.EmployeeNumber = T.EmployeeNumber
group by E.EmployeeNumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber) as NewTable
order by ENumber, TransactNumber, EmployeeFirstName, EmployeeLastName
```
  **note, you must also update the column names in order by to reflect the inner query's new names**

  
```
Select *
from(
select E.EmployeeNumber as ENumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber as TransactNumber,
		sum(T.Amount) as TotalAmount
from tblEmployee as E
left join tblTransaction as T
on E.EmployeeNumber = T.EmployeeNumber
group by E.EmployeeNumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber) as NewTable
where TransactNumber is null
order by ENumber, TransactNumber, EmployeeFirstName, EmployeeLastName
```

---
  
```
Select Enumber, EmployeeFirstName, EmployeeLastName
from(
select E.EmployeeNumber as ENumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber as TransactNumber,
		sum(T.Amount) as TotalAmount
from tblEmployee as E
left join tblTransaction as T
on E.EmployeeNumber = T.EmployeeNumber
group by E.EmployeeNumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber) as NewTable
where TransactNumber is null
order by ENumber, TransactNumber, EmployeeFirstName, EmployeeLastName
```

### changing from a left join to a right join
```
Select *
from(
select E.EmployeeNumber as ENumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber as TransactNumber,
		sum(T.Amount) as TotalAmount
from tblEmployee as E
right join tblTransaction as T
on E.EmployeeNumber = T.EmployeeNumber
group by E.EmployeeNumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber) as NewTable
--where TransactNumber is null
order by ENumber, TransactNumber, EmployeeFirstName, EmployeeLastName
```

find all the phantom transactions, ie transactions created without an employee

```
Select *
from(
select E.EmployeeNumber as ENumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber as TransactNumber,
		sum(T.Amount) as TotalAmount
from tblEmployee as E
right join tblTransaction as T
on E.EmployeeNumber = T.EmployeeNumber
group by E.EmployeeNumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber) as NewTable
where ENumber is null
order by ENumber, TransactNumber, EmployeeFirstName, EmployeeLastName
```

should returns 104 rows.

## Quiz 24: Missing data

There are two tables - tblFirst and tblSecond.
I want the following query to have the fields of tblFirst, but only when there are no matching rows in tblSecond.
How does this query end?

```
SELECT tblFirst.* from tblFirst LEFT JOIN tblSecond ON tblFirst.ID = tblSecond.ID
```

Answer:
```
Where tblSecond.ID is NULL
```

## 73. Deleting data
```
begin transaction

select count(*) from tblTransaction

delete tblTransaction
from tblEmployee as E
right join tblTransaction t
on e.EmployeeNumber = t.EmployeeNumber
where e.EmployeeNumber is null

select count(*) from tblTransaction

rollback transaction
```
---
```
begin transaction
select count(*) from tblTransaction

delete
from tblTransaction
where EmployeeNumber in
(
Select TransactNumber
from(
select E.EmployeeNumber as ENumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber as TransactNumber,
		sum(T.Amount) as TotalAmount
from tblEmployee as E
right join tblTransaction as T
on E.EmployeeNumber = T.EmployeeNumber
group by E.EmployeeNumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber) as NewTable
where ENumber is null)

select count(*) from tblTransaction
rollback transaction
```

## Quiz 25: Deleting data
<img width="948" height="388" alt="image" src="https://github.com/user-attachments/assets/eac289ab-487d-4d54-aa92-2c4d9c985a9c" />

<img width="933" height="324" alt="image" src="https://github.com/user-attachments/assets/eccaae26-ef58-4eaa-9d08-e463e1277021" />

<img width="925" height="554" alt="image" src="https://github.com/user-attachments/assets/12434c11-62ec-4b9f-9a7c-3e1bdfe90501" />

## 74. Updating data
```
select * from tblEmployee where EmployeeNumber = 194
select * from tblTransaction where EmployeeNumber = 3
select * from tblTransaction where EmployeeNumber = 194
```
the transaction done by empNo. 3 should have been done by empNo. 194, therefore we need to update it



```
begin tran
select * from tblTransaction where EmployeeNumber = 194


--
update tblTransaction
set EmployeeNumber = 194
from tblTransaction
where EmployeeNumber = 3


--
select * from tblTransaction where EmployeeNumber = 194
rollback tran

```

If you need to update multiple values, eg update all the empno. 3, 5, 7 and 9


begin tran
select * from tblTransaction where EmployeeNumber = 194


--
update tblTransaction
set EmployeeNumber = 194
from tblTransaction
where EmployeeNumber in (3,5,7,9)


--
select * from tblTransaction where EmployeeNumber = 194
rollback tran

---

To see what rows are deleted and inserted, use **output** keyword

```
begin tran

update tblTransaction
set EmployeeNumber = 194
output inserted.*, deleted.*
from tblTransaction
where EmployeeNumber in (3,5,7,9) 

rollback tran
```

## Quiz 26: Updating data

<img width="982" height="393" alt="image" src="https://github.com/user-attachments/assets/57639746-4dcb-40d9-af2b-d761486b92ed" />

<img width="921" height="473" alt="image" src="https://github.com/user-attachments/assets/f0d5608f-92c4-4746-a7c4-1e98cabcff13" />











