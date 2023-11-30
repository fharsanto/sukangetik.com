---
title: "Postgresql Vacuum"
date: 2023-11-30T19:50:04+07:00
categories: ["tech/snippets"]
tags: ["snippets", "postgresql"]

---

## When is VACUUM needed
```sql
SELECT 
    relname AS table_name,
    n_live_tup,
    n_dead_tup,
    last_vacuum,
    last_autovacuum
FROM 
    pg_stat_user_tables
WHERE 
    n_dead_tup > (n_live_tup * 0.2);  -- Using 20% as the threshold
```


In this query:

`relname` is the name of the table.  
`n_live_tup` is the number of live tuples (rows) in the table.  
`n_dead_tup` is the number of dead tuples in the table.  
`last_vacuum` shows when the last manual VACUUM was performed on the table.  
`last_autovacuum` shows when the last automatic VACUUM was performed.   

This query will help you identify tables where the proportion of dead tuples to live tuples is high, indicating that a VACUUM might be beneficial. The threshold value (0.2 in this example) can be adjusted based on your database's performance and maintenance needs.