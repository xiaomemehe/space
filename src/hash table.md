# 哈希表--散列表
* 是根据关键码值(Key value)而直接进行访问的数据结构
* 哈希表是一种通过**哈希函数**将特定的键映射到特定值的一种数据结构，他维护者键和值之间一一对应关系。
## 涉及概念
* 键(key)：又称为关键字。唯一的标示要存储的数据，可以是数据本身或者数据的一部分。
* 槽(slot/bucket)：哈希表中用于保存数据的一个单元，也就是数据真正存放的容器。
* 哈希函数(hash function)：将键(key)映射(map)到数据应该存放的槽(slot)所在位置的函数。
* 哈希冲突(hash collision)：哈希函数将两个不同的键映射到同一个索引的情况。

## 哈希冲突
#### 存在多个不同键值，通过哈希函数，映射到相同的slot。
1. **Open Hash拉链法**
* 名词解释：叫拉链，是因为哈希冲突后，用**链表**去**延展**来解决。
* 将这几个映射到相同slot的**键值**，通过链表存于slot下。
* 用链表延展去存储同键值的数据。
* **优点**
* 拉链法处理冲突简单，且**无堆积现象**，即非同义词决不会发生冲突，因此平均查找长度较短
* 在用拉链法构造的散列表中，**删除结点**的操作易于实现
* **缺点**
* 在对链表进行**存储空间分配**的时候，会降低整个程序的运行速率
2. **Close Hash 开放地址法 （Open Addressing）**
* 名词解释：叫Closed，是因为哈希冲突后，并**不会**在本身之外开拓新的空间，而是继续**顺延下去**某个位置来存放，所以是一个密闭的空间，所以叫“Closed”，
至于**开地址（Open Addressing）**，这个应该相对于那种通过**链表**来**开拓新空间**，它是在**本身地址上**，另外找个位置。所以叫开地址。
2.1 **Bucket Hashing哈希桶**
* 建立多个hash桶，每个桶里存放多个slot
* 存入数据时，如果发生冲突，即桶里的存在不为空的slot，继续往下存
* 当桶中的slot被在满时，把数据放到overflow里面（overflow可能为一个普通的链表）
* **查找**时，先顺序查找bucket中的，如果没有，查找overflow中的
2.2 **Probing探测** --nodone



From: <a href="https://www.jianshu.com/p/dbe7a1ea5928">HashTable</a>