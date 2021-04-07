# proj44-AliOS-Things-Thread-level-RWLock
### 项目名称
基于AliOS Things操作系统提供线程级读写锁功能

### 项目描述

AliOS Things中，互斥量（mutex）实现了最基础的线程（即task）互斥。
此外，业界还存在一种与互斥量类似的实现线程互斥的机制----读写锁。它实现更细粒度的线程互斥，允许更高的并行性。其特性为：

* 多个读操作可以并行：即同一时刻允许多个读者并行操作。
* 多个写操作之间互斥：即同一时刻只允许一个写者操作。
* 读操作与写操作之间互斥：即不允许读者与写者并行。

本实验的目标是在AliOS Things上面实现线程级读写锁功能。

### 所属赛道

2021全国大学生操作系统比赛的“OS功能设计”赛道



### 参赛要求

- 以小组为单位参赛，最多三人一个小组，且小组成员是来自同一所高校的本科生（2021年春季学期或之后本科毕业的大一~大四的学生）
- 如学生参加了多个项目，参赛学生选择一个自己参加的项目参与评奖
- 请遵循“2021全国大学生操作系统比赛”的章程和技术方案要求



### 项目导师

黄震

* github

* email wuqi.hz@alibaba-inc.com



### 难度

中等



### 特征

* 使用C语言编写

* 留意题目要求是线程级读写锁，并非读写自旋锁

* 读写锁数据结构`krwlock_t`，接口要求如下：

  ```c
  //读写锁创建
  kstat_t krhino_rwlock_create(krwlock_t *rwlock, const name_t *name);
  //读写锁删除
  kstat_t krhino_rwlock_del(krwlock_t *rwlock);
  //读写锁读加锁
  kstat_t krhino_rwlock_rdlock(krwlock_t *rwlock);
  //读写锁写加锁
  kstat_t krhino_rwlock_wrlock(krwlock_t *rwlock);
  //读写锁解锁
  kstat_t krhino_rwlock_unlock(krwlock_t *rwlock);
  ```

  



### 文档
* 硬件平台：阿里云IoT官方推出的HaaS EDU K1或HaaS100
* 软件平台：AliOS Things物联网操作系统
* HaaS EDU K1技术文档：https://blog.csdn.net/haastech/category_10825080.html
* HaaS100快速开始文档：https://help.aliyun.com/document_detail/184184.html
* AliOS Things物联网操作系统说明文档：https://github.com/alibaba/AliOS-Things/tree/dev_3.1.0_haas

### License

* [Apache-2.0](https://opensource.org/licenses/Apache-2.0)



## 预期目标

### 注意：下面的内容是建议内容，不要求必须全部完成。选择本项目的同学也可与导师联系，提出自己的新想法，如导师认可，可加入预期目标



### 第一题：实现不同的读写锁操作模式

读操作优先：允许最大读并发。即当已经有读者或写者加锁时，后续到来的读请求优先于写请求得到满足。
写操作优先：解决“读操作优先”模式下写请求容易饿死的问题。即当已经有读者或写者加锁时，后续到来的写请求优先于读请求得到满足。

### 第二题：实现读写锁的可重入机制
允许同一个线程对同一个读写锁进行多次加锁与解锁操作。
比如同一个线程可以对同一个读写锁加锁N次，当完成N次释放锁操作之后，该线程才这正释放锁。
