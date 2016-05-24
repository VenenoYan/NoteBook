## [常用命令]()：
```C
运行的进程：ps aux    ps-ef
实时显示系统中各个进程的资源占用状况：top
查看服务对应端口：netstat -nlp
同步数据到硬盘：sync
显示开机信息：dmesg
查找grep：(global search regular expression(RE) and print out the line
    grep [-acinorvw] [--color=auto] '搜寻字符串' filename/*
        选项与参数：
        -a ：将 binary 文件以 text 文件的方式搜寻数据
        -c ：计算找到 '搜寻字符串' 的次数
        -i ：忽略大小写的不同，所以大小写视为相同
        -n ：顺便输出行号
        -o ：只显示正则表达式匹配的部分
        -r ：递归的读取目录下的所有文件，包括子目录。
        -v ：反向选择，亦即显示出没有 '搜寻字符串' 内容的那一行！
        -w ：精确匹配单词
        --color=auto ：可以将找到的关键词部分加上颜色的显示喔！
```
## OS
```C
互斥锁 读写锁  自旋锁  RCU锁     区别联系，应用举例
vim快捷键
```

统计出一个文件夹下面大小大于7MB的文件夹

[返回目录](README.md)