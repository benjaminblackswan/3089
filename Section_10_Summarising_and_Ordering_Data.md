## 60. Summarising and ordering data
select * from tblEmployee
where DateOfBirth between '19760101' and '19861231'
**returns 396**

select * from tblEmployee
where DateOfBirth >= '19760101' and DateOfBirth <= '19861231'

---
select * from [dbo].[tblEmployee]
where year(DateOfBirth) between 1976 and 1986
**do not use**

---
**group by clause**
select year(Dateofbirth) as YearofBirth, count(*) as number_born
from tblEmployee
group by year(Dateofbirth)

---
