## 基本查询方法
* db.COLLECTION_NAME.find()   非结构化显示
* db.col.find().pretty()    格式化显示
### 比较
操作|格式|范例|RDBMS中的类似语句
--|:--:|:--:|--:
等于|{\<key\>:\<value\>}|db.col.find({"name":"w3cschool"}).pretty()|where name = 'w3cschool'
小于|{\<key\>:{$lt:\<value\>}}|db.col.find({"price":{$lt:50}}).pretty()|where price < 50
小于或等于|{\<key\>:{$lte:\<value\>}}|db.col.find({"price":{$lte:50}}).pretty()|where price <= 50
大于|{\<key\>:{$gt:\<value\>}}|db.col.find({"price":{$gt:50}}).pretty()|where price>50
大于等于|{\<key\>:{$gte:\<value\>}}|db.col.find({"price":{$gte:50}}).pretty()|where price >= 50
不等于|{\<key\>:{$ne:\<value\>}}|db.col.find({"price":{$ne:50}}).pretty()|where price != 50
### AND&&OR
* db.col.find({key1:value1, key2:value2}).pretty()
* db.col.find({$or: [{key1: value1}, {key2:value2}]}).pretty()
* db.col.find({"likes": {$gt:50}, $or: [{"by": "w3cschool"},{"title": "MongoDB 教程"}]}).pretty()
### 清空
* db.col.remove({})
###  $type 操作符
* db.col.find({"title" : {$type : 2}})
* **type值**
1. double  1
2. string 2
3. object 3
4. array 4
5. binary data 5
6. Object id 7
7. boolean 8
8. Date 9 
9. Null 10
10. Timestamp 17
11. Min key 255
12. Max key 127

### Limit && Skip
* db.COLLECTION_NAME.find().limit(NUMBER).skip(NUMBER)
### 排序Sort
* db.COLLECTION_NAME.find().sort({KEY:1})  //1升序 -1降序

# 索引
* 使用ensureIndex来创建索引
* db.COLLECTION_NAME.ensureIndex({KEY:1}) //语法中 Key 值为你要创建的索引字段，1为指定按升序创建索引，如果你想按降序来创建索引指定为-1即可
* db.mycol.ensureIndex({"title":1,"description":-1}) //复合索引
* db.values.ensureIndex({open: 1, close: 1}, {background: true}) //存在可选参数

### 聚合 aggregate()

表达式|描述|范例
--|:--:|--:
$sum  |计算总和。|   db.mycol.aggregate({$group : {_id : "$by_user", num_tutorial : {$sum : "$likes"}}})
$avg  |计算平均值 |  db.mycol.aggregate({$group : {_id : "$by_user", num_tutorial : {$avg : "$likes"}}})
$min  |获取集合中所有文档对应值得最小值。|   db.mycol.aggregate({$group : {_id : "$by_user", num_tutorial : {$min : "$likes"}}})
$max  |获取集合中所有文档对应值得最大值。|   db.mycol.aggregate({$group : {_id : "$by_user", num_tutorial : {$max : "$likes"}}})
$push |在结果文档中插入值到一个数组中。 |   db.mycol.aggregate({$group : {_id : "$by_user", url : {$push: "$url"}}})
$addToSet   |在结果文档中插入值到一个数组中，但不创建副本。 |  db.mycol.aggregate({$group : {_id : "$by_user", url : {$addToSet : "$url"}}})
$first    |根据资源文档的排序获取第一个文档数据。|     db.mycol.aggregate({$group : {_id : "$by_user", first_url : {$first : "$url"}}})
$last     |根据资源文档的排序获取最后一个文档数据|   db.mycol.aggregate({$group : {_id : "$by_user", last_url : {$last : "$url"}}})

## 管道符
* **MongoDB的聚合管道将MongoDB文档在一个管道处理完毕后将结果传递给下一个管道处理。管道操作是可以重复的。**

* $project：修改输入文档的结构。可以用来重命名、增加或删除域，也可以用于创建计算结果以及嵌套文档。 -- field
* $match：用于过滤数据，只输出符合条件的文档。$match使用MongoDB的标准查询操作。    -- where 
* $limit：用来限制MongoDB聚合管道返回的文档数。   -- limit 
* $skip：在聚合管道中跳过指定数量的文档，并返回余下的文档。     -- page
* $unwind：将文档中的某一个数组类型字段拆分成多条，每条包含数组中的一个值。
* $group：将集合中的文档分组，可用于统计结果。
* $sort：将输入文档排序后输出。
* $geoNear：输出接近某一地理位置的有序文档。



