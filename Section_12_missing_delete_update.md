## 72. Missing data
```
select E.EmployeeNumber as ENumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber as Number,
		sum(T.Amount) as TotalAmount
from tblEmployee as E
left join tblTransaction as T
on E.EmployeeNumber = T.EmployeeNumber
group by E.EmployeeNumber, E.EmployeeFirstName,
		E.EmployeeLastName, T.EmployeeNumber
```
