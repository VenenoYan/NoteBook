#Blog
<hr>

程序就是指令的集合，一个特定的指令序列。而一个指令的执行过程：```取指令->分析指令->执行->取下一条指令的循环。指令在内存中是顺序存放的，只要设置一个指令指针(IP)，每取一条就自加1即可指向下一个指令，只有在转移指令时才在指令中指出下一条指令的地址。```
```C
程序计数器(PC):程序开始时，将程序的起始地址送入PC中，执行指令时CPU自动修改PC内容，即要执行的下一条指令的地址
指令寄存器(IR)：CPU执行指令时，先把其从内存读到IR中暂存，指令译码器根据内容产生对应微操作，执行以完成所需功能。
```
[Example](http://m.blog.csdn.net/blog/u010926964/45693773)
### **源码到指令：**


##### 如何将一个用户源程序变为可在内存中执行的指令,通常都要经过以下几个步骤:

##### 1、 首先是要编译,由编译程序(Compiler)将用户源代码编译成若干个目标模块(ObjectModule:.o二进制文件);当然中间可以先编译成汇编文件，然后再编译汇编文件为目标模块。
            程序文件---->>汇编文件(可选)--[编译]-->>对应计算机指令集的指令(X86等)保存在代码区

##### 2、 其次是链接,由链接程序(Linker)将编译后形成的一组目标模块,以及它们所需要的库函数链接在一起,   形成一个完整的装入模块(Load Module);

##### 3 、最后是装入,由装入程序(Loader)将装入模块装入内存
编译程序一般都含有几个部分：即词法分析、语法分析/语义分析、中间代码生成、代码优化程序、目标代码生成、错误检查和处理以及各种信息表格的管理。


### 程序的运行

首先是OS为其新建一个进程，然后进程装入已编译和链接的模块：内存代码区加载到IC，从IC取指令解析，decode成uops,然后rename分析依赖&allocate分配执行和ROB空间,最后经调度进入执行单元，执行完后进入ROB以正常顺序结束。

### **内存的分区**


* 
**代码区**　　存放代码(指令序列)
* 
**全局数据区 **　　存放全局变量（在编译阶段就会把分配空间。按照声明变量的字母顺序按照空间递增顺序）
* 
**堆 ** 　　　　动态预留的内存空间：函数运行过程中，使用malloc或new等申请，delete自己释放。
* 
**栈  **　　　　存放局部变量和函数参数(局部变量分配空间的顺序跟变量的声明顺序直接相关，同时按照内存由高到低递减的顺序分配。只有当定义它们的程序块被调用时（即执行时），才分配空间，**声明或定义时并不分配内存**
    1. 
**堆**：应用程序(进程)运行时动态分配(预留的内存空间)；由自己申请和释放；较慢；出入无限制
    1. 
**栈**：为执行线程留出的空间；附属于线程，线程自己控制(进程创建时分配大小，退出时回收)；较快；先入后出
================>>   多线程:各自有自己的栈,但是共享堆
<hr>

### **常见命名法：**

**匈牙利命名：**
开头字母用变量类型的缩写，其余部分用变量的英文或英文的缩写，要求单词第一个字母大写。
<br>　　　　　　　For example: long lSum = 0;　　//　"l"是类型的缩写；<br>
**小驼峰式：**
第一个单词首字母小写，后面其他单词首字母大写。
<br>　　　　　　　For example: string firstName = string.Empty;<br>
**大驼峰式：**
每个单词的第一个字母都大写;
<br>　　　　　　　For example：string FirstName = string.Empty<br>
##　　　　　     　　　　　　　　　　　　　　 　　　　---By　Leo


