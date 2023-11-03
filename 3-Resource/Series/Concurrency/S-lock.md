  
select * from PRODUCT lock in share mode ;  
  
select * from PRODUCT for share ;  
  
> SELECT ... FOR SHARE is a replacement for SELECT ... LOCK IN SHARE MODE, but LOCK IN SHARE MODE remains available for backward compatibility. The statements are equivalent. However, FOR SHARE supports OF table_name, NOWAIT, and SKIP LOCKED options. See Locking Read Concurrency with NOWAIT and SKIP LOCKED.