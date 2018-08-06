## 第4章 进程调度
### 4.1 多任务
cooperative multitasking : Linux, Unix, Max OS9, Windows3.1 协作式任务管理器
preemptive multitasking: 抢占式 任务管理器

### 4.2 Linux的进程调度
Linux 设计来一个 O(1) 的 Scheduler

CFS use a red-black tree to manager the list of runnable process.

O(1) scheduler: Rotating Staircase Deadline scheduler, Completely Fair Scheduler (CFS)

I/0-Bound Versus Processor-Bound Processes

I/0 not only the disk, but also any type of blockable resource, such as keyboard input , mouse, or network I/0. Most GUI are I/0 bound, they spend most of their time waiting on user ineraction.

### 4.3 策略
#### 4.3.1 I/O 消耗型和处理器消耗型的进程
#### 4.3.2 进程优先级
Process Priority
two separate priority ranges:
first:
nice value : -20 ~ +19, default is 0, nice value is smaller, priority is higher. To see a list if nice value ps -el

second:
real-time priority The values are configurable, but by default range from 0 to 99, inclusive. Opposite from nice vales, higher real-time priority values correspond to a greater priority

#### 4.3.3 时间片
#### 4.3.4 调度策略的活动
#### 4.4 Linux 调度算法
#### 4.4.1 调度器类
#### 4.4.2 Unix系统中的进程调度
在抢占式时间片调度器中， 有四大问题：

第一个问题：
    后台的进程，计算密集型进程，需要频繁的上下文切换，但是因为 nice 值高(优先级比较低)， 所以时间片小，上下文切换的代价非常大.

第二问题:

第三问题：

第四问题：

问题的本质在于使用了固定的时间片和固定的切换频率. 这种Fixed 系统模型设计，一般来说效率不高。
所以我们要解决的问题是, 使用更加灵活的CPU 分配方式。

由此产生了 CFS 调度器.

#### 4.4.3 公平调度
The core of CFS’s scheduling algorithm: Pick the task with the smallest vruntime.
CFS uses a red-black tree to manage the list of runnable processes and efficiently find the process with the smallest vruntime.
key for each node is the runnable process’s virtual runtime.

The vruntime variable stores the virtual runtime of a process, which is the actual runtime (the amount of time spent running) normalized (or weighted) by the number of runnable processes.

How to calculate the vruntime?

### 4.5 Linux 调度的实现
#### 4.5.1 时间记账
1 调度器实体结构

2 虚拟实时

#### 4.5.2 进程选择
1 挑选下一个任务

2 向树中加入进程

3 从树中删除进程

#### 4.5.3 调度器入口
#### 4.5.4 睡眠和唤醒
1 等待队列
2 唤醒

### 4.6 抢占和上下文切换
#### 4.6.1 用户抢占
#### 4.6.2 内核抢占
#### 4.7 实时调度策略
### 4.8 与调用相关的系统调用
#### 4.8.1 与调度策略和优先级相关的系统调用
#### 4.8.2 与处理器绑定有关的系统调用
#### 4.8.3 放弃处理器时间
## 4.9 小结
既合适众多的可运行进程, 又具有可伸缩性，还能在调度周期和吞吐量之间求得平衡，同时还满足各种负载的需求。
