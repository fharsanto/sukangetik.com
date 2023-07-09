---
title: "SQL Server: Create/Drop Scripts for existing FK"
date: 2023-07-09T18:47:42+07:00
categories: ["tech/snippets"]
tags: ["snippets", "mssql"]
# draft: true
---

## Create FK
```sql
SELECT  'ALTER TABLE ' + SCHEMA_NAME(F.schema_id) + '.'
        + OBJECT_NAME(F.parent_object_id) + ' ADD CONSTRAINT ' + F.name
        + ' FOREIGN KEY ' + '(' + COL_NAME(FC.parent_object_id, FC.parent_column_id) + ')'
        + ' REFERENCES ' + SCHEMA_NAME(RefObj.schema_id) + '.'
        + OBJECT_NAME(F.referenced_object_id) + ' ('
        + COL_NAME(FC.referenced_object_id, FC.referenced_column_id) + ')'
FROM    SYS.FOREIGN_KEYS AS F
        INNER JOIN SYS.FOREIGN_KEY_COLUMNS AS FC ON F.OBJECT_ID = FC.constraint_object_id
        INNER JOIN sys.objects RefObj ON RefObj.object_id = f.referenced_object_id
--WHERE   OBJECT_NAME(F.PARENT_OBJECT_ID) = 'YourObjectName'
```

## Drop FK
```sql
SELECT  'ALTER TABLE ' + SCHEMA_NAME(F.schema_id) + '.'
        + OBJECT_NAME(F.parent_object_id) + ' DROP CONSTRAINT ' + F.name + ';'
FROM    SYS.FOREIGN_KEYS AS F
        INNER JOIN SYS.FOREIGN_KEY_COLUMNS AS FC ON F.OBJECT_ID = FC.constraint_object_id
--WHERE   OBJECT_NAME(F.PARENT_OBJECT_ID) = 'YourObjectName'
```


[Original Sources](http://connectsql.blogspot.com/2011/05/sql-server-createdrop-scripts-for-all.html)