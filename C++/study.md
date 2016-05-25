1. 
全局变量可以定义在被多个.c文件包含的头文件中吗？<br>
答：如果是static是可以的，因为每一个源文件会自动编译为**自己的局部全局变量**；但是如果是普通的，那么会造成**重复定义**
1. 
类中public与private函数可以同名吗？<br>
答：不能，
1. 
父指针指向孩子对象，调用普通函数与虚函数的区别？<br>
答：普通函数调用父亲自己的，虚函数才会调用孩子的。
* 
模板Template用到class、typename这两个关键字，那么他们相同吗？<br>
答：在C++刚开始引入模板时，class表示类，所以直接被用来表示引用的类型```template<class T>```；但是为避免class在两个地方使用造成误解，所以引入typename关键字来表示后面的符号为类型。所以class、template的作用是相同的。```template<class T>```与```template<typename T>```等价。
* 
auto



[返回目录](README.md)