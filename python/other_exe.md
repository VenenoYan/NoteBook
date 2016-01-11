Python执行系统命令的方法: ```os.system()，os.popen()，commands```
```python
#test.sh
#!/bin/bash
echo "hello world!"
exit 3
```
1. 
os.system(cmd):
```python
该方法在调用完shell脚本后，返回一个16位的二进制数，低位为杀死所调用脚本的信号号码，高位为脚本的退出状态
码，即脚本中“exit 1”的代码执行后，os.system函数返回值的高位数则是1，如果低位数是0的情况下，则函数的返回值
是0×100,换算为10进制得到256。
如果我们需要获得os.system的正确返回值，那使用位移运算可以还原返回值：
n = os.system(test.sh)
n >> 8
3```
1. 
os.popen(cmd): 
```python
这种调用方式是通过管道的方式来实现，函数返回一个file-like的对象，里面的内容是脚本输出的内容
    （可简单理解为echo输出的内容）。```