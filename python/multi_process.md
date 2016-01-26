
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
#实例1
import multiprocessing
import time

def worker(ti):
    n=6
    while n>0:
        print("time is {0}".format(time.ctime()))
        time.sleep(ti)
        n-=1
    
if __name__=="__main__":
    p = multiprocessing.Process(target=worker,args = (3,))
    p.start()
    print("pid is {0}".format(p.pid))
    print("name is {0}".format(p.name))
    print("isalive is {0}".format(p.is_live()))
```

