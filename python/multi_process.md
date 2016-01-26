
## 多进程


在python中多线程并不是真正的多线程，只是体现在CPU的快速切换上，如果想真正利用多核CPU，就要使用多进程。

### 基础

```python
创建:
Process([group[,target[,name[,args[,kwargs]]]]]):
    group  一般不用
    target 调用的对象
    name    别名
    args    参数,元组形式
    kwargs  字典
方法:
    is_alive()
    join([timeout])
    run()
    start()
    terminate()
属性:
    authkey     
    daemon      在start()之前设置：意味着父进程终止后自动终止，且自己不能产生新进程
    exitcode
    name
    pid
```

### 使用

```python
#实例1：单个
import multiprocessing
import time

def worker(ti):
    n=6
    while n>0:
        print("time is {0}".format(time.ctime()))
        time.sleep(ti)
        n-=1
    
if __name__=="__main__":
    print("the number of cpu is {0}".format(multiprocessing.cpu_count()))
    p = multiprocessing.Process(target=worker,args = (3,))
    p.start()
    print("pid is {0}".format(p.pid))
    print("name is {0}".format(p.name))
    print("isalive is {0}".format(p.is_live()))
```
```python
#实例2：多个
import multiprocessing
import time

def worker1(ti):
    print("time is {0}".format(time.ctime()))
    time.sleep(ti)
def worker2(ti):
    print("time is {0}".format(time.ctime()))
    time.sleep(ti)
def worker3(ti):
    print("time is {0}".format(time.ctime()))
    time.sleep(ti)
def worker4(ti):
    print("time is {0}".format(time.ctime()))
    time.sleep(ti)
if __name__=="__main__":
    print("the number of cpu is {0}".format(multiprocessing.cpu_count()))
    p1 = multiprocessing.Process(target=worker1,args = (4,))
    p2 = multiprocessing.Process(target=worker2,args = (3,))
    p3 = multiprocessing.Process(target=worker3,args = (2,))
    p4 = multiprocessing.Process(target=worker4,args = (1,))
    p1.start()
    p2.start()
    p3.start()
    p4.start()
    for p in multiprocessing.active_children():
        print("name is {0}, id is {1}".format(p.pid,p.name))
```
```python
#实例3：daemon
import multiprocessing
import time

def worker(ti):
    print("start time is {0}".format(time.ctime()))
    time.sleep(ti)
    print("end time is {0}".format(time.ctime()))
    
if __name__=="__main__":
    print("the number of cpu is {0}".format(multiprocessing.cpu_count()))
    p = multiprocessing.Process(target=worker,args = (3,))
    p.start()
    print("end!!!")
输出;
    end!!!
    start time is ...
    end tiem is...
    
#daemon:设置为True则意味着父结束子自动结束
import multiprocessing
import time

def worker(ti):
    print("start time is {0}".format(time.ctime()))
    time.sleep(ti)
    print("end time is {0}".format(time.ctime()))
    
if __name__=="__main__":
    print("the number of cpu is {0}".format(multiprocessing.cpu_count()))
    p = multiprocessing.Process(target=worker,args = (3,))
    p.daemon = True
    p.start()
    print("end!!!")
输出：end!!!
因为设置daemon为True：父进程结束后子进程也结束。
```

