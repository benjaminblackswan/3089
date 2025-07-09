# Section 3: Creating tables - First pass

create table tblSecond
(myNumbers int)

create table tblSecond
(myNumbers int);
go

insert into tblSecond values (234)

insert into tblSecond values (678)

insert into [dbo].[tblSecond]
values (456), (156), (478)

## exercise 2
INSERT 
into SportTeams
values ('Wolf FC');

-- Need to end this first command with a semicolon please.

SELECT * FROM SportTeams

---
select myNumbers from tblSecond;

select * from [tblFirst];

## exercise 3

select TeamID as ID, TeamName as Name
from SportTeams

delete from tblFirst

truncate table tblSecond

drop table tblFirst

**Note: you have to collapse the 3089-Burton DB, then click refresh to make tblFirst disappear from the object explorer (OE)**

drop table tblSecond

select * from tblSecond

**Note: refresh local cache to update intellisense, ctrl + shft + R**
