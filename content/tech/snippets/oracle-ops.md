---
title: "Oracle Operations"
date: 2023-07-09T20:19:30+07:00
categories: ["tech/snippets"]
tags: ["snippets", "oracle"]
# draft: true
toc:
  auto: true
---

Discover what the issue in oracle day to day operations
<!--more-->

## Oracle Long Operations
```sql
COLUMN percent FORMAT 999.99 
SELECT sid, to_char(start_time,'hh24:mi:ss') stime, 
message,( sofar/totalwork)* 100 percent 
FROM v$session_longops
WHERE sofar/totalwork < 1
/
```

## Oracle query Locking
```sql
select
  object_name, 
  object_type, 
  session_id, 
  type,         -- Type or system/user lock
  lmode,        -- lock mode in which session holds lock
  request, 
  block, 
  ctime         -- Time since current mode was granted
from
  v$locked_object, all_objects, v$lock
where
  v$locked_object.object_id = all_objects.object_id AND
  v$lock.id1 = all_objects.object_id AND
  v$lock.sid = v$locked_object.session_id
order by
  session_id, ctime desc, object_name
/
```

## Oracle check active query
```sql
select S.USERNAME, s.sid, s.osuser, t.sql_id, sql_text
from v$sqltext_with_newlines t,V$SESSION s
where t.address =s.sql_address
and t.hash_value = s.sql_hash_value
and s.status = 'ACTIVE'
and s.username <> 'SYSTEM'
order by s.sid,t.piece
/
```

## Oracle check process user
```sql
SELECT sess.process, sess.status, sess.username, sess.schemaname, sql.sql_text FROM v$session sess, v$sql sql
WHERE sql.sql_id(+) = sess.sql_id
AND sess.type = 'USER'
/
```

## Oracle gather stats
```sql
begin
    dbms_stats.gather_fixed_objects_stats;
    dbms_stats.gather_dictionary_stats;
end;
/
```