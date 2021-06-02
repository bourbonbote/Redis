# 入门概述

## 简介

> Redis即REmote DIctionary Server(远程字典服务器)

是完全开源免费的，用C语言编写的，遵守BSD协议，是一个高性能的(key/value)分布式内存数据库，基于内存运行
并支持持久化的NoSQL数据库，是当前最热门的NoSql数据库之一,也被人们称为数据结构服务器

Redis 特点

1. Redis支持数据的持久化，可以将内存中的数据保持在磁盘中，重启的时候可以再次加载进行使用
2. Redis不仅仅支持简单的key-value类型的数据，同时还提供list，set，zset，hash等数据结构的存储
3. Redis支持数据的备份，即master-slave模式的数据备份

## Redis基础知识

### 单进程

```java
单进程模型来处理客户端的请求。对读写等事件的响应是通过对epoll函数的包装来做到的。Redis的实际处理速度完全依靠主进程的执行效率
    
Epoll是Linux内核为处理大批量文件描述符而作了改进的epoll，是Linux下多路复用IO接口select/poll的增强版本，
它能显著提高程序在大量并发连接中只有少量活跃的情况下的系统CPU利用率。
```

### 数据库管理

```java
默认16个数据库，类似数组下表从零开始，初始默认使用零号库
    Redis数据库的索引都是从零开始
	Select命令切换数据库
	Dbsize查看当前数据库的key的数量
	Flushdb：清空当前库
    Flushall；通杀全部库
    
统一密码管理，16个库都是同样密码，要么都OK要么一个也连接不上
```

## Redis数据类型

### 五大数据类型

- String（字符串）

  ```bash
  string是redis最基本的类型，你可以理解成与Memcached一模一样的类型，一个key对应一个value。
   
  string类型是二进制安全的。意思是redis的string可以包含任何数据。比如jpg图片或者序列化的对象 。
   
  string类型是Redis最基本的数据类型，一个redis中字符串value最多可以是512M
  ```

- Hash（哈希，类似java里的Map）

  ```bash
  Redis hash 是一个键值对集合。
  Redis hash是一个string类型的field和value的映射表，hash特别适合用于存储对象。
    
  类似Java里面的Map<String,Object>
  ```

- List（列表）

  ```bahs
  Redis 列表是简单的字符串列表，按照插入顺序排序。你可以添加一个元素导列表的头部（左边）或者尾部（右边）。
  它的底层实际是个链表
  ```

- Set（集合）

  ```bash
  Redis的Set是string类型的无序集合。它是通过HashTable实现实现的
  ```

- Zset(sorted set：有序集合)

  ```bash
  Redis zset 和 set 一样也是string类型元素的集合,且不允许重复的成员。
  
  不同的是每个元素都会关联一个double类型的分数。
  
  redis正是通过分数来为集合中的成员进行从小到大的排序。zset的成员是唯一的,但分数(score)却可以重复。
  ```

### redis常见数据类型操作命令

