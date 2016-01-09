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

q.put(item,block[False],timeout[None])
        block=True:若queue已满，调用该queue的线程阻塞直至出现一个空的单元。
        block=False:满了就会引起Full异常
        
q.get(item,block,timeout)
        block=True:若queue为空，调用该queue的线程阻塞直至出现一个可用单元。
        block=False:满了就会引起Empty异常
```
范例1：
```python
import Queue,threading,time,random

class consumer(threading.Thread):
    def __init__(self,que):
        threading.Thread.__init__(self)
        self.daemon = False
        self.queue = que
    def run(self):
        while True:
            if self.queue.empty():
                break
            item = self.queue.get()
            #processing the item
            time.sleep(item)
            print self.name,item
            self.queue.task_done()
        return
que = Queue.Queue()
for x in range(10):
    que.put(random.random() * 10, True, None)       #生产者
consumers = [consumer(que) for x in range(3)]

for c in consumers:
    c.start()
que.join()

代码的功能是产生10个随机数（0～10范围），sleep相应时间后输出数字和线程名称
这段代码里，是一个快速生产者（产生10个随机数），3个慢速消费者的情况。
在这种情况下，先让三个consumers跑起来，然后主线程用que.join()阻塞。
当三个线程发现队列都空时，各自的run函数返回，三个线程结束。同时主线程的阻塞打开，全部程序结束。
```