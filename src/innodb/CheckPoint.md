* 缓冲池的设计是为了提高CPU速度和磁盘速度之间的鸿沟。因此页的操作都是在缓冲池中完成的。如果一条DML语句，如update或delete改变了页中的记录，那么此时页是脏的，即缓冲池中的页的版本要比磁盘中的新。数据库需要将新版本的页从缓冲池刷新到磁盘。
## CheckPoint（检查点）技术的目的是为了解决以下几个问题：
1. 缩短数据库的恢复时间
2. 缓冲池不够用时，将脏页刷新到磁盘
3. 重做日志不可用时，刷新脏页
* 当数据库发生宕机时，数据库不需要重做所有的日志，因为CheckPoint之前的页都已经刷新回磁盘。故只需要将CheckPoint之后的重做日志进行恢复。
* 此外，当缓冲池不够用时，根据LRU算法会溢出最近最少使用的页，若此页为脏页，那么需要强制执行CheckPoint，将脏页也就是页的新版本刷回磁盘。
## Innodb引擎内部，存在两个CheckPoint，分别是：
#### Sharp CheckPoint
* Sharp CheckPoint发生在数据库关闭时将所有的脏页都刷新回磁盘，这是默认的工作方式，即参数innodb_fast_shutdown=1
* 如果在数据库运行时也使用Sharp CheckPoint，那么数据库的可用性就会受到很大的影响。故在Innodb存储引擎内部使用Fuzzy CheckPoint进行页的刷新，即只刷新一部分脏页，而不是刷新所有的脏页回磁盘。
#### Fuzzy CheckPoint
1. Master Thread CheckPoint
* 以每秒或每十秒的速度从缓冲池的脏页列表刷新一定比例的页回磁盘。这个过程是异步的，即此时Innodb存储引擎可以进行其他的操作，用户查询线程不会阻塞。
2. FLUSH_LRU_LIST CheckPoint
* 由于Innodb存储引擎需要保证LRU列表中差不多100个空闲页可供使用。在Innodb1.1.x版本之前，需要检查LRU列表中是否有足够的可用空间操作发生在用户查询线程中，显然这会阻塞用户的查询操作。如果没有100个空闲页，那么Innodb会将列表尾部的页移除。假如被移除的页中存在脏页，需要进行CheckPoint操作，而这些页来自LRU列表，因此被称为FLUSH_LRU_LIST CheckPoint
* 而从Mysql5.6版本，也就是Innodb1.2.x版本开始，这个检查被放在了一个单独的Page Cleaner线程中进行，并且用户可以通过参数innodb_lru_scan_depth控制列表中可用页的数量，默认为1024
3. Async/sync Flush ChcekPoint
* 此方式指的是重做日志文件不可用的情况，这时需要强制将一些页刷新回磁盘，而此时脏页是从脏页列表中选取的。
4. Dirty Page too much CheckPoint


