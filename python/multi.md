多线程采用的是分时复用技术，即不存在真正的多线程，cpu做的事是快速地切换线程，以达到类似同步运行的目的，因为高密集运算方面多线程是没有用的，但是对于存在延迟的情况（延迟IO，网络等）多线程可以大大减少等待时间，避免不必要的浪费。

对于资源，加锁是个重要的环节。因为python原生的list,dict等，都是not thread safe的。而Queue，是线程安全的，因此在满足使用条件下，建议使用队列。

```Python 
Queue模块有三种队列及构造函数:
Python Queue模块的FIFO队列先进先出。 class Queue.Queue(maxsize)
LIFO类似于堆，即先进后出。 class Queue.LifoQueue(maxsize)
还有一种是优先级队列级别越低越先出来。 class Queue.PriorityQueue(maxsize)

此包中的常用方法(q = Queue.Queue()):
q.qsize() 返回队列的大小
q.empty() 如果队列为空，返回True,反之False
q.full() 如果队列满了，返回True,反之False
q.full 与 maxsize 大小对应
q.get([block[, timeout]]) 获取队列，timeout等待时间
q.get_nowait() 相当q.get(False)
非阻塞 q.put(item) 写入队列，timeout等待时间
q.put_nowait(item) 相当q.put(item, False)
q.task_done() 在完成一项工作之后，q.task_done() 函数向任务已经完成的队列发送一个信号
q.join() 实际上意味着等到队列为空，再执行别的操作
```