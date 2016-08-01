####1. 复制相关
众所周知，MySQL**只支持一对多的主从复制**，而不支持多主（multi-master）复制（MySQL使用多主复制时，需要修改自增长变量参数）。 MySQL 5.1 中，在复制方面的改进就是引进了新的复制技术：基于行的复制。
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

####3. 

####4. 

####5. 

####6. 

####7. 

####8. 

####9. 

####10. 

####11. 

####12. 

####13. 

####14. 

####15. 
