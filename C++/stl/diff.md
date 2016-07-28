```C
vector无的操作：
    push_front()
string无：
    front()
    back()
    pop_back()
    push_front()
    pop_front()
list无：
    除了  ++   --  ！=   == 之外，所有的算术运算和关系运算都不支持
```
```C
string 特有：
    substr
    append
    replace
    find
    compare
vector特有：
    capacity
    reserve
```

C++中的容器种类：

1. 
序列容器（7个）
    * 
vector：提供了自动内存管理功能（采用了STL普遍的内存管理器allocator），可以动态改变对象长度，提供随机访问。在尾部添加和删除元素的时间是常数的，但在头部或中间就是线性时间。
    * 
deque：双端队列（double-ended queue），支持随机访问，与vector类似，主要区别在于，从deque对象的开始位置插入和删除元素的时间也是常数的，所以若多数操作发生在序列的起始和结尾处，则应考虑使用deque数据结构。为实现在deque两端执行插入和删除操作的时间为常数时间这一目的，deque对象的设计比vector更为复杂，因此，尽管二者都提供对元素的随机访问和在序列中部执行线性时间的插入和删除操作，但vector容器执行这些操作时速度更快些。
    * 
list：双向链表（是循环的）。目的是实现快速插入和删除。
    * 
forward_list(C++11)：实现了单链表，不可反转。相比于list，forward_list更简单，更紧凑，但功能也更少。
    * 
queue：是一个适配器类。queue模板让底层类（默认是deque）展示典型的队列接口。queue模板的限制比deque更多，它不仅不允许随机访问队列元素，甚至不允许遍历队列。与队列相同，只能将元素添加到队尾、从队首删除元素、查看队首和队尾的值、检查元素数目和测试队列是否为空。
    * 
priority_queue：是另一个适配器类，支持的操作与queue相同。
        priority_queue模板类是另一个适配器类，它支持的操作与queue相同。两者之间的主要区别在于，在priority_queue中，最大的元素被移到对首。内部区别在于，默认的底层类是vector。可以修改用于确定哪个元素放到队首的比较方式，方法是提供一个可选的构造函数参数：
```C++
        priority_queue<int> pq1;                     // default version
        priority_queue<int> pg2(greater<int>);       // use greater<int> to order
        greater<>函数是一个预定义的函数对象。```

        stack：与queue相似，stack也是一个适配器类，它给底层类（默认情况下为vector）提供了典型的栈接口。
1. 
关联容器
        4种有序关联容器：set、multiset、map和multimap，底层基于树结构
        C++11又增加了4种无序关联容器：unordered_set、unordered_multiset、unordered_map和unordered_multimap，底层基于hash。



[返回目录](README.md)