* Master Thread线程拥有最高的线程优先级别。其内部由多个循环（loop）组成,主循环（loop）,后台循环(background loop),刷新循环(flush loop),暂停循环(suspend loop).Master Thread会根据数据库运行状态在各个循环进行切换。

## Master Thread在innodb1.0.x版本之前
* Loop主循环中主要操作为每1秒和每10秒进行的两大操作
* **每1的操作包括：**
* 日志缓冲刷入到磁盘，即使这个事务还没有提交（总是）
* 合并插入缓冲（可能）
* 至多刷新100个缓冲池中的脏页到磁盘（可能）
* 如果当前没有用户活动，切换到background loop(可能)
* **每10秒的操作**
* 刷新100个脏页到磁盘（可能）
* 至多合并5个插入缓冲（总是）
* 将日志缓冲刷入到磁盘（总是）
* 删除无用的Undo页（总是）
* 刷新100个或10个脏页到磁盘（总是）
* **background loop进行的操作**
* 删除无用的Undo页（总是）
* 合并20个插入缓冲（总是）
* 跳回到主循环（总是）
* 不断刷新100个页直到符合条件（可能，跳转到flush loop中完成）
* **若flush loop中也没有什么事情可以做就切换suspend loop，将Master Thread挂起，等待事件的发生**

## Master Thread在innodb1.2.x版本之前
* 从1.0.x版本开始，innodb提供了innodb_io_capacity参数，用来表示磁盘io的吞吐量，默认值200。对于刷新到磁盘页的数量，根据参数innodb_io_capacity的百分比进行控制
* 在合并插入缓冲时，合并插入缓冲的数量为innodb_io_capacity的5%
* 在从缓冲池刷新脏页时，为inndob_io_capacity的设定值
* 参数innodb_adaptive_flushing(自适应地刷新)，该值影响每秒钟刷新脏页的数量
* 参数innodb_purge_batch_size控制每次full purge回收Undo页的数量，之前是每次只回收20个

## Master Thread在innodb1.2.x版本中
* 将Master Thread中的刷新脏页操作分离到一个单独的线程中Page Cleaner Thread线程中
