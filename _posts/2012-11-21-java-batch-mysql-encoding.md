---
layout: page
title: "关于Java调用批处理命令向mysql导入数据的中文乱码问题"
category: mysql
tags: [mysql,批处理,java,bat,乱码]
description: 
---

最近写了个很没意思的小工具，写到一半的时候发现，mysql的可视化工具里面有可以导入excel文件的工具。不过步骤太多不适合不懂sql的人使用，由此，还是将写到一半的小工具给完成了吧，此工具对于懂代码的人来说没有任何的意义，因为你完全可以使用工具来做。我之所以写这个工具姑且说是一个平台吧，由于要让公司销售渠道上的人来使用，他不需要懂代码，也不需要操作这么繁琐的mysql工具。 
半天没有进入正题，大体的说一下它的功能吧，就是把excel中的内容插入到数据库中（Mysql）。 渠道人员在平台上上传excel文件，并选择要导入的表，和表中的哪些列（当然这些列的顺序可以自己随意的调整）。平台就可以自动的为他将excel中的内容插入到所选表的所选列中，同时生成sql文件。 
平台的内部实现，其实是先将excel中的内容拼接成sql语句，并写入到硬盘的sql文件中去，再由Java来调用批处理命令来执行导入刚才生成的sql文件。调用批处理的代码如下： 

public void executeSql(String sqlFilePath) throws IOException{ 
String command = &quot;cmd  /c  mysql -urichmobi -prichmobi heima_2012_3 &lt; d:\\sql_Output.sql&quot;; 
Runtime.getRuntime().exec(command); 
} 

但是中途遇到一个问题，我在第一步将excel中的内容生成sql语句的时候，采用的编码都是utf-8的，我的mysql数据库编码也是utf-8,sql语句中的内容也大多都是中文的，想着应该没有问题。但是问题发生了，在导入完成后发现库中的内容都为乱码，很郁闷。。不都是utf-8的吗。一时间不知道是哪里出了问题。各种百度谷歌也没查到，于是乎想起来这个命令 ：set names utf8; 于是乎就ok了。暂时的解决方案就是 ：“set names utf8;”作用只是临时的，在mysql 重启以后就会恢复默认，所以为了不让乱码有机可乘，最好每次对数据库写中文的时候加上这句话。