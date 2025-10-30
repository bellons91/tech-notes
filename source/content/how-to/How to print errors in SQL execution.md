---
tags:
  - database
  - sql
---

```sql
PRINT 'An error occurred at line ' + CAST(ERROR_LINE() AS varchar(20)) + ': ' + ERROR_MESSAGE();
```