---
tags:
  - database
  - sql
  - tsql
---
## Use a variable as a scalar value (like varchar)

```sql
DECLARE @DefaultValue NVarChar(30) = 'My Value'

SELECT whatever 
FROM somewhere 
WHERE value = @DefaultValue
```


## Use a variable to store list of values

This query is useful if you want to use the `IN` operator

```sql
DECLARE @SearchedCodes table(Node NVARCHAR(Max) )
Insert
	into
	@SearchedCodes
values ('AA'),
('BB'),
('CC'),
('DD')


SELECT whatever 
FROM somewhere 
WHERE value IN (SELECT Node from @SearchedCodes))
```