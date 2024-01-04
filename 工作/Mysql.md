 **添加主键**
```mysql 
-- 已有字段
alter table [tablename] add constraint primary key (col);
-- 新增主键字段
alter table [tablename] add [col] [type] primary key auto_increment;
```

 **时间格式转换**
```mysql
-- 字符串转时间
select str_to_date('2023-10-23 00:00:00','%Y-%m-%d %H-%i:%s')

-- 时间转字符串
select date_format(now(),'%Y-%m-%d %H-%i:%s')

-- 秒转时间
select sec_to_time(111)

-- unix转时间(秒)
select from_unixtime(1704184169)

-- 时间转unix(秒)
select unix_timestamp(now())

-- 时间差 second/minute/hour/day
select timestampdiff(second,[start],[end])
```
 
 




