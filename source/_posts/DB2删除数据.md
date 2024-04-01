
# 一次删除N条数据d 

```SQL
delete from table where id in (select id from table where info = '1' order by id fetch first 1 rows only)
```

# 删除数据不记录日志

[删除数据时不记录日志正确方式](https://www.cnblogs.com/OliverQin/p/10219108.html)

## 临时方法

```SQL
db2 connect to db
db2 +c "ALTER TABLE name activate NOT LOGGED initially"
db2 +c "delete from table where id in (select id from table where info = '1' order by id fetch first 1 rows only)"
db2 commit;
```
