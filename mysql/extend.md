##升级使用
```C++
    修改密码：
        1)终端：mysqladmin -u[user-name] -p[old-password] password [new-password]
        2)mysql环境：set password for [username]@[host]=password('new password')  修该某一用户
                set password=password('new password')       修该当前用户
    添加用户：
        grant [select,insert,update,delete] on [DB].[T] to [username]@[host] identified by [p-word]
        即：
            新建用户：create user [username]@[host] identified by [password]
            授权：grant [privileges] on [DBname].[Tname] to [username]@[host]
        注：
            username   用户名
            host       指定用户从那个主机登陆(本机：localhost)
            password   用户密码
            privileges  允许该用户的操作如select、update等（all 代表所有操作都允许）
            DBname/Tname  允许访问的数据库和表（*.*即所有都可以）
            可以用通配符  
    显示当前所有用户：
        select user from mysql.user;
    显示
    撤销授权：
        revoke [privileges] on [DBname].[Tname] from [username]@[host];
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
        select * from table1 order by field1,field2 [desc/asc] 
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
一些好的实例：
```C++
    1、复制表(只复制结构,源表名：a 新表名：b) (Access可用) 
        法一：select * into b from a where 1<>1 
        法二：select top 0 * into b from a 
    2、拷贝表(拷贝数据,源表名：a 目标表名：b) (Access可用) 
        insert into b(a, b, c) select d,e,f from b; 
    3、跨数据库之间表的拷贝(具体数据使用绝对路径) (Access可用) 
        insert into b(a, b, c) select d,e,f from b in ‘具体数据库’ where 条件 
        例子：..from b in ‘"&Server.MapPath(".")&"\data.mdb" &"’ where.. 
    4、子查询(表名1：a 表名2：b) 
        1)select a,b,c from a where a IN (select d from b )
        2)select a,b,c from a where a IN (1,2,3) 
    5、显示文章、提交人和最后回复时间 
        select a.title,a.username,b.adddate from table a,(select max(adddate) adddate from table 
            where table.title=a.title) b 
    6、外连接查询(表名1：a 表名2：b) 
        select a.a, a.b, a.c, b.c, b.d, b.f from a LEFT OUT JOIN b ON a.a = b.c 
    7、在线视图查询(表名1：a ) 
        select * from (SELECT a,b,c FROM a) T where t.a > 1; 
    8、between的用法,between限制查询数据范围时包括了边界值,not between不包括 
        select * from table1 where time between time1 and time2 
        select a,b,c, from table1 where a not between 数值1 and 数值2 
    9、in 的使用方法 
        select * from table1 where a [not] in (‘值1’,’值2’,’值4’,’值6’) 
    10、两张关联表，删除主表中已经在副表中没有的信息 
        delete from table1 where not exists ( select * from table2 where 
                table1.field1=table2.field1 ) 
    11、四表联查问题： 
        select * from a left inner join b on a.a=b.b right inner join c on a.a=c.c inner join d 
            on a.a=d.d where ….. 
    12、日程安排提前五分钟提醒 
        select * from 日程安排 where datediff(’minute’,f开始时间,getdate())>5 
    13、一条sql 语句搞定数据库分页 
        select top 10 b.* from (select top 20 主键字段,排序字段 from 表名 order by 排序字段 desc)
        a,表名 b where b.主键字段 = a.主键字段 order by a.排序字段 
    14、前10条记录 
        select top 10 * form table1 where 范围 
    15、选择在每一组b值相同的数据中对应的a最大的记录的所有信息(类似这样的用法可以用于论坛每月排行榜,
    每月热销产品分析,按科目成绩排名,等等.) 
        select a,b,c from tablename ta where a=(select max(a) from tablename tb where tb.b=ta.b) 
    16、包括所有在 TableA 中但不在 TableB和TableC 中的行并消除所有重复行而派生出一个结果表 
        (select a from tableA ) except (select a from tableB) except (select a from tableC) 
    17、随机取出10条数据 
        select top 10 * from tablename order by newid() 
    18、随机选择记录 
        select newid() 
    19、删除重复记录 
        Delete from tablename where id not in (select max(id) from tablename group by col1,col2,…) 
    20、列出数据库里所有的表名 
        select name from sysobjects where type=’U’ 
    21、列出表里的所有的 
        select name from syscolumns where id=object_id(’TableName’) 
    22、列示type、vender、pcs字段，以type字段排列，case可以方便地实现多重选择，类似select 中的case。 
        select type,sum(case vender when ‘A’ then pcs else 0 end),sum(case vender when ‘C’ then 
        pcs else 0 end),sum(case vender when ‘B’ then pcs else 0 end) FROM tablename group by type 
            显示结果： 
            type vender pcs 
            电脑 A 1 
            电脑 A 1 
            光盘 B 2 
            光盘 A 2 
            手机 B 3 
            手机 C 3 
    23、初始化表table1 
        TRUNCATE TABLE table1 
    24、选择从10到15的记录 
        select top 5 * from (select top 15 * from table order by id asc) T_别名 order by id desc 
```