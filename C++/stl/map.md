## stl_map.h
 Map是c++的一个标准容器，她提供了很好一对一的关系，在一些程序中建立一个map可以起到事半功倍的效果，总结了一些map基本简单实用的操作！
 
```C
0. 基本类型
    map<k,v>::key_type  键类型
    map<k,v>::mapped_type   值类型
    map<k,v>::value_type  键-值类型(first second)
1. map最基本的构造函数；
   map<string , int >mapstring;         
   map<int ,string >mapint(mapstring);
   map<k,v> m(b,e);
2. map添加数据； 
   maplive.insert(pair<int,string>(102,"aclive"));
   maplive.insert(make_pair(102,"aclive"));
   maplive.insert(beg,end);
   maplive.insert(iter,e);
   maplive[112]="April";    //map中最简单最常用的插入添加！
3，map中元素的查找：
   find()函数返回一个迭代器指向键值为key的元素，如果没找到就返回指向map尾部的迭代器。   
        maplive.find(112);
   find()函数返回出现的次数。   
        maplive.count(112);
4 map中元素的删除：
   m.clear()
   m.erase(k)   删除键为K的元素，返回删除的个数
   m.erase(iter)   删除iter指向的元素，返回void
   m.erase(b,e)   删除范围内的元素，返回void
5 map中 swap的用法：
  Map中的swap不是一个容器中的元素交换，而是两个容器交换；
6.map的sort问题：
  Map中的元素是自动按key升序排序,所以不能对map用sort函数：
7 map的基本操作函数：
      C++ Maps是一种关联式容器，包含“关键字/值”对
      begin()          返回指向map头部的迭代器
      end()            返回指向map末尾的迭代器   (first ,second)
      clear(）         删除所有元素
      count()          返回指定元素出现的次数
      empty()          如果map为空则返回true
      equal_range()    返回特殊条目的迭代器对
      erase()          删除一个元素
      find()           查找一个元素
      get_allocator()  返回map的配置器
      insert()         插入元素
      key_comp()       返回比较元素key的函数
      lower_bound()    返回键值>=给定元素的第一个位置
      max_size()       返回可以容纳的最大元素个数
      rbegin()         返回一个指向map尾部的逆向迭代器
      rend()           返回一个指向map头部的逆向迭代器
      size()           返回map中元素的个数
      swap()            交换两个map
      upper_bound()     返回键值>给定元素的第一个位置
      value_comp()      返回比较元素value的函数
```
