##基础：
```C++
MySQL 为关系型数据库(Relational Database Management System), 这种所谓的"关系型"可以理解为"表格"的概念, 
        一个关系型数据库由一个或数个表格组成
不区分大小写
SQL语句分为两种：DML（Data Manipulation Language）与DDL(Data Definition Language)
    1、DML
        select、update、delete、insert into
    2、DDL
        create database、alter database、create table、alter table、alter table、drop table
算术操作符：
    +、-、/、*、%、|、^、&、<<、>>
比较操作符：
    =、>、<、<=、>=、！= 
逻辑操作符：
    not、！     or、||      XOR         and、&&
数据类型：
    1)算术：
        tinyint、smallint、mediumint、int、bigint、float(M,D)、double(M,D)、decimal(M,D)
            MySQL数据类型	    含义（有符号）
            tinyint(m)	     1个字节  范围(-128~127)
            smallint(m)	    2个字节  范围(-32768~32767)
            mediumint(m)	   3个字节  范围(-8388608~8388607)
            int(m)	         4个字节  范围(-2147483648~2147483647)
            bigint(m)	      8个字节  范围(+-9.22*10的18次方)
            float(m,d)	    单精度浮点型    8位精度(4字节)     m总个数，d小数位
            double(m,d)	   双精度浮点型    16位精度(8字节)    m总个数，d小数位
            decimal(m,d)      参数m<65 是总个数，d<30且 d<m 是小数位。
    2)文本：
        char、varchar、tinyblob、blob、mediumblob、longblob、enum、set
    3)时间：
        date、datetime、time、timestamp、year
    4)字符：
        bit、string、boolean、Null、hexadecimal、decimal
基本操作：
    登录：
        mysql -u[user-name] -p[password]
    修改密码：
        mysqladmin -u[user-name] -p[old-password] password [new-password]
    数据库：
        show databases;
        create database [DBname];
        use [DBname];
        drop [DBname];
        rename database [olddbname] to [newdbname]
    表：
        show tables;
        create table [Tname] (col_name col_type,...) ENGINE=InnoDB DEFAULT CHARSET=gbk;
        drop table [Tname];
        describe [Tname];
        select */col1,col2,... from [Tname] where coli=[str1] and colj=[str2];
        insert into [Tname](col1,col2,...) values('v1','v2',...);
        update [Tname] set coli=[str1] where colj=[str2];
        delete from [Tname] where coli=[str2];
        alter table [Tname] add column [col_name] [col_type];
        alter table [Tname] change [old_col] [new_col] [col_type];
        alter table [Tname] drop column [col_ame]
```