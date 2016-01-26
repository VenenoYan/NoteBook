
## 多进程


在python中多线程并不是真正的多线程，只是体现在CPU的快速切换上，如果想真正利用多核CPU，就要使用多进程。

### 创建
```python
Process([group[,target[,name[,args[,kwargs]]]]]):
    group  一般不用
    target 调用的对象
    name    别名
    args    参数
    kwargs  字典
```

