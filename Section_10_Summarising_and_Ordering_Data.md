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

**can not use alias in group by statement**

---
**returned result is not deterministic, to guarantee use order by**

select year(Dateofbirth) as YearofBirth, count(*) as number_born
from tblEmployee
where 1=1
group by year(Dateofbirth)
order by year(Dateofbirth)

## Quiz 19: Summarising and ordering data

I'm counting the number of people born by year. What is needed in the GROUP BY?
```
SELECT year(DateOfBirth) as YearOfDateOfBirth, count(*) as NumberBorn
FROM tblEmployee
GROUP BY ...?
```

Answer:
```
Group by year(Dateofbirth)
```

---
What does "deterministic" refer to?

answer: it means that given the same input, the output will be the same.

---

I want to ORDER BY two different columns. It should order by the first column and then, if there are any ties, it should order by the second column.

I want to order by Column1 from smallest to biggest, and then Column2 from biggest to smallest.

Which of the following would do this?

```
order by column1, column2 desc
```

---

## Coding Exercise 9: Summarising data

There is a table called SportTeams with the following columns: TeamID, TeamName, Attack and Defense.

I want to write code which summarises data. It should have each different Attack on a different row, and the number of rows that uses that Attack.

```
SELECT Attack, COUNT(*) AS NumberOfRows
FROM SportTeams
group by attack
```

## Coding Exercise 10: Ordering data

We are going to continue to develop our query we have just created.

I want to order the results, so that we have the biggest NumberOfRows as the top.

In the event of any ties, we should order by Attack (smallest to largest).

```
SELECT Attack, COUNT(*) AS NumberOfRows
FROM SportTeams
GROUP BY Attack
order by NumberOfRows desc, attack
```

## 61. Criteria on summarised data

select left(EmployeeLastName, 1) as Initial
, count(*) as CountInitial
from [dbo].[tblEmployee]
group by left(EmployeeLastName, 1)
order by left(EmployeeLastName, 1)

---
select left(EmployeeLastName, 1) as Initial
, count(*) as CountInitial
from [dbo].[tblEmployee]
group by left(EmployeeLastName, 1)
order by CountInitial desc

---

select top (5) left(EmployeeLastName, 1) as Initial
, count(*) as CountInitial
from [dbo].[tblEmployee]
group by left(EmployeeLastName, 1)
order by CountInitial desc

**the bracket around 5 is optional**

---
```
select left(EmployeeLastName, 1) as Initial
, count(*) as CountInitial
from [dbo].[tblEmployee]
group by left(EmployeeLastName, 1)
having count(*) >= 50
order by CountInitial desc
```

---
```
select left(EmployeeLastName, 1) as Initial, count(*) as CountInitial
from [dbo].[tblEmployee]
where DateOfBirth > '19860101'
group by left(EmployeeLastName, 1)
having count(*) >= 20
order by count(*) desc
```

**you can use the alias in the order clause**


```
select left(EmployeeLastName, 1) as Initial, count(*) as CountInitial
from [dbo].[tblEmployee]
where DateOfBirth > '19860101'
group by left(EmployeeLastName, 1)
having count(*) >= 20
order by CountInitial desc
```

## Quiz 20: Criteria on summarised data

The order of the clauses in a SELECT statement, in the order that you write them, are:

SELECT, ??, WHERE, ??, HAVING and ??.

from, group by, order by

---

The WHERE clause can reduce the number of rows remaining only before the GROUP BY takes place, and the HAVING can reduce the number of rows after the grouping.

true

---
A SELECT clause alias is:

SELECT MyField as MyNewField

The only clause in which you can refer to aliases used in the SELECT clause is the:

```
order by clause
```

## Coding Exercise 11: Criteria on summarised data

In this coding exercise, we'll have a look at reducing the number of rows after summarising data.


We are going to continue to develop our query we have just created.

The current query shows the following:

    Attack  NumberOfRows
    4	6
    8	4
    3	3
    7	3
    5	2
    6	2
    1	1
    2	1

I want to reduce the number of rows, so it only returns those rows where NumberOfRows is 4 or greater.


The end result should be this:

    Attack  NumberOfRows
    4	6
    8	4

If you have any problems, you will get hints after two incorrect attempts.

```
SELECT Attack, COUNT(*) AS NumberOfRows
FROM SportTeams
GROUP BY Attack
having count(*) >=4
ORDER BY NumberOfRows DESC, Attack
```


Before the next video, can you please run the following code:

```
    Update tblEmployee
    Set EmployeeMiddleName = NULL
    Where EmployeeMiddleName = ''

```

This will change blank Middle Names to NULL Middle names.

---














