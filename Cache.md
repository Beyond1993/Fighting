最近在给系统加缓存

关于缓存一致性问题，一种方法是简单的用 Updater 直接广播 更新的值到 Cache

还有就是之前上Architecture的时候专门讲到的cache 一致性原理。

但是这些方法共同的特点是Cache 之间是不相互通信的。 要么保持和数据库一致，要么保持和主存一致