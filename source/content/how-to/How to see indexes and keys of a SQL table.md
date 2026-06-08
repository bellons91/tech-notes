---
tags:
  - sql
  - sql-server
  - tsql
---
To see the whole picture of a table, including indexes and keys:

```sql
SELECT 
    SCHEMA_NAME(t.schema_id) AS SchemaName,
    t.name as TableName,
    ind.name as IndexName,
    col.name as ColumnName,
    ind.type_desc as IndexType,
    ind.is_primary_key as IsPrimaryKey,
    ic.key_ordinal as KeyOrdinal
FROM sys.indexes ind 
INNER JOIN sys.index_columns ic ON ind.object_id = ic.object_id 
    AND ind.index_id = ic.index_id 
INNER JOIN sys.columns col ON ic.object_id = col.object_id 
    AND ic.column_id = col.column_id 
INNER JOIN sys.tables t ON ind.object_id = t.object_id 
WHERE t.name = '<TABLE-NAME>'
ORDER BY IndexName, ic.key_ordinal
```