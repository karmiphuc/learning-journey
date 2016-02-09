---
layout: post
---
MySQL có lưu lại timestamp access của từng bảng trong 1 schema :O Hơi bị đã, nhưng chỉ hỗ trợ MyISAM, còn InnoDB thì phải dùng trick.

```sql
    SELECT table_schema,
      table_name,
      update_time as LastAccessed
    FROM information_schema.tables
    WHERE table_schema = 'scheme_name'
    AND table_name LIKE '%temp\_survey%'
    AND DATE_ADD(update_time, INTERVAL +1 month) < CURDATE()
    ORDER BY update_time DESC
```