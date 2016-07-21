###几个函数
* 
malloc：申请一段内存，不初始化
* 
calloc：申请一段内存，初始化为0
* 
realloc：重新对原有的空间，分配大小。一般是扩容：realloc(pt, 1000*sizeof(char));
* 
alloca：最特殊的开辟栈空间方法，优点是当离开调用这个函数的时候，栈所分配的空间会自动释放（也就是free）

###Linux通过slab容器分配task_struct结构，这样能达到对象复用和缓存着色的目的”
* 
task_struct：学过操作系统的知道，每个进程都有一个PCB（process control block），是控制进程的唯一也是最有效的手段；在调用fork()函数创建新的进程时时系统自动为我们创建的。
* 
slab分配器：某些对象（如进程描述符等）由于频繁的申请和释放内存，而它们很小，那么很可能就出现很多的内部碎片而且分配效率和速度都不好；而slab分配器正是基于对象进行管理的，对于相同的对象归为一类，当申请时从一个slab列表中分配，回收时再加入进来，减少碎片，也减少频繁的申请和释放内存调用；
 slab分配器使用slab分配算法进行实现并采用空间换时间的方式提高分配效率
* 
对象复用 ：对象就是对象，而复用指的是
slab分配器对于已分配的对象并不丢弃，而是释放并把它们保存在内存中。这样当以后又要请求新的对象时，就可以从内存直接获取而不用重复初始化。=======》像不像Java中申请内存
* 
slab缓解内部碎片问题，buddy算法负责外部碎片问题


###[内存分配](http://blog.csdn.net/littlehedgehog/article/details/2856933)
内存的延迟分配：用户申请内存的时候，只是给它分配了一个线性区（也就是虚存），并没有分配实际物理内存；只有当用户使用这块内存的时候，内核才会分配具体的物理页面给用户，这时候才占用宝贵的物理内存。内核释放物理页面是通过释放线性区，找到其所对应的物理页面，将其全部释放的过程。
* 
分配和释放的调用：brk(小于128K),sbrk,mmap(大于128K),unmmap。而它们的参数就是虚拟内存
```C
char *p=malloc(2048); //这里只是分配了虚拟内存2048，并不占用实际内存。 
strcpy(p,”123”) ;//分配了物理页面，虽然只是使用了3个字节，但内存还是为它分配了2048字节的物理内存。 
free(p) ;//通过虚拟地址，找到其所对应的物理页面，释放物理页面，释放线性区。  
```
但并不是每次申请是否都系统调用，glibc负责批发和零售

##glibc的malloc内部机制
可以先运行下面的程序，会发现：16、24、32、40(32Bit系统)；32、48、64(64Bit系统)；会有跳变<br>当然也可以用top命令重点才看res(Resident size)指标

