## 64. Adding a second table

**go to tblEpmloyee, script table as**
<img width="975" height="468" alt="image" src="https://github.com/user-attachments/assets/3b97d30e-61d3-4429-b17a-3dc57f740c38" />
```
CREATE TABLE [dbo].[tblEmployee](
	[EmployeeNumber] [int] NOT NULL,
	[EmployeeFirstName] [varchar](50) NOT NULL,
	[EmployeeMiddleName] [varchar](50) NULL,
	[EmployeeLastName] [varchar](50) NOT NULL,
	[EmployeeGovID] [char](10) NULL,
	[DateOfBirth] [date] NULL,
	[department] [varchar](20) NULL
) ON [PRIMARY]
GO
```

## 65. Designing a connection
```
create table tblTransaction (
Amount smallmoney not null,
DateOfTransaction smalldatetime null,
EmployeeNumber int not null)
```
