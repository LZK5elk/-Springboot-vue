一、框架基础学习

安装mysql-8.31（要添加path，net start mysql启动）

nodejs-24（要添加path）

jdk-17（要添加path）

idea-2025，redis-3.2.100

 

Redis 中字符串类型常用命令：

\- SET key value             设置指定key的值

\- GET key                 获取指定key的值

\- SETEX key seconds value     设置指定key的值，并将 key 的过期时间设为 seconds 秒

\- SETNX key value 只有在 key   不存在时设置 key 的值

 

Redis hash 是一个string类型的 field 和 value 的映射表，hash特别适合用于存储对象，常用命令：

\- HSET key field value       将哈希表 key 中的字段 field 的值设为 value

\- HGET key field            获取存储在哈希表中指定字段的值

\- HDEL key field            删除存储在哈希表中的指定字段

\- HKEYS key                获取哈希表中所有字段

\- HVALS key                获取哈希表中所有值

\- HGETALL key             获取在哈希表中指定 key 的所有字段和值

 

Redis 列表是简单的字符串列表，按照插入顺序排序，常用命令：

\- LPUSH key value1 [value2]     将一个或多个值插入到列表头部

\- LRANGE key start stop         获取列表指定范围内的元素

\- RPOP key                    移除并获取列表最后一个元素

\- LLEN key                     获取列表长度

\- BRPOP key1 [key2 ] timeout    移出并获取列表的最后一个元素， 如果列表没有元素会阻塞列表直到等待超   

 

Redis set 是string类型的无序集合。集合成员是唯一的，这就意味着集合中不能出现重复的数据，常用命令：

\- SADD key member1 [member2]       向集合添加一个或多个成员

\- SMEMBERS key                  返回集合中的所有成员

\- SCARD key                     获取集合的成员数

\- SINTER key1 [key2]               返回给定所有集合的交集

\- SUNION key1 [key2]              返回所有给定集合的并集

\- SDIFF key1 [key2]                返回给定所有集合的差集

\- SREM key member1 [member2]       移除集合中一个或多个成员

 

Redis sorted set 有序集合是 string 类型元素的集合，且不允许重复的成员。每个元素都会关联一个double类型的分数(score) 。redis正是通过分数来为集合中的成员进行从小到大排序。有序集合的成员是唯一的，但分数却可以重复。

常用命令：

\- ZADD key score1 member1 [score2 member2]   向有序集合添加一个或多个成员，或者更新已存在成员的 分数 

\- ZRANGE key start stop [WITHSCORES]        通过索引区间返回有序集合中指定区间内的成员

\- ZINCRBY key increment member            有序集合中对指定成员的分数加上增量 increment

\- ZREM key member [member ...]             移除有序集合中的一个或多个成员

 

Redis中的通用命令，主要是针对key进行操作的相关命令：

\- KEYS pattern  查找所有符合给定模式( pattern)的 key 

\- EXISTS key  检查给定 key 是否存在

\- TYPE key  返回 key 所储存的值的类型

\- TTL key  返回给定 key 的剩余生存时间(TTL, time to live)，以秒为单位

\- DEL key  该命令用于在 key 存在是删除 key

 

新建redisdemo项目:

![img](1.assets/wps1.jpg) 

在RedisConfig里写出格式化工厂

![img](1.assets/wps2.jpg) 

Test/java中写测试项目，resdis语句学习

二、实训项目背景

（一）Web应用发展历程

Web应用开发经历了从传统单体架构到现代前后端分离架构的演变过程。早期的Web开发采用JSP、Servlet等技术，前后端代码紧密耦合在一起，导致开发效率低下、维护困难。随着互联网技术的快速发展和用户需求的日益复杂化，传统的开发模式已经无法满足现代Web应用的需求。

 

（二）前后端分离架构的兴起

前后端分离架构将应用分为独立的前端展示层和后端服务层，两者通过RESTful API进行数据交互。这种架构模式具有以下显著优势：

 

1. 开发效率提升

 

前后端团队可以并行开发，互不干扰

前端专注于用户体验和界面交互

后端专注于业务逻辑和数据处理

2. 技术选型灵活

 

前端可以自由选择React、Vue、Angular等框架

后端可以选择Java、Python、Node.js等技术栈

双方只需约定好API接口规范即可

3. 维护成本降低

 

代码职责清晰，易于定位问题

模块化开发，便于测试和调试

版本迭代更加灵活

三、实训项目实现（知识点，笔记

运行后端:

打开health，连接mysql数据库，打开redis，运行若依

![img](1.assets/wps3.jpg) 

 

运行前端:

![img](1.assets/wps4.jpg) 

打开dev运行

 

 

在health-vue3-ui更换ui:

标签logo:删除原有的favicon.ico，把新拷贝过来的logo更名为favicon.ico

标签标题:找到根目录下的index.html文件，把title更换为自己的内容

登录标题和背景图:src/views/login.vue更换

 

 

二次开发:

在sql中执行语句生成新的表

代码生成中

![img](1.assets/wps5.jpg) 

生成新的代码

将生成新的sql语句执行

![img](1.assets/wps6.jpg) 

将main和vue中代码分别放入前端和后端项目中

 

优化前端代码:

在vue中src/veiws/reservation里的三个项目分别进行优化

![img](1.assets/wps7.jpg)