[求助](Http://redisdoc.com/)

#### key

- Key *

  ​	表名查询所有

- Type key

  ​	返回 key 所储存的值的类型。

- Rename key

  ​	修改key的名称

- Del key

  ​	key存在的话，将其删除

- Exists key

  ​	检查给定的key是否存在

- Expire key

  ​	为给定key设置过期时间，以秒计

- TTL key

  ​	以秒为单位，返回给定 key 的剩余生存时间(TTL, time to live)。

 

#### String

> **增**

| [APPEND key   value](https://www.runoob.com/redis/strings-append.html)  如果 key 已经存在并且是一个字符串， APPEND 命令将指定的  value 追加到该 key 原来值（value）的末尾。 |
| ------------------------------------------------------------ |
| [SET key value](https://www.runoob.com/redis/strings-set.html)  **设置指定  key 的值** |
| [INCR key](https://www.runoob.com/redis/strings-incr.html)  将 key 中储存的数字值增一。 |
| [INCRBY key   increment](https://www.runoob.com/redis/strings-incrby.html)  将 key 所储存的值加上给定的步长（increment）  。 |
| [INCRBYFLOAT   key increment](https://www.runoob.com/redis/strings-incrbyfloat.html)  将 key 所储存的值加上给定的步长（increment）  。 |
| [DECR key](https://www.runoob.com/redis/strings-decr.html)  将 key 中储存的数字值减一。 |
| [DECRBY key   decrement](https://www.runoob.com/redis/strings-decrby.html)  key 所储存的值减去给定的减量值（decrement） 。 |

 

> **删除**  

- del key

> **改**

- [SETRANGE key offset value](https://www.runoob.com/redis/strings-setrange.html)

  ​	用 value 参数覆写给定 key 所储存的字符串值，从偏移量 offset 开始。

> **查**  

- [GET key](https://www.runoob.com/redis/strings-get.html)

  ​	获取指定 key 的值。

- [STRLEN key](https://www.runoob.com/redis/strings-strlen.html)

  ​	返回 key 所储存的字符串值的长度。

- [GETRANGE key start end](https://www.runoob.com/redis/strings-getrange.html)

  ​	返回 key 中字符串值的子字符

#### Hash

> **增** 

| [HSET key   field value](https://www.runoob.com/redis/hashes-hset.html)  将哈希表 key 中的字段 field 的值设为 value 。 |
| ------------------------------------------------------------ |
| [HMSET key   field1 value1 [field2 value2 \]](https://www.runoob.com/redis/hashes-hmset.html)  同时将多个 field-value (域-值)对设置到哈希表 key  中。 |
| [HSETNX key   field value](https://www.runoob.com/redis/hashes-hsetnx.html)  只有在字段 field 不存在时，设置哈希表字段的值。 |
| [HINCRBY key   field increment](https://www.runoob.com/redis/hashes-hincrby.html)  为哈希表 key 中的指定字段的整数值加上增量 increment  。 |
| [HINCRBYFLOAT   key field increment](https://www.runoob.com/redis/hashes-hincrbyfloat.html)  为哈希表 key 中的指定字段的浮点数值加上增量 increment  。 |

> **删** 

- [HDEL key field1 [field2\]](https://www.runoob.com/redis/hashes-hdel.html)

  ​	删除一个或多个哈希表字段

> **查**

| [HGET key   field](https://www.runoob.com/redis/hashes-hget.html)  获取存储在哈希表中指定字段的值。 |
| ------------------------------------------------------------ |
| [HGETALL key](https://www.runoob.com/redis/hashes-hgetall.html)  获取在哈希表中指定 key 的所有字段和值 |
| [HLEN key](https://www.runoob.com/redis/hashes-hlen.html)  获取哈希表中字段的数量 |
| [HMGET key   field1 [field2\]](https://www.runoob.com/redis/hashes-hmget.html)  获取所有给定字段的值 |
| [HVALS key](https://www.runoob.com/redis/hashes-hvals.html)  获取哈希表中所有值。 |
| [HKEYS key](https://www.runoob.com/redis/hashes-hkeys.html)  获取所有哈希表中的字段 |

#### List

> **增** 

- [LPUSH key value1 [value2\]](https://www.runoob.com/redis/lists-lpush.html)

  ​	将一个或多个值插入到列表头部

- [RPUSH key value1 [value2\]](https://www.runoob.com/redis/lists-rpush.html)

  ​	在列表中添加一个或多个值

- [LPUSHX key value](https://www.runoob.com/redis/lists-lpushx.html)

  ​	将一个值插入到已存在的列表头部

- [RPUSHX key value](https://www.runoob.com/redis/lists-rpushx.html)

  ​	为已存在的列表添加值

 

> **删** 

- [LPOP key](https://www.runoob.com/redis/lists-lpop.html)

  移出并获取列表的第一个元素

- [RPOP key](https://www.runoob.com/redis/lists-rpop.html)

  移除列表的最后一个元素，返回值为移除的元素。

- [LTRIM key start stop](https://www.runoob.com/redis/lists-ltrim.html)

  对一个列表进行修剪(trim)，就是说，让列表只保留指定区间内的元素，不在指定区间之内的元素都将被删除。

- [LREM key count value](https://www.runoob.com/redis/lists-lrem.html)

  移除count个列表元素

> **改** 

- [LSET key index value](https://www.runoob.com/redis/lists-lset.html)

  通过索引设置列表元素的值

- [LINSERT key BEFORE|AFTER pivot value](https://www.runoob.com/redis/lists-linsert.html)

  在列表的元素前或者后插入元素

> **查** 

- [LRANGE key start stop](https://www.runoob.com/redis/lists-lrange.html)

  获取列表指定范围内的元素

- [LLEN key](https://www.runoob.com/redis/lists-llen.html)

  获取列表长度

- [LINDEX key index](https://www.runoob.com/redis/lists-lindex.html)

  通过索引获取列表中的元素

#### Set

> **增** 

- [SADD key member1 [member2\]](https://www.runoob.com/redis/sets-sadd.html)

  向集合添加一个或多个成员

> **删** 

- [SREM key member1 [member2\]](https://www.runoob.com/redis/sets-srem.html)

  移除集合中一个或多个成员

> **查** 

- [SCARD key](https://www.runoob.com/redis/sets-scard.html)

  获取集合的成员数

- [SISMEMBER key member](https://www.runoob.com/redis/sets-sismember.html)

  判断 member 元素是否是集合 key 的成员

- [SMEMBERS key](https://www.runoob.com/redis/sets-smembers.html)

  返回集合中的所有成员

> **数学集合** 

- [SDIFF key1 [key2\]](https://www.runoob.com/redis/sets-sdiff.html)

  返回第一个集合与其他集合之间的差异。

- [SDIFFSTORE destination key1 [key2\]](https://www.runoob.com/redis/sets-sdiffstore.html)

  返回给定所有集合的差集并存储在 destination 中

- [SINTER key1 [key2\]](https://www.runoob.com/redis/sets-sinter.html)

  返回给定所有集合的交集

- [SINTERSTORE destination key1 [key2\]](https://www.runoob.com/redis/sets-sinterstore.html)

  返回给定所有集合的交集并存储在 destination 中

- [SUNION key1 [key2\]](https://www.runoob.com/redis/sets-sunion.html)

  返回所有给定集合的并集

- [SUNIONSTORE destination key1 [key2\]](https://www.runoob.com/redis/sets-sunionstore.html)

  所有给定集合的并集存储在 destination 集合中

- [SMOVE source destination member](https://www.runoob.com/redis/sets-smove.html)

  将 member 元素从 source 集合移动到 destination 集合 

- [SRANDMEMBER key [count\]](https://www.runoob.com/redis/sets-srandmember.html)

  返回集合中一个或多个随机数

- [SPOP key](https://www.runoob.com/redis/sets-spop.html)

  移除并返回集合中的一个随机元

#### Zset

> **增** 

- [ZADD key score1 member1 [score2 member2\]](https://www.runoob.com/redis/sorted-sets-zadd.html)

  向有序集合添加一个或多个成员，或者更新已存在成员的分数

- [ZINCRBY key increment member](https://www.runoob.com/redis/sorted-sets-zincrby.html)

  有序集合中对指定成员的分数加上增量 increment

> **删** 

- [ZREM key member [member ...\]](https://www.runoob.com/redis/sorted-sets-zrem.html)

  移除有序集合中的一个或多个成员

- [ZREMRANGEBYLEX key min max](https://www.runoob.com/redis/sorted-sets-zremrangebylex.html)

  移除有序集合中给定的字典区间的所有成员

- [ZREMRANGEBYRANK key start stop](https://www.runoob.com/redis/sorted-sets-zremrangebyrank.html)

  移除有序集合中给定的排名区间的所有成员

- [ZREMRANGEBYSCORE key min max](https://www.runoob.com/redis/sorted-sets-zremrangebyscore.html)

  移除有序集合中给定的分数区间的所有成员

> **查** 

- [ZSCORE key member](https://www.runoob.com/redis/sorted-sets-zscore.html)

  返回有序集中，成员的分数值
- [ZRANGE key start stop [WITHSCORES\]](https://www.runoob.com/redis/sorted-sets-zrange.html)

  通过索引区间返回有序集合指定区间内的成员

- [ZRANGEBYLEX key min max [LIMIT offset count\]](https://www.runoob.com/redis/sorted-sets-zrangebylex.html)

  通过字典区间返回有序集合的成员

- [ZRANGEBYSCORE key min max [WITHSCORES\] [LIMIT]](https://www.runoob.com/redis/sorted-sets-zrangebyscore.html)

  通过分数返回有序集合指定区间内的成员

- [ZRANK key member](https://www.runoob.com/redis/sorted-sets-zrank.html)

  返回有序集合中指定成员的索引

- [ZREVRANGE key start stop [WITHSCORES\]](https://www.runoob.com/redis/sorted-sets-zrevrange.html)

  返回有序集中指定区间内的成员，通过索引，分数从高到低
- [ZREVRANGEBYSCORE key max min [WITHSCORES\]](https://www.runoob.com/redis/sorted-sets-zrevrangebyscore.html)

  返回有序集中指定分数区间内的成员，分数从高到低排序

- [ZREVRANK key member](https://www.runoob.com/redis/sorted-sets-zrevrank.html)

  返回有序集合中指定成员的排名，有序集成员按分数值递减(从大到小)排序

> **集合**

- [ZINTERSTORE destination numkeys key [key ...\]](https://www.runoob.com/redis/sorted-sets-zinterstore.html)

  计算给定的一个或多个有序集的交集并将结果集存储在新的有序集合 destination 中

> **计算**

- [ZCARD key](https://www.runoob.com/redis/sorted-sets-zcard.html)

  获取有序集合的成员数

- [ZCOUNT key min max](https://www.runoob.com/redis/sorted-sets-zcount.html)

  计算在有序集合中指定区间分数的成员数

- [ZLEXCOUNT key min max](https://www.runoob.com/redis/sorted-sets-zlexcount.html)

  在有序集合中计算指定字典区间内成员数量

- [ZUNIONSTORE destination numkeys key [key ...\]](https://www.runoob.com/redis/sorted-sets-zunionstore.html)

  计算给定的一个或多个有序集的并集，并存储在新的 key 中

