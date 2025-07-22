# 45. Date Data Types
Is your SSMS set up in English? If so, please go to the next video.

If not, then...

As you have seen in the previous video, Microsoft has recommended that you create dates in this format:

'2025-01-01'

However, this doesn't necessarily work if you are using an interface language other than English. In the next video, I'll use the statement:

    declare @mydate as datetime = '2015-06-24 12:34:56.124'

If this doesn't work on your version of SQL Server, then please use one of the following 2 formats instead:

    declare @mydate as datetime = '20150624 12:34:56.124'

    declare @mydate as datetime = '2015-06-24T12:34:56.124'

In the first statement, you remove the hyphens. In the second statement, use a letter T instead of a space between the date and time. However, this only works if you have a time part.

## 47. Setting dates and Date extraction
```
declare @mydate as datetime = '2025-06-24 12:34:56.126'
select @mydate as MyDate
```

---
```
declare @mydate as datetime = '20250624 12:34:56.126'
select @mydate as MyDate
```

---
```
declare @mydate as datetime2 = '20250624 12:34:56.126'
select @mydate as MyDate
```

---
```
select DATEFROMPARTS(2025,06,24) as thisDate
select DATETIME2FROMPARTS(2025,06,24,12,34,56,124,3) as ThatDate
select DATETIME2FROMPARTS(2025,06,24,12,34,56,124,5) as ThatDate
```

---
```
declare @mydate as datetime = '2025-06-24 12:34:56.126'
select year(@mydate) as myYear
, month(@mydate) as myMonth
, day(@mydate) as myDay
```

---
```
declare @mydate as datetime = '2025-06-24 12:34:56.126'
select year(@mydate) as myYear
, month(@mydate) as myMonth
, day(@mydate) as myDay
```

## Quiz 14

Question 1:
I need to store the date and time, and I need accuracy to the nearest minute. Which of these types is definitely NOT suitable?
* datetime
* datetime2
* date
* smalldatetime

Answer: date: because it will not store the time.

---
Question 2:
What is the accuracy of the variable @mydate?
```
DECLARE @mydate AS datetime2
```

Answer: to the nearest 0.0000001th of a second

---

Question 3:
What is the standard format for creating a date?

'YYYY-MM-DD'

## 48. Today's date, and more date functions
```
select CURRENT_TIMESTAMP as RightNow_Ansi
```

**this is Ansi standard**
```
select getdate() as RightNow_MS
```

**this is microsoft proprietary function**
```
select SYSDATETIME() as rightnow
```

**more accurate, because it returns datetime2**

---
```
select dateadd(year,1,'2025-01-02 03:04:05') as myYear
select datepart(hour,'2025-01-02 03:04:05') as myHour
select datename(WEEKDAY, getdate())
select datediff(second, '2025-01-02 03:04:05', getdate()) as SecondsElapsed
select datediff(month, '2025-01-02 03:04:05', getdate()) as SecondsElapsed
```

---

## Quiz 15
Question 1:
Which of these returns the current date and time in the datetime2(7) data type? (Not the datetime format, but datetime2(7) format.)

Answer: sysdatetime()

---
Question 2:
What function can I use to get the hour from the time right now?

Answer:
```
select datepart(hour, sysdatetime())
```

## 50. Converting from date to strings
```
declare @mydate as datetime = '2015-06-25 01:02:03.456'
select 'The date is ' +  @mydate
```

---
```
declare @mydate as datetime = '2015-06-25 01:02:03.456'
select 'The date and time is ' + convert(nvarchar(20), @mydate) as myConvertedDate
```

---
```
declare @mydate as datetime = '2015-06-25 01:02:03.456'
select 'The date and time is ' + cast(@mydate as nvarchar(20)) as myConvertedDate
```

---
```
select convert(date, 'Thursday, 25 June 2015') as MyConvertedDate
```

**will not work**

---
```
select parse('Thursday, 25 June 2015' as date) as MyConvertedDate
select parse('Jueves, 25 de junio de 2015' as date using 'es-ES') as MyConvertedDateSpanish
```

---
```
select format(cast('2025-06-25 01:59:03.456' as datetime),'D') as myFormattedLongDate
select format(cast('2025-06-25 01:59:03.456' as datetime),'d') as myFormattedShortDate
```

---
```
select format(cast('2025-06-25 01:59:03.456' as datetime),'dd-MM-yyyy') as myFormattedBritishDate
```

**note: the MM must be in capitalised, otherwise it will take minutes value**
<img width="1034" height="343" alt="image" src="https://github.com/user-attachments/assets/bfcb17ed-4f76-43fa-a61a-ed0035df74ed" />

---
```
select format(cast('2025-06-25 01:59:03.456' as datetime),'D', 'es-ES') as myFormattedSpanish
select format(cast('2025-06-25 01:59:03.456' as datetime),'D', 'de-DE') as myFormattedGerman
select format(cast('2025-06-25 01:59:03.456' as datetime),'D', 'zh-CN') as myFormattedChinese
```
