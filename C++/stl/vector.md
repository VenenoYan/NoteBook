## stl_vector.h
```C++
vector是C++标准模板库中模板。它是一个多功能的，能够操作多种数据结构和算法的模板类和函数库。
vector之所以被认为是一个容器，是因为它能够像容器一样存放各种类型的对象，
简单地说，vector是一个能够存放任意类型的动态数组，能够增加和压缩数据。
　　简单的使用方法如下:
　　vector<int> test;//建立一个vector
　　test.pushback(1);//把1和2压入vector 这样test[0]就是1,test[1]就是2
　　test.pushback(2);
　　我们可以用一个迭代器：
　　vector<int>::iterator iter=text.begin();//定义一个可以迭代int型vector的迭代器iter，它指向text的首位
为了可以使用vector，必须在你的头文件中包含下面的代码：
　　#include <vector>
　　函数表述
　　c.assign(beg,end)   将[beg; end)区间中的数据赋值给c（beg,end不可是C的）
    c.assign(n,elem)    将n个elem的拷贝赋值给c
　　
　　c.at(idx)
　　传回索引idx所指的数据，如果idx越界，抛出out_of_range。
　　c.back()
　　传回最后一个数据，不检查这个数据是否存在。
　　c.begin()
　　传回迭代器中的第一个数据地址。
　　c.capacity()
　　返回容器中数据个数。
　　c.clear()
　　移除容器中所有数据。
　　c.empty()
　　判断容器是否为空。
　　c.end()
　　指向迭代器中末端元素的下一个，指向一个不存在元素。
　　c.erase(pos)
　　c.erase(beg,end)
　　删除pos位置的数据，传回下一个数据的位置。
　　删除(beg,end)区间的数据，传回下一个数据的位置。
　　c.front()
　　传回第一个数据。
　　get_allocator
　　使用构造函数返回一个拷贝。
　　c.insert(pos,elem)
　　c.insert(pos,n,elem)
　　c.insert(pos,beg,end)
　　在pos位置插入一个elem拷贝，传回新数据位置。在pos位置插入n个elem数据。无返回值。在pos位置插入在[beg,end)区间的数据。无返回值。
iterator insert( iterator loc, const TYPE &val ); 
void insert( iterator loc, size_type num, const TYPE &val ); 
void insert( iterator loc, input_iterator start, input_iterator end ); 

insert() 函数有以下三种用法: 

在指定位置loc前插入值为val的元素,返回指向这个元素的迭代器, 
在指定位置loc前插入num个值为val的元素 
在指定位置loc前插入区间[start, end)的所有元素 . 
举例: 

//创建一个vector,置入字母表的前十个字符 
vector <char> alphaVector; 
for( int i=0; i < 10; i++ ) 
  alphaVector.push_back( i + 65 ); 

//插入四个C到vector中 
vector <char>::iterator theIterator = alphaVector.begin(); 
alphaVector.insert( theIterator, 4, 'C' ); 

//显示vector的内容 
for( theIterator = alphaVector.begin(); theIterator != alphaVector.end(); theIterator++ ) 
  cout < < *theIterator; 

这段代码将显示:

CCCCABCDEFGHIJ

　　c.max_size()
　　返回容器中最大数据的数量。
　　c.pop_back()
　　删除最后一个数据。
　　c.push_back(elem)
　　在尾部加入一个数据。
　　c.rbegin()
　　传回一个逆向队列的第一个数据。
　　c.rend()
　　传回一个逆向队列的最后一个数据的下一个位置。
　　c.resize(num)
　　重新指定队列的长度。
　　c.reserve()
　　保留适当的容量。
　　c.size()
　　返回容器中实际数据的个数。
　　c1.swap(c2)
　　swap(c1,c2)
　　将c1和c2元素互换。同上操作。
　　vector<Elem>
　　cvector<Elem> c1(c2)
　　vector <Elem> c(n)
　　ector <Elem> c(n, elem)
　　vector <Elem> c(beg,end)
　　c.~ vector <Elem>()
　　创建一个空的vector。复制一个vector。创建一个vector，含有n个数据，数据均已缺省构造产生。创建一个含有n个elem拷贝的vector。创建一个以[beg;end)区间的vector。销毁所有数据，释放内存。
　　operator[]
　　返回容器中指定位置的一个引用。
　　创建一个vector
　　vector容器提供了多种创建方法，下面介绍几种常用的。
　　创建一个Widget类型的空的vector对象：
　　vector<Widget> vWidgets;
　　创建一个包含500个Widget类型数据的vector：
　　vector<Widget> vWidgets(500);
　　创建一个包含500个Widget类型数据的vector，并且都初始化为0：
　　vector<Widget> vWidgets(500, Widget(0));
　　创建一个Widget的拷贝：
　　vector<Widget> vWidgetsFromAnother(vWidgets);
　　向vector添加一个数据
　　vector添加数据的缺省方法是push_back()。push_back()函数表示将数据添加到vector的尾部，并按需要来分配内存。例如：向vector<Widget>中添加10个数据，需要如下编写代码：
　　for(int i= 0;i<10; i++) {
　　vWidgets.push_back(Widget(i));
　　}
　　获取vector中制定位置的数据
　　vector里面的数据是动态分配的，使用push_back()的一系列分配空间常常决定于文件或一些数据源。如果想知道vector存放了多少数据，可以使用empty()。获取vector的大小，可以使用size()。例如，如果想获取一个vector v的大小，但不知道它是否为空，或者已经包含了数据，如果为空想设置为-1，你可以使用下面的代码实现：
　　int nSize = v.empty() ? -1 : static_cast<int>(v.size());
　　访问vector中的数据
　　使用两种方法来访问vector。
　　1、 vector::at()
　　2、 vector::operator[]
　　operator[]主要是为了与C语言进行兼容。它可以像C语言数组一样操作。但at()是我们的首选，因为at()进行了边界检查，如果访问超过了vector的范围，将抛出一个例外。由于operator[]容易造成一些错误，所有我们很少用它，下面进行验证一下：
　　分析下面的代码：
　　vector<int> v;
　　v.reserve(10);
　　for(int i=0; i<7; i++) {
　　v.push_back(i);
　　}
　　try {int iVal1 = v[7];
　　// not bounds checked - will not throw
　　int iVal2 = v.at(7);
　　// bounds checked - will throw if out of range
　　} catch(const exception& e) {
　　cout << e.what();
　　}
　　删除vector中的数据
　　vector能够非常容易地添加数据，也能很方便地取出数据，同样vector提供了erase()，pop_back()，clear()来删除数据，当删除数据时，应该知道要删除尾部的数据，或者是删除所有数据，还是个别的数据。
　　Remove_if()算法 如果要使用remove_if()，需要在头文件中包含如下代码：：
　　#include <algorithm>
　　Remove_if()有三个参数：
　　1、 iterator _First：指向第一个数据的迭代指针。
　　2、 iterator _Last：指向最后一个数据的迭代指针。
　　3、 predicate _Pred：一个可以对迭代操作的条件函数。
　　条件函数
　　条件函数是一个按照用户定义的条件返回是或否的结果，是最基本的函数指针，或是一个函数对象。这个函数对象需要支持所有的函数调用操作，重载operator()()操作。remove_if()是通过unary_function继承下来的，允许传递数据作为条件。
　　例如，假如想从一个vector<CString>中删除匹配的数据，如果字串中包含了一个值，从这个值开始，从这个值结束。首先应该建立一个数据结构来包含这些数据，类似代码如下：
　　#include <functional>
　　enum findmodes {
　　FM_INVALID = 0,
　　FM_IS,
　　FM_STARTSWITH,
　　FM_ENDSWITH,
　　FM_CONTAINS
　　};
　　typedef struct tagFindStr {
　　UINT iMode;
　　CString szMatchStr;
　　} FindStr;
　　typedef FindStr* LPFINDSTR;
　　然后处理条件判断：
　　class FindMatchingString : public std::unary_function<CString, bool> {
　　public:
　　FindMatchingString(const LPFINDSTR lpFS) :
　　m_lpFS(lpFS) {
　　}
　　bool operator()(CString& szStringToCompare) const {
　　bool retVal = false;
　　switch (m_lpFS->iMode) {
　　case FM_IS: {
　　retVal = (szStringToCompare == m_lpFDD->szMatchStr);
　　break;
　　}
　　case FM_STARTSWITH: {
　　retVal = (szStringToCompare.Left(m_lpFDD->szMatchStr.GetLength())
　　== m_lpFDD->szWindowTitle);
　　break;
　　}
　　case FM_ENDSWITH: {
　　retVal = (szStringToCompare.Right(m_lpFDD->szMatchStr.GetLength())
　　== m_lpFDD->szMatchStr);
　　break;
　　}
　　case FM_CONTAINS: {
　　retVal = (szStringToCompare.Find(m_lpFDD->szMatchStr) != -1);
　　break;
　　}
　　}
　　return retVal;
　　}
　　private:
　　LPFINDSTR m_lpFS;
　　};
　　通过这个操作你可以从vector中有效地删除数据：
　　FindStr fs;
　　fs.iMode = FM_CONTAINS;
　　fs.szMatchStr = szRemove;
　　vs.erase(std::remove_if(vs.begin(), vs.end(), FindMatchingString(&fs)), vs.end());
　　Remove(),remove_if()等所有的移出操作都是建立在一个迭代范围上的，不能操作容器中的数据。所以在使用remove_if()，实际上操作的时容器里数据的上面的。
　　看到remove_if()实际上是根据条件对迭代地址进行了修改，在数据的后面存在一些残余的数据，那些需要删除的数据。剩下的数据的位置可能不是原来的数据，但他们是不知道的。
　　调用erase()来删除那些残余的数据。注意上面例子中通过erase()删除remove_if()的结果和vs.enc()范围的数据。

例子：
// vector.cpp : Defines the entry point for the console application.

#include<iostream>
using namespace std;
#include<vector>
#include<algorithm>
#include<fstream>
int bitsquaresum(int a)
{
int sum=0;
for(int temp=a;temp;temp/=10)//计算每位数的各位数字的平方和
   sum+=(temp)*(temp);
return sum;
}
bool maxthanbitsum(int a,int b)
{
return bitsquaresum(a)<bitsquaresum(b);
}
void print(vector <int> data )//输出向量函数
{
for(int i=0;i<data.size();i++)
   cout<<data[i]<<" ";
}
int main(int argc, char* argv[])
{
vector<int> data;         //定义向量vector
ifstream in("abc.txt");
cout<<"===============bit square sum as follows======================/n"<<endl;
for(int a;in>>a;)         //将文件中的数据输入到a中
{
   data.push_back(a);    //在向量vector最后插入元素a  
   cout<<a<<"="<<bitsquaresum(a)<<'/t';//输出每位数的各位数字的平方之和
}
cout<<endl<<"/n========================The primary's data====================================/n"<<endl;
print(data);
cout<<endl<<endl<<endl;
sort(data.begin(),data.end(),maxthanbitsum);
cout<<"===========form min to max sort result as follows================/n"<<endl;
for(int i=0;i<data.size();i++)
   cout<<data[i]<<'/t';
cout<<endl<<endl<<endl;
return 0;
}```
```C
// Filename:    stl_vector.h

/*
 *
 * Copyright (c) 1994
 * Hewlett-Packard Company
 *
 * Permission to use, copy, modify, distribute and sell this software
 * and its documentation for any purpose is hereby granted without fee,
 * provided that the above copyright notice appear in all copies and
 * that both that copyright notice and this permission notice appear
 * in supporting documentation.  Hewlett-Packard Company makes no
 * representations about the suitability of this software for any
 * purpose.  It is provided "as is" without express or implied warranty.
 *
 *
 * Copyright (c) 1996
 * Silicon Graphics Computer Systems, Inc.
 *
 * Permission to use, copy, modify, distribute and sell this software
 * and its documentation for any purpose is hereby granted without fee,
 * provided that the above copyright notice appear in all copies and
 * that both that copyright notice and this permission notice appear
 * in supporting documentation.  Silicon Graphics makes no
 * representations about the suitability of this software for any
 * purpose.  It is provided "as is" without express or implied warranty.
 */

/* NOTE: This is an internal header file, included by other STL headers.
 *   You should not attempt to use it directly.
 */

#ifndef __SGI_STL_INTERNAL_VECTOR_H
#define __SGI_STL_INTERNAL_VECTOR_H

__STL_BEGIN_NAMESPACE

#if defined(__sgi) && !defined(__GNUC__) && (_MIPS_SIM != _MIPS_SIM_ABI32)
#pragma set woff 1174
#endif


////////////////////////////////////////////////////////////////////////////////
//
////////////////////////////////////////////////////////////////////////////////


// 默认allocator为alloc, 其具体使用版本请参照<stl_alloc.h>
template <class T, class Alloc = alloc>
class vector
{
public:
  // 标记为'STL标准强制要求'的typedefs用于提供iterator_traits<I>支持
  typedef T value_type;                         // STL标准强制要求
  typedef value_type* pointer;                  // STL标准强制要求
  typedef const value_type* const_pointer;
  // 由于vector的特性, 一般我们实作的时候都分配给其连续的内存空间,
  // 所以其迭代器只需要定义成原生指针即可满足需要
  typedef value_type* iterator;                 // STL标准强制要求
  typedef const value_type* const_iterator;
  typedef value_type& reference;                // STL标准强制要求
  typedef const value_type& const_reference;
  typedef size_t size_type;
  typedef ptrdiff_t difference_type;            // STL标准强制要求

#ifdef __STL_CLASS_PARTIAL_SPECIALIZATION
  typedef reverse_iterator<const_iterator> const_reverse_iterator;
  typedef reverse_iterator<iterator> reverse_iterator;
#else /* __STL_CLASS_PARTIAL_SPECIALIZATION */
  typedef reverse_iterator<const_iterator, value_type, const_reference,
                           difference_type>  const_reverse_iterator;
  typedef reverse_iterator<iterator, value_type, reference, difference_type>
          reverse_iterator;
#endif /* __STL_CLASS_PARTIAL_SPECIALIZATION */

protected:
  // 这个提供STL标准的allocator接口
  typedef simple_alloc<value_type, Alloc> data_allocator;

  iterator start;               // 内存空间起始点
  iterator finish;              // 当前使用的内存空间结束点
  iterator end_of_storage;      // 实际分配内存空间的结束点

  void insert_aux(iterator position, const T& x);

  // 释放分配的内存空间
  void deallocate()
  {
    // 由于使用的是data_allocator进行内存空间的分配,
    // 所以需要同样嗲用data_allocator::deallocate()进行释放
    // 如果直接释放, 对于data_allocator内部使用内存池的版本
    // 就会发生错误
    if (start) data_allocator::deallocate(start, end_of_storage - start);
  }

  void fill_initialize(size_type n, const T& value)
  {
    start = allocate_and_fill(n, value);
    finish = start + n;                         // 设置当前使用内存空间的结束点
    // 构造阶段, 此实作不多分配内存,
    // 所以要设置内存空间结束点和, 已经使用的内存空间结束点相同
    end_of_storage = finish;
  }

public:
  // 获取几种迭代器
  iterator begin() { return start; }
  const_iterator begin() const { return start; }
  iterator end() { return finish; }
  const_iterator end() const { return finish; }
  reverse_iterator rbegin() { return reverse_iterator(end()); }
  const_reverse_iterator rbegin() const {
    return const_reverse_iterator(end());
  }
  reverse_iterator rend() { return reverse_iterator(begin()); }
  const_reverse_iterator rend() const {
    return const_reverse_iterator(begin());
  }

  // 返回当前对象个数
  size_type size() const { return size_type(end() - begin()); }
  size_type max_size() const { return size_type(-1) / sizeof(T); }
  // 返回重新分配内存前最多能存储的对象个数
  size_type capacity() const { return size_type(end_of_storage - begin()); }
  bool empty() const { return begin() == end(); }
  reference operator[](size_type n) { return *(begin() + n); }
  const_reference operator[](size_type n) const { return *(begin() + n); }

  // 本实作中默认构造出的vector不分配内存空间
  vector() : start(0), finish(0), end_of_storage(0) {}

////////////////////////////////////////////////////////////////////////////////
// 本实作中给定个数和对象, 则只分配所需内存, 不会多分配
////////////////////////////////////////////////////////////////////////////////
//                    vector(size_type n, const T& value)
//                                   ↓
//                         fill_initialize(n, value)
//                                   ↓
//                        allocate_and_fill(n, value)
//                                   ↓
//          data_allocator::allocate(n)          <stl_alloc.h>
//          uninitialized_fill_n(result, n, x)  <stl_uninitialized.h>
////////////////////////////////////////////////////////////////////////////////

  vector(size_type n, const T& value) { fill_initialize(n, value); }
  vector(int n, const T& value) { fill_initialize(n, value); }
  vector(long n, const T& value) { fill_initialize(n, value); }

  // 需要对象提供默认构造函数
  explicit vector(size_type n) { fill_initialize(n, T()); }

////////////////////////////////////////////////////////////////////////////////
// 复制构造, 同样不会多分配内存
////////////////////////////////////////////////////////////////////////////////
//                     vector(const vector<T, Alloc>& x)
//                                   ↓
//         allocate_and_copy(x.end() - x.begin(), x.begin(), x.end());
//                                   ↓
//        data_allocator::allocate(n)              <stl_alloc.h>
//        uninitialized_copy(first, last, result); <stl_uninitialized.h>
////////////////////////////////////////////////////////////////////////////////

  vector(const vector<T, Alloc>& x)
  {
    start = allocate_and_copy(x.end() - x.begin(), x.begin(), x.end());
    finish = start + (x.end() - x.begin());
    end_of_storage = finish;
  }

// 复制指定区间的元素, 同样不多分配内存
#ifdef __STL_MEMBER_TEMPLATES
////////////////////////////////////////////////////////////////////////////////
// 复制一个区间进行构造, 可能会导致多分配内存
////////////////////////////////////////////////////////////////////////////////
//               vector(InputIterator first, InputIterator last)
//                                   ↓
//            range_initialize(first, last, iterator_category(first));
//                                   ↓
//                     for ( ; first != last; ++first)
//                         push_back(*first);
//            由于使用push_back()操作, 可能导致多次重复分配内存,个人感觉应该先
//            data_allocator::allocate((last - first) * sizeof(T));
//            然后uninitialized_copy(first, last, result);
//            这样不会多分配内存， 也不会导致多次重新分配内存问题
////////////////////////////////////////////////////////////////////////////////

  template <class InputIterator>
  vector(InputIterator first, InputIterator last) :
    start(0), finish(0), end_of_storage(0)
  {
    range_initialize(first, last, iterator_category(first));
  }
#else /* __STL_MEMBER_TEMPLATES */

////////////////////////////////////////////////////////////////////////////////
// 复制一个区间进行构造, 可能会导致多分配内存
////////////////////////////////////////////////////////////////////////////////
//              vector(const_iterator first, const_iterator last)
//                                   ↓
//                        distance(first, last, n);
//                                   ↓
//                      allocate_and_copy(n, first, last);
//                                   ↓
//       data_allocator::allocate(n)               <stl_alloc.h>
//       uninitialized_copy(first, last, result);  <stl_uninitialized.h>
////////////////////////////////////////////////////////////////////////////////

  vector(const_iterator first, const_iterator last) {
    size_type n = 0;
    distance(first, last, n);
    start = allocate_and_copy(n, first, last);
    finish = start + n;
    end_of_storage = finish;
  }
#endif /* __STL_MEMBER_TEMPLATES */

  ~vector()
  {
    // 析构对象
    destroy(start, finish);
    // 释放内存
    deallocate();
  }

  vector<T, Alloc>& operator=(const vector<T, Alloc>& x);

////////////////////////////////////////////////////////////////////////////////
// 预留一定空间, 如果n < capacity(), 并不会减少空间
////////////////////////////////////////////////////////////////////////////////
//                          reserve(size_type n)
//                                   ↓
//                   allocate_and_copy(n, start, finish)
//                   destroy(start, finish);               <stl_construct.h>
//                   deallocate();
////////////////////////////////////////////////////////////////////////////////

  void reserve(size_type n)
  {
    if (capacity() < n) {
      const size_type old_size = size();
      iterator tmp = allocate_and_copy(n, start, finish);
      destroy(start, finish);
      deallocate();
      start = tmp;
      finish = tmp + old_size;
      end_of_storage = start + n;
    }
  }

  // 提供访问函数
  reference front() { return *begin(); }
  const_reference front() const { return *begin(); }
  reference back() { return *(end() - 1); }
  const_reference back() const { return *(end() - 1); }

////////////////////////////////////////////////////////////////////////////////
// 向容器尾追加一个元素, 可能导致内存重新分配
////////////////////////////////////////////////////////////////////////////////
//                          push_back(const T& x)
//                                   |
//                                   |---------------- 容量已满?
//                                   |
//               ----------------------------
//           No  |                          |  Yes
//               |                          |
//               ↓                          ↓
//      construct(finish, x);       insert_aux(end(), x);
//      ++finish;                           |
//                                          |------ 内存不足, 重新分配
//                                          |       大小为原来的2倍
//      new_finish = data_allocator::allocate(len);       <stl_alloc.h>
//      uninitialized_copy(start, position, new_start);   <stl_uninitialized.h>
//      construct(new_finish, x);                         <stl_construct.h>
//      ++new_finish;
//      uninitialized_copy(position, finish, new_finish); <stl_uninitialized.h>
////////////////////////////////////////////////////////////////////////////////

  void push_back(const T& x)
  {
    // 内存满足条件则直接追加元素, 否则需要重新分配内存空间
    if (finish != end_of_storage) {
      construct(finish, x);
      ++finish;
    }
    else
      insert_aux(end(), x);
  }

  // 交换两个vector, 实际上是交换内部的状态指针
  void swap(vector<T, Alloc>& x)
  {
    __STD::swap(start, x.start);
    __STD::swap(finish, x.finish);
    __STD::swap(end_of_storage, x.end_of_storage);
  }

////////////////////////////////////////////////////////////////////////////////
// 在指定位置插入元素
////////////////////////////////////////////////////////////////////////////////
//                   insert(iterator position, const T& x)
//                                   |
//                                   |------------ 容量是否足够 && 是否是end()?
//                                   |
//               -------------------------------------------
//            No |                                         | Yes
//               |                                         |
//               ↓                                         ↓
//    insert_aux(position, x);                  construct(finish, x);
//               |                              ++finish;
//               |-------- 容量是否够用?
//               |
//        --------------------------------------------------
//    Yes |                                                | No
//        |                                                |
//        ↓                                                |
// construct(finish, *(finish - 1));                       |
// ++finish;                                               |
// T x_copy = x;                                           |
// copy_backward(position, finish - 2, finish - 1);        |
// *position = x_copy;                                     |
//                                                         ↓
// data_allocator::allocate(len);                       <stl_alloc.h>
// uninitialized_copy(start, position, new_start);      <stl_uninitialized.h>
// construct(new_finish, x);                            <stl_construct.h>
// ++new_finish;
// uninitialized_copy(position, finish, new_finish);    <stl_uninitialized.h>
// destroy(begin(), end());                             <stl_construct.h>
// deallocate();
////////////////////////////////////////////////////////////////////////////////

  iterator insert(iterator position, const T& x)
  {
    size_type n = position - begin();
    if (finish != end_of_storage && position == end()) {
      construct(finish, x);
      ++finish;
    }
    else
      insert_aux(position, x);
    return begin() + n;
  }

  iterator insert(iterator position) { return insert(position, T()); }

#ifdef __STL_MEMBER_TEMPLATES
////////////////////////////////////////////////////////////////////////////////
// 在指定位置插入一个区间
////////////////////////////////////////////////////////////////////////////////
//     insert(iterator position, InputIterator first, InputIterator last)
//                                   ↓
//       range_insert(position, first, last, iterator_category(first));
//                                   ↓
//                      for ( ; first != last; ++first) {
//                              pos = insert(pos, *first);
//                               ++pos;
//                      }
////////////////////////////////////////////////////////////////////////////////

  template <class InputIterator>
  void insert(iterator position, InputIterator first, InputIterator last)
  {
    range_insert(position, first, last, iterator_category(first));
  }
#else /* __STL_MEMBER_TEMPLATES */
  void insert(iterator position,
              const_iterator first, const_iterator last);
#endif /* __STL_MEMBER_TEMPLATES */

  void insert (iterator pos, size_type n, const T& x);

  void insert (iterator pos, int n, const T& x)
  {
    insert(pos, (size_type) n, x);
  }

  void insert (iterator pos, long n, const T& x)
  {
    insert(pos, (size_type) n, x);
  }

  void pop_back()
  {
    --finish;
    destroy(finish);
  }

  iterator erase(iterator position)
  {
    if (position + 1 != end())
      copy(position + 1, finish, position);
    --finish;
    destroy(finish);
    return position;
  }

////////////////////////////////////////////////////////////////////////////////
// 擦除指定区间的元素
////////////////////////////////////////////////////////////////////////////////
//                 erase(iterator first, iterator last)
//                                   ↓
//           ---------- copy(last, finish, first);      <stl_algobase.h>
//           |          destroy(i, finish);             <stl_construct.h>
//           |
//           |                                  -------------- copy(...)
//           |          特化                    |  char *特化   memmove()
//      ---------------------------------------|
//      |  泛化                                 |  wchar_t特化  copy(...)
//      |                                       -------------- memmove()
//      |
// 调用__copy_dispatch<InputIterator,OutputIterator>()(first, last, result);
// 进行__copy(first, last, result, iterator_category(first));派发
//      |
//      |
//      |                       random_access_iterator_tag
// --------------------------------------------------------------
// |  input_iterator_tag                                        |
// |                                                            |
// ↓                                                            |
// __copy(..., input_iterator_tag)                              |
// for ( ; first != last; ++result, ++first)                    |
//    *result = *first;                                         ↓
//                         __copy(..., random_access_iterator_tag)
//                         __copy_d(first, last, result, distance_type(first));
//                                              |
//                                              |
//                                              ↓
//              for (Distance n = last - first; n > 0; --n, ++result, ++first)
//                      *result = *first;
////////////////////////////////////////////////////////////////////////////////
  iterator erase(iterator first, iterator last)
  {
    iterator i = copy(last, finish, first);
    // 析构掉需要析构的元素
    destroy(i, finish);
    finish = finish - (last - first);
    return first;
  }

  // 调整size, 但是并不会重新分配内存空间
  void resize(size_type new_size, const T& x)
  {
    if (new_size < size())
      erase(begin() + new_size, end());
    else
      insert(end(), new_size - size(), x);
  }
  void resize(size_type new_size) { resize(new_size, T()); }

  void clear() { erase(begin(), end()); }

protected:
  // 分配空间, 并且复制对象到分配的空间处
  iterator allocate_and_fill(size_type n, const T& x)
  {
    iterator result = data_allocator::allocate(n);
    __STL_TRY {
      uninitialized_fill_n(result, n, x);
      return result;
    }
    __STL_UNWIND(data_allocator::deallocate(result, n));
  }

// 分配空间并且拷贝一个区间的元素到新分配空间处
#ifdef __STL_MEMBER_TEMPLATES
  template <class ForwardIterator>
  iterator allocate_and_copy(size_type n,
                             ForwardIterator first, ForwardIterator last)
  {
    iterator result = data_allocator::allocate(n);
    __STL_TRY {
      uninitialized_copy(first, last, result);
      return result;
    }
    __STL_UNWIND(data_allocator::deallocate(result, n));
  }
#else /* __STL_MEMBER_TEMPLATES */
  iterator allocate_and_copy(size_type n,
                             const_iterator first, const_iterator last)
  {
    iterator result = data_allocator::allocate(n);
    __STL_TRY {
      uninitialized_copy(first, last, result);
      return result;
    }
    __STL_UNWIND(data_allocator::deallocate(result, n));
  }
#endif /* __STL_MEMBER_TEMPLATES */


#ifdef __STL_MEMBER_TEMPLATES
  // 初始化一个区间, 使用push_back()操作, 可能引发内存多次重新分配
  // 解决方案见
  // template <class InputIterator>
  // vector(InputIterator first, InputIterator last)
  // 我评注部分
  template <class InputIterator>
  void range_initialize(InputIterator first, InputIterator last,
                        input_iterator_tag)
  {
    for ( ; first != last; ++first)
      push_back(*first);
  }

  // This function is only called by the constructor.  We have to worry
  //  about resource leaks, but not about maintaining invariants.
  template <class ForwardIterator>
  void range_initialize(ForwardIterator first, ForwardIterator last,
                        forward_iterator_tag)
  {
    size_type n = 0;
    distance(first, last, n);
    start = allocate_and_copy(n, first, last);
    finish = start + n;
    end_of_storage = finish;
  }

  template <class InputIterator>
  void range_insert(iterator pos,
                    InputIterator first, InputIterator last,
                    input_iterator_tag);

  template <class ForwardIterator>
  void range_insert(iterator pos,
                    ForwardIterator first, ForwardIterator last,
                    forward_iterator_tag);

#endif /* __STL_MEMBER_TEMPLATES */
};

////////////////////////////////////////////////////////////////////////////////
// vector实现部分
////////////////////////////////////////////////////////////////////////////////

template <class T, class Alloc>
inline bool operator==(const vector<T, Alloc>& x, const vector<T, Alloc>& y)
{
  return x.size() == y.size() && equal(x.begin(), x.end(), y.begin());
}

// 字典序比较
template <class T, class Alloc>
inline bool operator<(const vector<T, Alloc>& x, const vector<T, Alloc>& y)
{
  return lexicographical_compare(x.begin(), x.end(), y.begin(), y.end());
}

#ifdef __STL_FUNCTION_TMPL_PARTIAL_ORDER

template <class T, class Alloc>
inline void swap(vector<T, Alloc>& x, vector<T, Alloc>& y)
{
  x.swap(y);
}

#endif /* __STL_FUNCTION_TMPL_PARTIAL_ORDER */

////////////////////////////////////////////////////////////////////////////////
// 重载赋值运算符
////////////////////////////////////////////////////////////////////////////////
//                  operator=(const vector<T, Alloc>& x)
//                                   |
//                                   |---------------- 是否是自赋值?
//                                   ↓
//              -----------------------------------------
//        No    |                                       | Yes
//              |                                       |
//              ↓                                       |------- 容量判断
//        return *this;                                 |
//                                                      ↓
//      -----------------------------------------------------------------
//      |x.size() > capacity()          | size() >= x.size()            | other
//      |                               |                               |
//      ↓                               ↓                               |
//  容量不足, 需要重新分配        容量足够, 只需要析构掉多余的对象             |
//  allocate_and_copy(         copy(x.begin(), x.end(), begin());       |
//      x.end() - x.begin(),   destroy(i, finish);                      |
//      x.begin(), x.end());                                            |
//  destroy(start, finish);                                             |
//  deallocate();                                                       ↓
//                     copy(x.begin(), x.begin() + size(), start);
//                     uninitialized_copy(x.begin() + size(), x.end(), finish);
////////////////////////////////////////////////////////////////////////////////

template <class T, class Alloc>
vector<T, Alloc>& vector<T, Alloc>::operator=(const vector<T, Alloc>& x)
{
  if (&x != this) {
    // 如果x.size() > capacity()那么就需要重新分配内存
    // 首先分配内存, 并将容器内原来的元素拷贝到新分配内存中
    // 然后析构原容器中元素, 调整内存状态变量
    if (x.size() > capacity()) {
      iterator tmp = allocate_and_copy(x.end() - x.begin(),
                                       x.begin(), x.end());
      destroy(start, finish);
      deallocate();
      start = tmp;
      end_of_storage = start + (x.end() - x.begin());
    }
    else if (size() >= x.size()) {
      iterator i = copy(x.begin(), x.end(), begin());
      destroy(i, finish);
    }
    else {
      copy(x.begin(), x.begin() + size(), start);
      uninitialized_copy(x.begin() + size(), x.end(), finish);
    }
    finish = start + x.size();
  }
  return *this;
}

////////////////////////////////////////////////////////////////////////////////
// 提供插入操作
////////////////////////////////////////////////////////////////////////////////
//                 insert_aux(iterator position, const T& x)
//                                   |
//                                   |---------------- 容量是否足够?
//                                   ↓
//              -----------------------------------------
//        Yes   |                                       | No
//              |                                       |
//              ↓                                       |
// 从opsition开始, 整体向后移动一个位置                     |
// construct(finish, *(finish - 1));                    |
// ++finish;                                            |
// T x_copy = x;                                        |
// copy_backward(position, finish - 2, finish - 1);     |
// *position = x_copy;                                  |
//                                                      ↓
//                            data_allocator::allocate(len);
//                            uninitialized_copy(start, position, new_start);
//                            construct(new_finish, x);
//                            ++new_finish;
//                            uninitialized_copy(position, finish, new_finish);
//                            destroy(begin(), end());
//                            deallocate();
////////////////////////////////////////////////////////////////////////////////

template <class T, class Alloc>
void vector<T, Alloc>::insert_aux(iterator position, const T& x)
{
  if (finish != end_of_storage) {       // 还有剩余内存
    construct(finish, *(finish - 1));
    ++finish;
    T x_copy = x;
    copy_backward(position, finish - 2, finish - 1);
    *position = x_copy;
  }
  else {        // 内存不足, 需要重新分配
    // 本实作中是按原内存2倍进行重新分配
    const size_type old_size = size();
    const size_type len = old_size != 0 ? 2 * old_size : 1;
    iterator new_start = data_allocator::allocate(len);
    iterator new_finish = new_start;
    // 将内存重新配置
    __STL_TRY {
      new_finish = uninitialized_copy(start, position, new_start);
      construct(new_finish, x);
      ++new_finish;
      new_finish = uninitialized_copy(position, finish, new_finish);
    }
// 分配失败则抛出异常
#       ifdef  __STL_USE_EXCEPTIONS
    catch(...) {
      destroy(new_start, new_finish);
      data_allocator::deallocate(new_start, len);
      throw;
    }
#       endif /* __STL_USE_EXCEPTIONS */
    // 析构原容器中的对象
    destroy(begin(), end());
    // 释放原容器分配的内存
    deallocate();
    // 调整内存指针状态
    start = new_start;
    finish = new_finish;
    end_of_storage = new_start + len;
  }
}

////////////////////////////////////////////////////////////////////////////////
// 在指定位置插入n个元素
////////////////////////////////////////////////////////////////////////////////
//             insert(iterator position, size_type n, const T& x)
//                                   |
//                                   |---------------- 插入元素个数是否为0?
//                                   ↓
//              -----------------------------------------
//        No    |                                       | Yes
//              |                                       |
//              |                                       ↓
//              |                                    return;
//              |----------- 内存是否足够?
//              |
//      -------------------------------------------------
//  Yes |                                               | No
//      |                                               |
//      |------ (finish - position) > n?                |
//      |       分别调整指针                              |
//      ↓                                               |
//    ----------------------------                      |
// No |                          | Yes                  |
//    |                          |                      |
//    ↓                          ↓                      |
// 插入操作, 调整指针           插入操作, 调整指针           |
//                                                      ↓
//            data_allocator::allocate(len);
//            new_finish = uninitialized_copy(start, position, new_start);
//            new_finish = uninitialized_fill_n(new_finish, n, x);
//            new_finish = uninitialized_copy(position, finish, new_finish);
//            destroy(start, finish);
//            deallocate();
////////////////////////////////////////////////////////////////////////////////

template <class T, class Alloc>
void vector<T, Alloc>::insert(iterator position, size_type n, const T& x)
{
  // 如果n为0则不进行任何操作
  if (n != 0) {
    if (size_type(end_of_storage - finish) >= n) {      // 剩下的内存够分配
      T x_copy = x;
      const size_type elems_after = finish - position;
      iterator old_finish = finish;
      if (elems_after > n) {
        uninitialized_copy(finish - n, finish, finish);
        finish += n;
        copy_backward(position, old_finish - n, old_finish);
        fill(position, position + n, x_copy);
      }
      else {
        uninitialized_fill_n(finish, n - elems_after, x_copy);
        finish += n - elems_after;
        uninitialized_copy(position, old_finish, finish);
        finish += elems_after;
        fill(position, old_finish, x_copy);
      }
    }
    else {      // 剩下的内存不够分配, 需要重新分配
      const size_type old_size = size();
      const size_type len = old_size + max(old_size, n);
      iterator new_start = data_allocator::allocate(len);
      iterator new_finish = new_start;
      __STL_TRY {
        new_finish = uninitialized_copy(start, position, new_start);
        new_finish = uninitialized_fill_n(new_finish, n, x);
        new_finish = uninitialized_copy(position, finish, new_finish);
      }
#         ifdef  __STL_USE_EXCEPTIONS
      catch(...) {
        destroy(new_start, new_finish);
        data_allocator::deallocate(new_start, len);
        throw;
      }
#         endif /* __STL_USE_EXCEPTIONS */
      destroy(start, finish);
      deallocate();
      start = new_start;
      finish = new_finish;
      end_of_storage = new_start + len;
    }
  }
}

#ifdef __STL_MEMBER_TEMPLATES

// 在指定位置插入指定区间的对象
template <class T, class Alloc> template <class InputIterator>
void vector<T, Alloc>::range_insert(iterator pos,
                                    InputIterator first, InputIterator last,
                                    input_iterator_tag)
{
  for ( ; first != last; ++first) {
    pos = insert(pos, *first);
    ++pos;
  }
}

template <class T, class Alloc> template <class ForwardIterator>
void vector<T, Alloc>::range_insert(iterator position,
                                    ForwardIterator first,
                                    ForwardIterator last,
                                    forward_iterator_tag)
{
  if (first != last) {
    size_type n = 0;
    distance(first, last, n);
    if (size_type(end_of_storage - finish) >= n) {
      const size_type elems_after = finish - position;
      iterator old_finish = finish;
      if (elems_after > n) {
        uninitialized_copy(finish - n, finish, finish);
        finish += n;
        copy_backward(position, old_finish - n, old_finish);
        copy(first, last, position);
      }
      else {
        ForwardIterator mid = first;
        advance(mid, elems_after);
        uninitialized_copy(mid, last, finish);
        finish += n - elems_after;
        uninitialized_copy(position, old_finish, finish);
        finish += elems_after;
        copy(first, mid, position);
      }
    }
    else {
      const size_type old_size = size();
      const size_type len = old_size + max(old_size, n);
      iterator new_start = data_allocator::allocate(len);
      iterator new_finish = new_start;
      __STL_TRY {
        new_finish = uninitialized_copy(start, position, new_start);
        new_finish = uninitialized_copy(first, last, new_finish);
        new_finish = uninitialized_copy(position, finish, new_finish);
      }
#         ifdef __STL_USE_EXCEPTIONS
      catch(...) {
        destroy(new_start, new_finish);
        data_allocator::deallocate(new_start, len);
        throw;
      }
#         endif /* __STL_USE_EXCEPTIONS */
      destroy(start, finish);
      deallocate();
      start = new_start;
      finish = new_finish;
      end_of_storage = new_start + len;
    }
  }
}

#else /* __STL_MEMBER_TEMPLATES */

template <class T, class Alloc>
void vector<T, Alloc>::insert(iterator position,
                              const_iterator first,
                              const_iterator last) {
  if (first != last) {
    size_type n = 0;
    distance(first, last, n);
    if (size_type(end_of_storage - finish) >= n) {
      const size_type elems_after = finish - position;
      iterator old_finish = finish;
      if (elems_after > n) {
        uninitialized_copy(finish - n, finish, finish);
        finish += n;
        copy_backward(position, old_finish - n, old_finish);
        copy(first, last, position);
      }
      else {
        uninitialized_copy(first + elems_after, last, finish);
        finish += n - elems_after;
        uninitialized_copy(position, old_finish, finish);
        finish += elems_after;
        copy(first, first + elems_after, position);
      }
    }
    else {
      const size_type old_size = size();
      const size_type len = old_size + max(old_size, n);
      iterator new_start = data_allocator::allocate(len);
      iterator new_finish = new_start;
      __STL_TRY {
        new_finish = uninitialized_copy(start, position, new_start);
        new_finish = uninitialized_copy(first, last, new_finish);
        new_finish = uninitialized_copy(position, finish, new_finish);
      }
#         ifdef __STL_USE_EXCEPTIONS
      catch(...) {
        destroy(new_start, new_finish);
        data_allocator::deallocate(new_start, len);
        throw;
      }
#         endif /* __STL_USE_EXCEPTIONS */
      destroy(start, finish);
      deallocate();
      start = new_start;
      finish = new_finish;
      end_of_storage = new_start + len;
    }
  }
}

#endif /* __STL_MEMBER_TEMPLATES */

#if defined(__sgi) && !defined(__GNUC__) && (_MIPS_SIM != _MIPS_SIM_ABI32)
#pragma reset woff 1174
#endif

__STL_END_NAMESPACE

#endif /* __SGI_STL_INTERNAL_VECTOR_H */

// Local Variables:
// mode:C++
// End:```