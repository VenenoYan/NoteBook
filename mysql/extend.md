##升级使用
```C++
    修改密码：
        mysqladmin -u[user-name] -p[old-password] password [new-password]
    添加用户：
        grant select,insert,update,deleteon *.* to [username]@localhost identified by\"[password]\";        
```