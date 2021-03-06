# RDD运行原理
<!-- TOC -->

- [RDD运行原理](#rdd运行原理)
    - [MapReduce问题](#mapreduce问题)
    - [RDD](#rdd)
        - [RDD是什么](#rdd是什么)
        - [RDD运行过程](#rdd运行过程)
        - [转换类型](#转换类型)
        - [动作类型](#动作类型)
        - [粗细粒度](#粗细粒度)
        - [特点](#特点)
        - [运行原理](#运行原理)

<!-- /TOC -->


## MapReduce问题
MapReduce 查询计算 是读取，写入磁盘

带来的问题：
1.迭代
2.反复读写工作子集
3.磁盘IO开销
4.序列化和反序列化开销

序列化: 对象->可保存和传输格式
Java 对象->二进制，字符串

反序列化: 可保存和传输格式->对象


## RDD

### RDD是什么
RDD - 提供抽象的数据结构 （弹性分布式数据集）

### RDD运行过程

![](https://raw.githubusercontent.com/Syncma/Figurebed/master/img/20200126125224.png)

本质是只读的分区记录集合

只能通过生成新的RDD来完成一个数据修改的目的




### 转换类型

![](https://raw.githubusercontent.com/Syncma/Figurebed/master/img/20200126125736.png)

### 动作类型
![](https://raw.githubusercontent.com/Syncma/Figurebed/master/img/20200126125657.png)




### 粗细粒度

支持粗粒度修改，一次只能针对RDD全集进行转换
不支持细粒度修改，不适合数据库对单条进行修改， 不适合网页爬虫


### 特点
1.天然的高效容错性

现有容错机制- 数据复制（数据备份），记录日志（日志操作）

弊端：开销大


DAG - Lineage血缘关系图（可以快速恢复数据）



2.中间结果 ->在内存的多个RDD之间传递转换
![](https://raw.githubusercontent.com/Syncma/Figurebed/master/img/20200126130815.png)

3.避免不必要的序列化和反序列化开销


### 运行原理
![](https://raw.githubusercontent.com/Syncma/Figurebed/master/img/20200127102003.png)
