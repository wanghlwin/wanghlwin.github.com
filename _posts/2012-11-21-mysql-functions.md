---
layout: page
title: "Mysql 中一些常用函数 "
category: mysql
tags: [mysql , function , 函数]
description: 
---

# 一.字符串类 
{% highlight javascript %} 
CHARSET(str) //返回字串字符集
CONCAT (string2  [,... ]) //连接字串
INSTR (string ,substring ) //返回substring首次在string中出现的位置,不存在返回0
LCASE (string2 ) //转换成小写
LEFT (string2 ,length ) //从string2中的左边起取length个字符
LENGTH (string ) //string长度
LOAD_FILE (file_name ) //从文件读取内容
LOCATE (substring , string  [,start_position ] ) 同INSTR,但可指定开始位置
LPAD (string2 ,length ,pad ) //重复用pad加在string开头,直到字串长度为length
LTRIM (string2 ) //去除前端空格
REPEAT (string2 ,count ) //重复count次
REPLACE (str ,search_str ,replace_str ) //在str中用replace_str替换search_str
RPAD (string2 ,length ,pad) //在str后用pad补充,直到长度为length
RTRIM (string2 ) //去除后端空格
STRCMP (string1 ,string2 ) //逐字符比较两字串大小,
SUBSTRING (str , position  [,length ]) //从str的position开始,取length个字符
{% endhighlight%}
 
# 二.数学类
{% highlight javascript %} 
ABS (number2 ) //绝对值
BIN (decimal_number ) //十进制转二进制
CEILING (number2 ) //向上取整
CONV(number2,from_base,to_base) //进制转换
FLOOR (number2 ) //向下取整
FORMAT (number,decimal_places ) //保留小数位数
HEX (DecimalNumber ) //转十六进制
注：HEX()中可传入字符串，则返回其ASC-11码，如HEX('DEF')返回4142143
也可以传入十进制整数，返回其十六进制编码，如HEX(25)返回19
LEAST (number , number2  [,..]) //求最小值
MOD (numerator ,denominator ) //求余
POWER (number ,power ) //求指数
RAND([seed]) //随机数
ROUND (number  [,decimals ]) //四舍五入,decimals为小数位数]
{% endhighlight%} 
 
# 三.日期时间类
{% highlight javascript %} 
ADDTIME (date2 ,time_interval ) //将time_interval加到date2
CONVERT_TZ (datetime2 ,fromTZ ,toTZ ) //转换时区
CURRENT_DATE (  ) //当前日期
CURRENT_TIME (  ) //当前时间
CURRENT_TIMESTAMP (  ) //当前时间戳
DATE (datetime ) //返回datetime的日期部分
DATE_ADD (date2 , INTERVAL d_value d_type ) //在date2中加上日期或时间
DATE_FORMAT (datetime ,FormatCodes ) //使用formatcodes格式显示datetime
DATE_SUB (date2 , INTERVAL d_value d_type ) //在date2上减去一个时间
DATEDIFF (date1 ,date2 ) //两个日期差
DAY (date ) //返回日期的天
DAYNAME (date ) //英文星期
DAYOFWEEK (date ) //星期(1-7) ,1为星期天
DAYOFYEAR (date ) //一年中的第几天
EXTRACT (interval_name  FROM date ) //从date中提取日期的指定部分
MAKEDATE (year ,day ) //给出年及年中的第几天,生成日期串
MAKETIME (hour ,minute ,second ) //生成时间串
MONTHNAME (date ) //英文月份名
NOW (  ) //当前时间
SEC_TO_TIME (seconds ) //秒数转成时间
STR_TO_DATE (string ,format ) //字串转成时间,以format格式显示
TIMEDIFF (datetime1 ,datetime2 ) //两个时间差
TIME_TO_SEC (time ) //时间转秒数]
WEEK (date_time [,start_of_week ]) //第几周
YEAR (datetime ) //年份
DAYOFMONTH(datetime) //月的第几天
{% endhighlight%}