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
        添加主键： Alter table tabname add primary key(col) 
        删除主键： Alter table tabname drop primary key(col) 
    索引
        创建索引：create [unique] index idxname on tabname(col….) 
        删除索引：drop index idxname 
        注：索引是不可更改的，想更改必须删除重新建。 
    视图
        创建视图：create view viewname as select statement 
        删除视图：drop view viewname 
```