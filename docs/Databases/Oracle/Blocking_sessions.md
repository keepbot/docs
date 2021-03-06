
### Find all locking sessions
```
SELECT * FROM v$lock;
```

### View all blocking sessions ver.1
```
SELECT s.blocking_session, s.sid, s.serial#, s.seconds_in_wait FROM v$session s WHERE blocking_session IS NOT NULL;
```

### View all blocking sessions ver.2
```
SELECT s1.username || '@' || s1.machine
    || ' ( SID=' || s1.sid || ' )  is blocking '
    || s2.username || '@' || s2.machine || ' ( SID=' || s2.sid || ' ) ' AS blocking_status
    FROM v$lock l1, v$session s1, v$lock l2, v$session s2
    WHERE s1.sid=l1.sid AND s2.sid=l2.sid
    AND l1.BLOCK=1 AND l2.request > 0
    AND l1.id1 = l2.id1
    AND l1.id2 = l2.id2;
```

### View SID and ID of blocking sessions
```
SELECT sid, id1 FROM v$lock WHERE TYPE='TM';
```

### View the name of blocking session
```
SELECT object_name FROM dba_objects WHERE object_id=101482;
```

### Kill session: " ALTER SYSTEM KILL SESSION 'SID,ID' "
```
ALTER SYSTEM KILL SESSION '1621,24543';
```

### View all active sessions
```
SELECT s.inst_id,
       s.sid,
       s.serial#,
       p.spid,
       s.username,
       s.program
FROM   gv$session s
       JOIN gv$process p ON p.addr = s.paddr AND p.inst_id = s.inst_id
WHERE  s.type != 'BACKGROUND';
```
