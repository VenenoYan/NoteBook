MySQL 5.1 中，在复制方面的改进就是引进了新的复制技术：基于行的复制。
简言之，这种新技术就是关注表中发生变化的记录，而非以前的照抄 binlog 模式.<br>
从 MySQL 5.1.12 开始，可以用以下三种模式来实现：
-- 基于SQL语句的复制(statement-based replication, SBR)，
-- 基于行的复制(row-based replication, RBR)，
-- 混合模式复制(mixed-based replication, MBR)。
相应地，binlog的格式也有三种：STATEMENT，ROW，MIXED。 MBR 模式中，SBR 模式是默认的。