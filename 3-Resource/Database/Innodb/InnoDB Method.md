---
date: 2024-04-27 23:11:42+4360
updatedAt: 2024-04-27 23:14:02+1880
---
## index_read()

```cpp
int ha_innobase::index_read(
    uchar * buf,
    const uchar * key_ptr,
    uint key_len,
    ha_rkey_function find_flag
) override virtual
```
Positions an index cursor to the index specified in the handle.
Fetches the row if any.
### Returns
- `0`,`HA_ERR_KEY_NOT_FOUND` or error number

### Parameters
- `buf` (in/out): buffer for the returned row
- `key_ptr` (in): key value; if this is NULL we position the cursor at the start or end of index; this can also contain an InnoDB row id, in which case `key_len` is the InnoDB row id length; the key value can also be a prefix of a full key value, and the last column can be a prefix of a full column
- `key_len` (in): key value length
- `find_flag` (in): search flags from `my_base.h`