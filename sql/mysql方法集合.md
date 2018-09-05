

[mysql 5.5 安装图解](http://blog.csdn.net/lanzhghz100/article/details/50685879)

[MySQL函数](http://www.cnblogs.com/kissdodog/p/4168721.html)

MySQL中的LOCATE和POSITION函数






```sql
# 当前时间
now()
sysdate()
CURDATE()

# 格式化日期 '%Y%m%d%H%i%s'
SELECT date_format(CURDATE(), '%Y-%m-%d');

# 日期加减 month day   hour minute second microsecond week  quarter year
#  date_sub() 日期时间函数 和 date_add() 用法一致
select date_add(@dt, interval 1 day); -- add 1 day


# 两个日期相减 date1 - date2，返回天数   
# 两个日期相减 time1 - time2，返回 time 差值  -- 08:08:08
datediff(date1,date2), timediff(time1,time2)


INSERT INTO  test_book1
    SELECT 1, 'TEST', 'ABC' FROM dual
    WHERE NOT EXISTS( SELECT 1 FROM test_book1 WHERE id = 1);

```