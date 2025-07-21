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


The background color is `#ffffff` for light mode and `#000000` for dark mode.



































