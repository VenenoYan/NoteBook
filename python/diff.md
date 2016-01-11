## 主要是python2.X和python3.X的不同

1. 
输入：
```python
在python2.7中：input()和raw_input()都可以，而且input()由raw_input()实现
但在python3中，仅留下了input()方法```
1. 
输出：
```python
python2.7或之前，print只是语句而不是函数。  print "hello"
但python3之后，必须函数形式才行。    print("hello")
```
1. 
除法
```python
在python2.7前，‘/’代表floor除     3/2=1
python3后，‘/’代表除法(/、//无差)  3/2=1.5
当然可在python2.X中：from __future__ import division来使用Python3的除法或者强制转换(float)3/2、3/2.0
```
1. range()/xrange()
```python
对于range()和xrange()，python2.X是不同的。但是python3没有xrange()了，统一用range()。
而且range()有了一个新的__contains__方法。__contains__方法可以有效的加快整数和布尔型的“查找”速度。
　
x = 10000000
def val_in_range(x, val):
        return val in range(x)
　 
def val_in_xrange(x, val):
        return val in xrange(x)
%timeit val_in_range(x, x/2)　　　　　  ＃除法
%timeit val_in_range(x, x//2)           #地板除
执行结果：   整数比查找浮点数要快大约6万倍
1 loops, best of 3: 742 ms per loop
1000000 loops, best of 3: 1.19 µs per loop
```
1. 
异常
```python
首先是引起异常的方式：
        python2.X:  raise IOError, "file error"
                    raise IOError("file error")  #====>均可得到：IOError: file error
        python3.X： 仅支持括号
                    raise IOError, "file error"  #====>错误： SyntaxError: invalid syntax
                    raise IOError("file error")  #====>正确可得到：IOError: file error
    处理方式：
        python2.X:  在except语句块外面仍可以访问异常对象
                    try:
                        let_us_cause_a_NameError
                    except NameError, err:
                        print err, '--> our error message'
                    print err   #正确
        python3.X: 1）必须使用关键字as而且多个异常时必须用小括号(元组)，否则error；
                   2）在except代码块外面访问错误。
                    try:
                        let_us_cause_a_NameError
                    except (NameError,ValueError) as e:
                        print e.err, '--> our error message'
                    print e     #错误
```
1. 
比较操作
```python
python2.X:  [1,2]>"helo" 返回False
python3.X:  [1,2]>"helo" 引起异常
```
1. 
bool与int:
```python
2.X中bool是int的子集```