##升级使用
```C++
    修改密码：
        mysqladmin -u[user-name] -p[old-password] password [new-password]
    添加用户：
        grant select,insert,update,deleteon *.* to [username]@localhost identified by\"[password]\";
    显示当前所有用户：
        select user from mysql.user;
    删除用户：
        drop user [username];
    主键
        添加主键： Alter table [Tname] add primary key(col) 
        删除主键： Alter table [Tname] drop primary key(col) 
    索引
        创建索引：create [unique] index [idxname] on [Tname](col….) 
        删除索引：drop index [idxname] 
        注：索引是不可更改的，想更改必须删除重新建。 
    视图
        创建视图：create view [viewname] as select statement 
        删除视图：drop view [viewname] 
    查找：
        select * from table1 where field1 like ’%value1%’ —like的语法很精妙，查资料! 
    排序： 
        select * from table1 order by field1,field2 [desc] 
    总数：
        select count as totalcount from table1 
    求和：
        select sum(field1) as sumvalue from table1 
    平均：
        select avg(field1) as avgvalue from table1 
    最大：
        select max(field1) as maxvalue from table1 
    最小：
        select min(field1) as minvalue from table1 
```