####1. 复制相关
众所周知，MySQL**只支持一对多的主从复制**，而不支持多主（multi-master）复制。 
* 
在有多个slave参与的半同步复制中，master并不一定需要等待全部slave返回
* 
MySQL使用多主复制时，需要修改自增长变量参数,所以有人认为不支持。
* 
一般情况下，异步复制的性能比半同步复制好，但后者相对更为安全<br>
**基于行的复制** MySQL 5.1 中，在复制方面的改进就是引进了新的复制技术.基于行的复制。
简言之，这种新技术就是关注表中发生变化的记录，而非以前的照抄** binlog 模式**。<br>
从 MySQL 5.1.12 开始，可以用以下三种模式来实现：
* 
基于SQL语句的复制(statement-based replication, SBR)，
* 
基于行的复制(row-based replication, RBR)，
* 
混合模式复制(mixed-based replication, MBR)。<br>
相应地，binlog的格式也有三种：STATEMENT，ROW，MIXED。 MBR 模式中，SBR 模式是默认的。<br>
**Mysql复制分成三步：** 
* 
master将改变记录到二进制日志(binary log)中（这些记录叫做二进制日志事件，binary log events）； 
* 
slave将master的binary log events拷贝到它的中继日志(relay log)； 
* 
slave重做中继日志中的事件，将改变反映它自己的数据。

####3. 事务：
是一系列的数据库操作，是数据库应用的基本逻辑单位。性质：
* 
原子性。即不可分割性，事务要么全部被执行，要么就全部不被执行。
* 
一致性。事务的执行使得数据库从一种正确状态转换成另一种正确状态
* 
隔离性。在事务正确提交之前，不允许把该事务对数据的任何改变提供给任何其他事务，
* 
持久性。事务正确提交后，其结果将永久保存在数据库中，即使在事务提交后有了其他故障，事务的处理结果也会得到保存。

####4. 三范式：
* 
1NF:每个属性是不可分的。 
* 
2NF:若关系R是１NF,且每个非主属性都完全函数依赖于R的键。例SLC(SID#, CourceID#, SNAME,Grade),则不是2NF; 
* 
3NF:若R是2NF，且它的任何非键属性都不传递依赖于任何候选键。

####5.  完整性约束：
* 
实体完整性
* 
参照完整性
* 
用户定义完整性

####6. 索引作用

####7. 内联接,外联接区别？
* 
内连接是保证两个表中所有的行都要满足连接条件，而外连接则不然。
* 
在外连接中，某些不满条件的列也会显示出来，也就是说，只限制其中一个表的行，而不限制另一个表的行。分左连接、右连接、全连接三种

####8. 锁：共享锁、互斥锁
两段锁协议：阶段１：加锁阶段 阶段２：解锁阶段

####9. 死锁及处理：事务循环等待数据锁，则会死锁。

死锁处理：预防死锁协议，死锁恢复机制

####10. 视图

####11. 

####12. 

####13. 

####14. 

####15. 