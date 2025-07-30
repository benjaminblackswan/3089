## 123. Let's create our first procedure

creating first simply stored proc

```
create proc NameEmployees as
begin
	select EmployeeNumber, EmployeeFirstName, EmployeeLastName
	from tblEmployee
end
```

remember that stored Proc must be have `begin` and `end`

To run the stored proc

```
exec NameEmployees
```