```C
#include <stdio.h>
#include <stdlib.h>
void main()
{
    char *p1;
    char *p2;
    int i=1;
    printf("%d\n",sizeof(char *));
    for(;i<100;i++)
    {
        p1=NULL;
        p2=NULL;
        p1=(char *)malloc(i*sizeof(char));
        p2=(char *)malloc(1*sizeof(char));
        printf("i=%d     %d\n",i,(p2-p1));   //两个指针的距离===得到内存布局
    }

    getchar();
}
```
####为什么会这样？
不是申请多少用多少吗？从上面知道glibc是批发和零售的，所以不会每次都去“进货”，那么一次批发多少？
<br>通过查看glibc源码中malloc.c可知：
```C
#ifndef INTERNAL_SIZE_T  
#define INTERNAL_SIZE_T size_t  
#endif  
#define SIZE_SZ                (sizeof(INTERNAL_SIZE_T))  
#ifndef MALLOC_ALIGNMENT  
#define MALLOC_ALIGNMENT       (2 * SIZE_SZ)  
#endif  

/*===================================================================
    MALLOC_ALIGNMENT：是不是对齐单位？
    不是，这个是每次申请空间大于阀值(下面的MINSIZE)时，补充的大小；
===================================================================*/
//注：在glibc中空闲的内存块会由双链表连起来，每个链表结点就是一个管理单元，它的结构定义如下：

struct malloc_chunk {  
  INTERNAL_SIZE_T      prev_size;  /* Size of previous chunk (if free).  */  
  INTERNAL_SIZE_T      size;       /* Size in bytes, including overhead. */  
  struct malloc_chunk* fd;         /* double links -- used only if free. */  
  struct malloc_chunk* bk;  
};  

/*=================================================================================
    An allocated chunk looks like this:  
    chunk-> +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+  
            |             Size of previous chunk, if allocated            | |  
            +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+  
            |             Size of chunk, in bytes                       |M|P|  
      mem-> +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+  
            |             User data starts here...                          .  
            .                                                               .  
            .             (malloc_usable_size() bytes)                      .  
            .                                                               |  
nextchunk-> +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+  
            |             Size of chunk                                     |  
            +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+  
*    由上可知，使用malloc时消耗系统内存的最小单位就是sizeof(struct malloc_chunk)。
*   实际上，差不多就是这样，只是还需要将sizeof(struct malloc_chunk)作内存对齐。
===============================================================================================*/           
            
#define MALLOC_ALIGN_MASK      (MALLOC_ALIGNMENT - 1)  
#define MIN_CHUNK_SIZE        (sizeof(struct malloc_chunk))  
#define MINSIZE  /  
  (unsigned long)(((MIN_CHUNK_SIZE+MALLOC_ALIGN_MASK) & ~MALLOC_ALIGN_MASK))  
/* pad request bytes into a usable size -- internal version */  
#define request2size(req)                                         /  
  (((req) + SIZE_SZ + MALLOC_ALIGN_MASK < MINSIZE)  ?             /  
   MINSIZE :                                                      /  
   ((req) + SIZE_SZ + MALLOC_ALIGN_MASK) & ~MALLOC_ALIGN_MASK)
/*===================================================================
    从上可知：
        1）32Bit系统下MINSIZE大小是16B，其中去掉4B(即SIZE_SZ)的保留大小，用户可以使用的12B；
            而当申请13B时，request2size发现大于MINSIZE大小，就额外分配MALLOC_ALIGNMENT(8B)大小；
            所以才会有16、24、32、40等关键值；
            申请：0~12B时，分配16B；
                  13~20B时，分配24B；
                为什么不是13~24B？因为我们指定，扩充每次扩充MALLOC_ALIGNMENT大小，所以只额外多了8B；
        2）64Bit系统下MINSIZE大小是32B，其中去掉8B的保留大小，用户可以使用的24B；
            而当申请25B时，request2size发现大于MINSIZE大小，就额外分配MALLOC_ALIGNMENT(16B)大小；
            所以才会有32、48、64等关键值；
            申请：0~24B时，分配32B；
                  25~40B时，分配48B；
                为什么不是25~48B？因为我们指定，扩充每次扩充MALLOC_ALIGNMENT大小，所以只额外多了16B；
===================================================================*/
```
* 
C++中的new底层也是用的malloc实现的
    ```C++
    #include <vector>  
    using namespace std;  
    int main(int argc, char *argv[])  
    {  
        int malloc_size = atoi(argv[1]);  
        vector<char *> malloc_vec(1 * 1024 * 1024);  
        for (size_t i = 0; i < malloc_vec.size(); ++i) {  
            malloc_vec[i] = new char[malloc_size];  
        }  
        while (1) {}  
        return 0;  
    }  
    输入23，25会top命令查看内存使用，发现40、56M出跳变：原因vector本身占用8M，剩余32M、48M。同理！！！
    ```
张状_zhangzhuang24@163.com_13161064957_中科院软件所_计算机技术_来自牛客网推荐
实习期间参加微架构模拟器的设计，自己对CPU微架构的知识从一无所知到慢慢入手实现，学习能力和理解能力得到肯定，同和团队合作也提高了我表述自己和理解他人的能力。

1）研究生期间作为学生会体育部部长，以发起人和负责人身份组织中国科学院大学第一届学生运动会，同时还顺利举办了篮球赛、羽毛球赛等，而且有时候不仅仅需要自己部门参与，还要调动整个学生会参与（比如运动会），自己与人交流以及处理应急事件的能力得到锻炼；
2）个人很喜欢玩游戏，更喜欢研究游戏，比如大学期间玩穿越火线，当时我们不仅仅玩游戏，还会对游戏进行研究比如打玩家身体那一个部分掉血比较多，然后找到杀人效率比较高的那条准线，最后在南京赛区获得第二名；
3）实习期间参与过整个项目的开发流程，表达自己和理解别人的能力有很大的提高；）实习期间参与过整个项目的开发流程，表达自己和理解别人的能力有很大的提高；


[返回目录](README.md)