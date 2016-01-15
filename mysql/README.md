##基础：
```C++
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
        create table [Tname] (col_name col_type,...);
        drop table [Tname];
        describe [Tname];
        select */col1,col2,... from [Tname] where coli=[str1];
        insert into [Tname](col1,col2,...) values('v1','v2',...);
        delete from [Tname] where coli=[str2];
        alter table [Tname] add column [col_name] [col_type];
        alter table [Tname] change [old_col] [new_col] [col_type];
        alter table [Tname] drop column [col_ame]
```