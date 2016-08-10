## 进程与线程：

[转载处](http://www.ruanyifeng.com/blog/2013/04/processes_and_threads.html)

### 区别：

0、计算机中:
   1. 
进程是最小的资源分配单位；进程之间各自拥有各自的内存空间，都是2^32（地址总线定）
   1. 
一个进程可以有多个线程，线程是最小的执行单元；线程共享进程的所有资源，包括缓冲区、调用栈（堆不是，只有部分）。
   1. 
进程的中断代表资源的释放或者申请，线程的切换只是同一进程下另一个执行路径的切换而已。
   1. 
进程的切换效率比较低，但是健壮性高；线程的切换效率高，但是一个线程死亡代表着整个进程的死掉，所以健壮性不高。


 1、计算机的核心是CPU，它承担了所有的计算任务。它就像一座工厂，时刻在运行。
 ![](1.jpg)
 
 2、假定工厂的电力有限，一次只能供给一个车间使用(早期的CPU）。也就是说，一个车间开工的时候，其他车间都必须停工。
 背后的含义就是，单个CPU一次只能运行一个任务。
 
 ![](2.png)
 
 3、进程就好比工厂的车间，它代表CPU所能处理的单个任务。任一时刻，CPU总是运行一个进程，其他进程处于非运行状态。
 
 ![](3.jpg)
 
 4、一个车间里，可以有很多工人。他们协同完成一个任务。
 ![](4.jpg)
 
 5、线程就好比车间里的工人。一个进程可以包括多个线程。
 
 ![](5.jpg)
 
 6、车间的空间是工人们共享的，比如许多房间是每个工人都可以进出的。这象征一个进程的内存空间是共享的，每个线程都可以使用这些共享内存。
 
 ![](6.png)
 
 7、可是，每间房间的大小不同，有些房间最多只能容纳一个人，比如厕所。里面有人的时候，其他人就不能进去了。这代表一个线程使用某些共享内存时，其他线程必须等它结束，才能使用这一块内存。
 
 ![](7.jpg)
 
 8、一个防止他人进入的简单方法，就是门口加一把锁。先到的人锁上门，后到的人看到上锁，就在门口排队，等锁打开再进去。这就叫"互斥锁"（Mutual exclusion，缩写 Mutex），防止多个线程同时读写某一块内存区域。
 
 ![](8.jpg)
 
 9、还有些房间，可以同时容纳n个人，比如厨房。也就是说，如果人数大于n，多出来的人只能在外面等着。这好比某些内存区域，只能供给固定数目的线程使用。
 
 ![](9.jpg)
 
 10、这时的解决方法，就是在门口挂n把钥匙。进去的人就取一把钥匙，出来时再把钥匙挂回原处。后到的人发现钥匙架空了，就知道必须在门口排队等着了。这种做法叫做"信号量"（Semaphore），用来保证多个线程不会互相冲突。
 
 ![](10.jpg)
 
 
不难看出，mutex是semaphore的一种特殊情况（n=1时）。也就是说，完全可以用后者替代前者。但是，因为mutex较为简单，且效率高，所以在必须保证资源独占的情况下，还是采用这种设计。

![](11.png)

 11、操作系统的设计，因此可以归结为三点：<br>
（1）以多进程形式，允许多个任务同时运行；<br>
（2）以多线程形式，允许单个任务分成不同的部分运行；<br>
（3）提供协调机制，一方面防止进程之间和线程之间产生冲突，另一方面允许进程之间和线程之间共享资源。<br>
```python
所以对于单进程的JS语言来说，就会很浪费资源： 
Event Loop就是为了解决这个问题而提出的。Wikipedia这样定义： 
    "Event Loop是一个程序结构，用于等待和发送消息和事件。
    （a programming construct that waits for and dispatches events or messages in a program.）" 
简单说，就是在程序中设置两个线程：
    一个负责程序本身的运行，称为"主线程"；
    另一个负责主线程与其他进程（主要是各种I/O操作）的通信，被称为"Event Loop线程"（可以译为"消息线程"）。
python中通过协程来处理：async/await  分别用来定义协程函数和调用
    async def get_reddit_top(subreddit, client):
           data1 = await get_json(client, 'https://www.reddit.com/r/'+subreddit + '/top.json?
                                            sort=top&t=day&limit=5')
           j = json.loads(data1.decode('utf-8'))
           for i in j['data']['children']:
                 score = i['data']['score']
                 title = i['data']['title']
                 link = i['data']['url']
                 print(str(score) + ': ' + title + ' (' + link + ')')
           print('DONE:', subreddit + '\n')
    def signal_handler(signal, frame):
          loop.stop()
          client.close()
          sys.exit(0)
    signal.signal(signal.SIGINT, signal_handler)
    asyncio.ensure_future(get_reddit_top('python', client))
    asyncio.ensure_future(get_reddit_top('programming', client))
    asyncio.ensure_future(get_reddit_top('compsci', client))
    loop.run_forever()
```
###Linux与fork()
两种方式创建进程：
* 
操作系统：fork()，有两个返回值；两个进程运行顺序不定；有不同的栈段、数据段、堆段等，子进程采用写时拷贝(copy-on-write)拷贝来的(即啥时候修改啥时候拷贝过来)；
  * vfork实际上也是调用的fork，但共享父进程中数据，且保证子进程先执行，exit()结束子进程后父才会继续(不能同时！！！)，但是共享内存不安全，并不鼓励
  * 创建子进程就是一个clone的过程。目前**三个fork、clone、vfork**，其实后面两个都是调用的fork

* 
父进程自己创建

###return 和 exit的不同
* 
exit是系统调用，是不会退栈的，表示一个进程的结束！！它会将控制权交给系统（多线程返回给父进程），删除进程使用的内存空间，并将应用程序的一个状态返回给OS，这个状态标识了应用程序的一些运行信息，
* return不是系统调用是C语言的函数，它会退栈将执行控制权交给调用函数，引发退栈操作，子进程退栈的操作可能会修改父进程的栈，所有return不行。
* main函数中调用return，会隐式调用exit：非主函数中调用return和exit效果很明显，但是在main函数中调用return和exit的现象就很模糊，多数情况下现象都是一致的。
* fork和vfork中区别大，因为vfork是共享内存，所以可以exit，但是不能是return，否则子结束因为退栈把父的也改变了。

###IPC：

[返回目录](README.md)