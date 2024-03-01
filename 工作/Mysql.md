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
 
 查所有周的起止日期
 ```mysql
 insert into weeklydata (id,week_dates)  
select  
t.datai,t.ranger  
from (  
SELECT  
datai,  
concat(date_format(DATE_FORMAT(DATE_ADD('2023-01-01', INTERVAL week_number * 7 DAY), '%Y-%m-%d') - INTERVAL weekday('2023-01-01') DAY,'%Y%m%d'),'-',  
date_format((DATE_FORMAT(DATE_ADD('2023-01-01', INTERVAL week_number * 7 DAY), '%Y-%m-%d')) + INTERVAL 6 DAY - INTERVAL weekday('2023-01-01') DAY,'%Y%m%d')) as ranger,  
DATE_FORMAT(DATE_ADD('2023-01-01', INTERVAL week_number * 7 DAY), '%Y-%m-%d') - INTERVAL weekday('2023-01-01') DAY AS start_date  
FROM  
(  
with recursive c(week_number,datai) as (select 0,concat(date_format(DATE_ADD('2023-01-01',interval 0 * 7 DAY) - INTERVAL weekday('2023-01-01') DAY + INTERVAL 6 DAY,'%Y'),week(DATE_ADD('2023-01-01',interval 0 * 7 DAY) - INTERVAL weekday('2023-01-01') DAY + INTERVAL 6 DAY))  
from dual  
union all  
select week_number + 1,concat(date_format(DATE_ADD('2023-01-01',interval (week_number+1) * 7 DAY) - INTERVAL weekday('2023-01-01') DAY + INTERVAL 6 DAY,'%Y'),week(DATE_ADD('2023-01-01',interval (week_number+1) * 7 DAY) - INTERVAL weekday('2023-01-01') DAY + INTERVAL 6 DAY))  
from c  
where week_number < 350)  
select *  
from c) AS weeks where  
DATE_FORMAT(DATE_ADD('2023-01-01', INTERVAL week_number * 7 DAY), '%Y-%m-%d') <= LAST_DAY('2028-12-31')  
ORDER BY  
start_date  
) t
```



