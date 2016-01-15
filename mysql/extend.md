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
    创建详细功能表：
        create table students
    	（
    		id int unsigned not null auto_increment primary key,
    		name char(8) not null,
    		sex char(4) not null,
    		age tinyint unsigned not null,
    		tel char(13) null default "-"
    	);
```